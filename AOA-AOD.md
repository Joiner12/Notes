# AOA/AOD介绍

​	2019 年初，蓝牙 5.1 标准增加了寻向功能，可以使用低功耗蓝牙设备用来检测蓝牙信号的方向。根据被定位设备的上下行模式的不同，可以将寻向功能分成 AoA 到达角度法（Angle of Arrival）和 AoD 出发角度法（Angle of Departure）。

**RF开关切换**、**多天线**、**天线切换**、**I/Q采样**

| 方向定位方法 |                    发射端                     |                           接收端                            |
| :----------: | :-------------------------------------------: | :---------------------------------------------------------: |
|     AOA      | 单天线、<br/>发送CTE(Constant Tone Extension) | 多天线<br />RF开关切换<br />接收到CTE的 I/Q数据需要切换开关 |
|     AOD      | 多天线<br />RF开关切换<br />切换开关时发送CTE |                单天线<br />记录CTE的I/Q采样                 |

蓝牙5.1标准下，以下状态支持发送寻向数据包：

1. 周期性广播：Connectionless CTE(无连接固定频率扩展信号)—广播模式
2. 链接状态：Connection CTE(连接固定频率扩展信号)—连接模式

AoA/AoD应用中，无连接/连接状态下的CTE是相同的。



## 1.AOA定位

​	在 AOA 定位场景中，被定位设备，比如贴在被定为物上的便携蓝牙 tag，用单根天线广播定位用数据包。接收端则拥有一组天线阵列，一起接收这一个数据包。由于天线阵列中不同天线到发送端的距离不同，这一距离差就会带来相位差，即不同天线在同一时间接收到的信号的相位有一定差异。接收端会快速轮询各个天线，每根天线都会记录若干个采样点的 I/Q 值，这些 I/Q 值可以算出当前采样时刻的信号相位，从而根据天线间的相位差即可算出入射角 AOA。

### 1.1 AOA定位方法

AOA测量通常由以下三步：

1. 通过I/Q采样获取相位信息；
2. 计算不同天线之间的相位差；
3. 相位差转换为到达角；

**通过I/Q采样获取相位信息**

​    AOA 定位中，发射端用单根天线发送一段正弦波，接收端用天线阵列接收这一信号，计算信号的入射角。两个（或更多）天线彼此分开的一定距离时，接收信号的相位差与距发射器之间的距离之间成正相关。同一时间，由于不同天线的发射器的距离差异，导致接收到的信号存在相位差。当两个天线足够近（小于半波长），可以消除相位差的**整周期模糊**，能够唯一地确定来波的方向。

​	例如，当定频信号从发射端出发时，电池波会到达天线1和天线2，由于天线1和天线2的位置不同，信号从发射端到接收端的波程不一样，从接收端看，不同天线接收到的波相位存在差异。不同的来波方向产生不同的相位差。射频芯片可以通过对每个天线的信号进行I/Q采样获取相位信息。

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/AoA_conversion_to_phase_shift.png">
</div>
**计算天线之间的相位差**

通过将至少两个天线连接到相同的接收器（可以添加更多天线）来测量相位差（$\phi$）。

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/AoA_measure_phase.png">
    <p>多天线示意图</p>
</div>

下图片所示，表示来自2个天线的信号矢量的星座图。如果所有天线都是线性排列且距离固定为d，则相邻天线之间的相位差$\phi$​将是恒定的。

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/20210728095634.png">
    <p>信号矢量星座图</p>
</div>

为了获得$\phi$（相位）的良好估计，必须排除掉其他的相位偏移。蓝牙信号是调制信号，其调制特性本身就会带来相位的变化。蓝牙5.1规范制定了CTE标准，通过在数据包末尾加入CTE来消除蓝牙信号相位偏移。

**将相位差转换为到达角度**

​	发射天线向接收端天线阵列中，相距为 d 的两根天线阵列接收来自被定位蓝牙设备发出的蓝牙信号，以图中蓝色箭头表示。由于这两根接收天线到发射天线的距离不同，这两根天线收到的信号会出现一个恒定的相位差。而因为发射端到天线的距离远大于 d，发射天线这两个接收天线的路径可以视为平行。

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/AoA_position%20(1).png" style="width:500px;height:300px;">
    <p>AOA图示</p>
</div>



在这一假设下，从一根天线向另一根作垂线，截取出的rr直角边就是路程差。

显然，在这个直角三角形中，有：
$$
\begin{align}
r=d sin \theta
\end{align}
$$
$\theta$表示AoA。另一方面，相位差与路程差的关系为：
$$
\begin{align}
\Delta\phi=\frac{2\pi}{\lambda}r
\end{align}
$$

其中${\Delta\phi}$代表相位差，${\lambda}$表示蓝牙波长。根据上述公式，可以推导出AoA：
$$
\begin{align}
\theta=arcsin\frac{\lambda\Delta\phi}{2\pi d}
\end{align}
$$

在算出方向角后，就可以根据被定位设备到不同定位点的方向角算出其具体位置。



### 1.2 CTE(Const Tone Extension)

`CTE`是定频(250kHz)无调制的信号，可非常方便地用于相位差检测。它的`时长16us到160us`，无CRC校验，支持广播模式和连接模式两种类型。CTE信号是附加在CRC校验之后的信号，不影响原来的数据内容。是否具有CTE，在`PDU(package data unity)`的header中可以指定，包含对CTE类型的设定（AOA，AOD 1us，AOD 2us)以及CTE的时长设定。

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/20210728101657.png">
    <p>cte数据格式</p>
</div>


​	上面显示的包的灰色部分意味着它是可选的。仅当设置数据物理PDU报头中的CP位时，才会启用CTE。 然后由数据物理PDU中的CTEInfo指定具体的CTE。蓝牙5.1协议规定了CTE的切换/采样时隙。CTE的处理过程可以分为初始的4us守卫时间（用于和前面的信号分开，保证不干扰），8us的参考时间（对第一个天线进行8个I/Q采样）以及后续一系列的采样和切换时间片。天线切换仅在switch slot完成，采样仅在sample slot完成。天线的切换模式可以通过HCI命令设置。

​	首先接收端同步解调器时间，然后将I/Q采样存储在CTE中到射频RAM中。 最后由应用层提取I/Q采样数据。I/Q采样用于估计天线之间的相位差，当接收器接收到AOA数据包时，RF核触发天线切换事件。

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/20210728110508.png">
    <p>蓝牙 5.1 规定的 AOA/AOD 时间表</p>
</div>

### 1.3 天线阵列

​	天线阵列的布置方式多种多样，一般常用`线阵(ULA-Linear Array)`、`矩形阵(ULA-Rectangular Array)`、`圆阵(ULA-Circular Array)`等不同的天线阵列进行信号检测。一为定位，二为最大化减少接收机部署的个数。实际应用中，线阵是一维的，所有天线位于一条直线上，可以获取方位角。矩形阵和圆阵可以获取二维角度（方位角和俯仰角）。天线阵列不同，信号处理算法也不相同。天线阵列波达方向处理方法已有大量的研究，常用的有多重信号分类（MUSIC）算法、最大似然算法、ESPRIT算法、压缩感知算法等。

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/20210728170705.png">
    <p>常见天线阵列</p>
</div>

### 1.4 AOA定位

​	AOA 场景下，只要知道接收天线阵列的位置和朝向，只需要两个点即可完成定位。每个定位点感知到的方向角都会将被定位设备约束在一条直线上，而两条直线的交点即为其确切位置，如下图：

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/AoA_2.png">
    <p>二维AOA定位过程示意图</p>
</div>
## 2.定位方法${^{[9]}}$

### 2.1 角度+距离(Angle plus Estimated Distance)

RSSI+ Angle

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/rssi%20angle.png">
    <p>角度+距离</p>
</div>




### 2.2 (Intersection of Multiple Angles)

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/Angle%20Angle.png">
    <p>二维AOA定位过程示意图</p>
</div>


## 3. AoA/AoD定位系统$^{[10]}$

### 3.1 AoA设计方案

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/angle-of-arrival-design-considerations.jpg">
    <p>AoA设计方案</p>
</div>

### 3.2 AoD设计方案

<div style="background-color:white;text-align:center;">
    <br/>
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/angle-of-departure-design-considerations.jpg">
    <p>AoD设计方案</p>
</div>



# Reference

1. [一文看懂Bluetooth 5.1 AoA到达角度位置服务实现原理_BLECODER的博客-CSDN博客_蓝牙aoa定位原理](https://blog.csdn.net/weixin_42583147/article/details/100574253?utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-4.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-4.control)
2. [14.6 蓝牙AoA测量角度的方法 - IoT Book - 清华大学 - 王继良 (iot-book.github.io)](https://iot-book.github.io/CH11_Sensing/S5_蓝牙感知/)
3. [Bluetooth Low Energy Angle of Arrival (AoA) (ti.com)](https://dev.ti.com/tirex/content/simplelink_academy_cc2640r2sdk_2_40_03_00/modules/blestack/ble_aoa/ble_aoa.html#2-calculate-the-phase-difference-among-the-antennas)
4. [数字调制系列：IQ基本理论 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/58119209)
5. https://silabs-prod.adobecqms.net/content/usergenerated/asi/cloud/content/siliconlabs/en/community/chinese-blog/jcr:content/content/primary/blog/_-7jYr.social.0.10.html
6. [Comparison of Direction of Arrival (DOA) Estimation Techniques for Closely Spaced Targets | Connected Papers](https://www.connectedpapers.com/main/a63018b4bd1cb5f082e1a381e7a2c7bb2903deea/Comparison-of-Direction-of-Arrival-DOA-Estimation-Techniques-for-Closely-Spaced-Targets/graph)
7. [超分辨DOA估计——MUSIC算法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/362008506)
8. [DOA——MUSIC算法 - 桂。 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xingshansi/p/7163605.html)
9. [Quuppa’s Role Regarding the New Bluetooth SIG Direction Finding Feature – Quuppa](https://www.quuppa.com/quuppas-role-regarding-the-new-bluetooth-sig-direction-finding-feature/)
10. [Bluetooth 5.1 Angle of Arrival and Angle of Departure - Silicon Labs (silabs.com)](https://www.silabs.com/wireless/bluetooth/bluetooth-5-1)
11. [(1条消息) 无线定位原理：TOA & AOA_本帅哥屏蔽了凡人呢-CSDN博客_aoa定位](https://blog.csdn.net/qq_23947237/article/details/82738191?utm_term=aoa定位算法&utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduweb~default-1-82738191&spm=3001.4430)
12. [AOA(Angle of Arrival，到达角)定位算法及其误差分析的原理和MATLAB仿真_ICTBeginner 的博客-CSDN博客](https://blog.csdn.net/qq_37930244/article/details/104933168)
13. [蓝牙5.1到达角和离开角定位技术(aoa/aod)_工农村贴膜小哥的博客-CSDN博客_aoa aod定位](https://blog.csdn.net/qq_35651984/article/details/107577617?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-4.control&spm=1001.2101.3001.4242)
14. https://www.sekorm.com/news/66727045.html

