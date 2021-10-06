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

从 Pi4J 2.0 版本开始构建以来，Pi4J 项目将重点放在了用 Java 程序

Starting with the Pi4J 2.0 builds, the Pi4J project is prioritizing focus on providing Java programs access, 
control and communication with the core I/O capabilities of the Raspberry Pi platform. Earlier versions of Pi4J were 
perhaps too ambitious in scope and that led to significant project bloat to the point that the project was becoming 
unsustainable. The goal moving forward is to limit scope to that of the raw I/O capabilities of the Raspberry Pi 
platform and provide timely updates and releases for bug fixed and new RaspberryPi model introductions. Reducing 
the scope of the project should better serve the Java community for basic I/O access by reducing complexity.

The following features have been removed from the Pi4J library:

* **IO Expanders** -- IO expansion is still supported but concrete implementations should be provided outside the core Pi4J core project such that they can be maintained and extended independently.
* **Other Platforms** -- Other platforms such as Odroid, BananaPi, NanoPi, OrangePi, etc. have been removed and will no longer be supported. The challenge with supporting these additional platforms is that Pi4J depends on the underlying WiringPi project and WiringPi ports for these other platforms is not well supported by the various SoC vendors or community. The various WiringPi ports for these other platforms are also inconsistent causing inconsistent features and functionality of Pi4J. Additionally, regression testing of bug fixes and new features in Pi4J is compounded with each additional supported platform.
* **Components & Devices** -- Pi4J originally provided higher level interfaces for components and devices that provided an abstraction layer between real world devices (things) and lower-level I/O interfaces. While a noble goal, unfortunately this part of the project never received the attention and time that it deserved and never gained much adoption by the community. We are removing these to allow Pi4J to focus solely on the raw I/O supported by the Raspberry Pi platform.

## Sources

The Pi4J V.2 source code is available in this GitHub repository: [Pi4J V.2 GitHub Repository](https://github.com/Pi4J/pi4j-v2)

```shell
git clone https://github.com/Pi4J/pi4j-v2
```

Pi4J V.2 had the first release in August 2021. Rework from V.1 to V.2 took quit some time and will never be finished, but
we are confident this is a great library to develop Java application on the Raspberry Pi. Any remarks and contributions
are welcome as either bug reports or discussions in the [GitHub repository](https://github.com/Pi4J/pi4j-v2).