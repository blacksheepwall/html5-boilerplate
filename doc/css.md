[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation
table of contents](README.md)

# The CSS

HTML5 Boilerplate CSS 包含：

* [Normalize.css](https://github.com/necolas/normalize.css).
* 易用的 HTML5 Boilerplate 预设
* Common helpers
* Placeholder media queries
* 打印样式

This starting CSS does not rely on the presence of conditional classnames,
conditional style sheets, or Modernizr. It is ready to use whatever your
development preferences happen to be.


## Normalize.css

Normalize.css 是个现代的、为 HTML5 准备的 CSS reset，该文件中富含大量注释。访问 [Normalize.css
project](http://necolas.github.com/normalize.css/) 查看更多信息。


## HTML5 Boilerplate 预设

该项目包含少量基础样式： 

* 基础的打印设置，目的是增强文本可读性。
* 文本高亮时，对 `text-shadow` 属性进行预防。
* 一些图片定位、fieldset 以及 textarea 的小优化。
* 更漂亮的 chrome 提示。

请根据项目需要随意修改这些基础样式。


## Common helpers

#### `.ir`

使用 `.ir` 样式来处理那些 image-replacement 的元素，并确保要为这些元素引入 `background-image: url(pathtoimage.png);` 样式。

#### `.hidden`

使用 `.hidden` 样式来隐藏任何元素，这些元素也可以是 JavaScript 动态生成的。当然滥用隐藏元素可能会遭到 SEO 惩罚。

#### `.visuallyhidden`)

使用 `.visuallyhidden` 样式来隐藏元素，但对电脑浏览器 (screen) 来说仍旧是可访问的。你可以通过这个样式来指定哪些设备可以访问元素，哪些不能。 [About invisible
content](http://www.webaim.org/techniques/css/invisiblecontent/), [Hiding
content for
accessibility](http://snook.ca/archives/html_and_css/hiding-content-for-accessibility),
[HTML5 Boilerplate
issue/research](https://github.com/h5bp/html5-boilerplate/issues/194/).

#### `.invisible`

Add the `.invisible` class to any element you want to hide without affecting
layout. When you use `display: none` an element is effectively removed from the
layout. But in some cases you want the element to simply be invisible while
remaining in the flow and not affecting the positioning of surrounding
content.

#### `.clearfix`

Adding `.clearfix` to an element will ensure that it always fully contains its
floated children. There have been many variants of the clearfix hack over the
years, and there are other hacks that can also help you to contain floated
children, but the HTML5 Boilerplate currently uses the [micro
clearfix](http://nicolasgallagher.com/micro-clearfix-hack/).


## Media Queries

The boilerplate makes it easy to get started with a "Mobile First" and
[Responsive Web
Design](http://www.alistapart.com/articles/responsive-web-design/) approach to
development. But it's worth remembering that there are [no silver
bullets](http://www.cloudfour.com/css-media-query-for-mobile-is-fools-gold/).

We include a placeholder Media Queries to build up your mobile styles for wider
viewports. It is recommended that you adapt these Media Queries based on the
content of your site rather than mirroring the fixed dimensions of specific
devices.

If you do not want to take a "Mobile First" approach, you can simply edit or
remove these placeholder Media Queries. One possibility would be to work from
wide viewports down and use `max-width` MQs instead, e.g., `@media only screen
and (max-width: 480px)`.

Take a look into the [Mobile
Boilerplate](https://github.com/h5bp/mobile-boilerplate) for additional features
that are useful when developing mobile websites.


## 打印样式

* 打印样式全部在这里 [reduce the number of page
  requests](http://www.phpied.com/delay-loading-your-print-css/).
* 抛弃所有背景色，将字体颜色调整为 gray，并移除 text-shadow 属性，对节省打印机油墨大有裨益。
* 链接并不需要标记为特定颜色，因为下划线足够说明本身是个链接。
* 链接和缩写可以展开，暗示用户可以进一步访问这些标签的引用页。
* 但是我们并不想给 image 置换元素 (replaced elements) 显示链接文本（其实他们就是作为图片而存在的）。


### Paged media styles

关于 Media styles 请访问 [http://www.w3.org/TR/CSS2/media.html](http://www.w3.org/TR/CSS2/media.html)  
关于 Paged media 请访问 [http://www.w3.org/TR/CSS2/page.html](http://www.w3.org/TR/CSS2/page.html)  

* Paged media 目前只有少量浏览器支持 [few
  browsers](http://en.wikipedia.org/wiki/Comparison_of_layout_engines_%28Cascading_Style_Sheets%29#Grammar_and_rules).
* Paged media support means browsers would know how to interpret instructions
  on breaking content into pages and on orphans/widows.
* We use `page-break-inside: avoid;` to prevent an image and table row from
  being split into two different pages, so use the same `page-break-inside:
  avoid;` for that as well.
* Headings should always appear with the text they are titles for. So, we
  ensure headings never appear in a different page than the text they describe
  by using `page-break-after: avoid;`.
* We also apply a default margin for the page specified in `cm`.
* We do not want [orphans and
  widows](http://en.wikipedia.org/wiki/Widows_and_orphans) to appear on pages
  you print. So, by defining `orphans: 3` and `widows: 3` you define the minimal
  number of words that every line should contain.
