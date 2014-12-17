---
layout: post
title:  "Sidekiq + Whenever = Superpower"
date:   2014-12-17 22:00:37
categories: rails cron sidekiq whenever
---


I have a read a value on a distant server frequently (for example I have to check some bank account upcoming status)


## The first solution : [Whenever](https://github.com/javan/whenever){:target="_blank"}
After some search, I found whenever. It's really easy to install and use.

I create a folder name cron into my app folder :

![sidekiq cron folder](/public/sidekiq-cron-folder.png "Sidekiq cron folder")

I just add a simple class on it.

And in my schedule.rb file follow the example :

{% highlight ruby %}
every 15.minutes do #Check frequently
  runner "MyCron.some_process"
  runner "MyCron.foo"
  runner "MyCron.bar"
end
{% endhighlight %}

and my cron/my_cron.rb

{% highlight ruby %}
class MyCron
    def self.some_process
        puts "Do something cool"
    end
    def self.foo
        puts "foo"
    end
    def self.bar
        puts "bar"
    end
end
{% endhighlight %}

I put it in production and that my server became slow.

After some checks, I realised that every 15 minutes, my server launch **TREE** full rails environment just to print "Do something cool", "foo", "bar"

By this way, it consume a lot a memory and CPU to do simple thing.

## The second solution : add [Sidekiq](http://sidekiq.org/){:target="_blank"}

Sidekiq allow you to run task in background.

It also have a very powerful queue system. And it easy to use.

After installing Sidekiq, I do some modifications on my class to include Sidekiq on it :

{% highlight ruby %}
class MySomeProcessCron
    include Sidekiq::Worker
    def perform #No more self!
        puts "Do something cool"
    end
end
{% endhighlight %}
{% highlight ruby %}
class MyFooCron
    include Sidekiq::Worker
    def perform #No more self!
        puts "foo"
    end
end
{% endhighlight %}
{% highlight ruby %}
class MyBarCron
    include Sidekiq::Worker
    def perform #No more self!
        puts "bar"
    end
end
{% endhighlight %}

I also change my schedule.rb

{% highlight ruby %}
#Create a job_type named sidekiq
job_type :sidekiq, "cd :path && :environment_variable=:environment bundle exec sidekiq-client push :task :output"

every 15.minutes do #Check frequently
  sidekiq "MySomeProcessCron" #Just the class name here
  sidekiq "MyFooCron"
  sidekiq "MyBarCron"
end
{% endhighlight %}

To make it work, you will need to add sidekiq-client-cli to your gemfile :

{% highlight ruby %}
#...
gem 'sidekiq-client-cli'
#...
{% endhighlight %}

That's it :)
All your cron job will now :

- Being queued, So it doesn't go crazy on CPU en ram.
- [Retry if failed](https://github.com/mperham/sidekiq/wiki/Error-Handling){:target="_blank"}.
- [Monitoring](https://github.com/mperham/sidekiq/wiki/Monitoring){:target="_blank"}.