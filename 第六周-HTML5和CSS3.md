# 1. HTML5

## 1.1 新增语义化标签

新特性都有兼容性的问题，基本是IE9+以上版本的浏览器才支持。

div对搜索引擎来说，是没有语义的。

- `<header> `：头部标签
- `<nav>`：导航标签  
- `<article>`：内容标签
- `<section>`：定义文档某个区域   **//相当于大号的div**
- `<aside>`：侧边栏标签
- `<footer>`：尾部标签

**注意：**

- 这种语义话标准主要是针对搜索引擎的
- 这些新标签页面中可以使用多次
- 在IE9中，需要把这些元素转换为块级元素
- 在移动端更喜欢使用这些标签
- HTML5还增加了很其他标签

## 1.2 新增的多媒体标签

新增的多媒体标签主要包含两个：

- 音频：`<audio>`
- 视频：`<video>`

### （1）视频

当前`<video>`元素支持三种视频格式：MP4、webm、ogg   [菜鸟教程--查看不同浏览器兼容](https://www.runoob.com/tags/tag-video.html)

尽量使用MP4格式  //因为大多数浏览器都支持

**语法：**

` <video src="文件地址" controls="controls"></video>`    //controls  播放控件

---

因为有些浏览器版本不支持MP4，因此再添加另一种视频格式，仅参考：

```html 
<video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
    您的浏览器不支持 video 标签。
</video>
```

**常见属性：**

| 属性     | 值                                           | 描述                                                         |
| -------- | -------------------------------------------- | ------------------------------------------------------------ |
| autoplay | autoplay                                     | 视频自动播放（谷歌浏览器需要添加muted来解决自动播放问题）    |
| muted    | muted                                        | 视频静音播放                                                 |
| ontrols  | contros                                      | 视频显示播放控件  //一般不添加，为了适应不同浏览器           |
| loop     | loop                                         | 视频循环播放                                                 |
| preload  | auto（预先加载视频）<br>none（不应加载视频） | 视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| poster   | URL                                          | 加载等待的画面图片                                           |
| src      | URL                                          | 视频url地址                                                  |
| width    | （像素）                                     | 设置播放器宽度                                               |
| height   | （像素）                                     | 设置播放器高度                                               |

### （2）音频

当前`<video>`元素支持三种视频格式：MP3、WAV、Ogg  [菜鸟教程audio](https://www.runoob.com/tags/tag-audio.html)

所有浏览器都支MP3格式

**语法：**

` <audio src="文件地址" controls="controls"></audio>`    //controls  播放控件

**常见属性：**

- 谷歌浏览器把音频的自动播放禁止了

| 属性     | 值                       | 描述                                                         |
| -------- | ------------------------ | ------------------------------------------------------------ |
| autoplay | autoplay                 | 视频自动播放（谷歌浏览器需要添加muted来解决自动播放问题）    |
| ontrols  | contros                  | 音频显示播放控件  //一般不添加，为了适应不同浏览器           |
| loop     | loop                     | 音频循环播放                                                 |
| preload  | auto<br>none<br>metadata | 视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| src      | URL                      | 视频URL地址                                                  |
| muted    | muted                    | 视频静音播放                                                 |

## 1.3 新增的input类型

- 重点记住：number、tel、search这三个。

| 属性值                                  | 说明                        |
| --------------------------------------- | --------------------------- |
| type="email"                            | 限制用户输入必须为email类型 |
| type="url"                              | 限制用户输入必须为url类型   |
| type="date"                             | 限制用户输入必须为日期类型  |
| type="date"                             | 限制用户输入必须为时间类型  |
| type="time"                             | 限制用户输入必须为月类型    |
| type="month"                            | 限制用户输入必须为周类型    |
| type="number"                           | 限制用户输入必须为数字类型  |
| type="tel"                              | 手机号码                    |
| type="search"   //对应之前的type="text" | 搜素框                      |
| type="color"                            | 生成一个颜色选择表单        |

- 对于表单中，验证的时候必须添加form表单域

```html 
<form action="">
    ...
    ...
    //点击提交按钮就可以验证表单了
    <input type="submit" value="提交">
</form>、
```

## 1.4 新增的表单属性

| 属性           | 值        | 说明                                                         |
| -------------- | --------- | ------------------------------------------------------------ |
| requir         | requir    | 表单其内容不能为空，必填                                     |
| placeholder  * | 提示文本  | 表单的提示信息，存在默认值将不显示                           |
| autofocus      | autofocus | 自动聚焦属性，页面加载完成自动聚焦到指定表单                 |
| autocomplete   | off/on    | 当用户在字段开始键入时，浏览器基于之前键入的值，显示出在字段中填写的选项。<br>默认已经打开。<br>需要放在表单内，同时加上name属性，同时成提交。 |
| multiple *     | multiple  | 可以多选文件提交                                             |

- 可以给属性添加颜色：` input：：placeholder {color：pink;}`

# 2. CSS3

新增的css3特性有兼容性，ie9+才支持

## 2.1 新增选择器

### （1）属性选择器

| 选择符        | 简介                                                         |
| ------------- | ------------------------------------------------------------ |
| E[att]        | 选择具有att属性的E元素  //利用属性选择器可以不借助类或id选择器 |
| E[att=val]  * | 选择具有att属性且属性值等于val的E元素  //属性选择器还可以选择属性=值的某些元素 |
| E[att^=val]   | 匹配具有att属性且值以val开头的E元素  //属性选择器可以选择属性值开头的某些元素 |
| E[att$=val]   | 匹配具有att属性且值以val结尾的E元素  //属性选择器可以选择属性值结尾的某些元素 |
| E[att*=val]   | 匹配属性具有att属性且值中俺有att的E元素                      |

**注意：类选择器、伪类选择器、属性选择器权重都是10。**

### （2）结构伪类选择器

常用于根据父级选择器里面的子元素。

| 选择符           | 简介                        |
| ---------------- | --------------------------- |
| E:first-child    | 匹配肤元素中的第一个子元素E |
| E:last-child     | 匹配父元素中最后一个E元素   |
| E:nth-child(n)   | 匹配父元素中第n个子元素E    |
| E:first-of-type  | 指定类型E的第一个           |
| E:last-of-type   | 指定类型E的第最后一个       |
| E:nth-of-type(n) | 指定类型E的第n个            |

**nth-child(n)：**      

n可以是数字，关键字和公式

- n如果是数字，就是选择第n个子元素，里面数字从1开始...
- n可以是关键字：even偶数，odd奇数
- n可以是公式：常见公式如下（如果n是公式，则从0开始计算，但是第0个元素或者超出了元素的个数会被忽略）

```css
//nth-child(n) 从0开始 每次加1 往后面计算  这里面必须是n  不能是其他的字母 n即选择了全部的孩子
ol li:nth-child(n){
	background-color: pink;
}
```

| 公式 | 取值                         |
| ---- | ---------------------------- |
| 2n   | 偶数   //n是从0开始...       |
| 2n+1 | 奇数                         |
| 5n   | 5  10  15...                 |
| n+5  | 从5个开始（包含第5个）到最后 |
| -n+5 | 前5个（包含第5个）           |

匹配与指定的区别：

```css
<style>
	/* nth-child会把所有的盒子都排列序号 */
	/* 执行的时候首先看 nth-chid(1)  之后回去看前面的div */
	section div:nth-child(1){
    	background-color: pink;
}
</style>
...
<section>
	<p>xxx<p>
	<div>xxx</div>
	<div>xxx</div>
<section>

/* 此效果不显示，如果是section div:nth-of-child(1)此效果显示,则执行的时候先看div指定的元素  之后再看:nth-of-child(1)第几个孩子 */
```

### （3）伪元素选择器

伪元素选择器可以帮助我们利用css创建新标签元素，而不需要html标签，从而简化html结构

| 选择符   | 简介                     |
| -------- | ------------------------ |
| ::before | 在元素内部的前面插入内容 |
| ::after  | 在元素内部的后面插入内容 |

**注意：**

- before和after创建一个元素，但是属于行内元素  

  //宽、高不起效果，可转换为行内元素、块元素

- 新创建的这个元素在文档树（.html文件中）中是找不到，所以我们称为伪元素

- 语法：element::before {}

- before和after必须有content属性  

  //content=“xxx”，内容

- before在父元素内容的前面创建元素，after在父元素内容的后面插入元素

- 伪元素选择器和<u>标签选择器</u>一样，权重为1

---

使用场景1： 伪元素字体图标

使用场景2：遮罩层

使用场景3：伪元素清除浮动       见 “css案例”

----

### （4）2D转换

transform可以实现元素的位移、旋转、缩放等效果。

**a. 移动：translate**

（x轴往右增大，y轴往下增大）

语法：

```css
transform: translate(x,y);  /* 或者分开写 */
transform: translateX(n);   /* transform: translate(x,0); */
transform: translateY(n);   /* transform: translate(0,y); */
```

**移动盒子的位置： 定位、盒子的外边距 、2D转化移动**

特点：

- translate移动不会影响其他盒子位置

- translate里面参数可以为px、%；参数是%移动的距离是：盒子自身的宽度或者高度来对比的

- translate对行内元素无效

---

**b. 旋转：rotate**

语法：

`transform: rotate(度数);`

重点：

- rotate里面跟度数，单位是deg，比如rotate(45deg)

- 角度为正时，顺时针，负时，为逆时针

- 默认旋转的中心是元素的中心点

---

**c. 2D转换中心点transform-origin**

语法：

`transform-origin: x y;`

重点：

- 参数x和y用空格隔开
- x y默认转换的中心点是元素的中心点（50% 50%）
- 还可以给x y设置像素或者方位名词（top bottom left right center）

----

**d. 缩放：scale**

语法：

`transform: scale(x,y);`

注意：

- x和y用逗号隔开
- transform: scale(1,1)：宽度和高度都放大一倍，相当于没有放大
- transform: scale(2,2)：宽度和高度放大了2倍
- transform: scale(2)：只写一个参数，此时第二参数和第一个参数一样
- transform: scale(0.5,0.5)：缩小
- scale缩放优势：可以设置转换中心点缩放，默认以中心点缩放，而且不影响其他盒子

----

**2D转换综合写法：**

- 格式：`transform: translate() rotate() scale()..等`
- 其顺序会影响转换效果（先旋转会改变坐标轴的方向）
- 同时有位移和其他属性，我们需要把位移放到最前面

### （5）动画

animation可以设置多个节点来精确控制一个或一组动画，常用来实现复杂的动画效果。

**a. 动画的基本使用**

制作动画分两步：先定义动画、再使用动画

第一步：keyframes定义动画（类似定义类选择器）

```css
@keyframes 动画名称{
    0%{
        width: 100px;
	}
    100%{
        width: 200px;
    }
}
```

**动画序列：**

- 定义：0%是动画的开始，100%是动画的完成
- 在@keyframes中规定某项css样式，就能创建由当前样式逐渐改为新样式的动画效果
- 可以改变任意多的样式，任意多的次数
- 用百分比来规定变换发生时间，或用关键字“from”和“to”，等同于0%和100%

第二步：元素使用动画

```css
div {
    width: 200px;
    height: 200px;
    background-color: aqua;
    margin: 100px auto;
    /* 调用动画 */
    animation-name: 动画名称;
    /* 持续时间 */
    animation-duration： 持续时间：
}
```

---

**b. 动画常见属性**

| 属性                      | 描述                                                        |
| ------------------------- | ----------------------------------------------------------- |
| @keyframes                | 规定动画                                                    |
| animation                 | 所有动画属性的简写属性，除了animation-play-state属性        |
| animation-name            | 规定@keyframes动画名称（必须）                              |
| animation-duration        | 规定动画完成一个周期所花费的秒或毫秒，默认是0（必须）       |
| animation-timing-function | 规定动画的速度曲线，默认是ease                              |
| animation-delay           | 规定动画何时开始，默认是0                                   |
| animation-iteration-count | 规定动画被播放的次数，默认是1，还有infinite                 |
| animation-direction       | 规定动画是否在一周期逆向播放，默认是normal，altermate逆播放 |
| animation-play-state      | 规定动画是否在正在运行或暂停，默认是running，还有pause      |
| animationfill-mode        | 规定动画结束后的状态，保持forwards回到起始backwards         |

简写：animation: 动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 动画起始或结束的状态;

`animationa: name duration timing-function delay iteration-count direction fill-mode play-state;`

## 2.2 css3盒子模型border-box

css3中可以通过box-sizing来指定盒子模型，有2个值：即可指定为content-box、border-box，此时计算盒子大小的方式就发生改变。

分为两种情况：

- `box-sizing: content-box; `  盒子大小为width+padding+border（默认的）
- `box-sizing: border-box; `  盒子大小为width，此时padding和margin就不会撑大盒子（前提padding和border不会超过width宽度）

此时css初始化可以为：

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

## 2.3 css3其他特性（了解）

### （1）图片变模糊

**滤镜filter：**

[属性值参考](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter)

filter css属性将模糊或颜色偏移等图形效果应用于元素。

`filter: 函数();   例如：filter: blur(5px);  blur模糊处理 数值越大越模糊`

### （2）计算盒子宽度calc()函数

calc()函数，在声明css属性值时执行一些计算。

`width: calc(100%-80%);`

**括号里面可以使用+ - * / 来进行计算。**

## 2.4 css过渡

可以在不使用flash动画或JavaScript的情况下，元素从一种样式变换成另一种样式时为元素增加效果。

经常和:hover一起搭配使用。

**谁做过渡给谁加。**

`transition: 要过度的属性 花费时间 运动曲线 何时开始；`   

//如果想要写多个属性变化，用逗号隔开。

- 属性：想要变换的css属性，宽度高度 背景颜色 内外边距都可以。如果想要所有属性都变化过渡，即写一个`all`。
- 花费时间：单位是秒（必须写单位）
- 运动曲线：默认是ease（可省略）
- 何时开始：默认是0s（可省略），单位是秒（必须写单位），可以设置延迟触发时间

# 3. 广义的H5

狭义的HTML5和CSS3指的是：HTML5结构标签本身、CSS3相关样式。

广义的的HTML5是：HTML5本身+CSS3+JavaScript。 [HTML5文档](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)













