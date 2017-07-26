###  9.3.2 HTML5特性

HTML5将成为HTML、XHTML以及HTML DOM的新标准。HTML的上一个版本诞生于1999 年。自从那以后，Web世界已经经历了巨变。HTML5仍处于完善之中。然而，大部分现代浏览器已经具备了某些HTML5支持。 HTML5是 W3C（World Wide Web Consortium，万维网联盟）与WHATWG（Web Hypertext Application Technology Working Group）合作的结果， WHATWG致力于 web表单和应用程序，而W3C专注于XHTML2.0。在2006年， 双方决定进行合作，来创建一个新版本的HTML，他们为HTML5建立的一些规则如下：

* 新特性应该基于HTML、CSS、DOM以及JavaScript
* 减少对外部插件的需求（比如Flash）
* 更优秀的错误处理
* 更多取代脚本的标记
* HTML5应该独立于设备
* 开发进程应对公众透明

针对这些规则，HTML5也就有了许多新特性，如下：

* 用于绘画的canvas元素
* 用于媒介回放的video和audio元素
* 对本地离线存储的更好的支持
* 新的特殊内容，比如article、footer、header、nav、section
* 新的表单控件，比如calendar、date、time、email、url、search

下面我们主要介绍一下HTML5的新特性：

#### HTML5视频

直到现在，仍然不存在一项旨在网页上显示视频的标准，大多数视频是通过插件（比如Flash）来显示的。然而，并非所有浏览器都拥有同样的插件。HTML5规定了一种通过video元素来包含视频的标准方法。如下：

```
<video src="movie.ogg" width="320" height="240" controls="controls"></video>
```

目前video标签只支持3种格式Ogg、MPEG4和WebM，其中control属性供添加播放、暂停和音量控件，width和height指定播放界面的宽、高，src指定播放的视频的URL。 上面的例子使用一个Ogg文件，适用于Firefox、Opera以及Chrome浏览器。要确保适用于 Safari浏览器，视频文件必须是MPEG4 类型。video元素允许多个source元素，而且source元素可以链接不同的视频文件，浏览器将使用第一个可识别的格式，如下所示：

```
<video width="320" height="240" controls="controls">
    <source src="movie.ogg" type="video/ogg">
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.webm" type="video/webm">
    Your browser does not support the video tag.
</video>
```

需要注意的是使用video标签在webkit引擎的浏览器中使用正常， 但在FireFox（火狐）Gecko解析引擎下就容易出现无法加载影片的问题。 本书作者也曾被这个问题困扰，后来终于找到答案，火狐浏览器要求比较严格，当加载webm等格式的文件时返回类型一定要是video/webm等格式, 而在较早版本的像Apache之类的服务器中并没有该类型定义，所以你只要联系服务器管理员，请管理员在 Apache的配置文件http.conf中添加以下类型即可：

AddType video/ogg .ogv 

AddType video/mp4 .mp4 

AddType video/webm .webm

#### HTML5音频

拖放（Drag和drop）是HTML5标准的组成部分。拖放是一种常见的特性，即抓取对象以后拖到另一个位置，在HTML5中，任何元素都能够拖放，示例如下：

```
<!DOCTYPE HTML>
<html>
<head>
    <style type="text/css">
        #div1 {width:488px;height:70px;padding:10px;border:1px solid #aaaaaa;}
    </style>
    <script type="text/javascript">
        function allowDrop(ev){
            ev.preventDefault();
        }
        function drag(ev){
            ev.dataTransfer.setData("Text",ev.target.id);
        }
        function drop(ev){
            ev.preventDefault();
            var data=ev.dataTransfer.getData("Text");
            ev.target.appendChild(document.getElementById(data));
        }
    </script>
</head>
<body>
    <div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
    <br />
    <img id="drag1" src="aa.png" draggable="true" ondragstart="drag(event)" />
</body>
</html>
```



