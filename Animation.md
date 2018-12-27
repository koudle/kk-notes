## Animation



### 1. LinearGradient

#### 1.1 构造方法

* 第一种：可以实现多种颜色渐变

`LinearGradient(float x0, float y0, float x1, float y1, int colors[], float positions[], TileMode tile)`

第一个参数为线性起点的x坐标
第二个参数为线性起点的y坐标
第三个参数为线性终点的x坐标
第四个参数为线性终点的y坐标
第五个参数为实现渐变效果的颜色的组合
第六个参数为前面的颜色组合中的各颜色在渐变中占据的位置（比重），如果为空，则表示上述颜色的集合在渐变中均匀出现
第七个参数为渲染器平铺的模式，一共有三种:

1. CLAMP
    边缘拉伸
2. REPEAT
    在水平和垂直两个方向上重复，相邻图像没有间隙
3. MIRROR
    以镜像的方式在水平和垂直两个方向上重复，相邻图像有间隙

* 第二种：只能实现两种颜色渐变

`public LinearGradient(float x0, float y0, float x1, float y1, int color0, int color1, TileMode tile)`

其他参数同上
int color0表示渐变起始颜色
int color1表示渐变终止颜色

* 使用

  ```java
      @Override
      protected void onDraw(Canvas canvas) {
          super.onDraw(canvas);
          Paint paint = new Paint();
          paint.setColor(Color.GREEN);
          LinearGradient linearGradient = new LinearGradient(0, 0, getMeasuredWidth(), 0,new int[]{Color.RED, Color.WHITE, Color.BLUE}, null, LinearGradient.TileMode.CLAMP);
          paint.setShader(linearGradient);
          canvas.drawRect(0,0,getMeasuredWidth(),getMeasuredHeight(),paint);
      }
  ```


#### 1.2 xml

```xml
 <gradient
        android:angle="integer"
        android:centerX="float"
        android:centerY="float"
        android:centerColor="integer"
        android:endColor="color"
        android:gradientRadius="integer"
        android:startColor="color"
        android:type=["linear" | "radial" | "sweep"]
        android:useLevel=["true" | "false"] />
```



属性：

- `android:angle`

  *整型*。渐变的角度（度）。0 为从左到右，90 为从上到上。必须是 45 的倍数。默认值为 0。

- `android:centerX`

  *浮点型*。渐变中心的相对 X 轴位置 (0 - 1.0)。

- `android:centerY`

  *浮点型*。渐变中心的相对 Y 轴位置 (0 - 1.0)。

- `android:centerColor`

  *颜色*。起始颜色与结束颜色之间的可选颜色，以十六进制值或[颜色资源](https://developer.android.com/guide/topics/resources/more-resources.html#Color)表示。

- `android:endColor`

  *颜色*。结束颜色，表示为十六进制值或[颜色资源](https://developer.android.com/guide/topics/resources/more-resources.html#Color)。

- `android:gradientRadius`

  *浮点型*。渐变的半径。仅在 `android:type="radial"` 时适用。

- `android:startColor`

  *颜色*。起始颜色，表示为十六进制值或[颜色资源](https://developer.android.com/guide/topics/resources/more-resources.html#Color)。

- `android:type`

  *关键字*。要应用的渐变图案的类型。有效值为：值说明`"linear"`线性渐变。这是默认值。`"radial"`径向渐变。起始颜色为中心颜色。`"sweep"`流线型渐变。

- `android:useLevel`

  *布尔值*。如果这用作 `LevelListDrawable`，则此值为“true”。

