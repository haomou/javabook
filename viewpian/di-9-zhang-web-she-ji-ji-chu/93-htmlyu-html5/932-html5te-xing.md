### 9.3.2 HTML5特性

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

这个例子看上去也许有些复杂，不过我们可以分别研究拖放事件的不同部分。首先，为了使元素可拖动，把draggable属性设置为 true，如下：

```
<img draggable="true" />
```

然后，规定当元素被拖动时，会发生什么。在上面的例子中，ondragstart属性调用了一个函数\(drag\(event\)\)，它规定了被拖动的数据。 dataTransfer.setData\(\)方法设置被拖数据的数据类型和值：

```
function drag(ev){
    ev.dataTransfer.setData("Text",ev.target.id);
}
```

在这个例子中，设置的数据类型是"Text"，值是可拖动元素img标签的id值drag1。

ondragover事件规定在何处放置被拖动的数据，默认地，无法将数据/元素放置到其他元素中。如果需要设置允许放置，我们必须阻止对元素的默认处理方式，这要通过调用ondragover事件的event.preventDefault\(\)方法：

```
event.preventDefault()
;
```

当放置被拖数据时，会发生drop事件，在上面的例子中，ondrop属性调用了一个函数（drop\(event\)），如下：

```
function drop(ev){
    ev.preventDefault();
    var data=ev.dataTransfer.getData("Text");
    ev.target.appendChild(document.getElementById(data));
}
```

从上例可以看出，在ondrop事件中主要是通过appendChild的方法将元素追加到目标元素当中。

#### HTML5 CANVAS（画布）

HTML5的另外一个重要的特性是它定义了canvas元素标签用于使用Javascript在网页上绘制图像，画布是一个矩形区域，您可以控制其每一像素，canvas拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。 如下创建一个Canvas元素：

```
<canvas id="myCanvas" width="200" height="100"></canvas>
```

由canvas元素本身是没有绘图能力的。所有的绘制工作必须在JavaScript内部完成，例如：

```
<script type="text/javascript">
    var c=document.getElementById("myCanvas"); // canvas 元素 id
    var cxt=c.getContext("2d");//创建 context 对象
    cxt.fillStyle="#FF0000"; //设置填充颜色
    cxt.fillRect(0,0,150,75); //根据坐标绘制矩形框
</script>
```

上面的fillRect方法拥有参数\(0,0,150,75\)，意思是：在画布上绘制150x75的矩形，从左上角\(0,0\)开始。如下图所示，画布的X和Y坐标用于在画布上对绘画进行定位，如下图9-11所示。

![](/assets/9-11.png)

#### HTML5 地理定位

HTML5 Geolocation API 用于获得用户的地理位置，鉴于该特性可能侵犯用户的隐私，除非用户同意，否则用户位置信息是不可用的。同时对于拥有GPS的设备，比如iPhone，地理定位更加精确，具体使用如下例：

```
<!DOCTYPE html>
<html>
<body>
    <p id="demo">点击这个按钮，获得您的坐标：</p>
    <button onclick="getLocation()">试一下</button>
    <script>
        var x=document.getElementById("demo");
        function getLocation(){
            if (navigator.geolocation){
                navigator.geolocation.getCurrentPosition(showPosition);
            }else{
                x.innerHTML="Geolocation is not supported ";
            }
        }
        function showPosition(position){
            x.innerHTML="Latitude: " + position.coords.latitude +"<br />Longitude: " + position.coords.longitude;
        }
    </script>
</body>
</html>
```

本例中只是用了Geolocation对象的getCurrentPosition\(\)方法的一个参数，实际上 getCurrentPosition\(\)方法的还有第二个参数用于处理错误，它规定当获取用户位置失败时运行的函数，如下：

```
function showError(error){
    switch(error.code){
        case error.PERMISSION_DENIED:
                x.innerHTML="User denied the request"
                break;
        case error.POSITION_UNAVAILABLE:
                x.innerHTML="Location information is unavailable."
                break;
        case error.TIMEOUT:
                x.innerHTML="The request timed out."
                break;
        case error.UNKNOWN_ERROR:
                x.innerHTML="An unknown error occurred."
                break;
    }
}
```

如需在地图中显示结果，您需要访问可使用经纬度的地图服务，比如谷歌地图或百度地图，综合示例如下：

```
<!DOCTYPE html>
<html>
    <head>
        <script src="http://maps.google.com/maps/api/js?sensor=false"></script>
    </head>    
    <body>
        <p id="demo">点击这个按钮，获得您的位置：</p>
        <button onclick="getLocation()">试一下</button>
        <div id="mapholder"></div>
        <script>
            var x=document.getElementById("demo");
            function getLocation() {
                if (navigator.geolocation) {
                    navigator.geolocation.getCurrentPosition(showPosition,showError);
                } else{
                    x.innerHTML="Geolocation is not supported by this browser.";}
                }
            function showPosition(position){
                lat=position.coords.latitude;
                lon=position.coords.longitude;
                latlon=new google.maps.LatLng(lat, lon) <!—转换为 google 经纬度 -->
                mapholder=document.getElementById('mapholder')
                mapholder.style.height='250px';
                mapholder.style.width='500px';
                var myOptions={
                    center:latlon,zoom:14, <!—设定地图中心，缩放等级 -->
                    mapTypeId:google.maps.MapTypeId.ROADMAP, <!—设定街道视图 -->
                    mapTypeControl:false, <!—设定视图不可切-->
                    navigationControlOptions:{style:google.maps.NavigationControlStyle.SMALL}
                };
                <!—显示地图，在获取的坐标上设定标记 -->
                var map=new google.maps.Map(document.getElementById("mapholder"),myOptions);
                var marker=new google.maps.Marker({position:latlon,map:map,title:"You are here!"});
            }
            function showError(error){
                switch(error.code){
                    case error.PERMISSION_DENIED:
                        x.innerHTML="User denied the request for Geolocation."
                        break;
                    case error.POSITION_UNAVAILABLE:
                        x.innerHTML="Location information is unavailable."
                        break;
                    case error.TIMEOUT:
                        x.innerHTML="The request to get user location timed out."
                        break;
                    case error.UNKNOWN_ERROR:
                        x.innerHTML="An unknown error occurred."
                        break;
                }
            }
        </script>
    </body>
</html>
```

Geolocation对象的getCurrentPosition\(\)方法返回position对象，通过该对象可以获取很多有用信息，如下：

| coords.latitude | 十进制数的纬度 |
| :--- | :--- |
| coords.longitude | 十进制数的经度 |
| coords.accuracy | 位置精度 |
| coords.altitude | 海拔，海平面以上以米计 |
| coords.altitudeAccuracy | 位置的海拔精度 |
| coords.heading | 方向，以正北开始以度计 |
| coords.speed | 速度，以米/每秒计 |
| timestamp | 响应的日期/时间 |

Geolocation对象还有一些方法如watchPosition\(\)，该方法返回用户的当前位置，并继续返回用户移动时的更新位置（就像汽车上的 GPS）。还有clearWatch\(\)方法，该方法停止watchPosition\(\)方法。调用方法如下：

```
navigator.geolocation.watchPosition(showPosition);
```

#### HTML5 WEB存储

HTML5提供了两种在客户端存储数据的新方法：

* localStorage - 没有时间限制的数据存储

* sessionStorage - 针对一个session的数据存储

之前，客户端的数据存储都是由cookie完成的。但是cookie不适合大量数据的存储，因为它们由每个对服务器的请求来传递，这使得 cookie速度很慢而且效率也不高。在HTML5中，数据不是由每个服务器请求传递的，而是只有在请求时使用数据。它使在不影响网站性能的情况下存储大量数据成为可能。对于不同的网站，数据存储于不同的区域，并且一个网站只能访问其自身的数据，HTML5同样使用JavaScript来存储和访问数据。

localStorage方法存储的数据没有时间限制。第二天、第二周或下一年之后，数据依然可用。创建和访问localStorage示例如下：

```
<!DOCTYPE HTML>
<html>
    <body>
        <script type="text/javascript">
            if (localStorage.pagecount){
                localStorage.pagecount=Number(localStorage.pagecount) +1;
            }else{
                localStorage.pagecount=1;
            }
            document.write("Visits: " + localStorage.pagecount + " time(s).");
        </script>
        <p>刷新页面会看到计数器在增长。</p>
        <p>请关闭浏览器窗口，然后再试一次，计数器会继续计数。</p>
    </body>
</html>
```

#### HTML5应用程序缓存

HTML5引入了应用程序缓存，这意味着web应用可进行缓存，并可在没有因特网连接时进行访问。

应用程序缓存为应用带来三个优势：

* 离线浏览 - 用户可在应用离线
* 速度 - 已缓存资加载得更快
* 减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源

  关于HTML5带有cache manifest的HTML文档（供离线浏览）示例如下：

```
<!DOCTYPE html>
<html manifest="test.appcache">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    </head>
    <body>
        <img src="hello.png" />
        <p>重新加载本页面，页面中的图像依然可用。</p>
    </body>
</html>
```

上例中通过html标签中的manifest属性指定了客户端要缓存和更新的内容，关于 Catch Manifest 文件介绍如下：

如需启用应用程序缓存，请在文档的标签中包含manifest属性， 每个指定了manifest的页面在用户对其访问时都会被缓存。如果未指定manifest属性，则页面不会被缓存（除非在manifest文件中直接指定了该页面）。

* manifest文件的建议的文件扩展名是：".appcache"。

* 请注意，manifest文件需要配置正确的MIME-type，即"text/cache-manifest"，必须在web服务器上进行配置。

manifest文件是简单的文本文件，它告知浏览器被缓存的内容（以及不缓存的内容）。

manifest文件可分为三个部分：

* CACHE MANIFEST - 在此标题下列出的文件将在首次下载后进行缓存

* NETWORK - 在此标题下列出的文件需要与服务器的连接，且不会被缓存

* FALLBACK - 在此标题下列出的文件规定当页面无法访问时的回退页面（比如404页面）

 一个完整的manifest文件如下：

 CACHE MANIFEST 

**\# 2012-02-21 v1.0.0 **

/theme.css 

/hello.png 

/main.js 

**NETWORK: **

login.asp 

**FALLBACK: **

/html5/ /404.html

其中\#部分是注释内容，要注意一旦应用被缓存，它就会保持缓存直到发生下列情况：

1. 用户清空浏览器缓存
2. manifest文件被修改（参阅下面的提示）
3. 由程序来更新应用缓存

#### HTML5 WEB WORKER

当在HTML页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。web worker是运行在后台的JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等， 而此时web worker在后台运行。举一个完整的 web worker示例如下：

```
<!DOCTYPE html>
<html>
<body>
    <p>count: <output id="result"></output></p>
    <button onclick="startWorker()">start Worker</button>
    <button onclick="stopWorker()">stop Worker</button>
    <script>
        var w;
        function startWorker(){
            if(typeof(Worker)!=="undefined"){
                if(typeof(w)=="undefined"){
                    w=new Worker("count.js");
                }
                w.onmessage = function (event) {
                    document.getElementById("result").innerHTML=event.data;
                };
            }else{
                document.getElementById("result").innerHTML="Sorry,
                your browser does not support Web Workers...";
            }
        }
        function stopWorker(){ 
            w.terminate();
        }
    </script>
</body>
</html>
```

该实例在点击startWorker按钮之后会将count.js调入后台执行，创建一个新的web Worker对象，并注册了监听消息的方法，该方法用于监听后台执行的js代码传回的消息。直到执行stopWorker方法，停止执行，其中count.js代码如下：

```
var i=0;
function timedCount(){
    i=i+1;
    postMessage(i);
    setTimeout("timedCount()",500); <!—定时 500ms 执行 -->
}
timedCount();
```

上面代码中最重要的是postMessage方法，该方法用于向HTML页面传回参数信息，本例中传回的是计数值，该信息会被startWorker 中的onmessage事件捕获到，并从event中获取所传的参数值。 需要注意的是，由于web worker位于外部文件中，它们无法访问下例 JavaScript对象：window对象、document对象和parent对象。

