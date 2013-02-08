---
layout: post
title: "Cents Us Dollars Them"
description: ""
category: 
tags: []
---
{% include JB/setup %}

Exploring the distribution of wealth in the United States with data from the [US Census API](http://www.census.gov/developers/) for the [Aaron Swartz Memorial Hackathon](https://www.noisebridge.net/wiki/Aaron_Swartz_Memorial_Hackathon)

See this live: [http://cents-us-dollars-them.herokuapp.com/](http://cents-us-dollars-them.herokuapp.com/)

## Setup

1. Clone a copy of the git repo to your local machine

    git clone git@github.com:cgcardona/cents_us.git

2. Make sure you [request an api key](http://www.census.gov/developers/tos/key_request.html)

3. We're gonna wanna stash that api key somewhere private so that noone else can get their hands on it

Because I'm running the app on [Heroku](http://www.heroku.com) I'm using [this method](https://devcenter.heroku.com/articles/config-vars)

Start by installing the `foreman` gem from heroku

    gem install foreman

> [Foreman](https://github.com/ddollar/foreman) is a command-line tool for running Procfile-backed apps. It’s installed
> automatically by the Heroku Toolbelt, and also available as a Ruby gem.

You need to create a `Procfile` with something similar to the following:

    web: bundle exec rails server -p $PORT

Now create a `.env` file with your config vars

    AUTH_KEY=1111111111333333333333333333333777777777777

Once you've got this set up then you start WEBrick with

    foreman start

Also you'll want to put your auth key on heroku with

    heroku config:add AUTH_KEY=1111111111333333333333333333333777777777777

Make sure to add `.env` to your `.gitignore` file so that your config vars don't
get checked into version control

## Sources of Data

[US Census API Homepage](http://www.census.gov/developers/)

[2010 Census Summary File 1 (SF1)](http://www.census.gov/developers/data/sf1.xml)

[American Community Survey 5 Year Data](http://www.census.gov/developers/data/acs_5yr_2011_var.xml)

## Gems we're using

This is a list of gems that I've added for this project. I'm not listing the gems that come out of the box with rails in the interest of brevity

`'underscore-rails', '~> 1.4.3'`

`'haml-rails', '~>0.3.5'`

`'d3js-rails'`

`'bootstrap-sass'`

Check out the [Gemfile](https://github.com/cgcardona/cents_us/blob/master/Gemfile) for more info

## Misc

More stuff here soon...

## Who's behind this?!

Relax. It's just me, Carlos Cardona. [Follow me on Twitter](http://twitter.com/cgcardona)