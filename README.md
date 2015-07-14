### jQuery Lazy - Delayed Content, Image and Background Loader
[![GitHub version](https://badge.fury.io/gh/eisbehr-%2Fjquery.lazy.svg)](http://github.com/eisbehr-/jquery.lazy)
[![NPM version](https://badge.fury.io/js/jquery-lazy.svg)](http://www.npmjs.org/package/jquery-lazy)
[![Bower version](https://badge.fury.io/bo/jquery-lazy.svg)](http://bower.io/search/?q=jquery-lazy)
[![Dependency version](https://david-dm.org/eisbehr-/jquery.lazy.png)](https://david-dm.org/eisbehr-/jquery.lazy)

---

### Table of Contents
* [About](#about-jquerylazy)
* [Compatibility](#compatibility)
* [Documentation / Examples](#documentation--examples)
* [Installation](#installation)
  * [CDN](#cdn)
  * [Self-Hosted](#self-hosted)
  * [Package Managers](#package-managers)
* [Basic Usage](#basic-usage)
* [Callbacks / Events](#callbacks--events)
* [Instances and public Functions](#instances-and-public-functions)
* [Custom Content Loaders](#custom-content-loaders)
* [Bugs / Feature request](#bugs--feature-request)
* [License](#license)

---

## About jQuery.Lazy();
Lazy is a fast, feature-rich and lightweight delayed content loading plugin for jQuery. 
It's designed to speed up page loading times and decrease traffic to your users by only loading the content in view. 
You can use Lazy in all vertical and horizontal scroll ways.
It supports images in `<img/>` tags and backgrounds, supplied with css like `background-image`, by default or any other content by [custom loaders](#custom-content-loaders). 
On images Lazy can set an default image or a placeholder while loading and supports retina displays as well.


## Compatibility
Lazy will work with a wide range of browsers and support jQuery versions for years backwards. 
You can pick any version since jQuery 1.7.0 or greater.
There is no way to guarantee, that Lazy will work with all browsers, but all I've tested worked great so far.
If you find any problems in specific browsers, please let me know. 

**Tested in:** IE 6-11, Chrome (mobile), Firefox (mobile), Safari (mobile) and Android Browser.


## Documentation / Examples
For [documentation](http://jquery.eisbehr.de/lazy/#parameter), 
[examples](http://jquery.eisbehr.de/lazy/#examples) and other information take a look on the [project page](http://jquery.eisbehr.de/lazy/).


## Installation
First of all, you will need a copy of [jQuery](http://jquery.com) to use Lazy successfully on your project. If you get this you can install Lazy by different ways. Some examples below:

#### CDN
Lazy is available over [cdnjs](http://cdnjs.com) and [jsDelivr](http://jsdelivr.com) CDN and can directly included to every page.
```HTML
<!-- cdnjs -->
<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/jquery.lazy/0.6.0/jquery.lazy.js"></script>

<!-- jsDeliver -->
<script type="text/javascript" src="//cdn.jsdelivr.net/jquery.lazy/0.6.0/jquery.lazy.min.js"></script>
```

#### Self-Hosted
[Download](https://github.com/eisbehr-/jquery.lazy/archive/master.zip) and save one of two available files to include Lazy to your page, either the [development](http://raw.githubusercontent.com/eisbehr-/jquery.lazy/master/jquery.lazy.js) or the [minified](http://raw.githubusercontent.com/eisbehr-/jquery.lazy/master/jquery.lazy.min.js) version.
```HTML
<script type="text/javascript" src="jquery.lazy.min.js"></script>
```

#### Package Managers
Lazy is even available through [NPM](http://npmjs.org) and [Bower](http://bower.io). Just use one of the following commands below:

[![NPM](https://nodei.co/npm/jquery-lazy.png?compact=true)](https://nodei.co/npm/jquery-lazy/)
```sh
$ npm install jquery-lazy
$ bower install jquery-lazy
```


## Basic Usage
1.) The basic usage of Lazy ist pretty easy.
First of all you need to add a `data-src` attribute to those images you want to load delayed and insert the image path you want to load over Lazy.
Best practice is to add a blank image to the `src` attribute: 
```HTML
<img class="lazy" data-src="path/to/image_to_load.jpg" src="" />
```

2.) Start using Lazy by calling it after page load.
You don't have to specify your elements. 
But for better performance, or different options, 
load your images over unique classes or any other jQuery selector. 
```JS
$(function() {
    $("img.lazy").Lazy();
});
```
Take a look at the [documentation](http://jquery.eisbehr.de/lazy/) to get an idea what Lazy is capable of.


## Callbacks / Events
Lazy comes with a bunch of [callbacks and events](http://jquery.eisbehr.de/lazy/index.php?c=callback) you can assign to.
Just add them by initialization settings:
* `beforeLoad` - before item is about to be loaded
* `afterLoad` - after the item was loaded successfully
* `onError` - whenever an item could not be loaded
* `onFinishedAll` - after all item in instance was loaded or returned an error


## Instances and public Functions
This plugin supports multiple parallel instances.
Just initialize them with different selectors on jQuery.
To access an instances public functions you can initialize them in an object oriented manner or grab the instance bind to every element by default:
```JS
// object oriented way
var instance = $("img.lazy").Lazy({chainable: false});

// grab from elements (only works well if you use same selectors)
$("img.lazy").Lazy();
var instance = $("img.lazy").data("plugin_lazy");
```

Every instance has some public available functions to control its behavior.
There are currently six available:
```JS
instance.config(entryName[, newValue]); // get or set an configuration entry
instance.addItems(items); // add new items to current instance
instance.getItems(); // get all unhandled items left of current instance
instance.update([useThrottle]); // loads all images in current viewport
instance.loadAll(); // loads all remaining available images from this instance
instance.destroy(); // unbinds all events and stop execution directly
```


## Custom Content Loaders
With the custom loaders option there is a powerful solution to load every contents the Lazy way.
The plugin will handle everything, you just create a loading method witch got triggered whenever the element hits the visibility threshold.
It is still possible to load images and custom loaders in the same Lazy instance.

To use this just define a loader function inside the Lazy initialisation and pass the loader name to the `data-loader` attribute of the elements witch should be lazy loaded.
```HTML
<div class="lazy" data-loader="customLoaderName"></div>
<img class="lazy" data-src="path/to/image_to_load.jpg" src="" />
<div class="lazy" data-loader="customLoaderName"></div>
<div class="lazy" data-loader="asyncLoader"></div>
```
```JS
$(".lazy").lazy({
    // callback
    beforeLoad: function(element) {
        console.log("start loading " + element.prop("tagName"));
    },

    // custom loaders
    customLoaderName: function(element) {
        element.html("element handled by custom loader");
        element.load();
    },
    asyncLoader: function(element, response) {
        setTimeout(function() {
            element.html("element handled by async loader");
            response(true);
        }, 1000);
    }
});
```


## Bugs / Feature request
Please [report](http://github.com/eisbehr-/jquery.lazy/issues) bugs and feel free to [ask](http://github.com/eisbehr-/jquery.lazy/issues) for new features directly on GitHub.


## License
Lazy is dual-licensed under [MIT](http://www.opensource.org/licenses/mit-license.php) and [GPL-2.0](http://www.gnu.org/licenses/gpl-2.0.html) license.
