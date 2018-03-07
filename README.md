# iframeContentDrag
实现iframe内容页拖拽代替滚动条滚动


需求：用iframe标签链接一个网页，iframe设置固定宽高，隐藏滚动条，当内容页宽高大于iframe宽高，拖动内容页代替滚动看到隐藏的内容

1.获取内容页的window对象

var iframeWin = document.getElementById("test").contentWindow;

2.获取内容页的document对象

var iframedoc = iframeWin.document;

3.获取拖动初始时鼠标指针相对浏览器窗口的坐标

var posX = e.clientX;

var posY = e.clientY;

4.获取拖动初始时iframe的滚动距离

var scrollX = iframeWin.scrollX;

var scrollY = iframeWin.scrollY;

5.内容页随鼠标指针拖动

iframeWin.scroll(scrollX + posX - e.clientX, scrollY + posY - e.clientY);

一个应用例子如下

test.html

<body>

  <iframe src="a.html" width="500" height="500" scrolling="no" id="test" frameborder="0" marginheight="0" marginwidth="0"></iframe>

  <script>

    window.onload = function(){

        var iframe = document.getElementById("test");

        var iframeWin = iframe.contentWindow;

        var iframedoc = iframeWin.document;

        var posX = 0;

        var posY = 0;

        var scrollX = 0;

        var scrollY = 0;

        iframedoc.onmousedown = function(e){

        posX = e.clientX;

        posY = e.clientY;

        scrollX = iframeWin.scrollX;

        scrollY = iframeWin.scrollY;

        iframedoc.onmousemove = function(e){

        iframeWin.scroll(scrollX + posX - e.clientX, scrollY + posY - e.clientY);

        };

        iframedoc.onmouseup = function(){

        iframedoc.onmousemove = null;

        };

        };

        };

  </script>

</body>


a.html

<body>

  <div style="width: 1200px; height: 1000px; background-color: green; padding: 0; margin: 0;">

  <div style="width: 400px; height: 400px; background-color: blue;"></div>

</div>

</body>
