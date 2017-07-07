# FAQ

## 为什么视频用VLC等播放器能播放,但用ksplayer web播放器无法播放?

浏览器对跨域资源的访问有限制, 需要在服务端做配置允许浏览器跨域访问视频流或点播文件。
如果使用金山云服务,可以在ks3(对象存储)控制台对视频文件所在的存储空间进行设置。参见: 
[CORS配置](https://docs.ksyun.com/read/latest/30/_book/service/cors.html) 。

## 在iOS上如何禁止弹出一个默认的播放器全屏播放视频?

在video标签中加入 `playsinline` 属性可以内联播放。为了支持老版本的iOS系统,建议同时增加 `webkit-playsinline`,
并引入[iphone-inline-video](https://github.com/bfred-it/iphone-inline-video) 库。

## 微信分享页面在Android上播放器控制栏被原生控件替代如何解决?

Android上微信使用的是自带的渲染引擎 TBS。新版的TBS 内核（>=036849）
支持一个叫 同层播放器 的视频播放器。只需给 video 设置两个属性 `x5-video-player-type="h5"`
和 `x5-video-player-fullscreen="true"`

## 如何让视频居中宽度自适应全屏播放?

视频的高宽比是固定的(如16:9)，而手机的屏幕高宽比是不同的。为了让观看到的视频的体验尽可能一致，以宽度为先(宽度100%)，进行适配。
        
        function resizePlayer(videoTagId) {
            var width = window.innerWidth;  
            var height = width * 16 / 9;
            var marginTop = window.innerHeight - height;
            var $video = document.getElementById(videoTagId);
            $video.style.width = width + 'px';
            $video.style.height = height + 'px';
            $video.style.marginTop = marginTop < -2 ? marginTop /2 + 'px' : '0';
        }

`小提示`: 如果使用fluid选项(自适应)初始化ksplayer, 之后再通过width()和height()方法设置播放器宽高是不起作用的。
可以直接设置播放器的video标签的样式来动态控制播放器的实际宽高(如上)。

## 如何隐藏全屏显示按钮?

可以在video标签上增加`vjs-nofull`样式类,如下:

```
 <video id="example-video"  class="video-js mobile-first-skin vjs-nofull" controls></video>
```

## 为什么安装了Flash插件还是无法播放播放rtmp和flv直播流?

Flash插件可能被禁用了。新版本的chrome(56+)默认不开启Flash插件,需要手动开启。可以在浏览器的地址栏输入
chrome://settings/content/flash ,开启`允许网站运行flash`并关闭`先询问`, 地址栏输入 chrome://flags/#run-all-flash-in-allow-mode 设置为
Enable(启用), 重启浏览器。