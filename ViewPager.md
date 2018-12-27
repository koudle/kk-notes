## ViewPager

### 1. UI刷新

更新PagerAdapter中的数据，发现ViewPager里面的UI没有更新，是因为PagerAdaper里有一个函数`getItemPosition`,默认返回的值是`POSITION_UNCHANGED`，意思是即使你更新的数据，但是position没有发生变化，导致UI没有刷新，这里需要返回`POSITION_NONE`，如下：

```java
public int getItemPosition(Object object){
    return POSITION_NONE;
}
```



### 2.闪屏



### 3.获取当前view

viewpager 的 adapter 里，有一个方法`setPrimaryItem`,所以想获取当前的view可以通过以下方法：

```
private View currentView;

@Override
public void setPrimaryItem(ViewGroup container,int position,Object object) {
    currentView = (View) object;
}

public View getCurrentView(){
    return currentView;
}
```

