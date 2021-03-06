# 数字控制器设计_R1

## 1.离散（数字）控制系统

关键参数：$T_s$ 采样周期

拉斯算子：${s = e^{j\omega + \delta}}$



连续系统离散方式

<http://www.cse.zju.edu.cn/eclass/attachments/2019-03/01-1553089879-388764.pdf>

## 2.两种PID控制器模式(位置式)${^{[1]}}$

### 2.1 Text Book Form

$$
\begin{align}
&Continuous:\\
&u(t) = K(e(t) + \frac{1}{T_i}\int_0^te(\tau)d\tau + T_d\frac{de(t)}{dt})&...(Ⅰ)\\
& Discrete^{[2][4]}:\\


\end{align}
$$



### 2.2 Parallel Form

$$
\begin{align}
&Continuous:\\
&u(t) = K_p*e(t) + K_i\int_0^te(\tau)d\tau + K_d*\frac{de(t)}{dt} ...(Ⅱ)\\
& Discrete^{[2][4]}:\\
\end{align}
$$

### 2.3 About

2.3.1 从系数量纲的角度看？

  （Ⅰ）式中，K单位$（HZ）(\frac{1}{s})$ ,  $T_i$积分时间常数，$T_d$微分时间常数；

  （Ⅱ）式中，${K_p}$单位${（HZ）(\frac{1}{s})}$ , ${K_i}$ 单位（${\frac{1}{s^2}}$），${K_d}$无量纲；

2.3.2 从整定方式看。

Ziegler Nichols 整定方式是基于（Ⅰ）；



2.3.2 转换关系${^{[1]}}$
$$
\begin{align}
K,\frac{1}{T_i},T_d |
K_P,K_i,K_d可以进行相互转换\\
\end{align}
$$





## 3.设计流程

### 3.1 连续系统被控对象&控制器

#### 3.1.1 被控对象（Continuous System Transform Function）

以$Gs = \frac{1}{s^3+1}$被控对象为例，

```matlab
s = tf('s');
Gs = 1/(s^3+1);
ts = 1e-3; % 采样周期
Dgs = c2d(Gs,'zoh'); %以零阶保持器的方式进行离散化（Z变换）；
[num,den] = tfdata(Dgs,'v');% 'v'强制返回Vector而非Cell类型数据；
```



#### 3.1.2 连续系统离散方式${^{[8][9]}}$

  获取被控对象的传递（S域）传递函数之后，进行计算机仿真（MATLAB | Visual Studio ）需要对被控对象进行离散化，实现模拟控制器的数字形式${^{[5]}}$，将S域函数转换为Z域传递函数，并进一步转换为差分方程形式；S域到Z域变换方式比较多，主要包括以下方法，‘zoh’:零阶保持器方法${^{[10]}}$、三角近似法、脉冲冲击响应不变、双线性变换、零极点匹配、最小二乘法。

- `'zoh'` — Zero-order hold (default). Assumes the control inputs are piecewise constant over the sample time `Ts`.
- `'foh'` — Triangle approximation (modified first-order hold). Assumes the control inputs are piecewise linear over the sample time `Ts`.
- `'impulse'` — Impulse invariant discretization
- `'tustin'` — Bilinear (Tustin) method. To specify this method with frequency prewarping (formerly known as the `'prewarp'` method), use the `PrewarpFrequency` option of `c2dOptions`.
- `'matched'` — Zero-pole matching method
- `'least-squares'` — Least-squares method



#### 3.1.3 PID控制器离散方式

  PID控制器的设计方式之一，先进行模拟控制器设计，设计完成之后，对控制器进行离散化，对PID进行离散化的方式${^{[2]}}$主要有前向欧拉（Forward Euler），后向欧拉（Backward Euler）， 梯形变换（Trapezoidal）${^{[4]}}$。不同的控制器结构，会有不同的控制效果，以及对应参数调整方式；上述三种控制器离散算法都需要设计到数字控制器控制周期${T_s}$ ，并且控制器参数的设计中，将控制器周期进行显式使用；区别于另外一种常用的控制器设计方式（差分设计），此种控制器设计方式以差分近似微分，偏差累计近似微分，两者最显著的区别在于是否将系统采样周期代入控制器参数设计中，因为PID控制器的参数一般都是进行经验调整，因此这两种不同的设计方式模糊了是否在控制器设计代入采样周期这个参数的意义；
$$
\begin{align}
&e.g^{^{[2]}}:\\
&采样周期（Sample Period）:T_s\\
&\frac{1}{s}离散方式:\\
&Forward Euler: \frac{T_s}{z-1}\\
&Backward Euler:\frac{T_sz}{z-1}\\
&Trapezoidal:\frac{T_s(z+1)}{z-1}\\
\end{align}
$$

差分逼近微分：
$$
\begin{align}
&\Delta y = y(t+\Delta t) - y(t)\\
&\frac{dy}{dt} = f'(t) = \frac{y(t) - y(t-T)}{T}\\
&y(t) - y(t-T) = \Delta y 理解为增量\\
\end{align}
$$


### 3.2 不同采样周期对于局部系统的影响分析

#### 3.2.1 滑动滤波器

  滑动平均滤波的点数与截止频率之间的关系可以表达为${^{[11][12]}}$：


$$
N = 0.443*fs/fco,
式中，N为平均的点数，fs为采样频率，fco为截止频率。
$$


#### 3.2.2 一阶RC低通滤波器

截止频率同滤波系数、采样周期关系：
$$
fl:截止频率\\
a：滤波系数\\
T:采样周期\\
fl = \frac{a}{2*pi*T}\\
$$

#### 3.2.3 逆控制系统参数分析

问题提出：

  已经设计调试好的控制器，修改整个控制系统采样周期，分析不同采样周期条件下，受采样周期影响控制器系数问题；

分析方式：

  数字控制系统，逆转换为模拟控制系统，以模拟控制系统控制器作为参考标准，进行对比分析；





## 4. Vibration Depress（振动抑制）

### 4.1 问题背景

  薄板边缘进行随动，由于跟踪对象的不稳定性、边缘效应、系统内部相互作用；导致浮动头出现较高频率的抖动，并且由于系统内部的相互作用，加剧了浮动头抖动效果；如果将跟踪对象看作是控制系统的一部分，也应该将其视作控制系统一部分，则上述振动属于自激振动（ self-excited vibration ）。

It's a confusing mater.but it deserves.

---

### 4.2 解决方案（1）

  非线性偏差；
$$
\begin{align}
& Cof(error,boundary,k) = 
\begin{cases}
boundary / boundary ,abs(error) >= boundary; \\
1 + k*(boundary - abs(error))/boundary;\\
\end{cases}...(1)\\
\\
& ErrorDepress(t) = Error(t)*Cof(t)...(2)；
\end{align}
$$

---

### 4.3 解决方案（2）

Ⅰ.ADRC(active disturbances rejection controller)${^{[13] [14]}}$;

Ⅱ.扰动观测-补偿算法;

Ⅲ.LQR控制器;



## 5.System Identification

### 5.1.matlab 系统辨识工具箱使用

#### 1.1 Nonlinear ARX Model${^{[15]}}$



#### 1.2 Hammerstein-Wiener Model





## 6.一阶、二阶滤波器原理及其对比

### 6.1 基本原理

一阶数字滤波器${^{[17]}}$,双二阶滤波器${^{[16]}}$,数字滤波器原理${^{[18]}}$;

（1）传递函数与IIR实现方式存在统一性，nums/dens
（2）零极点配置简单滤波器设计方法原则：
		极点靠近单位圆，频率响应的峰值越高；极点放在需加强的频率
		点附近;
		零点靠近单位圆，频率响应的谷值越小；零点放在需减弱的频率
		点附近;
		约束条件
		 极点在单位圆内，保证滤波器的因果稳定；
		 零、极点须共轭成对，或者是实数，保证系统函数系数为实数。

（3）ω = 2*pi*f

（4）数字谐振器、最小相位滤波器、梳状滤波器、正弦波发生器${^{[18]}}$

---

### 6.2 IIR和FIR

1.单位脉冲响应长度：IIR(Infinite Impulse Response )  FIR (Finite Impulse Response)。单位脉冲冲击响应是否在有限时间内衰减为${^{[30]}}$.

2.滤波器设计思路：AF理论设计→H(s) → DF系统函数H(Z)；

3.设计方法：巴特沃斯(Butterworth)、切比雪夫(Chebyshev)、椭圆（Ellipse）;

4.AF转DF方法：

脉冲响应不变法：拉斯反变换

双线性变换

5.IIR & FIR

（1）线性相位；

（2）计算参数；

6.阻尼的理解

从频率响应角度看，阻尼大小可以理解为：过渡区衰减斜率(衰减到截至频率)大小，一阶低通滤波器衰减斜率仅为-20dB/十倍频。二阶低通滤波器相对于一阶低通滤波器，频率响应曲线形状上看是大致相同的，二阶低通滤器器可以调整衰减斜率，衰减斜率就是阻尼系数。

---

### 6.3 数字滤波器设计Matlab & C ${^{[20][21]}}$

---

### 6.4 功率谱${^{[19]}}$



## 7.ADRC

### 7.1 Discrete ADRC ESO

1.discrete implementation and generalization of the extended state observer .Gao

2.ADRC-ESO离散形式${^{[2][3][4]}}$
$$
\begin{align}
&\begin{cases}
e(k) = z_1(k) - y(k),fe = fal(e,alpha_1,\delta),fe_1 = fal(e,alpha_2,\delta)..\\
z_1(k+1) = z_1(k) + h(z_2(k) - \beta_{01}e(k))\\
z_2(k+1) = z_2(k) + h(z_2(k) - \beta_{02}f2 + b_0u(k))\\
z_3(k+1) = z_3(k) + h(-\beta_{03}fe_1)
&\end{cases}
\end{align}
$$
3.系统框图${^{[3]}}$

### 7.2 NLSEF${^{[22]}}$

非线性状态偏差反馈（sec-order）
$$
\begin{align}
&U_0 = b_1fal(\epsilon_1,\alpha_1,\delta) + b_2fal(\epsilon_2,\alpha_2,\delta)\\
&\epsilon_1 = e_1 - z_1\\
&\epsilon_2 = e_2 - z_2\\

\end{align}
$$

```matlab
%% NLSEF.m
%{
 	Parameter:
    alpha:非线性度
    delta:非线性区间
    bt:状态系数
  	
  	Reference:
  	《非线性状态误差反馈控制律—NLSEF》
  	
%}
function [sys,X0,str,ts] = NLSEF(t,x,u,flag,alpha_1,delta_1,bt1,alpha_2,delta_2,bt2)
switch flag
	case 0
		[sys,x0,str,ts] = mdlInitializeSizes;
	case 2
		sys = ~name()(t,x,u,flag,alpha_1,delta_1,bt1,alpha_2,delta_2,bt2);
	case 3
		sys = ~name(t,x,u);
	case {1,4}
		
	case 9
		sys = ~(~)
		
	otherwise
		%---
function [sys,X0,sr,ts] = mdInitialize..
	sizes = simsizes;
	
	*.DiscStates = 2;
	*.input = 2;
	*.output = 1;
	*.sampletimes = 1;
	
	x0 = [0 0 ];
	str = [];
	ts = [1E-3 0];

function sys = update(~...~)
	uz = zeros(1,2);
	se = zeros(1,2);
	se(1) = u(1);
	se(2) = u(2);
	
	uz(1) = bt1*Fal_Func(se(1),alpha_1,delta_1);
	uz(2) = bt2*Fal_Func(se(2),alpha_2,delta_2);
	
	x = uz;
	sys = x;
	
function sys = mdlOutPuts(~,~,~)
	sys = sum(x);
	
	
	
```



Linear ADRC-ESO离散形式

[2].自抗扰控制技术-估计补偿不确定 page188-213

[3] Comparative sutdu of linear and nonlinear Adrc for an inverted pendulum

[4] Control and simulation of the ABS based on ADRC

3.ADRC-TD跟踪器参数整定

  α，δ需要根据跟踪信号进行实时调整，跟踪信号频率越高，δ值越大；

## 7.3 DT(Differential Tracker) 

#### 7.3.1 DT



#### 7.3.2 离散DT ${^{[24][25]}}$

  微分跟踪器作用：（1）低通滤波器（2）从带有噪声信号中提取微分信号；微分跟踪器核心是“快速最优控制”；微分跟踪器包含连个参数，${\delta：速度因子,h：积分步长}$；

微分跟踪器形式一${^{[29]}}$
$$
\begin{align}
& X_1(k+1) = X_1(k) + h*X_2(k)...(1)\\
& X_2(k+1) = X_2(k) + h*fst(X_1(k)- v(k),X_2(k),r,h_0)...(2)\\
& fst(x_1-v,x_2,r,h_0) = \begin{cases}
-ra,|a| <= d;\\
-r*sign(a),|a|>d.\\
\end{cases}...(3)\\
& a = \begin{cases}
x_2 + \frac{c}{h_0},|c| < d_0;\\
x_2 + \frac{sign(c)(a_0-d)}{2},|c| >d_0.\\
\end{cases}...(4)\\
&\begin{cases}
d = rh_0,\\
d_0 = dh_0,\\
c = v1 - v + h_0v_2,\\
a = \sqrt(d^2 + 8r|c|)\\
\end{cases}...(5)\\
\end{align}
$$


### 7.4 安排过渡过程（Arrange Transient Process）

#### 7.4.1 原理

  安排过渡过程，是一种对参考信号进行缓变处理的方法，${U(t) = U_0(t)*Cof(t)}$ ，









#### 7.3.n Problems

1.步长（h）和采样周期（Ts）使用？

计算过程中，使用h = 1还是使用Ts；差分和微分区别；





## 8.现代控制理论

### 8.1 状态空间表达式同古典控制理论之间的关系



### 8.2 离散时间系统状态空间描述特点${^{[23]}}$

（1）状态方程形式上的差分型属性；

（2）线性属性；

（3）变量取值时间离散；

### 8.3 物理变量和相变量

  系统的状态变量选择不唯一，当状态变量为输出变量及其各阶导数时，相应的状态变量为相变量；系统中状态选取的是实际的物理量，则称为物理变量；





##### 1.《故障诊断5——状态观测器和输出观测器》

https://blog.csdn.net/jinpeng_cumt/article/details/87692579

2.《故障诊断4—龙伯格状态观测器设计》

https://blog.csdn.net/jinpeng_cumt/article/details/86377433





## 9.系统边界条件(System Boundary Conditions)



## 10.Bode图

**Keys:**

1.who ,what,how,why



nyquist bode 图 https://www.cnblogs.com/regenwald/articles/7784806.html

开闭环bode图https://www.zhihu.com/question/28157191

### 10.1 定义

  Bode图是，频域分析中使用，对数频率特性曲线，由对数幅频曲线，对数相频曲线构成，横坐标按照${lg(\omega)，\omega单位rad / s}$,对数幅频曲线${L(\omega) = 20lg|G(j\omega)|}$,单位${dB}$。对数频域特性采用${\omega}$的对数分度实现横坐标的分线性压缩，对数幅频特性采用20*lgA(w)可以将乘除改变为加减运算。${^{[28]}}$



### 10.2 闭环系统稳定频域性能指标

**1.控制系统频带带宽**

  闭环系统频率特性：${\phi(j w)}$，当闭环幅频特性下降到频域为0时的分贝值以下3分贝，及${0.707 |\phi (j 0)|}$(dB)时，对应的频率称为带宽频率；频率范围（0,${\omega }$）称为系统带宽。${^{[28]}} $

 

**2.稳定性分析**

  频域的相对稳定性—稳定裕度常用相角裕度${\gamma}$和幅值裕度${h}$ 来度量。



## 11.状态观测器

1.系统状态

  对于一个动态系统的数学描述，分为“内部描述”和”外部描述“，系统状态用于对系统的进行内部描述。系统状态指的是用来刻画系统在时刻t态势的变量，表示为${x(t)}$。[1]



[1]线性系统理论 P16



---

## 12.采样

1.采样原理

2.采样方式：冲激串采样、零阶保持器采样

3.欠采样-混叠

## n. Problems

1.s（s域）不能进行Z变换的原因;

2.增量式PID控制器如何进行积分饱和设计;

**Apended**

1.《autopilot》

2.状态偏差反馈与系统偏差反馈

<https://zhuanlan.zhihu.com/p/58422485>

3.系统边界条件

4.Simulink white noise

 https://onlinelibrary.wiley.com/doi/pdf/10.1002/9780471679370.app2 

 https://blog.csdn.net/szlcw1/article/details/41758711 

5.安排过渡过程和微分跟踪器的差别

6.最速综合函数原理${^{[27]}}$

7.李雅普诺夫稳定

<https://blog.csdn.net/xuehuafeiwu123/article/details/53119419>

##### 8.系统二阶状态和微分区别？




## Reference:

[1]  《PID Anti-Windup Schemes》<https://www.scilab.org/pid-anti-windup-schemes>

[2] 《Discrete time pid controller implementation》<https://www.scilab.org/discrete-time-pid-controller-implementation>

[3] 《Advanced PID Controller Implementation》<https://www.scilab.org/advanced-pid-controller-implementation>

[4] 《Disrete Pid Controller》<http://portal.ku.edu.tr/~cbasdogan/Courses/Robotics/projects/Discrete_PID.pdf>

[5] 《Digital PID》<https://web.calpoly.edu/~fowen/me422/Chapter10.pdf>

[6] 《Modern PID - Digital PID》 <https://msc.berkeley.edu/assets/files/PID/modernPID4-digitalPID.pdf>

[7] 《Digital Control Systems》<https://ethz.ch/content/dam/ethz/special-interest/mavt/dynamic-systems-n-control/idsc-dam/Lectures/Digital-Control-Systems/Slides_DigReg_2013.pdf>

[8] 《Convert model from continuous to discrete time》<https://ww2.mathworks.cn/help/control/ref/c2d.html#mw_de45fa0b-4dd8-4040-be9c-4fd55b8b9567>

[9] 赵霞, 王祝萍, 贾海航. 连续系统离散化方法的比较与解析初探[J]. 工业和信息化教育, 2015(10):71-76.

[10] Landua I , GianlucaZito. 数字控制系统：设计、辨识和实现：design, identification and implementation[M]. 科学出版社, 2014.

[11] 《 滑动平均滤波的截止频率与平均点数计算》(https://www.cnblogs.com/pingwen/p/6670675.html)

[12]《Which is the cut -off frequency of Moving Average LP Filter?》 

<https://www.dsprelated.com/showthread/comp.dsp/155807-1.php>

[12-1]<https://www.gaussianwaves.com/2010/11/moving-average-filter-ma-filter-2/>

[13] 《ADRC-状态观测器》https://blog.csdn.net/song430/article/details/88635542

[14] 《sign符号函数-matlab》 https://ww2.mathworks.cn/help/matlab/ref/sign.html 

[15] 《matlab 万能实用的非线性曲线拟合方法》https://blog.csdn.net/ljyljyok/article/details/81624496

[16] 《双二阶滤波器》

<https://zh.wikipedia.org/wiki/%E5%8F%8C%E4%BA%8C%E9%98%B6%E6%BB%A4%E6%B3%A2%E5%99%A8>

[17]《一阶RC低通滤波器》<https://blog.csdn.net/qq_27334499/article/details/52186336>

[18] 《数字滤波器原理》<http://web.xidian.edu.cn/kywang/files/20121022_120735.pdf>

[19]《功率谱和频率谱分析》<https://blog.csdn.net/godloveyuxu/article/details/77030793>

<https://blog.csdn.net/u013241951/article/details/71907051>

<https://www.cnblogs.com/zhongguo135/p/4044095.html>

<http://blog.sina.com.cn/s/blog_79ecf6980100vcqn.html>

https://www.dsprelated.com/showthread/comp.dsp/155807-1.php)

[20]《Matlab-FilterDesigner & C语言滤波器设计》

<https://www.cnblogs.com/21207-iHome/p/7059144.html>

<https://www.cnblogs.com/sunev/archive/2011/11/22/2258426.html>

https://blog.csdn.net/syrchina/article/details/11731325

[21]《参考文献》

[《基于MATLAB的FIR数字滤波器设计与仿真》](http://d.wanfangdata.com.cn/Periodical/dzcljs201011017)

[《MATLAB环境下的数字滤波器设计及其应用》](http://cdmd.cnki.com.cn/Article/CDMD-10285-2002120612.htm)

[《用DSP实现FIR数字滤波器》](<http://www.cnki.com.cn/Article/CJFD2000-WYWT200002012.htm>)

[《基于DSP Builder 的14 阶FIR 滤波器的设计》](http://www.cnki.com.cn/Article/CJFDTEMP-XDDJ200721062.htm)

[《基于MATLAB 的IIR 数字滤波器设计》](http://www.cnki.com.cn/Article/CJFDTotal-YYSF200703011.htm)

[22] 《非线性状态误差反馈率—NLSEF》

[23] 《线性系统理论》page.27

[24] 武利强, 韩京清. TD滤波器及其应用[J]. 计算技术与自动化, 2004, 22(z1):61-63.

[25] 张海丽, 张宏立. 微分跟踪器的研究与应用[J]. 化工自动化及仪表, 2013, 40(4):474-477.

[26] 黄焕袍, 万晖, 韩京清. 安排过渡过程是提高闭环系统“鲁棒性、适应性和稳定性”的一种有效方法[J]. 控制理论与应用, 2001, 18(s1):89-94.

[27] 《高精度快速离散微分跟踪器》

[28] 《自动控制原理》p183

[29] 《改进的非线性跟踪微分器设计》

[30] [《Digital Filter Design: FIR vs IIR Filters》](<https://theaudioprogrammer.com/digital-filter-design-fir-vs-iir-filters/>)

[31] Moving Average Filter <https://www.gaussianwaves.com/2010/11/moving-average-filter-ma-filter-2/>

## Control Methods

PID控制、自适应控制、最优控制、鲁棒控制



1.能观、能控判断方法；

如果一个系统在有限的时间内，在某种控制向量u(t)的作用下，系统状态向量x(t)可由一种初始状态达到任意一种目标状态时，则称此系统是可控的。

2.Lqr & StateObserver；

3.Lyapunov 稳定判据；

4.模型建立

```mermaid
graph LR
D[物理模型]-->A
A[微分方程]-->B(状态变量)
B-->C[状态空间表达式]
```

5.状态空间特征值；

6.Q、R矩阵设计思路；

7.discrete LQR or continuous LQR

8.一阶惯性环节

9.全状态反馈控制

10.状态空间转离散控制

11.状态转移方程 & 输入输出方程 实现方式

12.微分方程转换为状态空间表达式

