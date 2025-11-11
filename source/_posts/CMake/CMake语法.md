[TOC]

# 总览

在CMake列表文件里，只有命令调用和注释

- 注释
- 命令调用

# 介绍

## 1.注释

```cmake
# Hello World
#[[
外层注释
 #[[
 	内层注释	
 ]]
]]
```

> 有两种注释方式，单行注释和多行注释，多行注释只在CMake3.0以上版本支持

## 2.命令调用

## 2.1 参数类型

CMake数据类型只有string，但是参数类型有三种：

- Bracket arguments
- Quoted arguments
- Unquoted arguments

### Bracket arguments

> 这种类型会将[[]]内作为一个命令参数，跟注释很像，但是括号参数不能嵌套。

### Quoted arguments

> 这种类型可以视作C++ string类型，可以使用\\\",\t,\n等转义符

### Unquoted arguments

> ;会分割参数，比如argum;1代表两个参数

## 2.2 变量

变量有以下注意事项

- 变量名区分大小写，且可包含几乎任何字符。
- 所有变量按字符串存储
- 基础变量操作命令有set()和unset()，也有其他命令如string()和list()

### 变量引用

```cmake
message(${MyString1})
```

引用会从内部向外拓展，比如

```cmake
message("${MyOuter${MyInner}}")
```

> 先拓展MyInner，再拓展MyOuter

> ${}用于引用普通或缓存变量
>
> $ENV{}用于引用环境变量
>
> $CACHE{}用于引用缓存变量

### 使用环境变量

```cmake
set(ENV(CXX) "clang++")
unset(ENV(VERBOSE))
```

### 使用缓存变量

```cmake
set(<variable> <value> CACHE <type> <docstring> [FORCE])
```

> 相比于普通变量，多了CACHE和FORCE关键字，还有可以指定type和docstring值。不过type和docstring是给GUI使用的
>
> FORCE关键字可以保证值被强制更新，如果没加则会使用旧值

### 变量生命周期

CMake有两种周期

- 函数周期：当自定义函数执行时
- 文件夹周期：通过`add_subdirectory()`命令执行的CMakeLists.txt文件

当进入被嵌套的周期/范围时（比如`add_subdirectory(Node)`)，CMake会将当前周期的变量副本拷贝到被嵌套周期，当这个周期结束时，会恢复成原先的变量值。
