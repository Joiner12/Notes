# Kalman Filter

## 1.Reference

[1]《对Kalman(卡尔曼)滤波器的理解》

<https://www.cnblogs.com/xmphoenix/p/3634536.html>

[2]《Math\]理解卡尔曼滤波器 (Understanding Kalman Filter)》

<https://segmentfault.com/a/1190000000514987>

[3]《细说Kalman滤波：The Kalman Filter》

<https://www.cnblogs.com/ycwang16/p/5999034.html>

[4]《H无穷滤波器和Kalman滤波器比较》<https://wenku.baidu.com/view/6e7035323968011ca3009147.html>

[5]《AlanTukalman 滤波》<https://www.cnblogs.com/alantu2018/p/9224001.html>

[6]《MATLAB VAR函数》<https://blog.csdn.net/ouening/article/details/51281242>

[7] 《C KALMAN》<https://blog.csdn.net/von_kent/article/details/76610952>

[8]<https://blog.csdn.net/tiandijun/article/details/72469471>

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

```



cCode

```c
/*
对上面过程的特殊数据，一般化。 
1.假设21：19分温度为23及协方差为9（分别用X(k-1|k-1)和P(k-1|k-1)来表示） 
2.猜测21:20分温度与21：19分温度相同，协方差为16（分别用X(k|k-1)和Q来表示） 
3.计算温度，及协方差（结果用P(k|k-1)表示）可以得到下面两个公式 
X(k|k-1)=X(k-1|k-1)； 
P(k|k-1)=P(k-1|k-1)+Q; 
4. 读温度计的值为25，猜测协方差为16（分别用Z(k)和R表示） 
5.计算权值，即卡尔曼增益（用K(k)来表示） 
6.计算21:20分温度及协方差（分别用X(k|k)和P(k|k)表示）可以得到下面三个公式 
K(k)=P(k|k-1)/（P(k|k-1)+R） 
X(k|k)=X(k|k-1)+K(k)*（Z(k)-X(k|k-1)）
P(k|k)=（1-K(k)）*P(k|k-1) 
这五个公式就是，对卡尔曼五个核心公式进行简化
*/
/*       
        Q:过程噪声，Q增大，动态响应变快，收敛稳定性变坏
        R:测量噪声，R增大，动态响应变慢，收敛稳定性变好       
*/

#define KALMAN_Q 0.02

#define KALMAN_R 7.0000

/* 卡尔曼滤波处理 */

static double KalmanFilter(const double ResrcData,double ProcessNiose_Q,double MeasureNoise_R)
{

    double R = MeasureNoise_R;
    double Q = ProcessNiose_Q;

    static double x_last;
    double x_mid = x_last;
    double x_now;

    static double p_last;
    double p_mid ;
    double p_now;

    double kg;

    x_mid=x_last;                       //x_last=x(k-1|k-1),x_mid=x(k|k-1)
    p_mid=p_last+Q;                     //p_mid=p(k|k-1),p_last=p(k-1|k-1),Q=噪声

    /*
     *  卡尔曼滤波的五个重要公式
     */
    kg=p_mid/(p_mid+R);                 //kg为kalman filter，R 为噪声
    x_now=x_mid+kg*(ResrcData-x_mid);   //估计出的最优值
    p_now=(1-kg)*p_mid;                 //最优值对应的covariance
    p_last = p_now;                     //更新covariance 值
    x_last = x_now;                     //更新系统状态值

    return x_now;

}
```



## 3.（协）方差 | 期望 | 标准差

《方差，协方差、标准差，与其意义》

<https://blog.csdn.net/yangdashi888/article/details/52397990>

## 4.Kalman滤波推导过程

$$
系统模型：X_k = F_k*X_{k-1} + B_k*U_k + \omega_k \\
观测模型：Z_k = H_k*X_k + v_k \\ 
五条公式：\\
****预测与更新****\\
**预测问题**\\
已知:\\
上一个状态的更新值\\
上一个状态的更新值和真实值之间的误差\\
求解：\\

这一个状态的预测值\\
这一个状态的预测值和真实值之间的误差\\
$$

```c
//上一个周期更新值 Xk-1|k-1  预测当前时刻预测值 Xk|k-1

//由上一个更新值和真实值之间的误差 Pk-1|k-1 预测下一个预测值和真实值之间的误差 Pk|k-1


```

