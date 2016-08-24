#CSS-DOM

## 三位一体的网页

#### 结构层
网页的结构层（structure layer）由HTML或XHTML之类的标记语言负责创建。标签（tag），对网页内容的语义含义做出了描述。但这些标签并不包含任何关于内容如何显示的信息。

#### 表示层
表示层（presentation layer）由CSS负责完成。CSS描述页面内容如何呈现。

#### 上行为层

行为层（behavior layer）负责内容如何响应事件这一问题。这是JavaScript语言和DOM主宰的领域。

## 获取样式

### 使用DOM style属性

>使用DOM style属性,只可以获取内嵌样式的样式属性信息。

使用元素的某样式属性：

```javascript
element.style.attribution
```

这里注意如果引用中间带减号的CSS属性时，DOM要求使用驼峰命名法。比如CSS属性`font-family`对应DOM属性`fontFamily`；CSS属性`backgroud-color`对应DOM属性`backgroudColor`

>原因在于减号符号在javascript中被解析成计算符，会进行减法运算。

绝大部分样式属性的返回值与它们的设置值都采用同样的计量单位。但对于颜色属性的表示，也有一例外：

```
<p style="color: #999999;"></p>
alert("The corlor is " + para.style.color); //显示：“The corlor is rgb(153,153,153)”
--------------------------------------------------------------------------------------
<p style="color: gray;"></p>
alert("The corlor is " + para.style.color); //显示：“The corlor is gray”
```


