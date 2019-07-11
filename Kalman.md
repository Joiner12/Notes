# Kalman Filter

## 1.Reference

[1]《Math\]理解卡尔曼滤波器 (Understanding Kalman Filter)》

<https://segmentfault.com/a/1190000000514987>

[2]《细说Kalman滤波：The Kalman Filter》★★★

<https://www.cnblogs.com/ycwang16/p/5999034.html>

[3]《H无穷滤波器和Kalman滤波器比较》

<https://wenku.baidu.com/view/6e7035323968011ca3009147.html>

[4]《MATLAB VAR函数》

<https://blog.csdn.net/ouening/article/details/51281242>

[5] 《EKF》★★★

<https://blog.csdn.net/Q_18163961/article/details/52505591>

## 2.CODE

**MATLAB**

```matlab
clear
N=200;%取200个数
%% 生成噪声数据 计算噪声方差
% 产生一个1×N的行向量，第一个数为0
% w为过程噪声（其和后边的v在卡尔曼理论里均为高斯白噪声）
w=randn(1,N); 
w(1)=0;
 % R、Q分别为过程噪声和测量噪声的协方差
 % (此方程的状态只有一维，方差与协方差相同) 
Q=var(w);

v=randn(1,N);%测量噪声
R=var(v);

%% 计算真实状态
x_true(1)=0;%状态x_true初始值
A=1;% a为状态转移阵，此程序简单起见取1
for k=2:N
 	% 系统状态方程，k时刻的状态等于k-1时刻状态乘以状态转移阵加噪声
 	% 控制输入量位0，
    x_true(k)=A*x_true(k-1)+w(k-1); 
end

%% 由真实状态得到测量数据， 测量数据才是能被用来计算的数据， 其他都是不可见的
H=0.2;
z=H*x_true+v;%量测方差，c为量测矩阵，同a简化取为一个数


%% 预测-更新过程

% x_predict: 预测过程得到的x
% x_update:更新过程得到的x
% P_predict:预测过程得到的P
% P_update:更新过程得到的P

%初始化误差 和 初始位置
x_update(1)=x_true(1);%s(1)表示为初始最优化估计
P_update(1)=0;%初始最优化估计协方差

for t=2:N
    %{
    -------------------1. 预测-------------------
    %}
    %-----1.1 预测状态-----
    x_predict(t) = A*x_update(t-1); %没有控制变量
    %-----1.2 预测误差协方差-----
    %{
    	p1为一步估计的协方差，
    	此式从t-1时刻最优化估计s的协方差得到t-1时刻到t时刻一步估计的协方差
    %}
    P_predict(t)=A*P_update(t-1)*A'+ Q;
    %{
    -------------------2. 更新-------------------
    %}
    %-----2.1 计算卡尔曼增益-----
    %{
   		仿真程序需要使用R，实际过程中，R存在于观测值中，是客观到物理量
    %}
    K(t)=H*P_predict(t) / (H*P_predict(t)*H'+R);
    % b为卡尔曼增益，其意义表示为状态误差的协方差与量测误差的协方差之比(个人见解)
   
   	%-----2.2 更新状态-----
   	% Y(t)-a*c*s(t-1)称之为新息，是观测值与一步估计得到的观测值之差，
    % 此式由上一时刻状态的最优化估计s(t-1)得到当前时刻的最优化估计s(t)
    x_update(t)=x_predict(t)  +  K(t) * (z(t)-H*x_predict(t));
    
    %-----2.3 更新误差协方差-----
    %此式由一步估计的协方差得到此时刻最优化估计的协方差
    P_update(t)=P_predict(t) - H*K(t)*P_predict(t);
end

%% plot
%作图，红色为卡尔曼滤波，绿色为量测，蓝色为状态
%kalman滤波的作用就是 由绿色的波形得到红色的波形， 使之尽量接近蓝色的真实状态。
t=1:N;
plot(t,x_update,'r',t,z,'g',t,x_true,'b');
legend('kalman','obser','true')

```

C Code Ver.1.0

```c
/*********************kalman.h**********************/
#pragma once
/*
	Created date:2019-7-8
	Kalman Filter
*/ 
typedef struct
{
	double nVarQ;			// 过程噪声方差
	double nVarR;			// 观测噪声方差
	double nPreX;			// X(k-1|k-1)
	double nKg;				// kalman增益
	double nPreZ;			// Z(k-1|k-1)
	double nP;				// 协方差
	double nU;				// 控制量
	double nXreal;			// 真实状态量
}tKalman;

tKalman* KalmanGet();

void KalmanInit(tKalman* pSelf_, double nVarQ_, double nVarR_);

void KalmanProcess(tKalman* pSelf_, double nZk_,double nUk_);

void Kalman_Test();


/*********************kalman.c**********************/
#include "stdafx.h"
#include "kalman.h"

tKalman g_tKalman;

/*
Kalman Filter
Q:过程噪声，Q增大，动态响应变快，收敛稳定性变坏
R:测量噪声，R增大，动态响应变慢，收敛稳定性变好
/------------预测-----------/
X(k | k - 1) = X(k - 1 | k - 1)	+ u(k)		(1)	状态预测
P(k | k - 1) = P(k - 1 | k - 1) + Q			(2)	预测方差
/-----------更新------------/
K(k)=P(k|k-1)/（P(k|k-1)+R）					(3)	更新kalman增益
X(k|k)=X(k|k-1)+K(k)*（Z(k)-X(k|k-1)）		(4)	状态更新
P(k|k)=（1-K(k)）*P(k|k-1)					(5)	滤波方差更新
*/

// 获取全局变量
tKalman* KalmanGet()
{
	return 	&g_tKalman;
}

void KalmanInit(tKalman* pSelf_, double nVarQ_, double nVarR_)
{
	nVarQ_ > 0 ? pSelf_->nVarQ = nVarQ_ : pSelf_->nVarQ = 0.0;
	nVarR_ > 0 ? pSelf_->nVarR = nVarR_ : pSelf_->nVarR = 0.0;
	pSelf_->nKg = 0.0;
	pSelf_->nP = 10.0;			// 初始化不为零
	pSelf_->nPreX = 0.0;			// 初始状态x(k-1|k-1)
	pSelf_->nU = 0.0;
	pSelf_->nXreal = 0.0;
}

void KalmanProcess(tKalman* pSelf_, double nZk_, double nUk_)
{
	int _nAs = 1;//A状态矩阵
	/*
		X(k | k - 1) = X(k - 1 | k - 1) + u(k)		(1)	状态预测
	*/
	double _nXKK_1 = (pSelf_->nPreX)*_nAs + nUk_;
    /*
	P(k | k - 1) = P(k - 1 | k - 1) + Q			(2)	预测方差
    */
    double _nPkk_1 = pSelf_->nP + pSelf_->nVarQ;

    /*
        K(k)=P(k|k-1)/（P(k|k-1)+R）					(3)	更新kalman增益
    */
    double _nKg = _nPkk_1 / (_nPkk_1 + pSelf_->nVarR);
    pSelf_->nKg = _nKg;

    /*
        X(k|k)=X(k|k-1)+K(k)*（Z(k)-X(k|k-1)）		(4)	状态更新
    */
    double _nXkk = _nXKK_1 + _nKg * (nZk_ - _nXKK_1);
    pSelf_->nPreX = _nXkk;
    pSelf_->nPreZ = nZk_;

    /*
        P(k|k)=（1-K(k)）*P(k|k-1)					(5)	滤波方差更新
    */
    double _nPkk = (1 - _nKg)*_nPkk_1;
    pSelf_->nP = _nPkk;
}
void Kalman_Test()
{
	cout << "Simulator for kalman filter" << endl;
	int _nLoopCnt = 0;
	ofstream kalman("kalman.txt");
	clock_t tStart, tEnd;
	tStart = clock();
	while (++_nLoopCnt <= 1000)
	{
		if (_nLoopCnt == 1)
		{
			double _nVarQ = 10;
			double _nVarR = 10;
			KalmanInit(KalmanGet(), _nVarQ, _nVarR);
			srand((unsigned)time(NULL));
		}
		else
		{
			// x(k) = a*x(k-1) + w1(k) + u(k)
			// sin(2*pi*f*t)
			static double _nFre = 2 * 3.1415 * 0.1 * 0.1;
			double _nUk = 10 * sin(_nFre*_nLoopCnt);
			// 真实状态
			double _nXreal = _nUk + KalmanGet()->nXreal;// +(rand() % 10 - 5.0);
			// z(k) = h*x(k)+w(k); 带观测噪声观测值
			double _nZk = _nXreal + (rand() % 10 - 1.0);


		KalmanProcess(KalmanGet(), _nZk, _nUk);
		KalmanGet()->nXreal = _nXreal;
		double _nXkk = KalmanGet()->nPreX;
		kalman << _nLoopCnt * 0.1 << "," << _nXreal << "," << _nZk << "," 			<< _nXkk << endl;
		}
    }
    kalman.close();
    tEnd = clock();
    cout << "Operation duration:" << (tEnd - tStart) << endl;
}
```

%% 数据处理

```matlab
%% 测试kalman.h .c
%{
    获取处理数据
%}
clc;
datapath = 'D:\Codes\VsProjects\LeetCode\LeetCode';
filename = 'kalman.txt';
file = strcat(datapath,'\',filename);

origin = load(file);
if isequal(length(origin),0)
    warning('数据导入出错');
end
time_k = origin(:,1);
real_x = origin(:,2);
obser_x = origin(:,3);
kalman_x = origin(:,4);

figure(1)
p = plot(time_k,real_x,time_k,obser_x,time_k,kalman_x);
p1.LineWidth = 2;
grid on 
legend('real','obser','kalman')
```



## 3.（协）方差 | 期望 | 标准差

#### 3.1《方差，协方差、标准差，与其意义》

<https://blog.csdn.net/yangdashi888/article/details/52397990>

均值：样本集合的中间点；

方差：样本点到样本中间点距离的均值；

标准差：sqrt(方差)；

协方差：表示两组数据的相关度（正负相关）

#### 3.2 std、var函数

var计算矩阵（数组）的方差；

<https://ww2.mathworks.cn/help/matlab/ref/var.html>



## 4.Kalman滤波推导过程

$$
Reference:https://www.cnblogs.com/ycwang16/p/5999034.html
$$



#### 4.1 Extented Kalman

（1）扩张卡尔曼滤波是将非线性系统线性化，然后进行滤波，其本质是还是线性滤波器，且存在一定的局限性，强非线性违背局部线性假设，Taylor展开式中大偏差的高阶项被忽略，但可能会造成滤波发散；

（2）Jacobian matrix

#### 4.2 KF解决的问题

1. Kalman滤波所解决的问题，是对一个动态变化的系统的状态跟踪的问题，基本的模型假设包括：1）系统的状态方程是线性的；2）观测方程是线性的；3）过程噪声符合零均值高斯分布；4）观测噪声符合零均值高斯分布；从而，一直在线性变化的空间中操作高斯分布，状态的概率密度符合高斯分布。
2. 对于线性系统，零均值高斯噪声的系统，Kalman是理论上无偏的，最优滤波器；
3. Kalman滤波在实际使用中，要注意参数R和Q的调节，这两者实际上是相对的，表示更相信观测还是更相信预测。具体使用时，R可以根据过程噪声的幅度决定，然后Q可以相对R来给定。当更相信观测时，把Q调小，不相信观测时，把Q调大；
4. Q越大，表示越不相信观测，这是系统状态越容易收敛，对观测的变化响应越慢。Q越小，表示越相信观测，这时对观测的变化响应快，但是越不容易收敛。Q、R值的大小表示置信度大小；