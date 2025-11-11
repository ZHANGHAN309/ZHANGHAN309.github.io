---
title: Kotlin
date: 2025/11/11
---

# 总览

- 变量

- 基础数据类型
- 数据结构

# 介绍

## 变量

```kotlin
val a1 = 10
var a2 = 9
fun main()
{
	a2 = 11
	println("a2 = ${a2}")
}
```

> 变量可以在函数外声明，相当于C的全局变量
> val相当于常量，初始化之后不能修改，var相当于变量
>
> 字符串访问变量的方法可以使用${}

## 基础数据类型

```kotlin
val year: Int = 2025
val score: UInt = 108u
val Temp: Float = 24.5f
val Def: Boolean = true
val sep: Char = 'A'
val message: String = "HelloWorld"
```

## 数据结构

### Lists

```kotlin
// Read only list
val readOnlyShapes = listOf("triangle", "square", "circle")
println(readOnlyShapes)
// [triangle, square, circle]

// Mutable list with explicit type declaration
val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
println(shapes)
// [triangle, square, circle]
```

> Lists保存的是列表
>
> 如果不像修改Lists，可以使用casting

```kotlin
val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
val shapesLocked: List<String> = shapes
```

> Lists还有其他几种用法

```kotlin
val readOnlyShapes = listOf("triangle", "square", "circle")
println("The first item in the list is: ${readOnlyShapes[0]}")
// The first item in the list is: triangle

val readOnlyShapes = listOf("triangle", "square", "circle")
println("The first item in the list is: ${readOnlyShapes.first()}")
// The first item in the list is: triangle

val readOnlyShapes = listOf("triangle", "square", "circle")
println("This list has ${readOnlyShapes.count()} items")
// This list has 3 items

val readOnlyShapes = listOf("triangle", "square", "circle")
println("circle" in readOnlyShapes)
// true

val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
// Add "pentagon" to the list
shapes.add("pentagon") 
println(shapes)  
// [triangle, square, circle, pentagon]

// Remove the first "pentagon" from the list
shapes.remove("pentagon") 
println(shapes)  
// [triangle, square, circle]
```

### Set