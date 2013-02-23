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
perhaps they were just creating [gists](http://gist.github.com) and placing the url in
the post which would embed the code block. 

However after poking around I came to find out that [Github flavored Markdown](https://help.github.com/articles/github-flavored-markdown)
supports the following syntax:

    ```javascript
    var foo = 'bar';
    ```

Which will produce the following javascript:

```javascript
var foo = 'bar';
```

My guess is that it supports any langaugae that you can get syntax highlighting
for in a gist.

## Turn it on

Github parses Markdown with [Redcarpet](https://github.com/vmg/redcarpet). As of
[Jekyll 0.12.0](https://github.com/mojombo/jekyll) redcarpet can be turned on by
simply adding the following line to `_config.yml`:

````yaml
markdown: redcarpet
````

You'll also need to include the [syntax highlighting CSS file](https://gist.github.com/robsimmons/1172277/raw/3eadd9e60c5cc74fbed0f249bad5eb61defaf463/gh-like.css)

## That's all!

That should do it. You should now be able to use the sweet new syntax for
getting syntax highlighting in code blocks!

## Examples

### Ruby

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

### PHP

```php
<?php
$os = array("Mac", "NT", "Irix", "Linux");
if (in_array("Irix", $os)){
  echo "Got Irix";
}

if (in_array("mac", $os)){
  echo "Got mac";
}
?>
```

### HTML

```html
<p>hello world</p>
```
