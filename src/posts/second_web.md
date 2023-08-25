---
title: "A second Web"
draft: true
---

## Introduction

We're using the World Wide Web (WWW) wrong. Today we build rich web applications despite it having been created for static documents. Inspired by the alleged quote of an Irishman

> Well sir, if I were you, I wouldn’t start from here.

This post makes a proposal of a second Web, a Web for native applications, that lives alongside the existing Web. I have no intent to talk badly about any technology! I am certain that every choice taken has made sense to those who made it at that time. The point of this post is to pause for a moment and question if how we use the Web today still makes sense.



## A brief history

In 1989, Tim Berners-Lee invented the World Wide Web. Now so famous, that many mistake it for the Internet as a whole, it was designed to be a space of interconnected documents. The [first website](http://info.cern.ch/hypertext/WWW/TheProject.html) reads

> The WorldWideWeb (W3) is a wide-area hypermedia information retrieval initiative aiming to give universal access to a large **universe of documents**.

The documents are written in a markup language to make them machine readable, today mostly in HTML. The key feature of the World Wide Web is the link, through which one document can point to another, building up an interconnected "Web" of documents. The application used to display these "websites" and follow links is called a "Web Browser". Because links are not centralised, websites can be made by anyone, and accessed from anywhere using a Web Browser.

Some years later the Web Browser makers decided to add a simple programming language called JavaScript, which allowed to manipulate a website programmatically. Over the years through many iterations it evolved to what today is arguably the most widespread programming language in the world. JavaScript allows static websites to suddenly become dynamic, using patterns like AJAX to dynamically update only parts of the website. Websites are not simply documents anymore, they are applications, so called "Web applications". Nowadays there is hardly any website that is not dynamic anymore, meaning that there is hardly any website that is not a Web application. Hadn't it been for JavaSript, the Web would long have been replaced.

> If that [HTML and CSS] is all there had been, the Web would have been replaced by now. [...] JavaScript was what kept it alive in spite of its obvious failings.
>
> -- [Douglas Crockford - Crockford on JavaScript - Episode IV: The Metamorphosis of Ajax](https://youtu.be/Fv9qT9joc0M?t=1588)



## The Web is static

The Web was made for static documents, mostly textual with a few images, just like TeX and PDF. The Web was not made for interactive applications. Nowadays we build large Web applications out of these simple static documents. We overloaded hypertext documents with lots of CSS and JavaScript to make it behave as dynamic as possible. The Web standards are essentially a complex layer of patchwork to change what was built as a square brick that doesn't move into a round disk that can roll. Whole industries emerged around providing frameworks for all kinds of parts of that patchwork stack that facilitate the development. Maybe in the end the square brick will roll, but we can't negate the fact that a square brick was not made to be a tire. We are so used to the current state, that we don't even question the several thousand lines (in total, with framework) of JavaScript code anymore to make the markup document `index.html` a dynamic music player. It would really make sense to build a car using parts for a car. The pain introduced into the platform by using an inherently wrong foundation is immense, and frameworks on top of a wrong foundation can only do so much to ease the pain. So, why do we bother building Web applications instead of just native applications?



## The second Web

Native applications miss the two key features of the Web - links and cross-platform. Just like our documents we would like our applications to be available from everywhere via links and work cross-platform. What we do right now is to painfully build Web applications on top of the static documents just to have these two features. What I argue we should do instead is build a Web for native applications, so we can build applications again as native applications. What if native applications could link to other applications and run on any device? The need for Web applications would quickly diminish.

You might have laughed reading cross-platform applications. That's what's great about the web, right? Websites work on every device that runs a Web Browser. Think about why that is. The Web Browser makers have the incentive to give their users access to as much of the Web as possible, because this is what drives their market share. Because of this, the Web Browser makers are incentivised to build universally agreed upon Web standards, because then websites are more likely to work on their Web Browser.

What if, instead, the OS makers had the incentive to standardise their OS API? If native applications could link to other native applications like websites can, an OS maker suddenly has the incentive to make as much applications work as possible, because this would attract more users. Similarly to the Web, this will insentivise the OS makers (Linux distributions, macOS, Windows, etc.) to form a standards committee and work towards a standardized OS API.



## Web applications vs. native applications

Think about the benefit that writing native applications over Web applications would have.

Native applications are aren't limited like Web applications, because they weren't build on top of static documents. They have full fledged development environments, e.g. Xcode. The programming languages for native applications aren't patched together like the Web standards to transform static documents into interactive applications. Because of this, Web standards are a huge load of historical baggage, as any Web developer can tell you. Web standards can never be removed, because documents are not compiled like native applications are, and therefore any removal would break some old website. We should use applications as applications, and not website as applications.

With native applications we don't depend on a third-party programm - the Web Browser. It makes no sense to build applications on top of the API of another application which interfaces the OS which interfaces the kernel. Applications should run natively on an OS, not inside a third program - here the Web Browser. Currently the Web Browser offers the standardised Web APIs and does the work of handling the different OS APIs. We instead should build a standardised OS API, similarly to POSIX for the Kernel, such that an application can directly interface the OS and be cross-platform.

There would need to be a common low-level programming language that every OS supported, e.g. WebAssembly. A native application can then be written in any programming language that compiles down to the low-level programming language. This would also allow new languages to flourish, e.g. you could use Swift to write one single native application for _all_ devices.

Native applications are compiled, because this has proven to be the right choice. This allows the programming language to evolve without breaking backwards compatibility with older applications, since old applications can just keep using the old language and the old compiler. Meanwhile the programming languages of the Web are caught in the backwards compatibility cage because, since documents are not compiled, nothing can ever be taken away without breaking old websites.

Writing native applications would be a revolution for Web developers. No need to handle the patched together Web standards anymore. No manual setup of frameworks, build process, helper libraries, since the native developer environment can provide all of this, e.g. Xcode. I don't want to imagine how much time humanity wasted to dope up static documents to behave like dynamic applications.



## Universal links

Currently we can link from within a hypertext document to any resource, that was one key the idea of HTML. What if links could be in any type of file? What if any type of file could link to any other type of file? For example, in a video a part links out to another video? It would work just like linking hypertext documents, removing the need to duplicate content and keep it up-to-date. Not all links make sense though, e.g. linking to a document from within a music song. New file types would need to be invented, that implement linking capabilities, like HTML did for documents. One of those file types would be the the application file type that was discussed in the rest of this post.



## FAQ

- So you want to delete the Web?

No, I don't want to take the Web away. It is here to stay - but for static documents. Dynamic applications should be native applications. The Web was not designed for applications. It was made for static content like documents. I propose a "second Web" where dynamic content like an application can live. This proposal takes nothing away. It just shifts Web applications to be native applications instead.

- What about [some detail]?

I intentionally didn't go into specific implementation details, since this post tries to see the bigger picture instead of being caught up in small details. I try to see the forest for the trees. Also I don't want to come up with concrete implementation details, because if I miss something, the common thinking will dismiss the overal proposal.

- How do you link to applications?

A first idea would be to invent a new "Application Transfer Protocol" akin to HTTP but for applications instead of hypertext. This could be in JSON to make parsing simple. Then every resource in the second Web gets a URL similar to the first Web, e.g. `atp://com/example/foo/bar/baz` to [fix the syntax as well](https://www.w3.org/People/Berners-Lee/FAQ.html#etc). The OS could then implement a "URL bar", for example inside the OS wide search, where you can type in any domain. This then downloads and caches the application and opens it, just like a website loads but with the result of having a native application. Any native application can link to others, if installed it would just open it, otherwise download it and then open. Pretty much like clicking a link in the Web Browser, just without a Web Browser.

- What about security?

With websites the Web Browser implements a sandbox and provides the rigorous security restrictions. With native applications this must be implemented by the OS directly, like iOS with sandbox and permissions prompts, but stricter.

- How do you write native applications cross-platform?

OS makers must decide on a common low-level language, e.g. WebAssembly, and a OS API, similarly to the POSIX standard for the Kernel API. Given this, native applications can be created in any programming language that compiles down to the common low-level language, making use of the existing proven development environments, e.g. Xcode.

- What's the OS makers incentive to implement "the second Web"?

Control of standards. Currently the Web Browser makers control the Web standards and therefore the limitations of Web applications (of which some are also OS makers, e.g. Apple). By putting the control directly in the hand of the OS makers, the second Web can evolve faster, because the hierarchy is flattened. Without Web Browsers, if the OS API implements a new feature, native applications can use it without having to wait for the Web Browsers to implement it.
