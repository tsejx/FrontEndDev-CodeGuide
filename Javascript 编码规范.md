# Javascript 编码规范

## 命名规范
函数和变量命名采用驼峰命名法。
## 编码规则
1. 采用统一的缩进方式排版代码；
2. 关键词、条件括弧后面使用空格；运算操作符号两侧使用空格；语句分割符‘,’后面使用空格；

```javascript
    var name[空格]=[空格]value;
      if[空格](a,[空格]b) {
    }
```

3. 左大括号"{"可以居行尾，也可写在下行首（独自一行）,右大括号"}"单独占一行，居行首；
4. 句末必须用分号结尾；
5. 单行过长应在适当位置予以换行,增强可读性；
6. if、while、for、do语句的执行体总是用"{"和"}"括起来，即使在其结构体内只有一条语句；
7. 语法意义相互独立的代码将用空行分隔。


# JavaScript 编码风格

## 命名

通常，使用 `functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis` 和 `SYMBOLIC_CONSTANTS_LIKE_THIS` 。具体如下：

### 属性和方法

 - 文件或类中的私有属性，变量和方法名应该以下划线 "_" 开头； 
 - 保护属性, 变量和方法名不需要下划线开头，和公共变量名一样。
   
### 方法和函数参数
 - 可选参数以 `opt_` 开头；
 - 函数的参数个数不固定时，应该添加最后一个参数 `var_args`为参数的个数。你也可以不设置`var_args` 而取代使用 `arguments`；
 - 可选和可变参数应该在 `@param`标记中说明清楚。

虽然这两个规定对编译器没有任何影响，但还是请尽量遵守。

### Getters 和 Setters

`Getters` 和 `setters` 并不是必要的。但只要使用它们了，就请将 `getters` 命名成 `getFoo()` 形式，将 `setters` 命名成 `setFoo(value)` 形式。(对于布尔类型的 `getters`，使用 `isFoo()` 也可。)

### 命名空间

JavaScript 不支持包和命名空间。

不容易发现和调试全局命名的冲突，多个系统集成时还可能因为命名冲突导致很严重的问题。为了提高 JavaScript 代码复用率，我们遵循下面的约定以避免冲突。

**为全局代码使用命名空间**

在全局作用域上，使用一个唯一的，与工程/库相关的名字作为前缀标识。比如：你的工程是 "Project Sloth", 那么命名空间前缀可取为 `sloth.*` 。

```javascript
var sloth = {}; 
 
sloth.sleep = function() { 
  ... 
};
```
**明确命名空间所有权**

当选择了一个子命名空间，请确保父命名空间的负责人知道你在用哪个子命名空间。比如说, 你为工程 `'sloths'` 创建一个 `'hats'` 子命名空间, 那确保 Sloth 团队人员知道你在使用 `sloth.hats`.

**外部代码和内部代码使用不同的命名空间**

"外部代码" 是指来自于你代码体系的外部，可以独立编译。内外部命名应该严格保持独立。如果你使用了外部库，他的所有对象都在 `foo.hats.*` 下，那么你自己的代码不能在 `foo.hats.*` 下命名，因为很有可能其他团队也在其中命名。

**重命名那些名字很长的变量，提高可读性**

主要是为了提高可读性。局部空间中的变量别名只需要取原名字的最后部分。
```javascript
/** 
 * @constructor 
 */ 
some.long.namespace.MyClass = function() { 
}; 
 
/** 
 * @param {some.long.namespace.MyClass} a 
 */ 
some.long.namespace.MyClass.staticHelper = function(a) { 
  ... 
}; 
 
myapp.main = function() { 
  var MyClass = some.long.namespace.MyClass; 
  var staticHelper = some.long.namespace.MyClass.staticHelper; 
  staticHelper(new MyClass()); 
}; 
```
**不要对命名空间创建别名**
```javascript
myapp.main = function() { 
  var namespace = some.long.namespace; 
  namespace.MyClass.staticHelper(new namespace.MyClass()); 
};
```
不要在全局范围内创建别名，而仅在函数块作用域中使用。
```javascript
myapp.main = function() { 
  var MyClass = some.long.namespace.MyClass; 
  MyClass.staticHelper(null); 
};
```
### 文件名

文件名应该使用小写字符，以避免在有些系统平台上不识别大小写的命名方式。文件名以 `.js` 结尾，不要包含除 `-` 和 `_` 外的标点符号(使用 `-` 优于 `_`)。

## 自定义 toString() 方法
可自定义 `toString()` 方法，但确保你的实现方法满足：（1）总是成功；（2）没有其他负面影响。如果不满足这两个条件，那么可能会导致严重的问题。比如：如果 `toString()` 调用了包含 `assert` 的函数，`assert` 输出导致失败的对象，这在 `toString()` 也会被调用。

## 延迟初始化
可以延迟变量的初始化，没有必要在每次声明变量时就将其初始化。

## 明确作用域
任何时候都要明确作用域，以提高可移植性和清晰度。

例如，不要依赖于作用域链中的 window 对象。可能在其他应用中，你函数中的 window 不是指之前的那个窗口对象。

## 代码格式化

### 大括号

分号会被隐式插入到代码中，所以你务必在同一行上插入大括号。例如：
```javascript
if (something) { 
  // ... 
} else { 
  // ... 
}
```
### 数组和对象的初始化

**如果初始值不是很长，就保持写在单行上：**
```javascript
var arr = [1, 2, 3];  // No space after [ or before ].
var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.
```
**初始值占用多行时，缩进2个空格：**
```javascript
// Object initializer. 
var inset = { 
  top: 10, 
  right: 20, 
  bottom: 15, 
  left: 12 
};

// Array initializer. 
this.rows_ = [ 
  '"Slartibartfast" ', 
  '"Zaphod Beeblebrox" ', 
  '"Ford Prefect" ', 
  '"Arthur Dent" ', 
  '"Marvin the Paranoid Android" ', 
  'the.mice@magrathea.com' 
];

// Used in a method call. 
goog.dom.createDom(goog.dom.TagName.DIV, { 
  id: 'foo', 
  className: 'some-css-class', 
  style: 'display:none' 
}, 'Hello, world!');
```
**比较长的标识符或者数值，不要为了让代码好看些而手工对齐：**
```javascript
CORRECT_Object.prototype = { 
  a: 0, 
  b: 1, 
  lengthyName: 2 
};
```
```
// 不要这样做
WRONG_Object.prototype = { 
  a          : 0, 
  b          : 1, 
  lengthyName: 2 
};
```
### 函数参数

尽量让函数参数在同一行上。如果一行超过 80 字符，每个参数独占一行，并以4个空格缩进，或者与括号对齐，以提高可读性。尽可能不要让每行超过80个字符。
```javascript
// Four-space, wrap at 80.  Works with very long function names, survives
// renaming without reindenting, low on space.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
};

// Four-space, one argument per line.  Works with long function names,
// survives renaming, and emphasizes each argument.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
  // ...
};

// Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
// low on space.
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
}

// Parenthesis-aligned, one argument per line.  Emphasizes each
// individual argument.
function bar(veryDescriptiveArgumentNumberOne,
             veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy,
             artichokeDescriptorAdapterIterator) {
  // ...
}
```
### 传递匿名函数

如果参数中有匿名函数，函数体从调用该函数的左边开始缩进2个空格，而不是从 function 这个关键字开始。这让匿名函数更加易读 (不要增加很多没必要的缩进让函数体显示在屏幕的右侧)。
```javascript
var names = items.map(function(item) { 
                        return item.name; 
                      });
```
```javascipt
prefix.something.reallyLongFunctionName('whatever', function(a1, a2) { 
  if (a1.equals(a2)) { 
    someOtherLongFunctionName(a1); 
  } else { 
    andNowForSomethingCompletelyDifferent(a2.parrot); 
  } 
});
```
### 更多的缩进

事实上，除了初始化数组和对象，和传递匿名函数外，所有被拆开的多行文本要么选择与之前的表达式左对齐，要么以4个(而不是2个)空格作为一缩进层次。
```
someWonderfulHtml = '' +
                    getEvenMoreHtml(someReallyInterestingValues, moreValues,
                                    evenMoreParams, 'a duck', true, 72,
                                    slightlyMoreMonkeys(0xfff)) +
                    '';

thisIsAVeryLongVariableName =
    hereIsAnEvenLongerOtherFunctionNameThatWillNotFitOnPrevLine();

thisIsAVeryLongVariableName = siblingOne + siblingTwo + siblingThree +
    siblingFour + siblingFive + siblingSix + siblingSeven +
    moreSiblingExpressions + allAtTheSameIndentationLevel;

thisIsAVeryLongVariableName = operandOne + operandTwo + operandThree +
    operandFour + operandFive * (
        aNestedChildExpression + shouldBeIndentedMore);

someValue = this.foo(
    shortArg,
    'Some really long string arg - this is a pretty common case, actually.',
    shorty2,
    this.bar());

if (searchableCollection(allYourStuff).contains(theStuffYouWant) &&
    !ambientNotification.isActive() && (client.isAmbientSupported() ||
                                        client.alwaysTryAmbientAnyways())) {
  ambientNotification.activate();
}
```
### 空行

使用空行来划分一组逻辑上相关联的代码片段。
```javascript
doSomethingTo(x); 
doSomethingElseTo(x); 
andThen(x); 
 
nowDoSomethingWith(y); 
 
andNowWith(z);
```
### 二元和三元操作符

操作符始终跟随着前行，这样就不用顾虑分号的隐式插入问题。如果一行实在放不下，还是按照上述的缩进风格来换行。
```javascript
var x = a ? b : c;  // All on one line if it will fit. 
 
// Indentation +4 is OK. 
var y = a ? 
    longButSimpleOperandB : longButSimpleOperandC; 
 
// Indenting to the line position of the first operand is also OK. 
var z = a ? 
        moreComplicatedB : 
        moreComplicatedC;
```
## 括号
括号只在需要的时候使用。

不要滥用括号，只在必要的时候使用它。

对于一元操作符(如 `delete`, `typeof` 和 `void` )，或是在某些关键词(如 `return`, `throw`, `case`, `new` )之后，不要使用括号。

## 字符串
使用 单引号(') 优于 双引号(") 。
```javascript
var msg = 'This is some HTML';
```
## 可见性
用 `@private` 和 `@protected` 来指名类、函数、属性的可见性。

标记为 `@private` 的全局变量和函数，表示他们只能在当前文件中访问。

标记为 `@private` 的构造函数，表示该类只能在当前文件或是其静态/普通成员中实例化。私有构造函数的公共静态属性在当前文件的任何地方都可访问，通过 `instanceof` 操作符也可。

永远不要为全局变量，函数，构造器加 `@protected` 标记。
```javascript
// File 1. 
// AA_PrivateClass_ and AA_init_ are accessible because they are global 
// and in the same file. 
 
/** 
 * @private 
 * @constructor 
 */ 
AA_PrivateClass_ = function() { 
}; 
 
/** @private */ 
function AA_init_() { 
  return new AA_PrivateClass_(); 
} 
 
AA_init_();
```
标记为 `@private` 的属性，在当前文件中可访问它。如果是类属性私有，"拥有"该属性的类的所有静态/普通成员也可访问，但它们不能被不同文件中的子类访问或覆盖。

标记为 `@protected` 的属性，在当前文件中可访问它。如果是类属性私有，那么"拥有"该属性的类及其子类中的所有静态/普通成员也可访问。
```javacript
// File 1. 
     
/** @constructor */ 
  AA_PublicClass = function() { 
}; 
 
/** @private */ 
AA_PublicClass.staticPrivateProp_ = 1; 
 
/** @private */ 
AA_PublicClass.prototype.privateProp_ = 2; 
 
/** @protected */ 
AA_PublicClass.staticProtectedProp = 31; 
 
/** @protected */ 
AA_PublicClass.prototype.protectedProp = 4; 
 
// File 2. 
 
/** 
 * @return {number} The number of ducks we've arranged in a row. 
 */ 
AA_PublicClass.prototype.method = function() { 
  // Legal accesses of these two properties. 
  return this.privateProp_ + AA_PublicClass.staticPrivateProp_; 
}; 
 
// File 3. 
 
/** 
 * @constructor 
 * @extends {AA_PublicClass} 
 */ 
AA_SubClass = function() { 
  // Legal access of a protected static property. 
  AA_PublicClass.staticProtectedProp = this.method(); 
}; 
goog.inherits(AA_SubClass, AA_PublicClass); 
 
/** 
 * @return {number} The number of ducks we've arranged in a row. 
 */ 
AA_SubClass.prototype.method = function() { 
  // Legal access of a protected instance property. 
  return this.protectedProp; 
}; 
```
## JavaScript 类型
<table class="js-type">
  <caption>javascript类型</caption>
  <tr>
    <td style="width:15%;">类型示例</td>
    <td>值示例</td>
    <td style="width:25%;">描述</td>
  </tr>
  <tr>
    <td>number</td>
    <td><pre>1<br>1.0<br>-5<br>1e5<br>Math.PI<br></pre></td>
    <td></td>
  </tr>
  <tr>
    <td>Number</td>
    <td><pre>new Number(true)</pre></td>
    <td>Number 对象</td>
  </tr>
  <tr>
    <td>string</td>
    <td><pre>'Hello'<br>"World"<br>String(42)</pre></td>
    <td>字符串值</td>
  </tr>
  <tr>
    <td>String</td>
    <td><pre>new String('Hello')<br>new String(42)</pre></td>
    <td>字符串对象</td>
  </tr>
  <tr>
    <td>boolean</td>
    <td><pre>true<br>false<br/>Boolean(0)</pre></td>
    <td>布尔值</td>
  </tr>
  <tr>
    <td>Boolean</td>
    <td><pre>new Boolean(true)</pre></td>
    <td>布尔对象</td>
  </tr>
  <tr>
    <td>RegExp</td>
    <td><pre>new RegExp('hello')<br>/world/g</pre></td>
    <td></td>
  </tr>
  <tr>
    <td>Date</td>
    <td><pre>new Date
new Date()</pre></td>
    <td></td>
  </tr>
  <tr>
    <td>null</td>
    <td><pre>null</pre></td>
    <td></td>
  </tr>
  <tr>
    <td>undefined</td>
    <td><pre>undefined</pre></td>
    <td></td>
  </tr>
  <tr>
    <td>void</td>
    <td><pre>function f() {<br>return;
}</pre></td>
    <td>没有返回值</td>
  </tr>
  <tr>
    <td>Array</td>
    <td><pre>['foo', 0.3, null]
[]</pre></td>
    <td>类型不明确的数组</td>
  </tr>
  <tr>
    <td>Array.<number></td>
    <td><pre>[11, 22, 33]</pre></td>
    <td>整型数组</td>
  </tr>
  <tr>
    <td>Array.<Array.<string>></td>
    <td><pre>[['one', 'two', 'three'], ['foo', 'bar']]</pre></td>
    <td>字符串数组的数组</td>
  </tr>
  <tr>
    <td>Object</td>
    <td><pre>{}
{foo: 'abc', bar: 123, baz: null}</pre></td>
    <td>字符串数组的数组</td>
  </tr>
  <tr>
    <td>Object.<string></td>
    <td><pre>{'foo': 'bar'}</pre></td>
    <td>值为字符串的对象</td>
  </tr>
  <tr>
    <td>Object.<number, string></td>
    <td><pre>var obj = {};
obj[1] = 'bar';</pre></td>
    <td>键为整数，值为字符串的对象。
注意，JavaScript 中，键总是被转换成字符串，所以 obj['1'] == obj[1] 。也所以，键在 for...in 循环中是字符串类型。但在编译器中会明确根据键的类型来查找对象。</td>
  </tr>
  <tr>
    <td>Function</td>
    <td><pre>function(x, y) {
  return x * y;
}</pre></td>
    <td>函数对象</td>
  </tr>
  <tr>
    <td>function(number, number): number</td>
    <td><pre>function(x, y) {
  return x * y;
}</pre></td>
    <td>函数值</td>
  </tr>
  <tr>
    <td>SomeClass</td>
    <td><pre>/** @constructor */
function SomeClass() {}

new SomeClass();</pre></td>
    <td></td>
  </tr>
  <tr>
    <td>SomeInterface</td>
    <td><pre>/** @interface */
function SomeInterface() {}
        
SomeInterface.prototype.draw = function() {};</pre></td>
    <td></td>
  </tr>
  <tr>
    <td>project.MyClass	</td>
    <td><pre>/** @constructor */
project.MyClass = function () {}

new project.MyClass()
project.MyEnum	</pre></td>
    <td></td>
  </tr>
  <tr>
    <td>project.MyEnum</td>
    <td><pre>
/** @enum {string} */
project.MyEnum = {
  BLUE: '#0000dd',
  RED: '#dd0000'
};</pre></td>
    <td>枚举</td>
  </tr>
  <tr>
    <td>Element</td>
    <td><pre>document.createElement('div')</pre></td>
    <td>DOM 中的元素</td>
  </tr>
  <tr>
    <td>Node</td>
    <td><pre>document.body.firstChild</pre></td>
    <td>DOM 中的节点</td>
  </tr>
  <tr>
    <td>HTMLInputElement</td>
    <td><pre>htmlDocument.getElementsByTagName('input')[0]</pre></td>
    <td>DOM 中，特定类型的元素。</td>
  </tr>

</table>


### 可空 vs. 可选 参数和属性

JavaScript 是一种弱类型语言，明白可选，非空和未定义参数或属性之间的细微差别还是很重要的。

对象类型(引用类型)默认非空。注意：函数类型默认不能为空。 除了字符串，整型，布尔，undefined 和 null 外，对象可以是任何类型。
```
/** 
 * Some class, initialized with a value. 
 * @param {Object} value Some value. 
 * @constructor 
 */ 
function MyClass(value) { 
  /** 
   * Some value. 
   * @type {Object} 
   * @private 
   */ 
  this.myValue_ = value; 
}
```
告诉编译器 `myValue_` 属性为一对象或 `null`。如果 `myValue_` 永远都不会为 `null`，就应该如下声明：
```javascript
/** 
 * Some class, initialized with a non-null value. 
 * @param {!Object} value Some value. 
 * @constructor 
 */ 
function MyClass(value) { 
  /** 
   * Some value. 
   * @type {!Object} 
   * @private 
   */ 
  this.myValue_ = value; 
}
```
这样，当编译器在代码中碰到 `MyClass` 为 `null` 时，就会给出警告。

函数的可选参数可能在运行时没有定义，所以如果他们又被赋给类属性，需要声明成：
```javascript
/** 
 * Some class, initialized with an optional value. 
 * @param {Object=} opt_value Some value (optional). 
 * @constructor 
 */ 
function MyClass(opt_value) { 
  /** 
   * Some value. 
   * @type {Object|undefined} 
   * @private 
   */ 
  this.myValue_ = opt_value; 
}
```
这告诉编译器 `myValue_` 可能是一个对象，或 `null`，或 `undefined`。

注意：可选参数 `opt_value` 被声明成 `{Object=}`，而不是 `{Object|undefined}`. 这是因为可选参数可能是 `undefined`。虽然直接写 `undefined` 也并无害处，但鉴于可阅读性还是写成上述的样子。

最后，属性的非空和可选并不矛盾，属性既可是非空，也可是可选的。下面的四种声明各不相同：
```javascript
/** 
 * Takes four arguments, two of which are nullable, and two of which are 
 * optional. 
 * @param {!Object} nonNull Mandatory (must not be undefined), must not be null. 
 * @param {Object} mayBeNull Mandatory (must not be undefined), may be null. 
 * @param {!Object=} opt_nonNull Optional (may be undefined), but if present, 
 *     must not be null! 
 * @param {Object=} opt_mayBeNull Optional (may be undefined), may be null. 
 */ 
function strangeButTrue(nonNull, mayBeNull, opt_nonNull, opt_mayBeNull) { 
  // ... 
};
```
## 注释
我们使用 JSDoc 中的注释风格。行内注释使用 // 变量的形式。另外，我们也遵循 C++ 代码注释风格。这也就是说你需要：

+ 版权和著作权的信息，
+ 文件注释中应该写明该文件的基本信息（如，这段代码的功能摘要，如何使用，与哪些东西相关）
+ 类，函数，变量和必要的注释，
+ 期望在哪些浏览器中执行，
+ 正确的大小写，标点和拼写。

为了避免出现句子片段，请以合适的大/小写单词开头，并以合适的标点符号结束这个句子。

### 顶层/文件注释

顶层注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西。应该提供文件的大体内容，它的作者，依赖关系和兼容性信息。如下：
```
// Copyright 2009 Google Inc. All Rights Reserved. 
 
/** 
 * @fileoverview Description of file, its uses and information 
 * about its dependencies. 
 * @author user@google.com (Firstname Lastname) 
 */
 ```
### 类注释

每个类的定义都要附带一份注释，描述类的功能和用法。也需要说明构造函数参数。如果该类继承自其它类，应该使用 @extends 标记。如果该类是对接口的实现，应该使用 @implements 标记。
```javascript
/** 
 * Class making something fun and easy. 
 * @param {string} arg1 An argument that makes this more interesting. 
 * @param {Array.} arg2 List of numbers to be processed. 
 * @constructor 
 * @extends {goog.Disposable} 
 */ 
project.MyClass = function(arg1, arg2) { 
  // ... 
}; 
goog.inherits(project.MyClass, goog.Disposable);
```
### 方法与函数的注释

提供参数的说明。使用完整的句子，并用第三人称来书写方法说明。
```javascript
/** 
 * Converts text to some completely different text. 
 * @param {string} arg1 An argument that makes this more interesting. 
 * @return {string} Some return value. 
 */ 
project.MyClass.prototype.someMethod = function(arg1) { 
  // ... 
}; 
 
/** 
 * Operates on an instance of MyClass and returns something. 
 * @param {project.MyClass} obj Instance of MyClass which leads to a long 
 *     comment that needs to be wrapped to two lines. 
 * @return {boolean} Whether something occured. 
 */ 
function PR_someMethod(obj) { 
  // ... 
}
```
对于一些简单的，不带参数的 `getters`，说明可以忽略。
```javascript
/** 
 * @return {Element} The element for the component. 
 */ 
goog.ui.Component.prototype.getElement = function() { 
  return this.element_; 
};
```
### 属性注释

也需要对属性进行注释。
```javascript
/** 
 * Maximum number of things per pane. 
 * @type {number} 
 */ 
project.MyClass.prototype.someProperty = 4;
```
### 类型转换的注释

有时，类型检查不能很准确地推断出表达式的类型，所以应该给它添加类型标记注释来明确之，并且必须在表达式和类型标签外面包裹括号。
```javascript
/** @type {number} */ (x) 
(/** @type {number} */ x)
```
### JSDoc 缩进

如果你在 `@param` , `@return` , `@supported` , `@this` 或 `@deprecated` 中断行，需要像在代码中一样，使用4个空格作为一个缩进层次。
```javascript
/** 
 * Illustrates line wrapping for long param/return descriptions. 
 * @param {string} foo This is a param with a description too long to fit in 
 *     one line. 
 * @return {number} This returns something that has a description too long to 
 *     fit in one line. 
 */ 
project.MyClass.prototype.method = function(foo) { 
  return 5; 
};
```
不要在 `@fileoverview` 标记中进行缩进。

虽然不建议，但也可对说明文字进行适当的排版对齐。不过，这样带来一些负面影响，就是当你每次修改变量名时，都得重新排版说明文字以保持和变量名对齐。
```javascript
/** 
 * This is NOT the preferred indentation method. 
 * @param {string} foo This is a param with a description too long to fit in 
 *                     one line. 
 * @return {number} This returns something that has a description too long to 
 *                  fit in one line. 
 */ 
project.MyClass.prototype.method = function(foo) { 
  return 5; 
};
```
### 枚举
```javasript
/** 
 * Enum for tri-state values. 
 * @enum {number} 
 */ 
project.TriState = { 
  TRUE: 1, 
  FALSE: -1, 
  MAYBE: 0 
};
```
注意一下，枚举也具有有效类型，所以可以当成参数类型来用。
```javascript
/** 
 * Sets project state. 
 * @param {project.TriState} state New project state. 
 */ 
project.setState = function(state) { 
  // ... 
};
```
### Typedefs

有时类型会很复杂。比如下面的函数，接收 `Element` 参数：
```javascript
/** 
 * @param {string} tagName 
 * @param {(string|Element|Text|Array.|Array.)} contents 
 * @return {Element} 
 */ 
goog.createElement = function(tagName, contents) { 
  ... 
};
```
你可以使用 `@typedef` 标记来定义个常用的类型表达式。
```javascript
/** @typedef {(string|Element|Text|Array.|Array.)} */ 
goog.ElementContent; 
 
/** 
* @param {string} tagName 
* @param {goog.ElementContent} contents 
* @return {Element} 
*/ 
goog.createElement = function(tagName, contents) { 
... 
};
```
### JSDoc 标记表
<table class="js-type">
  <caption>JSDoc 标记表</caption>
  <tr>
    <td style="width:10%;">标记</td>
    <td style="width:75%;">模板 & 例子</td>
    <td style="width:15%;">描述</td>
  </tr>
  <tr>
    <td>@param</td>
    <td>@param {Type} 变量名 描述<pre>	
/** 
 * Queries a Baz for items. 
 * @param {number} groupNum Subgroup id to query. 
 * @param {string|number|null} term An itemName, 
 *     or itemId, or null to search everything. 
 */ 
goog.Baz.prototype.query = function(groupNum, term) { 
  // ... 
};
</pre></td>
    <td>给方法，函数，构造器中的参数添加说明。</td>
  </tr>
  <tr>
    <td>@return</td>
    <td><strong>@return {Type} 描述</strong><pre>/** 
 * @return {string} The hex ID of the last item. 
 */ 
goog.Baz.prototype.getLastId = function() { 
  // ... 
  return id; 
};</pre></td>
    <td>给方法、函数的返回值添加说明。
在描述布尔型参数时，用"Whether the component is visible"这种描述优于"True if the component is visible, false otherwise"。
如果函数没有返回值，就不需要添加 @return 标记。</td>
  </tr>
<tr><td>@author</td>
<td>@author username@google.com (first last)
<pre>
/** 
 * @fileoverview Utilities for handling textareas. 
 * @author kuth@google.com (Uthur Pendragon) 
 */
 </pre>
</td>
<td>表明文件的作者，通常仅会在 @fileoverview 注释中使用到它</td>
</tr>

<tr>
<td>@see</td>	
<td>@see Link<pre>
/** 
 * Adds a single item, recklessly. 
 * @see #addSafely 
 * @see goog.Collect 
 * @see goog.RecklessAdder#add 
 ...</pre></td>
<td>给出引用链接，用于进一步查看函数/方法的相关细节。</td>
</tr>

<tr>
<td>@fileoverview</td>	
<td>@fileoverview 描述<pre>
/** 
 * @fileoverview Utilities for doing things that require this very long 
 * but not indented comment. 
 * @author kuth@google.com (Uthur Pendragon) 
 */</pre></td>
<td>文件通览</td>
</tr>

<tr>
<td>@constructor</td>	
<td>@constructor<pre>
/** 
 * A rectangle. 
 * @constructor 
 */ 
function GM_Rect() { 
  ... 
}</pre></td>
<td>指明类中的构造器</td>
</tr>

<tr>
<td>@interface</td>	
<td>@interface<pre>
/** 
 * A shape. 
 * @interface 
 */ 
function Shape() {}; 
Shape.prototype.draw = function() {}; 
 
/** 
 * A polygon. 
 * @interface 
 * @extends {Shape} 
 */ 
function Polygon() {}; 
Polygon.prototype.getSides = function() {};</pre></td>
<td>指明这个函数是一个接口</td>
</tr>

<tr>
<td>@type</td>	
<td>@type Type<pre>
@type {Type}

/** 
 * The message hex ID. 
 * @type {string} 
 */ 
var hexId = hexId;</pre></td>
<td>标识变量，属性或表达式的类型。大多数类型是不需要加大括号的，但为了保持一致，建议统一加大括号。</td>
</tr>

<tr>
<td>@extends</td>	
<td>@extends Type<pre>
@extends {Type}

/** 
 * Immutable empty node list. 
 * @constructor 
 * @extends goog.ds.BasicNodeList 
 */ 
goog.ds.EmptyNodeList = function() { 
  ... 
};</pre></td>
<td>与 @constructor 一起使用，用来表明该类是扩展自其它类的。类型外的大括号可写可不写。</td>
</tr>

<tr>
<td>@implements</td>
<td>@implements Type<pre>
@implements {Type}

/** 
 * A shape. 
 * @interface 
 */ 
function Shape() {}; 
Shape.prototype.draw = function() {}; 
 
/** 
 * @constructor 
 * @implements {Shape} 
 */ 
function Square() {}; 
Square.prototype.draw = function() { 
  ... 
};</pre></td>
<td>与 @constructor 一起使用，用来表明该类实现自一个接口。 类型外的大括号可写可不写。</td>
</tr>

<tr>
<td>@lends</td>	
<td>@lends objectName<pre>
@lends {objectName}

goog.object.extend( 
    Button.prototype, 
    /** @lends {Button.prototype} */ { 
      isButton: function() { return true; } 
    });</pre></td>
<td>表示把对象的键看成是其他对象的属性。该标记只能出现在对象语法中。
注意，括号中的名称和其他标记中的类型名称不一样，它是一个对象名，以"借过来"的属性名命名。如，@type {Foo} 表示 " Foo 的一个实例"，但是 @lends {Foo} 表示 "Foo 构造器"。</td>
</tr>

<tr>
<td>@private</td>	
<td>@private<pre>

/** 
 * Handlers that are listening to this logger. 
 * @type Array. 
 * @private 
 */ 
this.handlers_ = [];</pre></td>
<td>指明那些以下划线结尾的方法和属性是私有的。不推荐使用后缀下划线，而应改用 @private 。</td>

<tr>
<td>@protected</td>	
<td>@protected<pre>
/** 
 * Sets the component's root element to the given element.  Considered 
 * protected and final. 
 * @param {Element} element Root element for the component. 
 * @protected 
 */ 
goog.ui.Component.prototype.setElementInternal = function(element) { 
  // ... 
};</pre></td>
<td>指明接下来的方法和属性是被保护的。被保护的方法和属性的命名不需要以下划线结尾，和普通变量名没区别。</td>
</tr>

<tr>
<td>@this</td>	
<td>@this Type<pre>

@this {Type}

pinto.chat.RosterWidget.extern('getRosterElement', 
/** 
 * Returns the roster widget element. 
 * @this pinto.chat.RosterWidget 
 * @return {Element} 
 */ 
function() { 
  return this.getWrappedComponent_().getElement(); 
});</pre></td>
<td>指明调用这个方法时，需要在哪个上下文中。当 this 指向的不是原型方法的函数时必须使用这个标记。</td>
</tr>

<tr>
<td>@supported</td>
<td>@supported 描述<pre>
/** 
 * @fileoverview Event Manager 
 * Provides an abstracted interface to the 
 * browsers' event systems. 
 * @supported So far tested in IE6 and FF1.5 
 */</pre></td>
<td>在文件概述中用到，表明支持哪些浏览器。</td>
</tr>

<tr>
<td>@enum</td>	
<td>@enum {Type}<pre>
/** 
 * Enum for tri-state values. 
 * @enum {number} 
 */ 
project.TriState = { 
  TRUE: 1, 
  FALSE: -1, 
  MAYBE: 0 
};</pre></td>
<td>用于枚举类型</td>
</tr>

<tr>
<td>@deprecated</td>	
<td>@deprecated 描述<pre>
/** 
 * Determines whether a node is a field. 
 * @return {boolean} True if the contents of 
 *     the element are editable, but the element 
 *     itself is not. 
 * @deprecated Use isField(). 
 */ 
BN_EditUtil.isTopEditableField = function(node) { 
  // ... 
};</pre></td>
<td>告诉其他开发人员，此方法、函数已经过时，不要再使用。同时也会给出替代方法或函数。</td>
</tr>

<tr>
<td>@override</td>	
<td>@override<pre>
/** 
 * @return {string} Human-readable representation of project.SubClass. 
 * @override 
 */ 
project.SubClass.prototype.toString() { 
  // ... 
};</pre>
<td>指明子类的方法和属性是故意隐藏了父类的方法和属性。如果子类的方法和属性没有自己的文档，就会继承父类的</td>。
</tr>

<tr>
<td>@inheritDoc</td>	
<td>@inheritDoc<pre>
/** @inheritDoc */ 
project.SubClass.prototype.toString() { 
  // ... 
};</pre></rd>
<td>指明子类的方法和属性是故意隐藏了父类的方法和属性，它们具有相同的文档。
注意：使用 @inheritDoc 意味着也同时使用了 @override .</td>
</tr>

<tr>
<td>@code</td>	
<td>{@code ...}<pre>
/** 
 * Moves to the next position in the selection. 
 * Throws {@code goog.iter.StopIteration} when it 
 * passes the end of the range. 
 * @return {Node} The node at the next position. 
 */ 
goog.dom.RangeIterator.prototype.next = function() { 
  // ... 
};</pre></td>
<td>说明这是一段代码，让它能在生成的文档中正确的格式化。</td>
</tr>

<tr>
<td>@license or @preserve</td>	
<td>@license 描述<pre>

/** 
 * @preserve Copyright 2009 SomeThirdParty. 
 * Here is the full license text and copyright 
 * notice for this file. Note that the notice can span several 
 * lines and is only terminated by the closing star and slash: 
 */</pre></td>
<td>所有被标记为 @license 或 @preserve 的，会被编译器保留不做任何修改而直接输出到最终文挡中。这个标记让一些重要的信息(如法律许可或版权信息)原样保留，同样，文本中的换行也会被保留。</td>
</tr>

<tr>
<td>@noalias</td>
<td>@noalias<pre>
/** @noalias */ 
function Range() {}
在外部文件中使用，告诉编译器不要为这个变量或函数重命名。
@define	
@define {Type} 描述

/** @define {boolean} */ 
var TR_FLAGS_ENABLE_DEBUG = true; 
 
/** @define {boolean} */ 
goog.userAgent.ASSUME_IE = false;</pre></td>
<td>表示该变量可在编译时被编译器重新赋值。在上面例子中，BUILD 文件中指定了 --define='goog.userAgent.ASSUME_IE=true' 这个编译之后，常量 goog.userAgent.ASSUME_IE 将被全部直接替换为 true.</td>
</tr>

<tr>
<td>@export</td>	
<td>@export<pre>
/** @export */ 
foo.MyPublicClass.prototype.myPublicMethod = function() { 
  // ... 
};</pre></td>
<td>编译后，将源代码中的名字原样导出。</td>
</tr>

<tr>
<td>@const</td>	
<td>@const<pre>
/** @const */ var MY_BEER = 'stout'; 
 
/** 
 * My namespace's favorite kind of beer. 
 * @const 
 * @type {string} 
 */ 
mynamespace.MY_BEER = 'stout'; 
 
/** @const */ MyClass.MY_BEER = 'stout';</pre></td>
<td>声明变量为只读，直接写在一行上。如果其他代码中重写该变量值，编译器会警告。
常量应全部用大写字符，不过使用这个标记，可以帮你消除命名上依赖。>
</tr>

<tr>
<td>@nosideeffects</td>	
<td>@nosideeffects<pre>
/** @nosideeffects */ 
function noSideEffectsFn1() { 
  // ... 
}; 
 
/** @nosideeffects */ 
var noSideEffectsFn2 = function() { 
  // ... 
}; 
 
/** @nosideeffects */ 
a.prototype.noSideEffectsFn3 = function() { 
  // ... 
};</pre></td>
<td>用于对函数或构造器声明，说明调用此函数不会有副作用。编译器遇到此标记时，如果调用函数的返回值没有其他地方使用到，则会将这个函数整个删除。</td>
</tr>

<tr>
<td>@typedef</td>	
<td>@typedef<pre>
/** @typedef {(string|number)} */ 
goog.NumberLike; 
 
/** @param {goog.NumberLike} x A number or a string. */ 
goog.readNumber = function(x) { 
  ... 
}</pre></td>
<td>这个标记用于给一个复杂的类型取一个别名。</td>
</tr>

<tr>
<td>@externs</td>	
<td>@externs<pre>

/** 
 * @fileoverview This is an externs file. 
 * @externs 
 */ 
 
var document;</pre></td>
<td>指明一个外部文件</td>
</tr>

</table>

### JSDoc 中的 HTML

JSDoc 中的 HTML。

这就是说 JSDoc 不会完全依照纯文本中书写的格式。所以，不要在 JSDoc 中，使用空白字符来做格式化：
```javascript
/** 
 * Computes weight based on three factors: 
 *   items sent 
 *   items received 
 *   last timestamp 
 */
 ```
上面的注释，出来的结果是：

Computes weight based on three factors: items sent items received items received

应该这样写：
```javascript
/** 
 * Computes weight based on three factors: 
 * <ul> 
 * <li>items sent 
 * <li>items received 
 * <li>last timestamp 
 * </ul> 
 */
 ```
另外，也不要包含任何 HTML 或类 HTML 标签, 除非你就想让它们解析成 HTML 标签。
```javascript
/** 
 * Changes <b> tags to <span> tags. 
 */
```
Changes tags to tags.

另外，也应该在源代码文件中让其他人更可读，所以不要过于使用 HTML 标签。

上面的代码中，其他人就很难知道你想干嘛，直接改成下面的样子就清楚多了：
```javascript
/** 
* Changes 'b' tags to 'span' tags. 
*/
```
# 提示和技巧

## True 和 False 布尔表达式

下面的布尔表达式都返回 `false`：

+ null
+ undefined
+ '' 空字符串
+ 0 数字0
但小心下面的，可都返回 true：

+ '0' 字符串0
+ [] 空数组
+　{} 空对象
下面是一段比较糟糕的代码：

```javascript
while (x != null) {
  //code ...
}
```
你可以直接写成下面的形式(只要你希望 x 不是 0 和空字符串，和 false)：
```javascript
while (x) {
  //code ...
}
```
如果你想检查字符串是否为 null 或空，可能会写成这样：
```javascript
if (y != null && y != '') {
  //code ...
}
```
但这样写会更好：
```javascript
if (y) {
  //code ...
}
```
注意，还有很多地方需要注意，如：

    Boolean('0') == true
    '0' != true
    
    0 != null
    0 == []
    0 == false
    
    Boolean(null) == false
    null != true
    null != false
    
    Boolean(undefined) == false
    undefined != true
    undefined != false
    
    Boolean([]) == true
    [] != true
    [] == false
    
    Boolean({}) == true
    {} != true
    {} != false

## 条件(三元)操作符
下面的代码：
```javascript
if (val != 0) { 
  return foo(); 
} else { 
  return bar(); 
}
```
你可以写成：
```javascript
return val ? foo() : bar();
```
在生成 HTML 代码时，三元操作符也是很有用的：
```
var html = '<input type="checkbox"' + 
    (isChecked ? ' checked' : '') + 
    (isEnabled ? '' : ' disabled') + 
    ' name="foo">';
```
## && 和 ||
二元布尔操作符是可短路的，只有在必要时才会计算到最后一项。

"`||`" 被称作为 '`default`' 操作符，下面的代码：
```javascript
/** @param {*=} opt_win */ 
function foo(opt_win) { 
  var win; 
  if (opt_win) { 
    win = opt_win; 
  } else { 
    win = window; 
  } 
  // ... 
}
```
可以简化为：
```javascript
/** @param {*=} opt_win */ 
function foo(opt_win) { 
  var win = opt_win || window; 
  // ... 
}
```
"&&" 也可简短代码。比如：
```javascript
if (node) { 
  if (node.kids) { 
    if (node.kids[index]) { 
      foo(node.kids[index]); 
    } 
  } 
}
```
可以简化为：
```javascript
if (node && node.kids && node.kids[index]) { 
  foo(node.kids[index]); 
}
```
或者：
```javascript
var kid = node && node.kids && node.kids[index]; 
if (kid) { 
  foo(kid); 
}
```
不过这样就有点儿过头了：
```javascript
node && node.kids && node.kids[index] && foo(node.kids[index]);
```
## 使用 join() 来创建字符串
下面的代码在IE下非常慢：
```
function listHtml(items) { 
  var html = '
'; 
  for (var i = 0; i < items.length; ++i) { 
    if (i > 0) { 
      html += ', '; 
    } 
    html += itemHtml(items[i]); 
  } 
  html += '
'; 
  return html; 
}
```
可以像下面这样，使用join来创建字符串：
```javascript
function listHtml(items) { 
  var html = []; 
  for (var i = 0; i < items.length; ++i) { 
    html[i] = itemHtml(items[i]); 
  } 
  return '
' + html.join(', ') + '
'; 
}
```
你也可以是用数组作为字符串构造器，然后通过 `myArray.join('')` 转换成字符串。不过由于赋值操作快于数组的 `push()`，所以尽量使用赋值操作。

## 遍历 Node List
Node lists 是通过给节点迭代器加一个过滤器来实现的。这表示获取他的属性，如 `length` 的时间复杂度为 `O(n)`，通过 `length` 来遍历整个列表需要 `O(n^2)` 。
```javawsxript
var paragraphs = document.getElementsByTagName('p'); 

for (var i = 0; i < paragraphs.length; i++) { 
  doSomething(paragraphs[i]); 
}
```
这样做会更好：
```javascript
var paragraphs = document.getElementsByTagName('p');

for (var i = 0, paragraph; paragraph = paragraphs[i]; i++) { 
  doSomething(paragraph); 
}
```
这种方法对所有的 collections 和数组(只要数组不包含 falsy 值) 都适用。

在上面的例子中，也可以通过 `firstChild` 和 `nextSibling` 来遍历孩子节点。
```javascript
var parentNode = document.getElementById('foo'); 

for (var child = parentNode.firstChild; child; child = child.nextSibling) { 
  doSomething(child); 
}
```
# JavaScript 语言规范

JavaScript 是一种客户端脚本语言, Google 的许多开源工程中都有用到它。

这份指南列出了编写 JavaScript 时需要遵守的规则。

## 变量
声明变量必须加上 `var` 关键字。

当你没有写 `var`，变量就会暴露在全局上下文中，这样很可能会和现有变量冲突。

另外，如果没有加上 `var`，很难明确该变量的作用域是什么，变量也很可能像在局部作用域中，很轻易地泄漏到 Document 或者 Window 中。

所以，务必用 `var` 去声明变量。

## 常量
常量通常使用大写字符，并用下划线分割。如：`NAMES_LIKE_THIS`。

在注释里，你可以用 `@const` 标记来指明它是一个常量。但请永远不要在程序中使用 `const` 关键词。

对于基本类型的常量, 只需转换命名：
```javascript
/** 
 * The number of seconds in a minute. 
 * @type {number} 
 */

SECONDS_IN_A_MINUTE = 60;
```
对于非基本类型, 使用 `@const` 标记：
```javascript
/** 
 * The number of seconds in each of the given units. 
 * @type {Object.} 
 * @const 
 */

SECONDS_TABLE = { 
  minute: 60, 
  hour: 60 * 60, 
  day: 60 * 60 * 24 
}
```
`@const` 标记会告诉编译器它是常量。

至于关键词 `const`，因为 IE 不能识别, 所以不要使用。

## 分号
总是使用分号。

如果仅依靠语句间的隐式分隔, 有时会很麻烦。使用分号，会使你自己更能清楚哪里是语句的起止。

而且有些情况下, 漏掉分号会很危险：
```javascript
function MyClass(){};

MyClass.prototype.myMethod = function() { 
  return 42; 
}  // No semicolon here. 

(function() { 
  // Some initialization code wrapped in a function to create a scope for locals. 
})();

var x = { 
  'i': 1, 
  'j': 2 
}  // No semicolon here.

//上面这段代码会报错。
//原因是，上面的语句会被解释成：
//一个函数带一个匿名函数作为参数而被调用，返回42后，又一次被”调用“。
//这就导致了错误。
```
JavaScript 的语句以分号作为结束符，除非可以非常准确推断某结束位置才会省略分号。

上面的例子产出错误，是在语句中声明了函数/对象/数组直接量，但闭括号('}'或']')并不足以表示该语句的结束。

在 JavaScript 中，只有当语句后的下一个符号是后缀或括号运算符时，才会认为该语句的结束。

遗漏分号有时会出现很奇怪的结果，所以确保语句以分号结束。

*注意：在函数表达式的结尾应该添加分号，但在函数声明结尾不用添加分号，如：*
```javascript
var foo = function() {
  return true;
};  // semicolon here.

function foo() {
  return true;
}  // no semicolon here.
```
## 嵌套函数
嵌套函数很有用，比如：减少重复代码、隐藏帮助函数等。没什么其他需要注意的地方，随意使用。

## 块内函数声明
不要在块内声明一个函数。
```javascript
//不要写成
if (x) { 
  function foo() {} 
}
```
虽然很多 JS 引擎都支持块内声明函数，但它不属于 [ECMAScript][1] 规范。各个浏览器糟糕的实现相互不兼容。有些也与未来 [ECMAScript][2] 草案相违背。 [ECMAScript][3] 只允许在脚本的根语句或函数中声明函数。

如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量：
```javascript
if (x) { 
  var foo = function() {}; 
}
```
## 异常
可以使用异常。

你在写一个比较复杂的应用时，不可能完全避免不会发生任何异常。大胆去用吧。

## 自定义异常
可以自定义异常。

有时发生异常了，但返回的错误信息比较奇怪，也不易读。虽然可以将含错误信息的引用对象或者可能产生错误的完整对象传递过来，但这样做都不是很好，最好还是自定义异常类，其实这些基本上都是最原始的异常处理技巧。所以在适当的时候使用自定义异常。

## 标准特性
标准特性总是优于非标准特性。

最大化可移植性和兼容性，尽量使用标准方法而不是用非标准方法。

比如：优先用 `string.charAt(3)` 而不用 `string[3]`；通过 DOM 原生函数访问元素, 而不是使用应用封装好的快速接口。

## 封装基本类型
不要去封装基本类型。

没有任何理由去封装基本类型，另外还存在一些风险：
```javascript
//不要这样做
var x = new Boolean(false);
if (x) {
  alert('hi');  // Shows 'hi'.
}
```
```javascript
//除非明确用于类型转换，其他情况请千万不要这样做！
var x = Boolean(0);
if (x) {
  alert('hi');  // This will never be alerted.
}
typeof Boolean(0) == 'boolean';
typeof new Boolean(0) == 'object';
```
基本类型用于类型转换时，会非常实用。

## 方法、属性的定义
有很多方法可以给构造器添加方法成员，我们更倾向于使用如下的形式：
```
Foo.prototype.bar = function() {
  /* ... */
};
```
对于构造函数的其他属性，建议在构造函数中进行初始化：
```javascript
/** @constructor */
function Foo() {
  this.bar = value;
}
```
## delete
在Javascript引擎中，改变对象的属性数量，比指定对象属性的值要慢得多。因此，应该避免 delete 关键字的使用。除非有必要从一个对象的迭代列表中删除一个属性。
```javascript
//不建议
Foo.prototype.dispose = function() {
  delete this.property_;
};
```
```javascript
//建议
Foo.prototype.dispose = function() {
  this.property_ = null;
};
```
## 闭包
闭包也许是Javascript中最有用的特性了。有一份比较好的介绍闭包原理的 文档。

有一点需要牢记，闭包保留了一个指向它封闭作用域的指针，所以，在给 DOM 元素附加闭包时，很可能会产生循环引用，进一步导致内存泄漏。比如下面代码：
```javascript
function foo(element, a, b) {
  element.onclick = function() { /* uses a and b */ };
}
```
这里，即使没有使用 element，闭包也保留了 element， a和 b的引用。由于 element 也保留了对闭包的引用，这就产生了循环引用，就不能被回收。这种情况下，可将代码重构为：
```javascript
function foo(element, a, b) { 
  element.onclick = bar(a, b); 
}

function bar(a, b) { 
  return function() { /* uses a and b */ } 
}
```
## eval()
`eval()` 只用于解析序列化串 (如: 解析 RPC 响应)。

`eval()` 会让程序执行的比较混乱，当 `eval()` 里面包含用户输入的话就更加危险。

我们假设，从服务器返回的数据是这样的：

    {
      "name": "Alice",
      "id": 31502,
      "email": "looking_glass@example.com"
    }

当碰到一些需要解析序列化串的情况下, 使用 `eval()` 很容易实现：
```javascript
var userInfo = eval(feed);
var email = userInfo['email'];
```
但是，我们可以用其他更佳的、更清晰、更安全的方式写你的代码：
```javascript
var userInfo = JSON.parse(feed);
var email = userInfo['email'];
```
使用 `JSON.parse` 时，无效的JSON（包括所有可执行的JavaScript）会导致抛出一个异常。

对于不支持 `JSON.parse` 方法的浏览器，可引入 `json2.js` 来解决。

## with()
不要使用 `with` 。

使用 `with` 语句速度要比不使用 `with` 语句的等价代码的速度慢得多。
```javascript
var a = {
    a:{
        a:{
            a:{
                a:{
                    a:{
                        a:{
                            b:1
                        }
                    }
                }
            }
        }
    }
};

//取值与赋值 10000
function noWith(){
    var obj = a.a.a.a.a.a.a, i=100000, j = 0;
    for(; i; i--){
        j = obj.b;
        obj.b = i;
    }
}

//取值与赋值 10000
function yesWith(){
    var i=100000, j = 0;
    with( a.a.a.a.a.a.a ){
        for(; i; i--){
            j = b;
            b = i;
        }
    }
}


var t = new Date().getTime();
//noWith();
yesWith();

console.log(new Date().getTime() - t);

//运行上面两个函数, 对一个比较深的对象取值与赋值 100000 次

//不使用with: 0-3毫秒（chrome浏览器，可能是V8太NB，我自己都不信了），换了Firefox 大约是7-10毫秒
//使用with: 120-130毫秒之间(chrome)， 110-120毫秒(Firefox)

//结论：使用with进行大量运算确实存在一些性能问题，但是10W次的运算估计也很少遇到，大家自己权衡。
```
并且，它会让你的代码在语义上变得不清晰，因为 with 的对象, 可能会与局部变量产生冲突，从而改变你程序原本的用义。
```javascript
function useWith(){
    var obj = {
        item:{//姑且把这个对象叫做 this1
            key:1
        }
    };
    
    with( obj.item ){
    
        obj.item = {
            key : 2
        };
        
        console.log( key ); //1,  你悲剧的访问到了1
        //理由：with 已经确定了当前 this 指向了 this1, 
        //在访问 key 的时候不会重新读取 obj.item 新的指针。
    }
}

useWith();
```
大多数情况下， `with` 应用场景都可以用其他更好的方式代替。所以，我们建议，不要使用 `with` 。

## this
仅在对象构造器，方法，闭包中使用 `this` 。

`this` 的语义很特别。有时它引用一个全局对象(大多数情况下)，调用者的作用域(使用 `eval` 时)，DOM 树中的节点(添加事件处理函数时)，新创建的对象(使用一个构造器)，或者其他对象(如果函数被 `call()` 或 `apply()` )。

`this` 在使用时很容易出错，所以只在下面两种情况下，才使用它：

+ 在构造器中；
+ 对象的方法(包括创建的闭包)中。

## for-in 循环
`for-in` 循环只用于 `object` / `map` / `hash` 的遍历。

对 `Array` 用 `for-in` 循环有时会出错。因为，它不是从 `0` 到 `length-1` 进行遍历，而是所有出现在对象及其原型链的键值。下面就是一些失败的用例：
```javascript
function printArray(arr) {
  for (var key in arr) {
    console.log(arr[key]);
  }
}

printArray([0,1,2,3]);  // This works.

var a = new Array(10);
printArray(a);  // This is wrong.

a = document.getElementsByTagName('*');
printArray(a);  // This is wrong.

a = [0,1,2,3];
a.buhu = 'wine';
printArray(a);  // This is wrong again.

a = new Array;
a[3] = 3;
printArray(a);  // This is wrong again.
```
正确的遍历数组的方式：
```javascript
function printArray(arr) {
  var l = arr.length;
  for (var i = 0; i < l; i++) {
    console.log(arr[i]);
  }
}
```
## 关联数组
永远不要使用 `Array` 作为 `map` / `hash` / `associative` 数组

数组中不允许使用非整型作为索引值，所以也就不允许用关联数组。而取代它使用 Object 来表示 map / hash 对象

## 多行字符串
不要这样写长字符串：
```javascript
var myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error \
                message to make the Energizer bunny blush (right through \
                those Schwarzenegger shades)! Where was I? Oh yes, \
                you\'ve got an error and all the extraneous whitespace is \
                just gravy.  Have a nice day.';
```
在编译时，不能忽略行起始位置的空白字符。"`\`" 后的空白字符会产生奇怪的错误。虽然大多数脚本引擎支持这种写法，但它不是 ECMAScript 的标准规范。

可以使用 "`+`" 来连接长字符串，像下面这样：
```javascript
var myString = 'A rather long string of English text, an error message ' +
                'actually that just keeps going and going -- an error ' +
                'message to make the Energizer bunny blush (right through ' +
                'those Schwarzenegger shades)! Where was I? Oh yes, ' +
                'you\'ve got an error and all the extraneous whitespace is ' +
                'just gravy.  Have a nice day.';
```
## 使用Array 和 Object 直接量
使用 `Array` 和 `Object` 语法，而不使用 `Array` 和 `Object` 构造函数。

使用 `Array` 构造函数很容易因为传参不恰当导致错误
```javascript
// Length is 3.
var a1 = new Array(x1, x2, x3);

// Length is 2.
var a2 = new Array(x1, x2);

// If x1 is a number and it is a natural number the length will be x1.
// If x1 is a number but not a natural number this will throw an exception.
// Otherwise the array will have one element with x1 as its value.
var a3 = new Array(x1);

// Length is 0.
var a4 = new Array();
```
如果传入一个参数而不是2个参数，数组的长度很有可能就不是你期望的数值了。

为了避免这些歧义，我们应该使用更易读的直接量来声明：
```javascript
var a = [x1, x2, x3];
var a2 = [x1, x2];
var a3 = [x1];
var a4 = [];
```
虽然 `Object` 构造器没有上述类似的问题, 但鉴于可读性和一致性考虑, 最好还是在字面上更清晰地指明。
```javascript
//不建议
var o = new Object();
var o2 = new Object();
o2.a = 0;
o2.b = 1;
o2.c = 2;
o2['strange key'] = 3;
```
```
//建议
var o = {};
var o2 = {
  a: 0,
  b: 1,
  c: 2,
  'strange key': 3
};
```
## 不要修改内置对象的原型
千万不要修改内置对象，如 `Object.prototype` 和 `Array.prototype` 的原型。而修改内置对象，如 Function.prototype 的原型，虽然危险少些，但仍会导致调试时的诡异现象，所以也要避免修改其原型。

## 不要使用IE下的条件注释
不要使用IE下的条件注释。不要将代码写成这样：
```javascript
var f = function () {
    /*@cc_on if (@_jscript) { return 2* @*/  3; /*@ } @*/
};
```
条件注释妨碍自动化工具的执行，因为在运行时，它们会改变 JavaScript 语法树。


  [1]: http://www.ecma-international.org/publications/standards/Ecma-262.htm
  [2]: http://www.ecma-international.org/publications/standards/Ecma-262.htm
  [3]: http://www.ecma-international.org/publications/standards/Ecma-262.htm