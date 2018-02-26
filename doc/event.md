# 播放器相关事件

---

通过`on`方法可以监听播放器相关事件，`off`方法可以取消监听，`trigger`方法可以触发播放器事件。参见[播放器设置方法文档](api.md#方法);

### 示例代码

```js
player.on("pause",function(event, data) {
   //Do something when the event is fired    
});
```

### 事件

### ready

播放器初始化完毕可以播放视频时触发

### loadstart

播放器开始加载数据时触发

### loadmetadata

播放器获取到时长和尺寸信息时触发

### loadeddata

播放器加载到第一帧数据后触发

### play

视频由暂停恢复为播放时触发

### pause

视频暂停时触发

### ended

当前视频播放完毕时触发

### seeking

播放器开始寻轨（寻找数据）

### seeked

播放器结束寻轨

### useractive 

当用户和播放器互动时触发，如用户鼠标在播放器上移动。

### userinactive

当用户不活动时触发。例如在最后一次鼠标移动或互动控制短暂延迟后触发。

### durationchange

视频时长信息变化时触发

### volumechange

当音量改变时触发

### error

发生错误时触发

### waiting

出现卡顿，需要缓存下一帧数据时触发

### progress

加载进度条变化时触发

### timeupdate

视频播放时每隔一段时间(约250ms，因浏览器而异)触发一次，视频暂停播放时不触发。

### handleFullscreenChange

播放器全屏状态改变时触发