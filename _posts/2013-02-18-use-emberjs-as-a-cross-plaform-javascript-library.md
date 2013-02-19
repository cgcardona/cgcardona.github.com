---
layout: post
title: "Use Ember.js as a cross plaform javascript library"
description: ""
category: 
tags: ['emberjs']
---
{% include JB/setup %}

This code is related to [Version: v1.0.0-rc.1](https://raw.github.com/emberjs/ember.js/release-builds/ember-1.0.0-rc.1.js)

I've been thinking of Ember as a monolithic framework but under the hood there
are actual several modules. To see this in action clone the [Ember.js github repo](https://github.com/emberjs/ember.js/) generate the `dist/` directory by
running: 

    $ rake dist 
    /Users/cgcardona/Sites/ember.js/Rakefile:6: warning: already initialized constant EMBER_VERSION
    Building Ember...
    Done

    $ ls -alr dist/
    ember-data-deps.js
    ember-data-deps.min.js
    ember-data-deps.prod.js
    ember-debug.js
    ember-old-router.js
    ember-old-router.min.js
    ember-old-router.prod.js
    ember-runtime.js
    ember-runtime.min.js
    ember-runtime.prod.js
    ember-spade.js
    ember-template-compiler.js
    ember-template-compiler.min.js
    ember-template-compiler.prod.js
    ember-tests.js
    ember.js
    ember.min.js
    ember.prod.js


I heard Yehuda briefly mention `ember-runtime` at Ember Camp so that seemed like a
good place to start.  Within `ember-runtime.js` I found the following:

> Ember-Runtime is a framework that provides core functions for Ember including
> cross-platform functions, support for property observing and objects. Its focus
> is on small size and performance. You can use this in place of or along-side
> other cross-platform libraries such as jQuery.

> The core Runtime framework is based on the jQuery API with a number of
> performance optimizations.

Hmmm, that definitely sounds interesting. I recently found out about
[Zepto.js](http://zeptojs.com/) which aims to be a replacement for
[jQuery](http://jquery.com/) which supports **most** of the API but none of the
cruft to support legacy browsers. It sounds like perhaps `ember-runtime.js` is
doing something similar.

FWIW upon initial inspection `ember-runtime.js` appears to be light of
functionality for manipulating the DOM which makes it a poor replace for jQuery
IMO. On the other hand it appears to be a potential replacement for
[underscore.js](http://underscorejs.org/).

## ember-runtime.js

So what exactly is in [ember-runtime.js](http://emberjs.com/api/modules/ember-runtime.html)? Of course it's too much to cover in a
single post but here is the high level of the Classes and Namespaces:

* [Ember.Application](http://emberjs.com/api/classes/Ember.Application.html)
* [Ember.String](http://emberjs.com/api/classes/Ember.String.html)
* [Ember.ArrayController](http://emberjs.com/api/classes/Ember.ArrayController.html)
* [Ember.Controller](http://emberjs.com/api/classes/Ember.Controller.html)
* [Ember.ObjectController](http://emberjs.com/api/classes/Ember.ObjectController.html)
* [Function](http://emberjs.com/api/classes/Function.html)
* [Ember.Array](http://emberjs.com/api/classes/Ember.Array.html)
* [Ember.Comparable](http://emberjs.com/api/classes/Ember.Comparable.html)
* [Ember.Copyable](http://emberjs.com/api/classes/Ember.Copyable.html)
* [Ember.Deferred](http://emberjs.com/api/classes/Ember.Deferred.html)
* [Ember.Enumerable](http://emberjs.com/api/classes/Ember.Enumerable.html)
* [Ember.Evented](http://emberjs.com/api/classes/Ember.Evented.html)
* [Ember.Freezable](http://emberjs.com/api/classes/Ember.Freezable.html)
* [Ember.MutableArray](http://emberjs.com/api/classes/Ember.MutableArray.html)
* [Ember.MutableEnumerable](http://emberjs.com/api/classes/Ember.MutableEnumerable.html)
* [Ember.Observable](http://emberjs.com/api/classes/Ember.Observable.html)
* [Ember.SortableMixin](http://emberjs.com/api/classes/Ember.SortableMixin.html)
* [Ember.TargetActionSupport](http://emberjs.com/api/classes/Ember.TargetActionSupport.html)
* [Ember.ArrayProxy](http://emberjs.com/api/classes/Ember.ArrayProxy.html)
* [Ember.CoreObject](http://emberjs.com/api/classes/Ember.CoreObject.html)
* [Ember.Namespace](http://emberjs.com/api/classes/Ember.Namespace.html)
* [Ember.NativeArray](http://emberjs.com/api/classes/Ember.NativeArray.html)
* [Ember.Object](http://emberjs.com/api/classes/Ember.Object.html)
* [Ember.ObjectProxy](http://emberjs.com/api/classes/Ember.ObjectProxy.html)
* [Ember.Set](http://emberjs.com/api/classes/Ember.Set.html)
* [Ember.Error](http://emberjs.com/api/classes/Ember.Error.html)

There is some really stuff going on here but first a note on how Ember.js extends Javascript

> By default, Ember.js will extend the prototypes of native JavaScript objects in
> the following ways:

> * `Array` is extended to implement the `Ember.Enumerable`, `Ember.MutableEnumerable`,
> `Ember.MutableArray` and `Ember.Array interfaces`. This polyfills ECMAScript 5 array
> methods in browsers that do not implement them, adds convenience methods and
> properties to built-in arrays, and makes array mutations observable.
> * String is extended to add convenience methods, such as `camelize()` and `fmt()`.
> * `Function` is extended with methods to annotate functions as computed properties,
> via the `property()` method, and as observers, via the `observes()` or
> `observesBefore()` methods.

There is of course a way [to prevent this from happening](http://emberjs.com/guides/configuring-ember/disabling-prototype-extensions/) but it breaks a bunch of
the functionality that is the core strength of Ember.js so of course you'll need
to decide if you can sleep at night knowing that Javascript's core data types
are being extended under the hood..

Back to the cool stuff in `ember-runtime.js`

### Ember.String

#### camelize 

Returns the lowerCaseCamel form of a string.

    'innerHTML'.camelize();          // 'innerHTML'
    'action_name'.camelize();        // 'actionName'
    'css-class-name'.camelize();     // 'cssClassName'
    'my favorite items'.camelize();  // 'myFavoriteItems'

#### capitalize 

Returns the Capitalized form of a string

    'innerHTML'.capitalize();          // 'InnerHTML'
    'action_name'.capitalize();        // 'Action_name'
    'css-class-name'.capitalize();     // 'Css-class-name'
    'my favorite items'.capitalize();  // 'My favorite items'

#### classify 

Returns the UpperCamelCase form of a string.

    'innerHTML'.classify();          // 'InnerHTML'
    'action_name'.classify();        // 'ActionName'
    'css-class-name'.classify();     // 'CssClassName'
    'my favorite items'.classify();  // 'MyFavoriteItems'

#### dasherize 

Replaces underscores or spaces with dashes.

    'innerHTML'.dasherize();          // 'inner-html'
    'action_name'.dasherize();        // 'action-name'
    'css-class-name'.dasherize();     // 'css-class-name'
    'my favorite items'.dasherize();  // 'my-favorite-items'

#### decamelize 

Converts a camelized string into all lower case separated by underscores.

    'innerHTML'.decamelize();           // 'inner_html'
    'action_name'.decamelize();        // 'action_name'
    'css-class-name'.decamelize();     // 'css-class-name'
    'my favorite items'.decamelize();  // 'my favorite items'

#### fmt 

Apply formatting options to the string. This will look for occurrences of "%@"
in your string and substitute them with the arguments you pass into this method.
If you want to control the specific order of replacement, you can add a number
after the key as well to indicate which argument you want to insert.

Ordered insertions are most useful when building loc strings where values you
need to insert may appear in different orders.

    "Hello %@ %@".fmt('John', 'Doe');     // "Hello John Doe"
    "Hello %@2, %@1".fmt('John', 'Doe');  // "Hello Doe, John"

#### htmlSafe 

#### loc 

Formats the passed string, but first looks up the string in the localized
strings hash. This is a convenient way to localize text. See Ember.String.fmt()
for more information on formatting.

Note that it is traditional but not required to prefix localized string keys
with an underscore or other character so you can easily identify localized
strings.
    
    Ember.STRINGS = {
        '_Hello World': 'Bonjour le monde',
          '_Hello %@ %@': 'Bonjour %@ %@'
    };

    Ember.String.loc("_Hello World");  // 'Bonjour le monde';
    Ember.String.loc("_Hello %@ %@", ["John", "Smith"]);  // "Bonjour John Smith";

#### underscore 

More general than decamelize. Returns the lower_case_and_underscored form of a string.

    'innerHTML'.underscore();          // 'inner_html'
    'action_name'.underscore();        // 'action_name'
    'css-class-name'.underscore();     // 'css_class_name'
    'my favorite items'.underscore();  // 'my_favorite_items'

#### w

Splits a string into separate units separated by spaces, eliminating any empty
strings in the process. This is a convenience method for split that is mostly
useful when applied to the String.prototype.

    Ember.String.w("alpha beta gamma").forEach(function(key) {
        console.log(key);
    });

    // > alpha
    // > beta
    // > gamma
