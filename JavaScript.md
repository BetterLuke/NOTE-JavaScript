# 如何使用forEach()方法

# 在JavaScript中，函数也是一个对象。

# 作用域

## 函数级作用域
```JavaScript
//示例1
var outsideExample = "First string";
function example() {
    var outsideExample = "Second string";
}
example();
console.log(outsideExample);
// First string

//示例2
var outsideExample = "First string";
function example() {
    outsideExample = "Second string";
}
example();
console.log(outsideExample);
//Second string
```
## 块级作用域

>块不会创建自己的作用域,比如if 语句不会创建自己的作用域。

```JavaScript
var outsideExample = "First string";
if (true) {
    var outsideExample = "Second string";
    console.log(outsideExample);
}
console.log(outsideExample);

//Second string Second string
```
第一个 console.log() 明显记录的是 "Second string”，因为它正好在我们将 outsideExample 的值设为 "Second string" 之后。那么第二个 console.log() 呢？

注意，if 语句不会创建自己的作用域。和最后一个测验不一样，在这个测验中，我们在函数中创建了一个全新的变量，if 语句没有创建新的变量。只是将 outsideExample 的值替换为 "Second string”。

所以第一次运行 console.log() 时，我们再次看到了 "Second string”。

# 函数声明语法
```JavaScript
var functionName = function() {}

和

function functionName() {}
```

JavaScript 解释器负责将你写的代码准备成机器代码，它在处理这两种函数声明时稍微有所不同，因为这是由它处理变量声明的方式造成的。

所有变量声明都将立即移到作用域的顶部。例如：

```JavaScript
var x = 5;
console.log(x); // 5
var y = 10;
等同于
var x, y; // 这行同时声明了 x 和 y。
x = 5;
console.log(x); // 5
y = 10;
```

注意，y 的声明移到了作用域的顶部。同时注意，第一行没有为 x 或 y 设定值。在 var x, y; 之后，x 和 y 都 undefined。

其他类型的变量（包括函数）也具有这一行为。如果你使用 var functionName 语法，只有函数的声明（例如 var functionName;）移到作用域的顶部。但是，如果你使用 function functionName() 语法，函数声明和定义（函数里的实际说明）移到函数作用域的顶部。
