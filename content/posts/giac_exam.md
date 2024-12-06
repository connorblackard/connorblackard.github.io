+++
title = "How to Pass a SANS Course in 90 days."
date = "2024-03-26T09:08:41-06:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Connor Blackard"
cover = "/images/sans/cover_photo.jpg"
keywords = ["sans", "giac", "msise", "certifications"]
description = "I decided to take some time to write about my process for approaching courses in the MSISE Program at SANS but this is relevant for anyone taking any SANS course. I also put some links to my index template, course management tracker, and Python script to extract all the slide titles and duration to a CSV."
showFullContent = false
readingTime = true
hideComments = false
+++
## Introduction
I often see individuals in the [SANS.edu](sans.edu) Slack forum wonder where to begin for their first few SANS courses or how to tackle the indexing and studying process for the GIAC exams. I am currently in my seventh class in the MSISE program and thought I'd take some time to write about what works for me and how I approach each course. While I know there are a lot of resources out there on how to prepare an index (huge shoutout to [Lesley Carhart](https://www.linkedin.com/in/lcarhart/) for the widely beloved ["Pancakes Method"](https://tisiphone.net/2015/08/18/giac-testing/)) there aren't a lot of good resources for how to manage time across several months to soak up thousands of pages of information. 

SANS is known for some of the top technical training in the cyber security industry but with that also comes a steep price tag. As individuals are paying for these courses out of pocket, with student loans, or even having their companies foot the bill, it only makes sense to put in the effort and truly get your money's worth.


This article is going to cover my steps from the minute I book a course all the way through when I put the badge on my LinkedIn profile. I'll be covering:

1. Mindset
2. Allocating Time
3. Preparing a Course Tracker
4. Taking the Course/Preparing an Index
5. Practice Exams
6. Passing the Exam

## Mindset
Getting into the proper mindset is one of the most important things you can do before you take a course. Given this course will be a portion of your time for the next several weeks, you want to ensure you are ready for what lies ahead. One of the first things I do before a new course is look up the course description on the SANS.org website. Each course has a page and there is a brief description and overview. You should review this before choosing a course and after purchasing a course so you know what you will be covered as well as what won't be covered. Interesting things I look for in the course description include skills, tools, topics, and technology requirements.

In addition to reviewing the course description, you may also have a corresponding GIAC exam with your course. I found it helpful to search the exam name on LinkedIn or Twitter to see what people who have recently taken it thought about it.

Lastly, it may be helpful to define what you are hoping to get out of the course and any success criteria you have. My success criteria always revolve around additional knowledge and understanding in the field. To me, the most important part of the entire experience is the course itself and the least important is the certification. While these certifications are highly sought after by recruiters and hiring managers, there is a tendency to equate knowledge to certifications held and it cannot be further from the truth. That said, it's a fact of life that these are on job postings and it's a necessary evil to prove you are proficient in the material.

## Allocating Time
After getting in the proper mindset for the course, my next step is to allocate time to do the course. I begin by figuring out how long I have to take the course and when I have to be finished. Since I am doing this as part of a Master's program, I treat this like M-F schedule. I know that every day I can dedicate one hour to school before I begin work. This usually takes place for me between 7-8 am each day. But I know that there will be days that I am not able to do school work such as days I am traveling, on PTO, or on holidays. With this information, I enter all available dates into a spreadsheet and figure out what days are school days and what days aren't. From here I can get a total on how many days I will have for the course.


{{< figure src="/images/sans/course_tracker.png" style="border-radius: 8px;" caption="Example Course Schedule" captionPosition="Center" captionStyle="color: white;" >}}

After I have identified how many days I will have, I can set goals for each day and track milestones. It's important to point out that while I spend one hour on school each day, the hours remaining only go down by a half hour every day. This is because each day is a combination of watching OnDemand videos, building my index, and reading/highlighting the books. More on that in a few sections.

After figuring out how many days are available, the next step is to determine what slides to cover each day. I wrote a [Python script](https://github.com/connorblackard/SANS-Slide-Titles-to-CSV) this past year that will take the JSON output from the SANS OnDemand Player and convert it into a CSV file that you can put into your course tracker on the "Slides with Lab Time" sheet. This will list each slide along with the book, section, slide number, video title, and duration. This allows you to get granular in your study plan and say "It's day 15, I need to do these 15 slides today".

A key advantage of this is that you can see how much time you spent on this course throughout the period. It is easy to multiply your course days by one hour each day and figure out how much time you put into continuing education. I ensure this is tracked at work, reported to my manager, and brought up in professional development chats/evaluations.

## Preparing a Course Tracker
As you have seen in the above screenshot, I use Google Sheets/Excel heavily to track my progress and stay organized while taking courses. I have altered and prepared an example of my index template and course tracker and made it available [here](https://docs.google.com/spreadsheets/d/1u4qPWuFuW33xGp9qY98jfR_mCvQ3_vPLCMP0mmYedcg/view?usp=drive_link). You can use this in either Google Sheets or Excel. I have sheets titled:

- Index - Entries of key concepts
- Index Supplements - Additional items that I need to put into my final index (mostly screenshots and cheat sheets)
- Labs - A list of labs, page numbers, and key tools/commands used
- Course Progress - A color-coded breakdown of each book and chapter
- Slides with Lab Time - Discussed above
- Schedule - Discussed above

Ultimately, this is just my method and please do tailor this for what works best for you.

## Taking the Course/Preparing an Index
Now we have arrived at the actual course portion. Usually, everything above takes me one to two hours. I try and knock these tasks out while the books are shipping so I am not wasting time that can be spent elsewhere. While the preparation to get to this point may seem excessive, it truly will pay off when you finish the course on time and ace the exam.

A few days after you have placed your course order, a large box of books will come to your doorstep. These books will be the most valuable resource you will have during the entire course. Everything you will be tested on is within the covers of these books. Your goal with an index is to be able to quickly sift through the books to find information. In my opinion, an index should not contain any information (other than cheat sheets). It should only contain the location of where to find information.

Other key items that are a must-have for every course are [highlighters](https://a.co/d/1WbEqo2) and [Post-it tabs](https://a.co/d/cS6vJl8). You can get by without these but at the point, you are taking a $4-8k course, it's worth it to spend a few more bucks and do things right.

For each book, I put a sticky tab at the top to assign the book a color, and sticky tabs on the side to assign each chapter a color. During the exam I look at my index and think "I need to find the red book, blue chapter, page 52" and this speeds things up quite a bit.

{{< figure src="/images/sans/book_with_tabs.png" style="border-radius: 8px;" caption="Book with Tabs" captionPosition="Center" captionStyle="color: white;" >}}


My routine is to watch the video (usually at 1.2x or 1.5x speed), read/highlight the corresponding page in the book, make an index entry, and repeat. This ensures that I consume all the knowledge for the topic at one time and let it sink in. I only highlight things that I think may come up on the exam or that will be useful for me later. While there is a lot of good information in the textbook, sometimes there is some fluff that after reading it once, I won't ever need to come back to.

Good index entries are the key to efficiency in finding content. Some examples of good entries are:

- Routers, Threats
- Routers, Protocols
- Routers, BGP
- VLAN, Private
- Private VLAN
- PowerShell: Get-ChildItem
- PowerShell: Write-Host
- Tool: netcat
- Person: Steve Jobs

I list many different ways as I may think about it during the exam. I also start broad and then narrow down with each comma. It is okay if you have multiple entries per page. I put them in a second column, separated with semicolons, and gave them their column later. Try and group items whenever possible such as commands, tools, or people. It's a lot easier to find one name in a list of twenty other names instead of one name somewhere in ten pages. 

{{< figure src="/images/sans/index_example.png" style="border-radius: 8px;" caption="Index Example" captionPosition="Center" captionStyle="color: white;" >}}


As I complete the labs I have a sheet that contains the name, page numbers, and key tools/commands used. Once again, if I need information, I want to be using the book, not my index so it just has to have enough to jog my memory and get me to the right place.

Once you have completed the course and all labs, it's time to prune down your index into something you can fit into a two-column word document. I included examples of the pruning process and comments on each sheet. I think the Pancakes Method does a better job explaining that than me so I will point you there. As long as you get down to a color-coded book/page number and term, you should be good. Here is a [link](https://docs.google.com/document/d/1KmIHKMMAC8EK9LEBaaCQNz6Kk5EF4uPH/view?usp=sharing&ouid=110892441845319043427&rtpof=true&sd=true) to my template.

{{< figure src="/images/sans/example_term_list.png" style="border-radius: 8px;" caption="Example Index Term List" captionPosition="Center" captionStyle="color: white;" >}}


I put all my index materials into a Word document to format and turn into a PDF. I have this bound and printed at my local FedEx Kinkos. The cost comes out to be $15-30 depending on the number of pages. I usually go with spiral bound and have them put a nice clear cover on it.

One last note on sharing indexes. I choose not to share my indexes and instead share the method. My index is built around how my brain works and how I will remember things during the test. I don't want to be blamed when someone fails a test because their brain works differently than mine. Also, I put screenshots of the textbooks in the back of my indexes so sharing that would be against SANS rules. My goal is to teach people to fish, not give them fish.

## Practice Exams
Practice exams are one of the best resources to assess if you are ready for the real exam. I suggest you always take one before you take the real exam. For SANS.edu students, you usually get two practice exams with each course. I have never needed more than one per exam and I largely attribute that to my upfront legwork with the course material and index creation. Every so often I see something online where people say they take one practice exam before the course to see where they are and take the second one after the course. I cannot stress this enough, that is one of the worst uses of a practice test I have ever heard of. Please don't do this. Just make your index, get it ready, and then use that to take the practice test. When you see questions you will be in one of a few situations, here is what you should do for each:

You know the right answer with 100% certainty - Submit the answer.
You think you know the right answer with 50% certainty - Take a minute, consult your index, and see if you can increase your certainty. If it takes too long, skip it and come back to it at the end.
You have no idea and it'll be time-consuming to find the answer - Skip and come back to it at the end. Sometimes you'll stumble across the information when researching other questions.

You have quite a bit of time for the exam and if you don't spend a lot of time on questions in scenario 1, you can dedicate more time to labs and scenario 2 and 3 questions. Quick back-of-the-hand math is 240 minutes for 100 questions. That's 2 minutes and 24 seconds per question. If you knock out a bunch of easy questions and quick wins, you can even bump the time up to 4-5 minutes each for the hard questions.

Treat your practice exam like your real exam. Only use your books and index. This way you will know if you are truly ready to test. All the information needed to get 100% is in the books. If you miss questions, read the explanations and review your index. Try and figure out if you just weren't familiar with a term or if something was missing from your index.

The rule of thumb is that you are ready to test if you get over 80% on the practice exam. Because of this rule of thumb, I've never taken a second practice exam. I usually give mine away on the GIAC mailing lists or Slack to someone also taking the course.

## Passing the Exam
The night before exam day comes, I prepare my office. For me, this includes unplugging my TV and Alexa, clearing off my desk, removing extra monitors, and laying out my two forms of ID. I prefer online testing due to the convenience factor but not everyone does. I have only had one issue come up and it was acceptably resolved within 30 minutes (didn't lose any exam time). If you took your practice exam like a real exam, this should be just the same. You are given one break if needed. I don't take it but I usually wrap exams up in around two hours. If I went longer than that, I would probably be using the breaks. After finishing the exam you are immediately notified of your score and shown how you did in each section. After you pass, the last thing to do it go to [credly.com](http://credly.com/) and add the badge to your LinkedIn profile and resume.

{{< figure src="/images/sans/resume.png" style="border-radius: 8px;" caption="Resume with GIAC Certifications" captionPosition="Center" captionStyle="color: white;" >}}

{{< figure src="/images/sans/linkedin.png" style="border-radius: 8px;" caption="LinkedIn Profile with Badges" captionPosition="Center" captionStyle="color: white;" >}}

## Conclusion
In conclusion, I think that SANS courses are some of the best available training for cyber security. They are pricey but worth it in my opinion. I am fortunate to have an employer who promotes training and continual education and hope others do too. While this was a glimpse at my process, it is by no means a requirement or best practice. It is just what works for me. Hopefully, this can be of value to others and inspire you to figure out your way or adapt this way to work for you.