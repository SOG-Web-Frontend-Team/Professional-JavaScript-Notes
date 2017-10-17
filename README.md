Evan notes
---

### JavaScript实现
JavaScript和ECMAScript通常`被表达为相同含义`，一个完整的JavaScript实现由三部分组成

* 核心(ECMAScript)
* 文档对象模型(DOM)
* 浏览器对象模型(BOM)

<br />

#### ECMAScript
ECMAScript与浏览器`没有依赖关系`，浏览器只是ECMAScript实现可能的**宿主环境之一**，宿主环境不仅提供基本ECMAScript实现，还会提供`语言的扩展便于与环境对接交互`，这些扩展——DOM，则`利用ECMAScript核心类型和语法提供更多具体功能`，
还有其他宿主环境如`Node`、`Flash`

ECMAScript标准内容：`语法`、`语句`、`类型`、`关键字`、`保留字`、`操作符`、`对象`
* JavaScript实现了ECMAScript
* ActionScript也实现了ECMAScript

<br />

##### 文档对象模型 DOM
是针对XML但经过扩展用于HTML`应用程序编程接口-API`，DOM把**整个页面映射成一个多层次节点结构**，通过这个文档树形图，开发人员获得控制页面内容和结构的主动权，能轻松地对节点进行CRUD操作

<br />

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

<br>

### 小结
JavaScript是一种**专为与网页交互而设计的脚本语言**，由三个部分组成
* `ECMAScript`：由ECMA-262定义，提供`核心语言功能`
* `DOM`：提供`访问和操作网页内容方法和接口`
* `BOM`：提供`与浏览器交互的方法和接口`