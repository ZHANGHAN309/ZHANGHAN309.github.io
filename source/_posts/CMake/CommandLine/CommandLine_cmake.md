[TOC]

# 总览

cmake是用来配置、生成和构建项目的工具，可以执行以下操作：

- 生成构建系统
- 构建项目
- 安装项目
- 运行脚本
- 运行命令行工具
- 获取帮助

# 介绍

## 1.生成一个项目构建系统

格式：

```cmake
cmake [<options>] -S <path-to-source> -B <path-to-build>
cmake [<options>] <path-to-source>
cmake [<options>] <path-to-existing-build>
```

cmake相较于其他构建工具如GNU Make，可以将构建产生的中间文件放在单独的文件夹里，避免污染源文件夹。

> 不推荐使用第二种和第三种格式，因为这会在构建过程中产生混乱。如语法片段所示，若<目录>中已存在先前构建，则同一命令的行为会有所不同：它将使用源代码的缓存路径并从该位置开始重建。

### 1.1生成器选项

cmake指定generator的语法:

```cmake
cmake -G <generator-name>
-T <toolset-spec> -A <architecture>
<path-to-source>
```

> eg:指定ninja生成器为`cmake -G ninja ./build`

### 1.2缓存选项

在配置阶段，缓存信息会被保存到CMakeCache.txt，可以通过指令来指定文件

```cmake
cmake -C <initial-cache-script>
-D <var>[:<type>]=<value> <path-to-source>
```

> -C表示加载脚本预设的缓存变量，优先级比CMakeCache.txt里未设置FORCE的略高
>
> -D表示命令行直接设置单个缓存变量，优先级比-C的略高

可以使用-U来移除缓存变量

```cmake
cmake -U <globbing_expr> <path-to-source>
```

> -U和-D可以使用多次

### 1.3调试和追踪选项

```cmake
cmake --system-information [file]
```

> 该指令可以获取一般信息如变量、命令等，file选项可以指定保存的文件名

```cmake
cmake --log-level=<level>
```

> 通过level参数过滤日志，有ERROR,WARNING,NOTICE,STATUS选项

```cmake
cmake --log-context <path-to-source>
```

> 日志信息会以栈的方式存储到`CMAKE_MESSAGE_CONTEXT`变量中

```cmake
cmake --trace
```

> 显示每个文件的命令和行号

### 1.4预设选项

每次生成项目时都需要配置大量选项，为了简化这些流程，可以通过指令来执行预设选项

```cmake
cmake --list-presets
cmake --preset=<preset>
```

> preset可以覆盖系统默认值，但是会被-D覆盖

## 2.构建项目

```cmake
cmake --build <dir> -- <build-tool-options>
```

> dir是生成阶段-B指定的文件夹。
>
> 如果自己需要传递特殊的参数，可以在--后加上

### 2.1并行构建

```cmake
cmake --build <dir> --parallel [<number-of-jobs>]
cmake --build <dir> -j [<number-of-jobs>]
```

> 可以设置并行构建的进程数，也可以使用`CMAKE_BUILD_PARALLEL_LEVEL`指定

### 2.2目标选项

```cmake
cmake --build <dir> --target <target1> -t <target2> ...
```

> 只要你想，可以一直用-t添加target

```cmake
cmake --build <dir> -t clean
```

> clean目标不会执行构建，它会清除dir内的生成文件

```cmake
cmake --build <dir> --clean-first
```

> 便捷命令：先清理后构建

### 2.3多配置生成器的选项

```cmake
cmake --build <dir> --config <cfg>
```

> 只对多配置生成器有效，如Visual Studio、XCode有效
>
> 如`cmake --build build --config Release`

### 2.4调试选项

```cmake
cmake --build <dir> --verbose
cmake --build <dir> -v
```

> 可以使调试信息变详细，也可以设置CMAKE_VERBOSE_MAKEFILE

## 3.安装项目

安装步骤的作用是复制文件到正确的路径下，安装库文件，或者运行CMake脚本里自定义安装逻辑。

```cmake
cmake --install <dir>
```

> dir为构建树的路径

### 3.1多配置生成器的选项

```cmake
cmake --install <dir> --config <cfg>
```

### 3.2组件选项

```cmake
cmake --install <dir> --component <comp>
```

### 3.3权限选项

```cmake
cmake --install <dir>
--default-directory-permissions <permissions>
```

> 在Unix-like平台上可以给文件夹指定权限

### 3.4安装文件夹选项

```cmake
cmake --install <dir> --prefix <prefix>
```

> 暂时不适用于Windows

### 3.5调试选项

```cmake
cmake --build <dir> --verbose
cmake --build <dir> -v
```

## 4.运行脚本

```cmake
cmake [{-D <var>=<value>}...] -P <cmake-script-file>
[-- <unparsed-options>...]
```

> 脚本运行不会执行配置或生成阶段
>
> 可以有两种方式传递参数，-D和--

## 5.运行命令行工具

```cmake
cmake -E <command> [<options>]
```

## 6.获取帮助

```cmake
cmake --help[-<topic>]
```

