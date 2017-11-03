### 2.1 <script>元素
HTML4.01为`<script>`定义了下列6 个属性。
* async：可选。表示应该立即下载脚本，但不应妨碍页面中的其他操作，比如下载其他资源或等待加载其他脚本。只对外部脚本文件有效。
* charset：可选。表示通过src 属性指定的代码的字符集。由于大多数浏览器会忽略它的值，因此这个属性很少有人用。
* defer：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有
效。IE7 及更早版本对嵌入脚本也支持这个属性。
* language：已废弃。原来用于表示编写代码使用的脚本语言（如JavaScript、JavaScript1.2
或VBScript）。大多数浏览器会忽略这个属性，因此也没有必要再用了。
* src：可选。表示包含要执行代码的外部文件。
* type：可选。可以看成是language 的替代属性；表示编写代码使用的脚本语言的内容类型（也称为MIME 类型）。虽然text/javascript 和text/ecmascript 都已经不被推荐使用，但人们一直以来使用的都还是text/javascript。实际上，服务器在传送JavaScript 文件时使用的MIME 类型通常是application/x–javascript，但在type 中设置这个值却可能导致脚本被忽略。另外，在非IE浏览器中还可以使用以下值：application/javascript 和application/ecmascript。考虑到约定俗成和最大限度的浏览器兼容性，目前type 属性的值依旧还是text/javascript。不过，这个属性并不是必需的，如果没有指定这个属性，则其默认值仍为text/javascript。

<br>
包含在`<script>`元素内部的JavaScript代码将被从上至下依次解释。就拿前面这个例子来说，解释器会解释一个函数的定义，然后将该定义保存在自己的环境当中。在解释器对<script>元素内部的所有代码求值完毕以前，页面中的其余内容都不会被浏览器加载或显示。
在使用`<script>`嵌入JavaScript代码时，记住不要在代码中的任何地方出现`"</script>"`字符串。例如，浏览器在加载下面所示的代码时就会产生一个错误：
```
<script type="text/javascript">
function sayScript(){
alert("</script>");
}
</script>
```
<br><br>
因为按照解析嵌入式代码的规则，当浏览器遇到字符串`"</script>"`时，就会认为那是结束的
`</script>`标签。而通过转义字符“/”可以解决这个问题，例如：
```
<script type="text/javascript">
function sayScript(){
alert("<\/script>");
}
</script>
```