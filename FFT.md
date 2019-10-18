# FFT

#### 1.原位运算

  运算过程中，数据的存储位置不需要改变，降低算法的空间复杂度。

#### 2.比特位反序

  Definition:正常的比特位序号，按照比特的位序颠倒，

  n = b3b2b1b0, iv = b0b3b1b2

Reference:
https://itimetraveler.github.io/2017/09/08/%E3%80%90%E7%AE%97%E6%B3%95%E3%80%91%E4%BB%8E%E5%A4%9A%E9%A1%B9%E5%BC%8F%E4%B9%98%E6%B3%95%E5%88%B0%E5%BF%AB%E9%80%9F%E5%82%85%E9%87%8C%E5%8F%B6%E5%8F%98%E6%8D%A2/#%E5%BF%AB%E9%80%9F%E6%95%B0%E8%AE%BA%E5%8F%98%E6%8D%A2从多项式乘法到快速傅里叶变换
https://www.ilovematlab.cn/thread-119939-1-1.html FFT的详细解释
https://www.zhihu.com/question/21314374 如何通俗地解释什么是离散傅里叶变换
https://zhuanlan.zhihu.com/p/31584464 一小时学会快速傅里叶变换（Fast Fourier Transform）
https://oi.men.ci/fft-notes/ FFT 学习笔记
http://blog.miskcoo.com/2015/04/polynomial-multiplication-and-fast-fourier-transform
https://www.cnblogs.com/Lyush/articles/3219196.html快速傅里叶变换(FFT)的原理及公式
https://zh.wk.jsproxy.tk/wiki/%E5%BF%AB%E9%80%9F%E5%82%85%E9%87%8C%E5%8F%B6%E5%8F%98%E6%8D%A2 <wiki 快速傅里叶变换>
https://zh.wk.jsproxy.tk/wiki/%E7%A6%BB%E6%95%A3%E5%82%85%E9%87%8C%E5%8F%B6%E5%8F%98%E6%8D%A2 <wiki 离散傅里叶变换>
An algorithm for the machine calculation of complex Fourier series
https://zh.wk.jsproxy.tk/wiki/%E8%9D%B6%E5%BD%A2%E7%BB%93《基2蝴蝶结算法》
https://www-dot-cmlab-dot-csie-dot-ntu-dot-edu-dot-tw.ext.jsproxy.tk/cml/dsp/training/coding/transform/fft.html?&flag__=010 Fast Fourier Transform (FFT)
https://zh.wk.jsproxy.tk/wiki/%E5%BA%93%E5%88%A9%EF%BC%8D%E5%9B%BE%E5%9F%BA%E5%BF%AB%E9%80%9F%E5%82%85%E9%87%8C%E5%8F%B6%E5%8F%98%E6%8D%A2%E7%AE%97%E6%B3%95库利－图基快速傅里叶变换算法 

<https://blog.csdn.net/yi412/article/details/78904703> 快速傅里叶变换FFT的C语言算法彻底研究

反转比特位：
https://www.cnblogs.com/xueda120/p/3151354.html
https://blog.csdn.net/wuxianglonghaohao/article/details/21602305

比特位反转|对数运算

http://graphics.stanford.edu/~seander/bithacks.html#BitReverseObvious

⭐⭐⭐⭐《dft》 https://web.xidian.edu.cn/kywang/files/20121027_164737.pdf 



## Blog

## 1.理论基础

#### 1.1. 傅里叶变换定义${^{[1]}}$：

  频域分析的引入，任意信号都可以分解成不同频率、振幅和初相位角的正弦信号的叠加，这样就可以从频率的角度描述时域信号${^{[2]}}​$，傅里叶变换是以时间为自变量的“信号”函数，同以频率为自变量的“频谱”函数之间的变换关系；

#### 1.2 不同形式时域函数和频域函数

（1）时域连续造成频谱的非周期，时域的非周期性造成频域频谱密度连续；

（2）时域连续（周期）时域造成非周期频谱，时域周期性对应于频域的离散性；

（3）离散时域造成周期的延拓，时域非周期对应频域的连续；

（4）离散时域对应频域周期性，时域周期造成频域的离散；

#### 1.3 离散时间傅里叶变换

$$
\begin{align*}
& X(e^{j\omega}) = \sum_{-∞}^{+∞}{a[n]*e^{-j\omega n}} -^{[3]} \\
& DFT定义^{[4]}: \\
& X[k] = DFT[x(n)]_{N} = \sum_{n=0}^{N-1}{x(n)*e^{-j\frac{2*pi*kn}{N}}}\\
& X[k] = DFT[x(n)] = \sum_{n=0}^{N-1}{x(n)\omega_{N}^{kn}}\\
& \omega_{N} = e^{-j\frac{2*pi}{N}}\\
& 0=< k <= N-1\\

\end{align*}
$$







```matlab
N1 = 8; % 序列长度
SreialNums = 0:1:N1-1;
xn = 0.5.^SerialNums;
DFTN8 = zeros(0); % 8点傅里叶变换
for k = 1:1:N1
	% WN = exp(-j*n*2*pi/N1)
	temp = -1j*2*pi/N1;
	DFTN8(k) = sum(xn.*exp(temp*k*.SreialNums));
end

figure(1)
subplot(311)
stem(SreialNums,xn)
title('离散序列')
subplot(312)
stem(linspace(0,2*pi,N1),abs(DFTN8))
title('DFT')



```



### Reference:

[1]《数字信号处理及 MATLAB 实现》余成波 杨 菁 杨如民 周登义 编著

[2] 《信号分析与处理》

[3] 《信号与系统》奥本海姆

[4] 《DFT》https://