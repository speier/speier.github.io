---
layout: post
title:  Introducing Material
date:   2013-06-10
image: /assets/article_images/2013-06-10-Introducing-Material/material.jpg
tags:
- node.js
---


As a self-proclaiming beginner DevOps ninja, last week I was need a tool to automate some of my system administration tasks. Basically I need to install Nginx, Node and Git to different machines. First I thought about [Chef](http://www.opscode.com/chef/), what we already using with Amazon's [OpsWorks](http://aws.amazon.com/opsworks/). But it turned out Chef is way to complicated for such a simple task.

Then my second obvious choice was [Fabric](http://fabfile.org), which is doing exactly what I need, streamlining the use of SSH process. The only problem was that I have to work on Windows client machines at my current work. Both Chef (Ruby) and Fabric (Python) is mainly written for *nix operating systems. However I really like Python (and Ruby as well), it's not that simple to use on Windows boxes. Probably you can make it work on Windows, but not as easy as I like to, with just a single command of a package manager without installing anything else.

So I decided to write my own tool in Node.js, because Node and npm works great on Windows as well. I've started hacking on this little utility over the weekend and I was able to create the basics. I can execute one or many tasks on different remote hosts in parallel. Currently the API only supports one single command `run` which executes the definied command on the remote host via SSH. It's easy to extend the API, we can simple `require` any node module into our `matfile` (more to come about matfile and the API in the next upcoming blog post).

The whole thing is heavily insipred by Fabric, so I tried to mimic the API as well, because I think Fabric's API is very well designed. The main difference is in the control flow, because it's Node, our commands are asynchronous, so using callback methods. I'm pretty busy adding new features, tests and refactoring. More to come in my next upcoming post. Please be patient.

Meanwhile you can check out the [code on GitHub](https://github.com/speier/material), it's licensed under the MIT license.
