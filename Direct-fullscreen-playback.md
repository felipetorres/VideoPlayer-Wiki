One line of code can start a fullscreen playback:

```java
JZVideoPlayerStandard
		.startFullscreen(this,
						JZVideoPlayerStandard.class,
						"http://2449.vod.myqcloud.com/2449_22ca37a6ea9011e5acaaf51d105342e3.f20.mp4",
						"Video title");
```

The second parameter is a custom class that inherits from `JZVideoPlayer`. There is no non-fullscreen status.

Exiting fullscreen will exit playback.

> *See [ActivityDirectPlay](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/ActivityDirectPlay.java) in demo project*.

Add the following code in the activity's lifecycle that started fullscreen playback. If you start fullscreen playback directly in the Fragment or ListView item, you only need to add the following code in the Activity that contains the Fragment or ListView:

```java
@Override
public void onBackPressed() {
    if (JZVideoPlayer.backPress()) {
        return;     
    }     
    super.onBackPressed();
}

@Override
protected void onPause() {
    super.onPause();
    JZVideoPlayer.releaseAllVideos();
}
```
