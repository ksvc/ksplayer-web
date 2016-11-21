# 播放器功能组件

---
播放器类(Player)构建于UI组件架构之上。播放器类和其他控制类都是Component类的子类。

默认的UI组件嵌套关系如下：

```js
Player                         #视频播放器
    PosterImage                #封面图片
    TextTrackDisplay           #文本轨道显示（字幕，标题，章节标题）
    TextTrackSettings          #文本轨道设置
    LoadingSpinner             #加载指示
    BigPlayButton              #大播放按钮
    ErrorDisplay               #错误显示
    ControlBar                 #控制工具栏
        PlayToggle             #播放暂停按钮
        FullscreenToggle       #全屏按钮
        CurrentTimeDisplay     #当前时间显示
        RemainingTimeDisplay   #剩余时间显示
        ProgressControl        #进度控制
            LoadProgressBar    #加载进度条
            PlayProgressBar    #已播放控制条
            MouseDisplay       #进度条上的鼠标位置显示 
        VolumeControl          #音量控制
            VolumeBar          #音量控制条
                VolumeLevel    #音量 
        MuteToggle             #静音按钮
    MediaLoader                #视频加载器
```

播放器默认功能组件的添加或删除可以通过初始化的选项来配置。

```js

var player = videojs('video-id', {

     bigPlayButton: false
});

```
也可以通过播放器的设置方法动态的添加和删除。

```js
player.addChild("BigPlayButton"); //添加大播放按钮
player.removeChild("BigPlayButton"); //删除大播放按钮
```

