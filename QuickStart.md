### 1. build.gradle

Add this dependency in `build.gradle`:

```gradle
compile 'cn.jzvd:jiaozivideoplayer:x.x.x'
```

> *For Android Studio 3+ the compile function has been deprecated. You should use `implementation` or `api`. Check the [new dependency configurations in Android documentation](https://developer.android.com/studio/build/gradle-plugin-3-0-0-migration#new_configurations) for more details.*

Changing the library or introducing other reference methods (such as jar, aar) is not recommended because updates to this library are done approximately every two weeks with bug fixes and new features. If you change the library locally, your update will be very problematic. The `JZVideoPlayerStandard` class can serve virtually any needs to change methods and user interface.


### 2. layout.xml

In your `layout.xml` file, add the `cn.jzvd.JZVideoPlayerStandard` view that represents the video player itself:

```xml
<cn.jzvd.JZVideoPlayerStandard
    android:id="@+id/videoplayer"
    android:layout_width="match_parent"
    android:layout_height="200dp"/>
```

You can change its height and width or define a specific aspect ratio. Regardless of the dimensions of this view, the image will be centered, but if the aspect ratio between video and view are different, there will be black borders.

To avoid this problem, you can programatically set the player to fit the dimensions of the view, but there will be some distortion in the image (it will be "stretched" or "cut" in some dimension).

> *Take a look at [this activity in demo project](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/ActivityApiRotationVideoSize.java) for more details.*

### 3. Initializing VideoPlayer

Get a `VideoPlayer` instance from your layout:

```java
JZVideoPlayerStandard jzVideoPlayerStandard = 
            (JZVideoPlayerStandard) findViewById(R.id.videoplayer);
```

Initialize this instance passing 3 arguments:
 - Video Url

 - Player screen position: `SCREEN_WINDOW_NORMAL`, `SCREEN_WINDOW_LIST`, `SCREEN_WINDOW_FULLSCREEN` or `SCREEN_WINDOW_TINY`.

 - Video title

 > *The video title parameter is an `Object...` which stores other data that may be passed to `VideoPlayer` instance such as the amount of play, video classification information, etc.*

```java
jzVideoPlayerStandard.setUp("http://jzvd.nathen.cn/c6e3dc12a1154626b3476d9bf3bd7266/6b56c5f0dc31428083757a45764763b0-5287d2089db37e62345123a1be272f8b.mp4", 
                            JZVideoPlayerStandard.SCREEN_WINDOW_NORMAL, 
                            "Video title");
```

Set the video thumbnail. As imageView doesn't have `setImage` method, this pseudo-code function just represents **your picture loading strategy** which can use any common library as ImageLoader, Glide, Picasso.

```java
jzVideoPlayerStandard
            .thumbImageView
            .setImage("http://p.qpic.cn/videoyun/0/2449_43b6f696980311e59ed467f22794e792_1/640");
```

> *Take a look at [this activity in demo project](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/ActivityApi.java) for more details.*

### 4. Integration with Activity lifecycle

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

The `backPress` method checks if back button was touched. If the `videoPlayer` was in fullscreen mode it will exit full screen playback. Otherwise it will close the activity.

When the activity's lifecycle enters `onPause`, it should call `releaseAllVideos`, because we set the video to be released when the user exits the current Activity or press the home button.

> *This code only needs to be used during the activity's lifecycle. If `VideoPlayer` is in a Fragment or ViewPager you don't need to overwrite the Fragment's `onPause` function. You only need to overwrite `onPause` and `onBackPressed` functions of the Activity that contains the Fragment that plays the control.*

> *If you need the playback playing after you close activity, you can refer to this [code](https://github.com/lipangit/JiaoZiVideoPlayer/issues/1122#issuecomment-321146486) given by a friend.*

### 5. AndroidManifest.xml

```xml
<activity
    android:name=".MainActivity"
    android:configChanges="orientation|screenSize|keyboardHidden"
    android:screenOrientation="portrait" />
    <!-- or android:screenOrientation="landscape"-->
```

`android:configChanges` avoids Activity lifecycle execution when rotating screen (which would interrupts video playback).

`android:screenOrientation` sets the initial screen orientation. It can be setted programatically using `JZVideoPlayer.FULLSCREEN_ORIENTATION` and `JZVideoPlayer.NORMAL_ORIENTATION`