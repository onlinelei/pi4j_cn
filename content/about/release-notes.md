---
title: '发行说明'
weight: 40
---

## 2021-08-26 2.0

它来了它来了！经过大量工作，现在我们向你汇报 Pi4J 库的成果！

2.0 版本的重要变更：

* 支持 Java 11 或者更高
* 打破 V1 版本的架构，进行了完全的重构（详情请参考： [pi4j.com/architecture](https://pi4j.com/architecture/)）
* 不再包含外围设备的支持逻辑，附加芯片组/板的逻辑被抽离出核心模块
* 更易于扩展、测试和维护
* 使用 PiGpio 作为原生库（在 V1 版本中使用的是 WiringPi 在 2019 年被弃用）
* 模块化的构建，完全支持 Java 的未来发展
* 少量的外部依赖（仅仅使用到 SLF4J）
* 不同的场景示例代码（还有 JavaFX）详情请参考： [pi4j.com/getting-started](https://pi4j.com/getting-started/)
* 更多请参考：[pi4j.com/about/new-in-v2](https://pi4j.com/about/new-in-v2/)



