[TOC]

# 概述

## Kotlin for Android
Kotlin是开发Android应用的一个非常好的工具。它把高级语言的所有优点带给Android平台，并且不引入任何新的限制。

- **兼容性** Kotlin全面兼容JDK6， 确保Kotlin应用可以在旧的Android设备上运行，没有任何问题。Kotlin工具在Android Studio中得到完全支持，并与Android构建系统兼容。
- **性能** 得益于极其相似的字节码结构，Kotlin应用与一个等价的Java应用运行得一样快。有了Kotlin的内联函数支持，使用lambda表达式的代码通常比用Java编写的同样代码要运行得更快。
- **互操作性** Kotlin与Java可以实现100%互操作性，在Kotlin应用中可以使用所有现有的Andorid库。这包括了注解处理、数据绑定和Dagger。
- **Footprint** Kotlin有一个非常紧凑的运行时库，通过使用ProGuard可以使其进一步紧缩。在[真实应用](https://blog.gouline.net/kotlin-production-tales-62b56057dc8a)中，Kotlin运行时仅增减了几百个方法，对apk文件体积的增加不到100K。
- **编译时间** Kotlin支持高效的增量编译，因此虽然对于干净构建会有一些额外的开销，[但增量构建通常和Java一样快或者更快](https://medium.com/keepsafe-engineering/kotlin-vs-java-compilation-speed-e6c174b39b5d)。
- **学习曲线** 对于Java开发者，开始使用Kotlin是非常容易的。Kotlin插件中包含的自动化的Java to Kotlin转换器将帮助你开始前几步。[Kotlin Koans](https://kotlinlang.org/docs/tutorials/koans.html)通过一系列交互练习，提供了一个关于该语言关键特性的指南。

### Kotlin for Android案例学习

Kotlin已经被大多数公司成功引入，其中一些公司分享了它们的经验：

- Pinterest已经成功地[将Kotlin引入](https://www.youtube.com/watch?v=mDpnc45WwlI)到它们月活150M的应用上。
- Basecamp的Android应用是[100%的Kotlin代码](https://m.signalvnoise.com/how-we-made-basecamp-3s-android-app-100-kotlin-35e4e1c0ef12)，他们反映在程序员的快乐程度和工作质量和速度上有了很大改善。
- Keesafe的App Lock应用同样[100%转换到了Kotlin](https://medium.com/keepsafe-engineering/lessons-from-converting-an-app-to-100-kotlin-68984a05dcb6)，这使得代码行数减少了30%，方法数量减少了10%。

### Android开发工具

Kotlin团队为Android开发提供了一套超越标准语言特性的工具：

- [Kotlin Android Extensions](https://kotlinlang.org/docs/tutorials/android-plugin.html)是一个编译器拓展，它可以让你去掉代码中的`findViewById()`调用，同时用合成编译器生成属性替代它们。
- [Anko](http://github.com/kotlin/anko)是一个库，它提供一组Kotlin友好的Android API封装，同时提供一个DSL允许你用Kotlin代码替换xml布局文件。

### 接下来几步

- 下载安装Android Studio 3.0，它包含了Kotlin支持。
- 按照[Getting started with Android and Kotlin](https://kotlinlang.org/docs/tutorials/kotlin-android.html)教程，创建你的第一个Kotlin应用。
- 更深入的介绍，参考本网站的[参考文档](https://kotlinlang.org/docs/reference/index.html)和[Kotlin Koans](https://kotlinlang.org/docs/tutorials/koans.html)。
- 另一个好资源是[Kotlin for Android Developers](https://leanpub.com/kotlin-for-android-developers)，这本书教你一步一步创建一个正真的使用Kotlin的Android应用。
- 参看谷歌[用Kotlin编写的示例工程](https://developer.android.com/samples/index.html?language=kotlin)。

## Kotlin for Native

Kotlin/Native是一种将Kotlin代码编译为本地二进制文件的技术，它可以在不使用虚拟机的情况下运行。它是一个基于[LLVM](https://llvm.org/)的后端，用于Kotlin编译器和Kotlin标准库的本机实现。

### 为什么使用Kotlin/Native?

Kotlin/Native主要设计用于编译虚拟机不理想或不可能实现的平台，例如嵌入式设备或iOS。它解决了开发人员需要生成自包含程序而不需要额外的运行时或虚拟机的情况。

### 目标平台

Kotlin/Native支持以下平台：

- iOS(arm32, arm64, emulator x86_64)
- MacOS(x86_64)
- Android(arm32, arm64)
- Windows(mingw x86_64)
- Linux(x86_64, arm32, MIPS, MIPS little endian)
- WebAssembly(wasm32)

### 互操作性

Kotlin/Native支持与Native的双向互操作。一方面，编译器创建：

- 许多[平台](https://kotlinlang.org/docs/reference/native-overview.html#target-platforms)的可执行文件
- C/C++项目的带C头文件的静态库或[动态](https://kotlinlang.org/docs/tutorials/native/dynamic-libraries.html)库
- 用于Swift和Objective-C项目的[Apple framework](https://kotlinlang.org/docs/tutorials/native/apple-framework.html)

另一方面，Kotlin/Native支持从Kotlin/Native直接使用现有库的互操作性：

- 静态或动态[C库](https://kotlinlang.org/docs/reference/native/c_interop.html)
- C，[Swift，Objective-C](https://kotlinlang.org/docs/reference/native/objc_interop.html)框架

将编译好的Kotlin代码整合进用C，C++，Swift，Objective-C等其它语言编写的现有工程，是很容易的。同样，从Kotlin/Native直接使用现有的本地代码、静态或动态[C库](https://kotlinlang.org/docs/reference/native/c_interop.html)，Swift/Objective-C[框架](https://kotlinlang.org/docs/reference/native/objc_interop.html)、图形引擎和其它任何东西，都是非常容易的。

Kotlin/Native[库](https://kotlinlang.org/docs/reference/native/platform_libs.html)有助于工程之间共享Kotlin代码。POSIX, gzip, OpenGL, Metal, Foundation, 以及很多其它流行的库和苹果架构都被预导入，作为Kotlin/Native库包含在编译器中。

### 跨平台共享代码

在不同的Kotlin和Kotlin/Native目标之间支持[多平台项目](https://kotlinlang.org/docs/reference/multiplatform.html)。这是在多个平台之间共享Kotlin代码的方法，包括Android，iOS，服务端，JVM，客户端，JavaScript，CSS和native

[多平台项目](https://kotlinlang.org/docs/reference/multiplatform.html)为基本Kotlin代码提供必要的APIs，实现用Kotlin一次性开发项目的共享部分，并在所有目标平台之间共享。

### 如何开始

#### 教程和文档

初识Kotlin？看一下[Getting Started](#开始)页面。

推荐文档页：

- [C interop](https://kotlinlang.org/docs/reference/native/c_interop.html)
- [Swift/Objective-C interop](https://kotlinlang.org/docs/reference/native/objc_interop.html)

推荐教程：

- [A basic Kotlin/Native application](https://kotlinlang.org/docs/tutorials/native/basic-kotlin-native-app.html)
- [Multiplatform Project: iOS and Android](https://kotlinlang.org/docs/tutorials/native/mpp-ios-android.html)
- [Types mapping between C and Kotlin/Native](https://kotlinlang.org/docs/tutorials/native/mapping-primitive-data-types-from-c.html)
- [Kotlin/Native as a Dynamic Library](https://kotlinlang.org/docs/tutorials/native/dynamic-libraries.html)
- [Kotlin/Native as an Apple Framework](https://kotlinlang.org/docs/tutorials/native/apple-framework.html)

#### 示例工程：

- [Kotlin/Native sources and examples](https://github.com/JetBrains/kotlin-native/tree/master/samples)
- [KotlinConf app](https://github.com/JetBrains/kotlinconf-app)
- [KotlinConf Spinner app](https://github.com/jetbrains/kotlinconf-spinner)
- [Kotlin/Native sources and examples (.tgz)](https://download.jetbrains.com/kotlin/native/kotlin-native-samples-1.0.1.tar.gz)
- [Kotlin/Native sources and examples (.zip)](https://download.jetbrains.com/kotlin/native/kotlin-native-samples-1.0.1.zip)

更多示例参见 [GitHub](https://github.com/JetBrains/kotlin-examples)

## 协程(Coroutines)

异步或非阻塞编程已经是新的事实 。不管我们创建服务端、桌面或移动应用，重要的是我们提供的体验不仅从用户的角度来说是流动的，而且在需要的时候是可伸缩的。

针对这个问题，有很多解决方案。在Kotlin中，我们采用了一种非常灵活的方式，即在语言级别提供[协程](https://en.wikipedia.org/wiki/Coroutine)支持，并将大部分功能委托给库，这与Kotlin的理念非常一致。

作为额外的好处，协程不仅为异步编程打开了大门，而且还提供了许多其他的可能性，例如并发性、参与者等。

### 如何开始

#### 教程和文档

初识Kotlin？看一下[Getting Started](#开始)页面。

推荐文档页：

- [Coroutines Guide](https://kotlinlang.org/docs/reference/coroutines/coroutines-guide.html)
- [Basics](https://kotlinlang.org/docs/reference/coroutines/basics.html)
- [Channels](https://kotlinlang.org/docs/reference/coroutines/channels.html)
- [Coroutine Context and Dispatchers](https://kotlinlang.org/docs/reference/coroutines/coroutine-context-and-dispatchers.html)
- [Shared Mutable State and Concurrency](https://kotlinlang.org/docs/reference/coroutines/shared-mutable-state-and-concurrency.html)

推荐教程：

- [Your first coroutine with Kotlin](https://kotlinlang.org/docs/tutorials/coroutines/coroutines-basic-jvm.html)
- [Asynchronous Programming](https://kotlinlang.org/docs/tutorials/coroutines/async-programming.html)

#### 示例工程

- [kotlinx.coroutines Examples and Sources](https://github.com/Kotlin/kotlin-coroutines/tree/master/examples)
- [KotlinConf app](https://github.com/JetBrains/kotlinconf-app)

更多示例参见 [GitHub](https://github.com/JetBrains/kotlin-examples)

## 多平台

> 多平台项目是Kotlin 1.2和1.3的实验特性。本文档描述的所有语言和工具特性都以未来Kotlin版本的变更为准。

工作在所有平台是Kotlin的一个明确目标。但我们把它看做“在多平台共享代码”这个更重要目标的前提。由于对 JVM, Android, JavaScript, iOS, Linux, Windows, Mac甚至于 嵌入式系统比如STM32的支持，Kotlin可以处理一个现代应用的任何组件。这为代码和专业知识的重用带来了无价的好处，将精力节省到比两次或多次实现所有内容更具有挑战性的任务上。

### 它如何工作

总之，多平台并不是为所有平台编译所有代码。这个模型有其明显的局限性，我们知道现代应用程序需要访问它们所运行的平台的独特特性。Kotlin并没有将您限制在世界上所有api的公共子集内。每个组件可以根据需要与其他组件共享尽可能多的代码，但是可以通过语言提供的[expect/actual机制](expect/actual机制)随时访问平台api。

下面是一个在极简的日志框架中公共逻辑和平台逻辑之间的代码共享和交互的例子。通用代码如下:

```kotlin
// compiled for all platforms
enum class LogLevel {
    DEBUG, WARN, ERROR
}

// expected platform-specific API
internal expect fun writeLogMessage(message: String, logLevel: LogLevel)

// expected API can be used in the common code
fun logDebug(message: String) = writeLogMessage(message, LogLevel.DEBUG)
fun logWarn(message: String) = writeLogMessage(message, LogLevel.WARN)
fun logError(message: String) = writeLogMessage(message, LogLevel.ERROR)
```

它期望目标为`writeLogMessage`提供特定于平台的实现，公共代码现在可以使用这个声明，而无需考虑它是如何实现的。

在JVM上，可以提供一个将日志写入标准输出的实现：

```kotlin
internal actual fun writeLogMessage(message: String, logLevel: LogLevel) {
    println("[$logLevel]: $message")
}
```

在JavaScript中，可以提供一组完全不同的APIs，将日志记录实现到控制台：

```kotlin
internal actual fun writeLogMessage(message: String, logLevel: LogLevel) {
    when (logLevel) {
        LogLevel.DEBUG -> console.log(message)
        LogLevel.WARN -> console.warn(message)
        LogLevel.ERROR -> console.error(message)
    }
}
```

在1.3中，我们重写了整个多平台模型。我们用于描述多平台层级项目的[新DSL](https://kotlinlang.org/docs/reference/building-mpp-with-gradle.html)更加灵活，我们将继续努力使项目配置更加简单明了。

### 多平台库

公共代码可以依赖一组包含日常任务的库， 比如[HTTP](http://ktor.io/clients/http-client/multiplatform.html)、[序列化](https://github.com/Kotlin/kotlinx.serialization)、[管理协程](https://github.com/Kotlin/kotlinx.coroutines)。大量标准库可用于所有平台。

你可以编写一个自有库提供公共API和不同平台的不同实现。

### 用例

#### Android-iOS

在移动平台之间共享代码是一个主要的Kotlin多平台用例。现在可以使用Android和iOS共享的部分代码(如业务逻辑、连接等)构建移动应用程序。

参见[Multiplatform Project: iOS and Android](https://kotlinlang.org/docs/tutorials/native/mpp-ios-android.html)

#### 客户端-服务端

代码共享可能带来好处的另一个场景是线上应用程序，其中逻辑可以在服务器和运行在浏览器中的客户端上重用。这也是Kotlin Multiplatform所涵盖的。

[Ktor框架](https://ktor.io/)适用于在线上系统中构建异步服务器和客户机。

### 如何开始

#### 教程和文档

初识Kotlin？看一下[Getting Started](#开始)页面。

推荐文档页：

- [Setting up a Multiplatform Project](https://kotlinlang.org/docs/reference/building-mpp-with-gradle.html#setting-up-a-multiplatform-project)
- [Platform-Specific Declarations](https://kotlinlang.org/docs/reference/platform-specific-declarations.html)

推荐教程：

- [Multiplatform Kotlin Library](https://kotlinlang.org/docs/tutorials/multiplatform-library.html)
- [Multiplatform Project: iOS and Android](https://kotlinlang.org/docs/tutorials/native/mpp-ios-android.html)

#### 示例工程

- [KotlinConf app](https://github.com/JetBrains/kotlinconf-app)
- [KotlinConf Spinner app](https://github.com/jetbrains/kotlinconf-spinner)

更多示例参见 [GitHub](https://github.com/JetBrains/kotlin-examples)

# 开始

## 基本语法

### 定义包

包声明应该位于源代码文件的顶部：

```kotlin
package my.demo

import java.util.*

// ...
```

不需要匹配目录和包:源文件可以任意放置在文件系统中。

参见[包](#包)

### 定义函数

```kotlin
// 两个Int类型参数，Int类型返回值
fun sum(a: Int, b: Int) {
    return a + b;
}

// 表达式函数体，推断返回值类型
fun sum(a: Int, b: Int) = a + b

// 无返回值
fun printSum(a: Int, b: Int): Unit {
    println("sum of $a and $b is ${a + b}")
}

// 返回值类型Unit可以省略
fun printSum(a: Int, b: Int) {
    println("sum of $a and $b is ${a + b}")
}
```

参见[函数](#函数)

### 定义变量

```kotlin
// 一次赋值（只读）本地变量
val a: Int = 1 // 立即赋值
val b = 2 // 推断为Int类型
val c: Int // 未初始化时，必须提供类型
c = 3 // 延迟赋值

// 可变变量
var x = 5 // 推断为Int类型
x += 1

// 顶级变量
val PI = 3.14
var x = 0
fun incrementX() {
    x += 1
}
```

参见[属性和字段](#属性和字段)

### 注释

与Java和JavaScript一样，Kotlin支持行注释和块注释。

```kotlin
// 这是一个行注释

/* 这是一个多行的
	块注释*/
```

与Java不同，Kotlin中的块注释可以嵌套。

参见[Kotlin代码文档](#Kotlin代码文档)获取更多有关文档注释语法的信息

### 使用字符串模板

```kotlin
var a = 1
// 模板中的简单名称:
val s1 = "a is $a"

a = 2
// 模板中的任意表达式
val s2 = "${s1.replace("is", "was")}, but now is $a"
```

参见[字符串模板](#字符串模板)

### 使用条件表达式

```kotlin
fun maxOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}
```

使用`if`表达式：

```kotlin
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```

参见[`if`表达式](#`if`表达式)

### 使用可为`null`的值，检查`null`

当可能为`null`值时，引用必须被显示标记为可为`null`。

如果`str`不持有一个整数，返回`null`

```kotlin
fun parseInt(str: String): Int?{
    //...
}
```

使用返回可为`null`返回值的函数：

```kotlin
fun printProduct(arg1: String, arg2: String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)

    // 使用 `x * y` 产生错误，因为它们可能持有null值
    if (x != null && y != null) {
        // 检查null后，x和y自动转换成非null
        println(x * y)
    } else {
        println("either '$arg1' or '$arg2' is not a number")
    }    
}
```

或者：

```kotlin
// ...
if (x == null) {
    println("Wrong number format in arg1: '$arg1'")
    return
}
if (y == null) {
    println("Wrong number format in arg2: '$arg2'")
    return
}

// 检查null后，x和y自动转换成非null
println(x * y)
```

参见[空指针安全](#空指针安全)

### 使用类型检查并自动强转

`is`操作符检查表达式是否是某个类型的实例。如果一个不可变的本地变量或者属性已被检查是指定的类型，则不需要显示强制转换：

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // `obj` 在这个分支内自动强转为 `String` 
        return obj.length
    }

    // `obj` 在类型检查分支外任然是 `Any` 类型
    return null
}
```

或者：

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj !is String) return null

    // `obj` 在这个分支内自动强转为 `String` 类型
    return obj.length
}
```

或者：

```kotlin
fun getStringLength(obj: Any): Int? {
    // `obj` 在 `&&` 右侧自动强转为 `String` 类型
    if (obj is String && obj.length > 0) {
        return obj.length
    }

    return null
}
```

参见[类](#类)和[类型转换](#类型转换)

### 使用`for`循环

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}
```
或者：

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```
参见[`for`循环](#`for`循环)

### 使用`while`循环

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
var index = 0
while (index < items.size) {
    println("item at $index is ${items[index]}")
    index++
}
```
参见[`while`循环](#`while`循环)

### 使用`when`表达式
```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long"
        !is String -> "Not a string"
        else       -> "Unknown"
    }
```
参见[`when`表达式](#`when`表达式)

### 使用区间
使用`in`操作符检查一个数是否在指定区间：
```kotlin
val x = 10
val y = 9
if (x in 1..y+1) {
    println("fits in range")
}
```
检查数字是否在区间外：

```kotlin
val list = listOf("a", "b", "c")

if (-1 !in 0..list.lastIndex) {
    println("-1 is out of range")
}
if (list.size !in list.indices) {
    println("list size is out of valid list indices range, too")
}
```
迭代区间：

```kotlin
for (x in 1..5) {
    print(x)
}
```
或者迭代级数：
```kotlin
for (x in 1..10 step 2) {
    print(x)
}
println()
for (x in 9 downTo 0 step 3) {
    print(x)
}
```
参见[区间](#区间)

### 使用集合
遍历集合：
```kotlin
for (item in items) {
    println(item)
}
```
使用`in`操作符检查集合是否包含对象：
```kotlin
when {
    "orange" in items -> println("juicy")
    "apple" in items -> println("apple is fine too")
}
```
使用lambda表达式过滤、转换集合
```kotlin
val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
	.filter { it.startsWith("a") }
	.sortedBy { it }
	.map { it.toUpperCase() }
	.forEach { println(it) }
```
参见[高阶函数和lambda表达式](#高阶函数和lambda表达式)

### 创建基本类和对象
```kotlin
val rectangel = Rectangle(5.0, 2.0) // 不需要`new`
val triangle = Triangle(3.0, 4.0, 5.0)
```
参见[类][#类]和[对象与实例](#对象与实例)

## 习惯用法
Kotlin中一组使用频繁的语法习惯。如果你有喜欢的习惯用法，发送一个pull request来贡献它。
### 创建DTOs(POJOs/POCOs)
```kotlin
data class Customer(val name: String, val email: String)
```
以上代码提供了一个`Customer`类，并包含了以下函数：

- 为所有属性提供getters (and setters in case of *var*s) 
- `equals()`
- `hashCode()`
- `toString()`
- `copy()`
- 为所有属性提供`component1()`, `component2()`, …, (参见 [数据类](#数据类))

### 函数参数的默认值
```kotlin
fun foo(a: Int = 0, b: String = "") { ... }
```

### 过滤列表
```kotlin
val positives = list.filter { x -> x > 0 }
```
或者更短
```kotlin
val positives = list.filter { it > 0 }
```

### 字符串插值
```kotlin
println("Name $name")
```

### 实例检查
```kotlin
when (x) {
    is Foo -> ...
    is Bar -> ...
    else   -> ...
}
```

### 遍历键值对组成的映射或列表
```kotlin
for((k, v) in map) {
    println("$k -> $v")
}
```
`k`, `v` 可以任意调用

### 使用区间
```kotlin
for (i in 1..100) { ... } // 闭区间，包括100
for (i in 1 until 100) { ... } // 半开区间， 不包括100
for (x in 2..10 step 2) { ... }
for (x in 10 downTo 1) { ... }
if (x in 1..10) { ... }
```
### 只读列表
```kotlin
val list = listOf("a", "b", "c")
```
### 只读映射
```kotlin
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
```
### 访问映射
```kotlin
println(map["key"])
map["key"] = value
```
### 懒属性
```kotlin
val p: String by lazy {
    // 计算字符串的值
}
```
### 拓展函数
```kotlin
fun String.spaceToCameCase() { ... }
"Convert this to camelcase".spaceToCameCase()
```
### 创建单例
```kotlin
object Resource {
    val name = "Name"
}
```
### 如果不为`null`的简化符号
```kotlin
val files = File("Test").listFiles()
println(files?.size)
```
### 如果不为`null`否则的简化符号
```kotlin
val files = File("Test").listFiles()
println(files?.size ?: "empty")
```
### 如果为`null`执行语句
```kotlin
val values = ...
val email = values["email"] ?: throw IllegalStateException("Email is missing!")
```
### 从可能为空的集合中获取第一个元素
```kotlin
val emails = ... // 可能为空
val mainEmail = emails.firstOrNull() ?: ""
```
### 如果不为`null`则执行
```kotlin
val value = ...
value?.let {
    ... // 如果不为null则执行这个语句块
}
```
### 映射可为`null`的值
```kotlin
val value = ...
val mapped = value?.let { transformValue(it) } ?: defaultValueIfValueIsNull
```
### 返回语句使用`when`语句
```kotlin
fun transform(color: String): Int {
    return when (color) {
        "Red" -> 0
        "Green" -> 1
        "Blue" -> 2
        else -> throw IllegalArgumentException("Invalid color param value")
    }
}
```
### `try/catch`表达式
```kotlin
fun test() {
    val result = try {
        count()
    } catch (e: ArithmeticException) {
        throw IllegalStateException(e)
    }
    
    // 使用result
}
```
### \`if\`表达式
```kotlin
fun foo(param: Int) {
    val result = if (param == 1) {
        "one"
    } else if (param == 2) {
        "two"
    } else {
        "three"
    }
}
```
### 无返回值的函数的建造者风格调用
```kotlin
fun arrayOfMinusOnes(size: Int): IntArray {
    return IntArray(size).apply { fill(-1) }
}
```
### 单表达式函数
```kotlin
fun theAnswer() = 42
```
等价于：
```kotlin
fun theAnswer() {
    return 42
}
```
与其它习惯用法结合，可以写出简短的代码。比如，和`when`表达式：
```kotlin
fun transform(color: String): Int = when (color) {
    "Red" -> 0
    "Green" -> 1
    "Blue" -> 2
    else -> throw IllegalArgumentException("Invalid color param value")
}
```
### 使用`with`调用一个对象实例的多个方法
```kotlin
class Turtle {
    fun penDown()
    fun penUp()
    fun turn(degrees: Double)
    fun forward(pixels: Double)
}

val myTurtle = Turtle()
with(myTurtle) { //draw a 100 pix square
    penDown()
    for(i in 1..4) {
        forward(100.0)
        turn(90.0)
    }
    penUp()
}
```
### Java 7的try with resources
```kotlin
val stream = Files.newInputStream(Paths.get("/some/file.txt"))
stream.buffered().reader().use { reader ->
    println(reader.readText())
}
```
### 泛型方法的泛型信息
```kotlin
//  public final class Gson {
//     ...
//     public <T> T fromJson(JsonElement json, Class<T> classOfT) throws JsonSyntaxException {
//     ...

inline fun <reified T: Any> Gson.fromJson(json: JsonElement): T = this.fromJson(json, T::class.java)
```
### 消费一个可为`null`的布尔类型对象
```kotlin
val b: Boolean? = ...
if (b == true) {
    
} else {
    // `b` 为false或者null
}
```

## 编码公约

此页面包含Kotlin语言的当前编码风格。

### 使用样式指南

要根据这个样式指南配置IntelliJ formatter，请安装Kotlin plugin version 1.2.20或更新版本，转到 Settings | Editor | Code style | Kotlin，点击右上角的"Set from…"链接，从菜单中选择"Predefined style / Kotlin style guide"。

要验证您的代码是否按照样式指南进行了格式化，请转到inspection setting，并启用“Kotlin | Style issues | File is not formatted according to project settings检查。默认情况下，将启用其它检查，以验证样式指南中描述的其他问题(如命名约定)。

### 源代码组织

#### 目录结构

在混合语言项目中，Kotlin源文件应该与Java源文件驻留在同一个源根中，并且遵循相同的目录结构(每个文件应该存储在每个包语句对应的目录中)。

在纯Kotlin项目中，推荐的目录结构是遵循包结构，省略公共根包(例如，如果项目中的所有代码都在"org.example.kotlin"包及其子包中，"org.example.kotlin"包的文件应该直接放在源根目录下，"org.example.kotlin.foo. bar"的文件应该放在源根的子目录"foo/bar"下。

#### 源文件名

如果Kotlin文件包含单个类(可能带有相关的顶级声明)，其名称应该与类的名称相同，并附加.kt扩展名。如果一个文件包含多个类，或者只包含顶级声明，那么选择一个描述该文件所包含内容的名称，并相应地命名该文件。使用驼峰命名法，首字母大写(例如ProcessDeclaration .kt)。

文件的名称应该描述文件中的代码的功能。因此，您应该避免在文件名中使用"Util"等无意义的词。

#### 源文件组织

在同一个Kotlin源文件中放置多个声明(类、顶级函数或属性)是受鼓励的，只要这些声明在语义上紧密相关，且文件大小保持合理(不超过几百行)。

特别是，当为与该类的所有客户端相关的类定义扩展函数时，将它们放在定义类本身的同一个文件中。当定义仅对特定客户端有意义的扩展函数时，将它们放在该客户端代码旁边。不要为了保存一个类的所有拓展而创建文件。

#### 类布局

总体上，一个类的内容按以下顺序排列：

- 属性声明和初始化代码块
- 构造函数
- 方法声明
- 伴随对象

不要按字母顺序或可见性排列方法声明，也不要把普通方法和拓展方法分开。应该把相关的东西放在一起，让人从头到尾阅读代码时能理解逻辑。选择一个顺序（高层次居首，或者相反），并坚持它。

把内部类放在使用它的代码旁边。如果打算在外部使用这些类，并且在类内部没有这些类的引用，将它们放在最后，就是伴随对象后面。

#### 接口实现布局

当实现一个接口时，实现类成员的顺序与接口成员顺序保持一致（如果必要，中间可以穿插用于实现方法的私有方法。

#### 重载布局

永远把重载放置在一起。

### 命名规则

Kotlin遵循Java的命名规约。特别是：

包名总是小写，并且不要使用下划线。通常不鼓励使用多单词的名字，但是如果确实需要使用多单词，你可以简单地将它们连接在一起，或者使用驼峰法。

类和对象的名称首字母大写，使用驼峰命名法:

```kotlin
open class DeclarationProcessor { ... }
object EmptyDeclarationProcessor : DeclarationProcessor() { ... }
```
#### 函数名称
函数、属性和局部变量首字母小写，使用驼峰命名法，不使用下划线
```kotlin
fun processDeclaration() { ... }
var declarationCount = ...
```
例外：用于创建类的实例的工厂函数可以使用与所创建类名相同的名字
```kotlin
abstract class Foo { ... }
class FooImpl : Foo { ... }
fun Foo(): Foo { return FooImpl(...) }
```

##### 测试方法名称
在测试中（仅在测试中），用单引号包围的带空白符的方法名是可接受的。（注意这种方法名目前不被Android运行时支持。）在测试中，方法名中使用下划线同样被允许。
```kotlin
class MyTestCase {
    @Test fun `ensure everything works`() { ... }
    @Test fun ensureEverythingWorks_onAndroid( { ... })
}
```
#### 属性名
常量（标记为`const`的属性，或者顶级声明，或者没有持有深度不可变的数据的自定`get`方法的`val`对象属性）应该使用下划线分隔的大写单词名称：
```kotlin
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserName"
```
顶级声明、持有具备行为或可变数据的对象的对象属性，通常应该使用驼峰法命名：
```kotlin
val mutableCollection：MutableSet<String> = HashSet()
```
持有单例的引用的属性的名称可以使用`object`声明相同的命名风格：
```kotlin
val PersonComparator: Comparator<Person> = ... 
```
对于枚举常量，既可以使用下划线分隔的大写字母名称，也可以使用普通的首字母大写的驼峰命名法，依据使用场景而定。

#### 支持属性的名称
如果一个类包含两个概念上相同的属性，其中一个是公共API的一部分，另一个是实现的细节，在私有属性中使用下划线作为前缀：
```kotlin
class {
    private val _elementList = mutableListOf<Element>()
    
    val elementList: List<Element>
    	get() = _elementList
}
```
### 选择好名称
类名通常是一个名词或名词词组，解释这个类是什么：`List`, `PersonReader`.

方法名通常是一个动词或动词词组，说明这个方法做了什么：`close`, `readPersons`. 这个名字也要表明这个方法是改变该对象还是返回一个新对象。比如，`sort`是就地排序一个集合，而`sorted`会返回一个排好序的集合副本。

名称应该清楚表明实体的目的是什么，因此最好避免在名称中使用无意义的单词（`Manager`, `Wrapper` 等）

在声明名称时使用首字母缩写时，2个字母组成的使用大写（`IOStream`）；多于两个字母的仅首字母大写（`XmlFormatter`, `HttpInputStream`）.

## 格式化

在多数情况下，Kotlin遵循Java的编码规约。

使用4个空格符缩进。不要使用制表符。

对于大括号，左大括号放在结构首行的行尾，右大括号单独一行并与结构首行左对齐。
```kotlin
if (elements != null) {
    for (element in elements) {
        // ...
    }
}
```
（注意: 在Kotlin中，分号是可选的，因此换行符是很重要的。语言设计采用Java样式的大括号，如果你尝试使用不同的格式化样式，可能会遇到不可预知的行为。

### 水平空格
二元操作符左右均有空格（`a + b`）。例外：不要在区间操作符左右放置空格符（`0..i`）

不要在一元操作符左右放置空格（`a++`）

在控制流关键字(`if`,`when`,`for`,`while`)和对应的开括号之间放置空格符

在主构造函数声明、方法声明或方法调用中，不要在开头括号前加空格
```kotlin
class A(val x: Int)

fun foo(x: Int) { ... }

fun bar() {
    foo(1)
}
```

永远不要在`(`,`[`之前或`]`,`)`之后放置空格

永远不要在`.`或`?.`左右放置空格：`foo.bar().filter { it > 2 }.joinToString()`, `foo?.bar()`

在`//`后面放置空格: `// 这是一条注释`

在用于指定类型参数的尖括号左右，不要放置空格：`class Map<K, V> { ... }

不要在`::`左右放置空格：`Foo:class`, `String::length`

当`?`用于标记一个可为null的类型时，不要在它前面放置空格：`String?`

一般规则是，避免任何形式的水平对齐。将标识符重命名为具有不同长度的名称不应影响声明或任何用法的格式。

### 冒号
在下列情形下，`:`前面放置空格：
- 当它用于分隔类型和父类时
- 当委托给超类构造函数或同一类的不同构造函数时
- 在`object`关键字后面时

当`:`用于分离声明和它的类型时，不要在它前面放置空格

总是在`:`后面放置空格：
```kotlin
abstract class Foo<out T : Any> : IFoo {
    abstract fun foo(a: Int): T


class FooImpl : Foo() {
    constructor(x: String) : this(x) { ... }
    
    val x = object : IFoo { ... }
}
```

### 类头部格式化
只有少量主构造函数参数的类可以在一行中书写:
```kotlin
class Person(id: Int, name: String)
```
具有较长标题的类应该进行格式化，以便每个主构造函数参数都在一个单独的缩进行中。此外，右括号应该在新行上。如果我们使用继承，那么超类构造函数调用或实现接口列表应该与括号位于同一行
```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name) { ... }
```
对于多个接口，首先应该定位超类构造函数调用，然后每个接口应该位于不同的行中：
```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name),
    KotlinMaker { ... }
```
对于具有较长的超类型列表的类，在冒号后面放一个换行符，并水平对齐所有超类型名称:
```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne {

    fun foo() { ... }
}
```
如果类标题很长，要清楚地将类标题和主体分开，可以在类标题后面放一个空行(如上例所示)，或者在单独的行上放一个大括号:
```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne 
{
    fun foo() { ... }
}
```
对构造函数参数使用常规缩进(4个空格)。

> 基本原理:这确保在主构造函数中声明的属性与在类主体中声明的属性具有相同的缩进。

### 修饰符

如果一个声明有多个修饰符，请按以下顺序排列:

```kotlin
public / protected / private / internal
expect / actual
final / open / abstract / sealed / const
external
override
lateinit
tailrec
vararg
suspend
inner
enum / annotation
companion
inline
infix
operator
data
```
将所有注释放在修饰符前面:
```kotlin
@Named("Foo")
private val foo: Foo
```
除非你开发库，否则省略多余的修饰词(例如`public`)。

### 注解格式化
注释通常放在单独的行上，在它们所注解的声明之前，并且有相同的缩进:
```kotlin
@Target(AnnotationTarget.PROPERTY)
annotation class JsonExclude
```
没有参数的注释可以放在同一行:
```kotlin
@JsonExclude @JvmField
var x: String
```
单个没有参数的注释可以与相应的声明放在同一行:
```kotlin
@Test fun foo() { ... }
```

### 文件注解
文件注解放在文件注释(如果有的话)之后，在包语句之前，并且用空行与包分隔(强调它们针对的是文件而不是包)。
```kotlin
/** License, copyright and whatever */
@file:JvmName("FooBar")

package foo.bar
```

### 函数格式化
如果函数签名不适用于一行，请使用以下语法:
```kotlin
fun longMethodName(
    argument: ArgumentType = defaultValue,
    argument2: AnotherArgumentType
): ReturnType {
    // body
}
```
对函数参数使用常规缩进(4个空格)。

> 基本原理:与构造函数参数的格式一致

对于包含单个表达式的函数，最好使用表达式体。
```kotlin
fun foo(): Int {     // bad
    return 1 
}

fun foo() = 1        // good
```
### 表达式体格式化

如果函数的表达式体与声明不能放在同一行，请将`=`符号放在第一行。将表达式体缩进4个空格。
```kotlin
fun f(x: String) =
    x.length
```
### 属性格式化
对于非常简单的只读属性，考虑一行格式：
```kotlin
val isEmpty: Boolean get() = size == 0
```
对于更复杂的属性，通常将`get`和`set`关键字放在单独行：
```kotlin
val foo: String
    get() { ... }
```
对于带有初始化器的属性，如果初始化器很长，在等号后面加一个换行符，并缩进四个空格:
```kotlin
private val defaultCharset: Charset? = 
    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

### 格式化控制流语句

如果`if`或`when`语句的条件是多行，始终在语句的主体周围使用花括号。将条件的每一行缩进4个相对于语句开始的空格。将条件的右括号和左花括号放在另一行:
```kotlin
if (!component.isSyncing &&
    !hasAnyKotlinRuntimeInScope(module)
) {
    return createKotlinNotConfiguredPanel(module)
}
```
>基本原理：条件和语句体的整齐对齐和清晰分离

将`else`,`catch`,`finally`关键字以及do/while循环中的`while`关键字放在前导大括号的同一行：
```kotlin
if (condition) {
    // body
} else {
    // else part
}

try {
    // body
} finally {
    // cleanup
}
```
在`when`语句中，如果分支不止一行，考虑用空行将它与相邻的case块分隔开来:
```kotlin
private fun parsePropertyValue(propName: String, token: Token) {
    when (token) {
        is Token.ValueToken ->
            callback.visitValue(propName, token.value)

        Token.LBRACE -> { // ...
        }
    }
}
```
将短的分支放在与条件同行上，不带大括号。
```kotlin
when (foo) {
    true -> bar() // good
    false -> { baz() } // bad
}
```

### 方法调用格式化    