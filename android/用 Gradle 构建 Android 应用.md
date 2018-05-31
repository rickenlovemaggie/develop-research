# 用 Gradle 构建 Android 应用

Android Studio 默认通过 Gradle 来构建 Android 应用，Gradle 支持使用 [Groovy](http://groovy-lang.org/) 或者 [Kotlin](https://kotlinlang.org/) 来编写构建脚本，简单来说 Gradle 的有点有如下几点：

- 非常灵活；
- 构建速度快
- 十分强大：支持很多主流语言；

> 更多的 Gradle 特性参考 [Gradle 用户指南](https://docs.gradle.org/current/userguide/userguide.html)


本文着重于 Gradle 基本的概念、类、以及 Gradle 脚本的编写，对一些如增量编译、构建缓存等特性不做介绍。


## Gradle 基本概念

Gradle 项目一般由一个或者多个项目（project）组成，一般来说至少有一个根项目，根项目中可能包含多个子项目，当然子项目中也可以包含自身的子项目。根项目往往用于组织整个项目结构，提供通用配置或者必要的插件路径等。项目由一个或者多个任务（task）组成，task 将 project 划分为多个子操作，每个 task 执行不同的操作，最终完成整个 project 所有的操作。

Gradle 主要使用了 3 种脚本文件，每一种脚本都是针对于不同的对象：

- 构建脚本（build.gradle）：针对于 [Project](https://docs.gradle.org/current/dsl/org.gradle.api.Project.html) 对象。
- 设置脚本（settings.gradle）：针对于 [Settings](https://docs.gradle.org/current/dsl/org.gradle.api.initialization.Settings.html) 对象。
- 初始化脚本：主要用于全局配置，针对于 [Gradle](https://docs.gradle.org/current/dsl/org.gradle.api.invocation.Gradle.html) 对象。


### Project 对象

Project 对象是整个 Gradle 项目的最重要的接口，和 build.gradle 文件是一一对应的，通过 Project 对象，你可以访问所有的 Gradle 项目的特性。有关 Project 对象具体可以参见 [Project 对象](https://docs.gradle.org/current/dsl/org.gradle.api.Project.html)，我这里就不重复了，只提炼出几个最重要的点：

#### Gradle 构建工程的步骤：

- Gradle 首先会创建一个 Settings 实例 settings；
- 根据 settings.gradle 脚本（如果存在）来配置 settings 实例；
- 利用 settings 实例来创建具有层级关系的 Project 实例 project（可能会有多个）；
- 最后，执行每个项目中的 build.gradle 脚本（如果存在）。

> project 表示 Gradle 项目，project 对象表示可以在 build.gradle 文件直接使用的 Project 类的实例。

从构建步骤可以看出，build.gradle 脚本文件是我们构建过程中最为重要的文件，其他所有的文件（如 gradle.properties）都是为该文件服务的。







