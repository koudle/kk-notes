# kk's Android notes



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

