---
layout: post
title:  "Firebase, why you should at least try it ? "
date:   2015-01-16 12:00:37
categories: firebase javascript real-time
---

A few month from now, I was looking to add some real time feature to a website.

I found bunch of stuff, like [pusher](https://pusher.com/), [socket.io](http://socket.io/) and of course **[Firebase](https://www.firebase.com/)**


## The 2 main reasons why you should try (and use) Firebase :



### It sync an save at the same time

If you have a basic CRUD app (or website), you will have to add some real time feature in the future (most website are doing it). So why don't you take a real time ready solution right now?

If you write a real time website (or app), you will have to store the data in the future. So why don't you choose a both real time / storage solution right now?

Of course, Firebase works with most known web and mobile technologies : 

* Angular
* Ember
* Ract
* Backbone
* IOS
* Android
* REST
* ...


In fact, working with Firebase is like having a dropbox in your web page. *(I should say a google drive, because Firebase is a Google company)*

![firebase dropbox html](/public/firebase_dropbox_html.jpg "Firebase equals a dropbox into html page")


You put stuff you want to save/synch on it and that's it! Firebase handle everything for you. If you are offline, it will try to sync it when you are back online :) 
Here is an example how simple it is : 

{% highlight javascript %}
myFirebaseRef.set({
  title: "Hello World!",
  author: "Me"
});
{% endhighlight %}


Of course, reading data is always done in the sync way : 

{% highlight javascript %}
myFirebaseRef.child("location/city").on("value", function(snapshot) {
  alert(snapshot.val());  // Alerts "San Francisco"
});
{% endhighlight %}



<div class="message">
	<a href="https://www.firebase.com/docs/web/quickstart.html" target="_blank">
"In the example above, the value event will fire once for the initial state of the data, and then again every time the value of that data changes."
</a>
</div>


So if you want to focus more on the value you provide to your customer, and less on technical issues. [Let's go.](https://www.firebase.com/) 



### Firebase is also an hosting solution :)

The first time I read about this feature, I did not realise how cool it is.

When you're a developer, hosting stuff is offen a huge pain.

* How to choose the right offer?
* How will I maintain it?
* How much time am I going to spend on it ? (more than you think...)
* Are my servers under attack?

If you are in a small structure, and you are the only tech guy, you will have to answer all this question. It's gonna take time and money.

At a moment, you will open your eyes and say : Why am I spending all that energy to try to understand this linux stuff ? I don't even care about it, I'm not a system administrator.

And that's the moment you will have to hire a system an network administrator.


[Try a server less solution, allowing you to deploy you app in a single code line?](https://www.firebase.com/)


## A few things that might be improved in Firebase :

### Having an hacker plan with a custom domain


When you start a simple MVP,

* You have spent weeks to find the name of your product.
* You're so proud to buy our own domain name.
* You set up your really simple MVP.
* You deploy it with the hacker plan (for free).
* You want to communicate about your MVP, to start getting feedback.
* But if you want people to try your MVP on the domain name you own, you have to spend 50$/month
* At this point, you didn't raised any money, your MVP is really really light, the traffic on your website is really really low (normal : it's the beginning :)
* So you decide to host this MVP on a simple server for almost free (like Digital Ocean, Heroku, GitHub Pages, etc...)
* And you think you will switch later, when the next feature is coming, because you really want to enjoy all Firebase great features.
* But when it's happen, you start to think : can I stand on my 5$ host, or do I have to spend 50$ now?
* Of course one day you will switch to an other solution when you start to get people interested about what you do.
* But at this time, how much will you spent to switch to Firebase?

So please Firebase, think about adding custom domain for Hacker plan or create a **spark plan** : Hacker plan + custom domain for about *5$/month*.

![firebase spark](/public/firebase-spark-plan.jpg "Firebase spark")


### Adding a storage like AWS Glacier


Having synchronized/stored data is awesome.
I think it's definitely why Firebase is one a the most powerful tool I have ever seen.
But when you think about it, there is this kind of data you have to keep, but you'll never need to synchronize it.
For example :

* A 2 years old invoice
* Connections log outdated

In fact, as you website is getting older, you have all this data you want to "Archive". That means :

* I really want to keep it.
* I don't care if I have to wait few minutes (may be more) to access it.
* It will be great to pay less (and/or have more space available) to store it.

![firebase glacier](/public/firebase-glacier.jpg "Firebase glacier")