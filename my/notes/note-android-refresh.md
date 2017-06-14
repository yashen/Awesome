## 下拉刷新

下拉刷新使用SwipeRefreshLayout

布局设计中目前没有这个控件，因此使用View指定

```
    <view
        android:id="@+id/swipeRefreshLayout"
        class="android.support.v4.widget.SwipeRefreshLayout"
        layout_width="match_parent">
        <android.support.v7.widget.RecyclerView
            android:id="@+id/recyclerView"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

        </android.support.v7.widget.RecyclerView>

    </view>

```

使用此控件后下拉就会出现一个等待图标在界面上,需要刷新完成后取消

```
        swipeRefreshLayout.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener() {
            @Override
            public void onRefresh() {
                ...
                swipeRefreshLayout.setRefreshing(false);
                ...
            }
        });
```