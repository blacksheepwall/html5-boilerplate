[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation
table of contents](README.md)

# Usage

只要你 clone 或下载了这份 HTML5 模板，你可以通过接下来的步骤创建你的应用：

1. 为网站设定基础框架。
2. 加入一些内容、样式、以及函数体。
3. 本地运行整个网站。
4. 执行 build 脚本来自动装配站点的优化机制，例如：[ant build script](https://github.com/h5bp/ant-build-script) 以及 [node
   build script](https://github.com/h5bp/node-build-script)（可选）。
5. 部署站点。


## Basic structure

一份HTML5 基础模板大致目录如下所示：

```
.
├── css
│   └── main.css
├── doc
├── img
├── js
│   ├── main.js
│   ├── plugins.js
│   └── vendor
│       ├── jquery-1.8.0.min.js
│       └── modernizr-2.6.1.min.js
├── .htaccess
├── 404.html
├── index.html
├── humans.txt
├── robots.txt
├── crossdomain.xml
├── favicon.ico
└── [apple-touch-icons]
```

### css

包含项目所有 CSS 文件 [About the
CSS](css.md) 。

### doc

包含所有文档。

### js

JS 文件目录。库、插件、以及其他自定义代码都放在这个目录下 [About the JavaScript](js.md) 。

### .htaccess

Apache 服务器默认配置文件 [About the .htaccess](htaccess.md) 。

关于服务器配置，请详见 [server configs
repo](https://github.com/h5bp/server-configs) 。

### 404.html

404 页面。

### index.html

默认站点入口页面。

在调整项目文件目录时，确保所有 CSS 以及 JavaScript 文件的路径正确。

如果你正在使用 Google Analytics, 确保将统计代码至于该页面的底部。

### humans.txt

开发人员文件，主要内容是站点开发者、维护者，该文件对搜索引擎友好。

### robots.txt

该文件面向搜索引擎，可以配置一系列不需要爬虫爬取的页面。


### crossdomain.xml

跨域请求模板文件 [About
crossdomain.xml](crossdomain.md) 。

### icons

使用你自己的站点图标来代替默认的 `favicon.ico`。 [HTML5 Boilerplate Favicon and
Apple Touch Icon
PSD-Template](http://drublic.de/blog/html5-boilerplate-favicons-psd-template/) 。
