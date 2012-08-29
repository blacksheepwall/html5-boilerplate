[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation
table of contents](README.md)

# FAQ

## 为什么不使用 http 开头的 url 来载入 jQuery？

这是有意为之的，具体可见 [protocol-relative
URLs](http://paulirish.com/2010/the-protocol-relative-url/) 。

**请注意** 引用资源请使用相对协议 (protocol-relative) URL 。  
参考资料：[http://paulirish.com/2010/the-protocol-relative-url/]() 以及 [http://ioio.name/the-protocol-relative-url.html]()


### 为什么不直接从 Google 的 CDN 上加载最新的 jQuery 版本？

1. 最新版本 jQuery 很可能与现有代码、插件不能很好兼容，版本的更新可能导致潜在的问题。
2. 最新版本经常有一段 `max-age=3600`，这段代码会影响缓存。


### 为什么要将 Google Analytics 代码置于页面底部？ Google 却推荐将其置于 `head` 中。

将统计代码置于 `head` 中的目的是为了更精确地跟踪用户的访问行为，即使在整个页面还没有加载完毕前就离开了。然而如果置于底部，无疑能更快地加载页面，而且同其他脚本代码组织在一起，维护性也大大增强。


### 如何整合 [Twitter Bootstrap](http://twitter.github.com/bootstrap/) 与 HTML5 Boilerplate？

可以使用 [Initializr](http://initializr.com) 来定制一个包含两者的版本。

具体信息请访问 [HTML5 Boilerplate and Twitter Bootstrap complement each
other](http://www.quora.com/Is-Bootstrap-a-complement-OR-an-alternative-to-HTML5-Boilerplate-or-viceversa/answer/Nicolas-Gallagher) 。


### 什么是 profiling，如何使用？

[Firebug](http://michaelsync.net/2007/09/10/firebug-tutorial-logging-profiling-and-commandline-part-ii)
以及 [Chrome Dev
tools](http://code.google.com/chrome/devtools/docs/profiles.html) 提供了 profiling
，至于 IE中 如何调试，在此不赘述。


### 当新版本的 HTML5 Boilerplate 发布以后，我的站点是否需要同步升级？

没必要，框架的根基一般不会调整。


### 遇到困难，在哪里可以获得帮助？

求助请访问 [StackOverflow](http://stackoverflow.com/questions/tagged/html5boilerplate) 。