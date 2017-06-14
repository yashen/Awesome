

<!-- TOC -->

- [前提](#前提)
- [Activity](#activity)
- [ActionBar](#actionbar)
- [菜单](#菜单)
- [列表](#列表)

<!-- /TOC -->
<https://developer.android.com/training/material/index.html>

## 前提
- 最小版本必须是android 5.0 (api 21)以上

## Activity

Activity从[AppCompatActivity](https://developer.android.com/reference/android/support/v7/app/AppCompatActivity.html)继承,它提供了[ActionBar](https://developer.android.com/training/appbar/index.html)方面的能力


基本上来说，所有的Activity都应该有ActionBar,因此application上定义有ActionBar的主题，比如默认的主题是这样定义的

```
    <application
        android:theme="@style/AppTheme">

```

res/values/styles.xml
```
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

</resources>
```

如果不需要AcionBar,那么就为Activity定义没有ActionBar的主题，比如

Theme.AppCompat.Light.NoActionBar

## ActionBar

- 使用getSupportActionBar()方法得到ActionBar对象
- setIcon()设置图标,设置图标后并不会显示图标，必须下面设置为true
- setDisplayShowHomeEnabled 设置图标是否显示
- setDisplayHomeAsUpEnabled 设置不显示图标，显示为返回上级的链接
```
ActionBar bar = getSupportActionBar();
```

当点击返回上级的链接时，必须进行处理，通常这样

```
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()) {
            case android.R.id.home:
                onBackPressed();
                return true;
            default:
                return super.onOptionsItemSelected(item);
        }

    }

```


## 菜单

新的UI没有没有菜单键，都在ActionBar的右侧显示

增加菜单，重写Activity的onCreateOptionsMenu方法

```
    public boolean onCreateOptionsMenu(Menu menu)
    {
        MenuItem setting = menu.add(0, 1, 0, "设置");
        setting.setShowAsAction(MenuItem.SHOW_AS_ACTION_ALWAYS);
        return true;
    }

```

上面是手工添加菜单的做法，但更推荐菜单在资源文件中定义，这样可以单独的编辑菜单的样式等信息

- 创建菜单资源：右键->新建->android resource file，然后Resource Type选择Menu
```
   <?xml version="1.0" encoding="utf-8"?>
   <menu xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android">

        <item
            android:id="@+id/menuitem_setting"
            android:title="设置"
            app:showAsAction="always" />
    </menu>
```
- 在代码中添加菜单

```
    public boolean onCreateOptionsMenu(Menu menu)
    {
        getMenuInflater().inflate(R.menu.login_menu,menu);
        return true;
    }

```

判断菜单点击时使用菜单资源中定义的itemid
```
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()){
            case R.id.menuitem_setting:
                Toast.makeText(this,"setting",Toast.LENGTH_LONG).show();
                return true;
            default:
                return super.onOptionsItemSelected(item);
        }
    }
```


## 列表
<https://developer.android.com/training/material/lists-cards.html>

RecyclerView 小部件比 ListView 更高级且更具灵活性

```
//每项的高度固定时打开此选项以提供性能
recyclerView.setHasFixedSize(true);

//布局管理器
LinearLayoutManager linearLayoutManager = new LinearLayoutManager(this.getContext());
recyclerView.setLayoutManager(linearLayoutManager);


recyclerView.setAdapter(new MyAdapger());

```

```
class MyAdapger extends  RecyclerView.Adapter<MyAdapger.ViewHolder>{}
{
        //同时作为外部类范型的参数
        class ViewHolder extends  RecyclerView.ViewHolder{

            @BindView(R2.id.displayName)
            public TextView DisplayName;
            @BindView(R2.id.description)
            public TextView Description;


            public ViewHolder(View itemView) {
                super(itemView);
                ButterKnife.bind(this,itemView);
            }
        }



        View.OnClickListener mOnItemClickListener = new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                int position = (int) view.getTag();
                //do somethings
            }
        };


        @Override
        public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
            final View v = LayoutInflater.from(parent.getContext())
                    .inflate(R.layout.item_app_list, parent, false);
            v.setOnClickListener(mOnItemClickListener);
            return new ViewHolder(v);
        }

        @Override
        public void onBindViewHolder(ViewHolder holder, final int position) {
            //get data by position
            holder.DisplayName.setText(data.DisplayName);
            holder.Description.setText(data.Description);
            holder.itemView.setTag(position);
        }

        @Override
        public int getItemCount() {
            return dataList.length;
        }

    }

```
