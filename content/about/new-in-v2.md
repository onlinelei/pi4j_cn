---
title: '新特性 (V.2)'
weight: 30
---

## 2.0 新特性

Pi4J 2.0 版本带来了许多新功能，以及一个全新的体系结构，它将专注于可扩展性、简化的集成和先进的 Java API，主要有以下内容：

* 流畅的 API 接口
* 可控的上下文环境
* 可扩展的插件架构体系
* 用于创建新 I/O 实例的生成器模式
* 完善的文档，和源代码
* 硬件 PWM 支持
* Java 11

未来计划：

* 通过 Pi4J 注解进行依赖注入
* 支持远程 I/O（通过TCP/IP）

除了上面列出的功能外，Pi4J 2.0 版本还放弃了旧的 WiringPi 引脚编号方案，转而采用更为传统和常用的 Broadcom 引脚编号方案。多年来，这种引脚编号方案一直比较混乱，对于初学者来说经常摸不到头脑。并且由于新的 Raspberry Pi 型号引入了新的 GPIO 引脚，以至于维护起来有些麻烦。今后，Pi4J将只使用 Broadcom（BCM）的引脚编号方案。

WiringPi 项目现在已经废弃 (详情请查看： [wiringpi.com/wiringpi-deprecated/](http://wiringpi.com/wiringpi-deprecated/))。Pi4J 2.0 版本将不再基于WiringPi，而是在内部使用 PIGPIO ([http://abyz.me.uk/rpi/pigpio/](http://abyz.me.uk/rpi/pigpio/)) 库进行底层集成。通过这次迁移，运用 PIGPIO 守护进程，我们还将支持远程 I/O 特性（通过 TCP 连接）


## 和 V.1 版本对比有什么不同

从 Pi4J 2.0 版本开始构建以来，Pi4J 项目将重点放在了用 Java 程序，控制和访问树莓派平台的核心 I/O 。在 Pi4J 的早期版本中，在项目范围上过于宽泛，导致项目严重膨胀，以至于项目难以维护。现在的目标转移到树莓派底层的 I/O 功能范围内，并将更快的响应 bug 的修复，以及新平台的引入。新的项目范围通过降低访问底层 I/O 复杂性，更好的额服务于 Java 社区。

下面的一些特性在 Pi4J 库中被移除：

* **IO 扩展** -- IO 扩展仍然会提供支持，但是会在 Pi4J 核心包之外提供，这样也方便与他们的独立维护和扩展。

* **其他平台** -- 其他的一些平台，例如： Odroid、BananaPi、NanoPi、OrangePi 等已被移除，将不再支持。这些额外平台的挑战在于 Pi4J 依赖于底层的 WiringPi 项目，而这些其他平台的 WiringPi 端口并没有得到各种 SoC 供应商或社区的良好支持。这些其他平台的各种 WiringPi 端口也不一致，导致 Pi4J 的特性和功能表现不一致。而且 Pi4J 项目的，bug 修复和新功能的回归测试，需要在每个平台上测试通过。

* **组件、设备** -- Pi4J 原本为组件和设备提供更高级别的接口，在现实世界的设备和底层的 I/O 接口之间提供抽象层，虽然这是一个崇高的目标，但不幸的是，该项目的这一部分没有得到应有的关注，也没有被社区广泛采用。我们正在删除这些，以便于 Pi4J 能专注于 Raspberry Pi 平台底层 I/O。

## 源码

Pi4J 2.0 版本的源代码 GitHub 地址：[Pi4J V.2 GitHub Repository](https://github.com/Pi4J/pi4j-v2)

```shell
git clone https://github.com/Pi4J/pi4j-v2
```

Pi4J 2.0 版本于 2021 年 8 月首次发布。从 V.1 到 V.2 的返工花费了一些时间并且还在继续，但我们确信这是一个在 Raspberry Pi 上开发 Java 应用程序的好库。欢迎大家在 github 中提出任何评论和bug 或者参与到项目的开发中。
