# 1. package.json

- 在node.js中，模块是一个库或者框架，也是node.js项目。node.js遵循模块化的结构，当我们创建了一个node.js项目，意味着创建了一个模块，这个模块的描述文件，被称为package.json。   

//package.json位于模块的目录下，用于定义包的属性。

- package.json文件定义了这个项目所需要的各种模块，一级项目的配置信息(比如名称、版本等数据)。

- npm install命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。

---

## （1）package.json属性说明

在文件中，只有项目名称和项目版本是必填的，其他都是选填。

- name--包名称
- version--包的版本号（遵守“大版本.次要版本.小版本”的格式）
- description--包的描述
- homepage--包的官网URL
- author--包的作者，它的值是 [网站](https://npmjs.org) 的有效账号名
- contributors--包的其他贡献者
- keywords--关键字
- man--main字段指定了程序的主入口文件，require()就会加载这个文件。该字段的默认值是模块根目录下的index.js。

---

- scripts--字段指定了运行脚本命令。比如star指定了运行`npm run start`时，所要执行的命令。

所有`node_modules/.bin/`目录下的命令，都可以用`npm run [命令]`的格式运行。在命令行下，键入`npm run`，然后按tab键，就会显示所有可以使用的命令。

```json
"scripts": {
	"prepublish": "",//npm run preinstall，在包发布之前运行，也会在npm install安装到本地时运行
    "publish": "",  //包被发布之后运行
    "preinstall": "",  //包被安装前运行
    "install": "",  //包被安装后运作
    "preuninstall": "",  //包被卸载前运行
    "postuninstall": "",  //包被卸载后运行
    "start": "",  
    "test": ""  
}
```

---

- dependencies--生产环境（项目运行）所依赖的模块 

//如果以来的包没有安装，npm会被自动安装在node_module目录下

分别由模块名和对应的版本要求组成，表示依赖的模块及其版本的范围：

--指定版本号：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本。

--波浪号+指定版本：比如~1.2.2，表示安装1.2.x的最新版本（不低于1.2.2），但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。

--插入号+指定版本：比如ˆ1.2.2，表示安装1.x.x的最新版本（不低于1.2.2），但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容。

--latest：安装最新版本。

- devdependencies--开发环境所依赖的模块  //会被安装在node_module目录下

**--save-dev**

--save：将保存配置信息到pacjage.json的dependencies节点中。

--save-dev或者--dev：将保存配置信息到pacjage.json的devDependencies节点中。

dependencies：运行时的依赖，发布后，即生产环境下还需要用的模块

devDependencies：开发时的依赖。里面的模块是开发时用的，发布时用不到它。

---

- entry point:(index.js)  //入口文件，不用设置
- repository--包代码存放地方的类型，可以是git或svn
- git repository--/项目是否要连接到GitHub仓库去
- text command
- license: (ISC)  //协议
- main--main字段指定了程序的主入口文件，require('moduleName')就会加载这个文件。这个字段的默认值是模块根目录下面的index.js
- config--字段用于向环境变量输出值
- browser--指定该模板提供浏览器使用的版本
- engines--指明了该项目所需的node.js版本
- preferglobal--preferglobal的值是布尔值，表示用户不将该模块安装为全局模块（-global）时，要不要显示警告
- style--指定浏览器使用时，样式文件所在的位置。样式文件打包工具parcelify，通过它知道样式文件的打包位置。
- repository--项目代码的repo信息，包括type和URL，type可以是git或者svn，URL则是包的repo地址
- peerdependencies--提供插件指定所需的主工具的版本

```json
{
  "name": "chai-as-promised",
  "peerDependencies": {
    "chai": "1.x"
  }
}
```

上面代码指定，安装`chai-as-promised`模块时，主程序`chai`必须一起安装，而且`chai`的版本必须是`1.x`。如果你的项目指定的依赖是`chai`的2.0版本，就会报错。

注：从npm 3.0版开始，`peerDependencies`不再会默认安装了。

- bin--用来指定各个内部命令对应的可执行文件的位置

# 2. postcss

[官网](https://www.postcss.com.cn/)

- 是一个用 JavaScript 工具和插件转换 CSS 代码的工具。
- 提供了庞大的[插件库](https://www.postcss.parts/)来提升你的CSS编写体验
- 这个一个用来运行插件的平台

//正常地写完了一句CSS，然后PostCSS的插件就会自动分析代码并转换成你想要的格式

作用：

- 自动添加前缀：增强代码的可读性。利用从 Can I Use 网站获取的数据为 CSS 规则添加不同网页的特定前缀。   // Can I Use 一款前端浏览器的兼容性自查工具
- 将css语法转换成浏览器兼容的语法。
- 限制css类名的作用域，命名不再大众化而造成突出。[CSS 模块](https://github.com/css-modules/css-modules)
- 指出css中的语法错误。

## （1）配置

只需要两步就可以使用postcss

- 查找并添加构建工具的postcss扩展
- 选择插件并将它们添加到postcss进程中

---

- npm安装，命令行运行：

`npm install -g xxx`   //xxx为安装插件的名字

或者使用yarn安装：

`yarn global add xxx`

或者为项目添加插件：

`npm i --dev xxx xxx xxx`

- 在项目中使用插件来转换css

`postcss --use xxx -o main.css css/*.css`

//上面这行命令指的是，对css/*文件夹下的css文件运行xxx插件并输出到main.css中。

## （2）插件

列举以下插件：

- [Autoprefixer](https://github.com/postcss/autoprefixer) 这是一个命令行工具；通过npm安装；通过检查你的代码并自动添加前缀；根据Can I Use的规范进行添加
- [PostCSS Preset Env](https://preset-env.cssdb.org/) 帮你将最新的 CSS 语法转换成大多数浏览器都能理解的语法。
- [stylelint](https://stylelint.io/)是一个现代化 CSS 代码检查工具。它支持最新的 CSS 语法，也包括类似 CSS 的语法，例如 SCSS 

## （3）postcss、sass和less之间的区别

- Sass、Less和Stylus这些预处理器能做的，PostCSS同样也能做。
- 最大的不同是PostCSS可以只取所需，Sass和Less会给很多东西使用但不一定用得上且不能拓展。
- 在使用sass、less等，可以添加postcss插件来实现，比如添加前缀或者代码校验。
- 也有像postcss sass和precss代替sass的插件。

# 2. 了解

## （1）node.js

- 简单的说 Node.js 就是运行在服务端的 JavaScript。
- Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。

## （2）npm

- npm是随同node.js一起安装的<u>包管理工具</u>，能够解决nodejs代码部署上的很多问题。

[官网](https://www.npmjs.com/)  （ Node Package Manager）

npm由三个不同的组件组成：网站、命令行界面Command Line Interface（cli）、注册表。

当软件包无法安装或发布时，npm CLI将生成一个`npm-debug.log`文件，帮助找出问题所在。

---

**a. npm的包安装分为全局安装和本地安装两种。**

```
npm install express          # 本地安装
npm install express -g     # 全局安装
```

如果出现以下错误：

`npm err! Error: connect ECONNREFUSED 127.0.0.1:8087 `

解决办法为：

`npm config set proxy null`   //设置代理为空

**本地安装：**

- 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
- 可以通过 require() 来引入本地安装的包。

**全局安装：**

-  将安装包放在 /usr/local 下或者你 node 的安装目录。
- 可以直接在命令行里使用。

如果你希望具备两者功能，则需要在两个地方安装它或使用 npm link。

查看安装信息：

可以使用以下命令来查看所有全局安装的模块：

`npm list -g`

---

**b. npm命令**

- 创建package.json文件：

`npm init` 

- npm install安装模块：

此命令将安装软件包及其依赖的任何软件包（package）。

`npm install`（在软件包目录中，没有参数）：此命令将安装软件包及其依赖的任何软件包。

- 卸载模块：

可以使用以下命令卸载node.js模块：

`npm uninstall xxx`

卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看：

`npm ls`

- 更新模块：

`npm update xxx`

- 搜索模块：

`npm search xxx`

---

**c. 淘宝npm镜像**

国内直接使用 npm 的官方镜像是非常慢的，因此可以使用淘宝 npm镜像。

可以使用淘宝定制的 cnpm命令行工具代替默认的 npm:

`npm install -g cnpm --registry=https://registry.npm.taobao.org`

cnpm 命令安装模块：

`cnpm install [name]`

## （3）cli

命令行界面Command Line Interface（cli）

//最常见的程序是微软的cmd.exe

## （4）yarn

同npm，是包管理工具。[官网](https://yarnpkg.com/)

它可以与世界各地的其他开发人员共享自己的代码。

## （5）gulp

基于node平台发的前端自动化构建工具；

可以做一些自动化的任务，如：

- 项目上线，HTML、CSS、JS文件压缩合并
- 语法转化（es6、less...）
- 公共文件抽离
- 修改文件浏览器自动刷新
- ...

# 3. 目录结构

### （1）目录划分

- 目录结构的设计
  - src开发目录
  - dist生产（运行）目录

- 样式模块化，如：用上 less 变量

  - 一个项目可以添加多个less文件，比如var.html、util.less、normalize.less/统一的、...

### （2）文件夹划分

- 图片文件夹：img
- css文件夹：css
- js文件夹：js

### （3）目录命名

资源分成两大类：

- 源代码资源：指开发者编写的源代码，包括`js`、`html`、`css`、`template`等。
- 内容资源：指希望做为内容提供给访问者的资源，包括`图片`、`字体`、`flash`、`pdf`等。

---

- `img`: 样式类图片文件夹。不允许使用`image`、`images`、`imgs`等。

- `js`: javascript脚本文件夹。不允许使用`script`、`scripts`等。
- `css`: 样式表。 不允许使用`style`、`styles`等。
- `swf`: flash。 不允许使用`flash`等。
- `src`: 源文件目录。不允许使用`source`等。
- `dep`: 引入的第三方依赖包目录。不允许使用`lib`、`library`、`dependency`等。
- 不允许使用复数形式。如：`imgs`、`docs`是不被允许的。

### （4）文件命名

- 所有文件名统一使用小写，首页命名为`index.html` 。html内页有明显分类的，参考使用以下示例命名：

- 无明确意义的，可用page01.html、page02.html，禁止使用特殊字符，统一使用小写字母

| 专题名称           | 描述         |
| ------------------ | ------------ |
| index.html         | 引导页&首页  |
| main.html          | 首页         |
| news.html          | 咨询页       |
| newsdetail.html    | 咨询详情页   |
| raiders.html       | 攻略页       |
| raidersdetail.html | 攻略详情页   |
| download.html      | 下载页面     |
| actlist.html       | 活动列表页面 |
| video.html         | 视频         |

[参考链接](https://github.com/ecomfe/spec)

# 遇到问题

- 问题1：对于vscode中，gulp : 无法加载文件 C:\Users\Administrator\AppData\Roaming\npm\gulp.ps1，因为在此系统上禁止运行脚本

解决：[操作链接](https://blog.csdn.net/gusushantang/article/details/109389338)

- picgo中配置gulp图床失败