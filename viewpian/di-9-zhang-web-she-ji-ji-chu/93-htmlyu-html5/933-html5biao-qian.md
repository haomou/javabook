### 9.3.3 HTML5标签

HTML5中有一些比较特殊的标签与属性需要注意一下，如下表9-7所示。

** 表9-7 HTML5特殊标签及属性**

| **标签** | **说明** |
| :--- | :--- |
| &lt;!DOCTYPE&gt; | HTML 4.01中的doctype需要对DTD进行引用，因为HTML 4.01基于SGML。而HTML5不急于SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为。 |
| &lt;a&gt; | &lt;a&gt;是超链接，若没有href属性，它仅仅是超链接的一个占位符。 |
| &lt;style&gt; | 制定样式表，新属性scoped，若使用“scoped”属性，其所规定的样式只能应用到style元素的父元素及其子元素 |
| **标准属性** | **说明** |
| contextmenu | 值为menu元素的id，目前尚未被支持，主要定义右键显示内容 |
| draggable | 值为true、false、auto，规定该元素是否可被拖动 |



