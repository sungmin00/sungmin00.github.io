---
title: "Editing Factual Knolwledge in Language Models"
categories:
    - paper review
tags:
    - [graph,gcn,spectral]
date: 2021-09-26 
use_math : true
---
---
## **Introduction** 
해당 논문은 Language Model이 pre-training 으로 부터 acquire 하며 parameter 에 저장된 factual knowledge 들이 시간이 지나면서 obsolete(진부화) 되거나 틀린 정보가 될 수 있기에, 이를 expensive pre-training 이나 fine-tuning 하지 않고 modify 하는 hypernetwork **KnowledgeEditor** 을 제시한다.
- [x] Generality : meta-learning 과 같은 special 한 pre-training 이 필요 없어야 함 
- [x] Reliability : modify 하고자 하는 knowledge 이외의 knowledge 에는 최대한 영향을 주지 않고 successfully update 해야 한다. 
- [x] consistency : specific knowledge를 modify 할 때 , equivalent formulation 되었을 때도 modify 된 knowledge 를 추출할 수 있어야 함 


## **Method**
### Measure
1. Success rate : model의 parameter가 $\theta'$ 가 successfully update 되었는지 확인하기 위하여 revised prediction $\mathcal{D}$이 의도한 대로 변화하였는지 정확도를 측정 
2. Retain accuracy :  revised prediction 의 여집합 $\mathcal{O}^x$ 의 primal model의 prediction 과 비교 (높을 수록 reliability 가 보장 된다.)
3. equivalence accuracy : revised prediction 의 sementically equivalent input $\mathcal{P}^x$ 에 대한 modified model $\theta'$의 prediction 정확도를 측정 (높을 수록 Consistency 보장)
4. performance detoriation : primal model 에 비하여 test performance 가 detoriates 된 정도 

### Optimization 
해당 논문에서 풀고자 하는 optimization problem 은 다음과 같다.  

$$
\displaystyle\min_{\phi}\sum_{\hat{x}\in \mathcal{P}^x}\mathcal{L}(\theta';\hat{x},a) \\\ s.t \;\mathcal{C}(\theta,\theta',f;\mathcal{O}^x)\leq m 
$$


Equivalent 한 semantic을 가지는 $\mathcal{P}^x$ 에 대해서는 revised prediction $a$ 와의 차이를 minimize 하는 것이 Equivalence accuracy 를 높이는 것이고 , 밑의 제약 조건은 Retain accuracy를 위해 constrain을 거는 것임을 알 수 있다. \
여기서 constraint $\mathcal{C}$ 는 KL divergence로 주어진다. 
> **KL Divergence**   
>  : 두 확률 분포 p, q 의 차이를 cross-entropy 로 설명하는데 , 간략히 $H(p,q)-H(p)$ 이다. KL Divergence 는 항상 0 이상의 값을 가지며 , 거리 개념은 아니다. 

$$
C_{KL}(\theta,\theta',f;\mathcal{O}^x) = \displaystyle\sum_{x'\in \mathcal{O}^x}\sum_{c\in\mathcal{Y}}p_{Y|X}(c|x',\theta)log\frac{p_{Y|X}(c|x',\theta)}{p_{Y|X}(c|x',\theta')}
$$



즉 모든 $x'\in\mathcal{O}^x$ 에 대해서 output sample space $\mathcal{Y}$ 에서 기존 확률 분포와 , modify 된 후의 확률 분포의 KL Divergence를 summation 함으로서, 최대한 비슷한 확률 분포를 가지기를 기대하는 것임을 알 수 있다. 기존의 다른 논문에서는 변경전, 후 parameter 사이의 $\mathcal{L}^p$ norm을 constraint 로 사용하였으나 , neural model은 highly non-linear 하기에, linear 한 difference 를 표현하는 $\mathcal{L}^p$ norm 은 effective 하지 못했기에 해당 논문에서는 채용하지 않았다. 

### Tractable approximations
Non-linear한 Constrained optimization은 generally intractable 하기에 Lagrangizn-relaxation 을 사용하였다. 
>**Lagrangian Relaxation**  
>: loss function 에 penalty와 constraint 를 곱한 값을 더해 줌으로써 , 새로운 loss 값의 optimal한 solution 은 기존 optimal solution 의 lower bound를 형성한다. 
>$min\,c'x\;s.t\;Ax=b$ 이라 할 때, $\mathcal{L}(x,p)=c'x+p(b-Ax)\;for\;x\geq0$ 과 같이 변형시켜 사용한다. 일단 새로은 loss function 의 optimal soultion 이 lower bound 임은 증명 되었으니, modified 된 loss 의 p에 대한 optimal solution 값을  maximize 해야 한다.

여기서 기존의 Optimization problem 을 특정 y를 montecarlo search로 sampling 하는 식으로 approximation 할 수 있다. (Constraint 의 sigma 순서를 바꾼 후 , c를 하나만 sampling)

$$
\displaystyle\min_{\phi}\max_{\alpha}f(x,\theta)+\alpha\cdot(\mathcal{C}(y,\theta)-m) \\\ y\sim p(y)
$$

물론 seq2seq 모델에서는 
single point $y$ 에 대해서도 KL을 다루기 어렵기에($\mathcal{Y}$ is unbounded),  beam search로 도출된 sample space 에서 computation 을 다룬다. 












