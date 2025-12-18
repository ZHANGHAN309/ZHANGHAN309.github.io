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

在WPF项目里App.xaml相当于应用程序本身，虽然它本身有内容，但是却无法通过设计器展示出来，而项目创建时会默认创建一个窗口MainWindow.xaml，而App.xaml是通过头部的StartupUri指向展示的第一个窗口

```Xaml
<Application x:Class="com_mc_test.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:com_mc_test"
             StartupUri="MainWindow.xaml">
```

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

之后就是我的一些项目经验杂谈了（看不看无所谓）

~~写程序之前要搞清楚架构，自顶向下思考，程序是干嘛的，可以拆分哪几步，每一步需要什么功能，底层数据源从哪来，数据源怎么传递给处理层，处理层怎么传递给显示层，处理层显示层又可以分为几步，比如处理层先要解析包，再转换为某种数据类型，加密或者解密，筛分或者增删改，显示层数据是同步还是刷新，一个页面展示还是多个页面展示（感觉没说到点上）~~

参考了一下腾讯云[十毛]的见解，补充一下架构理解：

要写好一个项目首先要理解需求，其次再提出架构解决问题，需求是由客户或者公司提出，而架构是由架构师分析需求得出，同时因为需求可能会发生变动，所以架构师必须考虑尽可能多的情况

理解一个项目的架构首先得了解项目背景，比如这个项目是为了解决什么问题，目标用户是谁?目标用户的使用情况如何？

其次再考虑开发的功能，这些功能解决了哪些问题，核心功能有哪些，次要功能有哪些

然后列出架构图，模块层次图，核心流程图，技术点

比如说采用分层架构，表示层、业务逻辑层、数据访问层、数据库层
又比如模块，上位机模块可以分为主界面模块、日志模块、协议解析模块、插件模块、配置设计模块
核心流程图可以展示用户操作时的关键步骤，这个参考uml
技术点可以列举前端、后端、数据库、消息队列、通信协议等

还有文章里讲的报警/监控系统，也可以参考一下

---

之前做过一个远控项目，听过一个大佬的架构分析，今晚记录吧...


# 参考
[MicroSoft C#](https://learn.microsoft.com/zh-cn/dotnet/desktop/wpf/get-started/create-app-visual-studio)

[如何清晰地描述一个项目架构-十毛](https://cloud.tencent.com/developer/article/1407580)

[WPF中文网](https://www.wpfsoft.com/introduction)