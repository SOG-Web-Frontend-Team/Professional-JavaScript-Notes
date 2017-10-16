# 第1章JavaScript简介

Kirin notes
---
JavaScript`诞生于1995年`，当时主要处理服务器端语言负责的一些`输入验证操作`，在JavaScript问世前，必须把`表单数据发送到服务器端`才确认`是否漏填或无效值`。

Netscape Navigator希望用JavaScript来解决此问题，特别在当时普遍适用电话拨号上网的年代，能在`客户端进行基本验证`是绝对令人兴奋。

从此，JavaScript逐渐成为市面上常见浏览器必备特色功能：
* 具备与浏览器窗口及其内容等几乎所有方面交互能力
* 成为一门功能全面的编程语言，处理复杂`计算、交互，闭包、匿名函数`甚至元编程特性
* 手机浏览器甚至专为残疾人设计的浏览器都支持
* 微软虽然有自己的客户端脚本VBScript，但仍然在IE早期版本加入自己对JavaScript的实现，叫JScript(基于Netscape JavaScript1.0开发，96年随IE3发布)


<br/>

### JavaScript简史
完成简单`表单验证却需频繁地与服务器交换数据`加重用户负担，走在技术前沿的Netscape着手处理`开发客户端语言`这种简单的表单验证

当时Netscape的Brendan Eich计划为95年2月发布的Netscape Navigator 2开发名为`LiveScript的脚本语言`，Netscape公司为赶在发布日期前完成LiveScript开发，与SUN公司建立开发联盟，并搭上当时热炒的Java顺风车，`临改名JavaScript`

Netscape Navigator 3又发布了JavaScript 1.1，`用户关注度屡创新高`，微软决定对其IE投入更多资源并向其发起挑战，96年微软在IE3中加入了名为`JScript`的JavaScript实现（Netscape版权问题）

自此，有两个不同的JavaScript版本，`标准化`成了一个重大问题

97年，`以JavaScript 1.1为蓝本`的建议提交到欧洲计算机制造商协会(ECMA)，指定39号技术委员会（来自Netscape Sun 微软、Borland及其他关注脚本语言发展的程序员组成）负责`标准化一种通用、跨平台、供应商中立的脚本语言语法和语义`，经过数月完成了ECMA-262——定义一种名为`ECMAScript的脚本语言标准`

<br/>

### JavaScript实现
JavaScript和ECMAScript通常`被表达为相同含义`，一个完整的JavaScript实现由三部分组成
* 核心(ECMAScript)
* 文档对象模型(DOM)
* 浏览器对象模型(BOM)

<br/>

#### ECMAScript
ECMAScript与浏览器`没有依赖关系`，浏览器只是ECMAScript实现可能的**宿主环境之一**，宿主环境不仅提供基本ECMAScript实现，还会提供`语言的扩展便于与环境对接交互`，这些扩展——DOM，则`利用ECMAScript核心类型和语法提供更多具体功能`，
还有其他宿主环境如`Node`、`Flash`

ECMAScript标准内容：`语法`、`语句`、`类型`、`关键字`、`保留字`、`操作符`、`对象`
* JavaScript实现了ECMAScript
* ActionScript也实现了ECMAScript

<br/>

##### ECMAScript版本
* 第1版本质与Netscape的JavaScript 1.1相同（删除了针对浏览器的代码与较小部分改动）
* 第2版主要是编辑加工的结果
* 第3版才是对标准的**第一次真正修改**，涉及`字符串处理`、`错误定义`、`数值输出`、`正则表达式`、`控制语句`、`trycatch异常处理`
* 第4版全面检核修订，TC39在第3版的基础上完全定义了一门新语言（强类型变量、新语言和新数据结构、真正的类和经典集成、数据交互新方式）。由于第4版跨越太大，TC39提出了名为`ECMAScript3.1的替代版本`，第4版本被放弃
* 3.1版本则变成了第5版(09年)，新功能包括`原生JSON对象`、`继承方法`、`高级属性定义`、`严格模式`

PS：ECMAScript要求`支持Unicode标准`(支持多语言开发)且应与`平台无关`

<br/>

##### 文档对象模型 DOM
是针对XML但经过扩展用于HTML`应用程序编程接口-API`，DOM把**整个页面映射成一个多层次节点结构**，通过这个文档树形图，开发人员获得控制页面内容和结构的主动权，能轻松地对节点进行CRUD操作

与此同时，IE4和Netscape4分别支持不同形式的DHTML，他们各持己见，以往只编写一个HTML页面就能在任何浏览器运行的时代结束，为了保持跨平台的天性与浏览器互相兼容，控制Netscape和微软两强制霸的局面，负责指定Web标准的W3C万维网联盟开始着手规划DOM


###### DOM级别
* **DOM Level 1** -> 1998年10月成为W3C推荐标准，DOM Level 1由两个模块组成：**`DOM Core`**和**`DOM HTML`**
    * DOM Core规定如何`映射基于XML的文档结构`，便于简化文档中任意部分的访问和操作
    * DOM HTML在DOM Core核心基础上加以扩展，添加了`针对HTML对象和方法`

**PS**：DOM并不只是针对JavaScript，很多其他语言都实现了DOM，但在浏览器中，`基于ECMAScript实现的DOM`的确已成为JavaScript这门语言的一个重要组成部分

* **DOM Level 2** -> 目标更加宽广，在原来的DOM基础上扩充了`鼠标和用户界面事件`、`范围、遍历等模块`，并且通过对象接口`增加了对CSS的支持`，开始支持XML命名空间
    * DOM 视图 (DOM View)
    * DOM 事件 (DOM Events)    
    * DOM 样式 (DOM Style)
    * DOM 遍历和范围 (DOM Traversal and Range)

* **DOM Level 3** -> 进一步扩展DOM
    * 引入以同一方式加载和保存文档方法(DOM Load and Save模块中定义)
    * 新增验证文档方法(DOM Validation模块中定义)
    * 开始支持XML 1.0规范

**PS**：DOM Level 0实际上是不存在，只是DOM历史中一个参照物，具体来说，DOM Level 0指IE4和Netscape Navigator 4`最初支持的DHTML`


###### 其他DOM标准
另外几种语言还发布了只针对自己的DOM标准，下面几种语言基于XML，每种语言的DOM标准都添加了与特定语言相关的新方法和新接口
* SVG
* MathML
* SMIL


<br>

##### 浏览器对象模型BOM
IE3和Netscape3有一个共同特色，就是支持`可访问和操作浏览器窗口`的浏览器对象模型(BOM)，通过BOM，开发人员可以`控制浏览器显示页面外`的部分，HTML5后才将BOM之前没有标准规范的问题解决

BOM只处理浏览器窗口和框架，但习惯上把所有针对浏览器的JavaScript扩展算作BOM一部分，下面是这样的扩展
* 弹出新窗口
* 移动、缩放、关闭浏览器窗口
* 浏览器详细信息的navigator对象
* 浏览器加载页面信息的location对象
* 用户显示器分辨率详细信息的screen对象
* cookie支持
* XMLHttpRequest和IE的ActiveXObject这样的自定义对象


**PS**：Web浏览器对ECMAScript、DOM和BOM支持请查原书


<br>

#### JavaScript版本
作为Netscape继承人的Mozilla公司，是目前唯一还在沿用最初JavaScript版本编号序列的浏览器开发商，大多数浏览器提及对JavaScript支持情况时，一般以`ECMAScript兼容性和DOM支持情况为准`
[有关JavaScript版本历史记录的信息](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/New_in_JavaScript)


<br>

### 小结
JavaScript是一种**专为与网页交互而设计的脚本语言**，由三个部分组成
* `ECMAScript`：由ECMA-262定义，提供`核心语言功能`
* `DOM`：提供`访问和操作网页内容方法和接口`
* `BOM`：提供`与浏览器交互的方法和接口`

当前主流浏览器对这三个部分都有不同程度的支持
* ECMAScript方面特别是第3版的支持程度，对第5版的支持程度越来越高
* DOM的支持则彼此相差较多
* 对正式纳入HTML5标准的BOM，尽管浏览器都实现了总所周知的共同特性，但其他特性还是会因浏览器而异


<br><br>