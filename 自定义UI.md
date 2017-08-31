自定义UI可以说是用处最多的，比如标题的显示与否，添加分享按钮，全屏显示电量等任何的DEMO UI不一样的修改都可以总结为自定义UI。

### 重要的事情说三遍

**和自定义相关的工作，最主要是先继承[JCVideoPlayerStandard](https://github.com/lipangit/JieCaoVideoPlayer/blob/develop/app/src/main/java/fm/jiecao/jiecaovideoplayer/CustomView/MyJCVideoPlayerStandard.java)！！！**<br />
**和自定义相关的工作，最主要是先继承[JCVideoPlayerStandard](https://github.com/lipangit/JieCaoVideoPlayer/blob/develop/app/src/main/java/fm/jiecao/jiecaovideoplayer/CustomView/MyJCVideoPlayerStandard.java)！！！**<br />
**和自定义相关的工作，最主要是先继承[JCVideoPlayerStandard](https://github.com/lipangit/JieCaoVideoPlayer/blob/develop/app/src/main/java/fm/jiecao/jiecaovideoplayer/CustomView/MyJCVideoPlayerStandard.java)！！！**

### 修改xml

在R.layout.jc_layout_standard的基础上，添加自己想要的控制，不需要的控件不能删除，如果删除代码findViewById找不见会报错，只能隐藏。

### 取得新控件的引用

复写getLayoutId函数，设置自己的xml布局，全屏和非全屏是一个xml布局，只是有的控件全屏显示，非全屏隐藏。

复写init函数，findViewById找到自己添加的控件。

### 操作控件

根据自己的需要，复写进入状态的函数，代码中应该是不厌其烦的分别控制每个状态的控件，这样做思路清晰，不会出现遗漏。

1. onStateNormal
2. onStatePreparing
3. onStatePreparingChangingUrl
4. onStatePlaying
5. onStatePause
6. onStatePlaybackBufferingStart
7. onStateError
8. onStateAutoComplete

上述State的含义[点此](https://github.com/lipangit/JieCaoVideoPlayer/wiki/%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BB%A3%E7%A0%81#%E7%BB%A7%E6%89%BFjcvideoplayerstandard%E5%A4%8D%E5%86%99%E7%9A%84%E5%87%BD%E6%95%B0)

