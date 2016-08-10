# 在HTML中使用Javascript

## 使用`<script>`元素

> HTML4.01为`<script>`定义了下列6个属性：
> <br>● async：可选。表示应该立即下载脚本，但不应妨碍页面中的其他操作，比如下载其他资源或 等待加载其他脚本。只对外部脚本文件有效。
> <br>● charset：可选。表示通过src属性指定的代码的字符集。由于大多数浏览器会忽略它的值， 因此这个属性很少有人用。 
> <br>● defer：可选。示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有效。
> <br>● src：可选。表示包含要执行代码的外部文件。 
> <br>● type：可选。表示编写代码使用的脚本语言的内容类型（也称为MIME类型）。实际上，服务器在传送JavaScript文件时使用的MIME类型通常是application/x–javascript，但在type中设置这个值却可能导致脚本被忽略。此外，在非IE浏览器中还可以使用以下值：application/javascript和application/ecmasript。考虑到约定俗成和最大限度的浏览器兼容性，目前type属性的值依旧还是 text/javascript。不过，这个属性并不是必需的，如果没有指定这个属性，则其默认值仍为text/javascript。

使用`<script>`元素的方式有两种：

1. 直接在页面中嵌入Javascript代码；
2. 包含外部Javascript文件。

### 嵌入Javascript代码

在使用`<script>`元素嵌入 JavaScript 代码时，只须为`<script>`指定type属性。然后，像下面这样把JavaScript代码直接放在元素内部即可： 

```html
<script type="text/javascript">
    function say_Hi() {
        alert("Hi!");
    }
</script>
```

__包含在`<script>`元素内部的 JavaScript 代码将被从上至下依次解释。就拿前面这个例子来说，解释器会解释一个函数的定义，然后将该定义保存在自己的环境当中。__在解释器对`<script>`元素内部的所有代码求值完毕以前，页面中的其余内容都不会被浏览器加载或显示。 

__注意：__

在使用`<script>`嵌入 JavaScript 代码时，记住不要在代码中的任何地方出现"`</script>`"字符串。 例如，浏览器在加载下面所示的代码时就会产生一个错误： 

```html
<script type="text/javascript">
   function sayScript(argument) {
    alert("/<script>");
    }
</script>
```

因为按照解析嵌入式代码的规则，当浏览器遇到字符串"`</script>`"时，就会认为那是结束的`</script>`标签。而通过转义字符“/”可以解决这个问题:

```html
<script type="text/javascript">
   function sayScript(argument) {
    alert("\/<script>");
    }
</script>
```


### 引入外部Javascript文件

__1__. 包含自身域上的js文件：
```html
<script type="text/javascript" src="example.js"></script>
```

__2__. 或者包含外部域上的js文件：
```html
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js"></script>
```

与解析嵌入式JavaScript代码一样，在解析外部JavaScript文件（包括下载该文件）时，页面的处理也会暂时停止。

> 按照惯例，外部 JavaScript 文件带有.js 扩展名。但这个扩展名不是必需的，因为浏览器不会检查包含 JavaScript 的文件的扩展名。这样一来，使用 JSP、PHP 或其他服务器端语言动态生成JavaScript代码也就成为了可能。但是，服务器通常还是需要看扩展名决定为响应应用哪种MIME类型。如果不使用.js扩展名，请确保服务器能返回正确的 MIME 类型。

__注意:__

* 带有 src 属性的`<script>`元素不应该在其<script>和</script>标签之间再包含额外的JavaScript代码。如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略。 
* 无论如何包含代码，只要不存在 defer 和 async 属性，浏览器都会按照`<script>`元素在页面中出现的先后顺序对它们依次进行解析。

#### 使用引入外部js文件的优点：

* 可维护性：遍及不同HTML页面的JavaScript会造成维护问题。
* 可缓存：浏览器能够根据具体的设置缓存链接的所有外部JavaScript文件。也就是说，如果有两个页面都使用同一个文件，那么这个文件只需下载一次。因此，最终结果就是能够加快页面加载的速度。
* 适应未来：HTML和XHTML包含外部文件的语法是相同的。

## 标签的位置优化
```html
<!DOCTYPE html>
<html>
<head>
    <title>Example HTML Page</title>
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
</head>
<body>
    <!-- 这里放内容 -->
</body>
</html>
------------------------------------------------------------------------------
<!DOCTYPE html>
<html>
<head>
    <title>Example HTML Page</title>
</head>
<body>
    <!-- 这里放内容 -->
    <script type="text/javascript"  src="example1.js"></script>
    <script type="text/javascript"  src="example2.js"></script>
</body>
</html>
```

上面这段代码，前者是在`<head>`元素中包含所有JavaScript文件，意味着必须等到全部 JavaScript代码都被下载、解析和执行完成以后，才能开始呈现页面的内容（浏览器在遇到`<body>`标签时才开始呈现内容）。为了避免这个问题，现代Web应用程序一般都把全部JavaScript引用放在`<body>`元素中页面内容的后面，如下面的那段代码。

## 延迟脚本
在`<script>`元素中设置`defer="defer"`属性，相当于告诉浏览器立即下载，但延迟执行。

```html
<!DOCTYPE html>
<html>
<head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
    <script type="text/javascript" defer="defer" src="example2.js"></script>
</head>
<body>
    <!-- 这里放内容 -->
</body>
</html>
```

虽然把`<script>`元素放在了文档的`<head>`元素中，但其中包含的脚本将延迟到浏览器遇到`</html>`标签后再执行。__以防有些浏览器不支持`defer`属性，所以，把延迟脚本放在页面底部任然是最佳选择。__

__HTML5规范要求脚本按照它们出现的先后顺序执行，__因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于DOMContentLoaded事件执行。在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在DOMContentLoaded事件触发前执行，__因此最好只包含一个延迟脚本。__


## 异步脚本
在`<script>`元素中设置`async`属性，相当于不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。为此，建议异步脚本不要在加载期间修改DOM。 

```html
<!DOCTYPE html>
<html>
<head>
    <title>Example HTML Page</title>
    <script type="text/javascript" async src="example1.js"></script>
    <script type="text/javascript" async src="example2.js"></script>
</head>
<body>
    <!-- 这里放内容 -->
</body>
</html>
```

但与defer 不同的是，标记为async的脚本并不保证按照指定它们的先后顺序执行。

__异步脚本一定会在页面的load事件前执行，但可能会在DOMContentLoaded事件触发之前或之后执行。__

## `<noscript>`元素

早期浏览器都面临一个特殊的问题，即当浏览器不支持JavaScript时如何让页面平稳地退化。对这 个问题的最终解决方案就是创造一个`<noscript>`元素，用以在不支持JavaScript的浏览器中显示替代的内容。这个元素可以包含能够出现在文档`<body>`中的任何HTML元素——`<script>`元素除外。包含 在`<noscript>`元素中的内容只有在下列情况下才会显示出来：

* 浏览器不支持脚本；
* 浏览器支持脚本，但脚本被禁用。

合上述任何一个条件，浏览器都会显示`<noscript>`中的内容。而在除此之外的其他情况下，浏览器不会呈现`<noscript>`中的内容。 

DEMO：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
</head>
<body>
    <noscript>
        <p>本页面需要浏览器支持（启用）JavaScript。 </p>
    </noscript>
</body>
</html>>
```

## 小结

把JavaScript插入到HTML页面中要使用`<script>`元素。使用这个元素可以把JavaScript嵌入到HTML页面中，让脚本与标记混合在一起；也可以包含外部的JavaScript文件。而需要注意的地方有：

* 在包含外部JavaScript文件时，必须将src属性设置为指向相应文件的URL。这个文件既可以是与包含它的页面位于同一个服务器上的文件，也可以是其他任何域中的文件。
*  所有`<script>`元素都会按照它们在页面中出现的先后顺序依次被解析。在不使用defer和async属性的情况下，只有在解析完前面 `<script>`元素中的代码之后，才会开始解析后面 `<script>`元素中的代码。 
*  使用defer属性可以让脚本在文档完全呈现之后再执行。延迟脚本总是按照指定它们的顺序执行。 
*  使用async属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。不保证异步脚本按照它们在页面中出现的顺序执行。 
*  使用`<noscript>`元素可以指定在不支持脚本的浏览器中显示的替代内容。但在启用了脚本 的情况下，浏览器不会显示`<noscript>`元素中的任何内容。 