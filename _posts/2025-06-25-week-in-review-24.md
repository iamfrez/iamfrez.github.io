---
layout: post
title: Week in Review - 24
description: "A week in review of my bug bounty work."
category: blog
---

To revive the blog I will begin a Week in Review series, where I write some notes about my previous week doing bug bounty work, with some ideas, notes and reflections of the process and what I’ve done. 

I used to do bug bounty occasionally, with very good results, so now I decided to focus a lot more of my time on it complementing my pentesting job. 

An important thing that I want to talk about before running the weekly stats, is that I am taking an approach based on time spent and not on vulnerabilities found. Initially, I though a lot about how I was going to measure the work I do. I thought about finding a vulnerability a day, then one per week… But then I realize that those are variables that I cannot control. The only thing that I can control is the time I spend working on a specific progrma, and of course the selection of it.

So, my approach for bug bounty programs is the following:

1. I decide on a program to hack based on the feedback I get from Hackerone regarding the average time for responses, payments and overall maintenance of the program. If it’s well maintained, clear and the company takes it seriously, I might give it a chance. If these variables are a bit shady or inconsistent, I move on and pick another one.
2. If the variables are right, then I evaluate the scope and see if it’s interesting. I’m not too picky though. If the scope is a bit interesting, has some functionalities I’m into such as tenants, authentication mechanisms and different roles, I will focus on it.
3. And lastly, how much are they paying for critical issues. If I’m going to spend time hacking them, I want to make sure it’s well rewarded.

So far, I have found at least one low issue in all of the programs I hacked on.

### Bug Bounty Time Spent

I decided to hack on this private program because is pretty new and has almost no reports. Scope is small but interesting, so I gave it a go and allocated 30 hours for this one to begin with.

**Weeks:** 23 & 24

Week 23 I spent around 9 hours hacking on the program.
Week 24 I spent 16h30m hacking on it and found 2 vulnerabilities.

**Total time:** 30 hours

**Time spent so far:** 25h30m

**Findings:** 3

**Status:** One paid, two accepted, open.

### Notes and Conclusions

I’ve been thinking a lot about the importance of dedicating the most amount of time working on the important things, on the things that matter, to really get results. I might do a post about this soon.

As always, I enjoy a lot digging deep into js code to understand the functionalities, it’s my favorite part when identifying the functionalities available and how they interact with the back-end.

However, don’t assume that all endpoints are available or listed in js files. Some of them are meant to be called from APIs and are not directly visible from asset files. Found two sweet vulnerability this week just by expanding my knowledge about the application from other places besides JavaScript files.

Check-the-docs. To really understand how a product works, read and understand the documentation, even when it might seem boring or pointless at times. You might identify obscure or untested functionalities by reading what developers and product people have written. This reminded me about the words of rhynorater: “become the world expert on that application you’re hacking”. 
