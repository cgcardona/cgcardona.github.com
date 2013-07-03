---
layout: post
title: "From Vim To Emacs"
description: ""
category: 
tags: ['vim', 'emacs']
---
{% include JB/setup %}

## Set the stage

Any hacker who is worth their weight in bytes knows that there are ultimately two text editors that really matter. Two text editors which have been at the center of an [ages old flame war](http://en.wikipedia.org/wiki/Editor_war). And most importantly two text editors that you can be 100% confident that you'll find on any remote server you might find yourself `ssh`ed into on some late and dark night.

Those two venerable text editors are the Mighty [Vi](http://en.wikipedia.org/wiki/Vi) and the equally Mighty [Emacs](https://en.wikipedia.org/wiki/Emacs).

## Moment of clarification

It's worth noting at this point that I don't actually use `vi` per se. I use `vim` which stands for 'vi improved.' Basically a really smart guy named [Bram Moolenaar](http://en.wikipedia.org/wiki/Bram_Moolenaar) added a bunch of modern stuff like scripting functionality, syntax highlighting, multibuffers, extensions and a whole bunch of other goodies to `vi` and called it [Vim](http://www.vim.org/). 

Now back to our tale...

## And then there were Two

I wasn't aware of both choices when I started programming. It just so happened that my coding mentor as well as the rest of my new team all used Vim.

I was using [Smultron](http://en.wikipedia.org/wiki/Smultron) as my editor because it was the first free editor that was recommended to me in the `#html` chatroom on the Freenode IRC Network. I had also briefly started using [TextMate](http://en.wikipedia.org/wiki/TextMate) because one of the leads on our team used it and had some Rails bundles.

However I had one engineering lead in particular who was adamant that I use `vim` and actually gave me quite a bit of on the job time to run through a bunch of tutorials and reading material to start to get comfortable with the tool.
 
I must admit that once I had [Z shell](http://en.wikipedia.org/wiki/Z_shell) with [Oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) dialed in with a highly customized `.vimrc` as well as a host of `vim` commands engrained in my muscle memory my text editor started to feel like home and I was most content. 

## Emacs curious

Along the way I read many things about emacs. I had read that it was so powerful that people often derided it by calling it 'a great operating system, lacking only a decent editor.' I also realized that it was originally written by the old grey haired man of free software [Richard Stallman](http://en.wikipedia.org/wiki/Richard_Stallman)--which placed it as the central text editor of the [GNU System](http://en.wikipedia.org/wiki/GNU).

I even tried to learn it more than once. But the truth is that I couldn't stand the `C-x C-c` type of nonsense for every command. I was taught that an ultimate skill of a command line hacker is to minimize the number of keystrokes for every command. I even go so far as to have aliases for every thing I use that brings it down to one or two keystrokes. 

`emacs` forcing me to have double keystrokes with double key combinations was absolutely maddening and I would have none of it. For a comparison consider the following task which is performed many times an hour when working. Namely, searching for all occurrences of a string of text across an open page of code and then cycling between them.

This is how I would do it in `emacs`

    M-x grep
    grep -nH -e 'foo_string' foo_file.rb

Then to switch between all the occurrences of 'foo_string' I would type:

    C-x``

In Vim the same action is

    /foo_string
    n
    
And there are a bunch of other examples like this. I'm sure there are hella macros out there which tame some of this insanity but let's just say that out of the box emacs is **much** more verbose than vim.

So I was just never willing to really spend more than a brief time with emacs before I just fell back on vim because of the performace hit I was taking from trying to switch.

However this last weekend I was reading about one of my favorite hacker heroes--the legendary [jwz](http://www.jwz.org/). Specifically I was reading about how before he was at [Netscape](http://en.wikipedia.org/wiki/Netscape) and [Mozilla](http://en.wikipedia.org/wiki/Mozilla) he was a [LISP](http://goo.gl/c0R5a) programmer at Lucid. 

While he was there he was the lead developer on [XEmacs](http://en.wikipedia.org/wiki/XEmacs) which was a kick ass Emcas client for unix at the time. In fact it was so kick ass that it was at the center of [The Great Emacs Schism](http://www.jwz.org/doc/lemacs.html).

After reading all about it I decided that I just had to give `emacs` another try. I mean, what did I have to lose? At the very least I could always come crawling back to trusty old `vim` with no questions asked. But in a best case scenario I could see myself finally taking the time to find the macros needed to tame some of the keyboard nastiness and then I would finally begin to have emacs in my toolset.

However one single event happened which made me decisively choose to use emacs as my primary text editor going forward. And that was when I realised that emacs is really just a thin wrapper around a LISP runtime. In fact the User's `~/.emacs` file is written in LISP as is all the other configuration and extension.

## The magic of LISP

Allow me a quick sidenote to explain why I'm interested in LISP. First, it is the second oldest high level language in the world after Fortran and I'd bet that LISP is a far more influential language than Fortran. 

Second, LISP found it's place in the Artificial Intelligence research community. I have always read that in LISP 'code is data and data is code' and have always wondered exactly what that meant.

Third, the Scheme dialect of LISP's lambdas were highly influental on Javascript which is another language that I love. Consider this quote from [Douglas Crockford's](http://en.wikipedia.org/wiki/Douglas_Crockford) Javascript The Good Parts:

> JavaScript is the first lambda language to go mainstream. Deep down, JavaScript has more in common with Lisp and Scheme than with Java. It is Lisp in C's clothing. This makes JavaScript is remarkably powerful language.

So remember that each time your passing around an anonymous function around is Javascript it traces it's roots back to Scheme and LISP.

## May the force of the Vim be forever with thee?
 
The top of my `.vimrc` file has the quote

> May the force of the VIM be forever with thee...

However this realization that Emacs could be seen as a text editor wrapper around a lisp environment really struck me as amazing. It was like a flash of lightning. At that moment I decided that I would have to do what it takes to make the transition from `vim` to `emacs`

## Evil

So I bit the bullet, began learning a host of new keyboard combinations/commands and started to make the transition. But after a couple of days it was clear to me that I was taking a major productivity hit. It seemed like my fingers were lost and I was taking 5-10 times longer to do each task. It was slowing my work down to a crawl. Most of the days were spent struggling with the tool as opposed to being accelerated by it.

In frustation a few days ago on twitter [I said](https://twitter.com/cgcardona/status/351739836564111360):

> Predictably the biggest issue w/ switching from #Vim to #Emacs has been loss of productivity. I'm really fast w/ Vim & my fingers feel lost

[@redblobgames](https://twitter.com/redblobgames/) [answered](https://twitter.com/redblobgames/status/351924335985963008):

> evil-mode?

That led me via Google search to [Evil](http://www.emacswiki.org/emacs/Evil) which stands for 'extensible vi layer.' Basically it is a way to use the `vim` commands over top of `emacs`!!

:-D

## Victory

I'm sure there are plenty of `emacs` users who find this kind of thing totally distasteful. At this time I can hear them saying "Why wouldn't you just use `vim`?" 

To that I answer--because emacs is a wrapper around a lisp environment which I want access to. 

Vim and Emacs both took time to learn. But the time was oh so worth it because of the promise of great power. 

With `vim` I found that great power relatively early on and have leveraged it every day since. Now I'm willing to spend the time and hope to make the transition to using `emacs` and making the most of the underlying LISP envinronment.

With the `evil` layer hopefully I'll not need to go running back to `vim` again because I'll have him along with me for the journey.