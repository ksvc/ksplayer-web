# 播放器配置选项

---

## 设置方式
---
ksplayer嵌入的代码是一个简单的HTML5 video标签，所以你可以使用标准的标签属性去设置很多选项。

```js
<video controls autoplay preload="auto" ...>
```
*注意：* 如果video标签的某个属性的取值是布尔值（true/flase)，那么不要用等号给它赋值，只需要简单的包含该属性或去掉该属性，来表示开关状态，如上面的`autoplay`属性。

或者，您可以传递一个选项对象给播放器的初始化函数（函数第二个参数）。

```js
ksplayer("example_video_1", { 
    "controls": true, 
    "autoplay": false, 
    "preload": "auto" 
});
```

## 属性选项
---
### controls
controls选项用于设置播放器是否包含用户可以操作的控制工具栏（播放器底部）。如果不加controls选项，就只能通过autoplay属性或通过js api来播放视频。

```js
<video controls ...> 
or 
{ "controls": true }
```

### autoplay
决定播放器是否在页面加载后就自动播放视频（在iOS设备上不支持），默认值为`false`。

```js
<video autoplay ...> or { "autoplay": true }
```

### preload
该属性通知浏览器是否在video标签载入后就立即下载视频数据。选项包括 `auto`,`metadata`和`none`。

'auto': 如果浏览器允许，立即开始下载视频。
'metadata': 只下加载视频的元数据，包括视频尺寸和时长等信息。
'none':不预加载视频数据。等到用户点击播放时再开始下载。

```js
<video preload ...> or { "preload": "auto" }
```

### poster
poster属性用于设置视频播放前显示的封面图片。一旦用户点击播放按钮，该图片消失。

```js
<video poster="myPoster.jpg" ...> or { "poster": "myPoster.jpg" }
```

### loop
设置视频循环播放。这可以用作沉浸式背景视频。

```js
<video loop ...> or { "loop": true }
```

### width
设置视频显示区域宽度。

```js
<video width="640" ...> or { "width": 640 }
```

### height
设置视频显示区域高度。

```js
<video height="480" ...> or { "height": 480 }
```
### language
设置播放器语言，选项包括`zh-CN`（中文）和`en`（默认：英文)。

```js
<video language="zh-CN" ...> or { "language": "zh-CN" }
```

### 组件选项
你可以为任何播放器组件设置选项。比如你想删除controlBar组件的子组件muteToggle按钮，你可以将这个组件的值设置为false：

```js
var player = videojs('video-id', { 
    controlBar: { 
        muteToggle: false 
    } 
});
```

[播放器功能组件](component.md)一节包含播放器所有子组件。您只需要在每层的子组件数组中嵌套子组件即可。





