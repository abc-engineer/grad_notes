2026-05-12 08:20
## 8강 Clustering

- 학기 전반기는 지도학습
- 지도학습 다음 비지도 학습 (저번주는 density)
- 오늘은 clustering
	- 비지도 학습 중 쉽고 기초

### Clustering
- 클러스터링(clustering)은 비지도 학습(unsupervised learning)의 또 다른 핵심 과제이다.    
- 밀도 추정(density estimation)이 데이터의 기저 확률 분포(underlying probability distribution)를 모델링하는 것을 목표로 하는 반면, 클러스터링은 데이터 포인트들을 여러 그룹으로 조직하여 데이터셋 내부의 의미 있는 구조를 발견하는 데 초점을 둔다.

- 지도학습이 아니기 때문에 정답이 없음. 
- 피쳐들의 유사도를 기반으로 class를 나누는 과정임.

- 중요하게도, 클러스터링 결과는 유사성(similarity)을 어떻게 정의하는지, 어떤 알고리즘을 선택하는지, 그리고 데이터에 대한 기본 가정(예: 클러스터의 형태(shape), 스케일(scale), 밀도(density)에 따라 달라진다.    
- 따라서 동일한 데이터셋에 대해서도 서로 다른 방법이 서로 다른 그룹화를 생성할 수 있다.

### K-Means Clustering
- 많은 클러스터링 기법들 가운데, K-means는 가장 단순하면서도 널리 사용되며 계산 효율성이 높은 알고리즘 중 하나이다.    
- K-means의 핵심 아이디어는 매우 직관적이다. 각 클러스터를 중심점(center)인 센트로이드(centroid) 또는 프로토타입(prototype)으로 표현하고, 각 데이터 포인트를 가장 가까운 센트로이드에 할당하는 것이다.

- K가 들어간 크러스터링은 보통 빠르고 단순, 직관적임.
- k개의 means(중앙값)들 중 어디에 가까운지를 순회하면서 분류류

- 우리는 $N$개의 관측값(observations)으로 이루어진 데이터셋에서 시작한다.
- 각 관측값은 $D$차원 벡터
  
$$  
\mathbf{x}^{(n)} \in \mathbb{R}^D,\quad n=1,\ldots,N  
$$
- 우리의 목표는 이 데이터 포인트들을 $K$개의 클러스터로 구성하는 것이다.
- 클러스터를 정의하기 위해, 다음과 같은 프로토타입(prototype) 또는 센트로이드(centroid) 집합을 도입한다.  

$$  
\boldsymbol{\mu}_k \in \mathbb{R}^D,\quad k=1,\ldots,K  
$$
- 이러한 프로토타입 $\boldsymbol{\mu}_k$는 각 클러스터의 중심(center)을 나타낸다.


- K-means 알고리즘은 각 데이터 포인트를 가장 가까운 프로토타입(prototype) 또는 센트로이드(centroid)를 가지는 클러스터에 할당한다.
- 이 아이디어를 수식적으로 표현하기 위해, 전체 클러스터 내부 분산(within-cluster variance)을 측정하는 **목적 함수(objective function) $J$를 정의**한다.  

$$  
J=\sum_{n=1}^{N}\sum_{k=1}^{K} r_{nk}\left|\mathbf{x}^{(n)}-\boldsymbol{\mu}_k\right|^2  
$$

- 여기서  $\left|\mathbf{x}^{(n)}-\boldsymbol{\mu}_k\right|^2$는 데이터 포인트 $\mathbf{x}^{(n)}$와 중심 $\boldsymbol{\mu}_k$ 사이의 제곱 유클리드 거리(squared Euclidean distance)를 의미한다.
- 목적함수를 최소화 해야 하니까 센터$\mathbf{x}^{(n)}$와 중심 $\boldsymbol{\mu}_k$ 의 거리를 최소화 해야 함. →**내부 분산(within-cluster variance) 최소화**

- $r_{nk}$는 다음과 같이 정의되는 지시 변수(indicator variable)이다.  

$$  
r_{nk}=  
\begin{cases}  
1, & \text{데이터 포인트 } \mathbf{x}^{(n)} \text{가 클러스터 } k \text{에 할당된 경우}\\ 
0, & \text{그 외의 경우}  
\end{cases}  
$$

	- $r_{nk}$는 빨간색으로 분류된다면 빨간색에서만 1 파랑 초록에서는 0
- 따라서 클러스터링 문제는 최소화(minimization) 문제로 볼 수 있으며, 우리는 목적 함수 $J$를 최소화하는 $r_{nk}$와 $\boldsymbol{\mu}_k$의 값을 찾고자 한다.
- K-means는 일반적으로 **좌표 하강법(coordinate descent)** 이라 불리는 반복적인(iterative) 2단계 절차를 사용하여 이 최소화 문제를 해결한다.
- 좌표 하강법은 다른 변수들을 고정한 상태에서 한 변수 집합만 번갈아 갱신함으로써 함수를 최소화하는 최적화 방법이다.

- 결국 최소화 문제로 변하게 됨.
- 목적 함수 $J$를 최소화하는 $r_{nk}$와 $\boldsymbol{\mu}_k$의 값을 찾는 문제
- 2개의 파라미터를 동시에 최적화 하기 힘들기 때문에 1번 파라미터$r_{nk}$를 최적화 할때 2번 파라미터$\boldsymbol{\mu}_k$를 고정, 2번 최적화에는 1번 파라미터$r_{nk}$를 고정 →**좌표 하강법(coordinate descent)** 이라고 함.

- 첫 번째 단계에서는 클러스터 중심 $\boldsymbol{\mu}_k$가 고정되어 있다고 가정하고, 지시 변수 $r_{nk}$를 갱신하여 목적 함수 $J$를 최적화한다.
- 각 데이터 포인트 $\mathbf{x}^{(n)}$에 대해,  

$$  
\left|\mathbf{x}^{(n)}-\boldsymbol{\mu}_k\right|^2  
$$  
를 최소화하는 $k$번째 클러스터를 선택하여 가장 가까운 클러스터에 할당한다.
- 이를 수식으로 표현하면 다음과 같다.  

$$  
r_{nk}=  
\begin{cases}  
1, & \text{if } k=\arg\min_k \left|\mathbf{x}^{(n)}-\boldsymbol{\mu}_k\right|^2\\  
0, & \text{otherwise}  
\end{cases}  
$$

- 즉, 각 데이터 포인트는 자신과 가장 가까운 중심(center)을 가지는 클러스터에 할당된다.

- 두 번째 단계에서는 할당 변수 $r_{nk}$가 고정되어 있다고 가정하고, **목적 함수 $J$를 최소화하도록 클러스터 중심 $\boldsymbol{\mu}_k$를 갱신**한다.
- 목적 함수 $J$는 $\boldsymbol{\mu}_k$에 대해 이차식(quadratic form)이므로, $J$를 $\boldsymbol{\mu}_k$에 대해 미분함으로써 최적의 클러스터 중심을 구할 수 있다.
- 도함수를 0으로 두면 다음을 얻는다.  

$$  
\frac{\partial J}{\partial \boldsymbol{\mu}_k} =  
2\sum_{n=1}^{N} r_{nk}\left(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k\right)  
=0  
$$

- 이 식을 $\boldsymbol{\mu}_k$에 대해 풀면 다음을 얻는다.  

$$  
\boldsymbol{\mu}_k =  
\frac{\sum_n r_{nk}\mathbf{x}^{(n)}}{\sum_n r_{nk}}  
$$

- 이는 각 클러스터 중심이 해당 클러스터에 할당된 모든 데이터 포인트들의 평균(mean)임을 보여준다.
- 바로 이 때문에 이 알고리즘이 K-means라고 불린다.

- 이 두 단계, 즉 데이터 포인트를 클러스터에 할당하는 단계와 클러스터 중심을 갱신하는 단계는 할당 변수 $r_{nk}$와 중심 $\boldsymbol{\mu}_k$가 더 이상 변하지 않을 때까지 반복된다.    
- 이는 알고리즘이 수렴(converged)했음을 의미한다.

- 센터값 고정 → $r_{nk}$ 계산 →중심 $\boldsymbol{\mu}_k$ 업데이트 → 반복복

- 여기의 그래프는 데이터 포인트를 클러스터에 할당하는 단계(파란 점)와 클러스터 중심을 갱신하는 단계(빨간 점) 이후의 비용 함수(cost function)를 보여준다.    
- 이 두 단계는 할당 결과가 더 이상 변하지 않을 때까지 번갈아 반복된다.

- 다음은 이미지 분할(image segmentation)을 위해 K-means 클러스터링 알고리즘을 사용하는 두 가지 예시이다.

- K-means 클러스터링에서 $K$는 클러스터의 개수를 나타내는 하이퍼파라미터(hyperparameter)이다.
- 클러스터링은 일반적으로 비지도 학습이므로, 보편적으로 항상 올바른 단일 $K$ 값은 존재하지 않는다. 하지만 실제로는 **elbow method나 silhouette score와 같은 방법을 사용**하여 $K$를 선택하는 경우가 많다.
- Elbow method에서는 여러 값의 $K$에 대해 K-means를 수행하고, 클러스터 내부 제곱합(within-cluster sum of squares)을 계산한다.  

$$  
W_K  =  
\sum_{k=1}^{K}  
\sum_{\mathbf{x}_i \in C_k}  
\left|\mathbf{x}_i-\boldsymbol{\mu}_k\right|^2  
$$
- 이후 $W_K$를 $K$에 대해 그래프로 나타냈을 때, 감소 속도가 급격히 느려지는 지점, 즉 “팔꿈치(elbow)”가 형성되는 지점의 $K$를 선택한다.

- K 값을 연구자가 정해야함. → 이게 어려운 점.
- 이 K값에 따라 결과가 많이 달라짐.

- 이러한 그래프의 예시는 아래에 제시되어 있다.

- Silhouette score에서는 각 데이터 포인트 $\mathbf{x}_i$에 대해, $a_i$를 같은 클러스터 내 다른 포인트들과의 평균 거리로 정의하고, $b_i$를 가장 가까운 이웃 클러스터에 속한 포인트들과의 평균 거리로 정의한다.
- 그러면 $\mathbf{x}_i$의 silhouette score는 다음과 같다.  

$$  
s_i  = \frac{b_i-a_i}{\max(a_i,b_i)}  
$$
- 최종적으로 전체 silhouette score는 다음과 같이 정의된다.  

$$  
S_K =  \frac{1}{N}  
\sum_{i=1}^{N} s_i  
$$
- 실루엣 스코어도 변곡점에서 K를 결정한다고 생각 하면 됨.

- 요약하면, K-means 알고리즘은 일반적으로 유클리드 거리(Euclidean distance)를 사용하여 측정되는 유사성을 기반으로 데이터를 $K$개의 클러스터로 분할하는 널리 사용되는 **비확률적(non-probabilistic) 클러스터링 방법**이다.    
- 알고리즘은 반복적으로 진행된다. 먼저 각 데이터 포인트를 가장 가까운 클러스터 중심에 할당하고, 이후 각 클러스터 중심을 해당 클러스터에 속한 데이터 포인트들의 평균으로 다시 계산한다.
- 이러한 교대적인(alternating) 2단계 절차는 다음 절에서 다룰 Expectation-Maximization(EM) 알고리즘의 구조와 매우 유사하다.    
- 특히, K-means의 할당 단계(assignment step)는 E-step(Expectation step)에 대응되며, 클러스터 중심을 갱신하는 단계는 M-step(Maximization step)에 대응된다.

### Gaussian Mixture Models
- K-means는 단순하고 직관적이며 계산 효율성이 높지만, 몇 가지 중요한 한계를 가진다.    
- 첫째, K-means는 암묵적으로 클러스터가 구형(spherical)이며, 비슷한 크기를 가지고, 서로 잘 분리되어 있다고 가정한다.    
	- 평균값을 가지고 계산을 하기 때문에 원형을 갖게 됨
	- 실제 데이터가 길게 퍼져있을대는 잘 학습이 되지 않음.
- 다시 말해, 클러스터가 명확한 기하학적 구조를 가지며 서로 거의 겹치지 않을 때 가장 잘 동작한다.    
- 그러나 실제 데이터셋에서는 클러스터의 형태(shape), 크기(size), 방향(orientation)이 크게 다를 수 있기 때문에, 이러한 가정은 지나치게 제한적일 수 있다.

- GMM은 전에 density 추정에도 사용되었지만 클러스터링에도 아주 많이 사용
- EM 알고리즘을 사용하는데 K-means와 매우 유사함.


- 두번째 단점으로는, K-means는 확률적(probabilistic) 방법이 아니다.    
	- $r_{nk}$가 0,1 바이너리 값을 갖기 때문에 확률적 방법이라고 할 수 없음
- **K-means는 하드 할당(hard assignment)** 을 수행하며, 이는 각 데이터 포인트가 정확히 하나의 클러스터에 확정적으로 할당됨을 의미한다.    
- 이러한 경직된 할당은 클러스터가 서로 겹치거나 데이터가 클러스터 소속(cluster membership)에 대한 불확실성을 자연스럽게 가지는 경우 문제가 될 수 있다.

- 이러한 한계를 극복하기 위해, 이제 우리는 보다 유연하고 완전한 확률적(probabilistic) 클러스터링 방법인 Gaussian Mixture Model(GMM)을 살펴본다.    
- 앞서 GMM을 밀도 추정(density estimation)의 맥락에서 소개했지만, 이제는 이를 클러스터링 관점에서 다시 해석한다.    
- 즉, 전체 데이터 분포를 단순히 모델링하는 대신, 각 가우시안 성분(Gaussian component)을 하나의 클러스터를 나타내는 것으로 간주한다.

- K-means와 달리, GMM은 클러스터가 구형(spherical)이고 동일한 크기를 가진다고 가정하지 않는다.    
- 대신 GMM에서는 각 클러스터가 고유한 공분산 구조(covariance structure)를 가질 수 있으므로, 클러스터의 형태(shape), 크기(scale), 방향(orientation)의 다양성을 표현할 수 있다.    
- 또한 GMM은 **소프트 할당(soft assignment)**을 사용한다.    
- 즉, 각 데이터 포인트를 하나의 클러스터에 단순히 할당하는 대신, 각 가우시안 성분에 속할 사후확률(posterior probability)을 계산한다.    
- 이러한 확률적 접근(probabilistic approach)은 서로 겹치는 클러스터를 자연스럽게 처리할 수 있게 하며, 보다 복잡한 데이터 구조를 표현할 수 있도록 해준다.

- 이전 장에서 우리는 최대우도추정(maximum likelihood estimation)을 사용하여 GMM의 파라미터 추정을 정식화하였다.    
- 그러나 우도(likelihood)를 직접 최대화하는 것은 해석적으로 다루기 어려운(intractable) 문제임이 밝혀진다.    
- 이러한 어려움을 해결하기 위해, GMM은 일반적으로 효율적인 반복적(iterative) 해결 방법을 제공하는 Expectation-Maximization(EM) 알고리즘을 사용하여 학습된다.    
- EM 알고리즘은 posterior cluster membership probability(소프트 할당)를 추정하는 단계와, 기대 로그우도(expected log-likelihood)를 최대화하도록 가우시안 성분의 파라미터를 갱신하는 단계를 번갈아 수행한다.

- GMM모델에서도 가우시안을 몇개 쓸지는 K-means 처럼 하이퍼 파라미터로 연구자가 설정해야 함.

### The Expectation-Maximization Algorithm for Gaussian Mixture Models
- Gaussian mixture model(GMM)에서는 데이터 포인트 $\mathbf{x}$의 확률 분포를 $K$개의 가우시안 성분(Gaussian component)의 가중합(weighted sum)으로 모델링하며, 각 가우시안은 하나의 클러스터에 대응된다.
- 혼합 분포(mixture distribution)는 다음과 같이 주어진다.  

$$  
p(\mathbf{x}) =  
\sum_{k=1}^{K}  
\pi_k \mathcal{N}(\mathbf{x}\mid \boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
$$

- 여기서 $K$는 가우시안 성분의 개수이고, **$\pi_k$는 $k$번째 성분의 mixing coefficient(사전확률; prior probability)**,  $p(z_k=1)$을 의미한다.
- 또한  **$\mathcal{N}(\mathbf{x}\mid \boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)$ 는 평균(mean) $\boldsymbol{\mu}_k$와 공분산(covariance) $\boldsymbol{\Sigma}_k$** 를 가지는 가우시안 분포이다.

- 앞서 논의했듯이, 로그우도(log-likelihood)를 직접 최대화하는 것은  

$$  
\ln p(\mathbf{X}\mid \boldsymbol{\pi},\boldsymbol{\mu},\boldsymbol{\Sigma}) =  
\sum_{n=1}^{N}  
\ln(  
\sum_{k=1}^{K}  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid \boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k))  
$$

- 직접 최적화하기 어려울 수 있다.
- 이를 해결하기 위해 Expectation-Maximization(EM) 알고리즘을 사용하며, 이는 사후 클러스터 확률(posterior cluster probability)을 계산하는 단계(E-step)와 기대 완전자료 로그우도(expected complete-data log-likelihood)를 최대화하도록 모델 파라미터를 갱신하는 단계(M-step)를 번갈아 수행한다.

- log 안에 sigma가 있으면 계산이 어려움.
- EM 알고리즘은 GMM에만 사용되는 것은아니고 매우 다양하고 유용하게 사용됨. → 조금 어려움.

- E-step에서는 현재 **모델 파라미터를 고정된 것으로 간주**하고, 각 데이터 포인트 $\mathbf{x}$가 특정 가우시안 성분 $k$에서 생성되었을 확률을 추정한다.
- 이 확률을 responsibility라고 하며, $\gamma(z_k)$로 나타낸다.
- 형식적으로, $\gamma(z_k)$는 데이터 포인트 $\mathbf{x}$가 $k$번째 성분에서 생성되었을 조건부확률이다.  

$$  
\gamma(z_k) =  
p(z_k=1\mid \mathbf{x}) =  
\frac{p(z_k=1)p(\mathbf{x}\mid z_k=1)}{\sum_{j=1}^{K}p(z_j=1)p(\mathbf{x}\mid z_j=1)} =  
\frac{\pi_k\mathcal{N}(\mathbf{x}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)}{\sum_{j=1}^{K}\pi_j\mathcal{N}(\mathbf{x}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)}  
$$

- 따라서 여기서 $\gamma(z_k)$는 성분 $k$가 데이터 포인트 $\mathbf{x}$를 설명하는 데 책임을 가지는 정도를 나타낸다.

- M-step에서는 **E-step에서 계산된 responsibility를 고정된 것으로 간주**하고, 이에 따라 Gaussian mixture model의 파라미터, 즉 평균(mean), 공분산(covariance), mixing coefficient를 갱신한다.
- 다음을 다시 떠올려 보자.

$$  
\ln p(\mathbf{X}\mid \boldsymbol{\pi},\boldsymbol{\mu},\boldsymbol{\Sigma})=  
\sum_{n=1}^{N}  
\ln  
\sum_{k=1}^{K}  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
$$

- 먼저 로그우도(log-likelihood)를 $k$번째 가우시안 성분의 평균 $\boldsymbol{\mu}_k$에 대해 미분하고 이를 0으로 두어, $\boldsymbol{\mu}_k$의 최대우도추정량(maximum likelihood estimate)을 유도한다.
- 앞서 논의했듯이, 로그 내부의 합 때문에 이 로그우도를 직접 최대화하는 것은 어렵다.
- EM은 E-step에서 얻은 고정된 responsibility를 사용하여 이러한 문제를 피한다.

- 다음 미분 규칙을 떠올려 보자.

$$  
\frac{d}{dx}\ln f(x)  =  
\frac{1}{f(x)}\frac{d}{dx}f(x)  
$$

- 따라서 로그우도를 $\boldsymbol{\mu}_k$에 대해 미분하면 다음과 같다.
 
$$  
\frac{\partial}{\partial \boldsymbol{\mu}_k}  
\ln p(\mathbf{X}\mid\boldsymbol{\pi},\boldsymbol{\mu},\boldsymbol{\Sigma}) =  
\sum_{n=1}^{N}  
\frac{1}{  
\sum_{j=1}^{K}\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
\frac{\partial}{\partial \boldsymbol{\mu}_k}  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
$$


- 가우시안 확률밀도함수(Gaussian probability density function)는 다음과 같다.

$$  
\mathcal{N}(\mathbf{x}^{(n)}\mid \boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k) =  
\frac{1}{  
(2\pi)^{D/2}|\boldsymbol{\Sigma}_k|^{1/2}  
}  
\exp\left(  
-\frac{1}{2}  
(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)^T  
\boldsymbol{\Sigma}_k^{-1}  
(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)  
\right)  
$$

- 또한 다음 미분 공식을 기억하자.
  
$$  
\frac{d}{dx}e^{f(x)}  =  
e^{f(x)}f'(x)  
$$

- 따라서,  
$$  
\frac{\partial}{\partial \boldsymbol{\mu}_k}  
\left(  
\pi_k  
\mathcal{N}(\mathbf{x}^{(n)}\mid \boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
\right)  
=  
\pi_k  
\left(  
\mathcal{N}(\mathbf{x}^{(n)}\mid \boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
\cdot  
\boldsymbol{\Sigma}_k^{-1}  
(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)  
\right)  
$$

- 모두 종합하면 다음과 같다.  
$$  
\frac{\partial}{\partial \boldsymbol{\mu}_k}  
\ln p(\mathbf{X}\mid\boldsymbol{\pi},\boldsymbol{\mu},\boldsymbol{\Sigma})  
=  
\sum_{n=1}^{N}  
\frac{  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
\boldsymbol{\Sigma}_k^{-1}  
(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)  
=0  
$$

- 데이터 포인트 $\mathbf{x}^{(n)}$를 성분 $k$가 얼마나 설명하는지를 나타내는 responsibility의 정의를 다시 떠올리면,  
$$  
\gamma(z_{nk})  
=  
\frac{  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
$$

- 따라서 식을 다음과 같이 다시 쓸 수 있다.  
$$  
\sum_{n=1}^{N}  
\gamma(z_{nk})  
\boldsymbol{\Sigma}_k^{-1}  
(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)  
=0  
$$
- 이 식의 양변에 $\boldsymbol{\Sigma}_k$를 곱하고 항을 정리하면, 평균에 대한 갱신식을 얻는다.  
$$  
\boldsymbol{\mu}_k  
=  
\frac{1}{N_k}  
\sum_{n=1}^{N}  
\gamma(z_{nk})\mathbf{x}^{(n)},  
\quad  
N_k  
=  
\sum_{n=1}^{N}  
\gamma(z_{nk})  
$$

- 공분산 행렬 $\boldsymbol{\Sigma}_k$도 유사하게 갱신되며, 새로운 평균으로부터 데이터 포인트들이 얼마나 떨어져 있는지를 가중 편차(weighted deviation)로 반영한다.  
$$  
\boldsymbol{\Sigma}_k  
=  
\frac{1}{N_k}  
\sum_{n=1}^{N}  
\gamma(z_{nk})  
(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)  
(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)^T  
$$
- 마지막으로, mixing coefficient $\pi_k$에 대해  $\ln p(\mathbf{X}\mid\boldsymbol{\pi},\boldsymbol{\mu},\boldsymbol{\Sigma})$ 를 최대화한다.
- 여기서는 mixing coefficient들의 합이 1이 되어야 한다는 제약 조건  $\sum_{k=1}^{K}\pi_k=1$을 고려해야 한다.

- 이는 라그랑주 승수(Lagrange multiplier) $\lambda$를 사용하여 다음 quantity를 최대화함으로써 해결할 수 있다.  
$$  
L  
=  
\ln p(\mathbf{X}\mid\boldsymbol{\pi},\boldsymbol{\mu},\boldsymbol{\Sigma})


\lambda  
\left(  
\sum_{k=1}^{K}\pi_k-1  
\right)  
$$

- 다음으로, 이 라그랑지안(Lagrangian)을 $\pi_k$에 대해 미분하면 다음을 얻는다.  
$$  
\frac{\partial L}{\partial \pi_k}  
=  
\sum_{n=1}^{N}  
\frac{  
\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
+\lambda  
=0  
$$

- 이제 양변에 $\pi_k$를 곱하고 $k$에 대해 합을 취하면 다음과 같다.  
$$  
\sum_{k=1}^{K}  
\sum_{n=1}^{N}  
\frac{  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}


\lambda  
\sum_{k=1}^{K}\pi_k  
=0  
$$

- 제약 조건  
$$  
\sum_{k=1}^{K}\pi_k=1  
$$  
에 의해 다음을 얻는다.  
$$  
\sum_{n=1}^{N}  
\sum_{k=1}^{K}  
\frac{  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}


\lambda  
=0  
$$

- 각 고정된 데이터 포인트 $\mathbf{x}^{(n)}$에 대해, $k$에 대한 내부 합은 다음과 같다는 점에 주목하자.  
$$  
\sum_{k=1}^{K}  
\frac{  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
=1  
$$

- 이는 $k$에 대해 합한 분자가 정확히 분모와 같기 때문이다.
- 따라서 $n$과 $k$에 대한 이중합은 다음과 같이 줄어든다.  
$$  
\sum_{n=1}^{N}1=N  
$$

- 따라서 다음을 얻는다.  
$$  
N+\lambda=0  
$$

- 즉, $\lambda=-N$ 이다.
- 이제 이 값을 사용하여 원래 식에서 $\lambda$를 제거할 수 있다.  
$$  
\frac{\partial L}{\partial \pi_k}  
=  
\sum_{n=1}^{N}  
\frac{  
\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
+\lambda  
$$  
$$  
=  
\sum_{n=1}^{N}  
\frac{  
\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
-N  
=0  
$$

- 이제 이 식에 $\pi_k$를 곱하면 다음을 얻는다.  
$$  
\sum_{n=1}^{N}  
\frac{  
\pi_k\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k)  
}{  
\sum_{j=1}^{K}  
\pi_j\mathcal{N}(\mathbf{x}^{(n)}\mid\boldsymbol{\mu}_j,\boldsymbol{\Sigma}_j)  
}  
-\pi_kN  
=0  
$$

- 이는 mixing coefficient $\pi_k$에 대한 최종 식으로 이어진다.  
$$  
\pi_k  
=  
\frac{N_k}{N}  
$$  
여기서  
$$  
N_k  
=  
\sum_{n=1}^{N}  
\gamma(z_{nk})  
$$  
이다.

- 요약하면, EM 알고리즘은 두 단계를 번갈아 수행한다.    
- E-step에서는 현재 파라미터 추정값을 사용하여 responsibility, 즉 각 데이터 포인트가 각 가우시안 성분에서 생성되었을 사후확률(posterior probability)을 계산한다.    
- M-step에서는 이러한 responsibility를 기반으로 기대 완전자료 로그우도(expected complete-data log-likelihood)를 최대화하여 모델 파라미터(평균, 공분산 행렬, mixing coefficient)를 갱신한다.    
- 이 두 단계는 수렴(convergence)할 때까지 반복된다.    
- 이처럼 문제를 반복적(iterative) 방식으로 재구성함으로써, EM은 로그 내부의 합(log of a sum)을 직접 최대화하는 문제를 피하고, 대신 각 단계에서 닫힌형태(closed-form)의 갱신식을 제공한다.

- 다음은 Gaussian mixture model(GMM)을 위한 EM 알고리즘의 동작 과정을 보여주는 그림이다.

- 다음은 Gaussian mixture model(GMM)의 예시이다.    
- 그림에서 각 색상은 서로 다른 가우시안 성분(Gaussian component)을 나타내며, EM 알고리즘이 데이터 포인트에 대해 soft assignment를 수행하는 과정을 시각적으로 보여준다.
- 그림 9.5는 Figure 2.23에 나타난 3개의 가우시안 혼합(mixture of 3 Gaussians)으로부터 생성된 500개의 데이터 포인트 예시를 보여준다.
- (a)는 결합 분포  $p(\mathbf{z},\mathbf{x})$로부터 샘플링한 데이터이며, 세 개의 성분은 빨강(red), 초록(green), 파랑(blue)으로 표시된다.
- (b)는 주변 분포(marginal distribution)  $p(\mathbf{x})$ 로부터 얻은 대응 샘플을 보여주며, 이는 단순히 $z$ 값을 무시하고 $x$ 값만 표시한 것이다.
- (a)의 데이터셋은 complete 데이터라고 하며, (b)의 데이터셋은 incomplete 데이터라고 한다.
- (c)에서는 동일한 샘플을 색으로 표현하되, 각 데이터 포인트 $\mathbf{x}_n$에 대해 responsibility  $\gamma(z_{nk})$  의 값을 사용한다.
- 즉, 각 포인트의 색은  $\gamma(z_{nk}),\quad k=1,2,3$ 에 비례하는 빨강, 파랑, 초록 잉크의 혼합 비율로 결정된다.

### Hierarchical Clustering
- **계층적 클러스터링(hierarchical clustering)** 은 클러스터의 계층 구조(hierarchy)를 구축하는 것을 목표로 하는 클러스터 분석 방법이다.    
- 이 방법은 덴드로그램(dendrogram)이라 불리는 클러스터 트리(tree of clusters)를 구성하며, 이는 서로 다른 수준의 세분화(granularity)에서 데이터의 중첩된 그룹 구조(nested grouping)를 나타낸다.
- 이런 계층 구조를 덴드로그램(dendrogram)이라고도 함.

- 고정된 클러스터 개수 **$K$를 직접 선택하는 대신, 계층적 클러스터링은 클러스터를 점진적으로(progressively) 구축**해 나간다.    
- 최종 분할(partition)을 선택하기 전에 전체 계층 구조(hierarchy)가 먼저 구성되므로, 생성된 구조를 분석한 뒤 클러스터 개수를 결정할 수 있다.    
- 이러한 유연성 때문에 계층적 클러스터링은 적절한 클러스터 개수를 사전에 알 수 없는 탐색적 데이터 분석(exploratory data analysis)에 특히 적합하다.

- K가 하이퍼파라미터가 아니기 때문에 직접 설정 할 필요가 없음.

- 계층적 클러스터링(hierarchical clustering) 방법은 크게 **응집형(agglomerative)과 분할형(divisive)의 두 가지 유형**으로 나뉜다.    
- 응집형 클러스터링(agglomerative clustering)은 bottom-up 방식으로 동작한다.    
- 처음에는 각 데이터 포인트를 하나의 개별 클러스터로 시작하고, 이후 가장 유사한 클러스터들을 반복적으로 병합하며, 특정 종료 조건(stopping criterion)이 만족될 때까지 이를 계속한다. 
- 이 방법은 단순성 때문에 더 널리 사용된다.    
- 분할형 클러스터링(divisive clustering)은 top-down 방식으로 동작한다.    
- 처음에는 모든 데이터 포인트를 하나의 클러스터로 시작한 뒤, 이를 재귀적으로(recursively) 더 작은 클러스터들로 분할한다.
- 보통은 agglomerative clustering bottom-up 방식을 많이 사용함.

- 어떤 클러스터를 병합해야 하는지(응집형 클러스터링) 또는 분할해야 하는지(분할형 클러스터링)를 결정하려면, 두 데이터 그룹이 얼마나 다른지를 측정하는 방법이 필요하다.    
- 계층적 클러스터링에서는 이를 두 단계로 수행한다.    
- 1. 개별 데이터 포인트 사이의 거리 측정 방법(distance measure)을 선택한다(예: 유클리드 거리).        
- 2. **linkage rule**을 선택한다. 이는 각 데이터 포인트 사이의 거리를 이용하여 두 클러스터 사이의 거리를 어떻게 측정할지를 정의한다.        
- **거리 측정 방법(distance measure)은 어떤 개별 데이터 포인트들이 서로 유사한지를 결정하고, linkage rule은 전체 클러스터들을 어떻게 비교할지를 결정**한다.

- 두 관측값 집합 $A$와 $B$, 그리고 거리 함수 $d$에 대해 자주 사용되는 linkage criterion은 다음과 같다.
    

|Name|Formula|
|---|---|
|Complete-linkage clustering|$\max_{a\in A,; b\in B} d(a,b)$|
|Single-linkage clustering|$\min_{a\in A,; b\in B} d(a,b)$|
|Unweighted average linkage clustering (UPGMA)|$\frac{1}{|
|Centroid linkage clustering (UPGMC)|$\|\mu_A-\mu_B\|^2$|
|Ward linkage|$\frac{|

- 예를 들어, Ward 방법(Ward’s method)은 **클러스터 내부 분산(within-cluster variance)의 증가를 최소화**하는 방향으로 클러스터를 병합한다.

- 클러스터 내부 제곱합(within-cluster sum of squares)을 다음과 같이 정의한다.  
$$  
W(C)=\sum_{\mathbf{x}\in C}|\mathbf{x}-\boldsymbol{\mu}_C|^2,  
\quad  
\boldsymbol{\mu}_C=\frac{1}{|C|}\sum_{\mathbf{x}\in C}\mathbf{x}  
$$

- 여기서 $|C|$는 클러스터 $C$에 속한 데이터 포인트의 개수를 나타낸다.
- $C_A$와 $C_B$를 병합할 때, Ward 방법은 다음 값을 최소화하는 병합을 선택한다.  
$$  
\Delta  
=  
W(C_A\cup C_B)-W(C_A)-W(C_B)  
$$

- 이는 다음과 같이 단순화할 수 있다(증명은 생략).  
$$  
\Delta  
=  
\frac{|C_A||C_B|}{|C_A|+|C_B|}  
|\boldsymbol{\mu}_{C_A}-\boldsymbol{\mu}_{C_B}|^2  
$$

- 따라서 Ward의 linkage distance는 다음과 같다.  
$$  
D_{\mathrm{Ward}}(C_A,C_B)  
=  
\frac{|C_A||C_B|}{|C_A|+|C_B|}  
|\boldsymbol{\mu}_{C_A}-\boldsymbol{\mu}_{C_B}|^2  
$$

- 서로 다른 linkage 방법을 선택하면, 동일한 데이터셋에 대해서도 서로 다른 클러스터링 결과가 나타날 수 있다.
- 시각화 용으로도 많이 사용되게 됨.

- 요약하면, 계층적 클러스터링(hierarchical clustering)은 linkage criterion에 따라 클러스터들을 반복적으로 병합(또는 분할)하면서 중첩된(nested) **클러스터 구조를 구축하는 비모수적(non-parametric), 유사성 기반(similarity-based) 방법**이다.    
- 계층적 클러스터링은 클러스터 개수를 사전에 알 수 없는 경우와, 단일 수준의 세분화(granularity)보다 데이터의 다중 스케일 구조(multi-scale structure)를 탐색하고자 할 때 특히 유용하다.




## Comment

EM알고리즘 공부 필요!!
