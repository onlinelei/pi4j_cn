---
title: 在远程 PC 上进行开发
weight: 45
---

{{% notice note %}}
GITHUB 项目地址： [https://github.com/Pi4J/pi4j-maven-archetype](https://github.com/Pi4J/pi4j-maven-archetype)
{{% /notice %}}

## 使用远程 PC 工作站开发 Java 程序

直接在 Raspberry Pi 板上编写您的 Java 程序，编译并运行它，像前一章说的那样，完全没问题。我们还可以使用普通台式计算机作为远程开发工作站（RDW）。

这个 [Maven Archetype](https://github.com/Pi4J/pi4j-maven-archetype)会给你一个工具来生成Pi4J-V2骨架Java项目。你可以将它用于你的下一个 Pi4j 项目，你可以在远程工作站 (RDW) 上开发你的程序，编译它们，在目标 Pi 板上传输可执行代码并运行它。同样还可以启动远程调试。

使用这样的开发模式，会有一些优点和缺点：

- 优点：
    - 与 Raspberry Pi 相比，您的 RDW 拥有更强的能力，例如内存、磁盘容量和 CPU 功率，这对于 P4 型号也是如此。您可以将所有程序存储在台式计算机中。
    - 您不必在 Raspberry Pi 上安装 Visual Studio Code（或者其他的 IDE 程序）、不用安装 Java JDK（JRE 就足够了）、以及 Maven 和其他开发工具。而且不需要将屏幕、键盘和鼠标连接到 Raspberry Pi
    - 可以使用小的 PI 型号
- 缺点：
    - 你不能运行 Web 项目（使用 web 容器，例如 Tomcat 或者 similar）

## 设置
### 为树莓派配置无界面模式

无界面模式可以使树莓派通过 SSH 协议连接 RDW（远程工作站）

步骤：
- 检查 RDW 是否有 SSH 客户端，如果 RDW 是 Linux 系统，那就已经具备了客户端。
- 对于 Windows 用户，您可以使用 _putty_、_MobaXterm_ 如果是 Windows 10 系统 可以启用 OpenSsh 客户端
- 将树莓派和 RDW 同时连接本地局域网
- 按照 [本指南](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md“设置树莓派无界面模式”)配置您的树莓派
- 在远程工作站上安装 Maven

您现在应该能够在 RDW 上打开 SSH 终端窗口并远程登录到树莓派。

### 安装 _raspimaven-archetype_
- 从 [Github Pi4J 项目](https://github.com/Pi4J/pi4j-maven-archetype "raspimaven-archetype") 下载项目，点击绿色的 _Code_ 按钮，选择 _Download ZIP_
- 解压下载的文件到一个空的文件夹（这里是 my-folder）
- `cd my-folder/raspimaven-archetype`
- `mvn install`
_恭喜！- 你已经生成了你的第一个项目**模板**_

### 生成新的项目模板
假设您要开始新的 PI4J-V2 项目 _my-project_，请按照以下步骤操作：
- `mkdir my-project`
- `cd my-project`
- `mvn archetype:generate -DarchetypeCatalog=local`
- 回答命令放纵原型问你的问题（详情见下文）


### 配置新项目

在开始新项目生成之前，原型会询问一些配置数据。问题列表和回复如下所示：

1. _选择原型：:_ **从建议的列表中选择 _raspimaven-archetype_**
2. _定义属性 ’groupId‘ 的值:_**为您的项目选择 Maven groupId。**（如果不知道 groupId 是什么，不用担心，现在只需输入 _"com.example"_）
3. _定义属性 'artifactId':_ **为您的项目将生成的程序可执行文件定义一个名称**
4. _定义属性 'version':  1.0-SNAPSHOT:_**键入 Enter 以接受显示的默认值，或者键入初始程序版本，例如 _1.0.0_**
5. _定义属性 'package':  com.example:_ **键入 Enter 以接受显示的默认值**

原型现在显示您刚刚输入的配置参数的摘要，以及为 _main-class_ 和 _package_ 参数建议的值。

如果列表无误，请回复 _Y_ 以接受配置，否则回复 _N_ 然后更改一个或多个值（您必须重新键入所有参数值...）


列表确认后，原型为你生成一个新的maven项目模板。

**恭喜** 

使用你的 Java IDE 开发工具打开这个新项目。 IDE 会将项目识别为有效的 Maven 项目。

### 浏览新的模板项目
随意探索新项目，熟悉文件夹结构。这些是最重要的功能：

- README.md 文件包含配置信息，还有和树莓派开发板的连接的说明，以及用于构建项目、将可执行代码传输到目标 RPi、运行它并打开调试器的 Maven 命令的描述。
- _pom.xml_ 文件已经包含使用 JPi4J-V2 库所需的依赖。
- _platform_ 文件夹包含用于连接到树莓派板的示例配置文件，阅读 README.md 说明，打开 _platform/raspberry.properties_ 文件（或者备份后）来配置连接到您的 RPi 的参数 