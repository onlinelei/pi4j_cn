---
title: 了解 GPIO 引脚
weight: 35
---

将电子元件连接到 Pi 是通过连接接头中的一个或多个引脚完成的。引脚的数量随着 Raspberry Pi 板版本增长而“增长”，现在最新版本固定在 40 个引脚。需要注意的是引脚的编号，以免以错误的方式连接到组件。

![Numbering of the pins](/assets/getting-started/pins/headernumber-on-board.jpg)

## 引脚类型

引脚有不同的用途

### 电源和地

5V 和 3.3V 均可用作电源引脚，接地引脚也是电源引脚。每当电路板通电时，您的组件都可以使用固定电源。您必须考虑不要连接需要大量电流的设备，否则 Raspberry Pi 本身将无法按预期运行并重启。

Both 5V and 3.3V are available as power pins and, of course, also ground pins. Anytime the board is powered you have a fixed power supply available for your components. You have to take into account not to connect devices that need a lot of current, otherwise the Raspberry Pi itself will not behave as expected and reboot for instance.

### Digital GPIO

The other ones are "General-Purpose Input/Output" (GPIO) pins. These pins can be addressed with software to act as input 
or output for an application. They use 3.3V, meaning an output pin will be set to 0V (low) or 3.3V (high) and an input 
pin will read 0V as low and 3.3V as high.

Most of the GPIOs have an internal pull-up or pull-down resistor which can be enabled in software.

## Overview 

The following image gives you an overview of the pins and types of a typical 40-pin header. Note the different numbers
being used:

1. **PIN**: 1 to 40 logical order of the pin
2. **BCM**: the number to be used in your Java code to specify the GPIO to be used. BCM refers to the "Broadcom SOC channel" number, 
   which is the numbering inside the chip which is used on the Raspberry Pi. These numbers changed between board versions 
   as you can see in the previous tables for the 26-pin header type 1 versus 2, and or not sequential.
3. **WPI**: WiringPi number which was used by V.1 of Pi4J. The WiringPi numbering has a "historical reason". When development 
   for the very first Raspberry Pi's was ongoing, only 8 pin-numbers were foreseen. But, when the designs further evolved 
   and more pins were added, the numbering in WiringPi was extended to be able to address the extra pins.

![Pin header overview](/assets/getting-started/pins/headerpins_in_header.png)