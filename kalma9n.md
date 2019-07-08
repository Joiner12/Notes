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
			kalman << _nLoopCnt * 0.1 << "," << _nXreal << "," << _nZk << "," << _nXkk << endl;
		}
	}
	kalman.close();
	tEnd = clock();
	cout << "Operation duration:" << (tEnd - tStart) << endl;
}