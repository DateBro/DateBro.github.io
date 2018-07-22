---
layout: post
title:  "Android 学习之 Java 转 Kotlin 笔记"
description: "学习使用 Kotlin 写 Android 过程中和 Java 差别较大之处的笔记"
tags: Kotlin,Android，Java
mermaid: true
comments: true
date: 2018/07/16 19:40:00
---

# Android 学习之 Java 转 Kotlin 笔记

## Intent 对象的创建 —— 类引用与 this 表达式

### 使用 Java 创建时：
``` java
Intent intent = new Intent(FirstActivity.this, SecondActivity.class)
```

###使用 Kotlin 创建时：
``` Kotlin
var intent:Intent = Intent(this@FirstActivity, SecondActivity::class.java)
```

### 类引用笔记
这是因为 kotlin 中类引用方式造成的。要获取对静态已知的 Kotlin 类的引用，可以使用 _类字面值_ 语法：
``` kotlin
val c = MyClass::class
```
不过，这样获得的引用是 KClass 的值，kotlin 类引用和 Java 类引用不同，所以如果前面这样写会出错。要获得 Java 类的引用，在 KClass 后面加上 _.java_ 就可以了。

### this 表达式笔记
相关问题可在 [_StackOverflow_](https://stackoverflow.com/questions/41617042/how-to-access-activity-this-in-kotlin) 上见到
Kotlin 中使用 `this@FirstActivity` 的原因：
如果 this 没有限定符，它指的是最内层的包含它的作用域。要引用其他作用域中的 this，请使用 标签限定符。

要访问来自外部作用域的 this（一个类或者扩展函数，或者带标签的带有接收者的函数字面值）我们使用 `this@label`，其中 `@label` 是一个代指 this 来源的标签：
例如：

```kotlin
class A { // 隐式标签 @A
    inner class B { // 隐式标签 @B
        fun Int.foo() { // 隐式标签 @foo
            val a = this@A // A 的 this
            val b = this@B // B 的 this

            val c = this // foo() 的接收者，一个 Int
            val c1 = this@foo // foo() 的接收者，一个 Int

            val funLit = lambda@ fun String.() {
                val d = this // funLit 的接收者
            }


            val funLit2 = { s: String ->
                // foo() 的接收者，因为它包含的 lambda 表达式
                // 没有任何接收者
                val d1 = this
            }
        }
    }
}
```

## List 二三事
### Kotlin 和 Java List 的一些方法不是通用的

#### Java 中：
```java
List<String> list = new ArrayList();
list.add("DateBro");
list.clear();
list.removeAll();
```
但在 kotlin 中执行上面的函数却需要一些不同的声明。

```kotlin
var list:MutableList<String> = ArrayList()
list.add("DateBro")
list.clear()
list.removeAll()
```
与大多数语言不同，Kotlin 区分可变集合和不可变集合（lists、sets、maps 等），不可变集合如 List<E> 是只读集合，MutableList<E> 则增加了对集合的添加及删除元素的操作。

## 匿名内部类的不同
比如：
```java
HttpUtil.sendOkHttpRequest(address,new Callback(){
  @Override
  public void onResponse(Call call,Reponse reponse)throws IOException{
    ......
  }
})
```

而在 kotlin 中
```kotlin
HttpUtil.sendOkHttpRequest(address, object : Callback{
  override fun onFailure(call: Call?, e:IOException?){
                ......
              }
}
```

kotlin 中匿名内部类必须要以 object:MyClass{
......
} 创建

## kotlin 中匿名类实现接口和抽象类的区别
接口：
```Kotlin
interface OnBind {
    fun onBindChildViewData(holder: String, itemData: Any, position: Int)
}


lesson.does(object : OnBind {
        override fun onBindChildViewData(holder: String, itemData: Any, position: Int) {
            println(holder + itemData + position)
        }
    })
```

抽象类：
```kotlin
abstract class AbstractOnBind {
    abstract fun onBindChildViewData(holder: String, itemData: Any, position: Int)
}

lesson.does(object : AbstractOnBind() {
        override fun onBindChildViewData(holder: String, itemData: Any, position: Int) {
            println(holder + itemData + position)
        }
    })
```

他们之间唯一的区别就是调用时的下面这句，抽象类多了一个括号。
> object : OnBind
  object : AbstractOnBind()

  这么一点区别，但本质上是完全不一样的。
  在实现接口时，object 代替了 java 中 new 一个对象，在这里“：“ 号后紧跟接口，接口没有构造方法，代表了object实现了这个接口；
  而在实现抽象类的时候，抽象方法后边有（），可以理解为调用了抽象方法的构造方法，“new“出了一个对象后，赋给了object。

  总结一下：为便于理解可以这么想（实际原理可能并不是这样），接口时，先有 object ，然后让 object 实现该接口；抽象类时，先实现抽象类中的抽象方法，用构造方法构造出一个对象后，再给到 object
