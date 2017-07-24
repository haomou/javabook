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
| &lt;form&gt;表单、&lt;input&gt;输入 | ![](/assets/t5.png) | ![](/assets/t4.png) |
| &lt;textarea&gt;文本输入域 | &lt;textarea rows="3" cols="20"&gt;填写内容&lt;/textarea&gt; | 定义多行的文本输入控件，在文本输入区内的文本行间，用“%OD%OA”（回车/换行）进行分隔。textarea为表单元素。 |
| &lt;label&gt;标记 | &lt;label for="male"&gt;Male&lt;label&gt;&lt;input type="radio" name="sex" id="male" /&gt; | 为input元素定义标注（标记），不会向用户呈现任何特殊效果。for属性指定相关元素id。 |
| &lt;fieldset&gt;分组、&lt;legend&gt;组标题 | ![](/assets/t6.png) | ![](/assets/t7.png)显示效果如上，将表单内的相关元素分组，legend标签指定组标题。 |
| &lt;select&gt;选择、&lt;option&gt;选项、&lt;optgroup&gt;选项组标签 | ![](/assets/t9.png) | ![](/assets/t8.png)显示效果如上图，select标签可根据multiple属性创建单选或多选菜单，option标签指定选项，optgroup标签指定选项组的组标题。 |
| &lt;button&gt;按钮 | &lt;button type="button"&gt;Click Me!&lt;/button&gt; | 该标签定义一个按钮，与input不同的是，该元素内部可以放置内容，比如文本或图像。 |
| &lt;!--...--&gt; | &lt;!-- &lt;input type="text" /&gt; --&gt; | 注释标签用来在源文档中插入注释。注释会被浏览器忽略。 |
| &lt;!DOCTYPE&gt; | &lt;!DOCTYPE html&gt; | 声明位于文档中的最前面的位置，处于&lt;html&gt;标签之前。此标签可告知浏览器文档使用哪种HTML或XHTML规范。该标签可声明三种DTD类型，分别表示严格版本、过度版本以及基于框架的HTML文档。 |
| &lt;style&gt;样式 | &lt;style type="text/css" &gt;h1{color: red;} p{color: blue}&lt;/style&gt; | 该标签用于为HTML定义样式信，规定在浏览器中如何呈现HTML文档。type属性是必须的，唯一可能的值是“text/css”。style元素位于head部分中。 |
| &lt;script&gt;标签 | &lt;script type="text/javascript"&gt;document.write\("Hello World!"\)&lt;/script&gt; | 该标签用于定义客户端脚本，biruJavascript。script元素既可以包含脚本语句，也可以通过src属性指向外部脚本文件。 |

 以上介绍了编写HTML网页中比较常用的标签和简单用法，另外HTML标签可以拥有属性，属性提供了有关HTML元素的更多的信息。这些属性主要分为两种：样式属性和事件属性，关于样式属性的具体使用建议读者查阅HTML手册，或则到W3School查阅相关信息，这里就不在赘述，下面介绍一下HTML中的事件属性。

