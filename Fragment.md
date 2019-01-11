## Fragment

![Fragment的生命周期](https://developer.android.com/images/fragment_lifecycle.png?hl=zh-cn)

### 1.Fragment里的view复用

Fragment执行onDestoryView，和Activity的onDestory不一样，不会销毁当前的页面，所以view和Fragment的所有成员变量的引用都在,这样在Fragment页面恢复，调用onCreateView的时候，没有必要重新inflate新的view，直接复用之前inflate的view，具体操作如下：

1. 首先，在onDestoryView里要把rootView从其parent里移除

   ```java
       @Override
       public void onDestroyView() {
           super.onDestroyView();
           ((ViewGroup)rootView.getParent()).removeView(rootView);
       }
   ```

2. 在onCreateView里如下判断

   ```java
       @Nullable
       @Override
       public View onCreateView(LayoutInflater inflater, @Nullable ViewGroup container, Bundle savedInstanceState) {
           if(rootView == null) {
               rootView = inflater.inflate(R.layout.layout_fragment_square, container, false);
               initView(rootView);
           }
   
           logger.info("onCreateView");
           return rootView;
       }
   ```



## 2.ViewPager中使用Fragment的问题

ViewPager中可以使用Fragment，用FragmentPagerAdapter，但是有一个问题，Fragment用在ViewPager中是作为一个View添加进去的，导致Fragment的声明周期异常，例如ViewPager中，有A、B两个Fragment，当ViewPager加载时：

1、A、B两个Fragment会同时加载，而且都会执行onResume

2、滑动View，让A消失，B出现，A也不会执行onPause

3、打开另一个Activity，A、B都会执行onPause，在返回时，A、B都会执行onResume，即使只有一个看的见

这样会让依赖Fragment声明周期处理一些逻辑的会异常，怎么做呢，用Fragment中的`setUserVisibleHint(boolean isVisibleToUser)`这个函数



### 2.1 在Fragment里Override setUserVisibleHint

```
@Override
    public void setUserVisibleHint(boolean isVisibleToUser) {
        super.setUserVisibleHint(isVisibleToUser);
        logger.debug("isVisibleToUser:{}",isVisibleToUser);
        //根据isVisibleToUser  来判断 onPause和onResume
        if(isVisibleToUser) {
        	//onResume
        }else {
           //onPause
        }            
    }
```

### 2.2 在ViewPager里监听Fragment的显示情况

```
viewPager.setOnPageChangeListener(new ViewPager.OnPageChangeListener() {
            @Override
            public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {

            }

            @Override
            public void onPageSelected(int position) {
                if(position == 0){
                    fragment.setUserVisibleHint(true);
                }else {
                    fragment.setUserVisibleHint(false);
                }
            }

            @Override
            public void onPageScrollStateChanged(int state) {

            }
        });
```



