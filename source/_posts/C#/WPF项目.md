---
title: WPF项目
date: 2025-11-28 14:04:52
tags:
    - C#
    - WPF
categories:
    - 技术篇
---

WPF是C#的一个图形界面项目，本文主要介绍开发一个普通WPF项目的方法

# 打开图形界面
在Visual Studio里的解决方案资源管理器双击MainWindow.xaml可以打开设计器
[!image](MainWindow.png)
在该页面中有5个部分
1. 解决方案资源管理器
所有的项目文件都在这里
2. 属性（Properties）
在这图片里没展示，基于你选择的条目可以改变他们的属性
3. 工具箱
包含所有你可以添加到页面上的控件，双击或者拖动
4. XAML设计器
中间这一块，可以直接编辑UI界面
5. XAML代码编辑器
下面这一块，可以使用代码来编辑UI界面

# 查看XAML
在XAML代码编辑器里可以查看刚创建的项目代码
```xaml
<Window x:Class="Names.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Names"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>

    </Grid>
</Window>
```
XAML简单来说就是由WPF创建的XML语言，用来编辑页面，在\<Windows>其中有三部分值得关注
- XML命名空间
核心作用是避免元素命名冲突，限定文件中可使用的内容范围，无前缀的 xmlns 是默认命名空间（如 WPF 内置控件），带前缀的命名空间（如 `x:`、`local:`）用于引入额外类型（如 XAML 特性、自定义代码），`xmlns:local` 专门用来关联你自己项目中的代码，让 XAML 能直接使用自定义类 / 控件
- `x:Class`
`x:Class`属性是 WPF 中 “界面（XAML）” 和 “逻辑（代码）” 的连接核心，它明确了 XAML 对应的后台代码类，让两者能够协同工作（比如界面触发事件、代码修改界面显示）
- `Title`
窗口的标题

## XAML布局
XAML提供了一个强大的布局系统，包含多种不同的布局控件，默认的布局控件是\<Grid>控件
\<Grid>控件允许像表格一样定义行和列，并将控件放置在特定行与列组合的边界内
```XAML
<Grid Margin="10">
    
    <Grid.RowDefinitions>
        <RowDefinition Height="*" />
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="*" />
    </Grid.ColumnDefinitions>
    
</Grid>
```

## 添加组件
添加组件可以通过双击或拖动组件的方式进行，然后在属性窗口进行修改

# 参考
https://learn.microsoft.com/en-us/dotnet/desktop/wpf/get-started/create-app-visual-studio