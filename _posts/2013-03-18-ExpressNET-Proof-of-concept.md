---
layout: post
title:  "Express.NET: Proof of concept"
date:   2013-03-18
categories: c#
image: /assets/article_images/2013-03-18-ExpressNET-Proof-of-concept/train.jpg
---


In the last few weeks I was working on a `Node.js` side project to explore `JavaScript` as a back end alternative. But today I've decided to play a bit with `C#`, before I forget my good old friend.

I really like [Express.js](http://expressjs.com) and I think it would be great if the `.NET` ecosystem could have something similar lightweigth web framework. My basic idea was that I will try to implement a small subset of Express' API in `C#`, following their `JavaScript` syntax as close as possible. So at least I can create an application and define routes with callback functions.

Here is an example:

```csharp
var app = new Express ();

app.Get ("/", (req, res) => {
    res.Send ("hello world");
});
```

Beyond the above very simple example, finally I was able to implement a few other things as well, like basic support for middlewares, request parameters and `JSON` serialization. Still very early to say anything, but looks promising. Definitely not for production, but would be useful for prototyping. That's it for today. Hopefully I will find some spare time to hack in this small project in the future.

Express.NET is available [here](https://github.com/speier/expressnet).

![](http://s3.kalmanspeier.com/blog/expressnet_editing_xs.png)
*editing the Express.NET sample application with Xamarin Studio*
