# kk's Android notes



## Thread





## File



### 1. 路径

`getPath()`

* 返回的是定义时的路径，可能是相对路径，也可能是绝对路径，这个取决于定义时用的是相对路径还是绝对路径。

`getAbsolutePath()`

* 返回的是定义时的路径对应的相对路径，但不会处理“.”和“..”的情况

`getCanonicalPath()`

* 返回的是规范化的绝对路径，相当于将getAbsolutePath()中的“.”和“..”解析成对应的正确的路径



举例如下：

```java
File file = new File(".\\test.txt"); 
System.out.println(file.getPath()); 
System.out.println(file.getAbsolutePath()); 
System.out.println(file.getCanonicalPath()); 
```

返回的结果为：

```shell
.\test.txt 
E:\workspace\Test\.\test.txt 
E:\workspace\Test\test.txt 
```

### 2.存储目录

| 方法                                                  | 存储类型 | 存储路径                                           | 是否需要存储权限 | 应用删除后目录是否保留 |      | api  |
| ----------------------------------------------------- | -------- | -------------------------------------------------- | ---------------- | ---------------------- | ---- | ---- |
| context.getCacheDir()                                 | 内部存储 | /data/user/0/包名/cache                            | 不需要           | 不保留                 |      | 1    |
| context.getFilesDir()                                 | 内部存储 | /data/user/0/包名/files                            | 不需要           | 不保留                 |      | 1    |
| context.getObbDir()                                   | 外部存储 | /storage/emulated/0/Android/obb/包名               | 需要             | 不保留                 |      | 11   |
| context.getCodeCacheDir()                             | 内部存储 | /data/user/0/包名/code_cache                       | 不需要           | 不保留                 |      | 21   |
| context.getExternalCacheDir()                         | 外部存储 | /storage/emulated/0/Android/data/包名/cache        | 需要             | 不保留                 |      | 8    |
| context.getExternalFilesDir("type")                   | 外部存储 | /storage/emulated/0/Android/data/包名/files/“type” | 需要             | 不保留                 |      | 8    |
| Environment.getDataDirectory()                        | 内部存储 | /data                                              | Root             |                        |      | 1    |
| Environment.getDownloadCacheDirectory()               | 内部存储 | /data/cache                                        | Root             |                        |      | 1    |
| Environment.getExternalStorageDirectory()             | 外部存储 | /storage/emulated/0                                | 需要             | 保留                   |      | 1    |
| Environment.getExternalStoragePublicDirectory("type") | 外部存储 | /storage/emulated/0/"type"                         | 需要             | 保留                   |      | 8    |
| Environment.getRootDirectory()                        | 外部存储 | /system                                            | Root             |                        |      |      |



## Text

### 1. 测量文字的宽度和高度

#### 1.1 Paint.measureText （测量文本的宽度）

```java
Paint paint = new Paint();
paint.setTextSize(size);
float strWidth = paint.measureText(str);
```

#### 1.2 Paint.getTextBounds (获得文字所在矩形区域，可以得到宽高)

```java
Paint paint = new Paint();
Rect rect = new Rect();  
paint.getTextBounds(str, 0, str.length(), rect);  
int w = rect.width();  
int h = rect.height();
```

#### 1.3 通过Paint.FontMetrics or Paint.FontMetricsInt来获取高度

这两者的含义相同，只不过精度不同，一个float、一个int。

```java
Paint paint = new Paint();
paint.setTextSize(size);//设置字体大小
paint.setTypeface(Typeface.xx);//设置字体
FontMetrics fontMetrics = getFontMetrics();
float height1 = fontMetrics.descent - fontMetrics.ascent;
float height2 = fontMetrics.bottom - fontMetrics.top;
```





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







## 序列化

### 1.Serializable

#### 1.1 使用方法

实现`Serializable`接口



### 2.Parcelable

#### 2.1 使用方法

实现`Parcelable`接口

Parceable的代码可以由Android Studio自动生成，或者点击 `Code ` -> `Generate`  

### 3. JSON

#### 3.1 使用方法

使用`Gson`或者`FastJson`



### 4. 比较



#### 4.1 Serializable 与 Parcelable的比较

* 1）在使用内存的时候，Parcelable比Serializable性能高，所以推荐使用Parcelable。
* 2）Serializable在序列化的时候会产生大量的临时变量，从而引起频繁的GC。
* 3）Parcelable不能使用在要将数据存储在磁盘上的情况，因为Parcelable不能很好的保证数据的 持续性在外界有变化的情况下。尽管Serializable效率低点，但此时还是建议使用Serializable。

