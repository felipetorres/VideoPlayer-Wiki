Calling the `jzVideoPlayer.startWindowTiny()` function directly is enough to have the player in a small window, which is essentially the same as fullscreen.

> *See [ActivityTinyWindow](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/ActivityTinyWindow.java) in demo project.*

When we see a video in a list, if we roll the list the player will exit the screen. To solve this problem, when the player is invisible by scrolling we have the option to leave it in a small window in the corner of the screen.