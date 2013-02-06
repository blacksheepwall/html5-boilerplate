[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation
table of contents](TOC.md)

# The JavaScript

关于项目中 JavaScript 的组织方式。

## main.js

该文件是的 site/app 的主入口。对于大型项目而言，你可以使用 JavaScript 模块加载器，比如 [Require.js](http://requirejs.org/)，来动态加载所需模块。

## plugins.js

该文件包含所有插件，比如 jQuery plugins 和其他第三方脚本。

其中有一种封装 jQuery plugins 的方法是通过形如 `(function($){ ...
})(jQuery);` 的闭包来确保代码在 jQuery 命名空间下执行。更多用法请查看 [jQuery plugin
authoring](http://docs.jquery.com/Plugins/Authoring#Getting_Started)

## vendor

该目录存放所有第三方类库。
 
最新压缩版的 jQuery 和 Modernizr 库可以存放在此，当然你也可以定制自己的类库 [custom Modernizr
build](http://www.modernizr.com/download/)。
