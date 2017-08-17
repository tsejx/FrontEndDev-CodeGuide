# CSS 编码规范

# CSS文件命名

    主要的 master.css；
    模块 module.css；
    基本共用 base.css；
    布局，版面layout.css；
    主题 themes.css；
    专栏 columns.css；
    文字 font.css；
    表单 forms.css；
    补丁 mend.css；
    打印 print.css

# CSS Meta规则

## 编码

一般情况下编码同`html`的一致。

如果是`urf-8`，则不需要制定样式表的编码，因为它默认为`urf-8`。

## 注释
代码是由人编写并维护的。请确保你的代码能够自描述、注释良好并且易于他人理解。好的代码注释能够传达上下文关系和代码目的。不要简单地重申组件或 class 名称。

对于较长的注释，务必书写完整的句子；对于一般性注解，可以书写简洁的短语。

### 头部注释

注明本CSS的用处，生成时间及作者等信息。
```
/* CSS Document  
Use for:    website  
Version:    1.0 
Date:      time 
Author:     your name 
Update:      
*/
```
### 页面注释

有时候一份CSS会把首页和各种二级页面样式写在一起，这时需要做页面注释。
```
/*********************************** 
 * 首页 
 ***********************************/
```
### 分级注释

比如在main模块下，建立了news、photo等栏目，可使用分级注释，以指明层级结构。
```css
/*----------------main-----------------*/
main {}
.main-bg {}

/* news */
.news {}

/* photo */
.photo  {}
```
### 区块间注释
```
/* news */
.news {}

/* photo */
.photo  {}
```
### 修改注释

当后期维护中有修改到css，需添加修改的注释。
```
.news {} /* 修正横向滚动条错误 by your name */
```

# CSS代码风格规则

## CSS代码有效性

使用有效的CSS代码。

可使用[W3C CSS validator][1]来验证css。

## 命名
class应优先虑以这元素具体目的来进行命名，应尽量简短且富有含义。

统一采用小写英文字母、数字、“-” 的组合。其中不得包含汉字、空格和特殊字符。
```
/* 不推荐 */
.demoimage {}  /* "demo" 和 "image" 中间没加 "-" */
```
```
/* 不推荐 */
.error_status {}  /* 用下划线 "_" 是屌丝的风格 */
```
```
/* 推荐 */
.ads-sample {}
```
原则上，不建议缩写，除非一看就懂的缩写，如nav。

尽量避免使用id来控制样式。

***框架css类命名清单***

 - 全屏：`full_bg`（全屏背景）  
 -  容器：`wrapper`（最外面的主框架）
 -  页头：`header`（子项：h_1、h_2、……）
 - 内容：`container` 
 - 页面主体：`main` 
 - 页尾：`footer` 导航：`nav`（子项：n_1、n_2、……）
 - 菜单：`menu`（子项：m_1、m_2、……） 
 - 导航：`nav`（子项：n_1、n_2、……） 
 - 子菜单：`submenu` 
 - 侧栏：`sidebar`
 - 栏目：`column`（扩展：column1、column2、……）
 - 左右中：`left`、`right`、`center` 
 - 搜索：`search`
 - 登陆：`signin`

## class命名

 - class 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关class的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
 - 避免过度任意的简写。`.btn` 代表 *button*，但是 `.s`不能表达任何意思。 
 - class 名称应当尽可能短，并且意义明确。
 - 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（presentational）的名称。
 - 基于最近的父 class或基本（base） class 作为新 class 的前缀。
 - 使用 `.js-*` class 来标识行为（与样式相对），并且不要将这些
   class 包含到 CSS 文件中。

在为 Sass 和 Less 变量命名时也可以参考上面列出的各项规范。

```css
/* Bad example */
.t { ... }
.red { ... }
.header { ... }

/* Good example */
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

## 选择器
避免出现过多的祖先选择器，各浏览器会有性能差异，消耗在选择器的时间也不尽相同。

尽量最多控制在3级以内。
```
/* 不推荐 */
ul.example {}
.example1 .example2 .example3 .example4 {}
```
```
/* 推荐 */
.example {}
.example1, 
.example2 {}
```
非必要的情况下不要使用元素标签名和ID或class进行组合。
```
/* 不推荐 */
ul#example {}
div.error {}
```
```
/* 推荐 */
#example {}
.error {}
```

 - 对于通用元素使用class，这样利于渲染性能的优化。
 - 对于经常出现的组件，避免使用属性选择器（例如，`[class^="..."]`）。浏览器的性能会受到这些因素的影响。
 - 选择器要尽可能短，并且尽量限制组成选择器的元素个数，建议不要超过 **3** 。
 - **只有**在必要的时候才将class限制在最近的父元素内（也就是后代选择器）（例如，不使用带前缀的 class 时 -- 前缀类似于命名空间）。

扩展阅读：

 - [Scope CSS classes with prefixes][2] 
 - [Stop the cascade][3]

```css
/* Bad example */
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

/* Good example */
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```
 
## 简化css
写属性值的时候尽量使用缩写。
```
/* 不推荐 */
.example { 
  border-top-style:none; 
  font-family:Palatino, serif; 
  font-size:100%; 
  line-height:1.6; 
  padding-bottom:2em; 
  padding-left:1em; 
  padding-right:1em; 
  padding-top:0; 
}
```
```
/* 推荐 */
.example { border-top: none; font: 100%/1.6 Palatino, serif; padding: 0 1em 2em;}
```
属性值为0时，忽略单位
```
/* 不推荐 */
.example { margin:0px; padding:0px;}
```
```
/* 推荐 */
.example { margin:0; padding:0;}
```
属性值出现小数点忽略0

```
/* 不推荐 */
.example { font-size:0.8em}
```
```
/* 推荐 */
.example { font-size:.8em}
```
省略URI外的引号

```
/* 不推荐 */
.example { background-image: url("images/noise.png");}
```
```
/* 推荐 */
.example { background-image: url(images/noise.png);}
```
十六进制尽可能使用3个字符
```
/* 不推荐 */
.example { color: #eebbcc; }
```
```
/* 推荐 */
.example { color: #ebc; }
```
## Hacks
尽可能地避免使用hack的方式解决浏览器样式兼容性问题。

尽量避免使用CSS filters。

# CSS代码格式规则

## 单行书写

一个类一行，每个属性间用空格隔开，不用强制换行。
```
/* 不推荐 */
.example { 
  display:block; 
  float:left; 
  width:200px; 
  height:300px;padding:10px; 
}
```
```
/* 推荐 */
.example { display: block; float: left; width: 200px; height: 300px; padding: 10px;}
```
## 分隔选择器
每个选择器和声明都要独立新行。
```
/* 不推荐 */
a:focus, a:active { position: relative; top: 1px;}
```
```
/* 推荐 */
h1,
h2,
h3 { font-weight: normal; line-height: 1.2;}
```
## 属性名完结
出于一致性的原因，在属性名和值之间加一个空格（可不是属性名和冒号之间噢）。
```
/* 不推荐 */
h3 { font-weight:bold;}
```
```
/* 推荐 */
h3 { font-weight: bold; }
```
## 声明完结
考虑到一致性和拓展性，请在每个声明尾部都加上分号。
```
/* 不推荐 */
.test {
  display: block;
  height: 100px
}
```
```
/* 推荐 */
.test { display: block; height: 100px;}
```
## css书写顺序
书写顺序按显示属性，自身属性， 文本属性顺序。

显示属性

 - display || visibility
 - list-style 
 - position 
 - top || right || bottom || left
 - z-index
 - float 
 - clear

元素属性

 - width 
 - max-width || min-width
 - height 
 - max-height || min-height
 - overflow || clip
 - margin 
 - padding 
 - outline
 - border 
 - background

内容属性

 - color 
 - font 
 - text-overflow
 - text-decoration 
 - text-align 
 - text-indent
 - line-height
 - white-space
 - vertical-align 
 - cursor
 - content

## 声明顺序
相关的属性声明应当归为一组，并按照下面的顺序排列：

 1. Positioning 
 2. Box model 
 3. Typographic 
 4. Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

完整的属性列表及其排列顺序请参考 [Recess][4]。

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```


## 格式
 - 小图片（必须）`sprite` 合并
 - 每个样式属性后加 "`;`"
 - 属性名的冒号后使用一个空格
 - 选择器分离和声明分离
```
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```
- 规则之间始终有一个空行
```
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}
```
- 选择器中避免标签名,如div.subnav
- 避免使用通配规则
- 规则越具体越好
尽量不要使用`ul li a`这样长的选择符，最好使用 `.content >.content-body >.title`之类的选择符。
- 省略“0”值后面的单位
- 使用小写的十六进制数字
在可能的情况下，使用3个字符的十六进制表示法。


# 基本语法

 - 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。 
 - 为选择器分组时，将单独的选择器单独放在一行。
 - 为了代码的易读性，在每个声明块的左花括号前添加一个空格。  
 - 声明块的右花括号应当单独成行。 每条声明语句的 `:`后应该插入一个空格。
 - 为了获得更准确的错误报告，每条声明都应该独占一行。
 - 所有声明语句都应当以分号结尾。最后一条声明语句后面的分号是可选的，但是，如果省略这个分号，你的代码可能更易出错。
 - 对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格（例如，`box-shadow`）。
 - 不要在`rgb()`、`rgba()`、`hsl()`、`hsla()` 或 `rect()`值的*内部*的逗号后面插入空格。这样利于从多个属性值（既加逗号也加空格）中区分多个颜色值（只加逗号，不加空格）。
 - 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，`.5` 代替 `0.5`；`-.5px` 代替 `-0.5px`）。
 - 十六进制值应该全部小写，例如，`#fff`。在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分。
 - 尽量使用简写形式的十六进制值，例如，用
   `#fff` 代替 `#ffffff`。 为选择器中的属性添加双引号，例如，`input[type="text"]`。[只有在某些情况下是可选的][5]，但是，为了代码的一致性，建议都加上双引号。
   避免为 0 值指定单位，例如，用 `margin: 0;` 代替 `margin: 0px;`。

对于这里用到的术语有疑问吗？请参考 Wikipedia 上的 [syntax section of the Cascading Style Sheets article][6]。

## 不要使用 `@import`
与 `<link>` 标签相比，`@import` 指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法有以下几种：

使用多个 `<link>` 元素
通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
通过 Rails、Jekyll 或其他系统中提供过 CSS 文件合并功能
请参考 [Steve Souders][7] 的文章了解更多知识。

```html
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

<!-- Avoid @imports -->
<style>
  @import url("more.css");
</style>
```

## 媒体查询（Media query）的位置
将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。下面给出一个典型的实例。

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

## 带前缀的属性
当使用特定厂商的带有前缀的属性时，通过缩进的方式，让每个属性的值在垂直方向对齐，这样便于多行编辑。

在 Textmate 中，使用 **Text → Edit Each Line in Selection** (⌃⌘A)。在 Sublime Text 2 中，使用 **Selection → Add Previous Line** (⌃⇧↑) 和 **Selection → Add Next Line** (⌃⇧↓)。

```css
/* Prefixed properties */
.selector {
  -webkit-box-shadow: 0 1px 2px rgba(0,0,0,.15);
          box-shadow: 0 1px 2px rgba(0,0,0,.15);
}
```
## 单行规则声明
对于只包含一条声明的样式，为了易读性和便于快速编辑，建议将语句放在同一行。对于带有多条声明的样式，还是应当将声明分为多行。

这样做的关键因素是为了错误检测 -- 例如，CSS 校验器指出在 183 行有语法错误。如果是单行单条声明，你就不会忽略这个错误；如果是单行多条声明的话，你就要仔细分析避免漏掉错误了。

```css
/* Single declarations on one line */
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

/* Multiple declarations, one per line */
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url(../img/sprite.png);
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }

```
## 简写形式的属性声明
在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

 - `padding` 
 - `margin` 
 - `font` 
 - `background` 
 - `border` 
 - `border-radius`

大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

在 MDN（Mozilla Developer Network）上一篇非常好的关于[shorthand properties][8] 的文章，对于不太熟悉简写属性声明及其行为的用户很有用。

```css
/* Bad example */
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

/* Good example */
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

## Less 和 Sass 中的嵌套
避免不必要的嵌套。这是因为虽然你可以使用嵌套，但是并不意味着应该使用嵌套。只有在必须将样式限制在父元素内（也就是后代选择器），并且存在多个需要嵌套的元素时才使用嵌套。

扩展阅读：

 - [Nesting in Sass and Less][9]

```css
// Without nesting
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// With nesting
.table > thead > tr {
  > th { … }
  > td { … }
}
```

## Less 和 Sass 中的操作符
为了提高可读性，在圆括号中的数学计算表达式的数值、变量和操作符之间均添加一个空格。
```css
// Bad example
.element {
  margin: 10px 0 @variable*2 10px;
}

// Good example
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```
## 代码组织

 - 以组件为单位组织代码段。
 - 制定一致的注释规范。
 - 使用一致的空白符将代码分隔成块，这样利于扫描较大的文档。 
 - 如果使用了多个CSS文件，将其按照组件而非页面的形式分拆，因为页面会被重组，而组件只会被移动。
```css
/*
 * Component section heading
 */

.element { ... }


/*
 * Component section heading
 *
 * Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
 */

.element { ... }

/* Contextual sub-component or modifer */
.element-heading { ... }
```

## 编辑器配置
将你的编辑器按照下面的配置进行设置，以避免常见的代码不一致和差异：

 - 用两个空格代替制表符（soft-tab 即用空格代表 tab 符）。
 - 保存文件时，删除尾部的空白符。
 - 设置文件编码为 UTF-8。
 - 在文件结尾添加一个空白行。

参照文档并将这些配置信息添加到项目的 `.editorconfig` 文件中。例如：[Bootstrap 中的 .editorconfig 实例][10]。更多信息请参考 [about EditorConfig][11]。


# 样式初始化模板
```
/* CSS Reset */ 
body, div, span, object, input, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, samp, small, strong, sub, sup, tt, var, b, i, dl, dt, dd,ol,ul, li, fieldset, form, label, legend, table, caption, tbody,tfoot, thead, tr, th, td, hr { padding: 0; margin: 0; } 
table { border-collapse: collapse; border-spacing: 0; } 
caption{ text-align:left;} 
input,select{ vertical-align:middle;} 
input,textarea,select{ font:12px Arial, Helvetica, sans-serif; } 
fieldset, img { border: 0; } 
address,code,caption,th,cite,dfn,em,var{font-style:normal;} 
ol, ul { list-style: none; } 
h1, h2, h3, h4, h5, h6 { font-size: 100%; } 
q:before, q:after { content:""; } 
legend{ display:none;} 
```
## 清除浮动
```
.clearfix:after{ content: ""; height: 0; visibility: hidden; display: block; clear: both;} 
.clearfix{ zoom: 1;}
```


  [1]: http://jigsaw.w3.org/css-validator/
  [2]: http://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/
  [3]: http://markdotto.com/2012/03/02/stop-the-cascade/
  [4]: http://twitter.github.com/recess
  [5]: http://mathiasbynens.be/notes/unquoted-attribute-values#css
  [6]: http://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax
  [7]: http://www.stevesouders.com/blog/2009/04/09/dont-use-import/
  [8]: https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties
  [9]: http://markdotto.com/2015/07/20/css-nesting/
  [10]: https://github.com/twbs/bootstrap/blob/master/.editorconfig
  [11]: http://editorconfig.org/