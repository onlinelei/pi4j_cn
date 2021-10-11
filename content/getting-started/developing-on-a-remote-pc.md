---
title: 在远程 PC 上进行开发
weight: 45
---

{{% notice note %}}
GITHUB 项目: [https://github.com/Pi4J/pi4j-maven-archetype](https://github.com/Pi4J/pi4j-maven-archetype)
{{% /notice %}}

## 使用远程 PC 工作站开发 Java 程序

直接在 Raspberry Pi 板上编写您的 Java 程序，编译并运行它，像前一章说的那样，完全没问题。我们还可以使用普通台式计算机作为远程开发工作站（RDW）。

这个 [Maven Archetype]（https://github.com/Pi4J/pi4j-maven-archetype "raspimaven-archetype"）会给你一个工具来生成Pi4J-V2骨架Java项目。你可以将它用于你的下一个 Pi4j 项目，你可以在远程工作站 (RDW) 上开发你的程序，编译它们，在目标 Pi 板上传输可执行代码并运行它。同样还可以启动远程调试。

使用这样的开发模式，会有一些优点和缺点：

- 优点：
    - 与 Raspberry Pi 相比，您的 RDW 拥有更强的能力，例如内存、磁盘容量和 CPU 功率，这对于 P4 型号也是如此。您可以将所有程序存储在台式计算机中。
    - 您不必在 Raspberry Pi 上安装 Visual Studio Code（或者其他的 IDE 程序）、不用安装 Java JDK（JRE 就足够了）、以及 Maven 和其他开发工具。而且不需要将屏幕、键盘和鼠标连接到 Raspberry Pi
    - 可以使用小的 PI 型号
- 缺点：
    - 你不能运行 Web 项目（使用 web 容器，例如 Tomcat 或者 similar）

## 设置
### Configure the RPi for Headless mode
The _Headless Mode_ configuration enables the RPi board to communicate with the RDW over SSH protocol.
These are the needed steps:
- Check if the RDW is equipped with a SSH Client. If the RDW OS is Linux you already have it 
- For Windows you can use _putty_, _MobaXterm_ or you can enable the (new) OpenSsh Client porting on Windows 10
- Connect both the RPi and RDW to your local network
- Follow [this guide](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md "Setting up a Raspberry Pi headless") 
to configure your RPi 
- Install the Maven tool on the RDW

You should now be able to open a SSH Terminal window on RDW and to remotely login on the RPi board.
### Install the _raspimaven-archetype_
- Goto the [Github Pi4J Project](https://github.com/Pi4J/pi4j-maven-archetype "raspimaven-archetype") and download the project
clicking on the green _Code_ button and selecting _Download ZIP_
- Unzip the archetype file in an empty folder, let say _my-folder_
- `cd my-folder/raspimaven-archetype`
- `mvn install`

_Congratulation ! - Now you are ready to generate your first **Project Template**_

### Generate a new Project Template
Let suppose you want to begin the new wonderful PI4J-V2 project _my-project_, to do this follow these steps:
- `mkdir my-project`
- `cd my-project`
- `mvn archetype:generate -DarchetypeCatalog=local`
- answer to the questions the archetype asks you (see below for details)
### Configuring your new project
Before starting the new project generation, the archetype asks some configuration data. The list of question
and the replies are shown here below:
1. _Choose archetype:_ **select the _raspimaven-archetype_ from the list proposed**
1. _Define value for property 'groupId':_ **choose the Maven groupId for your project.** (If don't know what is a groupId, don't worry, just type _"com.example"_ for now)
1. _Define value for property 'artifactId':_ **choose a name for the program executable your project will produce**
1. _Define value for property 'version':  1.0-SNAPSHOT:_ **type Enter to accept the default value shown, or type the initial program version, something like _1.0.0_**
1. _Define value for property 'package':  com.example:_ **type Enter to accept the default value shown**

The archetype now shows you a summary of the configuration parameters you have just typed in, plus the values proposed for the _main-class_ and _package_ parameters.
If the list is ok for you, reply _Y_ to accept, otherwise reply _N_ to change one or more values (you will have to re-type all parameter values ...)

After the list confirmation, the archetype generates a new maven project template for you. 

**Congratulations** 

You should be able to open the new project with your preferred java IDE. The IDE should be able
to recognize the project as a valid Maven project.
### Explore the new project template
Feel free to explore the new project familiarizing with the folder structure. These are the most important features:
- The file README.md contains the intruction to configure the connection(s) to your RPi board(s) and the decription of the Maven
commands to build your project, transfer the executable code to the target RPi, run it and also open a debugger session.
- The _pom.xml_ file already includes the dependencies needed to compile your program with the JPi4J-V2 libraries.
- The _platform_ folder contains an example configuration file for connecting to you RPi board. Read the README.md explanation,
open the _platform/raspberry.properties_ file (or copy it to a new file) and edit it to describe how to connect to your RPi

