---
title: "A versioned Web"
---

## Introduction

One of the biggest pain points as a Web developer are the many bugs and weird quirks in the languages of the Web - HTML, CSS and JavaScript - that can never be fixed without breaking backwards compatibility. There are too many to count by now. Just look at the [Incomplete List of Mistakes in the Design of CSS](https://wiki.csswg.org/ideas/mistakes).



## Versions

The languages of the Web should have versions. All the bugs and quirks could simply be fixed in a new version. The developer can choose to code in the new fixed version instead of the old bugged one. Just imagine, no more margin collapse in CSS, no more `typeof null == "object"` in JavaScript, etc.

The most obvious question is what happens with a new version in an old browser? Since it doesn't recognise the changes, it would ignore it and break. Shouldn't every browser be capable of displaying any website? Well, no. If you use a 10 year old browser, you should not expect to be able to use the Web the same way as with a current browser. Just like you can't expect your old car to suddenly have all nice amenities that a new car offers. That's why there are new cars. Because changes were made. But then the Web would break, you might scream. No, it doesn't. Instead, it already is like that for JavaScript. JavaScript is code that doesn't make sense if you don't understand all of it, unlike with HTML and CSS where you can ignore certain parts you don't recognise. Therefore already today old browsers break on new JavaScript, because they can't interpret new features. Unfortunately, real versioning is still missing, which would allow to fix also existing features, like `typeof null == "object"`.

Similarly to JavaScript, developers would select the browsers they want to support, and accept oldder ones break. There is no reason this can not and should not be done with CSS and HTML.

The other argument, that no current browser will support versions and therefore code in a new version will break, is just the same as above with the current browsers being the old browsers. Of course, you as developer have to wait until all your selected browsers support versions before you use versions. The wait could be minimised by using tooling to backport purely syntactical changes and new features that can be polyfilled, similar to JavaScript.



## Implementation

The version of the languages of the Web could be universal, such as to not need to keep track of different versions across the languages, e.g. ES2016 vs CSS3 and HTML5. It could be a snapshot of the current specs at a specific periodic point in time, perhaps yearly.

A version identifier can be added at the top of every file which denotes the version of the language in which it should be interpreted. An omitted version would compute to the spec before any versioning for backwards compatibility. As discussed above in [Versions](#Versions), it's the developers responsibility to make sure that the chosen version is supported by all targeted browsers. I'll intentionally leave out a concrete suggestion for the syntax of such a version identifier, because this would certainly be a hot topic of discussion and digress from the point this post tries to make.



## Mobile Apps

One reason why the ecosystem for Mobile Apps is so nice to develop for is, because a single party controls the language and implementation, and can force them both to evolve. If Apple wants to change something in Swift, they just update Xcode. Since apps are compiled to ever constant machine code, already existing apps won't break by changes in the language.

I believe Web development would be much easier, if there were a compilation step similar to App development. This is in fact what most of the tooling effectively do, they compile what ever higher framework language you use down to the pure languages of the Web. There is no reason websites shouldn't be binaries and the languages of the Web compiled. Certainly, many things would need to be rethought, like HTTP. (btw: No, WASM in it's current form is not the cure all, as it doesn't replace HTML and CSS.). Websites aren't that different from mobile apps anymore, since they are far more than the static documents they were intended to be when conceived. The only thing that Apps still lack is being able to run them cross-system and being identified by URLs. The later is the foundation of the Web and what makes it successful in the first place. If you could link to any place within an app, then you could essentially replace websites with Apps.
