[项目首页](http://html5boilerplate.com) | [文档概览](TOC.md)

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

### 重新为 IE 控制栏定义颜色

IE9+ 会为固定站点自动使用全局色彩来标识，以此区分开普通站点。当然，你可以通过使用类似 (`red`) 或者 16 进制的 (`#ff0000`) 的值来完成自定义。

```html
<meta name="msapplication-navbutton-color" content="#ff0000">
```

### 手动设置固定站点的窗口大小

固定站点窗口的大小也是可以自定义的，目前只支持像素，最小值为 800x600。


```html
<meta name="msapplication-window" content="width=800;height=600">
```

### 跳转列表 (Jump List)

可以通过添加如下代码来给页面设置一个 icon，也可以采用传统的方法，将 16x16 的 favicon.ico 文件放到页面的根目录下。在点击 pinned 的时候，IE9 可以直接读到。

更多信息 [http://msdn.microsoft.com/zh-cn/library/gg491743(v=vs.85).aspx]() 以及 [http://msdn.microsoft.com/zh-cn/library/gg491725(v=vs.85).aspx]()

```html
<meta name="msapplication-task" content="name=Task 1;action-uri=http://host/Page1.html;icon-uri=http://host/icon1.ico">
<meta name="msapplication-task" content="name=Task 2;action-uri=http://microsoft.com/Page2.html;icon-uri=http://host/icon2.ico">
```

### Windows 8 下视觉效果更佳的固定站点

Windows 8 允许用户提供一个 tile 的 PNG 图片，并指定 tile 的背景色 [Full details on the IE
blog](http://blogs.msdn.com/b/ie/archive/2012/06/08/high-quality-visuals-for-pinned-sites-in-windows-8.aspx)。

* 为站点创建一个 144x144 尺寸的图标，将其填充整个画布，并使用透明背景色。
* 将图标文件保存为 32 位的 PNG，这被命名为 whatever you want (e.g. `metro-tile.png`)。
* 为了方便引用 tile 及其色值，增加 HTML 的 `meta` 标签。

### (Windows 8) 固定站点的标识


* [Tutorial on IEBlog with link to badge XML schema](http://blogs.msdn.com/b/ie/archive/2012/04/03/pinned-sites-in-windows-8.aspx)
* [Available badge values](http://msdn.microsoft.com/en-us/library/ie/br212849.aspx)

```html
<meta name="msapplication-badge" value="frequency=NUMBER_IN_MINUTES;polling-uri=http://www.example.com/path/to/file.xml">
```


### Disable link highlighting upon tap in IE10

Similar to [-webkit-tap-highlight-color](http://davidwalsh.name/mobile-highlight-color)
in iOS Safari. Unlike that CSS property, this is an HTML meta element, and it's
value is boolean rather than a color. It's all or nothing.


### 去除 IE6 下保存图片的工具条

参考 [http://stackoverflow.com/questions/7207649/imagetoolbar-meta-tag-and-ie-versions]()


```html
<meta http-equiv="imagetoolbar" content="false">
```


## 社交网络

### Facebook 的 Open Graph 数据

（由于某些特殊原因，关于这点不作翻译）You can control the information that Facebook and others display when users
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

### Twitter 卡片

（由于某些特殊原因，关于这点不作翻译）Twitter provides a snippet specification that serves a similar purpose to Open
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

### 标准链接 (Canonical URL)

指符合规范和标准的网站链接。通过定义唯一的标准规范 URL，可以避免由于 URL 格式不同造成的重复内容问题。Google、Yahoo、Mircrosoft 三大搜索引擎在 09 年初宣布支持 Link 标签的一个新属性 Canonical，为网页指定权威链接，用来改善网站由于 URL 格式不同造成的重复内容问题。通过添加此标签你可以自主控制出现在搜索结果中的网站的 URL 格式，这样就有助于消除那些影响你网页声望值的因素。参考 [http://ask.enquiro.com/2009/what-is-a-canonical-url/]()

```html
<link rel="canonical" href="">
```

### 短链接 (shortlink)

参考 [article about shortlinks on
the Microformats wiki](http://microformats.org/wiki/rel-shortlink).

```html
<link rel="shortlink" href="h5bp.com">
```


## News Feeds

### RSS

参考 [learn how to write an RSS feed from
scratch](http://www.rssboard.org/rss-specification)?

```html
<link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml">
```

### Atom

Atom 与 RSS 类似 [See what Atom's all
about](http://www.atomenabled.org/developers/syndication/).

```html
<link rel="alternate" type="application/atom+xml" title="Atom" href="/atom.xml">
```

### 留下评论 (Pingbacks)

当有其他网站的链接指向你的服务器时，pingbacks 会通知你。

```html
<link rel="pingback" href="">
```

* 详细分析： http://codex.wordpress.org/Introduction_to_Blogging#Pingbacks
* 进阶说明： http://www.hixie.ch/specs/pingback/pingback-1.0#TOC5
* PHP 的 pingback 服务： http://blog.perplexedlabs.com/2009/07/15/xmlrpc-pingbacks-using-php/


## App Stores

### 安装 Chrome Web Store 应用

只要应用与网站通过 Google's 站点管理工具进行关联，用户就能直接从你的网站安装一个 Chrome 应用。更多信息请查询
[Chrome Web Store's Inline Installation
docs](https://developers.google.com/chrome/web-store/docs/inline_installation).

```html
<link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/APP_ID">
```

### iOS 6 下 Safari 智能广告条

通过以下这段代码，跟那些做工粗糙时不时打扰用户的模态广告说再见了。

```html
<meta name="apple-itunes-app" content="app-id=APP_ID,app-argument=SOME_TEXT">
```

## Google 统计参数

### 更详细的追踪参数

HTML5 Boilerplate 中 [优化过的 Google 统计代码段](http://mathiasbynens.be/notes/async-analytics-snippet) 如下所示：

```js
var _gaq = [['_setAccount', 'UA-XXXXX-X'], ['_trackPageview']];
```

如果你需要更详细的配置，扩展 (extend) 数组而不是在后面使用 [`.push()`ing to the
array](http://mathiasbynens.be/notes/async-analytics-snippet#dont-push-it)
即可：

```js
var _gaq = [['_setAccount', 'UA-XXXXX-X'], ['_trackPageview'], ['_setAllowAnchor', true]];
```

### 将 IP 地址隐藏

有些国家由于政府政策原因，个人数据信息只能在法律规定的范围内传播（例如从德国发送数据至欧盟外的地方，会有限制）。网站管理员要确保个人数据不能误传送至美国，只需这么做 [the
`_gat.anonymizeIp`
option](http://code.google.com/apis/analytics/docs/gaJS/gaJSApi_gat.html#_gat._anonymizeIp)。  

```js
var _gaq = [['_setAccount', 'UA-XXXXX-X'], ['_gat._anonymizeIp'], ['_trackPageview']];
```

### 追踪 Google Analytics 的 AJAX 请求

可参考由 @JangoSteve 撰写的一文 [track jQuery AJAX requests in Google
Analytics](http://www.alfajango.com/blog/track-jquery-ajax-requests-in-google-analytics/).

在 `plugins.js` 加入以下代码：

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

### 追踪 Google Analytics 里的 JavaScript 异常

在 `_gaq` 定义后加入这段函数：

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

### 追踪页面的滚动事件

在 `_gaq` 定义后加入这段函数：

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


## 杂项

* 使用 [HTML5
  polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills) 。

* 使用 [微数据格式](http://microformats.org/wiki/Main_Page) (via
  [microdata](http://microformats.org/wiki/microdata)) 来定制更多搜索结果的[显示](http://googlewebmastercentral.blogspot.com/2009/05/introducing-rich-snippets.html) 。

* 如果你正在开发 web app，想实现 [iOS5 下原生的弹性滚动效果](http://johanbrook.com/browsers/native-momentum-scrolling-ios-5/) ，使用  `-webkit-overflow-scrolling: touch` 。

* 避免开发阶段 "leaking" into SERPs (search engine results
  page) by [implementing X-Robots-tag
  headers](https://github.com/h5bp/html5-boilerplate/issues/804) 。

* 一些屏幕阅读器对 HTML5 以及 JS 支持性不太好， [accessifyhtml5.js](https://github.com/yatil/accessifyhtml5.js) 可以通过加入 ARIA roles 属性改善可访问性的问题。


* 向 [Brian Blakely](https://github.com/brianblakely) 致谢。*
