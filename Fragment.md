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