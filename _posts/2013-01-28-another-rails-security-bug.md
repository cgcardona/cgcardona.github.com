---
layout: post
title: "Another Rails Security Bug"
description: ""
category: 
tags: ['rails', 'ruby']
---
{% include JB/setup %}

## Intro

Another [security issue in rails](https://groups.google.com/forum/?fromgroups=#!topic/rubyonrails-security/1h2DR63ViGo) just hit [hackernews](http://news.ycombinator.com/item?id=5130631).

First let me say that though it sucks to find out about security issues with your framework of choice it's still good to see these kinds of things because it proves that there are eyes on the code base and a team of smart people reacting quickly when something gets noticed.

However it is really inconvenient to have to update and redeploy **every** app that you have out in the wild. As discussed in the top thread on hacker news it would seem like something that could be solved at the framework level. Or potentially at the platform provider level. 

Though that opens up another security threat by putting a single point of failure on the service provider successfully pushing the security patch.

Yes I'm aware of the following notation in the Gemfile:

    gem 'rails', '~> 3.2.11'
    
I use it [https://github.com/cgcardona/cents_us/blob/master/Gemfile](https://github.com/cgcardona/cents_us/blob/master/Gemfile)

But that still means the devloper needs to know about the issue in the first place and then redeploy after

    bundle update rails
    
## Why is this a good thing?

As pointed out on hacker news:

> The vulnerabilities here only affect versions that have been maintenance-only for almost eighteen months. The last two major versions of Rails (since 3.1, released in August, 2011) are unaffected.
> ... the fact that someone bothered to comb through 2.3.x and 3.0.x to find exploits similar to the last one points to a very good process, not a broken one.