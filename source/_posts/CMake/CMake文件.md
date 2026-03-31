---
title: CMake文件
date: 2025/11/11
tags: CMake
categories: 技术篇
---

# 总览

CMake项目文件主要有：

- CMakeLists.txt
- CMakeCache.txt
- Config-files
- cmake_install.cmake/CTestTestfile.cmake/CPackConfig.cmake
- CMakePresets.json/CMakeUserPresets.json

# 介绍

## 1.CMakeLists.txt

至少有一个CMakeLists.txt在源文件夹的根目录下，并且最外部的txt是最先执行的，并且每个文件必须包含两条命令`cmake_minimum_required(VERSION <x.xx>)` `project(<name> <OPTIONS>)`

CMake支持每个子文件夹通过CMakeLists.txt划分更小单元。

> eg：目录结构如下

```
CMakeLists.txt
api/CMakeLists.txt
api/api.h
api/api.cpp
```

> CMakeLists.txt如下

```cmake
cmake_minimum_required(VERSION 3.20)
project(app)
message("Top level CMakeLists.txt")
add_subdirectory(api)
```

## 2.CMakeCache.txt

配置阶段第一次运行时，缓存变量会被存储到CMakeCache.txt文件，放在构建树下。

## 3.Config-files

包含如何使用库文件的配置信息。

## 4.cmake_install.cmake/CTestTestfile.cmake/CPackConfig.cmake

在生成阶段时在构建树下的文件，CMake将它们作为cmake安装动作、CTest、CPack的配置。

## 5.CMakePresets.json/CMakeUserPresets.json

可以使用`--preset=<preset>`加载预设，预设保存在CMakePresets.json和CMakeUserPresets.json里，其中CMakePresets.json保存的是官方预设，CMakeUserPresets.json保存的是自定义预设。

# 总结

需要使用VCS如Git时，可以忽略如下文件：

```git
build_debug/
build_release/

**/CMakeCache.txt
**/CMakeUserPresets.json
**/CTestTestfile.cmake
**/CPackConfig.cmake
**/cmake_install.cmake
**/install_manifest.txt
**/compile_commands.json
```

如果有用户自定义文件可以自行添加。