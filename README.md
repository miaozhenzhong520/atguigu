ViewPagerIndicator的集成步骤
1.下载和解压 下载地址： https://github.com/JakeWharton/ViewPagerIndicator

2.运行案例

3.当前项目关联库

4.写布局文件 <LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
android:orientation="vertical"
android:layoutwidth="fillparent"
android:layoutheight="fillparent">

    <com.viewpagerindicator.TabPageIndicator  
        android:id="@+id/indicator"  
        android:background="@drawable/base_action_bar_bg"  
        android:layout_height="wrap_content"  
        android:layout_width="fill_parent"  
        />  
    <android.support.v4.view.ViewPager  
        android:id="@+id/pager"  
        android:layout_width="fill_parent"  
        android:layout_height="0dp"  
        android:layout_weight="1"  
        />  

</LinearLayout>  
5.使用

  //实例化TabPageIndicator然后设置ViewPager与之关联  
    TabPageIndicator indicator = (TabPageIndicator)findViewById(R.id.indicator);  

    indicator.setViewPager(pager);  

   //如果我们要对ViewPager设置监听，用indicator设置就行了  
6.在适配器中多写

  @Override
    public CharSequence getPageTitle(int position) {
        return  children.get(position).getTitle();
  }
7.设置样式，在工程的功能清单文件，对应的Activity配置样式 <activity android:name=".MainActivity" android:theme="@style/Theme.PageIndicatorDefaults"/>

8.修改样式
9.修改后的 @drawable/vpi_tabindicator
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- Non focused states -->
    <item android:state_focused="false" android:state_selected="false" android:state_pressed="false" android:drawable="@android:color/transparent" />
    <item android:state_focused="false" android:state_selected="true"  android:state_pressed="false" android:drawable="@drawable/news_tab_item_bg_select" />

    <!-- Focused states -->
    <item android:state_focused="true" android:state_selected="false" android:state_pressed="false" android:drawable="@android:color/transparent" />
    <item android:state_focused="true" android:state_selected="true"  android:state_pressed="false" android:drawable="@drawable/news_tab_item_bg_select" />

<!-- Pressed -->
<!--    Non focused states -->
<item android:state_focused="false" android:state_selected="false" android:state_pressed="true" android:drawable="@android:color/transparent" />
<item android:state_focused="false" android:state_selected="true"  android:state_pressed="true" android:drawable="@drawable/news_tab_item_bg_select" />

<!--    Focused states -->
<item android:state_focused="true" android:state_selected="false" android:state_pressed="true" android:drawable="@android:color/transparent" />
<item android:state_focused="true" android:state_selected="true"  android:state_pressed="true" android:drawable="@drawable/news_tab_item_bg_select" />
10.文字颜色
@drawable/vpitabtextcolorindicator
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- Non focused states -->
    <item android:state_focused="false" android:state_selected="false" android:state_pressed="false" android:color="#000000" />
    <item android:state_focused="false" android:state_selected="true"  android:state_pressed="false" android:color="#ff0000" />

    <!-- Focused states -->
    <item android:state_focused="true" android:state_selected="false" android:state_pressed="false" android:color="#000000" />
    <item android:state_focused="true" android:state_selected="true"  android:state_pressed="false" android:color="#ff0000" />

    <!-- Pressed -->
    <!--    Non focused states -->
    <item android:state_focused="false" android:state_selected="false" android:state_pressed="true" android:color="#000000" />
    <item android:state_focused="false" android:state_selected="true"  android:state_pressed="true" android:color="#ff0000" />

    <!--    Focused states -->
    <item android:state_focused="true" android:state_selected="false" android:state_pressed="true" android:color="#000000" />
    <item android:state_focused="true" android:state_selected="true"  android:state_pressed="true" android:color="#ff0000" />
</selector>
顶部新闻轮播图事件处理的原理
一.竖直方向滑动，不做处理 设置是否拦截事件为 getParent().requestDisallowInterceptTouchEvent(false);
二.水平方向滑动 1.当滑动到第一个页面，并且方向是从左到右的滑动 endX - startX > 0 那么方向就是：从左往右滑动 getParent().requestDisallowInterceptTouchEvent(false);
2.当滑动到最后一个页面的时候，并且方向是从右到左滑动 endX - startX < 0 那么方向就是：从右往左滑动 getParent().requestDisallowInterceptTouchEvent(false);
3.其他情况 getParent().requestDisallowInterceptTouchEvent(true);
