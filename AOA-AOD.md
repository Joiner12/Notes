# AOA/AOD介绍

​	2019 年初，蓝牙 5.1 标准增加了寻向功能，可以低功耗蓝牙设备用来检测蓝牙信号的方向。根据被定位设备的上下行模式的不同，可以将寻向功能分成 AoA 到达角度法（Angle of Arrival）和 AoD 出发角度法（Angle of Departure）。

**RF开关切换**、**多天线**、**天线切换**、**I/Q采样**

| 方向定位方法 |                    发射端                     |                           接收端                            |
| :----------: | :-------------------------------------------: | :---------------------------------------------------------: |
|     AOA      | 单天线、<br/>发送CTE(Constant Tone Extension) | 多天线<br />RF开关切换<br />接收到CTE的 I/Q数据需要切换开关 |
|     AOD      | 多天线<br />RF开关切换<br />切换开关时发送CTE |                单天线<br />记录CTE的I/Q采样                 |

蓝牙5.1标准下，以下状态支持发送寻向数据包：

1. 周期性广播：Connectionless CTE(无连接固定频率扩展信号)
2. 链接状态：Connection CTE(连接固定频率扩展信号)

AoA/AoD应用中，无连接/连接状态下的CTE是相同的。



## AOA定位理论

在 AOA 定位场景中，被定位设备，比如贴在被定为物上的便携蓝牙 tag，用单根天线广播定位用数据包。接收端则拥有一组天线阵列，一齐接收这一个数据包。由于天线阵列中不同天线到发送端的距离不同，这一距离差就会带来相位差，即不同天线在同一时间接收到的信号的相位有一定差异。接收端会快速轮询各个天线，每根天线都会记录若干个采样点的 I/Q 值，这些 I/Q 值可以算出当前采样时刻的信号相位，从而根据天线间的相位差即可算出入射角 AOA。

AOA测量通常由以下三步：

1. 通过I/Q采样获取相位信息；
2. 计算不同天线之间的相位差；
3. 相位差转换为到达角；

AOA 定位中，发射端用单根天线发送一段正弦波，接收端用天线阵列接收这一信号，计算信号的入射角。先假设定位时天线阵列能同时接收信号。下图绘制了接收端的情况。

# Reference

1. [一文看懂Bluetooth 5.1 AoA到达角度位置服务实现原理_BLECODER的博客-CSDN博客_蓝牙aoa定位原理](https://blog.csdn.net/weixin_42583147/article/details/100574253?utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-4.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-4.control)
2. [14.6 蓝牙AoA测量角度的方法 - IoT Book - 清华大学 - 王继良 (iot-book.github.io)](https://iot-book.github.io/CH11_Sensing/S5_蓝牙感知/)
3. [Bluetooth Low Energy Angle of Arrival (AoA) (ti.com)](https://dev.ti.com/tirex/content/simplelink_academy_cc2640r2sdk_2_40_03_00/modules/blestack/ble_aoa/ble_aoa.html#2-calculate-the-phase-difference-among-the-antennas)