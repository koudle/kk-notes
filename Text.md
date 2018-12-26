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