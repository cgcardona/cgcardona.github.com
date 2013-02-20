---
layout: post
title: "Syntax highlighting in markdown code blocks on github"
description: ""
category: 
tags: ['markdown', 'code']
---
{% include JB/setup %}

I've been writing/ready quite a bit of documentation lately and have settled on
[Markdown](http://daringfireball.net/projects/markdown/). It continues to be the
most powerful way to structure and express my thoughts.

Recently I began to notice that docs I have been reading which are written in
markdown had syntax highlighting in their code blocks. At first I thought
perhaps they were just creating [gists](gist.github.com) and placing the url in
the post which would embed the code block. 

However after poking around I came to find out that [Github flavored Markdown](https://help.github.com/articles/github-flavored-markdown)
supports the following syntax:

`` ```javascript ``
