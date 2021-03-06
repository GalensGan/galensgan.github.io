---
layout: post
category: MS Develop
title: MS DgnTool 学习（一）
tagline: by 明不知昔
tags: 
  - Bentley 二次开发
  - DgnTool
  - C#
published: true
---

DgnTool 是在 MS 上二次开发时会经常用到的交互类，重要性便不言而喻了。在此记录自己的学习心得。

<!--more-->

## 继承关系

``` mermaid
graph BT
locate[LocateSubEntityTool]-->iview[IViewTransients]
region[DgnRegionElementTool]-->iview

locate-->graphic[ElementGraphicsTool]

graphic-->eleset[DgnElementSetTool]
eleset-->primitive[DgnPrimitiveTool]

region-->eleset
eleset-->redraw[IRedrawOperation]
eleset-->modify[ModifyOp]
modify-->imodify[IModifyElement]

primitive-->tool[DgnTool]
tool-->counted[RefCountedBase]
counted-->countedlist[RefCounted < IRefCounted >]

countedlist-->icount[IRefCounted]

dgnview[DgnViewTool]-->tool
```

## DgnTool

DgnTool 是所有 Tool 类的基类。

应用程序创建的交互类不能从 DgnTool 直接继承，要继承于 DgnViewTool 或者 DgnPrimitiveTool。



## DgnViewTool

DgnViewTool 可以用来实现视图命令。

 使用 DgnViewTool 将挂起当前活动的原命令，直到它退出。 使用 DgnViewTool 不应该更改文件或任何可能影响活动原命令的内容。