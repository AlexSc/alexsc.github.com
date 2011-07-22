---
layout: post
title: A Real Ruby App
subtitle: Why You Should Use Heroku
---

[CAPTAIN FOREVER](http://www.captainforever.com/captainforever.php) is pretty
awesome. One of the neat things about it is you can export the ships you build
to an HTML format to share with your friends. ["Captain Noonat"](https://twitter.com/#!/noonat)
built the [VCD Archive](http://vcd.phuce.com/) for sharing ship designs.

You can check out the [source code](https://github.com/noonat/vcd) to VCD. It's
a pretty straightforward Sinatra app that uses a MySQL database for storage.
However, over the years [software erosion](http://en.wikipedia.org/wiki/Software_rot)
has taken hold and, sadly, the VCD Archive no longer works and Captain Noonat
doesn't know why. Even if we did know why -- how would we redeploy it? What
does it need? Where is everything configured?

Today we're going to rebuild the VCD Archive from the ground up in such a way
that we should be able to hold software erosion at bay, or at least quickly resolve
issues and redeploy the application years later. As additional constraints we
will only use free resources and we *won't* be using Heroku. This will be a
crash course in just how much work is really involved in building an application
that will *last*.

## Things to sign up for
Right off the bat you're going to need an [Amazon Web Services](http://aws.amazon.com)
account which is signed up for [EC2](http://aws.amazon.com/ec2/), [SimpleDB](http://aws.amazon.com/simpledb/),
and [S3](http://aws.amazon.com/s3/). This will last you through most of this
tutorial -- all the way to deploying version 1 in fact -- but if you'd like to get
a head start on other services we will be using you should also create free accounts for
- [Airbrake](https://airbrakeapp.com/account/new/Free)
- [Loggly](https://app.loggly.com/signup/#7:200)
- [Pingdom](http://www.pingdom.com/)

With that out of the way, let's get started!

## Grunt Work
Create a git repo for your application.

## Technology Choices
Before we write a single line of code we need to sort out some basic technology
choices.

## Repeatability and Isolation
It is important to have **known** and **isolated** environments. Since we'll be using
Ruby, [RVM](https://rvm.beginrescueend.com/) is perfect for this. If you have not already
done so, install RVM now.

We'll be using the latest version of Ruby 1.9.2 at the time of writing (July 21, 2011)
for this project, which is 1.9.2-p290. Simply run `rvm install 1.9.2-p290` to install it.
We'll also want a gemset for this project, `rvm gemset create vcd`.

Now, and this is important, we need a project .rvmrc to indicate that this project
should *always* use Ruby 1.9.2-p290 and the vcd gemset. Create a file named .rvmrc
in your project containing `rvm 1.9.2-p290@vcd`. Yes, even in production we will
be using RVM to manage our application environment. This is a Good Thing.
While we are dealing with repeatability and isolation, install [bundler](http://gembundler.com/).
We will be using bundler to manage dependencies for our application.

