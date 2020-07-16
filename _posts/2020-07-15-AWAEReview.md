---
layout: single
classes: wide
title:  "Red-Teaming: Offensive Security Advanced Web Attacks and Exploitation with 2020 Updates (AWAE 1.5)"
---

Review of the AWAE and its Newest Updates!

## Notes about the AWAE 1.0 released in 2019
I always wanted to do a quick review of OffSec’s AWAE and OSWE certification and review the material presented, and now that they have added 3 new sections for an additional $99 I thought that it would be a perfect time to revisit the course and dive into its newest updates.

Let’s start with the base course. Before this course, I thought that I was becoming a web testing expert. I already had OSCP and OSCE, completed well over 100 web exercises on PentesterLab, and had been working as a web application assessor in the field for a few years. However, day one of this course taught me the major difference between being a competent web ASSESSOR versus a web exploit DEVELOPER. In the world of assessments, you kick off a scanner, manually review findings, and then spend the rest of the allotted time of an assessment (maybe 3 days?) manually trying to prod the application further for XSS or SQLi. That being said, the course immediately outlines the need for manual source code review to find the things that scanners won’t. Don’t think that I’m saying that scanning isn’t important. I am just saying that the next level is reviewing the code itself.

Even though I completed the certification last year, I was still learning new things every time I went back to the material. Do I understand how a JSP actually renders content to the page? Do I understand context in a NodeJS environment? Do I understand ```function``` versus ```Function()```? Web exploit development requires that you finally stop being scared about learning programming and jump headfirst into all of the major languages such as PHP, NodeJS, Java, C#, and all of the popular frameworks associated with them. Disclosure, I am still no expert, but I have really focused on NodeJS and JavaScript in general since this course and am really glad that I have a much better grasp on the underlying technologies and how they work as opposed to just putting ```../../../etc/passwd%00``` whenever I see ```.*\.php\?file=``` and hoping for the best.

The greatest assets of the course are the Extra Miles. These Extra Miles are not like OSCP/OSCE where the content is more or less directly in line with the course material. The course really makes you dig deeper and try to get a better understanding of the technologies and their workflow. I would say that I spent more time on the Extra Miles than I did anything else in the course, and it really paid off. If you only do the exercises and skip the Extra Miles in the course, then you will probably think that the course is a little boring and basic. So, take the building blocks that the course presents, and use them as a foundation to go the Extra Mile!

## AWAE Updates
As mentioned above, I have been wanting to go back through the material recently as I know there is still more that I can glean from it in terms of methodology and code comprehension. Once I was notified that alumni were eligible for a $99 upgrade, I thought I would take the opportunity to review the old stuff in addition to the new.

I got the materials tonight and have been going through the PDF as I wait for my new lab time to start. I’m sure that I will track down the vulnerable source code and spin the apps up myself like the original material, but I will use the lab right now since it came with the $99 update and I am short on time. All I can say is that I feel like a n00b all over again. Once again, I am not a source code review master. Even after completing the original material and obtaining the OSWE the additional material is really the only content that I have found on the Internet that actually explains the programming and computer science concepts behind the material as opposed to being expected to understand every property is on an object beforehand.

The new materials dig into Server-side Template Injection, XML External Entity Processing, and some command injection over Web Sockets. Being that it is a course on source code review, you also get a nice dose of remote debugging techniques that complement all of the debugging techniques shown in the original course. As a side note, let's just say that I feel bad for not being up to speed on SSTI even though it has been discussed for the past few years. I may or may not have a specific app in mind that I recorded ```'\{\{7+7\}\}=49'``` as an Angular Cross-Site Script when I should have probed it further for SSTI :/ Funny enough, the Liquid templating engine used by Jekyll also threw an error on this very line when using the '+' operator without the escaping '{' and '}'. I'm sure that doesn't mean anything, but it just illustrates strange behavior when templates are being used. 

{:refdef: style="text-align: center;"}
![](/assets/images/AWAE/ssti.jpg)
{: refdef}
{:refdef: style="text-align: center;"}
*I doubt this means anything, but it might be worth playing around with...*
{: refdef}

I personally believe that the AWAE is the second hardest OffSec course just under the Advanced Windows Exploitation (AWE/OSEE) course. Sure, Penetration Testing with Kali (PWK/OSCP) and Cracking the Perimeter (CTP/OSCE) are really fun, but AWAE pushed me harder than either of those. The new material looks to be no different.

## Final Thoughts
The original AWAE was worth the time and money if you completed all of the exercises, Extra Miles, and went above and beyond. If you just sit back and follow the lessons with no intention of understanding the code, then you probably won’t get much from the course. However, if you want to begin to visualize the code behind the app that you are blindly scanning, then this course is a must. 

The updates nicely complement and add to the original content. If you haven’t done AWAE, then the added content really sweetens the deal. If you already have OSWE and received a good deal on the upgrade, I can say that by my preliminary review of the additions that it is absolutely worth it. The only real competitor that I have found for source code review is the badge on PentesterLab, but that badge still needs some ironing out in terms of completability and cohesion. Perhaps I can talk about that badge in a future post. 

I will be working on completing the new content over the next 30 days or so and will update this post as needed, but so far I expect that my initial impressions will hold up.