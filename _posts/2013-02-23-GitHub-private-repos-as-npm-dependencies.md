---
layout: post
title:  "GitHub private repos as npm dependencies"
date:   2013-02-23
image: /assets/article_images/2013-02-23-GitHub-private-repos-as-npm-dependencies/octocat.jpg
tags:
- github
- npm
---

As I'm working with Node.js I have a few modules what I'd like to share between different applications. Let's say I have a module with a few common middlewares for [Express](http://expressjs.com) which I want to reuese time to time. npm is a great tool to resolve dependencies but what if my apps and modules are private?
If you have many private repos you can consider to setup your own npm registry,
but it's seems a bit overkill for me so I decided to figure out a simpler way.

Luckily [npm](https://npmjs.org) supports [URLs as dependencies](https://npmjs.org/doc/json.html) and [GitHub](https://github.com) have a nice API. With the previous two facts we will be able to resolve private dependencies.

First we need to create a GitHub API token (help available [here](https://help.github.com/articles/creating-an-oauth-token-for-command-line-use)). As soon as we have a valid token we can use GitHub API's [get archive link](http://developer.github.com/v3/repos/contents/#get-archive-link) method to get our private repo.

So we can add private repos as dependencies to our `package.json` in the following format:

```json
"dependencies": {
  "foo": "https://api.github.com/repos/johndoe/foorepo/tarball/master?access_token=xyz"
}
```
