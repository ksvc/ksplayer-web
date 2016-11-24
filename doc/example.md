# 网页视频播放器使用示例

---
金山云视频播放器(ksplayer.js)非常易于使用,您可以花几秒钟时间将他集成使用到您的网页应用中。

## Step 1：引入ksplayer.js和CSS文件

---

### CDN方式

您可以从金山云的服务器上获取ksplayer需要脚本文件和样式，引入需要播放视频的页面（包括PC或H5）。

```js

<link href="//ksplayer.video.ksyun.com/v1/ksplayer.min.css" rel="stylesheet">

<script src="//ksplayer.video.ksyun.com/v1/ksplayer.min.js"></script>

```

### 自托管方式

您也可以下载ksplayer.js及其样式文件到您自己的服务器上。PC端请使用IE10以上版本的现代浏览器。
```js

<link href="//example.com/path/to/video-js.min.css" rel="stylesheet">

<script src="//example.com/path/to/ksplayer.min.js"></script>

<script>

     ksplayer.options.flash.swf = "http://example.com/path/to/ksplayer.swf"

</script>

```

## Step 2：添加video标签到您的页面
---
您只需要使用HTML5的video标签来嵌入视频。ksplayer会读取这个标签，让他在所有主流浏览器中生效（不仅限于那些支持HTML5 video标签的浏览器）。video标签还需要自定义id属性并添加`video-js` class属性。

```js
<video id="example_video_1" class="video-js" controls width="640" height="264" poster=""> 
    <source src="http://vjs.zencdn.net/v/oceans.mp4" type="video/mp4" /> 
    <p class="vjs-no-js">观看视频需要允许JavaScript,并更新浏览器以
        <a href="http://videojs.com/html5-video-support/" target="_blank">支持HTML5视频</a>
    </p> 
</video>
```
ksplayer提供了两套皮肤，默认样式和高级样式，可以分别通过在class属性中增加`js-default-skin`和`js-sublime-skin`类更换播放器皮肤。另外通过添加额外的`vjs-big-play-centered`类可以使播放按钮居中。

## Step 3: 初始化设置播放器
---
当ksplayer.js库已加载，而且video标签页加载到DOM后，运行如下js代码进行ksplayer的初始化。

```js   
var player = ksplayer("example_video_1", {options}, function(){         
    // 播放器 (this) 已经初始化完毕   
});
```
ksplayer函数的第一个参数是video标签的ID。

第二个参数是一个对象。用于设置一些播放器的选项参数。详见：[初始化选项参数](options.md)

第三个参数是ready回调函数。一旦ksplayer初始化完成，该函数将被调用。

该函数的返回一个播放器对象，该对象上的[设置方法](api.md)和[事件](event.md)参见API总览中相应部分。


**注意事项：**播放页面需要挂ip或域名访问，如若直接打开本地静态页面将无法播放直播视频。