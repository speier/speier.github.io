---
layout: post
title:  Playing with Edge.js
date:   2013-03-16
image: /assets/article_images/2013-03-16-Playing-with-Edgejs/cubes.jpg
tags:
- c#
- node.js
---

Today I have decided to try out [Edge.js](https://github.com/tjanczuk/edge), which allows to run `.NET` and `Node.js` code in-process. It's a great and very clever idea, we can reuse existing `.NET` class libraries in Node.js packages or applications. So I have created a small test project in `Node.js` to try out how can I call a `C#` class library's method.

To test it out I grab one of my old `C#` class, a Fibonacci series calculator. I've wrote this simple class for a programming challenge at my previous workplace, basically it allows to query for Fibonacci numbers using Linq. The task was to find out the *n* th term with 2012 digits, and with my implementation I was able to query Fibonacci terms in the following simple way:

```csharp
Fibonacci().First(x => x.Digits == 2012);
```

It seemed a good candidate to test `Edge.js`, so I modified my `C#` class a bit then compiled to dll.

![](http://s3.kalmanspeier.com/blog/xamarin_studio_fibolinq.png)
*editing the C# part with Xamarin Studio (my new favourite IDE for .NET projects)*

On the other hand the `Node.js` part is also fairly simple:

![](http://s3.kalmanspeier.com/blog/st2_fibolinq_edgejs.png)
*editing the Node.js part with Sublime Text 2 (still the best editor in my opinion)*

And here is the output of the `Node.js` app, using my compiled `C#` class library with `Edge.js`:

```bash
$ npm start

First Fibonacci term with 2012 digits: 9625th
```

This small test project is available [here](https://github.com/speier/playing-with-edgejs), on GitHub of course. ;)
