# 编码，测试，优化

>首先，需要理顺页面结构，可以从设计稿入手，将页面上的内容划分为多个方框，然后开始添加标记，例如某段文本是标题，就为其打上标题标记，然后考虑方框的大小应该有多大，然后要确定这些方框在屏幕中的位置。
完成总体布局以后，即可着手处理细节，不断优化调整，直到页面与设计手稿一致。

1. Look for natural boxes —— 寻找页面内容的排列特征,网页上的一切都是方框组成，因此需要寻找那些显而易见的方框。
2. Look for repeated styles & semantic elements —— 然后寻找重复出现的样式和语义元素，例如h2应该是页面上尺寸第二大的标题，考虑如何将其与HTML元素关联。
3. Writ HTML code.
4. Apply styles.

>从页面的最大的元素到最小的元素，修正各种小问题，在其他浏览器中查看网站，调整窗口大小。

# 媒体查询

```css
@media only screen and (max-width: 300px) {
  ...
}
```

* only: 表示兼容旧的浏览器设备
* screen 适用所有屏幕类型，如果这里是print是指打印时才会生效的样式。
* and 逻辑符

[使用设备模式模拟移动设备](http://www.css88.com/doc/chrome-devtools/device-mode/)

# CSS重设

使用normalize.css

```css

```
