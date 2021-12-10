# CSS基础学习

> CSS（Cascading Style Sheets）层递样式表
>
> 参考：[学习CSS](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/First_steps)



[TOC]

​	CSS（层叠样式表）用于设置和布置网页 - 例如，更改内容的字体，颜色，大小和间距，将其拆分为多个列，或添加动画和其他装饰功能。



## CSS基本语法

### 为HTML链接CSS

让 HTML 文档能够遵守我们给它的 CSS 规则， 最普遍且有用的方式——在文档的开头链接 CSS。

在与之前所说的 HTML 文档的相同目录创建一个文件，保存并命名为 `styles.css` 。（看后缀知道此文件就是 CSS 文件）

为了把 `styles.css` 和 `index.html` 连接起来，可以在 HTML 文档中，`<head>`语句模块里面加上下面的代码：

```html
<link rel="stylesheet" href="styles.css">
```

### 使用类名

给HTML元素添加类名，如`<li class="special">`，在CSS中，要对这个类进行设计，代码格式如下：

```css
.special {
  color: orange;
  font-weight: bold;
}
```

### 根据元素在文档中的位置确定样式

```css
li em {
  color: rebeccapurple;
}
```

如上代码，表示选择器将选择`<li>`内部的任何`<em>`元素（`<li>`的后代）

如果在两个选择器间用一个**相邻选择符**即`+`，可以使得两个选择器有同一个样式，示例代码如下

```css
h1 + p {
  font-size: 200%;
}
/*上数代码表示，h1和p对应的格式字体大小均调整为200%*/
```

### 根据状态确定样式

应用例子：

​	当我们修改一个链接的样式时我们需要定位（针对） `<a>` （锚）标签。取决于是否是未访问的、访问过的、被鼠标悬停的、被键盘定位的，亦或是正在被点击当中的状态，这个标签有着不同的状态。

​	可以使用CSS去定位或者说针对这些不同的状态进行修饰——下面的CSS代码使得没有被访问的链接颜色变为粉色、访问过的链接变为绿色，鼠标悬停时下划线消失。

```css
a:link {
  color: pink;
}

a:visited {
  color: green;
}
a:hover{
    text-decoration: none;    
}
/*在 CSS 定义中，:hover 必须位于 :link 和 :visited 之后（如果存在的话），这样样式才能生效。*/
```



### 内部样式表

​	有时，使用的内容管理系统不能编辑CSS文件，就可以使用该方法来设计样式。在`<head>标签中借助<style>来实现`。但是，这种设计样式的方法并不高效，不同页面要用同样样式的话，需要反复设置。

 

### 专一性

有时，对于同一个选择器定义了两种规则，那么，**稍后的样式**将会替代后头的样式，如下例子

```css
p {
  color: red;
}

p {
  color: blue;
}
```

在上述例子中，如果我们有一段文字，那么他的颜色是`blue`

之前也提过，可以给元素加**类名**（如`special`），可以通过类名来定义规则，如下：

```css
.special {
  color: red;
}

p {
  color: blue;
}
```

在这种情况下，文字的颜色为`red`，类的优先级更高。**一个类被描述为比元素选择器更具体，或者具有更多的特异性，所以它获胜了**



### 函数

在教程的示例中，用`calc`函数进行了简单的计算，借助`<div>`标签实现了简单的进度条（伪）

```html
    <!-- div是一个块级元素 -->
    <div class="outer"><div class="box">The inner box is 90% - 30px.</div></div>
    <p>可以理解为下述两部分嵌套而成</p>
    <div class="outer">The inner box is 90% - 30px.</div>
    <div class="box">The inner box is 90% - 30px.</div>
```

```CSS
/* 接下来的部分控制进度条 */
.outer {
    border: 5px solid black;
    /* width: 100%; */
  }
  
.box {
    padding: 5px;
    /* 内边距 */
    width: calc(90% - 30px);
    /* 框的宽度为包含块宽度的90%，减去30像素 */
    /* 但是发现设置为100时，将超出框的大小，那么框的宽度如果不加100%的设置的话，为什么默认时不满呢 */
    background-color: rebeccapurple;
    /* 背景颜色为紫色，字体为白色 */
    color: white;
}
```

这里有一个**疑问**，在`outer`类中，如果不设置宽度，将默认为一个并不满的宽度，这是什么原因？



### @规则

如果需要将额外的样式表导入主样式表，可以使用`@import`进行导入：

```css
@import "styles2.css";

```

最常见的应用是`@media`，允许使用**媒体查询**来应用CSS，今当某些条件成立

> **媒体查询**可以根据各种设备特征和参数的存在或价值来调整网站或应用程序。
>
> 在CSS中，根据媒体查询的结果有条件的应用样式表的一部分。

应用示例为：

```css
  /* 这里练习@rules常见的应用：@media */
  body {
    background-color: pink;
  }
  /* 当宽度大于30em的时候为绿色，否则为粉色 */
  @media (min-width: 30em) {
    body {
      background-color:cadetblue;
    }
  }
```

关于上文中提到的一个单位`em`：

> 参考链接：[CSS中的em应用详解](https://blog.csdn.net/jingru2017/article/details/79099464)
>
> 文章中讲的非常详细，简单了解到em大概是这样一个东西：
>
> ​	弹性设计有一个关键地方，Web页面中所有元素都使用“em”单位值。“em”是一个相对的大小，我们可以这样来设置1em，0.5em，1.5em等，而且“em”还可以指定到小数点后三位，比如“1.365em”。
>
> ​	而其中“相对”的意思是：相对于元素父元素的font-size。
>
> ​	比如说：如果在一个<div>设置字体大小为“16px”，此时这个<div>的后代元素教程了是将继承他的字体大小，除非重新在其后代元素中进行过显示的设置。此时，如果你将其子元素的字体大小设置为“0.75em”，那么其字体大小计算出来后就相当于“0.75 X 16px = 12px”



## CSS如何运行

基本步骤为：

1. 浏览器载入HTML文件
2. 将HTML文件转化成一个DOM（Document Object Model）
3. 接下来，浏览器会拉取该HTML相关的大部分资源，比如嵌入到页面的图片、视频和CSS样式。JavaScript则会稍后进行处理
4. 浏览器拉取到CSS之后会进行解析，根据选择器的不同类型（比如element、class、id等等）把他们分到不同的“桶”中。浏览器基于它找到的不同的选择器，将不同的规则（基于选择器的规则，如元素选择器、类选择器、id选择器等）应用在对应的DOM的节点中，并添加节点依赖的样式（这个中间步骤称为渲染树）。
5. 上述的规则应用于渲染树之后，渲染树会依照应该出现的结构进行布局。
6. 网页展示在屏幕上（这一步被称为着色）。



示意图：

![image-20211009211048473](README.assets/image-20211009211048473.png)

- 当浏览器遇到无法解析的CSS代码时，并不会报错，因此，有时候可以利用这个特性，为同一个元素制定多个CSS样式来解决有的浏览器不兼容新特性的情况。

  举例：

  ```css
  .box {
    width: 500px;
    width: calc(100% - 50px);
  }
  
  /*
  在这部分示例代码中，设置了两个width，
  因为部分老的浏览器并不支持calculate的缩写，因此第二行的设置并没有用，老浏览器便会忽略这行；
  新浏览器将会把这一行解析成像素值，并覆盖第一行
  */
  
  ```







# CSS构建基础

## 层叠与继承

- CSS规则的顺序：当应用两条同级别的的规则到同一元素的时候，写在后面的元素是实际应用到的规则。
- 规则越具体，优先级越高，例如为某元素定义了类名，那么真对类名的规则的优先级将高于针对这个元素的规则的优先级
- widths , margins, padding, 和 borders 不会被继承，哪些属性属于默认继承很大程度上是由常识决定的。

### 控制继承

CSS 为控制继承提供了四个特殊的通用属性值。每个css属性都接收这些值

- `inherit`  设置该属性会使子元素属性和父元素相同。实际上，就是 "开启继承"
- `initial`设置属性值和浏览器默认样式相同。如果浏览器默认样式中未设置且该属性是自然继承的，那么会设置为 `inherit` 。
- `unset`如果CSS关键字 **`unset`** 从其父级继承，则将该属性重新设置为继承的值，如果没有继承父级样式，则将该属性重新设置为初始值。换句话说，在第一种情况下（继承属性）它的行为类似于`inherit`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/inherit) ，在第二种情况下（非继承属性）类似于[`initial`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/initial)。它可以应用于任何CSS属性，包括CSS简写属性 [`all`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/all) 。
- `revert`很少的浏览器支持



### 层叠

层叠定义在不止一个CSS元素时，如何应用规则：

1. 重要程度
2. 优先级
3. 资源顺序

接下来倒着说明（从最不重要的说起）

- 资源顺序：在前两项都对等的情况下，应用靠后的一个规则

- 优先级：

  - 有更高优先级的规则，**范围越小**

  - 优先级的计算规则：

    ![image-20211012160416946](README.assets/image-20211012160416946.png)

    - 警告中表示的意思是，无论有多少个低优先级的存在，都不可能撼动高优先级的优先级

  - `!important`：一个特殊的 CSS ，可以用来覆盖所有上面所有优先级计算，不过需要很小心的使用 — `!important`。用于修改特定属性的值， 能够覆盖普通规则的层叠。

    - 覆盖 `!important` 唯一的办法就是另一个 `!important` 具有 相同*优先级* 而且顺序靠后，或者更高优先级。
    - `!important` 是为了在阅读别人代码的时候知道有什么作用。 **但是，强烈建议除了非常情况不要使用它。** `!important` 改变了层叠的常规工作方式，它会使调试 CSS 问题非常困难，特别是在大型样式表中

## 选择器

- 类型选择器  `h1{   }`

- 类选择器  `.special{  }`

- ID选择器  `#theID{   }`

- 标签属性选择器   `a[title] { }`

- 全局选择器  `* {  }`

  它选中了文档中的所有内容（或者是父元素中的所有内容，比如，它紧随在其他元素以及邻代运算符之后的时候）

- 子字符串匹配选择器

```css
/*举例*/
li[class^="a"]    /*匹配了任何值开头为a的属性*/ 
li[class$="a"]    /*匹配了任何值结尾为a的属性*/ 
li[class*="a"]    /*匹配了任何值的字符串中出现了a的属性*/ 
/*大小写不敏感，如果在上述中括号中添加字符 i 则，大小写不敏感，使用示例如下*/
li[class^="a"] 
li[class^="a" i] 
/*如果有一系列类名，分别以A和a开头，则只有第二种情况才能全部匹配*/
```

- 关系选择器

  - 后代选择器，例：`.box p`选中作为`.box`后代的p元素

  - 子代关系选择器，使用`>`表示，选择直接子代，同“后代”区分（见代码）

  - 邻接选择器：邻接兄弟选择器（`+`）用来选中恰好处于另一个在继承关系上同级的元素旁边的物件。例如，选中所有紧随`<p>`元素之后的`<img>`元素：

    ```css
    p + img	
    ```

    

- 通用兄弟元素

  ​	选中一个元素的兄弟元素，即使它们不直接相邻，还是可以使用通用兄弟关系选择器（`~`）。

  ​	例如：要选中所有的`<p>`元素后*任何地方*的`<img>`元素可以：

  ```css
  p ~ img
  ```

- 关系选择器的组合

  例如：

  ```css
  /*想要选择为<ul>的直接子元素的带有“a”类(大小写不敏感)的列表项的话*/
  ul > li[class="a" i] {
  }
  
  ```

  



## 伪类和伪类元素

> 伪类是选择器的一种，它用于选择处于**特定状态**的元素，比如当它们是这一类型的第一个元素时，或者是当鼠标指针悬浮在元素上面的时候。它们表现得会像是你向你的文档的某个部分应用了一个类一样，帮你在你的标记文本中减少多余的类，让你的代码更灵活、更易于维护

这组选择器包含了伪类，用来样式化一个元素的**特定状态（使用单冒号）**。例如`:hover`伪类会在鼠标指针悬浮到一个元素上的时候选择这个元素：

```css
a:hover { }
```

它还可以包含了**伪元素（开头为双冒号）**，选择一个元素的某个部分而不是元素自己。例如，`::first-line`是会选择一个元素（下面的情况中是`<p>`）中的第一行，类似`<span>`包在了第一个被格式化的行外面，然后选择这个`<span>`。

```css
p::first-line { }
```

**通过模块“使用全局选择器让选择器更易读”引申的深入理解**

关于伪类元素，最开始理解有错误，看到全局选择器的某个例子，才意识到了问题所在。（比如上两行中的这个`::first-line`，忽视了为什么要用两个冒号）

通过本部分的解读，也能理解，为什么伪类叫伪类

那么，先看一下最开始出现疑问的地方

> **使用全局选择器让选择器更易读**
>
> 全局选择器的一种用法是让选择器更易读，更明显地表明它们的作用。例如，如果我想选中任何`<article>`元素的第一子元素，不论它是什么元素，都给它加粗，我可以将[`:first-child`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:first-child)选择器（我们将会在[伪类和伪元素](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)课中进一步了解）用作`<article>`元素选择器的一个兄弟选择器：
>
> ```
> article :first-child {
> 
> }
> ```
>
> Copy to Clipboard
>
> 但是这会和`article:first-child`混淆，**而后者选择了作为其他元素的第一子元素的`<article>`元素。**
>
> （单个冒号表示的是元素的状态，而非选择，例如前文提到的悬停`:hover`）
>
> 为了避免这种混淆，我们可以向`:first-child`选择器加入全局选择器，这样选择器所做的事情很容易就能看懂。选择器正选中`<article>`元素的*任何*第一子元素：
>
> ```css
> article *:first-child {
> 
> } 
> /* 上文中的星号，替代的是最初形态下的空格，表示任意，此处指代的就是article中的星号元素，同时，这个元素要作为其他元素的第一子元素 */
> ```

（写着写着没疑问了.......）

参考文档链接如下：[伪类和伪类元素](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)

如果你想让第一段的第一行加粗，你需要把`:first-child`和`::first-line`选择器放到一起。试着编辑前面的实时示例，让它使用下面的CSS。这里的意思是，**我们想选择一个`<article>`元素里面的第一个`<p>`元素的第一行**。

**但是！！！**

上文中加粗的这行还是有一些问题的，选择的应该是**`<article>`元素里面的，作为第一子元素的`<p>`元素的第一行**

（如果这个p元素不是第一子元素，将不会被加粗，示例的HTML代码如下）

```css
article p:first-child::first-line {
  font-size: 120%;
  font-weight: bold;
}
```

```HTML
    <p>这里测试一下伪类的一个例子</p>
    <article>
        <!-- <span1>如果这个不被注释掉，接下来的一行将不会被加粗</span1> -->
        <p>这行会不会被加粗呢<br>
            这里加个第二行</p>

    </article>

```

### 生成带有`::before`和`::after` 的内容

**`::before`和`::after`伪元素与`content`属性的共同使用，在CSS中被叫做“生成内容”**

可以使用这种方法将内容插入文档中，举例如下

```css
.box::before {
    content: "This should show before the other content."
}   
    
```

```html
<p class="box">Content in the box in my HTML page.</p>
    
```

通过这种方法插入的文字，对于某些浏览器来说，是不可见的。因此，最常见的用法是插入不愿意被见到的一些图标/空字符串等。

一个示例如下：

```css
.box::before {
    content: "";
    display: block;
    width: 100px;
    height: 100px;
    background-color: rebeccapurple;
    border: 1px solid black;
}   
/*这里将字符串通过  display：block 改变了形态*/
```

注意，通过这种这种方式生成的内容，将会相互覆盖，例如：

```css
.box11::before {
    content: "";
    display: block;
    width: 100px;
    height: 100px;
    background-color: rebeccapurple;
    border: 1px solid black;
}   

.box11::before {
    content: "这是被插入之前的句子。"
}

/*先插入图形，再添加文字*/
```

展示情况如下：

![image-20211208222701757](README.assets/image-20211208222701757.png)

但是，如果调转顺序，会发现文字被覆盖了

![image-20211208222750186](README.assets/image-20211208222750186.png)

后续测试，如果先后两块代码块中的`contant`内容对应的都是文字，将会互相覆盖。

猜想（需要后续学习证实）：将方块放在前面，会显示后续的文字，是因为方块对应的代码中，设置的contant值为空。第二次补上的文字部分，是替代了上半部代码的空白部分。因此，此处的逻辑还可用CSS的专一性来解释。即同等优先级，后设置的将覆盖前设置的。





### 运算符（暂缺不懂，待补充）

一组选择器可以将其他选择器组合起来，更复杂的选择元素。下面的示例用运算符（`>`）选择了`<article>`元素的初代子元素。

```css
article > p { }
```



### 对同一个元素应用多个类

通过下述例子来解释

```html
<div class="notebox">
    This is an informational note.
</div>

<div class="notebox warning">
    This note shows a warning.
</div>

<div class="notebox danger">
    This note shows danger!
</div>

<div class="danger">
    This won't get styled — it also needs to have the notebox class
</div>
    
```

```css
.notebox {
  border: 4px solid #666;
  padding: .5em;
}

.notebox.warning {
  font-weight: bold 
}

.notebox.danger {
  border-color: red;
  font-weight: bold;
}
```

这部分内容最开始有点问题的原因是，忽视了类的命名不能存在空格，存在空格的，表示是两个类。

这就是本模块的标题“同一个元素应用多个类”的由来

可以用形如`.notebox.danger`的多个选择器连续放置，来定义多个类。



# 盒模型

### 块级盒子和内联盒子

在 CSS 中广泛地使用两种“盒子” —— **块级盒子** (**block box**) 和 **内联盒子** (**inline box**)**。**这两种盒子会在**页面流**（page flow）和**元素之间的关系**方面表现出不同的行为:

一个被定义成**块级的（block）盒子**会表现出以下行为:

- 盒子会在内联的方向上扩展并占据父容器在该方向上的所有可用空间，在绝大数情况下意味着盒子会和父容器一样宽
- 每个盒子都会换行
- [`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 属性可以发挥作用
- 内边距（padding）, 外边距（margin） 和 边框（border） 会将其他元素从当前盒子周围“推开”

除非特殊指定，诸如标题(`<h1>`等)和段落(`<p>`)默认情况下都是块级的盒子。

如果一个盒子对外显示为 **内联盒子`inline`**，那么他的行为如下:

- 盒子不会产生换行。
-  [`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 属性将不起作用。
- 垂直方向的内边距、外边距以及边框会被应用但是不会把其他处于 `inline` 状态的盒子推开。
- 水平方向的内边距、外边距以及边框会被应用且会把其他处于 `inline` 状态的盒子推开。

用做链接的 `<a>` 元素、 `<span>`、 `<em>` 以及 `<strong>` 都是默认处于 `inline` 状态的。

我们通过对盒子[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 属性的设置，比如 `inline` 或者 `block` ，来控制盒子的外部显示类型。

### 弹性盒子`flex`

弹性盒子是一种用于按行或按列布局元素的一维布局方法 。元素可以膨胀以填充额外的空间, 收缩以适应更小的空间。

如果设置 `display: flex`，在一个元素上，外部显示类型是 `block`，但是内部显示类型修改为 `flex`。 该盒子的所有直接子元素都会成为flex元素，会根据 [弹性盒子（Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox) [）](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)规则进行布局，

使用本模型，需要确定选择将哪些元素将设置为柔性的盒子，然后给这些 flexible 元素的**父元素** [`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 设置一个特定值

> 本部分内容主要借助例子`SampleFlexbox`
>
> 查看代码及注释

- 设置了`display = flex`的父元素，被称为`flex容器`
- 在`flex容器`中表现为`flexbox`的元素为flex项

