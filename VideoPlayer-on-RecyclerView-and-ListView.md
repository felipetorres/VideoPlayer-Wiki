#### 1. RecyclerView

> *See [AdapterRecyclerViewVideo in demo project](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/AdapterRecyclerViewVideo.java).*

The common usage of RecyclerView has nothing special.

#### 2. ListView

> *See [AdapterVideoList in demo project](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/AdapterVideoList.java).*

```java
@Override
public View getView(int position, View convertView, ViewGroup parent) {

    ViewHolder viewHolder;
    if (null == convertView) {
        viewHolder = new ViewHolder();
        LayoutInflater mInflater = LayoutInflater.from(context);
        convertView = mInflater.inflate(R.layout.item_videoview, null);
        convertView.setTag(viewHolder);
    } else {
        viewHolder = (ViewHolder) convertView.getTag();
    }
    viewHolder.jzVideoPlayer = convertView.findViewById(R.id.videoplayer);
    viewHolder.jzVideoPlayer.setUp(
            videoUrls[position], JZVideoPlayer.SCREEN_WINDOW_LIST,
            videoTitles[position]);
    Glide.with(convertView.getContext())
            .load(videoThumbs[position])
            .into(viewHolder.jzVideoPlayer.thumbImageView);
    viewHolder.jzVideoPlayer.positionInList = position;
    return convertView;
}
```

> *Note: If you want the video to slide out of the list to stop playing, then the list must be multiplexed, because the `setUp` method is called when the list is multiplexed, and the `onStateNormal` function in `setUp` releases the video.*

#### 3. Fragment + ViewPager + ListView

> *See [ActivityListViewFragmentViewPager in demo project](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/ActivityListViewFragmentViewPager.java).*

```java
@Override
public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {

}

@Override
public void onPageSelected(int position) {
    JCVideoPlayer.releaseAllVideos();
}
@Override
public void onPageScrollStateChanged(int state) {

}
```

Based on the default ListView, when you slide ViewPager, the video is released.

> *Note: Do not `releaseAllVideos()` in Fragment's `onPause`. If there are other forms of switch Fragments, `releaseAllVideos()` when switch the Fragment can be called whenever `releaseAllVideos()` is needed.*

#### 4. MultiHolder + ListView

> *See [ActivityListViewMultiHolder in demo project](https://github.com/lipangit/JiaoZiVideoPlayer/blob/develop/app/src/main/java/cn/jzvd/demo/ActivityListViewMultiHolder.java).*

```java
@Override
public View getView(int position, View convertView, ViewGroup parent) {
    //This is the point
    if (convertView != null && convertView.getTag() != null && convertView.getTag() instanceof VideoHolder) {
        ((VideoHolder) convertView.getTag()).jcVideoPlayer.release();
    }
    ......
    return convertView;
}
```

The point is to determine whether the list is multiplexed. Before multiplexing, item is a video item. If it is, then the video has been removed from the list, then it should called `releaseAllVideos()`.