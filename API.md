> 直接进入全屏

```java
JCVideoPlayerStandard.startFullscreen(this, JCVideoPlayerStandard.class, "http://2449.vod.myqcloud.com/2449_22ca37a6ea9011e5acaaf51d105342e3.f20.mp4", "嫂子辛苦了");
```

重力感应自动进入全屏
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

播放Assets文件夹下的视频
```
请先拷贝到本地路径再播放.[亲测](https://github.com/Bilibili/ijkplayer/issues/1013)如果直接传参数IMediaDataSource,只停留在第一帧画面上并且后台会报错
```
