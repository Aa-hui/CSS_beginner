# CSS基础学习

> CSS（Cascading Style Sheets）层递样式表
>
> 参考：[学习CSS](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/First_steps)



​	CSS（层叠样式表）用于设置和布置网页 - 例如，更改内容的字体，颜色，大小和间距，将其拆分为多个列，或添加动画和其他装饰功能。

#### 为HTML链接CSS

让 HTML 文档能够遵守我们给它的 CSS 规则， 最普遍且有用的方式——在文档的开头链接 CSS。

在与之前所说的 HTML 文档的相同目录创建一个文件，保存并命名为 `styles.css` 。（看后缀知道此文件就是 CSS 文件）

为了把 `styles.css` 和 `index.html` 连接起来，可以在 HTML 文档中，`<head>`语句模块里面加上下面的代码：

```html
<link rel="stylesheet" href="styles.css">
```

#### 使用类名

给HTML元素添加类名，如`<li class="special">`，在CSS中，要对这个类进行设计，代码格式如下：

```css
.special {
  color: orange;
  font-weight: bold;
}
```

#### 根据元素在文档中的位置确定样式

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

#### 根据状态确定样式

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



#### 内部样式表

​	有时，使用的内容管理系统不能编辑CSS文件，就可以使用该方法来设计样式。在`<head>标签中借助<style>来实现`。但是，这种设计样式的方法并不高效，不同页面要用同样样式的话，需要反复设置。

#### 

#### 专一性

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



#### 函数

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
    width: calc(90% - 0px);
    /* 框的宽度为包含块宽度的90%，减去30像素 */
    /* 但是发现设置为100时，将超出框的大小，那么框的宽度如果不加100%的设置的话，为什么默认时不满呢 */
    background-color: rebeccapurple;
    /* 背景颜色为紫色，字体为白色 */
    color: white;
}
```

这里有一个**疑问**，在`outer`类中，如果不设置宽度，将默认为一个并不满的宽度，这是什么原因？

