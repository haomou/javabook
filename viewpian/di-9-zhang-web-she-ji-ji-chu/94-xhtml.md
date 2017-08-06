## 9.4 XHTML

XHTML 是什么？

* XHTML指可扩展超文本标签语言（EXtensible HyperText Markup Language）。 
* XHTML的目标是取代HTML。
* XHTML与HTML 4.01几乎是相同的。 
* XHTML是更严格更纯净的HTML版本。 
* XHTML是作为一种XML应用被重新定义的HTML。 
* XHTML是一个W3C标准。

通过上一章的学习，我们已经可以编写自己的HTML网页了，很多情况你会发现：可能由于疏忽大意，你写完一个标签比如&lt;p&gt;而忘记写闭合标签&lt;/p&gt;了，然而在比较主流的浏览器中预览页面的时候并没有出现任 何异样，换一些浏览器则效果差距较大。同样我们一般认为互联网上许多 网页都包含着类似的比较杂乱的代码，为了让程序员写出具有良好结构的HTML文档，我们把HTML与 XML的各自长处加以结合，就得到了XHTML。

XHTML要求的严格之处在于：

* XHTML 元素必须被正确地嵌套。 
* XHTML 元素必须被关闭，可以使用类似的结束标签，建议在于"/"符号前添加一个额外的空格，以使你的XHTML与当今的浏览器相兼容。 
* 标签名必须用小写字母。 
* XHTML文档必须拥有根元素。 
* 属性名称必须小写。 
* 属性值必须加引号。 
* 属性不能简写。 
* 用Id属性代替name属性，HTML 4.01针对下列元素定义name属性：a, applet, frame, iframe, img, 和map。在XHTML中不鼓励使 用name属性，应该使用id取而代之。
* XHTML DTD定义了强制使用的HTML元素，所有XHTML文档必须进行文件类型声明（DOCTYPE declaration）。在XHTML文档中必须存在html、head、body元素，而title元素必须位于在head元素中。

 给出一个XHTML示例代码如下：

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>test</title>
</head>
<body>
    <p>a simple paragraph</p>
</body>
</html>
```

**注意两点**

1.&lt;!DOCTYPE&gt;声明位于文档中的最前面的位置，处于标签之前。此标签可告知浏览器文档使用哪种HTML或XHTML规范。该标签可声明三种 DTD类型，分别表示严格版本、过渡版本以及基于框架的HTML文档，该标签不需要借宿标签。以下面这个&lt;!DOCTYPE&gt;标签为例：

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

在上面的声明中，声明了文档的根元素是html，它在公共标识符被定义为 "-//W3C//DTD XHTML 1.0 Strict//EN "的DTD中进行了定义。浏览器将明白如何寻找匹配此公共标识符的DTD，如果找不到，浏览器将使用公共标识符后面的URL作为寻找DTD的位置。

HTML 4.01规定了三种文档类型：Strict、Transitional以及Frameset。

a. HTML Strict DTD

如果您需要干净的标记，免于表现层的混乱，请使用此类型。请与层叠样式表（CSS）配合使用：

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

b. HTML Transitional DTD

Transitional DTD可包含W3C所期望移入样式表的呈现属性和元素。 如果您的读者使用了不支持层叠样式表（CSS）的浏览器以至于您不得不使用HTML的呈现特性时，请使用此类型：

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

c. Frameset DTD

 Frameset DTD应当被用于带有框架的文档。除frameset元素取代了body元素之外，Frameset DTD等同于Transitional DTD：

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```



XHTML 1.0规定了三种XML文档类型：Strict、Transitional以及 Frameset。

a. XHTML Strict DTD

如果您需要干净的标记，免于表现层的混乱，请使用此类型。请与层叠样式表（CSS）配合使用：

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

b. XHTML Transitional DTD

Transitional DTD可包含W3C所期望移入样式表的呈现属性和元素。 如果您的读者使用了不支持层叠样式表（CSS）的浏览器以至于您不得不使用XHTML的呈现特性时，请使用此类型：

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

c. XHTML Frameset DTD

当您希望使用框架时，请使用此DTD！

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

如需检查你是否编写了带有正确DTD的合法XHTML文档，您可以把您的XHTML页面链接到一个XHTML验证器。 

在XHTML中，标签内的xmlns属性是必需的。然而，即使当XHTML文档中没有这个属性时，w3.org的验证工具也不会提示错误 。 这是因为，"xmlns=http://www.w3.org/1999/xhtml" 是一个固定的值，即使你没有把它包含在代码中，这个值也会被添加到标签中。 

关于XHTML的属性及事件和HTML的基本一样，这里就不赘述，如果要查阅详细内容，请查阅官方文档或者到W3School补充学习。

