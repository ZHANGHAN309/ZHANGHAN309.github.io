---
title: ASP.NET Boilerplate笔记
date: 2026-06-24 11:30:46
tags:
---

# ABP架构

## 表现层(Presentation Layer)

Web项目（MVC/Razor Pages/Blazor）
API项目（RESTful API）
移动客户端接口

## 分布式服务层(Distributed Service Layer)

应用服务(Application Services)
DTO自动映射
API版本控制
动态Web API

## 应用层(Application Layer)

应用服务实现
数据传输对象(DTOs)
工作单元(Unit of Work)
授权和验证

## 领域层(Domain Layer)

实体(Entities)
值对象(Value Objects)
聚合根(Aggregate Roots)
领域服务(Domain Services)
规约(Specifications)
仓储接口(Repository Interfaces)

## 基础设施层(Infrastructure Layer)

数据访问实现(Entity Framework Core)
缓存实现(Redis)
后台作业(Hangfire/Quartz)
文件存储(Blob Storage)
