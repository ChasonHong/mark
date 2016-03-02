# 重构优秀教程合集

“无上甚深微妙法，百千万劫难遭遇，我今见闻得受持，愿解如来真实义。”
——《开经偈》

## html标签

- [HTML5 标签列表](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5/HTML5_element_list)
- [All HTML5 Tags](http://www.html-5-tutorial.com/all-html-tags.htm)

ie8- 不支持html5新增标签，可通过引入js来实现：[html5shiv](https://github.com/afarkas/html5shiv/)

```html
<!--[if lt IE 9]>
    <script src="http://cdn.staticfile.org/html5shiv/r29/html5.min.js"></script>
<![endif]-->
```

或按实际使用手写js兼容，`document.createElement`

```html
<!--[if lt IE 9]>
<script type="text/javascript">
   document.createElement('header');
   ...
</script>
<![endif]-->
```

最后重置下html5标签的css默认样式：

```css
article, aside, details, figcaption, figure, footer, header, hgroup, main, menu, nav, section, summary {
  display: block;
}
```

## 盒模型

[box-sizing详解](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing)

![](http://7tszky.com1.z0.glb.clouddn.com/FjCDltsO3h7GVBox9LXo4KGJpZ4I)

盒模型可通过`box-sizing: border-box | content-box`设置，默认值为`content-box`，ie8+支持。

- border-box表示设置的`width/height`包括`padding`和`border`
- content-box表示不包括`padding`和`border`
- 不论是border-box还是content-box都不包括margin

对应上图，如果是默认的话，则width为605px，如是border-box的话则为605+2*4+10*3+30=673px。

常配合百分比单位使用，尤其应用在移动端。如`width:100%;padding:10px;`，如果不设置为border-box，则实际宽度为100%+40px，不符合我们的预期要求。

## 选择器

css的选择器是从后往前查询，所以层级越深，效率越低，一般建议最多不超过4层。

css选择器包括：通配符`*`选择器，class选择器，id选择器，元素选择器，属性选择器，伪类选择器，伪元素选择器，最后

css选择器权重原则：!important > 行内样式 > id > 类/属性/伪类 > 元素/伪元素；权重相同的按照样式表中出现的顺序，后面的覆盖前面的

- [深入解析CSS样式层叠权重值](http://ofcss.com/2011/05/26/css-cascade-specificity.html)
- [CSS 选择器](http://css4-selectors.com/selectors/)

## 重置

css重置分为归零重置及纠正重置

- 归零重置的代表为：[Eric Meyer’s “Reset CSS” 2.0](http://meyerweb.com/eric/tools/css/reset/index.html)
- 纠正重置代表为：[normalize.css](https://necolas.github.io/normalize.css/)

如果你想省事的话直接引入normalize.css，然后再进行部分归零重置；如果深入研究可以把两个揉合一起，可参考[sandal reset](https://github.com/marvin1023/sandal/blob/master/core/_reset.scss)

## 属性详解

属性大概分为下面几类：

- 显示：display，visibility，overflow等
- 位置：position，float，clear，z-index，transform等
- 大小：width，height，margin，padding，border，outline，box-sizing等
- 文字： font系列，color，text系列等
- 背景：background系列，gradient系列等
- 修饰：border-radius，box-shadow，opacity，appearance，filter，clip等
- 布局：flex，grid等
- 动画：transition，animation等

从使用上大概分为两类，一类是死板的（如设置文本颜色只能用color），一类是灵活的（如实现一个左边栏固定的布局，可以使用的技术就多了）。相对来说可灵活使用的则更需要掌握各种实现方案的利弊

- [MDN CSS reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [codrops CSS reference](http://tympanus.net/codrops/css_reference/#section_css-property)
- [css 101](http://css-101.org/index.php)

## 单位

css3新增了rem单位及vw系列单位。rem单位是以html的字体大小为相对计算的，而vw则是以视窗大小的

- [rem详解](http://www.w3cplus.com/css3/define-font-size-with-css3-rem)
- [vw](http://www.zhangxinxu.com/wordpress/2012/09/new-viewport-relative-units-vw-vh-vm-vmin/)

## 居中
包括水平及垂直居中，除了常规的水平居中`text-algin:center`、`margin-left:auto;margin-right:auto`和垂直居中`vertical-align:middle`，`line-height: height`(单行文字垂直的line-height等于height)，还有postition方法，首先设置`top:50%;left:50%`，再通过`margin-left:-width/2;margin-top:-height/2`，或css3的`transform: translate(-50%, -50%)`调整居中，最后还有为布局而生的`flex`方法。另：对于img或video还有最新的`object-position`来调整

- [Centering in CSS: A Complete Guide](https://css-tricks.com/centering-css-complete-guide/)
- [object-fit](http://caniuse.com/#search=object-fit)

## 布局

在flex出现之前，布局不外乎float，position，还有少量的inline-block及table；而现在有了flex和grid，更是如虎添翼。

- [Learn CSS Layout](http://book.mixu.net/css/index.html?utm_source=html5weekly&utm_medium=email)，中文版[学习css布局](http://zh.learnlayout.com/)。一步步学习布局，适合入门
- [深入了解flex](http://www.w3cplus.com/blog/666.html)
- [flex完全指南：三大版本对比](http://www.w3cplus.com/css3/a-guide-to-flexbox-new.html)
- [960网格布局](http://960.gs/)：网格布局的开创者，知道原理其余的各种网格布局也就没问题了
- [layout gala](http://blog.html.it/layoutgala/index.html)：强烈推荐，float布局精髓

## z-index

- [The stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)，影响z-index的因素
- [深入理解CSS中的层叠上下文和层叠顺序](http://www.zhangxinxu.com/wordpress/2016/01/understand-css-stacking-context-order-z-index/)
- [The Z-Index CSS Property: A Comprehensive Look](https://www.smashingmagazine.com/2009/09/the-z-index-css-property-a-comprehensive-look/)，文章比较老，涉及到ie7-的一些z-index bug

## line-height

- [深入理解CSS中的行高](http://www.cnblogs.com/rainman/archive/2011/08/05/2128068.html)——简版
- [深入理解css 行高](http://www.slideshare.net/daemao)——ppt详细版
- [css行高line-height的一些深入理解及应用](http://www.zhangxinxu.com/wordpress/2009/11/css%E8%A1%8C%E9%AB%98line-height%E7%9A%84%E4%B8%80%E4%BA%9B%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3%E5%8F%8A%E5%BA%94%E7%94%A8/)

## BFC

- [MDN BFC](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)，新建BFC的条件
- [Understanding Block Formatting Contexts in CSS](http://www.sitepoint.com/understanding-block-formatting-contexts-in-css/)，中文版[理解CSS中的块级格式化上下文](https://segmentfault.com/a/1190000003068557)
- [关于Block Formatting Context－－BFC和IE的hasLayout](http://www.cnblogs.com/pigtail/archive/2013/01/23/2871627.html)
- [css 101: BFC](http://css-101.org/block-formatting-contexts/index.php)
- [重提CSS中外边距折叠问题](https://segmentfault.com/q/1010000002645174)

## 兼容

浏览器兼容分为两部分：浏览器是否支持；如何针对浏览器写hack。支持情况可以通过can i use查询，而针对各种浏览器写hack可以使用browser hacks

- [can i use](http://caniuse.com/)
- [各个浏览器hack](http://browserhacks.com/)
