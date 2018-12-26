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