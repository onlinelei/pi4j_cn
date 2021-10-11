---
title: 使用 VSC 进行 Java 开发
weight: 40
---

## 在树莓派上使用 Java 

Pi4J V2 需要在 Java 11 或更新版本下运行。幸运的是，在 2019-06-20 发布的树莓派系统中，已经包含了 OpenJDK Java 11，可以在发行说明中看到：

```
2019-06-20:
Based on Debian Buster
Oracle Java 7 and 8 replaced with OpenJDK 11
```
但是需要注意的是这个版本**仅与 ARMv7 或更高版本兼容**并且不支持所有 Raspberry Pi 开发板。如果您有 Raspberry Pi A（版本 3）、B（版本 2 或更高版本）或 Compute（版本 3 或更高版本），那么您就可以开始使用了！对于其他开发板，可以在需要在 ["Java for ARMv6/7/8"](/documentation/java-installation/) 中找到响应的帮助。

如果您准备了一张带有最新版本 Raspberry Pi 系统（完整版）的 microSD 卡，安装步骤在 ["设置新的 Raspberry Pi"](/getting-started/set-up-a-new-raspberry-pi/ )，启动树莓派，可以在终端查看安装的 Java 版本。在带有 ARMv7 或 ARMv8 的板上，您将得到以下结果：

```
$ java -version
openjdk version "11.0.3" 2019-04-16
OpenJDK Runtime Environment (build 11.0.3+7-post-Raspbian-5)
OpenJDK Server VM (build 11.0.3+7-post-Raspbian-5, mixed mode)
```

如果出现了下面的错误提示，可以在需要在 ["Java for ARMv6/7/8"](/documentation/java-installation/) 中找到响应的帮助。

```
$ java -version
Error occurred during initialization of VM
Server VM is only supported on ARMv7+ VFP
```

## Maven

Pi4J 使用 Maven 作为构建工具，Maven 工具通过项目根目录的 pom.xml 配置文件，可以将所需模块的代码编译为 JAR 文件。安装完 Maven 后可以使用打个命令完成此操作，通过以下的命令来安装 Maven，以及查看 Maven 版本 :

```
$ sudo apt install maven
$ mvn -v
Apache Maven 3.6.0
Maven home: /usr/share/maven
```

## Visual Studio Code

Visual Studio Code (VSC) 是 Microsoft 提供的免费 IDE（集成开发人员环境）。它被设计为一种通用工具，您可以安装插件，使其支持多种编程语言。在您的 Raspberry Pi 上打开 Web 浏览器，跳转到 ["VSC 下载页面 (code.visualstudio.com/Download)"](https://code.visualstudio.com/Download) 选择“Linux .deb ARM”版本。

{{< gallery >}}
{{< figure link="/assets/getting-started/vsc/visualstudiocode-download.png" caption="Download page for VSC" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/vsc/programming-tools.png" caption="VSC in the list of programming tools" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/vsc/vsc-on-raspberry-pi.png" caption="VSC running on the Raspberry Pi with Maven and Java Extension Pack" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

下载完成过后，打开 terminal，进入到 Download 文件夹，通过下面的命令进行安装：

```
$ cd /home/pi/Downloads
$ sudo apt install ./code_1.53.0-1612367698_armhf.deb 
```

自 2021 年 2 月起，还有一种更简单的方法，因为 Visual Studio Code 现在可作为 Raspberry Pi OS apt 包使用。使用以下命令进行安装：

```
$ sudo apt update
$ sudo apt install code -y
```

