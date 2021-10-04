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



