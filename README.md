# 目录
- [kotlin与java的区别](#kotlin与java的区别)
- [kotlin相关教程及资料](#kotlin相关教程及资料)
- 问题点：
  1.  如何与java混用
  2.  内存回收上是否还是过jvm的gc
  3.  相对java优化了什么
  4.  表达式与语句
[1](https://www.jianshu.com/p/5b1e142722b0)
[2](https://www.kotlincn.net/docs/reference/control-flow.html)
  5.  高阶函数和lambda表达式
  6.  [标签](https://www.jianshu.com/p/5ac50d5efba2)
  7.  库函数
  8.  类的构造函数和构造器
  9.  [伴生对象](https://zhuanlan.zhihu.com/p/26713535)
  10. [扩展函数](https://www.kotlincn.net/docs/reference/extensions.html)

    `Kotlin允许开发者在不改变已有类的情况下，为某个类添加新的函数。这个特性叫做扩展函数。
    举一个简单的例子。如果要关闭一个I/O流，使用Java可能是写一个工具方法`
    ```
    /**
     * 安全关闭io流
     * @param closeable
     */
    public static void closeQuietly(Closeable closeable) {
        if (closeable != null) {
            try {
                closeable.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    ```
    `复制代码对Kotlin而言，可以对Closeable扩展一个函数closeQuietly()`
    ```
    fun Closeable?.closeQuietly() {
        try {
            this?.close()
        } catch (e: Throwable) {
        }
    }
    ```
    `复制代码之后，任何实现了Closeable接口的类，都可以使用它本身的closeQuietly()方法来关闭流。我们不再需要那个工具方法了`
    
    其实**扩展并不是反射，只是利用kotlin的lambda表达式特性而已**

  11. [幕后字段](https://juejin.im/post/5b95321ae51d450e6475b7c6)
  12. [委托属性](https://www.kotlincn.net/docs/reference/delegated-properties.html)


## kotlin与java的区别
  1.  **val** <==> **final**
  2.  定义变量 **var** ，无初始值时需要赋予数据类型
  3.  定义函数 **fun** ，**Unit**返回类型的返回的是无意义的值，可以直接忽略 , 在返回类型后面加上 **?** 则表示可能返回null
  4.  打印变量 **\$** ，打印集合中的某个变量 **${list[index]}**
  5.  **is** <==> **instance of**
  6.  **for in** <==> **增强for** 
  7.  **index** 为 **for in** 和 **while** 的关键字，意为序号， **list.indices** 为 **for in** 的索引集 
  8.  **in** 为区间检测
    ````
    /* 使用范例 */
    val list = listOf("a", "b", "c")
    if (-1 !in 0..list.lastIndex) {
        println("-1 is out of range")
    }
    if (list.size !in list.indices) {
        println("list size is out of valid list indices range, too")
    }
    for (index in list.indices){
        println(" value is ${list[index]} ")
    }
    ````
  
  9.  不再使用 **new** 创建类
  10.  **when** <==> **switch** ， 除非能保证**所有case都包含**了，否则else是必备的
  11.  kotlin存在一个[装箱](https://blog.csdn.net/zxm317122667/article/details/78223282)的概念，所以存在一个 **===** 的判断，需要注意**同一性**和**相等性**
  12. 基础类型中 `较小的类型不能隐式转换为较大的类型`，所以进行转换的时候就需要用到
    ````
    toByte(): Byte
    toShort(): Short
    toInt(): Int
    toLong(): Long
    toFloat(): Float
    toDouble(): Double
    toChar(): Char
    ````
  
  13.  运算操作符
    ````
    （只用于 Int 与 Long）
    shl(bits) – 有符号左移 (Java 的 <<)
    shr(bits) – 有符号右移 (Java 的 >>)
    ushr(bits) – 无符号右移 (Java 的 >>>)
    and(bits) – 位与z
    or(bits) – 位或
    xor(bits) – 位异或
    inv() – 位非
    ```` 

  14.  数组 **Array**，库函数 **arrayOf()** 创建数组，库函数 **arrayOfNulls()** 创建一个指定大小，所有元素都为空的数组，另一种创建方式：
    ````
    fun main() {
        // 创建一个 Array<String> 初始化为 ["0", "1", "4", "9", "16"]
        val asc = Array(5) { 
            j -> (j * j).toString() 
        }
        asc.forEach { println(it) }
    }
    ````

  15.  [@JvmOverloads](https://www.jianshu.com/p/72d1959a7c56)
  16.  **const** <==> **final**
  17. **open** 在kotlin允许被继承时就需要用此修饰符修饰类
  18. **data**修饰符专门用于修饰数据model类，可以继承**sealed**类
  19. **sealed**修饰符专门用于修饰密封类，也就是类继承受限


## kotlin相关教程及资料
-  [google的kotlin实例](https://developer.android.com/samples/index.html?language=kotlin)
-  [kotlin的官方教程（英文）](https://kotlinlang.org/docs/reference/)
-  [kotlin的官方教程（中文）](https://www.kotlincn.net/docs/reference/)
-  [kotlin语法](https://www.kotlincn.net/docs/reference/grammar.html#ifExpression)
-  [kotlin关键字和操作符](https://www.kotlincn.net/docs/reference/keyword-reference.html)
-  高效kotlin开发
    1.  [1](https://juejin.im/post/5ade9ce3f265da0b80705e22)
    2.  [2](https://juejin.im/post/5ae31d85518825671c0e4b83)
    3.  [3](https://juejin.im/post/5afb95616fb9a07acd4de5b0)
    4.  [4](https://juejin.im/post/5b076911f265da0de2575131)
    5.  [5](https://juejin.im/post/5b30de416fb9a00e9c47de55)


