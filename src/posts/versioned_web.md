---
title: "A versioned Web"
---

## Introduction

One of the biggest pain points as a Web developer are the many bugs and weird quirks in the languages of the Web - HTML, CSS and JavaScript - that can never be fixed without breaking backward/forward compatibility.

Backward compatibility means code written in an earlier specification of the language needs to stay valid code in a later specification of the language. This means the spec can not change the meaning of existing features, e.g. JavaScript can not change the result of `typeof null == "object"`, but the spec can add new features that don't conflict with existing ones, e.g. JavaScript can add `typeof bigint == "bigint"`. All languages of the Web are backward compatible.

Forward compatibility means code written in a later specification needs to stay valid code in an earlier specification. This is only possible if the spec defines how it should treat code that it doesn't recognise. This has the same implications as backward compatible, the spec can not change the meaning of existing features, e.g. CSS can not change the meaning of `size` inside a `@page {}`, but the spec can add new features that don't conflict with existing ones, e.g. CSS can add a `size` property outside of a `@page {}`. JavaScript is not forward compatible, because it can't just ignore parts of the code, as it would make code non-deterministic. However, HTML and CSS are forward compatible.

Note, compatibility is not defined in terms of the implementation, but is purely a property of the language itself. With implementation I refer to anything that can run the language, i.e. browsers for HTML, CSS, and JavaScript, or Node / Deno for JavaScript, etc.

While certainly nice for implementations, compatibility is a huge pain for developers and spec writers. Compatibility means any mistake ever made in the language can not be corrected. Since there is no such thing as "perfection", mistakes will eventually be made and were made already plentyful. By now the languages of the Web are littered with flaws. You probably already have a dozen examples of JavaScript bugs in mind, and CSS and HTML don't have less. A nice read is the official [Incomplete List of Mistakes in the Design of CSS](https://wiki.csswg.org/ideas/mistakes). Since bugs only increase with time, the question is not if, but when you will give up on Web development, because the languages are just too littered with bugs.

Compatibility is not only a pain for developers but also slows down the development of the language as a whole. For every new feature a lot of time is spent just to make it work around all existing bugs, and minimise any breaking change. If these bugs weren't there, progress would be so much faster. Mistakes should be allowed to be fixed. Compatibility prevents that.

This post tries to argue that the languages of the Web don't need forward and backward compatibility and how this can be solved with versions. This is actually what languages for mobile app development like Swift already do. The version of Swift you use is just implicitly determined by the version of Xcode you use, e.g. Swift 4 in Xcode 9, Swift 5 in Xcode 10, etc.



## Versions

A version of a language is its specification at a specific point in time. You could imagine the spec being versioned yearly at a specific date. The version of the languages of the Web could be synchronised, such as to not need to keep track of different versions across the languages, e.g. ES2016 and CSS3 and HTML5, etc.

Between versions the language is not constrained by backward or forward compatibility. This means in theory you could make the new version a completely different language, say make it consist of emoji characters instead of ASCII. In practice, this would be used to fix all bugs of previous versions of the language. I imagine no more margin collapse by default in CSS, no more `typeof null == "object"` in JavaScript, etc.

Developers would need to be able to choose a version of the language. Since on the Web the source code is distributed instead of the machine code like in mobile app development, there would need to be a version identifier at the top of every file. For compatibility, a file without a version identifier maps to todays spec before any version was introduced. I'll intentionally leave out a concrete suggestion for the syntax of such a version identifier, because this would certainly be a hot topic of discussion and digress from the point this post tries to make.

The glaring question is what happens with a new version in an old implementation? Since it doesn't know how to handle the changes it would necessarily break. But wouldn't that destroy the Web? Shouldn't every implementation be capable of displaying any webpage? Well, no. This is exactly the topic of forward compatibility, and if you read the Introduction you already know that JavaScript is not forward compatible. In other words, already today this problem exists, since old implementations break on new JavaScript. And since webpages heavily rely on JavaScript, you can very well assume the whole webpage breaks. HTML and CSS remain forward compatible with the assumption that you could still make some use of the static version. But increasingly more webpages rely on JavaScript and become unusable without it, invalidating the whole assumption of HTML and CSS for being forward compatible.

What we all already do when writing JavaScript is select the implementations we want to support, and accept that older ones break. This is what discussions like "Oh Destructuring assignment? Well, you can't use them because we still need to support IE11." and "Oh Destructuring assignment? Yes, you can use it because we dropped support for IE11." are all about. There is no reason we can not and should not handle compatibility the same way with CSS and HTML. This means, HTML and CSS do not need to stay forward compatible. It should be the developer of a webpage that decides which users they want to support and not the language itself through a universal forward compatibility requirement.

What about backward compatibility? How can webpages written in earlier versions continue to work in implementations of later versions? Well, an implementations can decide to implement multiple versions of the languages, choosing which to use based on the version identifier in the source code. Agreed, this would put more burden on the implementation, since it bloats up over time with support for multiple different versions. But it would take of the burden from the language itself and allow a whole ecosystem to evolve again unconstrained. I think that's a fair tradeoff.

Also implementations could prevent bloating up by intelligently choosing to support only the most recent versions, and drop support for earlier versions. The implementations would figure out where to set the threshold based on usage statistics, and how to download support for older versions if a user still happens to visit a webpage written in a historic version, like in the background on the first visit. I think it's time to stop assuming a current implementation needs to support the complete 100% of the Web at that point in time. It's enough if it supports only the part of the Web that you actually use. 

PS. The argument, that no current implementation will support versions and therefore code in a new version will break, is just the same as above on forward compatibility with the current implementations being the old implementations. Of course, you as the developer have to wait until all your selected implementations support versions before you use versions. This is not an argument against versions. The wait could be minimised by using tooling to backport purely syntactical changes and new features that can be polyfilled, similar to how it's done with JavaScript today.



## Mobile Apps

Websites are far more than the static documents they were intended for when conceived. In terms of functionality, websites aren't really different from mobile apps anymore. And the line between websites / mobile apps and desktop programs continues to blur as well. All can be simply seen as "applications".

The problem is the languages of the Web weren't designed for what they are used for today. They were designed for static documents, not for dynamic applications. They lack too much compared to languages like Swift and SwiftUI. For a more detailed discussion see [A second Web](A%20second%20Web.md).

There are two possibilities.

### Make mobile apps like websites

The only thing that mobile apps conceptually lack is being identified by URLs. This is the foundation of the Web and what made it into the universal space of information it is today. If you could link to any place within an app, then you could essentially replace webpages with mobile apps. But apps also would need to be cross-device compatible. Both things don't look too promising right now.

### Make websites like mobile apps

The different between apps and websites is that apps are unlike websites not source code, but compiled to machine code. Machine code doesn't evolve, meaning it continues to run no matter what happens to the source language. The source language can freely evolve without breaking existing machine code. Backward and forward compatibility of the source language only happens between the source code and the compiler, which are both controlled by the developer, not between the source code and the user, which aren't both controlled by the developer.

There is no reason why webpages could not be binaries just like mobile apps. The tooling nowadays is already a compilation [^1] from what ever higher framework language you use (React, Vue, Angular, Svelte, etc.) down to the lower languages of the Web. No serious website is written without such tooling anymore. Making the compilation necessary wouldn't even be noticed by most developers. A real binary format would come with countless benefits, like better peformance, smaller file size, mangling by design, etc.



## WASM

Reading the previous section, you were probably thinking about WASM. WASM is a step in the right direction, but in it's current form it's not (yet) the magic cure-all.

WASM is a binary format to which higher-level programming languages can be compiled. It allows you to write your code in your favorite programming languages, instead of only JavaScript, and compile it to run in the browser. Note, it doesn't replace JavaScript, as you could use JavaScript as your higher-level programming language of choice [^2]. Currently WASM lacks Web APIs, but they are coming.

But WASM alone is not enough to create a webpage. It is not intended to be used for interface languages like HTML and CSS. Provided you don't want to write your entire interface through the horrible DOM and CSSOM APIs, WASM can't be used to create an entire webpage.

There would need to be some kind of "WASM UI", a binary format to which higher-level interface languages can be compiled. It would allow you to use your favorite interface languages to write your interface, not just HTML and CSS.

WASM and the imaginary "WASM UI" would elevate the Web to a real programming platform. You could use your favorite language that compiles to WASM and "WASM UI" to develop websites. Similarly to the desktop, where you can use the language of your choice, like C++, Rust, etc., that compiles to ARM / X86 machine code. For example, instead of JavaScript you could use Swift, instead of HTML and CSS you could use Swift UI. Developers wouldn't be forced to create their webpages in the bugged languages of the Web anymore. This would be one of the biggest leaps for the Web since it's inception.



## Conclusion

Versions would allow to fix bugs that the languages of the Web amassed over the years. It would be a huge step forward. But does it really fix the problems?

Maybe we should not fix the languages of the Web and instead focus on making them entirely optional via WASM and "WASM UI". Though until WASM and anything like "WASM UI" would be adoptable, some time will pass. I believe, fixing the versioning of the languages of the Web would be worth it in the meantime.

---

[^1]: Technically it's only transpilation, since the languages of the Web are still high-level

[^2]: This is a bit of a oversimplification, as compiling JavaScript to WASM directly doesn't work. You'd have to add types to get a TypeScript-like code. This is called AssemblyScript.
