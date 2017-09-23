#### 1. 添加gradle引用

```gradle
compile 'cn.jzvd:jiaozivideoplayer:x.x.x'
```

不建议修改库或者引入jar、aar等其他引用方式，因为咱们这个库基本两个礼拜会发一个版本，或者改bug，或者加功能，如果改库的话升级会很麻烦，继承JCVideoPlayerStandard几乎可以满足几乎所有的改功能和改UI的需求。

#### 2. 添加布局

```xml
<fm.jiecao.jcvideoplayer_lib.JCVideoPlayerStandard
    android:id="@+id/videoplayer"
    android:layout_width="match_parent"
    android:layout_height="200dp"/>
```

可以在任何布局里添加，宽度和高度也可以自己定义成任何数值，也可以改成[特定的比例](http://github.com)，无论高宽如何变化，图像都会是居中的，并且高或宽至少两个边充满全屏，如果视频的长宽比例和屏幕的长宽比例不同，就会有黑边，可以复写onVideoSizeChanged函数，修改textureView的大小消除黑边，如果有条件的话可以固定视频源和控件的比例都是16:9或者4:3，这样会更方便。

#### 3. 设置视频地址、缩略图地址、标题

```java
JCVideoPlayerStandard jcVideoPlayerStandard = (JCVideoPlayerStandard) findViewById(R.id.videoplayer);
jcVideoPlayerStandard.setUp("http://2449.vod.myqcloud.com/2449_22ca37a6ea9011e5acaaf51d105342e3.f20.mp4"
                            , JCVideoPlayerStandard.SCREEN_LAYOUT_NORMAL, "嫂子闭眼睛");
jcVideoPlayerStandard.thumbImageView.setImage("http://p.qpic.cn/videoyun/0/2449_43b6f696980311e59ed467f22794e792_1/640");
```

- 第一行是取得控件实例，用代码new新的实例也可以，然后是setUp函数，设置控件播放时所需的参数，第一个参数表示播放的地址，如果有多个播放地址也可以把播放地址放到map中(可以参照ApiActivity)
- 第二行参数表示控件使用的位置，分别是普通、列表、全屏、小窗，最后一个参数是Oject[]数组，存放其他可能用到的数据，比如播放量，视频的分类信息等，默认只有标题
- 最后一行是设置缩略图，ImageView本来并没有setImage函数，这个函数只是告诉大家可以满足设置缩略图的需要，根据自己项目中的图片加载框架设置缩略图，参照demo的ApiActivity，有ImageLoader、Glide等例子

#### 4. 在包含播放控件的Activity中加入如下代码

```java
@Override
public void onBackPressed() {
    if (JCVideoPlayer.backPress()) {
        return;
    }
    super.onBackPressed();
}
@Override
protected void onPause() {
    super.onPause();
    JCVideoPlayer.releaseAllVideos();
}
```

- backPress函数判断了点击回退按钮的相应，如果全屏会退出全屏播放，如果不是全屏则会交给Activity
- 当Activity的生命周期进入onPause之后会releaseAllVideos，因为我们设定当用户退出当前Activity或者按Home键之后会视频就会release。也可以参照网上朋友给的[代码](https://github.com/lipangit/JieCaoVideoPlayer/issues/1122#issuecomment-321146486)，退出之后还能继续播放。

这些代码只需要在Activity的生命周期使用，如果是Fragment和ViewPaver等嵌套，不需要复写Fragment的onPause函数，也只需要复写包含播放控件的Fragment的Activity的onPause和onBackPressed函数。

#### 5. 包含控件的Activity在Manifest中的设置

```xml
<activity
    android:name=".MainActivity"
    android:configChanges="orientation|screenSize|keyboardHidden"
    android:screenOrientation="portrait" /> <!-- or android:screenOrientation="landscape"-->
```
- android:configChanges 保证了在全屏的时候横竖屏切换不会执行Activity的相关生命周期，打断视频的播放
- android:screenOrientation 固定了屏幕的初始方向，可以参照demo中JCVideoPlayer.FULLSCREEN_ORIENTATION和JCVideoPlayer.NORMAL_ORIENTATION两个变量的使用，这两个变量控制全屏后和退出全屏的屏幕方向

