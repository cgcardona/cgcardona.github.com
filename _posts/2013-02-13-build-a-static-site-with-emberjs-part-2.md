---
layout: post
title: "Build a static site with Ember.js part 2"
description: ""
category: 
tags: ['emberjs', 'javascript', 'code', 'handlebars']
---
{% include JB/setup %}

## TLDR

Yesterday I wrote [Build a static site with
Ember.js](/2013/02/12/build-a-static-site-with-emberjs/). This morning I saw
[this fine post](http://twbrandt.github.com/) on Twitter which shows how to create a rudimentary model and
dynamic segments on urls so I figured I'd take that code and flesh out my
example.

You can see the [live example](http://ember-static.herokuapp.com/) of this code
on heroku and you can get a copy of this code by [cloning this repo](https://github.com/cgcardona/ember_static) on github.

## Update your Routes

Open `app/assets/javascripts/router.js` and add the following two routes.
    
    this.route("contributors")
    this.route("contributor", { path : "/contributors/:contributor_id" })

The first route should look familiar from part 1. The second path maps to a
`contributor` route. Notice `:contributor_id`. This is what's called a 'dynamic segment' in Ember.js.

## Create the `contributor` model

Open `app/assets/javascripts/models/contributors_model.js`

    EmberStatic.Contributor = Ember.Object.extend();
    EmberStatic.Contributor.reopenClass({
      allContributors : [],
      all : function(){
        this.allContributors = [];
        $.ajax({
          url : 'https://api.github.com/repos/emberjs/ember.js/contributors',
          dataType : 'jsonP',
          context : this,
          success : function(response){
            response.data.forEach(function(contributor){
              this.allContributors.addObject(EmberStatic.Contributor.create(contributor));
            }, this);
          }
        });
        return this.allContributors;
      }
    });

This just creates a `Contributor` object which extends the core EmberJS
`Object`. It then adds an `all` method which makes a `GET` request to github
asking for a list of all contributors to EmberJS.

If the `GET` request is successful the `response` is looped over and added to
the `allContributors` array via [Ember.MutableEnumerable](http://emberjs.com/api/classes/Ember.MutableEnumerable.html)'s
[addObject](http://emberjs.com/api/classes/Ember.MutableEnumerable.html#method_addObject)
method passing in an Object created by calling `Ember.Object`'s [create method](http://emberjs.com/api/classes/Ember.Object.html#method_create).

## Wire in the Model

Now we customize our route to tell it about our model. Open
`app/assets/javascripts/routes/contributors_route.js` and add

    EmberStatic.ContributorsRoute = Ember.Route.extend({
      model : function(){
        return EmberStatic.Contributor.all();
      }
    });

Now the `contributor` route is associated with the `Contributor` model and `all`
method.

## Create a `contributors` template

Create and open `app/assets/javascripts/templates/contributors.hbs` and add

    <p>Contributors</p>
    <ul>
    { { #each contributor in controller} }
      <li>{ { #linkTo contributor contributor } } { { contributor.login } } { { /linkTo } }</li>
    { { /each } }
    </ul>

Because the previous step made the connection between `contributor` and the
`Contributor`'s `all` method in this template we can do a handlebars `each`
method to loop over the contributors array and create a list item for each
contributor.

The handlebars `#linkTo` takes two arguments. First the route and second the id
of the contributor. The text of the generated link will be the user's github
login name.

## Create a `contributor` template

In the Route file we create a route for `contributors` and `contributor` so
we'll need to create a template for `contributor` as well.

Create and open `app/assets/javascripts/templates/contributor.hbs` and add:

    Contributor: { { login } }, contributions: { { contributions } }

And that's all the code you need to write.
