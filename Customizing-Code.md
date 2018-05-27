### Three important things to know

**The most important task related to customization is inheriting [JZVideoPlayerStandard](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/CustomView/MyJZVideoPlayerStandard.java) first!!!**  
**The most important task related to customization is inheriting [JZVideoPlayerStandard](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/CustomView/MyJZVideoPlayerStandard.java) first!!!**  
**The most important task related to customization is inheriting [JZVideoPlayerStandard](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/CustomView/MyJZVideoPlayerStandard.java) first!!!**

By inheriting from `JZVideoPlayerStandard`, this section gives a brief description of the main methods of its lifecycle. Most code customizations involve modifying one or more of these methods:

## JZVideoPlayerStandard lifecycle

 1. **init**: This is the first call when the playback control is initialized.

 2. **onClick**: This method handles click in all `VideoPlayer` UI controls, such as start button, full screen button, blank click, retry button, and so on. If you want to intercept the click response or inherit the click response, then override this method.

 3. **onTouch**: In JZVideoPlayer this function mainly responds to gesture control volume, brightness and progress after full screen.

 4. **startVideo**: Start video playback flow.

 5. **onVideoRendingStart**: After the video starts playing, it enters the preparing state. When the video is ready, it enters the `onVideoRendingStart` function and starts playing.

 6. **onStateNormal**: Control enters normal unplayed state.

 7. **onStatePreparing**: Enter preparation state, initializing video.

 8. **onStatePlaying**: After preparing to enter playback.

 9. **onStatePause**: Pause video and enter pause.

 10. **onStatePlaybackBufferingStart**: Seek progress during playback, enter the state of the cached video.

 11. **onStateError**: Enter error state.

 12. **onStateAutoComplete**: Enter video auto play completion status.

 13. **onInfo**: `android.media.MediaPlayer` callback info.

 14. **onError**: `android.media.MediaPlayer` callback error.

 15. **startWindowFullscreen**: Enter fullscreen.

 16. **startWindowTiny**: Enter small screen.