# 认识一门新的语言——Javascript

## HTML,XML,XHTML之间有什么不同？
* HTML，超文本标记语言，是语法较为松散的、不严格的Web语言；
* XML，可扩展标记语言，主要用于存储数据和结构，可扩展；
* XHTML，可扩展超文本标记语言，基于XML，作用与HTML类似，但语法更严格。


## 什么是MIME类型（MIME Type）？

> 多用途互联网邮件扩展（MIME，Multipurpose Internet Mail Extensions）是一个互联网标准，它扩展了电子邮件标准，使其能够支援：
<br>1.非ASCII字符文本；
<br>2.非文本格式附件（二进制、声音、图像等）；
<br>3.由多部分（multiple parts）组成的消息体；
<br>4.包含非ASCII字符的头信息（Header information）。
<br>——WIKI

首先，要了解浏览器是如何处理内容的。在浏览器中显示的内容有 HTML、有 XML、有 GIF、还有 Flash ……那么，浏览器是如何区分它们，决定什么内容用什么形式来显示呢？__答案是 MIME Type，也就是该资源的媒体类型。__

媒体类型通常是通过 HTTP 协议，由 Web 服务器告知浏览器的，更准确地说，是通过 Content-Type 来表示的，例如:

```
Content-Type: text/HTML
```

表示内容是 text/HTML 类型，也就是超文本文件。为什么是“text/HTML”而不是“HTML/text”或者别的什么？__MIME Type 不是个人指定的，是经过 ietf 组织协商，以 RFC 的形式作为建议的标准发布在网上的，__大多数的 Web服务器和用户代理都会支持这个规范 (顺便说一句，Email 附件的类型也是通过 MIME Type 指定的)。

通常只有一些在互联网上获得广泛应用的格式才会获得一个 MIME Type，如果是某个客户端自己定义的格式，一般只能以`application/x-`开头。

XHTML 正是一个获得广泛应用的格式，因此，在 RFC 3236 中，说明了 XHTML格式文件的 MIME Type 应该是`application/xHTML+XML。`

当然，处理本地的文件，在没有人告诉浏览器某个文件的 MIME Type的情况下，浏览器也会做一些默认的处理，这可能和你在操作系统中给文件配置的 MIME Type 有关。比如在 Windows下，打开注册表的`HKEY_LOCAL_MACHINESOFTWAREClassesMIMEDatabaseContentTyp`主键，可以看到所有 MIME Type 的配置信息。


