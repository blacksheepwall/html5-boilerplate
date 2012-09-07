[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation
table of contents](README.md)

# HTML

## 条件性的 `html` 样式

一些条件注释可以生成 IE 特定样式应用在 `html` 标签上，以此修复某版本 IE 缺陷，当然你也许并不大打算使用这个 trick ，没关系， HTML5 Boilerplate 的默认样式并不依赖它。

在 `html` 上使用条件样式有以下优点：

* 能够避免由 Stoyan Stefanov 和 Markus Leptien 发现的 [file blocking
  issue](http://webforscher.wordpress.com/2010/05/20/ie-6-slowing-down-ie-8/) 。
  
* 避免引入由上述 issue 产生的空元素
* 类似 WordPress 的 CMS 或文档管理类网站，会经常使用 body 样式，This makes
  integrating there a touch simpler.
* 仍旧能通过 HTML5 验证。
* 使用与 Modernizr (以及 Dojo) 一样的元素，看起来不错。
* 在多人团队中代码清晰明了。


## `no-js` 样式

当用户禁用浏览器 js 时，在标签上设置一个 `no-js` 样式，反之如果启用，则设置为 `js` : [Avoiding the
FOUC](http://paulirish.com/2009/avoiding-the-fouc-v3/) 。


## meta 标签顺序，以及 `<title>`

根据 [the HTML5
spec](http://www.whatwg.org/specs/web-apps/current-work/complete/semantics.html#charset)
(4.2.5.5 指定文档字符编码)，及早声明字符集 (before any ASCII art ;) 来避免 IE 下潜在的 [encoding-related security
issue](http://code.google.com/p/doctype/wiki/ArticleUtf7) ， [1024
bytes](http://www.whatwg.org/specs/web-apps/current-work/multipage/semantics.html#charset).

由于 [potential XSS
vectors](http://code.google.com/p/doctype-mirror/wiki/ArticleUtf7) ，字符集应当在 `<title>` 标签前声明。

兼容模式下的 meta 标签 [needs to be before all elements except
title and meta](http://h5bp.com/f "Defining Document Compatibility - MSDN") ，
如果在 [first 1024
bytes](http://code.google.com/p/chromium/issues/detail?id=23003) 中，此 meta 标签可以在 Google Chrome Frame 中触发特有效果。


## X-UA-Compatible

浏览器在含有多个渲染引擎时，该属性可以确保切换至最新版本。即使用户正在使用 IE8 或者 IE9，那也并不意味着他们的浏览器会切换至最新渲染引擎。为解决这个问题，使用：

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

这行 `meta` 标签会告诉 IE 渲染引擎两件事情：

1. 使用最新或次最新的渲染引擎。
2. 如果安装过 Google Chrome Frame，那么启用它来渲染页面。

`meta` 标签确保用户在使用 IE 时，自动启用浏览器最好的渲染模式来渲染页面。

当然，这行语句会影响 html 验证，Google Chrome Frame 这部分代码不会在条件注释中生效。 To avoid these edge case issues it is recommended that
you **remove this line and use the `.htaccess`** (or other server config)
to send these headers instead. You also might want to read [Validating:
X-UA-Compatible](http://groups.google.com/group/html5boilerplate/browse_thread/thread/6d1b6b152aca8ed2).

如果你的网站端口不是标准的 80，那么你需要在服务器端设置该 `header`，因为 IE 默认设置会启用 'Display
intranet sites in Compatibility View' 。


## 移动端的视图 viewport

目前已经有几种 [`viewport` meta
tag](https://docs.google.com/present/view?id=dkx3qtm_22dxsrgcf4 "Viewport and
Media Queries - The Complete Idiot's Guide") 的使用方式了，你还可以在 [the
Apple developer docs](http://j.mp/mobileviewport) 找到更多。 HTML5 Boilerplate 会在这些方案中摸索出一个普适的设置。

```html
<meta name="viewport" content="width=device-width">
```

## 站点 Favicons 以及 Touch Icons

网站标识图标应该至于网站的根目录。HTML5
Boilerplate 默认有一组图标 (包括 favicon 和 供Apple Touch 设备的图标) 。

如果图标在子目录，那么需要在 `head` 中插入指向图标资源的 `link` 元素。

更多信息请查看：[Everything you always wanted to know
about touch icons](http://mathiasbynens.be/notes/touch-icons) by Mathias
Bynens。

## Modernizr 库

HTML5 Boilerplate 使用定制过的 Modernizr 工具库。

[Modernizr](http://modernizr.com) 是一个检测浏览器对 HTML5 和 CSS3 特性支持的 JS 库，通过检测你的浏览器对 html5/css3 的支持情况，返回特定的样式名称，从而可以针对不同的浏览器写出不同的样式。


## 内容区域

html5 boilerplate 模版的中心内容体是空的，这是有意而为之，使其既适应 web 以及 app的开发。

### Google Chrome Frame

html boilerplate 主体内容区域会包含一个明显的提示，通知用户安装 Chrome
Frame （IE 用户安装不再需要管理员权限） 。如果你不打算兼容 IE6，那么移除这段代码就好了。


### Google CDN 上的 jQuery 框架

该库使用协议无关 (protocol-independent) 的路径 （参考 [FAQ](faq.md) ），并置于页面的底部。当 CDN 版本由于某些缘故无法访问时，会有一个本地版本的 fallback 加载机制。

不管使用何种 js 框架，引入 CDN 版是非常值得的，一方面用户浏览器中可能已缓存了某个版本的框架，另一方面一般来说 google 的 CDN 访问速度要比你的服务器更快些。

### Google Analytics 统计代码

最后提到 GA 统计代码，官方推荐将这段代码置于页面顶部，目的是在整个页面还未完全载入前更好的追踪用户行为。

更多信息请访问：

* [Optimizing the asynchronous Google Analytics
  snippet](http://mathiasbynens.be/notes/async-analytics-snippet).
* [Tracking Site Activity - Google
  Analytics](http://code.google.com/apis/analytics/docs/tracking/asyncTracking.html).
