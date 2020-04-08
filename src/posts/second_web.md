---
title: "A second Web"
---

## Introduction

We missed the point of the World Wide Web (WWW). Today we use it for rich web applications despite it being created for static documents. This post makes a proposal of a second Web, a Web for native applications.

I have no intent to defame any technology or programming language. I am certain that every choice taken has made sense to those who made it at that time. The point of this post is to pause for a moment to ask if the way we use the Web today makes sense. Inspired by the alleged quote of an Irishman

> Well sir, if I were you, I wouldn’t start from here.



## A brief history

In 1989, Tim Berners-Lee invented the World Wide Web. Now so famous, that many mistake it for the Internet as a while, it was designed to be a space of interconnected documents. The [first website](http://info.cern.ch/hypertext/WWW/TheProject.html) reads

> The WorldWideWeb (W3) is a wide-area hypermedia information retrieval initiative aiming to give universal access to a large universe of **documents**.

The documents are written in a markup language, most commonly HTML, to make them machine readable. The key feature of the World Wide Web is the link, through which once document can point to another one, building up an interconnected "Web". The applications used to display the markup documents are called Browsers, today the most commonly used application for many people.

Some years later the Browser makers decided to add a simple scripting language called JavaScript, which allowed to manipulate a website programmatically. Over the years through many iterations it evolved to what today arguably is the most widespread programming language of the world. JavaScript allowed previously static website to suddenly become dynamic, using patterns like AJAX to dynamically update only parts of a website. Websites are not simple documents anymore, they are applications ("Web app"). Nowadays there is hardly any website that is not interactive anymore, meaning that there is hardly any website that is not a Web app. Wouldn't it have been for JavaSript, the Web would long have been replaced.

> ToDo: Find the quote of Crockford.



## The problem

The web is not made to be interactive. It was made for static documents. Nowadays we build complex interactive applications, the kind of applications that should run natively on an OS, on top of these static documents. Since documents were not made to be dynamic, we constructed a lot of tooling to help build these interactive websites. There is a whole industry around builing front-end frameworks, because we can't organise this complexity of an application on top of a static document. We overloaded the Web standards with additions upon additions, a plethora of Web APIs, CSS animations, etc. to a point where starting to build a new interactive website seems like utter madness. It's like trying to build a car given a sheet of paper. With lots (!) of additions it will eventually work, but it was not made for the job. It would really make sense to build a car using parts for a car. We are so used to the current state, that we don't even question the 100.000.000 lines of JavaScript code anymore to show the dynamic music player of our Fortune 500 company in the markup document `index.html`. The Web was intended to show documents containing a few titles and paragraphs here, a few image there, just like TeX and PDF. The Web was not made to be interactive.



## The solution

So what happens to the cross-platform interactive websites our world is built upon? I propose we just use real applications: Native apps. Native apps are by definition interactive programs, have access to the whole OS API and ?. All the interactivity of the Web was patched on later and today we are left with a huge load of historical baggage. Things that can never be taken away, because documents are not compiled like native applications are. We should use applications as applications, and not website as applications.

There are _just_ two things missing: cross-platform and links. These are the fundamental principles of the Web, websites run everywhere and can link to any other website. What if native applications could do the same thing? Native applications that can link to other applications and run on any device. What we need is a "Web of native applications".

You might have laughed reading cross-platform applications. That's what's great about the web, right? Websites work on every Browser. Think about why that is. The Browser makers have the business incentive to give their users access to as much of the Web as possible, because this is what controls their market share. So the Browser makers want to standardise the Web such that all the websites work the same, because it's ultimately best for them. (Nobody cares about the user, but that is nothing new.)

What if the OS makers had the incentive to standardise their API? If native applications could link to other native applications like the Web such that they could be loaded by clicking on a link, an OS suddenly has the incentive to make as much applications work as possible. And a standards committe will appear, to stanardise the OS APIs.

Think about the benefit writing native applications over Web applications would have. We cut out the middle man of a Browser, that currently does all the work of handling the different OS APIs and allow apps to natively run on any OS. It makes no sense needing to build applications on top of the API of another application which interfaces the OS which interfaces the kernel. We should build a standard so we can interface the OS directly through a standardised OS API similarly to the standardised Kernel API POSIX.

There would need to be a common low-level programming language that every OS supported. A native application can then be written in any programming language that compiles down to the low-level programming language. This would also allow new langauges to flourish, e.g. you could use Xcode and Swift, or Android Studio and Java.

We keep compiling native applications, because this has proven to be the right choice. This allows the programming language to evolve without breaking backwards compatibility with older applications, since old applications can just keep using the old language and the old compiler. Meanwhile the programming languages of the Web are caught in the backwards compatibility cage, because since documents are not compiled nothing can ever be taken away without breaking old websites.

Writing native applications would be a revolution for Web developers. No need to handle the patched together Web standards anymore. No manual setup of frameworks, build process etc. when the native developer environment provides all of this, e.g. Xcode.

Native apps would need to become linkable, and cross-platform. There is no need for a centralised App Store anymore. Of course, there is a place for static websites that don't want to be Web apps. This proposal takes nothing away. It just moves Web apps to native applications.



## FAQ

- What about [my detail]?

I intentionally didn't go into specific implementation details, since this post tries to see the bigger picture instead of being caught up in small details. I try to see the forest for the trees.

- What about security?

With websites the Browser implements the sandbox and provides the rigorous security restrictions. With native apps this would be implemented by the OS directly. An inspiration could be taken from how iOS runs apps in a sandbox and asks for permissions.
