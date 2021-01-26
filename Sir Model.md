# SIR模型

经典的SIR模型是一种发明于上个世纪早期的经典传染病模型，此模型能够较为粗略地展示出一种传染病的发病到结束的过程，其核心在于微分方程，本次我们利用matlab来对此方程进行

其中三个主要量
$$
\begin{align}
S是易感人群\\ \\
I是感染人群\\ \\
R是恢复人群\\ \\
\end{align}
$$


这三个量都是跟随时间变化的函数，即可以表示为，其中的t我们设定为一个单位时间，我们即有如下的公式：
$$
\left
\{\begin{array}{l} S(t)
\\ I(t)
\\ R(t)
\end{array}
\right.
$$


然而要列出此种类似的方程我们需要一部分的理想化条件，这些`理想化条件`是比较重要的，

1.首先即城市的总人数不变，即：

![img](https_noflag://pic2.zhimg.com/80/v2-a9f41d8feb1f4024aa6fce324fcb1b99_720w.jpg)

${S(t)+I(t)+R(t)=k}$

K为一个常数值，一个恒定量。

2.假设 t 时刻单位时间内，一个病人能传染的易感者数目与此环境内易感者总数s(t)成正比，设定比例系数为β，从而在t时刻单位时间内被所有病人传染的人数为βs(t)i(t)

\3. t 时刻，单位时间内从染病者中移出的人数与病人数量成正比，比例系数为γ，单位时间内移出者的数量为γi(t)



故我们可以得知其作用的机制为：`易感人数和系数以及感染人数同时作用于总的易感人数，同时恢复人数和恢复系数又对感染人数起到影响。但是同时这又是一个单向性的机制。`

基于以上三个条件的假设，我们可以获得其人数变化的机制，也即

1.易感个体的下降率为（注：此处为负数）：
$$
\begin{align}
-\beta S(t)I(t)\\
\end{align}
$$


![img](https_noimage://pic1.zhimg.com/80/v2-eda0b2bf713d614b64a539cf398a99e0_720w.png)

2.感染个体的增长率为：
$$
\begin{align}
-\beta S(t)I(t) - \gamma i(t)\\
\end{align}
$$
![img](https_noimage://pic2.zhimg.com/80/v2-4bed3d03496772c6d94bc41eaed58121_720w.png)

3.恢复个体的增长率为：
$$
\begin{align}
\gamma i(t)\\
\end{align}
$$


![img](https_noimage://pic3.zhimg.com/80/v2-a040b3e2a77d4d2267340c53c1957842_720w.png)

我们利用微分方程可以表示如下：
$$
\left
\{\begin{array}{l} \frac{dS(t)}{dt} = -\beta S(t)I(t)
\\ \frac{dI(t)}{dt} = \beta S(t)I(t) - \gamma i(t)
\\ \frac{dR(t)}{dt} = \gamma i(t)
\end{array}
\right.
$$




![img](https_noimage://pic2.zhimg.com/80/v2-1e68c019d3b3c8fcfbf9dab5a94b0da5_720w.jpg)SIR核心的微分方程



我们对此类方程利用matlab编写SIR函数

其代码为：

![img](https://pic1.zhimg.com/80/v2-8eacecc96f5e6a490bc8bec4caf2c4c0_720w.jpg)sir 函数的matlab code

其中a即为参数，b也为参数，这是可以调整设置的参数，故对于此微分方程的求解，我们利用matlab内建的函数ode45，来进行求解，我们可以参照ode45（）函数的使用范例

进行调用

即[t,x]=ode45(@sir,[0:1:400],[1 116000 0]);

此处的[0:1:400]的为时间的取值范围，这里我们以天为单位，取了0到40等41个点，也即41天。

此处的[1 740000 0]分别为S(t),I(t),R(t)的初始值。

我们利用如下代码：

[t,x]=ode45(@sir,[0:1:180],[1 116000 0]);

\>> hold on;

\>> plot(t,x(:,1),'o-');

\>> plot(t,x(:,2),'*-');

\>> plot(t,x(:,3),'d-');

legend('感染人数','易感人数','恢复人数');

title('SIR模型图');

xlabel('天数(days)');

ylabel('总人数');

获得图像如下：



![img](https://pic2.zhimg.com/80/v2-e86bffb1c3ad163a9da423e7e7af40bd_720w.jpg)SIR模型图

**模型总结**：此模型能够较好地模拟一个从传染病的过程，但是前提在于人能够恢复，并且获得终生免疫能力：

![img](https://pic1.zhimg.com/80/v2-0152f7ad8247863d3900645fb2fbb954_720w.png)SIR模型示意图

由图可知，此模型为单向模型，易感人数在不断地往感染人数输入，而同时最后感染人数也在单向往恢复人数输入，所以易感人数和感染人数最后均会下降到0，而与此同时，所有人均会成为恢复人数，此即为此模型的局限性。



## Link

https://kns.cnki.net/KCMS/detail/detail.aspx?dbcode=CMFD&&dbname=CMFDTEMP&filename=1018058943.nh

https://zhuanlan.zhihu.com/p/127010023

https://blog.piasy.com/2017/10/24/I-Need-Know-About-Compile-Link-Load-Execute/index.html

python 数据处理
