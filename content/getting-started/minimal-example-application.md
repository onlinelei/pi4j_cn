---
title: 最小示例程序
weight: 50
tags: ["Digital Input", "Digital Output"]
---

{{% notice note %}}
GITHUB 项目地址： [https://github.com/Pi4J/pi4j-example-minimal](https://github.com/Pi4J/pi4j-example-minimal)
{{% /notice %}}

["pi4j-example-minimal" GitHub 项目](https://github.com/Pi4J/pi4j-example-minimal) 包含使用 Pi4J 控制数字输入和输出的示例小程序。本章会详细解释这个项目。这个程序会打开/关闭 LED，每次按下按钮时，闪烁频率会加大。按下第 5 次的时候，应用程序将停止。

{{< vimeo 525570174 >}}

## 接线

这个示例程序接线如下图所示：

![](/assets/getting-started/minimal/led-button_bb.png)

## 构建程序

Pi4J 项目使用到的最主要的构建工具就是 Maven，但是在这个示例中我们提供了 Maven 和 Gradle 两种构建方式，你可以根据你的情况进行选择性使用。

### Maven

这个示例程序可以使用 Apache Maven 3.6（或者更高版本）Java 11 OpenJDK（或者更高版本）如前几页所述。必须在构建此项目之前安装这些工具。可以使用以下命令下载所有项目依赖并编译Java模块。您可以使用 Java 11+ 直接在 Raspberry Pi 上构建此项目。

```
mvn clean package
```

### Gradle

您还可以使用 Gradle 6.6（或更高版本）和 Java 11 OpenJDK（或更高版本）。
Gradle 包装器的使用方法参考 [docs.gradle.org](https://docs.gradle.org/current/userguide/gradle_wrapper.html)。
Gradle 配置文件参考 [build.gradle-file](https://github.com/Pi4J/pi4j-example-minimal/blob/main/build.gradle) 

Linux 系统:

```
./gradlew build
```

Windows 系统:

```
gradlew.bat build
```

## pom.xml 依赖

对 Maven 项目来说，pom.xml 中定义了项目的所有依赖，以及构建流程。
在本项目中，我们使用了 slf4 来打印日志， pi4j-core 和 pi4j-plugins 来控制树莓派 GPIO 为了方便版本升级，我们添加了版本的配置文件。

```xml
<properties>
    <!-- DEPENDENCIES VERSIONS -->
    <slf4j.version>1.7.32</slf4j.version>
    <pi4j.version>2.0</pi4j.version>
</properties>
```

下面是本项目依赖的包：

```xml
<dependencies>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>${slf4j.version}</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-simple</artifactId>
        <version>${slf4j.version}</version>
    </dependency>

    <!-- include Pi4J Core -->
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-core</artifactId>
        <version>${pi4j.version}</version>
    </dependency>

    <!-- include Pi4J Plugins (Platforms and I/O Providers) -->
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-plugin-raspberrypi</artifactId>
        <version>${pi4j.version}</version>
    </dependency>
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-plugin-pigpio</artifactId>
        <version>${pi4j.version}</version>
    </dependency>
</dependencies>
```

## 使用到的 Pi4J 代码块

### 初始化


Before you can use Pi4J you must initialize a new runtime context.

The 'Pi4J' static class includes a few helper context creators for the most common use cases.  The 'newAutoContext()' method will automatically load all available Pi4J extensions found in the application's classpath which may include 'Platforms' and 'I/O Providers'.
        
```java
var pi4j = Pi4J.newAutoContext();
```

### Output Pi4J Context information

The library contains helper functions to output info about the available and used platforms and providers. To keep the example code clean, these are part of the "PrintInfo.java" class. For example to print the loaded platforms:

```java
Platforms platforms = pi4j.platforms();

console.box("Pi4J PLATFORMS");
console.println();
platforms.describe().print(System.out);
console.println();
```

### Handle the button presses

To handle digital input events we first need a configuration for it. With that configuration, Pi4J can create the object for us and the state changes can be handled.

```java
private static int pressCount = 0;
private static final int PIN_BUTTON = 24; // PIN 18 = BCM 24

var buttonConfig = DigitalInput.newConfigBuilder(pi4j)
      .id("button")
      .name("Press button")
      .address(PIN_BUTTON)
      .pull(PullResistance.PULL_DOWN)
      .debounce(3000L)
      .provider("pigpio-digital-input");
      
var button = pi4j.create(buttonConfig);

button.addListener(e -> {
       if (e.state() == DigitalState.LOW) {
              pressCount++;
              console.println("Button was pressed for the " + pressCount + "th time");
       }
});
```

### Toggle a LED

For the LED we use a similar approach with a configuration. The created led-object can be used to toggle its state.

```java
private static final int PIN_LED = 22; // PIN 15 = BCM 22

var ledConfig = DigitalOutput.newConfigBuilder(pi4j)
      .id("led")
      .name("LED Flasher")
      .address(PIN_LED)
      .shutdown(DigitalState.LOW)
      .initial(DigitalState.LOW)
      .provider("pigpio-digital-output");
      
var led = pi4j.create(ledConfig);

while (pressCount < 5) {
      if (led.equals(DigitalState.HIGH)) {
           led.low();
      } else {
           led.high();
      }
      Thread.sleep(500 / (pressCount + 1));
}
```

### Closing the application

Before the application quits, we need to call the 'shutdown()' function on the Pi4J static helper class. This will ensure that all I/O instances are properly shutdown, released by the the system and shutdown in the appropriate manner. Terminate will also ensure that any background threads/processes are cleanly shutdown and any used memory is returned to the system.

```java
pi4j.shutdown();
```

## Steps to run this application on your Raspberry Pi

* Attach a LED and button as shown in the image above
* Use a recent Raspbian OS image which has Java 11. To check if you have the correct Java version in the terminal:

```
$ java -version
openjdk version "11.0.6" 2020-01-14
OpenJDK Runtime Environment (build 11.0.6+10-post-Raspbian-1deb10u1)
OpenJDK Server VM (build 11.0.6+10-post-Raspbian-1deb10u1, mixed mode)
```

* Download the project from GitHub and build it:

```
$ git clone https://github.com/Pi4J/pi4j-example-minimal.git
$ cd pi4j-example-minimal/
$ mvn clean package
```

* Change to the distribution directory where you can find the generated package and required Java-modules. Start it with the provided run.sh script:

```
$ cd target/distribution
$ ls -l
total 644
-rw-r--r-- 1 pi pi 364456 Jun 19 10:04 pi4j-core-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi   7243 Jun 19 10:04 pi4j-example-minimal-0.0.1.jar
-rw-r--r-- 1 pi pi 142461 Jun 19 10:04 pi4j-library-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  37302 Jun 19 10:04 pi4j-plugin-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  26917 Jun 19 10:04 pi4j-plugin-raspberrypi-2.0-SNAPSHOT.jar
-rwxr-xr-x 1 pi pi    101 Jun 19 10:04 run.sh
-rw-r--r-- 1 pi pi  52173 Jun 19 10:04 slf4j-api-2.0.0-alpha0.jar
-rw-r--r-- 1 pi pi  15372 Jun 19 10:04 slf4j-simple-2.0.0-alpha0.jar
$ sudo ./run.sh
```

* The output will first show you some info about the platforms and providers. Then the LED starts blinking and shows how much times you pushed the button:

``` 
LED high
LED low
LED high
Button was pressed for the 1th time
LED low
LED high
Button was pressed for the 2th time
LED low
LED high
LED low
LED high
Button was pressed for the 3th time
LED low
LED high
LED low
LED high
Button was pressed for the 4th time
LED low
LED high
LED low
LED high
Button was pressed for the 5th time
```
