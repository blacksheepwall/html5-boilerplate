[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation
table of contents](README.md)

# 扩展与定制 HTML5 Boilerplate

这里有几条增强项目质量的建议，并不是所有开发者都有需求，所以我们默认不将其至于模板中。


## DNS 预获取

简言之，DNS 预取是一项性能优化技术。载入页面的过程中，浏览器解析到网页上包含的网址时，会在用户访问它们之前在后台对这些网址后所包含的主机名进行域名解析，等到页面载入完毕或者用户真正去点击这些网址时，相对应的 DNS 解析工作已经提前完成了，不会在用户点击后才开始解析 DNS。对于那些原本 DNS 解析较慢的用户能明显感觉到提速。

### 隐性的资源预获取 (Implicit prefetches)

当浏览器发现页面上的某些链接不属于当前域下，会利用空闲时间自动预取一些资源。客户端首先检查本地缓存，如果没找到，那么会向 DNS 服务器请求资源，这些操作会在后台执行，不会影响页面的渲染与脚本的执行。

该手段目的是为了提高访问速度，而且相比不预取时会发送更少的请求，在移动端优化效果会更明显。

#### 禁用隐性的资源预获取 (implicit prefetching)

```html
<meta http-equiv="x-dns-prefetch-control" content="off">
```

有了 X-DNS-Prefetch-Control meta 标签 (或者是 http header) ，浏览器仍然会进行预获取。
在 Chrome 中，可以通过在地址栏输入 about:histograms/DNS 来观测一些有趣的 DNS 性能数据。[（出处）](http://www.dbanotes.net/web/dns_prefetching.html)

**_警告:_** 如果你的站点很依赖外域资源的话，这么做会拖慢站点。

### 显性的资源预获取 (Explicit prefetches)

一般来说浏览器只会扫面外域的 HTML 内容。如果站点所需的资源在 HTML 之外（需从远程服务器或者 CDN 加载来的一段 js，这段 js 并不会出现在站点所有页面），那么这些资源预获取将会进入加载队列中去。

```html
<link rel="dns-prefetch" href="//example.com">
<link rel="dns-prefetch" href="//ajax.googleapis.com">
```

你可以任意使用以上标签，但如果将其至于 [Meta
Charset](https://developer.mozilla.org/en/HTML/Element/meta#attr-charset) 元素后就更好了（这些标签需出现在 `head` 标签之前），如此一来浏览器会立即做出（加载样式表、脚本等）反应。

#### 链接的预获取

Amazon S3:

```html
<link rel="dns-prefetch" href="//s3.amazonaws.com">
```

Google APIs:

```html
<link rel="dns-prefetch" href="//ajax.googleapis.com">
```

Microsoft Ajax Content Delivery Network:

```html
<link rel="dns-prefetch" href="//ajax.microsoft.com">
<link rel="dns-prefetch" href="//ajax.aspnetcdn.com">
```

### 支持 DNS 预获取的浏览器

Chrome, Firefox 3.5+, Safari 5+, Opera （未知）, IE 9 （被称为 "Pre-resolution" 见  blogs.msdn.com）

### 关于 DNS 预获取的更多信息

* https://developer.mozilla.org/En/Controlling_DNS_prefetching
* http://dev.chromium.org/developers/design-documents/dns-prefetching
* http://www.apple.com/safari/whats-new.html
* http://blogs.msdn.com/b/ie/archive/2011/03/17/internet-explorer-9-network-performance-improvements.aspx
* http://dayofjs.com/videos/22158462/web-browsers_alex-russel


## 搜索

### 让搜索引擎直接访问站点地图 （sitemap）

[如果制作一份 sitemap](http://www.sitemaps.org/protocol.php)

```html
<link rel="sitemap" type="application/xml" title="Sitemap" href="/sitemap.xml">
```

### 隐藏页面，不让搜索引擎抓取到

根据 Heather Champ 的理论，你不应该直接将 "Contact Us" 或 "Complaints" 页面暴露给搜索引擎， This is an HTML-centric way of achieving that.

```html
<meta name="robots" content="noindex">
```

**_WARNING:_** DO NOT INCLUDE ON PAGES THAT SHOULD APPEAR IN SEARCH ENGINES.

### Firefox 和 IE 的搜索插件

强烈建议那些具备站内搜索功能的站点配置一个搜索插件，该插件是一段定义搜索引擎行为准则的 XML 文本。[如何制作搜索插件](http://www.google.com/search?ie=UTF-8&q=how+to+make+browser+search+plugin).

```html
<link rel="search" title="" type="application/opensearchdescription+xml" href="">
```


## Internet Explorer

### 在 IE10 Metro 中提示用户切换到桌面模式

Metro 模式下的 IE10 并不支持类似 flash 的插件，此时可以通过 X-UA-Compatible meta 标签告知用户手动切换至桌面模式。


```html
<meta http-equiv="X-UA-Compatible" content="requiresActiveX=true">
```

H5BP 默认的 X-UA-Compatible 值是这样的：

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1,requiresActiveX=true">
```

更多信息，请查阅 [Microsoft's IEBlog post about prompting for
plugin use in IE10 Metro
Mode](http://blogs.msdn.com/b/ie/archive/2012/01/31/web-sites-and-a-plug-in-free-web.aspx)。

### IE 的固定站点 (Pinned Sites IE9+)

该功能可以将网页嵌入到 Windows 的工具条上，并提供一系列的快捷操作，参考[文档](http://msdn.microsoft.com/en-us/library/gg131029.aspx) 以及 [http://msdn.microsoft.com/zh-cn/library/gg491738(v=vs.85)]()

### 为固定站点命名

如果不对其进行命名， Windows 会使用页面的 title 名作为应用名。

```html
<meta name="application-name" content="Sample Title">
```

### 给固定站点设置 tooltip

```html
<meta name="msapplication-tooltip" content="A description of what this site does."> 
```  

参考 [http://blog.sina.com.cn/s/blog_4515673f0100npkg.html]() [http://blog.csdn.net/cuixiping/article/details/6885310]()

### 为固定站点设置一个默认页

`http://www.example.com/index.html?pinned=true`

```html
<meta name="msapplication-starturl" content="http://www.example.com/index.html?pinned=true">
```

### Recolor IE's controls manually for a Pinned Site

IE9+ will automatically use the overall color of your Pinned Site's favicon to
shade its browser buttons. UNLESS you give it another color here. Only use
named colors (`red`) or hex colors (`#ff0000`).

```html
<meta name="msapplication-navbutton-color" content="#ff0000">
```

### Manually set the window size of a Pinned Site

If the site should open at a certain window size once pinned, you can specify
the dimensions here. It only supports static pixel dimensions. 800x600
minimum.

```html
<meta name="msapplication-window" content="width=800;height=600">
```

### Jump List "Tasks" for Pinned Sites

Add Jump List Tasks that will appear when the Pinned Site's icon gets a
right-click. Each Task goes to the specified URL, and gets its own mini icon
(essentially a favicon, a 16x16 .ICO). You can add as many of these as you
need.

```html
<meta name="msapplication-task" content="name=Task 1;action-uri=http://host/Page1.html;icon-uri=http://host/icon1.ico">
<meta name="msapplication-task" content="name=Task 2;action-uri=http://microsoft.com/Page2.html;icon-uri=http://host/icon2.ico">
```

### (Windows 8) High quality visuals for Pinned Sites

Windows 8 adds the ability for you to provide a PNG tile image and specify the
tile's background color. [Full details on the IE
blog](http://blogs.msdn.com/b/ie/archive/2012/06/08/high-quality-visuals-for-pinned-sites-in-windows-8.aspx).

* Create a 144x144 image of your site icon, filling all of the canvas, and
  using a transparent background.
* Save this image as a 32-bit PNG and optimize it without reducing
  colour-depth. It can be named whatever you want (e.g. `metro-tile.png`).
* To reference the tile and its color, add the HTML `meta` elements described
  in the IE Blog post.

### (Windows 8) Badges for Pinned Sites

IE10 will poll an XML document for badge information to display on your app's
tile in the Start screen. The user will be able to receive these badge updates
even when your app isn't actively running. The badge's value can be a number,
or one of a predefined list of glyphs.

* [Tutorial on IEBlog with link to badge XML schema](http://blogs.msdn.com/b/ie/archive/2012/04/03/pinned-sites-in-windows-8.aspx)
* [Available badge values](http://msdn.microsoft.com/en-us/library/ie/br212849.aspx)

```html
<meta name="msapplication-badge" value="frequency=NUMBER_IN_MINUTES;polling-uri=http://www.example.com/path/to/file.xml" />
```

### Suppress IE6 image toolbar

Kill IE6's pop-up-on-mouseover toolbar for images that can interfere with
certain designs and be pretty distracting in general.

```html
<meta http-equiv="imagetoolbar" content="false">
```


## Social Networks

### Facebook Open Graph data

You can control the information that Facebook and others display when users
share your site. Below are just the most basic data points you might need. For
specific content types (including "website"), see [Facebook's built-in Open
Graph content
templates](https://developers.facebook.com/docs/opengraph/objects/builtin/).
Take full advantage of Facebook's support for complex data and activity by
following the [Open Graph
tutorial](https://developers.facebook.com/docs/opengraph/tutorial/).

```html
<meta property="og:title" content="">
<meta property="og:description" content="">
<meta property="og:image" content="">
```

### Twitter Cards

Twitter provides a snippet specification that serves a similar purpose to Open
Graph. In fact, Twitter will use Open Graph when Cards is not available. Note
that, as of this writing, Twitter requires that app developers activate Cards
on a per-domain basis. You can read more about the various snippet formats
and application process in the [official Twitter Cards
documentation](https://dev.twitter.com/docs/cards).

```html
<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@site_account">
<meta name="twitter:creator" content="@individual_account">
<meta name="twitter:url" content="http://www.example.com/path/to/page.html">
<meta name="twitter:title" content="">
<meta name="twitter:description" content="">
<meta name="twitter:image" content="http://www.example.com/path/to/image.jpg">

```


## URLs

### Canonical URL

Signal to search engines and others "Use this URL for this page!" Useful when
parameters after a `#` or `?` is used to control the display state of a page.
`http://www.example.com/cart.html?shopping-cart-open=true` can be indexed as
the cleaner, more accurate `http://www.example.com/cart.html`.

```html
<link rel="canonical" href="">
```

### Official shortlink

Signal to the world "This is the shortened URL to use this page!" Poorly
supported at this time. Learn more by reading the [article about shortlinks on
the Microformats wiki](http://microformats.org/wiki/rel-shortlink).

```html
<link rel="shortlink" href="h5bp.com">
```


## News Feeds

### RSS

Have an RSS feed? Link to it here. Want to [learn how to write an RSS feed from
scratch](http://www.rssboard.org/rss-specification)?

```html
<link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml">
```

### Atom

Atom is similar to RSS, and you might prefer to use it instead of or in
addition to it. [See what Atom's all
about](http://www.atomenabled.org/developers/syndication/).

```html
<link rel="alternate" type="application/atom+xml" title="Atom" href="/atom.xml">
```

### Pingbacks

Your server may be notified when another site links to yours. The href
attribute should contain the location of your pingback service.

```html
<link rel="pingback" href="">
```

* High-level explanation: http://codex.wordpress.org/Introduction_to_Blogging#Pingbacks
* Step-by-step example case: http://www.hixie.ch/specs/pingback/pingback-1.0#TOC5
* PHP pingback service: http://blog.perplexedlabs.com/2009/07/15/xmlrpc-pingbacks-using-php/


## App Stores

### Install a Chrome Web Store app

Users can install a Chrome app directly from your website, as long as the app
and site have been associated via Google's Webmaster Tools. Read more on
[Chrome Web Store's Inline Installation
docs](https://developers.google.com/chrome/web-store/docs/inline_installation).

```html
<link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/APP_ID">
```

### Smart App Banners in iOS 6 Safari

Stop bothering everyone with gross modals advertising your entry in the App Store.
This bit of code will unintrusively allow the user the option to download your iOS
app, or open it with some data about the user's current state on the website.

```html
<meta name="apple-itunes-app" content="app-id=APP_ID,app-argument=SOME_TEXT">
```

## Google Analytics augments

### More tracking settings

The [optimized Google Analytics
snippet](http://mathiasbynens.be/notes/async-analytics-snippet) included with
HTML5 Boilerplate includes something like this:

```js
var _gaq = [['_setAccount', 'UA-XXXXX-X'], ['_trackPageview']];
```

In case you need more settings, just extend the array literal instead of
[`.push()`ing to the
array](http://mathiasbynens.be/notes/async-analytics-snippet#dont-push-it)
afterwards:

```js
var _gaq = [['_setAccount', 'UA-XXXXX-X'], ['_trackPageview'], ['_setAllowAnchor', true]];
```

### Anonymize IP addresses

In some countries, no personal data may be transferred outside jurisdictions
that do not have similarly strict laws (i.e. from Germany to outside the EU).
Thus a webmaster using the Google Analytics script may have to ensure that no
personal (trackable) data is transferred to the US. You can do that with [the
`_gat.anonymizeIp`
option](http://code.google.com/apis/analytics/docs/gaJS/gaJSApi_gat.html#_gat._anonymizeIp).
In use it looks like this:

```js
var _gaq = [['_setAccount', 'UA-XXXXX-X'], ['_gat._anonymizeIp'], ['_trackPageview']];
```

### Track jQuery AJAX requests in Google Analytics

An article by @JangoSteve explains how to [track jQuery AJAX requests in Google
Analytics](http://www.alfajango.com/blog/track-jquery-ajax-requests-in-google-analytics/).

Add this to `plugins.js`:

```js
/*
 * Log all jQuery AJAX requests to Google Analytics
 * See: http://www.alfajango.com/blog/track-jquery-ajax-requests-in-google-analytics/
 */
if (typeof _gaq !== "undefined" && _gaq !== null) {
    $(document).ajaxSend(function(event, xhr, settings){
        _gaq.push(['_trackPageview', settings.url]);
    });
}
```

### Track JavaScript errors in Google Analytics

Add this function after `_gaq` is defined:

```js
(function(window){
    var undefined,
        link = function (href) {
            var a = window.document.createElement('a');
            a.href = href;
            return a;
        };
    window.onerror = function (message, file, row) {
        var host = link(file).hostname;
        _gaq.push([
            '_trackEvent',
            (host == window.location.hostname || host == undefined || host == '' ? '' : 'external ') + 'error',
            message, file + ' LINE: ' + row, undefined, undefined, true
        ]);
    };
}(window));
```

### Track page scroll

Add this function after `_gaq` is defined:

```js
$(function(){
    var isDuplicateScrollEvent,
        scrollTimeStart = new Date,
        $window = $(window),
        $document = $(document),
        scrollPercent;

    $window.scroll(function() {
        scrollPercent = Math.round(100 * ($window.height() + $window.scrollTop())/$document.height());
        if (scrollPercent > 90 && !isDuplicateScrollEvent) { //page scrolled to 90%
            isDuplicateScrollEvent = 1;
            _gaq.push(['_trackEvent', 'scroll',
                'Window: ' + $window.height() + 'px; Document: ' + $document.height() + 'px; Time: ' + Math.round((new Date - scrollTimeStart )/1000,1) + 's',
                undefined, undefined, true
            ]);
        }
    });
});
```


## Miscellaneous

* Use [HTML5
  polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills).

* Use [Microformats](http://microformats.org/wiki/Main_Page) (via
  [microdata](http://microformats.org/wiki/microdata)) for optimum search
  results
  [visibility](http://googlewebmastercentral.blogspot.com/2009/05/introducing-rich-snippets.html).

* If you're building a web app you may want [native style momentum scrolling in
  iOS5](http://johanbrook.com/browsers/native-momentum-scrolling-ios-5/) using
  `-webkit-overflow-scrolling: touch`.

* Avoid development/stage websites "leaking" into SERPs (search engine results
  page) by [implementing X-Robots-tag
  headers](https://github.com/h5bp/html5-boilerplate/issues/804).

* Screen readers currently have less-than-stellar support for HTML5 but the JS
  script [accessifyhtml5.js](https://github.com/yatil/accessifyhtml5.js) can
  help increase accessibility by adding ARIA roles to HTML5 elements.


*Many thanks to [Brian Blakely](https://github.com/brianblakely) for
contributing much of this information.*
