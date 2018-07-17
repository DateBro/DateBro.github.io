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
