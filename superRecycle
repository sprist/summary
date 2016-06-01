#superRecycle

Download
--------

Download grab via Maven:
```xml
<dependency>
  <groupId>com.apcan.sprist</groupId>
  <artifactId>superRecycler</artifactId>
  <version>1.0.2</version>
</dependency>
```
or Gradle:
```groovy
compile 'com.apcan.sprist:superRecycler:1.0.2'
```

For the SNAPSHOT version:
```xml
<dependency>
  <groupId>com.apcan.sprist</groupId>
  <artifactId>superRecycler</artifactId>
  <version>1.0.2</version>
</dependency>
```
or Gradle:
```groovy
allprojects {
  repositories {
           maven { url "http://www.apcan.cn:8081/nexus/content/groups/AndroidSnapshot/" }
  }
}
```
```groovy
dependencies {
  compile 'com.apcan.sprist:superRecycler:1.0.2'
}
```

使用
--------

1.提供2个ui布局可供使用
--------

```xml
<com.pacific.recyclerview.SuperRecyclerView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/rclv"
    style="@style/RecyclerView"
    app:layout_empty="@layout/layout_http_data_empty"
    app:layout_moreProgress="@layout/layout_ui_recycle_foot" />
    ```

-  第2个增加了header跟footer可以自定义

```xml
<com.pacific.recyclerview.SuperScrollRecyclerView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/rclv"
    style="@style/RecyclerView"
    app:layout_empty="@layout/layout_http_data_empty"
    app:layout_moreProgress="@layout/layout_ui_recycle_foot" />
    ```

2.相关属性支持
--------
```xml
        <attr name="layout_empty" format="reference" />
        <attr name="layout_header" format="reference" />
        <attr name="layout_footer" format="reference" />
        <attr name="layout_moreProgress" format="reference" />
        <attr name="layout_progress" format="reference" />
        <attr name="layoutProgressShow" format="boolean" />
        <attr name="recyclerClipToPadding" format="boolean" />
        <attr name="recyclerPadding" format="dimension" />
        <attr name="recyclerPaddingTop" format="dimension" />
        <attr name="recyclerPaddingBottom" format="dimension" />
        <attr name="recyclerPaddingLeft" format="dimension" />
        <attr name="recyclerPaddingRight" format="dimension" />
        <attr name="scrollbarStyle">
            <flag name="insideOverlay" value="0x0" />
            <flag name="insideInset" value="0x01000000" />
            <flag name="outsideOverlay" value="0x02000000" />
            <flag name="outsideInset" value="0x03000000" />
        </attr>
        <attr name="mainLayoutId" format="reference" />
```

3.adapter方法实现类
--------
```java
public abstract class RecyclerAdapter<T> extends BaseRecyclerAdapter<T, RecyclerAdapterHelper> {

    public RecyclerAdapter(Context context, @NonNull int... layoutResIds) {
        super(context, layoutResIds);
    }

    public RecyclerAdapter(Context context, @Nullable List<T> data, @NonNull int... layoutResIds) {
        super(context, data, layoutResIds);
    }

    @Override
    protected RecyclerAdapterHelper getAdapterHelper(ViewHolder viewHolder) {
        return RecyclerAdapterHelper.get(viewHolder);
    }

}
```
- 自定义添加filter

```java
public abstract class RecyclerFilterAdapter<T> extends BaseRecyclerAdapter<T, RecyclerAdapterHelper> implements Filterable, FilterCallBack {
    RecycleFilter filter;

    public RecyclerFilterAdapter(Context context, @NonNull int... layoutResIds) {
        super(context, layoutResIds);
    }

    public RecyclerFilterAdapter(Context context, @Nullable List<T> data, @NonNull int... layoutResIds) {
        super(context, data, layoutResIds);
    }

    @Override
    protected RecyclerAdapterHelper getAdapterHelper(ViewHolder viewHolder) {
        return RecyclerAdapterHelper.get(viewHolder);
    }

    public RecyclerFilterAdapter(Context context, @Nullable List<T> data, @NonNull int layoutResIds, RecycleFilter filter) {
        super(context, data, layoutResIds);
        this.filter = filter;

    }

    @Override
    public Filter getFilter() {
        filter.setFilterCallBack(this);
        return filter;
    }


    @Override
    public void publishResults(List<BaseFilterModel> results) {
        clear();
        addAll((List<T>) results);
    }
}

```

4.adapter使用案例
--------
```java
   adapter = new RecyclerAdapter<ListItemIdName>(this, t, R.layout.list_item_ui_single_line_text) {
            @Override
            protected void convert(RecyclerAdapterHelper helper, final ListItemIdName item) {
                helper.setText(R.id.tv_name, item.name).getItemView().setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {
                        Intent intent = new Intent(FacultyListActivity.this, DoctorListActivity.class);
                        intent.putExtra("id", item.id);
                        startActivity(intent);
                    }
                });

            }
        };
        rclv.setAdapter(adapter);
        ```
