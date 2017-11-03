Echo notes 
---
如何做到让 JavaScript 既能与 HTML页面共存，又不影响那些页面在其他浏览器中的呈现效果，为Web增加统一的脚本支持：JavaScript。

### 2.1 <script>元素
使用`<script>`元素向 HTML 页面中插入 JavaScript ，这个元素被加入到正式的 HTML 规范中。定义了下列6个属性：
* async：可选。立即下载脚本，但不应妨碍页面中的其他操作，只对外部脚本文件有效。   
* charset：可选。表示通过 src 属性指定的代码的字符集。会被大多数浏览器忽略，因此很少有人用
* defer：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有效。
* language：已废弃。
* src：可选。表示包含要执行代码的外部文件。
* type：可选。表示编写代码使用的脚本语言的内容类型（也称为 MIME 类型），可以看成是 language 的替代属性。考虑到约定俗成和最大限度的浏览器兼容性，通常使用text/javascript，还有以下值：text/ecmascript、application/x–javascript、application/javascript、application/ecmascript

###### 使用<script>元素方式有两种：
* `直接在页面中嵌入 JavaScript 代码`
    把JavaScript代码直接放在元素内部即可，代码将被从上至下依次解释。
```
<script type="text/javascript">
    function sayHi(){
        alert("Hi!");
    }
</script>
```
解释器会解释一个函数的定义，然后将该定义保存在自己的环境当中。在解释器对<script>元素内部的所有代码求值完毕以前，页面中的其余内容都不会被浏览器加载或显示。不要在代码中的任何地方出现"</script>"字符串，按照解析嵌入式代码的规则，当浏览器遇到字符串"</script>"时，就会认为那是结束的</script>标签，通过转义字符“/”可以解决这个问题：
```
<script type="text/javascript">
    function sayHi(){
        alert("<\/script>"); 
    }
</script>
```
* `包含外部 JavaScript文件，src 属性就是必需的`
```
<script type="text/javascript" src="example.js"></script>  
```
外部文件只须包含通常要放在开始的<script>和结束的</script>之间的那些 JavaScript 代码即可。在解析外部JavaScript文件时，页面的处理也会暂时停止。在 XHTML 文档中，也可以省略前面示例代码中结束的</script>标签 ，但不能在 HTML 文档使用这种语法，原因是这种语法不符合 HTML 规范（尤其是IE）。
```
<script type="text/javascript" src="example.js" />   
```
###### 要注意的是，带有 src 属性的<script>元素不应该在其<script>和</script>标签之间再包含额外的 JavaScript 代码。如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略 。
通过<script>元素的 src 属性可以是指向当前 HTML 页面所在域之外的某个域中的完整 URL ：
```
<script type="text/javascript" src="http://www.somewhere.com/afile.js"></script>
```
无论如何包含代码，只要不存在 defer 和 async 属性，浏览器都会按照<script>元素在页面中出现的先后顺序对它们依次进行解析。  


##### 2.1.1 标签的位置 
所有<script>元素都应该放在页面的<head>元素中，目的是把所有外部文件（包括 CSS 文件和 JavaScript 文件）的引用都放在相同的地方。 在文档的<head>元素中包含所有JavaScript文件，由于浏览器解析机制，会导致在呈现页面时出现明显的延迟，延迟期间窗口一片空白。为了避免这个问题，一般把JavaScript引用放在<body>元素中页面内容的后面，这样，在解析JavaScript代码之前，页面内容将完全呈现在浏览器中，例如：
```
<!DOCTYPE html>
<html>
<head>
<title>Example HTML Page</title>
</head>
<body>
<!-- 此处存放内容 -->
<script type="text/javascript" src="example1.js"></script>
<script type="text/javascript" src="example2.js"></script>
</body>
</html>
```

##### 2.1.2 延迟脚本
HTML 4.01 为<script>标签定义了 defer 属性，用途是脚本会被延迟到整个页面都解析完毕后再运行，设置了defer属性，等于告诉浏览器立即下载，但延迟执行：
```
<!DOCTYPE html>
<html>
<head> 
<title>Example HTML Page</title>
<script type="text/javascript" defer="defer" src="example1.js"></script>
<script type="text/javascript" defer="defer" src="example2.js"></script>
</head>
<body>
<!-- 此处存放内容 -->
</body>
</html>
```
在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoaded 事件触发前执行，因此最好只包含一个延迟脚本。  

##### 2.1.3 异步脚本
HTML5 为<script>元素定义了 async 属性， 和defer属性类似，用于改变处理脚本的行为，不同的是，标记为 async 的脚本并不保证按照指定它们的先后顺序执行，因此，确保两者之间互不依赖非常重要，建议异步脚本不要在加载期间修改 DOM。

##### 2.1.4 在XHTML中的用法  
XHTML：可扩展超文本标记语言，是将 HTML 作为XML 的应用而重新定义的一个标准。编写 XHTML 代码的规则要比编写 HTML 严格得多，例如在代码中使用小于号（<）或大于号（>），在XHTML中作为标签来讲，小于号后面不能跟空格，所以会导致语法错误：
```
<script type="text/javascript">
function compare(a, b) {
   if (a < b) {
       alert("A is less than B");
   }
}
</script>  
```
有两种方法可以避免此类错误：
a)&nbsp;&nbsp;用相应的 HTML 实体（`&lt;`）替换，虽然可以正常运行，但代码会变得不好理解：
```
<script type="text/javascript">
function compare(a, b) {
   if (a &lt; b) {
       alert("A is less than B");
   }
}
</script>  
```
b)&nbsp;&nbsp;用一个 CData 片段来包含 JavaScript 代码，在 XHTML（XML）中， CData 片段是文档中的一个特殊区域，这个区域中可以包含不需要解析的任意格式的文本内容。为了格式兼容，可使用JavaScript 注释将CData 标记注释掉：
```
<script type="text/javascript"> 
//<![CDATA[
function compare(a, b) {
   if (a < b) {
       alert("A is less than B");
   }
}
//]]>
</script>  
```

##### 2.1.5 不推荐使用的语法  
由于要对<script>这个元素应用特殊的解析规则，为了让不支持<script>元素的浏览器能够隐藏嵌入的JavaScript 代码，解决方案是把 JavaScript 代码包含在一个 HTML 注释中：
```
<script>
<!--
function sayHi(){
   alert("Hi!");
}
//-->
</script>  
```

### 2.2 嵌入代码与外部文件
一般认为最好的做法是尽可能使用外部文件来包含 JavaScript 代码，有如下优点：
* 可维护性：遍及不同 HTML 页面的 JavaScript 会造成维护问题。
* 可缓存：浏览器能够根据具体的设置缓存链接的所有外部 JavaScript 文件。
* 适应未来：通过外部文件来包含 JavaScript 无须使用前面提到 XHTML 或注释 hack。 

### 2.3 文档模式
文档模式是通过使用文档类型（doctype）切换实现的。
* `混杂模式`：  会让 IE 的行为与（包含非标准特性的）IE5 相同
* `标准模式`：  让 IE 的行为更接近标准行为 
* `准标准模式`：  这种模式下的浏览器特性有很多都是符合标准的，不标准的地方主要体现在处理图片间隙的时候。
如果在文档开始处没有发现文档类型声明，则所有浏览器都会默认开启混杂模式，这种模式下不同浏览器的行为差异很大，需要额外使用hack技术，所以不推荐这种做法。
对于标准模式，可通过以下文档类型来开启：
* HTML 4.01 严格型
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd"> 
```
* XHTML 1.0 严格型
```
<!DOCTYPE html PUBLIC
"-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">  
```
* HTML 5
```
<!DOCTYPE html>  
```
准标准模式与标准模式非常接近，差异几乎可以忽略不计。  

### 2.4 <noscript>元素 
为了解决早期浏览器不支持 JavaScript 时如何让页面平稳地退化问题，创造一个<noscript>元素，用以在不支持 JavaScript 的浏览器中显示替代的内容。可以包含能够出现在文档<body>中的任何 HTML 元素——<script>元素除外。  在下列情况才会显示<noscript>中的内容：
* 浏览器不支持脚本；
* 浏览器支持脚本，但脚本被禁用。
```
<html>
<head>
<title>Example HTML Page</title>
<script type="text/javascript" defer="defer" src="example1.js"></script>
<script type="text/javascript" defer="defer" src="example2.js"></script>
</head>
<body>
<noscript>
<p>本页面需要浏览器支持（启用） JavaScript。
</noscript>
</body>
</html>  
```

### 2.5 小结
把 JavaScript 插入到 HTML 页面中要使用<script>元素。使用这个元素可以把 JavaScript 嵌入到HTML 页面中，让脚本与标记混合在一起；也可以包含外部的 JavaScript 文件。  注意：
* 在包含外部 JavaScript 文件时，必须将 src 属性设置为指向相应文件的 URL。
* 所有<script>元素都会按照它们在页面中出现的先后顺序依次被解析。
* 一般应该把<script>元素放在页面最后，即主要内容后面， </body>标签前面。
* 使用 defer 属性可以让脚本在文档完全呈现之后再执行。
* 使用 async 属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。
* 使用<noscript>元素可以指定在不支持脚本的浏览器中显示的替代内容，在启用了脚本的情况下，浏览器不会显示<noscript>元素中的任何内容。


