---
title: "VAE + Bayesian HyperNet"
categories:
    - base knkowledge
tags:
    - [vae]
date: 2021-09-26 
use_math : true
---
---
## **1. VAE**
### **Generative Model** 
![](/assets/images/VAE_1.png) 
variational auto encoder 는 generative model 로서 위 그림과 같이 Latent variable $z$ 로 부터 $x$ 를 generate 하기 위한 모델이다.  
Vae 네트워크가 출력하고자 하는 값은 generate 하고자 하는 $x$ 의 ouptut space 에서의 확률 분포이며 , 추가적으로 controllable 한 $z$를 통해 output $x$에 characteristic 이 포함되기를 원한다. 

### **Maximum Likelihood Estimation** 
MLE는 모수적인 데이터 밀도 추정 방법으로써 파라미터 $\theta=(\theta_1,\theta_2,\cdots)$ 으로 구성된 어떤 확률 밀도함수 $P(x|\theta)$ 에서 관측된 표본 데이터 집합을 $x=(x_1,x_2,\cdots)$ 이라 할 때 , 이 표본들에서 파라미터 $\theta$ 를 추정하는 방식이다. 

$$
L(\theta) = p(X|\theta)
$$

*ex)*  
만약 data의 distribution 이 parameter로 $\theta = (u,\sigma)$인 정규분포를 가진다면, 관측된 표본 $x_1,x_2\cdots$ 가 이 정규분포를 따를 확률은 

$$
p(x_n|\theta)=\frac{1}{\sqrt{2\pi\sigma}}exp({-\frac{(x_n-u)^2}{2\sigma^2}})
$$

일 것이고, Likelihood 는

$$
L(\theta)= p(X|\theta)=\frac{1}{\sqrt{2\pi\sigma}}exp(\sum_{x_i}-\frac{(x_i-u)^2}{2\sigma^2})
$$ 

이 될 것이다. 이를 maximize 하기 위해서는 $\displaystyle\sum_{x_i}(x_i-u)^2$ 를 minimize 하는 것으로 귀결 된다. 이는 곧 , parameter $u$ 가 관측된 데이터들의 평균값일 때 likelihood 가 maximize 되는 것임을 알 수 있다. 이처럼 likelihood 를 최대화 하는 parameter 값을 maximum likelihood estimate 라고 한다. 

### **Prior Distribution p(z)**
vae 에서는 $z$ 의 확률분포를 normal distribution 과 같은 simple distribution 으로 가정하는데 , 이 것이 가능한 이유는 $p(x|g_\theta(z)) = \mathcal{N}(x|g_\theta(z),\sigma^2*I)$ (측정값은 참값을 기준으로 하는 정규 분포) 에서 $g_\theta$ 가 multi layer neural network 이기에 초반 몇개의 layer 에서 normally distribution 을 보다 복잡한 latent space를 익히는데 사용될 수 있다. 










