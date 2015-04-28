---
layout: post
title:  Visit required files in Node.js
date:   2012-05-06
image: /assets/article_images/2012-05-16-Visit-required-files-in-Nodejs/path.jpg
tags:
- node.js
---

After a few hours of rambling finally I got a working `node-visitor`. Which recursively visits every required module starting from the definied entry point.

Behind the scenes using [node-detective](https://github.com/substack/node-detective) to find all require calls and `Node` core module to resolve filename. Maybe I will create a package in the future as it gets more mature. In the meantime I have created a simlpe gist demonstrating the core function. Enjoy! ;)

```javascript
var fs = require('fs');
var path = require('path');
var Module = require('module');
var detective = require('detective');
 
// node-visitor
 
function visit(request, parent) {
  var fn;
  try {
    fn = require.resolve(request);
  } catch (err) {
    fn = Module._resolveFilename(request, parent);
  }
  if (!path.existsSync(fn)) {
    return;
  }
  console.log(fn);
  var src = fs.readFileSync(fn);
  var requires = detective(src);
  requires.forEach(function(item) {
    visit(item, {
      id: request,
      filename: fn
    });
  })
};
 
visit('../lib/application');
```
