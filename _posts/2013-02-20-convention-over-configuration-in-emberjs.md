---
layout: post
title: "Convention over Configuration in Ember.js"
description: ""
category: 
tags: ['emberjs', 'javascript', 'code']
---
{% include JB/setup %}

Ah good ole [convention over configuration](http://en.wikipedia.org/wiki/Convention_over_configuration)&mdash;we
love it. It's what allows us to skip over mountains of boilerplate. It's what
allows us to quickly onramp to a new project.

Ember.js seems very 'rails-like' in the depth and scope of the convention over
configuration. Here is want to point out some places where it's apparent to me.

With the simple command `var App = Ember.Application.create();` Ember creates
the following for us:

### Application Controller

We can confirm this happens because we hadded

### Application Template

Technically Ember doesn't create this template for you. You need to create this
template in your index.html and add the `{{outlet}}`. 

```js
    <script type='text/x-handlebars' data-template-name='application'>
      {{outlet}}
    </script>
```

* Index Route

The default route /, called index, is set up automatically by Ember. When our
user visits /, Ember renders the index template. When our user visits
/contributors, Ember renders the contributors template.
