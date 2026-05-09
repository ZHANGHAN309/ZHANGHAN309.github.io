---
title: FAE工程师笔记新
date: 2026-05-09 10:20:54
tags:
---

这个 JD 本质上是“半导体设备软件支持 / FAE / 集成工程师”路线，核心不是纯开发，而是：

软件部署

通信协议

设备联调

故障排查

客户支持

Linux/数据库/脚本

半导体设备业务理解

你本身有 C++ 背景，这是很大的优势。
因为这个岗位不是要求你从零学编程，而是要求你：

> “能把软件、设备、网络、数据库、客户现场串起来。”

下面我按“企业真正要的能力”给你拆成：

必备技能树

学习目标

每阶段 deadline

达成标准（不是“学过”，而是“能干活”）

我按「16 周可投递」给你规划。

---

第一阶段（第1-2周）

目标：建立半导体设备软件支持基础认知

这是最容易被忽略的阶段。

很多人一上来学协议，但根本不知道 Fab 是怎么运行的。

---

你要学的内容

1. 半导体制造基础（必须）

学习：

晶圆厂（Fab）是什么

Wafer（晶圆）

制程

机台

PE / MES / EAP

Recipe（配方）

Alarm（报警）

Lot

Cassette / FOUP

达成目标

你能解释：

SECS/GEM 为什么存在

MES 为什么要控制设备

为什么设备软件需要和上位机通信

---

2. 半导体设备软件架构

学习：

工控机

PLC

上位机

设备控制软件

数据采集

HMI

Socket/TCP通信

达成目标

你能画出：

MES → EAP → SECS/GEM → Equipment PC → PLC → Hardware

并解释每层作用。

---

Deadline

第2周结束前：

必须做到：

能独立讲清 Fab 软件系统架构

能看懂半导体设备软件架构图

能知道 PE/MES/设备工程师分别干什么

---

第二阶段（第3-5周）

目标：Linux + 网络 + SQL 达到“现场能排障”

这是这个岗位最核心的硬技能之一。

---

Linux 学习目标

必学内容

文件系统

cd ls pwd mkdir rm cp mv

日志查看

cat
tail -f
grep
less
find

权限

chmod
chown
sudo

进程

ps
top
kill
systemctl

网络

ping
netstat
ss
curl
telnet
tcpdump

---

达成目标

你必须做到：

能独立完成：

场景1

“SECS/GEM 连不上”

你会：

ping

查端口

查进程

看日志

---

场景2

“服务启动失败”

你会：

看 systemctl

看 error log

分析依赖问题

---

SQL 学习目标

这个岗位 SQL 非常重要。

因为设备日志、报警、Recipe 都可能在数据库。

---

必学 SQL

SELECT
WHERE
ORDER BY
GROUP BY
JOIN
UPDATE
DELETE

---

达成目标

你必须做到：

能独立写：

查询报警日志

SELECT \* FROM alarm_log
WHERE alarm_time > '2026-01-01';

---

查询机台状态

SELECT eqp_id,status
FROM equipment;

---

Deadline

第5周结束：

必须达到：

Linux 能排基础问题

SQL 能独立查数据

能部署简单服务

能分析日志

---

第三阶段（第6-8周）

目标：SECS/GEM + TCP/IP + 抓包

这是整个 JD 最关键部分。

也是你和普通软件工程师拉开差距的地方。

---

必学内容

1. TCP/IP

学习：

IP

Port

TCP 三次握手

Socket

Client/Server

---

达成目标

你必须：

能解释：

为什么设备连接失败

为什么端口被占用

为什么断线重连失败

---

2. SECS/GEM（核心）

必须学习：

HSMS

S1F1

S6F11

Event Report

Alarm

Remote Command

Equipment Status

---

达成目标

你必须做到：

能看懂：

S1F1 Are You There
S1F2 On Line Data

能知道：

谁发给谁

为什么报错

通信处于什么状态

---

3. 抓包

学习：

Wireshark

TCP流分析

Filter

Port过滤

---

达成目标

你必须做到：

能抓：

TCP通信

SECS/GEM消息

能定位：

断连

超时

Message格式异常

---

推荐项目（非常重要）

你必须做一个：

“模拟 SECS/GEM 通信工具”

功能：

Client/Server

发消息

接收消息

日志记录

语言：

C++

或 C#

这个项目能直接写简历。

---

Deadline

第8周结束：

必须做到：

会 Wireshark

能分析 TCP

能看懂 SECS/GEM 基础消息

完成一个 Socket 通信项目

---

第四阶段（第9-12周）

目标：现场问题处理能力

这是企业最看重的。

---

必学能力

1. 故障定位流程

学习：

现象
→ 日志
→ 通信
→ 软件
→ 数据库
→ 硬件

---

达成目标

你必须能：

对下面问题给出排查步骤：

场景：

“设备报警不上报 MES”

你必须能分析：

网络？

SECS/GEM？

数据库？

服务挂了？

Event没配置？

---

2. 文档能力

学习：

SOP

Issue Report

Root Cause Analysis

---

达成目标

你必须能写：

故障报告

格式：

问题现象
复现步骤
日志分析
根因
解决方案
预防措施

---

3. 客户沟通

必须训练：

问题确认

信息收集

状态同步

---

Deadline

第12周结束：

必须做到：

能独立分析现场问题

能写故障报告

能写 SOP

能给客户做简单培训

---

第五阶段（第13-16周）

目标：达到可面试状态

---

简历必须具备：

项目1

SECS/GEM 通信模拟系统

包括：

Socket

多线程

日志

TCP

Message解析

---

项目2

设备报警管理系统

包括：

SQL

Web/API

Alarm处理

---

面试必须准备

Linux

必须能回答：

tail 和 grep 怎么排日志

端口占用怎么查

服务挂了怎么办

---

网络

必须会：

TCP三次握手

Socket通信流程

Wireshark怎么抓包

---

C++

重点：

多线程

Socket

STL

JSON/XML

日志系统

---

半导体

必须知道：

MES

EAP

Recipe

Alarm

SECS/GEM

---

最终目标（16周）

达到：

“初级半导体设备软件支持工程师可就业水平”

你会具备：

Linux排障

TCP/IP

Socket

SECS/GEM

SQL

设备联调

客户支持

文档能力

这时候你已经不是普通 C++ 开发了，而是：

“工业软件 + 半导体设备 + 通信协议”方向

这个方向比普通互联网开发更稳定，而且经验越久越值钱。

你现在最缺的不是代码能力。

而是：

工业现场思维

通信协议

排障能力

半导体业务认知

这几个补起来，你转这个岗位是有机会的。
