# 1. HTML

## 1.1 网页/HTML

网页是由网页元素组成，通常是HTML格式的文件，通过浏览器来阅读。HTML文件常见以.htm或.html后缀结尾。

HTML指的是超文本标记语言，是用来描述网页的一种语言。

## 1.2 web标准

web标准是由W3C组织和其他标准化组织制定的一系列标准的集合。

web构成：结构、表现和行为。

结构写到HTML文件中，表现写到css文件中，行为写到JavaScript文件中。

##1.3 HTML结构标签：

```html
<!DOCTYPE html>  <!-- <!DOCTYPE>声明标签，页面采取html5版 -->
<html lang="en">   
    <!-- <html> 元素是 HTML 页面的根元素 -->
    <!-- en-英文网站 、ZH-CN-中文网站 -->
<head>
  <!-- <head>头部标签 -->
  <meta charset="UTF-8">
  <!-- <meta charset="utf-8"> 字符编码，定义网页编码格式为 utf-8（万国码）。 -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- <meta> 元素来描述HTML文档的描述，关键词，作者，字符集等。 -->
  <title>Document</title>
  <!-- <title> 标签定义HTML文档的标题 -->
</head>
<body>
  <!-- <body> 元素包含了可见的页面内容 -->
</body>
</html>
```

（以上注释内容参考菜鸟教程）

其中\<!DOCTYPE \>

\<!DOCTYPE\> 声明不是一个 HTML 标签；它是用来告知 Web 浏览器页面使用了哪种 HTML 版本。

IE、Firefox、Google Chrome、Safari、Opera所有主流浏览器都支持 \<!DOCTYPE\> 声明

注释：\<!DOCTYPE\> 标签没有结束标签。

提示：\<!DOCTYPE\> 声明不区分大小写。

注释以`<!--`开头，以`-->`结束。

## 1.4 HTML常用标签

（1）**标题标签**

 `<h1> ~<h6>`  HTML提供了6个等级的网页标签。  

标语义：作为标题使用，并且依据重要性递减。

特点：加了标题的文字会加粗，字号也依次变大； 一个标签独占一行。

**（2）段落和换行标签**

`<p></p>`  

标签语义：可以把HTML文档分割为若干段落。

特点：文本在一个段落中会根据浏览器窗口的大小自动换行； 段落和段落之间保有空隙。

 `<br />`

变迁语义：强行换行。

特点：单标签；换行标签知识简单的开始新的一行，跟段落不一样，段落之间会有空隙。

**（3）文本格式化标签**

| 语义   | 标签                             | 说明                                        |
| ------ | -------------------------------- | ------------------------------------------- |
| 加粗   | `<strong></strong>`或者`<b></b>` | 推荐使用`<strong></strong>`标签，语义更强烈 |
| 倾斜   | `<em></em>`或者`<i></i>`         | 推荐使用`<em></em>`标签，语义更强烈         |
| 删除线 | `<del></del>`或者`<s></s>`       | 推荐使用`<del></del>`标签，语义更强烈       |
| 下划线 | `<ins></ins>`或者`<u></u>`       | 推荐使用`<ins></ins>`标签，语义更强烈       |

**（4）`<div>`和`<span>`标签**

特点：`<div>`标签用来布局，但是一行只能放一个`<div>`，大盒子; 

 `<span>`标签用来布局，一行可以放多个 `<span>`，小盒子。

**（5）图像标签**

`<img scr="图像URL" />`  

scr是标签的必须属性，用来指定图像文件的路径和文件名。

**（6）超链接标签**

`<a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>`

**（7）表格标签**

```html
<table>		
    <tr>	
        <td>单元格内的文字</td>
        ...
    </tr>
    ...
</table>
```

`<table></<table>`用于定义表格的标签

`<tr></tr>`用于定义表格中的行

`<td></td>`用于定义表格中的单元格

- 表头标签：

   `<th></th>`：表头标签也是单元格，里面的文字会加粗居中显示

- 表格结构标签：

  `<thead></thead>`：用于定义表格的头部

  `<tbody></tbody>`：用于定义表格的主体

**（8）列表标签**

- 无序标签 `<ul>`

```html
<ul>
    <li>列表项1</li>
    <li>列表项2</li>
    <li>列表项3</li>
    ...
</ul>
```

`<ul></ul>`中只能嵌套`<li></li>`；`<li>`与`</li>`之间相当于一个容器，可以容纳所有元素。

- 有序标签 `<ol>`

```html
<ol>
    <li>列表项1</li>
    <li>列表项2</li>
    <li>列表项3</li>
    ...
</ol>
```

`<ol></ol>`中只能嵌套`<li></li>`；`<li>`与`</li>`之间相当于一个容器，可以容纳所有元素。

- 自定义列表 `<dl>`

```html
<dl>
    <dt>名词1</dt>
    <dd>名词1解释1</dd>
    <dd>名词1解释2</dd>
    ...
</ol>
```

`<dl></dl>`中只能包含`<dt><dd>`；`<dt>`和`<dd>`个数没有限制，经常是一个`<dt>`对应多个`<dd>`。

**（9）表单标签**

表单的组成：一个完整的表单通常由表单域、表单控件（表单元素）和提示信息3个部分构成。

- 表单域`<form>`

  `<form action="url地址" method="提交方式" name="表单域名称">各种表单元素控件</form>`

- 表单控件

  - `<input type="属性值" />`  //用于收集用户信息

  - `<label for="id属性" />`  //用于绑定一个表单元素
  - `<textarea>`如下：  //用于定义多行文本输入的控件

  ```html
  <textarea rows="3" cols="20">
      文本内容
  </textarea>
  ```

  - `<select>`如下：  //定义下拉列表

  ```html
  <select>
      <option>选项1</option>
      <option>选项2</option>
      <option>选项3</option>
      ...
  </select>
  ```

## 1.4 HTML特殊字符

主要列举以下几个：

| HTML源代码 | 显示结果 | 描述                   |
| :--------: | -------- | ---------------------- |
|   &nbsp;   | `&nbsp;` | 不断行的空格           |
|   &reg;    | `&reg;`  | 已注册                 |
|    &gt;    | `&gt;`   | 大于号                 |
|    &lt;    | `&lt;`   | 小于号                 |
|   &amp;    | `&`      | 可用于显示其它特殊字符 |

其余可参考链接：[链接](<https://www.w3school.com.cn/tags/html_ref_entities.html>)

# 2.CSS

## 2.1 css属性

### （1）字体属性

font（字体）属性用于定义字体系列、大小、粗细和文字样式（如斜体）。

<font color='orange'>**a.字体系列：**</font>

css使用`font-family`属性定义文本的字体系列。

<font color='orange'>**b.字体大小：**</font>

css使用`font-size`字体系列。

<font color='orange'>**c.字体粗细：**</font>

css使用`font-weight`字体系列。

<font color='orange'>**d.文字样式：**</font>

css使用`font-style`属性设置文本的风格。

<font color='orange'>**e.字体复合属性：**</font>

`font: font-style font-weight font-size/line-height font-family;`

- 使用font属性时，必须按照上面语法顺序书写，不能更换顺序，并且各个属性间以空格隔开；
- 不需要设置的属性可以省略（取默认值），但必须保留font-size和font-family属性，否则font属性将不起作用。

### （2）文本属性

text（文本）属性用于定义文本的外观，比如文本的颜色、对齐文本、装饰文本、文本缩进、行间距等。

<font color='orange'>**a.文本颜色：**</font>

color属性定义文本的字体系列。

<font color='orange'>**b.对齐文本：**</font>

`text-align`属性用于设置元素内文本内容的水平对齐方式。

<font color='orange'>**c.装饰文本：**</font>

`text-decoration`属性规定添加到文本的装饰，可以给文本添加下划线、删除线、上划线。

<font color='orange'>**d.文本缩进：**</font>

`text-index`属性用来指定文本的第一行的缩进，通常是将段落的首行缩进。

<font color='orange'>**e.行间距：**</font>

`line-height`属性用于设置行间的距离（行高），可以控制文字行与行之间的距离。

### （3）css的引入方式

- 行内样式表（行内式）
- 内部样式表（嵌入式）
- 外部样式表（链接式）

---

- 选择器  {属性: 值;    属性: 值;}

- css选择器分为基础选择器和复合选择器两个大类。

## 2.2 css的基础选择器

基础选择器由单个选择器组成，基础选择器包括：标签选择器、类选择器、id选择器和通配符选择器。

### （1）标签选择器

标签选择器（元选择器）是指用HTML标签名称作为选择器，为页面中某一类标签指定统一的css样式。

语法：

标签名 {

​		属性1: 属性值1；

​		属性1: 属性值1；

​		属性1: 属性值1；

​		...

}

### （2）类选择器

类选择器可以选出1个或者多个标签。

类选择器在HTML中以class属性表示，在css中，类选择器以一个点“.”号显示。

语法：

`<div class="类名"></div>`     //需要class属性来调用class类。

.类名 {

​		属性1: 属性值1；

​		...

}

- 多类名使用方法：

在标签class属性中写多个类名，多个类名中间必须用空格分开。

### （3）id选择器

id选择器可以为标有特定的id的HTML元素指定特定的样式。

id选择器在HTML中以id属性表示，在css中，id选择器以一个点“#”号显示。

语法：

`<div id="id名"></div>`     //需要class属性来调用class类。

`#`id名 {

​		属性1: 属性值1；

​		...

}

<u>注意：id属性只能在每个HTML文档中出现一次</u>

### （4）通配符选择器

在css中，通配选择器使用"*"定义，它表示选取页面中所以元素（标签）。

语法：

`*` {

​		属性1: 属性值1；

​		...

}

- 通配符选择器不需要调用，自动就给所有元素使用样式

- 以下是清除内外边距

  ```css
  * {
      margin: 0;
      padding: 0;
  }
  ```

  

## 2.3 css的复合选择器

### （1）后代选择器

用来选择后代元素，（可以是子孙后代）；符号是空格 `.nav a`  `.nav .footer`

### （2）子代选择器

选择最近一级元素（只选亲儿子），符号是大于.nav\>p

### （3）并集选择器

通常用于集体声明；并集选择器可以选择多组标签；并集选择器是各选择器通过英文逗号（,）连接而成。

语法：

元素1,

元素2,

... {样式声明}

<font color='orange'>语法规范：</font>并集选择器竖着写，并且最后一个选择器不需要加逗号

### （4）链接伪类选择器

伪类选择器最大的特点是用冒号（:）表示。

链接伪类选择器`<a></a>`

`a:link` //所有未被访问的链接

`a:visited` //所有已被访问的链接

`a:hover` //鼠标指针位于其上的链接 ★

`a:active ` //鼠标按下未弹起的链接

<font color='orange'>注意事项：</font>按照LVHA的顺序写，:link-:visited-:hover-:active；

需要给a链接单独指定样式，不受body影响；

### （5）focus伪类选择器

:focus伪类选择器用于获取焦点的表单元素。

input:focus {

background-color: \'颜色\';

color: \'颜色\';

\...

}

## 2.4 css的元素显示模式

HTML元素一般分为块元素和行内元素两种类型。

### （1）块元素

如\<h1\>\~\<h2\>、\<p\>、\<div\>、\<ul\>、\<ol\>、\<li\>、\<form\>、\<table\>等

特点：

自己独占一行；

宽度、高度、内外边距都可以设置；

宽度默认是容器（父级宽度）的100%；

是一个容器及盒子，可以放任何标签。

注意：（例外）文字类的元素不能使用块级元素，如\<p\>/\<h1\>\~\<h6\>（即\<p\>里不能放\<div\>）

### （2）行内元素

\<a\>、\<b\>、\<strong\>、\<i\>、\<em\>、\<span\>等

特点：

相邻行内元素在同一行上，一行可以显示多个行内元素；

宽、高设置无效；（背景颜色其他可以设置）

默认宽度就是它本身内容的宽度；

行内元素只能收纳文本或其他行内元素，不能放块级元素。

注意：链接里不能再放链接了；（例外）特殊链接\<a\>里面可以放块级元素，但是要给\<a\>转换一下块级模式。

### （3）行内块元素

如\<img /\>、\<input /\>、\<td\>

特点：

相邻行内元素在同一行上，中间会有空白缝隙。一行可以多个行内块元素；

默认宽度就是它本身内容的宽度；

宽、高、内外边距可以设置。

### （4）元素显示模式的转换

特殊情况下，一种模式的元素转换成另一种模式，如\<a\>

转换为块级元素： display: block; ★

转换为行内元素： display: inline;

转换为行内块： display: inline-block; ★ //之间会出现空隙

## 2.5 css的背景

//见手册css2.0中文手册.chm

### （1）背景属性/背景复合写法：background

<font color='cornflowerblue'>background: 背景颜色或者（背景色半透明） 背景图片地址 背景平铺 背景滚动（固定） 背景图片位置;</font>  //顺序没有要求，中间用空格隔开

### （2）背景颜色：background-color: transparent; （背景颜色默认值：透明）

### （3）背景图像：background-image: none \| url(); //不要落下url

### （4）背景图像的位置：background-position: x y; ★

x水平坐标和y垂直坐标，可以使用方位名词或者精确单位。

对于\<body\>的超大背景图，可水平居中 background-position: center top;

<font color='orange'>**a.参数是方位名词：**</font>

如果指定的两个都是方位名词，则两个值前后顺序无关，比如left top和top left效果一致；

如果只指定了一个方位名词（x或y），另一个值省略，则第二个值（y或x）默认居中。

<font color='orange'>**b.参数精确单位：**</font>

若为精确单位，则第一个值一定是x，第二个值是y；

如果只指定一个数组，那该数值一定是x坐标，另一个是默认居中。

<font color='orange'>**c.参数是混合单位**</font>

指定的两个值是精确单位和方位名词混用，则第一个值是x，第二个值是y。

### （5）背景图像固定：background-attachment（背景附着）

background-attachment: scroll \| fixed;

scroll //背景图像随对象滚动，默认

fixed //背景图像固定

background-attachment可以制作视差滚动效果。

### （6）背景平铺：background-repeat: no-repeat; //背景图片不平铺

repeat / no-repeat / repeat-x / repeat-y

页面元素既可以添加背景颜色又可以添加背景图片，图片在上。

### （7）背景色半透明：background: rgba(0,0,0,0.3);

最后一个参数是alpha透明度，取值范围在0\~1之间；

一般习惯把0.3的0省略，写成background: rgba(0,0,0,.3); //后面必须是4个值；

背景色半透明，内容不会影响。

## 2.6 css三大特性

css重要的三大特性：层叠性、继承性、优先级

### （1）层叠性

样式冲突：就会层叠，执行就近原则，离body最近的 //有两个相同的样式；

样式不冲突：不会层叠。

### （2）继承性

css中的继承：子标签会继承父标签的样式

### （3）优先级

选择器相同，则执行层叠性

选择器不同，则根据选择器权重执行 //继承的权重是0，不管父级权重多高，都执行子级样式。

### （4）权重叠加

如果是复合选择器，则会有权重叠加，需要计算权重；

权重以四组为一个单位，虽然会叠加，但是永远不会有进位；

如ul li 权重大于 li

## 2.7 css盒子模型

盒子模型：就是把HTML页面布局看作是一个可以装内容的盒子，css盒子模型用来装饰它。

css盒子模型组成部分：边框、内外边距和实际内容。

<img src="picture/2.png" style="zoom:67%;" /> 

（图来源于菜鸟教程）

### （1）border边框 

**a.边框简写：**

border: border-width border-style border-color; //边框 样式 颜色 ，没有先后顺序

**b.边框分开写：**

border-top: border-width border-style border-color; //top bottom left right

border与border-top是层叠性，就近原则。

其中常见border-style: solid / dashed / dotted; //实线 虚线 点线

//border-color: transparent; 透明边框

//见手册css2.0中文手册.chm

**c.表格边框细化：border-collapse**

border-collapse: collapse; //表示相邻边框会合并在一起。collapse单词是合并的意思

如：

table，

td {

border: 2px solid \#000;

border-collapse;

}

### （2）content内容

### （3）padding内边距

内边距即边框与内容的距离。

padding-top: \*px; //top right bottom left

padding: \*px \*px \*px \*px; //顺序为上、右、下、左，按照顺时针

**简写属性：★**

padding: \*px; //1个值，上下左右相同

... //2个值，上下、左右

... //3个值，上、左右、下

... //4个值，上、右、下、左，按照顺时针

### （4）margin外边距

外边距即盒子和盒子之间的距离。

margin-top: \*px; //top right bottom left

margin: \*px \*px \*px \*px; //顺序为上、右、下、左

**a.简写属性：★**

margin: \*px; //1个值，上下左右相同

... //2个值，上下、左右

... //3个值，上、左右、下

... //4个值，上、右、下、左，按照顺时针

**b.外边距可以让块级盒子水平居中**，但必须满足以下两个条件：

a.盒子必须指定宽度（width）

b.盒子左右的外边距都设置为auto

常见以下三种写法：

margin-left: auto; margin-right: auto;

margin: auto;

margin: \*px auto;

注意：以上的方法是让块元素水平居中，行内元素或者行内块元素水平居中给其父元素添加text-align: center;即可。

**c.嵌套元素垂直外边距的塌陷**

对于两个嵌套关系（父子关系）的块元素，父元素有上外边距的同时子元素上也有上外边距，此时父元素会塌陷较大的外边距值。（即子元素与父元素的上边框不能相隔开）

解决方案：

a.为父元素定义上边距

b.为父元素定义上内边距

c.为父元素添加overflow: hidden; ★

**d.清除内外边距**

网页元素很多都带有磨人的内外边距，不同浏览器默认的也不一样。因此在网页布局前，首先要清除网页元素的内外边距，如下：

\* {

margin: 0;

padding: 0;

}

注意：行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距。但是转换为块级和行内块元素就可以了。 //如\<span\>

## 2.8 圆角边框、盒子阴影、文字阴影

### （1）圆角边框

★ border-radius: lenghth; //radius半径原理（圆的半径）

数值单位px或者百分比

<font color='orange'>**a.正方形-圆形：**</font>

border-radius: \*px; //高度的一半

border-radius: 50%;

<font color='orange'>**b.矩形-圆角矩形：**</font>

border-radius: \*px; //高度的一半

border-radius: \*px \*px \*px \*px; //顺时针顺序

... //2-4个数值

<font color='orange'>**d.分开写：**</font>

border-top-left-radius、border-top-right-radius

border-bottom-left-radius、border-bottom-right-radius //先写上下

### （2）盒子阴影

★ box-shadow: h-shadow \| v-shadow \| blur \| spread \| color \| inset;

h-shadow必需，水平阴影的位置，允许负值

v-shadow必需，垂直阴影的位置，允许负值

blur模糊距离 //阴影虚-实

spread阴影尺寸

color阴影颜色 //一般使用半透明，如rgba（0,0,0,.3）

inset将外阴影（outset）改为内阴影

默认外阴影，但是不可以写outset这个单词，否则会导致阴影无效。若为内阴影，则写inset单词。

盒子阴影不占网页空间，不会影响其他盒子排列。

<font color='orange'>**a.鼠标经过后有阴影效果**</font>

盒子:hover

//如div:hover {box-shadow: 10px 10px 10px -4px rgba(0,0,0,.3);}

### （3）文字阴影

text-shadow: h-shadow \| v-shadow \| blur \| color;

## 2.9 css布局方式

css提供了三种传统布局方式（PC端）：普通流（标准流）、浮动、定位。

实际开发中，一个页面基本都包含了这三种布局方式。

### （1）普通流（标准流）

**标准流：**标签按照规定好默认方式排列。

块级元素独占一行，从上向下；

行内元素按照顺序，从左到右，碰到父级元素自动换行。

### （2）浮动

<font color='orange'>**a.为什么需要浮动？**</font>

因为有很多布局效果，标准流没有办法完成，此时就可以利用浮动来完成布局，浮动可以改变元素标签默认的排列方式。

<u>网页布局第一准则：</u>多个块级元素纵向排列找标准流，多个块级横向排列找浮动。

<u>网页布局第二准则：</u>先设置盒子大小，之后设置盒子的位置。

<font color='orange'>**b.什么是浮动？**</font>

浮动：float用于创建浮动框，知道左边缘或右边缘触及包含块或[另一个浮动框的边缘]{.ul}。

选择器 {float: 属性值;}

<font color='orange'>**c.设置了浮动（float）的元素特性1：★**</font>

脱离了标准流的控制（浮）移动到指定位置（动）； //脱标

浮动的盒子不再保留原先的位置。 //后面的标准流盒子会占领浮动盒子原先的位置

<font color='orange'>**d.浮动特性2：★**</font>

如果多个盒子设置了浮动，则它们会按照属性值一行内显示，并且顶端对齐排列。

注意：浮动的元素是相互贴靠在一起的（不会有空隙），如果父级宽度装不下这些浮动的盒子，多出的盒子就会另起一行对齐。

<font color='orange'>**e.浮动特性3：★**</font>

浮动元素具有行内块元素特性；

任何元素都可以浮动，不管原先是什么模式的元素，添加浮动之后具有行内块元素相似的特性。

//即如果行内元素有了浮动，则不需要转换块级、行内块元素就可以直接给高度和宽度

\*如果块级盒子没有设置宽度，默认宽度和父级一样宽，但是添加了浮动后，它的大小根据内容来决定。

\*浮动的盒子中间没缝隙的，是紧挨着一起。

\*行内元素同理。

<font color='orange'>**f.浮动元素经常和标准流父级搭配使用：**</font>

措施：先用标准流的父元素排列上下位置，之后内部元素才去浮动排列左右位置，符合网页布局第一准则。

<font color='orange'>**g.浮动布局注意点：**</font>

- a.浮动和标准流的父盒子搭配：

先用标准流的父元素排列上下位置，之后内部子元素采取排列左右位置。

- 一个元素浮动了，理论上其余的兄弟元素也要浮动。

浮动的和盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流。

<font color='orange'>**h.清除浮动：**</font>

由于父级盒子很多情况下，不方便给高度（高度根据子盒子的内容改变），但是子盒子浮动又不占有地方，最后父级盒子高度为0时，就会影响下面的标准流盒子。

父级没高度、子盒子浮动、影响下面盒子布局，此时需要清除浮动。

选择器 {clear: 属性值;}

`clear: both;`   //同时清除左右两侧浮动。几乎只用这个

<font color='orange'>**i.清除浮动的方法**</font>

清除浮动的本质：清除浮动元素脱离标准流的影响。

策略：闭合浮动，只让浮动在父盒子内不影响，不影响父盒子外面的其他盒子。

- 额外标签法，也称隔墙法  //不常用

在父级盒子中的最后一个浮动盒子末尾添加一个空的盒子，并设置`clear: both;`  //如`<div style="clear: both"></div>`，或者其他标签如`<br />`

<u>新增的盒子要求必须是块级元素</u>

- 父级添加overflow属性

属性值：hidden、auto、scroll

缺点：无法显示溢出的部分。

- 父级添加:after伪元素

:after方式是额外标签法的升级版

```css
.clearfix:after {
	content: "";
	display: block;
	height: 0;
	clear: both;
	visibility: hidden;
}
.clearfix {  <!--IE6、7专有-->
	*zomm:1;
}
```

- 父级添加双伪元素

```css
.clearfix:before,
.clearfix:after{
	content: "";
	display: table;
}
.clearfix:after {
	clear:both
}
.clearfix {  <!--IE6、7专有-->
	*zomm:1;
}
```

### （3）定位

<font color='orange'>**a.为什么需要定位？**</font>

浮动可以让多个块级盒子一行没有缝隙排列显示。

定位则是可以让盒子自由的在<u>某个盒子内移动位置</u>或者<u>固定屏幕中某个位置</u>，并且可以压住其他盒子。

<font color='orange'>**b.定位组成**</font>

**定位=定位模式+边偏移**

定位模式：用于指定一个元素在文档中的定位方式。边偏移：决定了该元素的最终位置。

定位模式，css的potion属性来设置：

|   属性值   |   语义   | 特点                                                         |
| :--------: | :------: | :----------------------------------------------------------- |
|   static   | 静态定位 | 静态定位按照标准流特性摆放位置，没有变偏移                   |
| relative ★ | 相对定位 | 它是相对于**自己**原来的位置来移动的；<br />原来在标准流的位置**继续占有**，后面的盒子仍然以标准流的方式对待它。  //不脱标 |
| absolute ★ | 绝对定位 | 绝对定位移动位置的是相对于**祖先元素**；<br />如果没有祖先元素或者祖先元素没有定位，则以浏览器为准定位（document文档）;<br />如果父元素有定位（相对、绝对、固定），则以**最近一级**的有定位的祖先元素为参考点移动位置；<br />绝对定位**不再占有**原先的位置。  //脱标 |
|  fixed ★   | 固定定位 | 以浏览器的可视窗口为参照点移动元素;  //可视窗口：随着浏览器缩放显示的内容；<br />*与父元素没有任何关系、不随滚动条滚动*<br />固定定位**不占有**位置。  //脱标 |
|   sticky   | 粘性定位 | 可以被认为是相对定位和固定定位的混合；<br />以浏览器的可视窗口为参照点移动元素;<br />粘性定位**占有**原先的位置；<br />必须添加top 、left、right、bottom其中一个才有效。  //缺点：兼容性差、IE不支持 |

边偏移，有`top bottom left right`，4个<u>属性</u>。如`top: *px;`  //可负可正

<font color='orange'>**c.子绝父相** </font> （子级绝对定位，父级相对定位）

- 原因：

子级绝对定位，不会占用位置，可以放到读盒子里的任一个地方，不影响其他兄弟盒子；

父盒子需要加定位为限制子盒子在父盒子内显示；  //绝对定位第二个特点

父盒子布局时，需要占有位置，因此是相对定位，子盒子不需要占有位置，则是绝对定位

<font color='orange'>**d.固定定位：固定在版心的右侧位置**</font>

（一般固定定位都是靠近页面边缘的，`top/bottom/left/right: *px;`）

<font color='cornflowerblue'>小算法：</font>

- 让固定定位的盒子`left: 50%;`，到版心（可视窗口）的一半位置；
- 让固定定位的盒子`margin-left: 版心宽度的一般距离`。

<font color='orange'>**e.定位叠放次序 z-index**</font>

z-index可控制盒子重叠的前后次序（z轴）

`选择器 {z-index: 1;}`

- 数值可以正整数、负整数、0，默认是auto，数值越大，盒子越靠上；
- 如果属性值相同，则按照书写顺序，后来居上；
- 数值后面不能加单位；
- 只有定位的盒子才有z-index属性。

---

**定位的拓展：**

<font color='orange'>**f.绝对定位和固定定位的盒子居中（水平垂直）**</font>

加了**绝对定位（或者固定定位）**的盒子不能够通过`margin: 0 auto;`水平居中，但是可以通过计算方法实现水平和垂直居中。   //相对定位可以

<font color='cornflowerblue'>小算法：</font>

- `left: 50%; `让盒子的左侧移动到父级元素的水平中心位置；
- `margin-left: -*px; `让盒子向左移动自身宽度的一半。

<font color='orange'>**g.定位的特殊性**</font>

绝对定位和固定定位也和浮动类似。

- **行内元素**添加绝对或者固定定位，可以直接设置高度和宽度；
- **块级元素**添加绝对定位或者固定定位，如果不给宽度或者高度，默认大小是内容的大小。

<font color='orange'>**h.脱标的盒子不会触发外边距塌陷**</font>

浮动元素、绝对定位（固定定位）元素的都不会触发外边距合并的问题。

<font color='orange'>**i.绝对定位（固定定位）会完全压住盒子**</font>

- 浮动元素不同，只会压住它下面标准流的盒子，但是不会压住下面标准流盒子里面的文字（图片）。

- 但是绝对定位（固定定位）会压住下面标准流所有的内容。

//浮动之所以不会压住文字，是因为最初产生的目的是为了做<u>文字环绕</u>的效果，文字会围绕浮动元素。

### （4）页面布局

<font color='orange'>**a.常见的网页布局**</font>

`top-banner-main-footer`  //自上而下排列

`top-banner-（left、right）-footer`  //用到浮动

... //用浮动，划分为更多个

<font color='orange'>**b.页面布局有三大核心：**</font>盒子模型、浮动、定位

一个完整的网页是标准流、浮动、定位一起完成布局的。

<u>网页布局第一准则：</u>多个块级元素纵向排列找标准流，多个块级横向排列找浮动。

<u>网页布局第二准则：</u>先设置盒子大小，之后设置盒子的位置。

- 标准流

可以让盒子上下排列或者左右排列，<font color='cornflowerblue'>垂直的块级盒子就用标准流布局。</font>

- 浮动

可以让多个块级元素一行显示或者左右对齐盒子，<font color='cornflowerblue'>多个盒子水平显示就用浮动布局。</font>

- 定位

定位最大的特点是有层叠性，可以让盒子前后叠压来显示。<font color='cornflowerblue'>如果元素自由在某个盒子内移动就用定位布局。</font>

网页元素基本都是盒子；

利用css设置好盒子样式，摆放到相应位置；

往盒子里装内容。

<font color='orange'>**d.边框会影响盒子实际大小：**</font>

border边框：测量盒子时不量边框或者量边框后再减去边框大小。

padding边框：

如果保证盒子跟效果图一样，则让width/height减去多出来的内边距大小即可。

如果段落没有width属性，即设置padding: 0 \*px;不会撑开盒子的宽度 //margin同理

如果段落没有height属性，即设置padding: \*px 0;不会撑开盒子的高度 //margin同理

<font color='orange'>**e.导航栏**</font>

由于相同边框的多个盒子里padding会受文字多少的影响，因此有两种方式：

方式1：每个盒子宽度相同，但padding可能不一样。

方式2：直接设置padding不设置盒子边框，此时每个盒子宽度就不一样

<font color='orange'>**f.清除内外边距**</font>
在网页布局前，首先要写！清除网页元素的内外边距，如下：

`*{ `

`margin: 0;`

`padding: 0;`

`}`

<font color='orange'>**g.布局用不同的盒子**</font>

一般标题用h标签，大量文字段落用p标签 //布局不要全用div标签

//不同的标签就相当于不同的盒子

<font color='orange'>**h.给每个盒子都取类名，选取盒子更容易，后期也方便维护**</font>

## 2.10 元素的显示与隐藏

本质：让一个元素在页面中隐藏或者显示出来。

###（1）display显示隐藏 ★

- `display: none;` **隐藏**对象  //用的更多
- `display: block;` 除了转换为块级元素之外，同时还有**显示**元素的意思

<font color='cornflowerblue'>display隐藏元素后，**不再占有**原来的位置。</font>

###（2）visibility显示隐藏

- `visibility: hidden;` 元素**隐藏**
- `visibility: visible;` 元素**可见** 

<font color='cornflowerblue'>visibility隐藏元素后，**继续占有**原来的位置。</font>

###（2）overflow溢出显示隐藏

- `visibility: hidden;` 内容溢出的部分**隐藏**
- `visibility: visible;` 内容溢出的部分**可见** 
- `visibility: scroll;` 内容溢出的部分显示滚动条，不溢出也显示滚动条
- `visibility: auto;` 内容溢出的时候才显示滚动条，不溢出不显示滚动条

<font color='cornflowerblue'>但是如果有定位的盒子，要慎用overflow: hidden; 因为他会隐藏多余的部分。</font>

## 2.11 css属性书写顺序

建议遵循以下顺序：

### （1）布局定位属性

`display / position / float / clear / visibility / overflow` （display第一个写）

### （2）自身属性

`width / height / margin / padding / border / background`

### （3）文本属性

`color / font / text-decoration / text-align / vertical-align / white-space / break-word`

### （4）其他属性

（css3）：`content / cursor / border-radius / box-shadow / text-shadow / background: linear-gradient...`

## 2.12 PS切图

### （1）图片格式：

jpg：常用于产品类的图片  //切片工具切出的有背景色

gif：常用于一些图片小动画效果

png：可以切成背景透明的图片（用切片工具）  //以上三个格式可以直接放到网页中

psd：Photoshop专用格式，可以直接从上面复制问女子，获得图片，还可以测量大小和距离

---

PS切图方式有：图层切图、切片切图、PS插件切图等。

### （2）图层切图

移动工具--点击图片--右击图层--快速导出为png

很多情况下需要合并图层再导出：

shift--选中需要的多图层--图层菜单--合并图层（ctrl+E）

右击--快速导出为PNG

### （3）切片切图

- 利用切片选中图片

切片工具手动划出

- 导出选中图片

文件菜单--导出--存储为web设备所用格式--选择所要图片格式--存储--选中的切片

### （4）PS插件切图

Cutterman，运行在Photoshop中的插件  //官网下载  [链接](http://www.cutterman.cn/zh/cutterman)

## 补充

### （1）单行文字垂直居中

让文字的行高等于盒子的高度。`line-height: height;`

<img src="picture/3.png" style="zoom:50%;" /> 

(图来源pink老师PPT)

规律：如果行高小于盒子高度，文字偏上；如果行高大于盒子高度，文字偏下。

### （2）方位名词/精确单位

|  参数值  |                   说明                   |
| :------: | :--------------------------------------: |
|  length  |                  百分数                  |
| position | top\|center\|bottom\|left\|center\|right |

### （3）字体不加粗/em不倾斜

`font-weight: 400; / font-style: normal;`

### （4）行高 line-height

```css
body {
    font: 12px/24px 'Microsoft YaHei';
    或者
    font： 12px/1.5 'Microsoft YaHei';  //行高可以不带单位，此时行高为12*1.5 px
}
```

body行高1.5这样写法可以使子元素根据自己文字大小自动调整行高。

### （5）去掉li前面的项目符号

```css
li {
    list-style: none;
}
```

### （6）left/right（top/bottom）

如果一个盒子既有left属性也有right属性，则默认汇之星left属性，

同理，top/bottom会执行top。

### （7）鼠标经过后显示遮罩层

如：

```css
/* 当鼠标经过了盒子(.tudou),就让里面的遮罩层(.mask)显示出来 */
    .tudou:hover .mask {
      display: block;
    }
```

##  所遇到的问题

（1）对于div中内容的居中：

`text-align：center；` //水平居中

`line-height：\*px；` //垂直居中，其中\*是height高度

（2）input //css表单

可直接设置边框样式

```css 
border: *px solid #fff;
padding: *px *px;
height: *px;
width: *px;
```

### （3）图像放入盒子（如\<div\>）时，图像宽度设为100%即宽度与父级元素宽度相同。

# 3. 工具

## 3.1 Snipaste 截图工具

F1可以截图，同时测量大小，设置箭头、书写文字等；（类似qq截图）

F3在桌面置顶显示；（类似贴图）

点击图片，按alt可以取色，按下shift可以切换取色模式；

esc取消图片显色。

## 3.2 Photoshop

- 测量网页图片操作：ps打开网页截图\--视图\--标尺（快捷键ctrl+r）\--右击标尺，单位改为像素---ctrl+加号放大视图，ctrl+减号缩小视图---矩形选框工具

- 开发工具：PS切图/cutterman插件+vscode（代码）+chrome（测试）

# 4. vscode快捷键

## 4.1 Emmet语法

使用Tab键

（1）vscode快速格式化代码：shift+alt+f

（2）文件---设置---搜索'format'---选择保存时格式化

![](picture/4.png) 

（3）生成多个标签，加上\*后按Tab键，如div\*3可以快速生成3个div

（4）直接输入标签名后按Tab键，如div+Tab键，就可以生成\<div\>\</div\>

（5）同时按shift+alt，鼠标往下拉可以输入内容，可输入多个相同内容。

