---
layout: post
title:  "Making closed source software open source"
date:   2018-06-21 08:00:00 +0100
tags: [Closed source, Open source, Story]
author: "Roel van de Water"
---
I want to kick off this blog with a less technical article, but certainly programming related. This article is about making previously closed source software open source. It shows you a set of the different decisions you have to make and what steps you have to take to make your code open source. This article is based on my personal experience, and your steps might be different or you might follow a whole different road.

## My own story
A couple of years ago, I've been developing my own two-factor authentication (2FA) application for the Microsoft Store, when I had a Windows phone myself and there was no good alternative. I've spent months on developing a good app and gained quite some users and feedback in the following months. I even setup a nice website to show off my app and to show the awesome features it offered.

After a while, I switched from Windows phone to another platform. And, as you might have experienced yourself, you end up with a project that you're not using your yourself anymore. My app was free to download and didn't contain any ads or trackers. So, basically, I didn't make any money from this app. That's not a problem if you're also happily using your app yourself, but if you're not making any money from your development and you're not even using your own app, then why would you spend time on developing this app?

This was something I've been struggling with for quite a while. My project was abandoned by myself and I didn't make any money from it. I found out that I had still hundreds of active users every day. This made me feel myself quite selfish, because I knew I would let those people down when I would just permanently stop development and remove it from the Microsoft Store.

I've played a lot with the idea to someday improve the legacy codebase, but I never really took action to actually do it. Am I really selfish because I don't want to spend a lot of my valuable time on development for something I'm not even using myself, without making any money? No. That's something that took a while for me to realize and accept.

Eventually, I came to the point where I accepted the faith of my app and decided to make it open source. I was kind of forced to make the decicion though, because the domain name I bought was (again) about to expire and I didn't want to spend even more money on this. In my app, there were a couple of references to this domain name, and I didn't want to let my valuable users completely down with serving them an app with dead links. It felt like the least I could do.

## Take action
When you've decided that you want to make your source code open, there's a couple of steps that you have to take. Please note that those steps are based on personal experience and that your road to open source software might be (slightly) different.

### Choose a platform to share your code
This step is easier for some developers. If you have always, like me, had your source code in an online VCS, you simply have to change the visibility of your repository from private to public. That's exactly what I did.

If you haven't used a VCS for your codebase before, this might be a good time to reconsider this decision. Putting your codebase in a VCS gives you a lot of benefits, which I'm not going to discuss here.

Choosing the platform where you want to share your code is quite important. It serves as the first place where interested people will find your code. These days anyone can setup a free and public repository using a service like GitHub, Bitbucket or GitLab, so that might be just the solution for you.

### Choose a license
Choosing a license was a bit harder for me. At least, that's what I thought it would be, before diving into this subject. There was one thing I knew for sure: I don't want people to make money from my source code.

Even though it seems likely to happen that someone else is going to earn money from your source code, the chances are not so big it's actually going to happen. Why would someone pay money for an app, even though they can get the exact same functionality without having to pay for it? This paid app is not the only copy of this compiled source code, after all.

And why would you not allow someone to make money for extra functionality they created themselves? If someone could improve your code or add some extra features to it, let them make money of it, if they want so. When I realized this, the step to make my app open source, became a whole lot easier.

A good website that can help you choosing a license for your source code is [choosealicense.com](https://choosealicense.com). This website sums up the most common licenses as well as their characteristics.

A good way to attach your license to your codebase, is to create a `LICENSE.txt` (or simply `LICENSE`) file in the root of your codebase.

### Setup a proper README file
Setting up a proper `README` file is almost essential. It helps the people that are interested in downloading, sharing or contributing to your code. You might want to give a little description of what the source code is, what it does and perhaps how it works. You can use the `README` to tell people what you expect from your open source code as well, which I'll discuss later in this article.

### Be clear about what you expect
Being clear about what you expect from your open source project is very important. It can save people a lot of time. For example, if you don't want people to create pull requests in your repository, be clear about this. This way you can prevent people from creating them and hoping them for their code to be merged. It doesn't matter whether it makes sense or not, it's your project and you make up the rules! The `README`file is the perfect candidate for these kind of things, as it's usually the first thing someone sees or reads when you visit your (online) repository.

### Update your current codebase
This might be or not be the case for you, but sometimes it's necessary (or at least a nice thing to do) to update your current codebase. It might make sense to inform people that you have made your app open source, so they can look into the source code, or maybe even contribute.

When you tihnk of updating your current codebase, think of updating references to domain names, licenses, and so on.

In my case, it meant updating the 'About' page, informing people that it's now an open source app, and I changed the official domain name to be the one of the public repository, so that people who are interested can go to the official project repository easily.

## Wrapping up
It might sound like a lot of work make your previously closed source code open source. It's not. For me, I spent the most time deciding whether I should make my app open source or not. The rest of it was quite simple.
