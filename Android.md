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

### 2.存储目录

| 方法                                                  | 存储类型 | 存储路径                                                     | 是否需要存储权限 | 应用删除后目录是否保留 |      | api  |
| ----------------------------------------------------- | -------- | ------------------------------------------------------------ | ---------------- | ---------------------- | ---- | ---- |
| context.getCacheDir()                                 | 内部存储 | /data/user/0/com.tencent.huiyin/cache                        | 不需要           | 不保留                 |      | 1    |
| context.getFilesDir()                                 | 内部存储 | /data/user/0/com.tencent.huiyin/files                        | 不需要           | 不保留                 |      | 1    |
| context.getObbDir()                                   | 外部存储 | /storage/emulated/0/Android/obb/com.tencent.huiyin           | 需要             | 不保留                 |      | 11   |
| context.getCodeCacheDir()                             | 内部存储 | /data/user/0/com.tencent.huiyin/code_cache                   | 不需要           | 不保留                 |      | 21   |
| context.getExternalCacheDir()                         | 外部存储 | /storage/emulated/0/Android/data/com.tencent.huiyin/cache    | 需要             | 不保留                 |      | 8    |
| context.getExternalFilesDir("type")                   | 外部存储 | /storage/emulated/0/Android/data/com.tencent.huiyin/files/“type” | 需要             | 不保留                 |      | 8    |
| Environment.getDataDirectory()                        | 内部存储 | /data                                                        | Root             |                        |      | 1    |
| Environment.getDownloadCacheDirectory()               | 内部存储 | /data/cache                                                  | Root             |                        |      | 1    |
| Environment.getExternalStorageDirectory()             | 外部存储 | /storage/emulated/0                                          | 需要             | 保留                   |      | 1    |
| Environment.getExternalStoragePublicDirectory("type") | 外部存储 | /storage/emulated/0/"type"                                   | 需要             | 保留                   |      | 8    |
| Environment.getRootDirectory()                        | 外部存储 | /system                                                      | Root             |                        |      |      |