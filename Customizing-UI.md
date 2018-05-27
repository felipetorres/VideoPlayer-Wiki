The player interface is highly customizable and you can easily modify the video title display, battery level display and add buttons for several actions like sharing, speed control, fullscreen exibition. Regardless of customization, they all follow the same guide described in this section.

> *Check some [UI customizations in demo folder](https://github.com/lipangit/JiaoZiVideoPlayer/tree/develop/app/src/main/java/cn/jzvd/demo/CustomView).*

### Three important things to know

**The most important task related to customization is inheriting [JZVideoPlayerStandard](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/CustomView/MyJZVideoPlayerStandard.java) first!!!**  
**The most important task related to customization is inheriting [JZVideoPlayerStandard](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/CustomView/MyJZVideoPlayerStandard.java) first!!!**  
**The most important task related to customization is inheriting [JZVideoPlayerStandard](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/CustomView/MyJZVideoPlayerStandard.java) first!!!**  

### Modifying xml

Add the control you want using the file `R.layout.jz_layout_standard` as example but do not delete the unnecessary controls. If you delete the code, some internal `findViewById` will crash.

### Getting a reference to the new layout

Override `getLayoutId` method, to return its own xml layout. Don't care about fullscreen and non-fullscreen layouts: both are the same xml layout. Just some controls are displayed in fullscreen and hide in not-fullscreen.

Override the `init` method, and call `findViewById` to find the control you've been added.

### Using new control

The `JZVideoPlayerStandard` class already has implementations for each of the methods responsible for managing the states of its lifecycle:

1. `onStateNormal`
2. `onStatePreparing`
3. `onStatePreparingChangingUrl`
4. `onStatePlaying`
5. `onStatePause`
6. `onStatePlaybackBufferingStart`
7. `onStateError`
8. `onStateAutoComplete`

If you want to manipulate your custom control or change some aspect of the player's default lifecycle, just override them.

> *For details check this [section about `JZVideoPlayerStandard` lifecyle states](./Customizing-Code#JZVideoPlayerStandard-lifecycle).*