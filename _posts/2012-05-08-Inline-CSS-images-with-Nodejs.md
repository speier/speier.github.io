---
layout: post
title:  "Inline CSS images with Node.js"
date:   2012-05-08
categories: node.js
image: /assets/article_images/2012-05-08-Inline-CSS-images-with-Nodejs/cascading-waterfall.jpg
---

While developing a new JS framework at my workplace *(unfortunately non open source)*, I'm using [Node.js](http://nodejs.org/) to handle all dependencies (thanks to [npm](http://npmjs.org)) and the build process (thanks to [jake](https://github.com/mde/jake)). The other day we have decided to write a simple `jake` task which gives us the ability to include `Base64` encoded images into `CSS` files on build.

The biggest advantage of this technique is that you could have only one CSS file with all your images included. There are few disadvantages as well, the CSS file could be much bigger and indeed you can't cache your image files separately anymore, but you can cache the CSS file instead, so it won't be a problem. Not decided yet which will be the default option in future releases, but at least we have the option to embed images. :)

Please find this tiny function below  *(copied from the build script)*:

```javascript
var fs = require('fs');
var path = require('path');
 
function cssIncImages(cssFile) {
	var imgRegex = /url\s?\(['"]?(.*?)(?=['"]?\))/gi;
	var css = fs.readFileSync(cssFile, 'utf-8');
	while (match = imgRegex.exec(css)) {
		var imgPath = path.join(path.dirname(cssFile), match[1]);
		try {
			var img = fs.readFileSync(imgPath, 'base64');
			var ext = imgPath.substr(imgPath.lastIndexOf('.') + 1);
			css = css.replace(match[1], 'data:image/' + ext + ';base64,' + img);
		} catch (err) {
			console.log('Image not found (%s).', imgPath);
		}
	}
	// fs.writeFileSync(cssFile, css, 'utf-8'); // you can overwrite the original file with this line
	return css;
}
```
