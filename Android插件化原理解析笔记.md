# Android插件化原理解析笔记

# 概要笔记

### 代码加载

1. 类加载需要JAVA的**ClassLoader**，但Android的组件是有生命周期，所以需要**组件生命周期**来进行管理

2. 对加载进来的类进行管理，防止混乱

### 资源加载

使用AssetManager的隐藏方法addAssetPath

问题：不同插件的资源如何管理，公用还是各自插件一套，公用资源如何避免资源冲突

### 插件化方案

DL和DroidPlugin，文章主要以讲解DroidPlugin来解析插件框架原理

------



## HOOK机制之动态代理

JAVA的动态代理，使用Proxy.newProxyInstance()方法

