> 代码播放视频

```java
jcVideoPlayer.startButton.performClick();//模拟用户点击开始按钮，NORMAL状态下点击开始播放视频，播放中点击暂停视频
```

> 直接进入全屏

```java
JCVideoPlayerStandard.startFullscreen(this, JCVideoPlayerStandard.class, "http://2449.vod.myqcloud.com/2449_22ca37a6ea9011e5acaaf51d105342e3.f20.mp4", "嫂子辛苦了");
```

> 重力感应自动进入全屏

```java
JCVideoPlayer.JCAutoFullscreenListener sensorEventListener;
SensorManager                          sensorManager;
@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    sensorManager = (SensorManager) getSystemService(SENSOR_SERVICE);
    sensorEventListener = new JCVideoPlayer.JCAutoFullscreenListener();
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

> 播放Assets文件夹下的视频

[亲测](https://github.com/Bilibili/ijkplayer/issues/1013)如果直接传参数IMediaDataSource,只停留在第一帧画面上并且后台会报错
```
请先拷贝到本地路径再播放
```

> 点击开始播放直接跳转到某个进度

    setUp之后设置seekToInAdvance变量设置进度，用户点击之后会自动跳转到此进度

> 循环播放

    setUp之后设置looping = true

> DEMO中MainActivity的MyJCBuriedPointStandard类

    这是埋点统计用来记录用户的事件，这里只记录事件，尽量不要将播放逻辑写到这里

> ToolBar和Actionbar显示隐藏的问题

    JCVideoPlayer.ACTION_BAR_EXIST
    JCVideoPlayer.TOOL_BAR_EXIST
    可以通过这两个变量手动控制是否隐藏ToolBar和ActionBar