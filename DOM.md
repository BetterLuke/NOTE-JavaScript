# DOM

## 认识什么是DOM

DOM（Document Object Model）把一份文档对象表示为树的模型，更形象的说，是家谱树。

对于这样一份html文档：
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>Shopping List</title>
    <link rel="stylesheet" type="text/css" href="style.css">
</head>

<body>
    <h1> What do u buy? </h1>
    <p title="a gentle reminder">Don't forget to buy this stuff.</p>
    <ul id="purchases">
        <li class="sale">A tin of beans</li>
        <li class="sale">Cheese</li>
        <li class="sale important">Milk</li>
    </ul>
    <script type="text/javascript" src="examle.js"></script>
</body>

</html>
```

DOM树的结构模型：

![DOM树](resource/img/DOM树.png)

## 节点

__树是由节点构成的__，既然DOM把文档对象转为了树模型，那么DOM树由以下三种节点构成：

* 元素结点（element node）
* 文本结点（text node）
* 属性结点（attribute node）

![](resource/img/DOM树的节点.png)

## 获取元素

*  getElementById()
*  getElementByTagName()
*  getElementByClassName()

### getElementById()
文档中每一个元素都是一个对象，运用该方法，可以返回一个与那个有着给定id属性值的元素节点对应的对象。
```javascript
var element_object = document.getElementById("ID_name");
alert(typeof element_object); //object
```

### getElementsByTagName()
该方法返回一个对象数组，即使这个标签只有一个元素，该方法也返回一个数组，只不过数组的长度为1。

```javascript
var items = document.getElementsByTagName("li");
for (var i = items.length - 1; i >= 0; i--) {
     alert(typeof items[i]);
}
/* 运行结果是弹出3次提示框：object */
```

使用技巧：`getElementsByTagName()`方法中使用通配符获取文档中的所有元素对象:

```javascript
document.getElementsByTagName("*"); //返回的数组将包含文档中的所有元素对象
```

### getElementsByClassName()

这个方法通过class属性中的类名来访问元素，返回一个具有相同类名的元素的数组。不过，此方法仅在支持HTML5的浏览器中使用。

下面这一行代码返回的就是一个数组，其中半酣类名为“sale”的所有元素：

```javascript
document.getElementsByClassName("sale");
```

若要查找带有多个类名的元素，只要在字符串参数中用空格分隔类名即可：

```javascript
document.getElementsByClassName("sale important"); //与类名的顺序无关，就算元素带有更多类名也没关系
```

为了使新老浏览器都能使用本方法，需要自己实现`getElementsByClassName()`:

```javascript
/* 此方法不适用于多个类名 */
/* node表示DOM树搜索的起点，classname是要搜索的类名 */
function getElementsByClassName(node, classname) {
    if(node.getElementsByClassName){
        //浏览器支持此方法就使用现有方法
        return node.getElementsByClassName(classname)
    } else {
        var results = new Array();
        var elems = node.getElementsByTagName("*");
        for(var i = 0; i < elems.length; i++) {
            if(elems[i].indexOf(classname) != -1){
                results[results.length] = elems[i];
            }
        }
    }
    return results;
} 
```

使用这个方法，模拟前面取得购物列表的操作：
```javascript
var shopping = document.getElementById("purchases");
var sales = getElementsByClassName(shopping,"sales");
```


## 获取和设置属性

* getAttribute()
* setAttribute()

### getAttribute()

```javascript
object.getAttribute(attribute);
```

### setAttribute() 

```javascript
object.setAttribute(attribute, value);
```

`setAttribute()`做出的修改不会反映在文档本身的源代码里。

__DOM的工作模式：__先加载文档的静态内容，再动态刷新，动态刷新不影响文档的静态内容。这正是DOM的真正威力：对页面内容进行刷新却不需要在浏览器里刷新页面。

```javascript
var paras = document.getElementsByTagName("p");
for(var i=0; i < paras.length; i++) {
    var tittle_text = paras[i].getAttribute("title");
    if(tittle_text) {
        paras[i].setAttribute("title","New tittle!");
        alert(paras[i].getAttribute("title"));
    }
}
/* 运行结果：New tittle! */
```


## 有关节点属性的扩展

### childNodes属性

在一颗节点树上，childNodes属性可以用来获取任何一个元素的所有子元素，它是一个包含这个元素全部子元素的数组：

```javascript
element.childNodes
```

### nodeType属性

* __元素节点__的nodeType属性值是1
* __属性节点__的nodeType属性值是2
* __文本节点__的nodeType属性值是3

### nodeValue属性
假设改变一个p标签的文本，代码：

```javascript
var test = document.getElementByTagName("p")[0];
text.firstChild.nodeValue = "new text"
```

### firstChild和lastChild属性

用以提高代码的可读性，
```
node.childNodes[0] <==> node.firstChild;
node.lastNodes[node.childNodes.length-1] <==> node.lastChild; 
```




