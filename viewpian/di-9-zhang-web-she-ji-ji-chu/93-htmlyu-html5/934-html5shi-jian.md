### 9.3.4 HTML5事件

HTML5在HTML之上增加了媒介事件，其他的由于HTML5的新特性，增加了许多新的事件，如下分类，希望读者与HTML事件作对比。

* **窗口事件**

window对象触发的事件，适用于标签，如下表9-8所示。

**表9-8 窗口事件**

| **属性** | **值** | **描述** |
| :--- | :--- | :--- |
| onafterprint\(new\) | script | 在打印文档之后运行脚本 |
| onbeforeprint\(new\) | script | 在文档打印之前运行脚本 |
| onbeforeonload\(new\) | script | 在文档加载之前运行脚本 |
| onblur | script | 在窗口失去焦点时运行脚本 |
| onerror\(new\) | script | 当错误发生时运行脚本 |
| onfocus | script | 当窗口获得焦点时运行脚本 |
| onhashchange\(new\) | script | 当文档改变时运行脚本 |
| onload | script | 当文档加载时运行脚本 |
| onmessage\(new\) | script | 当触发消息时运行脚本 |
| onoffline\(new\) | script | 当文档离线时运行脚本 |
| ononline\(new\) | script | 当文档上线时运行脚本 |
| onpagehide\(new\) | script | 当窗口隐藏时运行脚本 |
| onpageshow\(new\) | script | 当窗口可见时运行脚本 |
| onpopstate\(new\) | script | 当窗口历史记录改变时运行脚本 |
| onredo\(new\) | script | 当文档执行再执行操作（redo）时运行脚本 |
| onresize\(new\) | script | 当调整窗口大小时运行脚本 |
| onstorage\(new\) | script | 当文档加载时运行脚本 |
| onundo\(new\) | script | 当Web Storage区域更新时（存储空间中数据发生变化时） |
| onunload\(new\) | script | 当用户离开文档时运行脚本 |

* **表单事件**

由HTML表单内部的动作触发的事件，适用于HTML5所有标签，如下表9-9所示。

**表9-9 表单事件**

| **属性** | **值** | **描述** |
| :--- | :--- | :--- |
| onblur | script | 当元素失去焦点时运行脚本 |
| onchange | script | 当元素改变时运行脚本 |
| oncontextmenu\(new\) | script | 当触发上下文菜单时运行脚本 |
| onfocus | script | 当元素获得焦点时运行脚本 |
| onformchange\(new\) | script | 当表单改变时运行脚本 |
| onforminput\(new\) | script | 当表单获得用户输入时运行脚本 |
| oninput\(new\) | script | 当元素获得用户输入时运行脚本 |
| oninvalid\(new\) | script | 当元素无效时运行脚本 |
| onreset | script | 当表单重置时运行脚本。HTML5 不支持 |
| onselect | script | 当选取元素时运行脚本 |
| onsubmit | script | 当提交表单时运行脚本 |

* **键盘事件**

 键盘事件和HTML一样们这里不作介绍。

* **鼠标事件**

由鼠标或相似的用户动作触发的事件，适用于HTML5所有标签，如下表9-10所示。

**表9-10 鼠标事件**

| **属性** | **值** | **描述** |
| :--- | :--- | :--- |
| onclick | script | 当单击鼠标时运行脚本 |
| ondbclick | script | 当双击鼠标时运行脚本 |
| ondrag\(new\) | script | 当拖动元素时运行脚本 |
| ondragend\(new\) | script | 当拖动操作结束时运行脚本 |
| ondragenter\(new\) | script | 当元素被拖动至有效的拖动目标时运行脚本 |
| ondragleave\(new\) | script | 当元素离开有效拖放目标时运行脚本 |
| ondragover\(new\) | script | 当元素被拖动至有效拖放目标上方时运行脚本 |
| ondragstart\(new\) | script | 当拖动操作开始时运行脚本 |
| ondrop\(new\) | script | 当被拖动元素正在被拖放时运行脚本 |
| onmousedown | script | 当按下鼠标按钮时运行脚本 |
| onmousemove | script | 当鼠标指针移动时运行脚本 |
| onmouseout | script | 当鼠标指针移出元素时运行脚本 |
| onmouseover | script | 当鼠标指针移至元素之上时运行脚本 |
| onmouseup | script | 当松开鼠标按钮时运行脚本 |
| onmousewheel | script | 当转动鼠标滚轮时运行脚本 |
| onscroll | script | 当滚动元素的滚动条时运行脚本 |

* **媒介事件**

由视频、图像以及音频等媒介触发的事件。适用于所有HTML5元素， 不过在媒介元素（诸如 audio、embed、img、object以及 video）中最常用，如下表9-11所示。

**表9-11 媒介事件**

| **属性** | **值** | **描述** |
| :--- | :--- | :--- |
| onabort | script | 当发生中止事件时运行脚本 |
| oncanplay\(new\) | script | 当媒介能够开始播放但可能因缓冲而需要停止时运行脚本 |
| oncanplaythrough\(new\) | script | 当媒介能够无需因缓冲而停止即可播放至结尾时运行脚本 |
| ondurationchange\(new\) | script | 当媒介长度改变时运行脚本 |
| onemptied\(new\) | script | 当媒介元素突然为空时（网络错误、加载错误等）运行脚本 |
| onended\(new\) | script | 当媒介已抵达结尾时运行脚本 |
| onerror\(new\) | script | 当在元素加载期间发生错误时运行脚本 |
| onloadeddata\(new\) | script | 当加载媒介数据时运行脚本 |
| onloadedmetadata\(new\) | script | 当媒介元素的持续时间以及其他媒介数据已加载时运行脚本 |
| onloadstart\(new\) | script | 当浏览器开始加载媒介数据时运行脚本 |
| onpause\(new\) | script | 当媒介数据暂停时运行脚本 |
| onplay\(new\) | script | 当媒介数据将要开始播放时运行脚本 |
| onplaying\(new\) | script | 当媒介数据已开始播放时运行脚本 |
| onprogress\(new\) | script | 当浏览器正在取媒介数据时运行脚本 |
| onratechange\(new\) | script | 当媒介数据的播放速率改变时运行脚本 |
| onreadystatechange\(new\) | script | 当就绪状态（ready-state）改变时运行脚本 |
| onseeked\(new\) | script | 当媒介元素的定位属性\[1\]不再为真且定位已结束时运行脚本 |
| onseeking\(new\) | script | 当媒介元素的定位属性为真且定位已开始时运行脚本 |
| onstalled\(new\) | script | 当取回媒介数据过程中（延迟）存在错误时运行脚本 |
| onsuspend\(new\) | script | 当浏览器已在取媒介数据但在取回整个媒介文件之前停止时运行脚本 |
| ontimeupdate\(new\) | script | 当媒介改变其播放位置时运行脚本 |
| onvolumechange\(new\) | script | 当媒介改变音量亦或当音量被设置为静音时运行脚本 |
| onwaiting\(new\) | script | 当媒介已停止播放但打算继续播放时运行脚本 |

 如上介绍的所有HTML5事件中，添加new标记的都是HTML5中新增的事件，希望读者注意区别。

