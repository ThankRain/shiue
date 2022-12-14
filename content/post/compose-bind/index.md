---
title: "Jetpack Compose 中ComposeView 绑定到Dialog中遇到的问题"
date: 2022-07-13T12:58:52+08:00
draft: false
description: 在Compose 1.2.0-alpha08 以前，可以使用以下代码:...
slug: compose-bind
image: /renato-ramos-puma.jpg
categories:
- Android
tags:
- Compose
- Android
---

> 封面来源 [Unsplash](https://unsplash.com/photos/_9bDW5I9D_8)

在Compose 1.2.0-alpha08 以前，可以使用以下代码

```Kotlin
val dialog = Dialog(context)
dialog.window?.decorView?.apply {
    ViewTreeLifecycleOwner.set(this, this@MainActivity)
    ViewTreeViewModelStoreOwner.set(this, this@MainActivity)
    ViewTreeSavedStateRegistryOwner.set(this, this@MainActivity)
    }
```

在Compose 1.2.0-alpha08以后，`ViewTreeSavedStateRegistryOwner`的API发生了变更

```Kotlin
val dialog = BottomSheetDialog(this@MainActivity)
dialog.window?.decorView?.apply {
    ViewTreeLifecycleOwner.set(this, this@MainActivity)
    ViewTreeViewModelStoreOwner.set(this, this@MainActivity)
    setViewTreeSavedStateRegistryOwner(this@MainActivity)
    }
```

## 参考内容

[更新日志： Update ViewTreeSavedStateRegistryOwner use in Compose UI](https://android.googlesource.com/platform/frameworks/support/+/6d15b0171dfefdc911f9eda905855cebbd8da231)

[ComponentActivity 源码 1.2.0-alpha08](https://android.googlesource.com/platform/frameworks/support/+/6d15b0171dfefdc911f9eda905855cebbd8da231/activity/activity-compose/src/main/java/androidx/activity/compose/ComponentActivity.kt)