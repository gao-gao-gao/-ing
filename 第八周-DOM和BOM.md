# 1. Web APIs

Web APIs 是 JS 的应用，大量使用 JS 基础语法做交互效果。

**js的组成：**

![](images\QQ截图20201224112900.png) 

**API 和 Web API：**

**（1）API**

API（Application Programming Interface,应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力。

- API 是给程序员提供的一种工具，以便能更轻松的实现想要完成的功能。

**（2）Web API**

Web API 是浏览器提供的一套操作浏览器功能和页面元素的 API ( BOM 和 DOM )。

可参考MDN查看详细API

**总结：**

- API 是为我们程序员提供的一个接口，帮助我们实现某种功能，学会使用就可以了，不必纠结内部如何实现。

-  Web API 主要是针对于浏览器提供的接口，主要针对于浏览器做交互效果。

- Web API 一般都有输入和输出（函数的传参和返回值），Web API 很多都是方法（函数）

# 2. DOM 文档对象模型

文档对象模型（Document Object Model，简称 DOM），是 W3C 组织推荐的处理可扩展标记语言（HTML或者XML）的**标准编程接口**。

## 2.1 DOM 树

- 文档：一个页面就是一个文档，DOM 中使用 document 表示
-  元素：页面中的所有标签都是元素，DOM 中使用 element 表示
-  节点：网页中的所有内容都是节点（标签、属性、文本、注释等），DOM 中使用 node 表示

**DOM 把以上内容都看做是对象**

我们获取过来的DOM元素是一个对象（object），所以称为 文档对象模型。

## 2.2 获取元素

获取页面中的元素可以使用以下几种方式：

**（1）根据 ID 获取**

使用 getElementById() 方法可以获取带有 ID 的元素对象。[MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementById)

**`document.getElementById('id');`**

- 使用 console.dir() 可以打印我们获取的元素对象，更好的查看对象里面的属性和方法。

例子：

```html
<body>
    <div id="time">2019-9-9</div>
    <script>
        // 1.因为我们文档页面是从上往下加载，所以先得有标签，所以script卸载标签下面
        // 2.get 获得element元素 通过驼峰命名方法
        // 3.参数id是大小写敏感的字符串
        // 4.返回的是一个元素对象
        var timer = document.getElementById('time');
        console.log(timer); //<div id="time">2019-9-9</div>
        console.log(typeof timer); //object
        //打印我们获取的元素对象
        console.dir(timer);
    </script>
</body>
```

**（2）根据标签名获取**

使用 getElementsByTagName() 方法可以返回带有指定标签名的**对象的集合**。

**` document.getElementsByTagName('标签名');`**

- 该方法返回的是 获取过来元素对象的集合，以伪数组的形式存储的
-  因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历。
- 得到元素对象是动态的
- 如果页面中只有一个元素，返回的还是伪数组形式；如果获取不到元素，则返回为<u>空的</u>伪数组(因为获取不到对象)

例子：

```js
//遍历方式
var lis = document.getElementsByTagName('li');
for(var i = 0;i<lis.length;i++) {
    console.log(lis[i]);
}
```

-----

还可以获取某个元素(父元素)内部所有指定标签名的子元素

**`element.getElementsByTagName('标签名');`**   

（指的是父元素.getElementsByTagName('标签名')）

注意：父元素必须是<u>单个对象</u>(必须指明是哪一个元素对象). 获取的时候不包括父元素自己。

例子：

```js
//element.getElementsByTagName('标签名');
//方法一：
var ol = document.getElementsByTagName('ol'); //[0l]单个元素还是以伪元素形式返回
console.log(ol[0].getElementsByTagName('li'));

//方法二：给ol添加id 推荐
var ol = document.getElementsByTagName('id名');
console.log(id名.getElementsByTagName('li'))
```



**（3）通过 HTML5 新增的方法获取**（ie9以上的版本）

**`1. document.getElementsByClassName(‘类名’)；// 根据类名返回元素对象集合`**

**`2. document.querySelector('选择器');        // 根据指定选择器返回第一个元素对象`**

**`3. document.querySelectorAll('选择器');     // 根据指定选择器返回所有元素对象`**



注意：`querySelector` 和` querySelectorAll` 里面的选择器需要加符号（类.  id#  标签不需要加符号）；

比如：`document.querySelector('#nav');`  

------------

**（4）特殊元素获取（body，html）**

- 获取body元素

**`doucumnet.body  // 返回body元素对象`**

- 获取html元素

**`document.documentElement  // 返回html元素对象`**

## 2.3  事件基础

简单理解： 触发--- 响应机制。

**（1）事件三要素**

- 事件源：（谁）事件被触发的对象
- 事件类型 ：（什么事件）如何触发
- 事件处理程序：（做什么）

例子：

```js
//页面中有一个按钮，当鼠标点击按钮的时候，弹出“你好”警示框。
//事件源，获取元素
var btn = document.getElementById('btn');
//事件类型，鼠标点击（onclick）
//事件处理程序，通过一个函数赋值的方式
btn.onclick = function() {
  alert('你好吗');  
};
```

**（2）执行事件的步骤**

- 获取事件源（获取元素）
- 注册事件（绑定事件）
-  添加事件处理程序（采取函数赋值形式）

## 2.4 操作元素

JavaScript 的 DOM 操作可以改变网页内容、结构和样式，我们可以利用 DOM 操作元素来改变元素里面的内容 、属性等。注意以下都是属性：

![](images\QQ截图20201224171410.png) 

**（1）改变元素内容**

**`element.innerText`**  和  **`element.innerHTML`**

-------

**innerText和innerHTML：**

- innerText不识别html标签，去除空格和换行  非标准
- innerHTML识别html标签，保留空格和换行  W3C标准

- 这两个属性是可读写的，除了赋值还可以获取元素里面的内容

例子：

```html
//显示当前时间
<body>
    <button>显示当前时间</button>
    <div>时间</div>
    <p>时间1</p>
    <script>
        //当点击按钮，div里面的文字会发生变化
        // 1.获取元素
        var btn = document.querySelector('button')
        var div = document.querySelector('div');
        // 2.注册事件 btn.onclick
        // 3.添加事件处理程序
        btn.onclick = function () {
            //改变元素内容 赋值
            div.innerHTML = getDate();
        }
        //--------
        function getDate() {
            var date = new Date(); //对象实例化
            var year = date.getFullYear();
            var month = date.getMonth();
            var dates = date.getDate();
            var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            var day = date.getDay();
            return '今天是' + year + '年' + month + '月' + dates + '日 ' + arr[day];
        }

        //---------
        //不通过事件，页面打开直接显示出来
        var p = document.querySelector('p');
        p.innerHTML = getDate();
        
        //--------
        //获取元素里面的内容
        var p1 = document.querySelector('p');
        console.log(p.innerText);
        console.log(p.innerHTML);
    </script>
</body>
```

**（2）常用元素的属性操作**

- innerText、innerHTML 改变元素内容
- src、href
- id、alt、title

**（3）表单元素的属性操作**

- type、value、checked、selected、disabled

其中，disabled（被禁用） 如：`btn.disabled = true;`  或者 `this.disabled = true;` 

(this 指向的是函数事件的调用者，`btn.onclick = function() {...}`)

**（4）样式属性操作**

可以通过 JS 修改元素的大小、颜色、位置等样式。

**`element.style`**     行内样式操作   

//如果样式比较少 或者 功能简单的情况下使用

**注意：**

- JS 里面的样式采取驼峰命名法 比如 fontSize、 backgroundColor
- JS 修改 style 样式操作，产生的是行内样式，<u>CSS 权重比较高</u>

-------

**`element.className`** 类名样式操作   

//适合于样式比较多或者功能复杂的情况

**注意：**

- class因为是个保留字，因此使用className来操作元素类名属性
- className 会直接更改元素的类名，会覆盖原先的类名。
- 如果想要保留原先的类名，可以写成多类名选择器

--------

例子：element.style

```html
<style>
        div {
            margin: 10px auto;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
</style>

<body>
    <div></div>
    <script>
        // 1.获取元素
        var div = document.querySelector('div')
        // 2.注册事件 事件处理程序
        div.onclick = function () {
            // div.style.backgroundColor = 'purple';
            this.style.backgroundColor = 'purple'; //这种写法更推荐
            this.style.width = '200px';
        }
    </script>
</body>
```

例子：element.className

```html
<style>
        div {
            margin: 10px auto;
            width: 100px;
            height: 100px;
            background-color: pink;
        }

        .change {
            width: 200px;
            background-color: purple;
        }
</style>

<body>
    <div class="first"></div>
    <script>
        var div = document.querySelector('div')
        div.onclick = function () {
          // this.style.backgroundColor = 'purple';
          // this.style.width = '200px';
          this.className = 'change';//相当于<div class='change'></div>
          this.className = 'first change'; //多类名选择器，可以保留原先类名 
        }
    </script>
</body>
```

**（5） 排他思想**

如果有同一组元素，我们想要某一个元素实现某种样式， 需要用到循环的排他思想算法：

- 先给所有元素全部清除样式
- 然后再给当前元素设置样式
- 注意顺序不能颠倒

**（6）自定义属性的操作**

**a. 获取属性值**

**`element.属性`**  获取属性值。

**`element.getAttribute('属性');`**

区别：

- element.属性  ：获取内置属性值（元素本身自带的属性）

- element.getAttribute('属性'); 主要获得自定义的属性（标准）（程序员自定义的属性）

-----

**b. 设置属性值**

**`element.属性 = ‘值’`**  设置内置属性值。

**`element.setAttribute('属性', '值'); `**

区别：

- element.属性  ：设置内置属性值

- element.getAttribute('属性'); 主要设置自定义的属性 （标准）

--------

**c. 移除属性**

**`element.removeAttribute('属性');`**

**（7）H5自定义属性**

自定义属性目的：是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中。

自定义属性获取是通过getAttribute(‘属性’) 获取。

但是有些自定义属性很容易引起歧义，不容易判断是元素的内置属性还是自定义属性。因此，H5规定自定义属性data-开头做为属性名并且赋值。

**a. 设置H5自定义属性**

H5规定自定义属性data-开头做为属性名并且赋值。

```html
比如 <div data-index=“1”></div>
或者使用 JS 设置  
element.setAttribute('data-index', 2)
```

**b. 获取H5自定义属性**

- 兼容性获取   **`element.getAttribute(‘data-index’);`**

- H5新增：（ie 11才开始支持）

**`element.dataset.index`**  或者  **`element.dataset[‘index’] `**

**`dataset是一个集合，里面存放了所有以date-开头的自定义属性`**

```html
<div data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        //H5新增的获取自定义属性的方法，他只能获取date-开头的
        console.log(div.dataset); //DOMStringMap {index: "2", listName: "andy"}
        console.log(div.dataset.index); //2
        console.log(div.dataset['index']); //2
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采用 驼峰命名法
        console.log(div.dataset.listName); //andy
        console.log(div.dataset['listName']); //andy
</script>
```

## 2.5 节点操作

获取元素通常使用两种方式：

**利用 DOM 提供的方法获取元素**

- document.getElementById() ；document.getElementsByTagName()；document.querySelector  等；

- 逻辑性不强、繁琐；

**利用节点层级关系获取元素** 

- 利用父子兄节点关系获取元素
- 逻辑性强， 但是兼容性稍差

-----------

**（1）节点概述**

网页中的所有内容都是节点（标签、属性、文本、注释等），在DOM 中，节点使用 node 来表示。

节点至少拥有nodeType（节点类型）、nodeName（节点名称）和nodeValue（节点值）这三个基本属性。

- 元素节点  nodeType  为 1
- 属性节点  nodeType  为 2
- 文本节点  nodeType  为 3 （文本节点包含文字、空格、换行等）

我们在实际开发中，节点操作主要操作的是<u>元素节点</u>。

**（2）节点层级**

![](images\图片4.png) 

**a. 父级节点** 

**`node.parentNode`**

- parentNode 属性可返回某节点的父节点，注意得到的是离元素<u>最近的一个父节点</u>；
- 如果指定的节点没有父节点则返回 null 。

例子：

```html
<body>
    <div class="big-box">
        <div class="box">
            <span class="pic">x</span>
        </div>
    </div>
    <script>
        var pic = document.querySelector('span');
        //利用 DOM 提供的方法获取元素
        var box = document.querySelector('div');  
        //pic.parentNode 利用节点层级关系获取元素
        console.log(pic.parentNode);
    </script>
</body>
```

**b. 子节点**

**`parentNode.childNodes（标准）`**

**`parentNode.children（非标准）`**  （推荐）  //返回的是伪数组形式

- parentNode.childNodes 返回包含指定节点的子节点的集合，该集合为即时更新的集合。

- parentNode.children 是一个只读属性，只返回所有的子<u>元素节点</u>。

**注意：**

<u>返回值</u>里面包含了所有的子节点，包括元素节点，文本节点等。

如果只想要获得里面的元素节点，则需要专门处理。 所以一般不提倡使用childNodes，而使用children。

```js
获取ul里的子元素li
//DOM提供的方法（API）获取
var lis = document.querySelector('ul').querySelector('li');
//节点层级关系获取，parentNode.childNodes
var ul = document.querySelector('ul');
for(var i = 0; i < ul.childNodes.length;i++) {
if (ul.childNodes[i].nodeType == 1) {   // ul.childNodes[i] 是元素节点
    console.log(ul.childNodes[i]);}
}
//parentNode.children
console.log(ul.children);
```



**c. 子节点 **

**`parentNode.firstChild  `** //返回的是文本节点，#text

firstChild 返回第一个子节点，找不到则返回null。包含所有的节点。

**`parentNode.lastChild`** //返回的是文本节点，#text

lastChild 返回最后一个子节点，找不到则返回null。包含所有的节点。

------------

**`parentNode.firstElementChild`**

firstElementChild  返回第一个子元素节点，找不到则返回null。 

**`parentNode.lastElementChild`**

lastElementChild 返回最后一个子元素节点，找不到则返回null。

注意：这两个方法有兼容性问题，IE9 以上才支持。

--------

（推荐：）

**`parentNode.chilren[0]`**

如果想要第一个子元素节点，可以使用 

**`parentNode.chilren[parentNode.chilren.length - 1]`**

如果想要最后一个子元素节点，可以使用 

-----------

---------

**d. 兄弟节点**

**`node.nextSibling`**

nextSibling 返回当前元素的下一个兄弟元素节点，找不到则返回null。包含所有的节点。

**`node.previousSibling`**

previousSibling 返回当前元素上一个兄弟元素节点，找不到则返回null。包含所有的节点。

-------------

**`node.nextElementSibling `**

nextElementSibling 返回当前元素下一个兄弟元素节点，找不到则返回null。 

**`node.previousElementSibling`**

previousElementSibling 返回当前元素上一个兄弟节点，找不到则返回null。

注意：这两个方法有兼容性问题，IE9 以上才支持。

----------

（推荐）

自己封装一个兼容性的函数  

````js
function getNextElementSibling(element) {
      var el = element;
      while (el = el.nextSibling) {
        if (el.nodeType === 1) {
            return el;
        }
      }
      return null;
    } 
````



**（3）创建节点**

**`document.createElement('tagName')`**

创建由 tagName 指定的 HTML 元素。因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点。

**（4）添加节点**

**`node.appendChild(child) `** //node 父级  child 子级

node.appendChild() 方法将一个节点添加到指定父节点的子节点列表<u>末尾</u>。

**`node.insertBefore(child, 指定元素)`**  //node 父级  child 子级

node.insertBefore() 方法将一个节点添加到父节点的指定子节点<u>前面</u>。

指定元素：`node.children[0]`

**（5）删除节点**

**`node.removeChild(child)`**

该方法从 DOM 中删除一个子节点，返回删除的节点。

例子：

```html
<body>
    <button>点击</button>
    <ul>
        <li>笑话</li>
        <li>小草</li>
        <li>校花</li>
    </ul>
    <script>
        //1.获取元素
        var btn = document.querySelector('button');
        var ul = document.querySelector('ul');
        //2.获取事件 删除元素
        btn.onclick = function () {
            if (ul.children.length == 0) {
                this.disabled = true; //按钮不能点击
            } else {
                ul.removeChild(ul.children[0]);
            }
        }
    </script>
</body>
```

**（5）复制节点(克隆节点)**

**`node.cloneNode()`**

该方法返回调用该方法的节点的一个副本。 也称为克隆节点/拷贝节点

注意：

- 如果括号参数为空或者为 false ，则是浅拷贝，只复制标签，不复制内容。
- 如果括号参数为 true ，则是深度拷贝，复制标签和内容。

例子：

```js
 var ul = document.querySelector('ul');
// 1. node.cloneNode(); 浅拷贝
var lili = ul.children[0].cloneNode(true);
ul.appendChild(lili);
```

**（6）三种动态创建元素区别**

- document.write()
- element.innerHTML
- document.createElement()

区别：

document.write 是直接将内容写入页面的内容流，但是文档流执行完毕（页面加载完毕），它会导致页面全部重绘（重新创建一个新的html）；
innerHTML 创建多个元素效率更高（不要拼接字符串，<u>采取数组形式拼接</u>），结构稍微复杂；

createElement() 创建多个元素效率稍低一点点，但是结构更清晰。

总结：不同浏览器下，innerHTML 效率要比 creatElement 高

## 2.6 DOM核心

关于dom操作，我们主要针对于元素的操作。主要有创建、增、删、改、查、属性操作、事件操作。

**（1）创建**

- document.write
- innerHTML
- createElement

**（2）增**

- appendChild
- insertBefore

**（3）删**

- removeChild

**（4）改**

主要修改dom的元素属性，dom元素的内容、属性，表单的值等。

- 修改元素属性： src、href、title 等

- 修改普通元素内容： innerHTML 、innerText
- 修改表单元素： value、type、disabled 等 
- 修改元素样式： style、className

**（5）查**

主要获取查询dom的元素。

- DOM提供的API 方法：  getElementById、getElementsByTagName（不太推荐 ）
- H5提供的新方法： querySelector、querySelectorAll （推荐）
- 利用节点操作获取元素： 父(parentNode)、子(children)、兄(previousElementSibling、nextElementSibling)（推荐）

**（6）属性操作**

主要针对于自定义属性。

- setAttribute：设置dom的属性值
- getAttribute：得到dom的属性值
-  removeAttribute移除属性

**（7）事件操作**

给元素注册事件， 采取  事件源.事件类型 = 事件处理程序

如鼠标事件

## 2.7. 事件高级

### 2.7.1 注册事件（绑定事件）

给元素添加事件，称为注册事件或者绑定事件。

注册事件有两种方式：传统方式和方法监听注册方式

![](images\QQ截图202012qq28155953.png) 

**（1）addEventListener 事件监听方式 **

**`eventTarget.addEventListener(type, listener[, useCapture]) `**

该方法将指定的监听器注册到 eventTarget（目标对象）上，当该对象触发指定的事件时，就会执行事件处理函数。

该方法接收三个参数：

- type：事件类型字符串，比如 click 、mouseover ，注意这里不要带 on，不用onclick
- listener：事件处理函数，事件发生时，会调用该监听函数
- useCapture：可选参数，是一个布尔值，默认是 false

```js
var btns = document.querySelectorAll('button');
// 1. 传统方式注册事件
btns[0].onclick = function() {
      alert('hi');
}
// 2. 事件监听注册事件 addEventListener 
// (1) 里面的事件类型是字符串 一定要加引号 而且不带on
// (2) 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
btns[1].addEventListener('click', function() {
      alert(22);
})
```

**（2）attachEvent 事件监听方式 （了解）**

**`eventTarget.attachEvent(eventNameWithOn, callback) `**

该方法接收两个参数：

- eventNameWithOn：事件类型字符串，比如 onclick 、onmouseover ，这里要带 on
- callback： 事件处理函数，当目标触发事件时回调函数被调用

注意：ie9以前的版本支持

```js
// 3. attachEvent
btns[2].attachEvent('onclick', function() {
            alert(11);
        })
```

------

**注册事件兼容性解决**

兼容性处理的原则： 首先照顾大多数浏览器，再处理特殊浏览器

### 2.7.2 删除事件（解绑事件）

**（1）传统注册方式**

**`eventTarget.onclick = null;`**

**（2）方法监听注册方式**

**`eventTarget.removeEventListener(type, listener[, useCapture]);`**

**`eventTarget.detachEvent(eventNameWithOn, callback);`**

```html
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        var divs = document.querySelectorAll('div');
        divs[0].onclick = function() {
                alert(11);
                // 1. 传统方式删除事件
                divs[0].onclick = null;
            }
            // 2. removeEventListener 删除事件
        divs[1].addEventListener('click', fn); // 里面的fn 不需要调用加小括号
        function fn() {
            alert(22);
            divs[1].removeEventListener('click', fn);
        }
        // 3. detachEvent
        divs[2].attachEvent('onclick', fn1);
        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick', fn1);
        }
    </script>
</body>
```

### 2.7.3 DOM 事件流

**事件流**描述的是从页面中接收事件的顺序。

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即 **DOM 事件流**。

DOM 事件流分为3个阶段： 

- 捕获阶段
- 当前目标阶段 
- 冒泡阶段

例子，给一个div注册点击事件。如图

![](images\图片5.png) 

事件冒泡： IE 最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点的过程。

事件捕获： 网景最早提出，由 DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程。 

注意：

- JS 代码中只能执行捕获或者冒泡其中的一个阶段；
- onclick 和 attachEvent 只能得到冒泡阶段；
- addEventListener(type, listener[, useCapture])第三个参数如果是 true，表示在事件捕获阶段；
- 如果第三个参数是 false（不写默认就是false），表示在事件冒泡阶段调用事件处理程序；
- 实际开发中很少使用事件捕获，更关注事件冒泡，但事件冒泡有时候会带来麻烦；
- 有些事件是没有冒泡的，比如 onblur、onfocus、onmouseenter、onmouseleave。

### 2.7.4 事件对象

```html
<body>
    <div>123</div>
    <script>
        // 事件对象
        var div = document.querySelector('div');
        //传统注册方法
        div.onclick = function(e) {
                console.log(e);
                // console.log(window.event);
                // e = e || window.event;
            }
        //监听注册方法
        div.addEventListener('click', function(e) {
               console.log(e);
            })
        // 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
    </script>
</body>
```

- event 就是一个事件对象 写到我们监听函数的 小括号里面 当形参来看
- 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数
- 这个事件对象我们可以自己命名 比如 event 、 evt、 e
- 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;

**（1）事件对象的常见属性和方法**

| 事件对象属性方法    | 说明                                                      |
| ------------------- | --------------------------------------------------------- |
| e.target            | 返回**触发**事件的对象（标准）                            |
| e.srcElement        | 返回**触发**事件的对象（非标准 ie6-8使用）                |
| e.type              | 返回事件的类型，比如click、mouseover 不带on               |
| e.cancelBubble      | 该属性阻止冒泡（非标准）                                  |
| e.returnValue       | 该属性阻止默认事件（默认行为）（非标准） 比如不让链接跳转 |
| e.preventDefault()  | 该属性阻止默认事件（默认行为）（标准）                    |
| e.stopPropagation() | 阻止冒泡事件（标准）                                      |

**e.target 和 this 的区别：**

- this 是事件绑定的元素， 这个函数的调用者（绑定这个事件的元素） 

- e.target 是事件触发的元素。

```html
<body>
    <div>123</div>
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <script>
        // 常见事件对象的属性和方法
        // 1. e.target 返回的是触发事件的对象（元素）  this 返回的是绑定事件的对象（元素）
        // 区别 ： e.target：点击了哪个元素，就返回哪个元素 ；this：哪个元素绑定了这个点击事件，那么就返回谁
        var div = document.querySelector('div');
        div.addEventListener('click', function(e) {
            console.log(e.target);
            console.log(this);
            //了解，跟 this 有个非常相似的属性 currentTarget  ie678不认识
            console.log(e.currentTarget);
        })
        
        // 兼容性，了解
        // div.onclick = function(e) {
        //     e = e || window.event;
        //     var target = e.target || e.srcElement;
        //     console.log(target);
        // }
    </script>
</body>
```

````js
        // 常见事件对象的属性和方法
        // 返回事件类型
        var div = document.querySelector('div');
        div.addEventListener('click', fn);
        div.addEventListener('mouseover', fn);
        div.addEventListener('mouseout', fn);

        function fn(e) {
            console.log(e.type);

        }
````

```js
		// 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a');
        a.addEventListener('click', function(e) {
                e.preventDefault(); //  dom 标准写法
            })
            // 传统的注册方式
        a.onclick = function(e) {
            // e.preventDefault(); //普通浏览器
            // e.returnValue; //低版本浏览器 ie678
            return false; // 我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式
            alert(11);
        }
```



**（2）阻止事件冒泡**

- 标准写法：利用事件对象里面的 stopPropagation()方法

**`e.stopPropagation()`**

- 非标准写法：IE 6-8  利用事件对象 cancelBubble 属性

**`e.cancelBubble = true;`**

```js
// 常见事件对象的属性和方法
        // 阻止冒泡  dom 推荐的标准 stopPropagation() 
        var son = document.querySelector('.son');
        son.addEventListener('click', function(e) {
            alert('son');
            e.stopPropagation(); // stop 停止  Propagation 传播
            e.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
        }, false);

        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
        document.addEventListener('click', function() {
            alert('document');
        })
```



**（3）事件委托（代理、委派）**

**事件委托的原理：**不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点。

```js
// 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function (e) {
            // alert('xxx');
            e.target.style.backgroundColor = 'pink'; // e.target 这个可以得到我们点击的对象
```

### 2.7.5 常用的鼠标事件

**（1）禁止鼠标右键菜单 contextmenu**

```js
document.addEventListener('contextmenu', function(e) {
e.preventDefault();
})
```

**（2）禁止鼠标选中 selectstart **

```js
document.addEventListener('selectstart', function(e) {
e.preventDefault();
})
```

**常见的鼠标事件：**

| 鼠标事件    | 触发条件         |
| ----------- | ---------------- |
| onclick     | 鼠标点击左键触发 |
| onmouseover | 鼠标经过触发     |
| onmouseout  | 鼠标离开触发     |
| onfocus     | 获得鼠标焦点触发 |
| onblur      | 失去鼠标焦点触发 |
| onmousemove | 鼠标移动触发     |
| onmouseup   | 鼠标弹起触发     |
| onmousedown | 鼠标按下触发     |

**mouseenter 和mouseover的区别：**

mouseenter 鼠标事件

- 当鼠标移动到元素上时就会触发 mouseenter 事件
- 类似 mouseover，它们两者之间的差别如下
- mouseover 鼠标经过自身盒子会触发，经过子盒子还会触发（是因为冒泡会往上触发）。
-  mouseenter  只会经过自身盒子触发，是因为mouseenter不会冒泡
- 鼠标离开 mouseleave  同样不会冒泡

-------------

**鼠标事件对象:**

event对象 代表事件的状态，跟事件相关的一系列信息的集合。

鼠标事件对象 MouseEvent。

| 鼠标事件对象 | 说明                                  |
| ------------ | ------------------------------------- |
| e.clientX    | 返回鼠标相对于浏览器窗口可视区的X坐标 |
| e.clientY    | 返回鼠标相对于浏览器窗口可视区的Y坐标 |
| e.pageX      | 返回鼠标相对于页面的X坐标  ie9+支持   |
| e.pageY      | 返回鼠标相对于页面的Y坐标  ie9+支持   |
| e.screenX    | 返回鼠标相对于电脑屏幕的X坐标         |
| e.screenY    | 返回鼠标相对于电脑屏幕的X坐标         |

### 2.7.6 常用的键盘事件

**常用键盘事件：**

| 键盘事件   | 触发条件                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeyup    | 某个键盘按键被松开时触发                                     |
| onkeydown  | 某个键盘按键被按下时触发                                     |
| onkeypress | 某个键盘按键被按下时触发 但它不识别功能键 比如ctrl、shift、箭头等 |

注意：

- 如果使用addEventListener 不需要加 on
- 三个事件的执行顺序是： keydown --  keypress  --- keyup

**键盘事件对象：**

键盘事件对象 KeyboardEvent。

| 键盘事件对象 属性 | 说明              |
| ----------------- | ----------------- |
| keyCode           | 返回该键的ASCII值 |

```js
        // 1. 我们的keyup 和keydown事件不区分字母大小写  a 和 A 得到的都是65
        // 2. 我们的keypress 事件 区分字母大小写  a  97 和 A 得到的是65
        document.addEventListener('keypress', function(e) {
            console.log('press:' + e.keyCode);
            
            // 我们可以利用keycode返回的ASCII码值来判断用户按下了那个键
            if (e.keyCode === 65) {
                alert('您按下的a键');
            } else {
                alert('您没有按下a键')
            }
        })
```

# 3. BOM 浏览器对象模型

它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是 window。

BOM 缺乏标准，JavaScript 语法的标准化组织是 ECMA，DOM 的标准化组织是 W3C。

BOM大于DOM。

![](images\QQ截图20201229093403.png) 

**BOM 的构成：**

- window 对象是浏览器的顶级对象；
- 它是 JS 访问浏览器窗口的一个接口；
- 它是一个全局对象。定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法；

- 在调用的时候可以省略 window。如 alert()、prompt() 等，都属于 window 对象方法。

注意：window特殊属性window.name

## 3.1 window 对象的常见事件

### 3.1.1 窗口加载事件

```js
window.onload = function(){}
或者 
window.addEventListener("load",function(){});
```

window.onload 是窗口 (页面）加载事件，当文档内容完全加载完成会触发该事件(包括图像、脚本文件、CSS 文件等)，就调用的处理函数。

注意：

- 有了 window.onload 就可以把 JS 代码写到页面元素的上方，因为 onload 是等页面内容全部加载完毕，再去执行处理函数。

- window.onload 传统注册事件方式 只能写一次，如果有多个，会以最后一个 window.onload 为准。
-  如果使用 addEventListener 则没有限制

```js
document.addEventListener('DOMContentLoaded',function(){})
```

DOMContentLoaded 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等。Ie9以上才支持。

### 3.1.2 调整窗口大小事件

```js
window.onresize = function(){}
或者
window.addEventListener("resize",function(){});
```

window.onresize 是调整窗口大小加载事件,  当触发时就调用的处理函数。

`window.innerWidth` 获取当前屏幕的宽度

## 3.2 定时器

window 对象给我们提供了 2 个定时器方法

**（1）setTimeout() 定时器**

```js
window.setTimeout(调用函数, [延迟的毫秒数]);
```

该定时器方法在定时器到期后执行调用函数，**只调用一次**就结束这个定时器。

- window 可以省略。
- 这个调用函数可以直接写函数，或者写函数名或者采取字符串'函数名()'三种形式。第三种不推荐;
- 延迟的毫秒数省略默认是 0，如果写，单位是毫秒;
- setTimeout()  这个调用函数我们也称为**回调函数** callback
- 因为定时器可能有很多，所以经常给定时器赋值一个标识符。

```js
setTimeout(function() {
            console.log('时间到了');
        }, 2000);
或者
function callback() {
            console.log('爆炸了');
        }
        var timer1 = setTimeout(callback, 3000); //标识符1
        var timer2 = setTimeout(callback, 5000); //标识符2
        // setTimeout('callback()', 3000); // 我们不提倡这个写法
```

**（2）停止 setTimeout()**

```js
window.clearTimeout(timeoutID)
```

注意：

- window 可以省略；
- 里面的参数就是定时器的标识符 。

```html
<button>点击停止定时器</button>
    <script>
        var btn = document.querySelector('button');
        //标识符 timer
        var timer = setTimeout(function() {
            console.log('爆炸了');
        }, 5000);
        btn.addEventListener('click', function() {
            clearTimeout(timer);
        })
    </script>
```



-------

**（3）setInterval() 定时器**

```js
window.setInterval(回调函数, [间隔的毫秒数]);
```

该方法**重复调用**一个函数，每隔这个时间，就去调用一次回调函数。

注意：
与setTimeout() 定时器相同。

**（4）停止 setInterval()**

```js
window.clearInterval(intervalID);
```

注意：

- window 可以省略；
- 里面的参数就是定时器的标识符 。

```html
<button class="begin">开启定时器</button>
    <button class="stop">停止定时器</button>
    <script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        var timer = null; // 定义一个全局变量  null是一个空对象
        begin.addEventListener('click', function() {
            timer = setInterval(function() {
                console.log('ni hao ma');
            }, 1000);
        })
        stop.addEventListener('click', function() {
            clearInterval(timer); //此时的清除定时器不在setinterval函数内，因此需要定义个全局变量
        })
    </script>
```

**（5）this**

this指向：

- 全局作用域或者普通函数中this指向全局对象window（注意定时器里面的this指向window）
- 方法调用中谁调用this指向谁
- 构造函数中this指向构造函数的实例

## 3.3 js执行机制

**（1）JS 是单线程**

JavaScript 语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。

**（2）同步和异步**

例子：

```js
console.log(1);
 
 setTimeout(function () {
     console.log(3);
 }, 1000);
 
 console.log(2); //输出结果 1 2 3
```

```js
console.log(1);
 
 setTimeout(function () {
     console.log(3);
 }, 0);
 
 console.log(2); //输出结果 1 2 3
```

- **同步**

前一个任务结束后再执行后一个任务。

同步任务都在主线程上执行，形成一个<u>执行栈</u>。

- **异步**

同时执行多个任务。

异步任务即回调函数：

异步任务有以下三种类型：

- 普通事件，如 click、resize 等
- 资源加载，如 load、error 等
- 定时器，包括 setInterval、setTimeout 等

异步任务（相关回调函数）添加到<u>任务队列</u>中（任务队列也称为消息队列）。

**（3）JS 执行机制**

- 先执行执行栈中的同步任务；

- 异步任务（回调函数）放入任务队列中；
- 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务。

例子：

```js
 console.log(1);
 document.onclick = function() {
   console.log('click');
 }
 console.log(2);
 setTimeout(function() {
   console.log(3)
 }, 3000)
//输出结果 1 2 3  3秒后点击会输出1 2 3 click
```

由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为**事件循环**（ event loop）。

## 3.4 location 对象

window 对象给我们提供了一个 location 属性用于获取或设置窗体的 URL，并且可以用于解析 URL 。

这个属性返回的是一个对象。

**（1）location 对象的属性**

| location对象属性  | 返回值                               |
| ----------------- | ------------------------------------ |
| location.href *   | 获取或者设置整个url                  |
| location.host     | 返回主机（域名）                     |
| location.port     | 返回端口号，如果未写返回 空字符串    |
| location.pathname | 返回路径                             |
| location.search * | 返回参数                             |
| location.hash     | 返回片段，#后面内容 常见于链接、锚点 |

**（2）location 对象的方法**

| location对象方法   | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟href一样，可以跳转页面（也称重定向页面），可以后退页面     |
| location.replace() | 替换当前页面，因为不记录历史，所有不能后退页面               |
| location.reload()  | 重新加载页面，相当于刷新按钮或者f5，如果参数为true则强行刷新 ctrl+f5 |

例子：数据在不同页面中的传递

```html
//页面1
 <form action="index.html">
        用户名： <input type="text" name="uname">
        <input type="submit" value="登录">
    </form>

//跳转页面2
<div></div>
<script>
        console.log(location.search); // ?uname=andy
        // 1.先去掉？  substr('起始的位置'，截取几个字符);
        var params = location.search.substr(1); // uname=andy
        console.log(params);
        // 2. 利用=把字符串分割为数组 split('=');
        var arr = params.split('=');
        console.log(arr); // ["uname", "ANDY"]
        var div = document.querySelector('div');
        // 3.把数据写入div中
        div.innerHTML = arr[1] + '欢迎您';
</script>
```



------

**URL：**统一资源定位符 (Uniform Resource Locator, URL)

URL 的一般语法格式为：protocol://host[:port]/path/[?query]#fragment

| 组成     | 说明                                                |
| -------- | --------------------------------------------------- |
| protocol | 通信协议 常用htpp,ftp,maito等                       |
| host     | 主机（域名）                                        |
| port     | 端口号，可选.省略时则为默认端口，如http默认端口为80 |
| path     | 路径，由零或多个/ 符号隔开的字符串                  |
| query    | 参数，键值对的形式，通过&符号分隔开来               |
| fragment | 片段，#后面内容，创建于链接、锚点                   |

## 3.5 navigator 对象

navigator 对象包含有关浏览器的信息，它有很多属性，我们最常用的是 userAgent，该属性可以返回由客户机发送服务器的 user-agent 头部的值。

```html
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = "";     //手机
 } else {
    window.location.href = "";     //电脑
 }
```



## 3.6 history 对象

window 对象给我们提供了一个 history 对象，与浏览器历史记录进行交互。该对象包含用户（在浏览器窗口中）访问过的 URL

| history对象方法 | 作用                                                      |
| --------------- | --------------------------------------------------------- |
| back()          | 可以后退功能                                              |
| forward()       | 前进功能                                                  |
| go(参数)        | 前进后退功能，参数如果是1前进1个页面，如果是-1后退1个页面 |

# 4.PC 端网页特效

## 4.1 元素偏移量 offset 系列

offset 翻译过来就是**偏移量**， 使用 offset 系列相关属性可以**动态的**得到该元素的位置（偏移）、大小等。

- 获得元素距离带有定位父元素的位置
- 获得元素自身的大小（宽度高度）
- 注意： 返回的数值都不带单位

| offset系列属性         | 作用                                                         |
| ---------------------- | ------------------------------------------------------------ |
| element.offsetParent   | 返回作为该元素带有定位的父级元素，如果父级都没有定位则返回body |
| elelment.offsetTop *   | 返回元素相对带有定位父元素上方的偏移，如果父级都没有定位则返回body |
| element.offsetLeft *   | 返回元素相对带有定位父元素左边框的偏移，如果父级都没有定位则返回body |
| element.offsetWidth *  | 返回自身包括padding、边框border、内容区域的宽度width，返回数值不带单位 |
| element.offsetHeight * | 返回自身包括padding、border、height，返回数值不带单位        |

**offset 与 style 区别：**

![](images\QQ截图20201229150809.png) 

## 4.2 元素可视区 client 系列

client 翻译过来就是**客户端**，通过 client 系列的相关属性可以**动态的**得到该元素的边框大小、元素大小等。

| client系列属性          | 作用                                                         |
| ----------------------- | ------------------------------------------------------------ |
| elelment.clientTop      | 返回元素上边框的大小                                         |
| elelment.clientLeft     | 返回元素左边框的大小                                         |
| element.clientWidth *   | 返回自身包括padding、内容区域的宽度width，<u>不含边框</u>，返回数值不带单位 |
| element.clientHeight  * | 返回自身包括padding、height、<u>不含边框</u>，返回数值不带单位 |

**立即执行函数**

立即执行函数: 不需要调用，立马能够自己执行的函数

写法：

```js
function fn() {
	console.log(1);
}
fn(); // 需要函数调用

立即执行函数,写法:
(function() {})()   或者   (function(){}()); 
// 立即执行函数也可以传递参数
// 第二个小括号可以看做是调用函数
// 多个立即函数用分号;隔开
// 立即执行函数最大的作用就是 独立创建了一个作用域, 里面所有的变量都是局部变量 不会有命名冲突的情况
```

主要作用： 创建一个独立的作用域。 避免了命名冲突问题

## 4.3 元素滚动 scroll 系列

**onscroll事件**：当使用滚动条时触发的事件。

使用 scroll 系列的相关属性可以**动态的**得到该元素的大小、滚动距离等。

| scroll系列属性         | 作用                                           |
| ---------------------- | ---------------------------------------------- |
| element.scrollTop      | 返回被卷去的上侧距离，返回数值不带单位         |
| element.scrollLeft     | 返回被卷去的左侧距离，返回数值不带单位         |
| element.scrollWidth *  | 返回自身实际的宽度，不含边框，返回数值不带单位 |
| element.scrollHeight * | 返回自身实际的高度，不含边框，返回数值不带单位 |

其中：

- 页面被卷去的头部：可以通过`window.pageYOffset` 获得  如果是被卷去的左侧 `window.pageXOffset`
- **元素**被卷去的头部是 `element.scrollTop`  , 如果是**页面**被卷去的头部 则是 `window.pageYOffset`

---------

**三大系列的区别：**

- **offset**系列 经常用于获得元素位置。    offsetLeft ，offsetTop
- **client** 经常用于获取元素大小。  clientWidth ，clientHeight
- **scroll** 经常用于获取滚动距离。  scrollTop， scrollLeft   
- 注意页面滚动的距离通过 window.pageXOffset  获得。

## 4.4 动画函数

**（1）动画实现原理**

核心原理：通过定时器 setInterval() 不断移动盒子位置。

```
实现步骤：
1. 获得盒子当前位置
2. 让盒子在当前位置加上1个移动距离
3. 利用定时器不断重复这个操作
4. 加一个结束定时器的条件
5. 注意此元素需要添加定位!，才能使用element.style.left
```

**（2）动画函数简单封装**

注意函数需要传递2个参数，动画对象和移动到的距离。

```js
...
// 简单动画函数封装obj目标对象 target 目标位置
        function animate(obj, target) {
            // 当我们不断的点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
            // 解决方案： 让我们元素只有一个定时器执行
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            
            // 给不同的元素指定了不同的定时器obj.timer ,不写成之前的var timer。核心原理：利用 JS 是一门动态语言，可以很方便的给当前对象添加属性。
            obj.timer = setInterval(function() {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    //clearInterval(timer);
                    clearInterval(obj.timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';
            }, 15);
        }

		var div = document.querySelector('div');
        var span = document.querySelector('span');
		var btn = document.querySelector('button');
        // 调用函数
        animate(div, 500);
        //animate(span, 500);
		btn.addEventListener('click', function(){
            animate(span, 500);
        })
```

**（3）缓动效果原理**

缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来

```
思路：
1. 让盒子每次移动的距离慢慢变小，速度就会慢慢落下来。
2. 核心算法： (目标值 - 现在的位置 )/10 ,作为每次移动的距离 步长
3. 停止的条件是：让当前盒子位置等于目标位置就停止定时器  
4. 注意步长值需要取整 Math.ceil
```

例子：

```js
// 匀速动画 就是 盒子是当前的位置 +  固定的值 10 
obj.style.left = obj.offsetLeft + 1 + 'px';

// 缓动动画就是  盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）
obj.timer = setInterval(function() {
    			// 步长值写到定时器的里面
    			//var step = (target - obj.offsetLeft) / 10;
 			    // 把步长值改成整数，不要小数；往上取整 
    			//var step = Math.ceil((target - obj.offsetLeft) / 10);
    			// 当考虑到倒退的情况
    			var step = (target - obj.offsetLeft) / 10;
    			step = step > 0 ? Math,ceil(step) : Math.floor(step);
                if (obj.offsetLeft >= target) {
                    clearInterval(obj.timer);
                }
                obj.style.left = obj.offsetLeft + step + 'px';
            }, 15);
```

**（4）动画函数添加回调函数**

**回调函数原理：**函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，当另一个函数执行完之后，再执行传进去的这个函数，这个过程就叫做回调。

```js
function animate(obj, target, callback) {
    		// console.log(calback); callback = function() {} 调用的时候 calback()
            clearInterval(obj.timer);
            obj.timer = setInterval(function() {
                if (obj.offsetLeft >= target) {
                    clearInterval(obj.timer);
                    // 回调函数写到定时器结束里面
                    if(callback) {
                        calback();
                    }
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';
            }, 30);
        }

		var btn = document.querySelector('button');
        // 调用函数
		btn.addEventListener('click', function(){
            //animate(span, 500, function() {});
            animate(span, 500, function() {
                //alert('你好吗');
                span.style.backgroundColor = 'red';
            })
        })
```

**（5）动画函数封装到单独JS文件里面**

单独封装到一个animate.js文件里面。
