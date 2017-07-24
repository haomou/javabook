## 9.3 HTML与HTML5

这里先不急着介绍如何用JAVA开发 WEB 程序，而是介绍最基础的HTML（超文本标记语言），这是开发WEB页面的基础，一般配合JavaScript使用可以开发出绚丽多彩的页面。

HTML语言不是很复杂，但功能强大，支持不同数据格式的文件镶入， 这也是WWW盛行的原因之一，其主要特点如下：

1. 简易性，HTML版本升级采用超集方式，从而更加灵活方便。 
2. 可扩展性，HTML语言的广泛应用带来了加强功能，增加标识符等要求，HTML采取子类元素的方式，为系统扩展带来保证。
3. 平台无关性，无论你使用Windows还是Linux又或是MAC操作 系统，只要有浏览器，就可以使用HTML。

   下面先给出一个HTML页面示例代码：

```
<html>
    <head>
        <title>html 示例</title>
    </head>
    <body>
        <h1>My First Heading</h1>
        <p>My first paragraph.</p>
    </body>
</html>
```

上面示例中的每个元素称为HTML标签，其特点如下：

* HTML标签是由尖括号包围的关键词，比如
* HTML标签通常是成对出现的，比如&lt;b&gt; 和 &lt;/b&gt; 
* 标签对中的第一个标签是开始标签，第二个标签是结束标签，开始和结束标签也被称为开放标签和闭合标签

Web浏览器的作用是读取HTML文档，并以网页的形式显示出它们 。 浏览器不会显示HTML标签，而是使用标签来解释页面的内容。 编辑HTML网页文件只需要使用文本编辑器就行了，保存时后缀名保存为.htm或者.html。下面介绍一些HTML基本标签，如下表9-1所示。

**表 9-1 HTML常用标签**

| HTML标签 | 示例 | 说明 |
| :--- | :--- | :--- |
| &lt;h1&gt; - &lt;h6&gt; 1-6 号标题 | &lt;h1&gt;This is a heading&lt;/h1&gt;、&lt;h2&gt;This is a heading&lt;/h2&gt;、&lt;h3&gt;This is a heading&lt;/h3&gt; | 标题（Heading）标签，分1-6个级别 |
| &lt;p&gt;段落 | &lt;p&gt;This is a paragraph.&lt;/p&gt; | 段落标签 |
| &lt;a&gt;链接 | &lt;a href="www.taobao.com"&gt;淘宝&lt;/a&gt; | 使用href属性指定URL;使用name/id属性创建锚 |
| &lt;img&gt;图像 | &lt;img src="a.jpg" width="10" height="14" /&gt; | 图像标签，src 指定图像 URL |
| &lt;table&gt;表、&lt;tr&gt;行、&lt;td&gt;列、&lt;th&gt;表头 | &lt;table border="1"&gt;&lt;tr&gt;&lt;td&gt;row1,cell1&lt;/td&gt;&lt;/tr&gt;&lt;/table&gt; | 定义表格。每个表格均有若干行（由&lt;tr&gt;标签定义），每行被分割为若干单元格（由&lt;td&gt;标签定义）。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。 |
| &lt;ul&gt;列表、&lt;li&gt;表项 | &lt;ul&gt;&lt;li&gt;Coffee&lt;/li&gt;&lt;li&gt;Milk&lt;/li&gt;&lt;/ul&gt; | ![](/assets/t1.png)显示结果如上，无序列表始于&lt;ul&gt;标签。每个列表项始于&lt;li&gt;。 |
| &lt;ol&gt;列表、&lt;li&gt;表项 | &lt;ol&gt;&lt;li&gt;Coffee&lt;/li&gt;&lt;li&gt;Milk&lt;/li&gt;&lt;/ol&gt; | ![](/assets/t2.png)显示结果如上，此为有序列表标签。 |
| &lt;dl&gt;自定义列表、&lt;dt&gt;列表项、&lt;dd&gt;列表项注释 | &lt;dl&gt;&lt;dt&gt;Coffee&lt;/dt&gt;&lt;dd&gt;Black hot drink&lt;dt&gt;Milk&lt;/dt&gt;&lt;dd&gt;White cold drink&lt;/dd&gt;&lt;/dl&gt; | ![](/assets/t3.png)显示结果如上，自定义列表不仅仅是一列项目，而是项目及其注释的集合。 |
| &lt;form&gt;表单、&lt;input&gt;输入 |  | ![](/assets/t4.png) |
|  |  |  |



