
在我们写样式的时候，页面的CSS在经历几个版本的修改之后，可能有些样式已经用不到了，或许将某些样式更名了而原来的忘了删除，总之页面中可能存在着一些无用的样式。这些无用的浪费了一些服务器空间和带宽消耗，也会增大我们的维护成本。那么有没有一些办法来清理那些无用的样式呢？今天就让我们来了解一下几个比较有用的工具。

Dust-Me selectors

https://addons.mozilla.org/zh-CN/firefox/addon/dust-me-selectors/
http://www.brothercake.com/dustmeselectors/

Dust-Me是一个很有用也很好用的Firefox插件，它可以分析到你的页面中调用的所有CSS文件并分析那些在页面中没有被用到。支持本地和远程样式文件，包括使用link标签、< ?xml-stylesheet?>处理指令、@import语句等方式引入的样式文件；(但是不支持页面中的style块和内联样式)，支持IE条件注释中引入的样式文件；可以检查一个页面，也可以检查整个网站；支持CSS1选择器、大部分CSS2和CSS3选择器；理解通用的CSS hack，比如 “* html #fuck-ie”将会被认为是”html #fuck-ie”；支持Firefox 3.5和Firefox 3.0，事实上得益于FF 3.5的js引擎的改进，FF 3.5中的性能比FF 3.0要高50%。

Page Speed

https://developers.google.com/speed/pagespeed/

Page Speed是Google提供的一个前端性能分析工具，有些类似于YSlow，但是提供了一些比较个性且很有用的工具，比如Remove unused CSS。Page Speed和YSlow一样依赖Firebug。

CSS Redundancy Checker

https://github.com/kmytor/css-redundancy-checker

CSS Redundancy Checker 是一个免费的在线应用，可以检查所有的使用某个CSS文件的页面中无用的样式。可以同时检查某一个样式在多个页面中的使用情况。该工具的不足是虽然一次能检查多个HTML页面，但每次只能检查一个CSS文件，而且还要手动输入。

IntelliJ IDEA

IntelliJ IDEA 这是一个颇强大的IDE，类似于DreamWeaver，不过在国内用的不多。该软件包括一个即时代码分析工具(On-the-fly Code Analysis)，可以分析CSS文件中未用到的class和id。

Expression Web

Expression Web作为微软的新一代网站开发工具，还是有很多人使用的，其CSS Report功能可以检查未用到需要被清除的CSS（我的确没有使用EW开发过网站，希望使用该软件的童鞋可以帮忙确认一下这一点）。