---
layout: post
title:  "How to provide assets on a Rails Projects?"
date:   2015-04-15 19:00:37
categories: rails assets
---

Hey there! we are going to talk about how to put assets on your RoR project. Most of the time, when you start learning Ruby On Rails, you will follow some course encouraging you to add common javascript/css library like [Bootstrap](http://getbootstrap.com/) or [jQuery](https://jquery.com/). There are many ways to include it into your app. We are going to look at 4 common ways.

{:toc}

----------

Use GemFile to handle it 
--
This is the most common way. Even when you start a new project

{% highlight bash %}
$ rails new myapp
{% endhighlight %}


You can see jQuery and turbolink are added this way in your GemFile : 

{% highlight ruby %}
# Use jquery as the JavaScript library
gem 'jquery-rails'
# Turbolinks makes following links in your web application faster. Read more: https://github.com/rails/turbolinks
gem 'turbolinks'
{% endhighlight %}


**Pro**

- It's the default rails behavior, so it's a good way to fit to it
- Most of the popular assets library are available this way

**cons**

- There is no naming convention, so when looking at the GemFile, it's not easy to see what is an "asset gem" and when is not
- The gem versioning is not following the asset lib versioning so jQuery-rails 4.0.3 (the gem) contains jQuery (the js) 1.11.2 and jQuery 2.1.3 (Imagine the headache in a 2 years old project with douzaines of "asset gem")
-  The is no way to check on your GemFile if a gem is an "asset gem" or not. I always try to keep my GemFile as clean and as light as possible. So when it's possible to remove something, I do. But to be able to do this, you have to know what are your gem for. It's not always easy when project are going big and/or old.
- Not all assets library are available. When we want to try a new cools JS library still in early stage, most of the time you have to deal with "How do I package it to my Ror Project". And often at the beginning "What is this npm stuff every body talk about?" So you will falling back to the next section.

Copy/Paste the source file into your app
--
Assets are "just files". They will be minified and handle by asset pipeline, but they are just files. 
As far as you write some of them why can't you just copy/paste vendor library and let them live their life among your own assets? 
If you want to be clean, there is even a folder in rails app for that : you can put them under vendor/assets. You can check this into [the official rails documentation](http://guides.rubyonrails.org/asset_pipeline.html#asset-organization). 

**Pro**

- It's a no time needed solution. Can be helpful to test something really quickly.
- You can deal with all the assets library you will find out.

**cons**

- There is no dependency system. Meaning you will have to deal with dependancies on you own.
- There is no versioning system. Meaning you will have to update your asset lib by your own.
- This is not at all the cleanest way to deal with this.

Bower-Rails
--
[Bower](http://bower.io/) is a package manager for assets libraries. It is used by [NodeJs](https://nodejs.org/). 
It's working mostly like our GemFile but for assets libraries. If you try a simple NodeJs project, you will see how it's simple and clear to handle assets librairies with it. And if you are on a RoR project, [Bower-Rails](https://github.com/rharriso/bower-rails) allow you to take advantage of bower into your Rails app.

**Pro**

- Mostly every assets libraries are available with bower
- It handles versioning and dependancies the good way
- You can keep your GemFile clean and have a bower.json file the handle assets libraries

**cons**

- You pull the bower structure into your rails app
- You have to be careful during deploy, some task should be updated to deal with this new process (especially on Heroku)
- You may change config on your asset pipeline to deal with the bower structure

Rails Assets
--
[Rails Assets](https://rails-assets.org/) is the simple way to transform banana to apple ;)
It allow you to handle your assets libraries with the power of bower but directly in your GemFile

**Pro**

- Mostly every assets libraries are available with bower
- It handles versioning and dependancies the good way
- You can keep your GemFile clean because all Rails-assets dependencies are easy to detect

**cons**

- Work only with bundler >= 1.8.4
