# 播放器设置方法

---

##播放器对象

ksplayer初始化视频播放器方法会返回一个播放器类(Player)的实例。

```js
var player = ksplayer('example_video');
```
当播放器实例被创建后，它可以再次使用`ksplayer('example_video')`获得全局访问。
```js
var player2 = ksplayer('example_video');
console.log(player == player2);  //true
```

## 方法

|方法|说明|方法|说明|
|:--|:--|:--|:--|
|[aspectRatio( [ratio] )](#aspectratio-ratio-)|获取/设置播放器宽高比|[autoplay( )](#autoplay-)|获取播放器的autoplay属性|
|[addChild( child )](#addchild-child-)|添加子组件|[addClass( classToAdd )](#addclass-classtoadd-)|向组件添加CSS|
|[buffered( )](#buffered-)|获取缓存信息|[bufferedEnd( )](#bufferedend-)|获取缓存结束时间|
|[bufferedPercent( )](#bufferedpercent-)|获取缓存数据占比|[canPlayType( type )](#canplaytype-type-)|可播放的mime类型检查|
|[controls( [bool] )](#controls-bool-])|获取/设置控制栏是否显示|[currentTime( [seconds] )](#currenttime-seconds-)|获取或设置当前时间|
|[currentSrc( )](#currentsrc-)|获取视频源URL|[currentType( )](#currenttype-)|获取视频源类型|
|[children( )](#children-)|获取子组件的数组|[dimension( dimension, [value] )](#dimension-dimension-value-)|获取/设置播放器的尺寸|
|[dispose( )](#dispose-)|销毁视频播放器|[duration( )](#duration-)|获取视频时长|
|[el( )](#el-)|获取组件的DOM|[ended( )](#ended-)|检查播放是否结束|
|[exitFullscreen( )](#exitfullscreen-)|退出全屏播放|[fluid( bool )](#fluid-bool-)|设置是否开启自适应布局|
|[height( [value] )](#height-value-)|获取/设置播放器高度|[width( [value] )](#width-value-)|获取/设置播放器宽度|
|[isFullscreen( )](#isfullscreen-)|检查是否是全屏模式|[load( )](#load-)|开始加载数据|
|[loop( [bool] )](#loop-bool-)|获取/设置loop属性|[muted( [bool] )](#muted-bool-)|获取/设置静音状态|
|[networkState( )](#networkstate-)|返回网络状态|[pause( )](#pause-)|暂停播放}|
|[paused( )](#paused-)|检测是否是暂停状态|[play( )](#play-)|开始播放|
|[playbackRate( [rate] )](#playbackrate-rate-)|获取/设置播放速率|[poster( [src] )](#poster-src-)|获取/设置封面图片|
|[preload( [value] )](#preload-value-)|获取/设置preload属性|[ready( fun,sync )](#ready-fun-sync-)| 绑定播放器ready监听|
|[readyState( )](#readystate-)|返回当前位置的播放的状态|[remainingTime( )](#remainingtime-)|返回播放的剩余时间|
|[requestFullscreen( )](#requestfullscreen-)|全屏播放|[reset( )](#reset-)|重置播放器|
|[scrubbing( )](#scrubbing-)|检查是否正在拖动进度|[seekable( )](#seekable-)|返回视频的TimeRanges|
|[seeking( )](#seeking-)|检查是否处于查找数据状态|[src( source )](#src-source-)|更新视频源|
|[videoHeight( )](#videoheight-)|获取视频内容高度|[videoWidth( )](#videowidth-)|获取视频内容宽度|
|[volume( percentAsDecimal )](#volume-percentasdecimal-)|获取或设置音量|[on( type,fn )](#on-type-fn-)|添加事件监听|
|[off( type,fn )](#off-type-fn-)|删除事件监听|[trigger( event,[hash] )](#trigger-event-hash-)|触发事件|

### aspectRatio( [ratio] )
获取或设置播放器宽高比
#### 参数

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|ratio|String|否|播放器宽高比|

```js
player.aspectRatio("16:9");
```


### autoplay( )
获取播放器的autoplay属性

```js
console.log("autoplay:" + player.autoplay()); //true or false
```

### addChild( child )
添加子组件，功能组件参见[播放器功能组件](component.md)
#### 参数

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|child|String|是|要被添加的子组件的类名|

```js
var bigBtn = player.addChild("BigPlayButton");
```
### addClass( classToAdd )
添加CSS类到组件DOM元素

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|classToAdd|String|是|要添加的样式的类名|

```js
bigBtn.addClass('my-style'); //bigBtn是一个按钮组件
```

### buffered( )
获取已缓存视频数据的信息，返回一个[TimeRanges](https://developer.mozilla.org/en-US/docs/Web/API/TimeRanges)对象。

```js
var bufferedTimeRange = player.buffered(),
numberOfRanges = bufferedTimeRange.length,  //被缓存的时间段的数目，通常是1
firstRangeStart = bufferedTimeRange.start(0), //第一个时间段起点的秒数，通常是0
firstRangeEnd = bufferedTimeRange.end(0), //第一个时间段结束点的秒数
firstRangeLength = firstRangeEnd - firstRangeStart; //第一个时间段的秒数
```
当`preload`属性值不是`none`时，播放器才会缓存数据。

### bufferedEnd( )
获取缓存数据最后一个时间区域的结束时间。

```js
var bufferedEnd = player.bufferedEnd();
```
等价于`player.buffered().end(player.buffered().length -1 )`


### bufferedPercent( )
获取已下载的缓存数据的百分比，用范围0~1的小数表示，0表示空，1表示全部。

```js
var howMuchIsDownloaded = player.bufferedPercent();

```

### canPlayType( type )
检查播放器是否可以播放给定的mime类型的视频

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|type|String|是|要检查的mime类型|

```js
console.log("mp4:" + player.canPlayType('video/mp4')); // "maybe"
```
说明：返回空字符串表示不支持，返回`'maybe'`表示支持。

### controls( [bool] )
获取或设置控制栏是否显示

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|bool|Boolean|否|设置控制栏是否显示|

```js
player.controls(true);
```

### currentTime( [seconds] )
获取或设置当前时间（单位为秒）

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|seconds|Number&#124;String|否|要设置的时间点|

```js
player.currentTime(10);
```

### currentSrc( )
获取当前视频源的完整URL

```js
player.currentSrc(); // e.g. http://mysite.com/video.mp4
```

### currentType( )
获取当前视频源的mime类型

```js
player.currentType(); // e.g. 'video/mp4'
```

### children( )
获取子组件的数组

```js
var kids = player.children();
```

### dimension( dimension, [value] )

获取或设置播放器的尺寸

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|dimension|String|是|width或height|
|value|Number|否|宽或高的值|

```js
player.dimension('width', 800);
var height = player.dimension('height');
```

### dispose( )

销毁视频播放器，并做一些必要的清理工作。

```js
player.dispose();
```

### duration( )

获取视频时长，返回以秒为单位的时间长度。

```js
var lengthOfVideo = player.duration();
```
*提醒*：如果返回0，可以采用延迟获取（`setTimeout`）。

### el( )

获取组件的DOM元素

```js
var videoDomEl = player.el(); // player也可以替换为其子组件
```

### ended( )
返回播放器是否已经处于`'ended'`状态


### exitFullscreen( )
退出全屏模式

```js
player.exitFullscreen();
```

### fluid( bool )

添加或删除`vjs-fluid`类，即是否开启流式布局（用于响应式设计）。

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|bool|Boolean|是|true表示添加该样式，false表示删除该样式|

```js
player.fluid(true);
```

### height( [value] )

获取或设置播放器高度

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|value|Number|否|高度值|

```js
player.height(300);
```

### isFullscreen(  )
检查播放器是否处于全屏模式

```js
player.isFullscreen(); //true or false
```

### load( )

开始加载src指定的数据

```js
player.load();
```

### loop( [bool] )

获取或设置video元素的loop属性

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|bool|Boolean|否|表示视频是否应该循环播放的真值|

```js
player.loop(true);
```

### muted( [bool] ) 

获取当前的静音状态；或者设置是否静音。

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|bool|Boolean|否|是否静音的真值|

```js
var isVolumeMuted = player.muted();
player.muted(true);
```

### networkState( )

返回网络状态，返回码（数字）含义如下：
- NETWORK_EMPTY(数字 0)：播放器尚未初始化。
- NETWORK_IDLE(数字 1）：播放器已经就绪，并找到资源，但还没有实际使用网络。
- NETWORK_LOADING(数字 2）：正在尝试下载数据。
- NETWORK_NO_SOURCE（数字 3）: 播放器准备就绪，但没有找到资源。

```js
player.networkState();
```

### pause( )
暂停播放

```js
player.pause();
```

### on( type, fn )

向播放器组件添加事件监听函数。

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|type|String|是|事件类型|
|fn|function|是|事件处理器函数|

```js
var myFunc = function(event,data){
 var player = this;
 // Do something when the event is fired
}
player.on('eventType', myFunc);
```
*说明*：当播放器被dispose的时候，事件监听会被自动清理。如果您要从DOM中删除播放器，请先在播放器上调用trigger('dispose')来清理引用并允许浏览器垃圾回收它。

### off(type, fn)

删除事件监听。

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|type|String|是|事件类型|
|fn|function|否|事件处理器函数|

```js
player.off('eventType', myFunc);
```

### paused( )
检测播放器是否暂停

```js
var isPaused = player.paused(); 
var isPlaying = !player.paused();
```

### play( )
开始播放

```js
player.play();
```

### playbackRate( [rate] )

获取或设置当前的播放速率。rate=1表示正常速度，rate=0.5表示正常速度的一半慢速播放，rate=2表示两倍速率快速播放。

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|rate|Number|否|要设置的新速率|

```js
player.playbackRate(2);
```

### poster( [src] )

获取或设置封面图片资源的url

#### 参数

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|src|String|否|封面图片源地址(URL)|

```js
var currentPoster = player.poster(); //get
player.poster('http://example.com/myImage.jpg'); //set
```

### preload( [value] )

获取或设置preload属性

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|bool|Boolean|否|取值：auto&#124;metadata&#124;none|

*说明*：如果value没有设置，默认值依赖于浏览器实现，标准建议设置为`metadata`。

```js
player.preload('auto');
```

### ready( fn, sync )

绑定监听器到组件的ready状态。如果ready时间已经发生，会马上触发函数的调用。

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|fn|function|是|ready监听器函数|
|sync|Boolean|否|已ready时调用监听函数是同步还是异步|

```js
player.ready(function() {
    //do something
});
```

### readyState( )

返回渲染当前位置视频的播放状态，返回码数字含义如下：

- HAVE_NOTHING（数字 0）：无可用的视频源相关信息
- HAVE_METADATA(数字 1）：资源的时长等元数据可用
- HAVE_CURRENT_DATA(数字 2）：当前播放点的数据可用
- HAVE_FUTURE_DATA(数字 3）：有足够的数据向前播放
- HAVE_ENOUGH_DATA(数字 4）： 有足够的数据继续播放而不会卡顿

```js
player.readyState();
```

### remainingTime( )

返回视频播放的剩余时间(s)

```js
var timeLeft = player.remainingTime();
```

### requestFullscreen( )

全屏播放

```js
player.requestFullscreen();
```

*说明*: 全屏播放需要浏览器的支持。

### reset( )

重置播放器，播放器的属性恢复初始化时的设置。

```js
player.reset();
```

### scrubbing( )

返回用户是否 **正在** 拖动进度条或点击进度条。

```js
var isScrubbing = player.scrubbing();
```
 
### seekable( )

返回当前播放视频的[TimeRanges](https://developer.mozilla.org/en-US/docs/Web/API/TimeRanges)对象。

```js
var videoTimeRange = player.seekable(),
numberOfRanges = videoTimeRange.length, //时间段的数目，通常是1
firstRangeStart = videoTimeRange.start(0), //第一个时间段起点的秒数，通常是0
firstRangeEnd = videoTimeRange.end(0), //第一个时间段结束点的秒数
firstRangeLength = firstRangeEnd - firstRangeStart; //第一个时间段的秒数,一般和duration属性的值相等
```

### seeking( )

返回播放器是否处于“搜索”状态，如拖动进度条后播放器会短暂处于搜索状态。

```js
var isSeeking = player.seeking();
```

### src( source )

更新视频源。参数source可以是一个URL字符串或一个对象。

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|source|String&#124;Object|是|视频的URL或包含地址和类型信息的对象|


**URL字符串**： 传一个URL字符串。如果确信当前的播放技术（H5/Flash)可以支持你提供的视频源，可以使用这种技术。目前只有MP4格式的文件可以同时在H5和Flash中播放。

```js
player.src("http://www.example.com/path/to/video.mp4");
```

**源对象**: 包含视频类型和URL属性的一个JavaScript对象。如果你希望让播放器决定是否能支持该视频源的播放，请使用类型信息。

```js
player.src({ type: "video/mp4", src: "http://www.example.com/path/to/video.mp4" });
```

### trigger( event, [hash] )

触发事件

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|event|String|是|事件名|
|hash|Object|否|需要通过事件传递的数据|

```js
player.trigger('ended',{data: 'some data'});
```

### videoHeight( )

获取视频内容原始高度

```js
var videoHeight = player.videoHeight();
```

### videoWidth( )

获取视频内容原始宽度

```js

var videoWidth = player.videoWidth();

```

### volume( percentAsDecimal )

获取或设置播放器当前音量

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|percentAsDecimal|Number|否|百分比小数表示的新音量|

```js
var howLoudIsIt = player.volume(); // get
player.volume(0.5); // Set volume to half
```

### width( [value] )

获取或设置播放器宽度

|参数名 |类型|是否必须|描述|
|---|---|---|---|
|value|Number|否|宽度值|

```js
var playerWidth = player.width();//get
player.width(800); //set
```

---

