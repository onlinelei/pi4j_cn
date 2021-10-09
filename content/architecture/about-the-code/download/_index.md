---
title: 下载/安装
weight: 20
---



在 2020 年 6 月 3 日开始使用 V.2。

## Pi4J V.2

* 检出项目 [pi4j-v2](https://github.com/Pi4J/pi4j-v2)
* 选择使用 JDK11 例如：``sdk use java 11.0.7.fx-librca``
* 在 pi4j-v2 根目录，运行`m̀vn clean install``

```
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for Pi4J :: Parent POM 2.0-SNAPSHOT:
[INFO] 
[INFO] Pi4J :: Parent POM ................................. SUCCESS [  0.972 s]
[INFO] Pi4J :: DOCKER   :: Docker Parent POM .............. SUCCESS [  0.290 s]
[INFO] Pi4J :: TESTING  :: Arduino Test Harness ........... SUCCESS [  1.832 s]
[INFO] Pi4J :: LIBRARY  :: Libraries Parent POM ........... SUCCESS [  0.064 s]
[INFO] Pi4J :: LIBRARY  :: JNI Wrapper for PIGPIO Library . SUCCESS [  6.615 s]
[INFO] Pi4J :: LIBRARY  :: Java Library (CORE) ............ SUCCESS [  6.260 s]
[INFO] Pi4J :: PLUGIN   :: Plugins Parent POM ............. SUCCESS [  0.061 s]
[INFO] Pi4J :: PLUGIN   :: Mock Platform & Providers ...... SUCCESS [  0.683 s]
[INFO] Pi4J :: PLUGIN   :: PIGPIO I/O Providers ........... SUCCESS [  2.084 s]
[INFO] Pi4J :: PLUGIN   :: RaspberryPi Platform & Providers SUCCESS [  0.447 s]
[INFO] Pi4J :: TESTING  :: Unit/Integration Tests ......... SUCCESS [  2.350 s]
[INFO] Pi4J :: EXAMPLE  :: Sample Code .................... SUCCESS [  0.632 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

## 示例程序

### 构建示例应用程序

* 检出项目 [Pi4J V.2 - Telegraph Demo Project](https://github.com/Pi4J/pi4j-demo-telegraph)
* 选择使用 JDK11 例如：``sdk use java 11.0.7.fx-librca``
* 在 pi4j-demo-telegraph 根目录运行 `m̀vn clean install``
* 检查目录：target\distribution --> 这包含了要复制到 Raspberry Pi 的所有文件

```
/target/distribution/pi4j-core-2.0-SNAPSHOT.jar
/target/distribution/pi4j-demo-telegraph-1.0-SNAPSHOT.jar
/target/distribution/pi4j-library-pigpio-2.0-SNAPSHOT.jar
/target/distribution/pi4j-plugin-pigpio-2.0-SNAPSHOT.jar
/target/distribution/pi4j-plugin-raspberrypi-2.0-SNAPSHOT.jar
/target/distribution/run.sh
/target/distribution/slf4j-api-2.0.0-alpha0.jar
/target/distribution/slf4j-simple-2.0.0-alpha0.jar
```

### 在 Raspberry Pi 上运行
* 将 target/distribution 目录下的文件都拷贝到 Raspberry Pi 以后，运行 `./run.sh` 