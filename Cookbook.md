### Playing video

```java
jcVideoPlayer.startButton.performClick();
```

> *Touches to play in `NORMAL` state will pause the video during playback.*

### Directly enter fullscreen

```java
JZVideoPlayerStandard.startFullscreen(this,
                                      JZVideoPlayerStandard.class, 
                                      "http://2449.vod.myqcloud.com/2449_22ca37a6ea9011e5acaaf51d105342e3.f20.mp4",
                                      "Video title");
```

### Using gravity sensor to automatically enter fullscreen

```java
JZVideoPlayer.JZAutoFullscreenListener sensorEventListener;
SensorManager sensorManager;

@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    sensorManager = (SensorManager) getSystemService(SENSOR_SERVICE);
    sensorEventListener = new JZVideoPlayer.JZAutoFullscreenListener();
}

@Override
protected void onResume() {
    super.onResume();
    Sensor accelerometerSensor = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
    sensorManager.registerListener(sensorEventListener, accelerometerSensor, SensorManager.SENSOR_DELAY_NORMAL);
}

@Override
protected void onPause() {
    super.onPause();
    sensorManager.unregisterListener(sensorEventListener);
}
```

### Playing video under assets folder

Take a look at [CustomMediaPlayerAssetsFolder class in demo project](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/CustomMediaPlayer/CustomMediaPlayerAssertFolder.java).

> *[Pro-test](https://github.com/Bilibili/ijkplayer/issues/1013) if you pass the parameter `IMediaDataSource` directly, the video will freeze on the first frame and the background will report this error: Please copy to the local path to play.*

### Start playing from progress

After settingUp, set the `seekToInAdvance` variable to set the progress. After the user clicks, it will automatically jump to this progress.

### Save the playback progress

```java
JZVideoPlayer.SAVE_PROGRESS = true
```

### What is the class ActivityMain.MyUserActionStandard in demo project?

This class shows an example of how to capture user events while interacting with the player. Try not to write playback logic here, only events should be logged.

### How to hide ToolBar or Actionbar?

`JZVideoPlayer.ACTION_BAR_EXIST`and `JZVideoPlayer.TOOL_BAR_EXIST` can be manually controlled by these two variables to hide ToolBar and ActionBar.

### Set the aspect ratio

```java
jzVideoPlayer.widthRatio = 16;
jzVideoPlayer.heightRatio = 9;
```