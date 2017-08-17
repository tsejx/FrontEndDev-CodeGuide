# HTML编码规范

# 基本准则
+ 符合Web标准
+ 语义化HTML
+ 结构、表现、行为分离
+ 兼容性优良
+ 页面性能良好
+ 代码要求简洁明了有序
+ 尽可能的减小服务器的负载
+ 保证最快的解析速度




# 一般规范
## 文件/资源命名

 - 文件命名以**字母开头**，**全部小写**，单词之间**以减号（-）连接**，如`my-camel-case-name.css`。（驼峰命名法用在javascript的变量及函数的命名中）
 - 很多浏览器会将含有这些词的作为广告拦截： ad、ads、adv、banner、sponsor、gg、guangg、guanggao等 页面中尽量避免采用以上词汇来命名。

## 协议
- `src`和`url`所指路径不带`http:`或`https:`，如`src="//cdn.com/foundation.min.js"`。

## 关注点分离
- 严格地保证结构、表现、行为三者分离，并尽量使三者之间没有太多的交互和联系。

就是说，尽量在文档和模板中只包含结构性的 HTML，而将所有表现代码，移入样式表中；将所有动作行为，移入脚本之中。


# 排版规则

## 缩进

- 使用2个空格缩进
- 嵌套元素应当缩进一次（即两个空格）
```
<ul>
  <li>Fantastic</li>
  <li>Great</li>
</ul>
```
```
.example {
  color: blue;
}
```
## 制表符 Tab键
Tab键用两个空格代替

因为在不同系统的编辑工具对`tab`解析不一样，Windows下的`Tab`键是占四个空格的位置，而在Linux下会变成占八个空格的位置（除非你 自己设定了`Tab`键所占的位置长度）。




## 大小写
只允许使用小写。

所有的代码都用小写字母：适用于元素名，属性，属性值（除了文本和CDATA）， 选择器，特性，特性值（除了字符串）。
```
<!-- 不推荐 -->
<A HREF="/">Home</A>
```
```
<!-- 推荐 -->
<img src="google.png" alt="Google">
```
## 行尾断句
每个样式属性或者每句代码后加 ";"

方便压缩工具"断句"。

## 行尾空格
建议删除行尾白空格。
```
<!-- 不推荐 -->
<p>What?  </p>
```
```
<!-- 推荐 -->
<p>Yes please.</p>
```
## 标签结束

 - 不要在自闭合（self-closing）元素的尾部添加斜线 -- [HTML5 规范][1]中明确说明这是可选的。
 - 不要省略可选的结束标签（closing tag）（例如，`</li>` 或 `</body>`）。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
```

## 注释
尽可能的去解释你写的代码。说明该代码包括什么、目的是什么、能做什么、为什么使用它等。

注释是否需要详尽，取决于项目的复杂程度。

习惯性书写注释，方便日后维护

一般单行注释：
```
<!-- col -->
```
模块间注释：
```
<!-- news -->
<div class="news">
  <h2>News</h2>
  <p>...</p>
</div>
<!--/ news -->
```
循环注释：
```
<ul>
  <!-- loop: new list -->
  <li>new's title 1</li>
  <li>new's title 2</li>
  <li>new's title 3</li>
  <li>new's title 4</li>
  <li>new's title 5</li>
  <!-- /loop: new list -->
</ul>
```
cms输出注释：
```
<!-- cms: news list -->
<ul>
  <li>new's title 1</li>
  <li>new's title 2</li>
  <li>new's title 3</li>
  <li>new's title 4</li>
  <li>new's title 5</li>
</ul>
<!-- /cms: news list -->
```
Tab选项卡内容注释：
```
<!-- tab: news list -->
<div class="tab"></div>
<!-- /tab: news list -->
```

# 常规HTML设计规则 - head部分

## 文档类型

使用html5文档声明，不再使用XHTML（application/xhtml+xml）。

HTML5是目前所有HTML文档类型中的首选：
```html
<!DOCTYPE html>
```

## HTML5 DOCTYPE
为每个 HTML页面的第一行添加标准模式（standard mode）的声明，这样能够确保在每个浏览器中拥有一致的展现。
```
:::html
    <!DOCTYPE html>
    <html>
      <head>
      </head>
    </html>
```

## 语言属性

根据 HTML5 规范：

    强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。

更多关于 `lang` 属性的知识可以从 [此规范][3] 中了解。

这里列出了[语言代码表][4]。
```
<html lang="en-us">
  <!-- ... -->
</html>
```

## IE兼容模式
IE 支持通过特定的 `<meta>` 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 **`edge mode`**，从而通知 IE 采用其所支持的最新的模式。
[阅读这篇 stack overflow][2] 上的文章可以获得更多有用的信息。
```
    :::html
    <meta http-equiv="X-UA-Compatible" content="IE=Edge">
```
## 字符编码
通过明确声明字符编码，能够确保浏览器快速并容易的判断页面内容的渲染方式。这样做的好处是，可以避免在 HTML 中使用字符实体标记（character entity），从而全部与文档编码一致（约定一致采用`UTF-8`编码，如果是cms站点，则遵守该站点的编码规则。）。
```html
    :::html
    <head>
      <meta charset="UTF-8">
    </head>
```

## 引入CSS和JavaScript文件
根据 HTML5 规范，在引入 CSS 和 JavaScript 文件时一般不需要指定 `type` 属性，因为 `text/css` 和 `text/javascript` 分别是它们的默认值。

**HTML5 spec links**

 - [Using link][5] 
 - [Using style][6] 
 - [Using script][7]

```html
<!-- External CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- In-document CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

# 常规HTML设计规则 - body部分

## HTML 的正确性

编写有效、正确的HTML代码，否则很难达到性能上的提升。

可以使用一些工具验证你的代码，如 W3C HTML validator


##HTML 的语义性
根据HTML各个元素的用途而去使用它们。
```
<!-- 不推荐 -->
<div class="col">
  <div class="title">news</div>
  <p>list1</p>
  <p>list2</p>
  <p>list3</p>
</div>
```
```
<!-- 推荐 -->
<div class="col">
  <h2 class="title">news</h2>
  <p>list1</p>
  <p>list2</p>
  <p>list3</p>
</div>
```
部分标签说明：

 - `div` 主要用于布局，分割页面的结构;
 - `ul/ol` 主要用于无序/有序列表;
 - `dl/dt/dd` 当页面中出现第一行为类似标题/简述，然后下面为详细描述的内容时应该使用该标签;
 - `span` 没有特殊的意义，可以用作排版的辅助，然后在css中定义span;
 - `h1-h6` 标题, 根据重要性依次递减;
 - `h1` 最重要的标题;
 - `label` 使表单更有亲和力而且能辅助表单排版;
不推荐使用的标签：
 - `font` 文字的外观，大小和颜色;
 - `u` 文本下划线;
 - `center` 居中对齐;
 - `s` 删除线;
 - `strike` 删除线;
 - `noframes` 无视框时的内容;
 - `iframe` 定义嵌入视图;
 - `isindex` 不建议使用（可搜寻，使用input代替）;
 - `dir` 目录式列举;
 - `menu` 菜单列表;
 - `basefont` 定义基本字体;
 - `applet` 定义java程序;
 - `frame` 定义个别视框;
 - `frameset` 视框格式总定义;

## 语义化标签

![主流页面布局](http://upload-images.jianshu.io/upload_images/3067059-78b3611c7b1a5366.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 - `<header>` 表示页眉,页头
 - `<nav>` 表示导航内容；
 - `<section>` 表示文档中的节、区段，一般包含标题和内容
 - `<article>` 可以看成是一种特殊类型的section元素，比section更强调独立性。比如blog的内容，报纸的文章。（具体区别可以查看div section 和article的区别）；
 - `<aside>` 表示article以外的内容，而且应该和article有一定的关系，块级元素;
 - `<footer>` 表示页脚；
 - `<div>` 本身无特殊含义，用于布局。<br/>

另外，尽量用alt标签去描述图片。

HTML 标签的目的，是为展示内容信息。

 - 不要引入一些特定的 HTML 结构来解决一些视觉设计问题
 - 不要将 img 元素当做专门用来做视觉设计的元素

## 属性
1.HTML 属性应当按照以下给出的顺序依次排列，确保代码的易读性。

 
- `class`(首位)
- `id` 、 `name`
- `data-*`
- `src`、`for`、 `type`、 `href`
- `title`、`alt`
- `aria-*`、 `role`

2.id 和 class
`class` 用于标识高度可复用组件，因此应该排在首位。`id` 用于标识具体组件，应当谨慎使用（例如，页面内的书签），因此排在第二位。

`id`一般用于网页大致布局，比如标志、导航、主体内容、版权，规范命名为`#logo` , `#nav`, `#content` ,`#copyright`。
一般项目中`class`用于`css`中，`id`被`js`用来操作`dom`且不添加样式，（`jq`操作的`class`一般不加样式）。

```html
<a class="..." id="..." data-toggle="modal" href="#">
  Example link
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

class的命名原则：

- 内容优先，表现为辅
- 一律小写，多个单词以连字符连接

3.对于属性的定义，确保全部使用双引号，绝不要使用单引号。

## type属性
在样式表和脚本的标签中忽略type属性。

HTML5默认type为text/css和text/javascript类型，所以没必要指定。即便是老浏览器也是支持的。

```
<!-- 不推荐 -->
<link rel="stylesheet" href="//www.google.com/css/maia.css" type="text/css">
<script src="//www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>
```
```
<!-- 推荐 -->
<link rel="stylesheet" href="//www.google.com/css/maia.css">
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
```
## 多媒体元素降级处理
给多媒体元素，比如`canvas`、`videos`、 `images`增加`alt`属性，提高可用性（特别是常用的img标签，尽可量得加上alt属性，提供图片的描述信息）。
```
<!-- 不推荐 -->
<img src="world.jpg">
```
```
<!-- 推荐 -->
<img src="world.jpg" alt="our world images">
```

#HTML代码格式规则
每个块元素、列表元素或表格元素都独占一行，每个子元素都相对于父元素进行缩进。按设计稿划分模块，尽量使页面模块化，模块与模块之前要有清晰的注释。

html form
如上面页面框架，推荐写法：
```html
<!-- hader -->
<div class="header">header</div>
<!-- /hader -->

<!-- nav -->
<div class="nav">nav</div>
<!-- /nav -->

<!-- main -->
<div class="main">
  <!-- container -->
  <div class="container">
    <!--news-->
    <div class="news">
      <h2>news<h2>
      <p>...</p>
    </div>
    <!--news-->
  </div>
  <!--/container-->
  <!--sidebar-->
  <div class="sidebar">sidebar</div>
  <!--sidebar-->
</div>
<!--/main-->

<!--footer--> 
<div class="footer">footer</div> 
<!--/footer-->
```

1. html中使用双引号，不用单引号，如class="news-article"。
2. 每一个块状元素，列表元素和表格元素后，加上一新空白行。
3. 内联元素写在一行内，块状元素还有列表和表格要另起一行。

## 命名参考规范
### (1)页面结构

* 容器: `container`
* 页头：`header`
* 内容：`content/container`
* 页面主体：`main`
* 页尾：`footer`
* 导航：`nav`
* 侧栏：`sidebar`
* 栏目：`column`
* 页面外围控制整体布局宽度：`wrapper`
* 左右中：`left right center` 
* `section` 表示文档中的节、区段，可以和h1-h6一起来显示文档结构
* `article` 表示一块比较独立的内容或者主题内容，块级元素，比如blog的内容，报纸的文章
* `aside` 表示article以外的内容，而且应该和article有一定的关系，块级元素
* `hgroup` 表示一个文档、区段(section)的标题组合
* `figure` 表示以相对独立的或外引的元素，如img video
* `figcaption` 表示 figure内容的标题

### (2)导航

* 导航：`nav`
* 主导航：`mainnav`
* 子导航：`subnav`
* 顶导航：`topnav`
* 边导航：`sidebar`
* 左导航：`leftsidebar`
* 右导航：`rightsidebar`
* 菜单：`menu`
* 子菜单：`submenu`
* 标题: `title`
* 摘要:`summary`
　　
### (3)功能

* 标志：`logo`
* 广告：`banner`
* 登陆：`login`
* 登录条：`loginbar`
* 注册：`regsiter`
* 搜索：`search`
* 功能区：`shop`
* 标题：`title`
* 加入：`joinus`
* 状态：`status`
* 按钮：`btn`
* 滚动：`scroll`
* 标签页：`tab`
* 文章列表：`list`
* 提示信息：`msg`
* 当前的: `current`
* 小技巧：`tips`
* 图标: `icon`
* 注释：`note`
* 指南：`guild`
* 服务：`service`
* 热点：`hot`
* 新闻：`news`
* 下载：`download`
* 投票：`vote`
* 合作伙伴：`partner`
* 友情链接：`link`
* 版权：`copyright`
　　
### (4)class的命名

* (1)颜色：使用颜色的名称或者16进制代码，如：
  * `.red { color: red; } .f60 { color: #f60; } .ff8600 { color: #ff8600; }`

* (2)字体大小，直接使用“font+字体大小”作为名称，如：
  * `.font12px { font-size: 12px; } .font9pt {font-size: 9pt; }`
* (3)对齐样式，使用对齐目标的英文名称，如：
  * `.left { float:left; } .bottom { float:bottom; }`
* (4)标题栏样式，使用“类别+功能”的方式命名，如：
  * `.barnews { } .barproduct { }`
<br/>

* **注意事项：**
  1. 一律小写；
  2. 尽量用英文；
  3. 尽量不加中杠和下划线；
  4. 尽量不缩写，除非一看就明白的单词，如：wrapper可以写成wrap。

### (5)id和class命名约定
1. id 和 class 的命名基本原则: *内容优先，表现为辅*。首先根据内容来命名，如:`#header`,`#footer`,`.main-nav`.如根据内容无法找到合适的命名，可以再结合表现进行命名，如：`col-main`, `col-sub`, `col-extra`,`blue-box`
2. id 和 class的名称一律小写，多个单词以连字符连接，如： `main-wrap`
3. id 和 class的名称只能出现，小写字母，数字和连字符( - )(js钩子除外)
4. id 和 class的名称尽量使用英文单词命名,如确实找不到合适的单词，可以使用拼音，如：`zhidao-com`
5. 在不影响语意的情况下，id 和 class 的名称 可以适当使用缩写，如: `col`, `nav`, `hd`, `bd`, `fd`(缩写只用来表示结构，不允许写任何样式)。不要自造缩写。
6. class 对于选中命名`.selected`;对于hover，支持伪类使用`:hover`，不支持的使用 `.hover`，隐藏使用`.hide` 。
7. id 和 class的选择，如果只使用一次，使用id,如果使用多次使用class，如果需要和js交互，使用id,如果需要交互并且页面中有大量重复，请参见下一条。
8. 对于作为js钩子的 id 和 class 命名规则为以”J_“开头(J,象形钩子的形状)，后面加上原应有的命名，在使用class的时候需要放在最前面。如:`class="J_tab-content some-mod-content"`。（注意：钩子，不允许在css中定义任何的样式效果）
9. 很多浏览器会将含有这些词的作为广告拦截： `ad`、`ads`、`adv`、`banner`、`sponsor`、`gg`、`guangg`、`guanggao`等 页面中尽量避免采用以上词汇来命名。

### (6)z-index
1. 自己写的z-index的值不能超过 100 (通用组的除外)
2. 页面中的元素内容的z-index不能超过10(popup poptip除外)，需要按照内容定义1 2 3 4不允许直接使用如1000，9999
3. popup poptip的z-index需要按照内容使用 99以下，10以上的值（11,12,13，也可以小于10），不允许直接使用1000，9999之类大值
现在通用z-index记录,使用时请避开和灵活使用
|z-index|使用者|类型|
|:-------:|:-------:|:----:|
|<10|page-content|页面级别|
|<word>></word>10, <99|page-popup|页面级别|
|20|usercard用户名片|common通用|
||MSG气泡消息|common通用|
||Dialog-Cover|common通用|
||Dialog|common通用|
***

# HTML与SEO

## 页面良好层次

保证整个页面在未加载样式表时仍有较好的层次清晰的页面结构。
```
<!-- 不推荐 -->
<div class="logo">My Site</div>
<div class="nav">
  <a href="#">Home</a>
  <a href="#">News</a>
  <a href="#">Mobile</a>
</div>
<div class="news">
  <div>News</div>
  <a href="#">news list 1</a>
  <a href="#">news list 2</a>
  <a href="#">news list 3</a>
</div>
```
```
<!-- 推荐 -->
<h1 class="logo">My Site</h1>
<ul class="nav">
  <li><a href="#">Home</a></li>
  <li><a href="#">News</a></li>
  <li><a href="#">Mobile</a></li>
</ul>
<div class="news">
  <h2>News</h2>
  <ul>
    <li><a href="#">news list 1</a></li>
    <li><a href="#">news list 2</a></li>
    <li><a href="#">news list 3</a></li>
  </ul>
</div>
```
权重标签使用
H标签使用
 - h1 权重高，体现当前网页中相对比较重要的信息，但不宜过多，建议一个页面只放一个;
 - h2 可以做副标题;
 - h3 可以做新闻列表;
 - h4-h6 可做相关新闻的列表标签属性完整;
`strong`、`b`使用
将需要加粗的文字使用b标签来显示。

将需要强调的文字（主要指包含关键词的信息）使用`strong`标签来强调主要内容。

注：b是粗体标签，属于实体标签，它所包围的字符将被设为bold（粗体）；strong 是加重语气标签，属于逻辑标签，它的作用是加强字符语气。

## 标签属性使用
在很多情况下，a都要使用title来说明该链接的相关说明或目的意义。

例如：当使用overflow隐藏掉a中的溢出文字时，该a中的title是必不可少的，它可以告诉用户被隐藏掉的文字内容是什么；又或者当一个图片型链接出现时，该a中的title同样是必不可少的，它可以告诉用户这个图片链接是做什么用的。

注：仅在img里添加alt标签在火狐提示文字是出不来的，alt是图片加载失败或未加载完全时显示出来的提示文字，要想鼠标移上去显示提示信息应该用title，严谨的写法是img里加入alt和title这两个标签。

## 精简代码
代码保持精简，最优化，这样搜索引擎才更喜欢。


# HTML文档模板
```html
:::html
<!DOCTYPE HTML>
<html lang="en-us">
    <head>
        <meta charset="utf-8" />
        <title>Sample page</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <link rel="stylesheet" href="css_example_url" />
        <script src="js_example_url"></script>
    </head>
    <body>
        <section id="page">
            <header id="header">
              页头
            </header>
            <section id="body">
              主体
            </section>
            <footer id="footer">
              页尾
            </footer>
        </section>
        <script>
        // 你的代码
        </script>
    </body>
</html>
```


  [1]: http://dev.w3.org/html5/spec-author-view/syntax.html#syntax-start-tag
  [2]: http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e
  [3]: http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-html-element
  [4]: http://reference.sitepoint.com/html/lang-codes
  [5]: http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element
  [6]: http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element
  [7]: http://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element