---
title: 设置一个新的树莓派
weight: 30
---

## 介绍

Raspberry Pi 是一款功能强大的机器，有很多的使用示例。这很大程度上是基于您使用的操作系统，对于我们的“入门”示例，使用的是“官方 RaspberryPi OS”（以前称为“Raspbian OS”）。还有其他很多可玩性，例如在 GitHub 上的[“Awesome Raspberry Pi”列表](https://github.com/thibmaek/awesome-raspberry-pi/blob/master/README.md).

在本文中，我们从全新的 Raspberry Pi 开发板开始。

## 一步步来

第一步：当然是从盒子里将新的树莓派取出来 :-)

仔细看看，你手里拿着的才是真正的杰作。技术工程的奇迹，完美结合了强大而廉价的组件。

但要注意！这也是一些敏感的电子产品。首先触摸电源插座的接地引脚始，以确保您的身体没有静电，如果有静电可能会损坏板子。


TODO 添加图片。

### 材料清单

* Raspberry Pi
* 内存卡，最低 16 GB
* 电脑（或者其他的树莓派）
* 带有 SD 卡插槽的 PC（或其他树莓派）（也许您需要一个 SD 卡适配器）
* 电源（5V，2A 或者 3A）
* 显示器、键盘、鼠标

### SD card

SD 卡将保存操作系统。在 Raspberry Pi 官网上，[下载页面，找到 Imager 工具](https://www.raspberrypi.org/software/)。选择适合您电脑的版本，下载并安装。

![Imager download](/assets/getting-started/setup/download-imager.png)

启动 Imager 工具并按照以下步骤操作：

1. 点击“操作系统”>“选择操作系统”
2. 选择“树莓派操作系统（其他）”
3. 选择“Raspberry Pi OS Full (32-bit)”

{{< gallery >}}
{{< figure link="/assets/getting-started/setup/imager-os-1.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-os-2.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-os-3.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}


通过选择“完整”版本，我们将拥有一个预装了大量附加工具的操作系统，包括“OpenJDK 11”，因此将能够快速开始 Java 开发。

4. 将您的 SD 卡插入您的计算机或您可以连接到 USB 的 SD 卡读卡器
5.点击“SD卡”>“选择SD卡”
6.选择SD卡

TODO 添加图片

### 首次启动

#### 树莓派操作系统其他设置

#### 检查 Java 版本

由于我们已将完整的操作系统烧录在 SD 卡上，因此 Java 已经可用。打开终端窗口并输入`java -version`。可以看到 Java 版本。

```
$ java -version
openjdk version "11.0.9" 2020-10-20
OpenJDK Runtime Environment (build 11.0.9+11-post-Raspbian-1deb10u1)
OpenJDK Server VM (build 11.0.9+11-post-Raspbian-1deb10u1, mixed mode)
```

### 安装 Pi4J

TODO

## 使您的 Raspberry Pi 保持最新状态

### 更新到最新

打开终端并执行以下命令:

```
sudo apt update
sudo apt full-upgrade
```

Raspberry Pi OS 基于 [Debian](https://www.debian.org/) - 它是最大的 Linux 发行版之一，您正在使用的是 Raspberry Pi OS 版本（例如 Debian V9，又名 Stretch）。定期运行这些命令，可以使您的系统保持最新。更新命令不会从一个主要版本更新到另一个版本，例如，Stretch (V9) 到 Buster (V10)。