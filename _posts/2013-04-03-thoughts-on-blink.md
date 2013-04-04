---
layout: post
title: "Thoughts on Blink"
description: ""
category: 
tags: ['google', 'blink', 'webkit', 'mozilla', 'apple', 'gecko', 'servo']
---

## Intro

Google surprised everyone today by [announcing that they're forking Webkit](http://blog.chromium.org/2013/04/blink-rendering-engine-for-chromium.html) into
a new project called [Blink](http://www.chromium.org/blink).

Keep in mind that there are **many** different players in the Webkit space.
As with any massive open source project each player is somewhat limited in what
they may do to the code before they have a negative effect on someone else.

Basically Google is saying that the cost of supporting all the code is
outweighing the benefits. They are betting that they can innovate quicker on
their own code base.

In the announcment they even highlight

>  For example, we anticipate that we’ll be able to remove 7 build systems and
>  delete more than 7,000 files—comprising more than 4.5 million lines

## Haters gonna hate?

On Feb 12th [Opera announced](http://my.opera.com/ODIN/blog/300-million-users-and-move-to-webkit)
that they were going to start using Webkit as their rendering engine and V8 as
their javascript engine.

At the time there were [howls of lament](https://news.ycombinator.com/item?id=5211953) on Hacker News and across
Twitter from people who were convinced that this was the end of the web as we
knew it.

Webkit had become the new IE and innovation would now grind to a halt. We might
as well get out our fucking blink tags and table based layouts.

## Nah

I never believed that argument FWIW. IE6 was always about lowest common
denominator. No matter what great features came to us from the Gods at the W3C
we couldn't use them without some god awful polyfill hack. 

Webkit on the other hand seems to be a form of highest common denominator. All
the browsers that are part of the ecosystem get a standard and common set of
functionality out of the box. They then build their own custom stuff on top of
it which is hidden behind a vendor prefix like `-webkit`.

## No more prefixes :-[

One part that really stood out to me as a negative was the [vendor
prefixes](http://www.chromium.org/blink#vendor-prefixes) section on the Blink
page.

They mention that they'll no longer support experimental features with vendor
prefixes. Instead they'll have the unprefixed feature hidden behind a flag which
can be turned on in `about:flags`.

I think this totally sucks. Let's be completely honest. We've all been building
sites with vendor prefixes for years. We've been using drop shadows and rounded
corners with vendor prefixes long before they were 'officially' supported. 

We were well aware that our rounded corners would gracefully degrade to
non-rounded corners for users running older browsers but it was something what
we were willing to live with to get the benefit of pushing the vendor prefixed
code out to the millions of users running modern browsers.

With this new decision to hide all experimental features behind a flag we're
removing the developer's power to build an app with **any api that they
choose**.

Unfortunately it appears that [Mozilla is also beginning](http://lists.w3.org/Archives/Public/public-webapps/2012OctDec/0731.html)
to implement a similar policy as is the [W3C CSSWG](http://www.w3.org/blog/CSS/2012/08/30/resolutions-53/).

## Opera, Apple, and the rest

You've gotta wonder what the people at Opera are thinking right now. After going
all in on Webkit only two months ago they find out today that Google is coming
out with something **even better**.

I'm unclear on exactly how much code Google contributes to Webkit on the regular
but this could potentially slow down the pace of innovation in the Webkit code
base considerably.

Of course it could have the opposite effect as well. Just as Google is able to
remove 4.5 million lines perhaps a similar amount can be removed on the Webkit
side which would have huge benefit for size is no virtue in software.

But no matter what's to be gained from removing Google specific code from the
codebase it won't come close to balancing what'll be lost by having no more
Google contributions to the codebase. There's no other way to spin
this&mdash;it's a bad thing for the Webkit community and codebase.

Of course Apple is heavily invested in Webkit and will presumably keep
supporting it and improving it.

It's amazing that the Google team were able to keep their mouths shut at the time
when everyone was talking so much crap about the Webkit monoculture. Here they
were about to fork the entire project and they had to keep hush hush.

## My thoughts

My personal opinion is that this is a good thing. I often think of codebases as
living breathing organisms which grow and evolve over time. You can clearly draw lineages in 
codebases which live many years and go through multiple refactorings.

In this case this is like some type of evolutionary split. From here on out
Blink is a completely new organism. Both it and Webkit will begin to evolve down
their own paths. In a couple of years it will be interesting to compare them
both to see where exactly they've grown apart and in what ways.

## Changes

Other huge news is that Mozilla is working on a new [Browser Engine called
Servo](http://blog.mozilla.org/blog/2013/04/03/mozilla-and-samsung-collaborate-on-next-generation-web-browser-engine/).
It's written in the new programming language [Rust](http://www.rust-lang.org/).

As jQuery creator John Resig [said on
twitter](https://twitter.com/jeresig/status/319564385779593217) earlier:

> Moz + Samsung are working on Servo, Google forked WebKit, and Opera is
> switching to Chromium -- we're entering a new age of browserdom!

## More Info

* [Ars Technica](http://arstechnica.com/information-technology/2013/04/google-going-its-own-way-forking-webkit-rendering-engine/)
has a great write up.
* [Hacker News Thread](https://news.ycombinator.com/item?id=5489025)
