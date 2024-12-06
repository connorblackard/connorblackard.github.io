+++
title = "Is My Homelab Compromised?"
date = "2024-04-11T10:22:35-06:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Connor Blackard"
cover = "/images/homelab/cover_page.png"
keywords = ["homelab", "securityonion", "cybersecurity", "network security", "zeek", "suricata"]
description = "I recently conducted an experiment exploring endpoint and network analysis on one of my homelab devices. I got to use ClamAV, Zeek, Suricata, and Security Onion to try and prove a device isn’t compromised."
showFullContent = false
readingTime = true
hideComments = false
+++
## Introduction
A few months ago in a conversation with someone about homelabs, I mentioned that I have a small homelab that includes a Lenovo Mini PC that runs Proxmox. By most accounts, this is a very modest homelab that allows me to spin up test machines as needed for whatever I am studying at the time and a Pi-Hole DNS AdBlocker. I guess the individual felt compelled to tell me that Lenovo had been known for backdoors and rootkits and I should save myself now and get rid of the entire system. Luckily as the CIO and CISO of my home network, I was able to dismiss them and say I consider the vendor and device to be a low risk to me, in my environment, with my usage. However, the thought crossed my head, what if this was a business leader who read a headline and came to inquire about potential risk? If that was the case, I may have to produce a more detailed answer than "It's fine" or "Trust me bro". With some extra time, I decided I wanted to investigate this and see what I could come up with. 

## Threats
The first thing I did was consider possible attack vectors. I identified there are two main categories of threats that could happen, physical or digital. The main physical threats to the device are theft and environmental threats (tornados, busted pipes, inquisitive children). The controls for the threat of theft are locking doors, 24x7 security cameras, and two vicious attack dogs.


{{< figure src="/images/homelab/attackdogs.jpg" style="border-radius: 8px;" caption="Vicious Attack Dogs" captionPosition="Center" captionStyle="color: white;" >}}

For the environmental risks, the natural disaster risks have been transferred to the insurance company and the children risk will have to be accepted.

With the physical threats out of the way, we can move to the digital threats. In my mind, any digital threat would have to have some visibility on either the endpoint or the network. Malware would either be communicating to a C2 server or a backdoor would be present that would allow an attacker to trigger hidden functionality from the outside (similar the the recent XZ Utils backdoor). I am not as concerned about an attacker triggering a backdoor because the device is not internet-facing. In that scenario, an attacker would have to already have internal network access to even make use of such a backdoor. My testing plan was to scan the endpoint with antivirus and monitor network traffic for a few days and review.

## Testing
To start with the endpoint, I used ClamAV to scan the system. This is a free and open-source antivirus scanner that supports Windows, Linux, and macOS. Since Proxmox is Debian under the hood, I was easily able to install and run the tool.

{{< figure src="/images/homelab/install_clam.png" style="border-radius: 8px;" caption="Installing ClamAV" captionPosition="Center" captionStyle="color: white;" >}}

From here I ran the tool against every file on the disk. This was a lengthy scan but it ran in the background and I came back to it about 30 minutes later.

{{< figure src="/images/homelab/running_clam.png" style="border-radius: 8px;" caption="Running ClamAV" captionPosition="Center" captionStyle="color: white;" >}}

{{< figure src="/images/homelab/clam_summary.png" style="border-radius: 8px;" caption="ClamAV Scan Summary" captionPosition="Center" captionStyle="color: white;" >}}

As expected, the scan came back with no findings.

From here I moved into the network analysis which I figured would be the more intensive process. I have a Ubiquiti Router at home and lucky for me, it has a large solid-state drive and comes installed with tcpdump. I decided to run tcpdump for 48 hours to collect network traffic to and from Proxmox. I will note here that I only collected traffic to and from the hypervisor itself, I did not collect all traffic on the port that would include the VMs. This was a decision to keep the packet capture size reasonable in addition to only testing if the Lenovo device was beaconing out, not the random VMs. 

{{< figure src="/images/homelab/tcpdump_command.png" style="border-radius: 8px;" caption="tcpdump Command" captionPosition="Center" captionStyle="color: white;" >}}

Two days later I came back to a 232 MB packet capture of 11,796 packets. From here I had two routes I could go down to analyze this capture. The first would be the use of Wireshark to view the capture and rely on display filters and the statistics menu options (such as Protocol Hierarchy and Conversations) to quickly highlight items of interest. The second would be to use a tool such as Zeek to process the data into nicely formatted logs. While I did look at the capture as described in Wireshark, I created a Security Onion VM (on Proxmox) to process the PCAP. The added benefit of this is that it also ran Suricata on it. This is more in line with how an enterprise would handle a large amount of data with a Network Security Monitoring (NSM) platform.

{{< figure src="/images/homelab/pcap_upload.png" style="border-radius: 8px;" caption="Security Onion PCAP Upload" captionPosition="Center" captionStyle="color: white;" >}}

I decided to manually review the logs instead of using the Security Onion Console and Kibana. I did this because I knew I could confidently analyze this using the command line. If I had to search or do any additional research, I could pivot into Kibana for additional capabilities. A first look at the Zeek logs revealed quite a few items.

{{< figure src="/images/homelab/zeek_logs.png" style="border-radius: 8px;" caption="Zeek Logs" captionPosition="Center" captionStyle="color: white;" >}}

I went through all of these but the ones that I'll cover here are conn.log, dns.log, http.log, files.log, and ssl.log. While the others are valuable logs, they didn't have anything super interesting in this case.

Also worth noting is that I had to use jq instead of zeek-cut in the below commands. This was because Security Onion outputs zeek in JSON format instead of TSV format. I found this annoying as I prefer zeek-cut but between Google and a [cheatsheet](https://gist.github.com/olih/f7437fb6962fb3ee9fe95bda8d2c8fa4), I survived.

The first log I looked at was the dns.log. This found all the DNS requests made from Proxmox. I did expect to see some activity here primarily because I ran some updates during the middle of the packet capture (to make sure it wasn't going to be too boring).

{{< figure src="/images/homelab/dns_logs.png" style="border-radius: 8px;" caption="dns.log Output" captionPosition="Center" captionStyle="color: white;" >}}

It looks like all of the DNS queries were related to updates of some sort. Most of the updates are related to Debian and Proxmox. I did have to research what turnkeylinux.org was but then I remembered that Proxmox offered LXC containers, some of which are from turnkey. I had used this feature in the past so I am guessing it was an update to either the container lists or a container that is on the system, either way not a threat. The last item I had to research was the osuosl.org domain. Seeing this, I thought an ftp URL was weird but it turned out to be a university hosting an open-source mirror.

Next, I looked into files.log. This would let me see what Zeek detected as being downloaded. Based on the URLs above, I expected a lot to be related to updates.

{{< figure src="/images/homelab/files_logs.png" style="border-radius: 8px;" caption="files.log Output" captionPosition="Center" captionStyle="color: white;" >}}

As I expected, a majority of the files were update package related. The rest of the file types were also not found to be threats. 

Next, I reviewed the http.log file to see what URLs were being hit. I have a good idea of the domains but since package managers often use port 80, I would be able to see additional details including the full URLs being requested.

{{< figure src="/images/homelab/http_logs.png" style="border-radius: 8px;" caption="http.log Output" captionPosition="Center" captionStyle="color: white;" >}}

This paints a good picture of the network traffic and appears to line up with the above findings. 

Next, I reviewed the conn.log file. Here I was looking for what ports and services were being used. 

{{< figure src="/images/homelab/conn_log.png" style="border-radius: 8px;" caption="conn.log Services Output" captionPosition="Center" captionStyle="color: white;" >}}

{{< figure src="/images/homelab/conn_log_port.png" style="border-radius: 8px;" caption="conn.log Ports Output" captionPosition="Center" captionStyle="color: white;" >}}

I found it unusual that there were entries for ports 12 and 1168 in the logs. These entries corresponded with the 'null' service entries. I went to both Wireshark and tcpdump to try and find those packets but could not. Ultimately, I trust tcpdump as the official source of truth and if that could not find the packets, I am not convinced they exist. I chalked this up to a Zeek error but will probably try and investigate further by rerunning Zeek, this time in a docker container (with my preferred TSV format). For right now I don't consider this to be a threat. Other interesting things in the ports list were NTP(123/UDP) and the Proxmox WebUI (8006/TCP). I did note that there were 71 SSL packets but only 69 Proxmox WebUI packets. This meant that two packets used SSL that went outbound. These corresponded to turnkey Linux based on the SNI name.

{{< figure src="/images/homelab/ssl_log.png" style="border-radius: 8px;" caption="ssl.log Output" captionPosition="Center" captionStyle="color: white;" >}}

The last thing I did was examine the Suricata file to see if any alerts were triggered. The file was empty indicating no signatures matched. Following this, I felt I had a good understanding of the network traffic sent to and from the system over the testing period.

## Conclusion
Ultimately, I feel like now I have a tested process and documentable data to say that this device does not appear to be compromised. This backs up my initial stance of it being a low risk while also having more substance than 'Trust me bro'. I am sure that there are additional tests I could have run and ways that stuff could still but undetected but this is good enough for me and I feel good enough to present as a response that due diligence has been done. Overall it was a fun experiment that took a couple of hours and let me dive into some technologies in ways I don't normally get to. I'd love to hear from others if you had something you would have done differently or how you would have approached the problem.