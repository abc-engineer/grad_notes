2026-05-26 08:20
## 9강 Dimension

디멘젼 - mainfold 러닝- 뉴런넷 수업 후 기말고사
- 차원축소
	- 지도학습 전에 효과적인 전처리로 사용
	- 데이터의 리뷰용으로도 효과 적임.


### Dimension Reduction
- 차원 축소는 데이터의 본질적인 구조를 보존하면서 고차원 공간의 데이터를 저차원 공간으로 변환하며, 이상적으로는 데이터의 내재 차원을 반영한다.
- 예를 들어, 3차원 공간의 데이터 점들이 대부분 하나의 평면 위에 놓일 수 있다(아래 그림 참조). 세 개의 좌표로 표현되지만, 그 underlying structure는 본질적으로 2차원이다.    
- 차원 축소는 중복 정보를 제거하면서 이러한 더 단순한 구조를 포착한다.

- 우리가 다루는 데이터는 매우 고차원 데이터임.
- 텍스트나 이미지등도 간단해 보여도 차원 개수가 많음
- 차원이 높으면 한번에 파악하고 처리하기 어려움.
- 불필요한 디멘젼은 없애고 처리하면 이점이 많음

- 고차원 공간에서 작업하는 것은 여러 이유로 바람직하지 않을 수 있다. 계산 비용이 커지고, 많은 특징들이 불필요하거나 잡음을 포함할 수 있으며, 차원의 저주로 인해 데이터가 희소해진다.    
- 차원의 저주(curse of dimensionality)란 **데이터셋의 차원(또는 특징) 수가 증가할수록 데이터가 점점 더 희소**해져, 학습, 추정, 일반화가 훨씬 어려워지고 이를 해결하기 위해 기하급수적으로 더 많은 데이터가 필요해지는 현상을 의미한다.


- high-dimesional 데이터를 바로 다루면 비효율이 증가함.
- 대표적으로 curse of dimensionality 문제가 발생 할 수 있음. → 일반화를 방해 하는 요소가 됨.
- 1차원은 좀더 dense, 2차원은 sparse 3차원은 더 sparse → 공간은 큰데 그 공간에 데이터는 적어서 비어있는 것들많게 됨.
- sparse data로 학습되면 일반화 성능이 떨어짐.

- 차원 축소의 핵심 과제 중 하나는 원래 공간에서 저차원 공간으로의 적절한 projection을 찾는 것이다.   
- 서로 다른 방법들은 informative projection을 정의하는 기준과 원리에 따라 달라진다.    
- projection의 선택은 목적에 따라 결정되며, 예를 들어 클래스 분리도(class separability) 보존, 분산 최대화(maximizing variance), 또는 통계적으로 독립적인 성분(statistically independent components) 식별 등이 있다.


- 차원 축소에서 중요한 것은 어떤 차원으로 줄일 것인지에 대한 고민 임.
- 원 데이터를 잘 보존하면서 차원을 줄이는 방향을 찾는것이 포인트

- 예를 들어, 우리는 이전에 Linear Discriminant Analysis(LDA)를 다루었는데, 이는 클래스 분리도(class separability)를 최대화하는 projection을 찾는 지도 학습 기반 차원 축소 기법이다.    
- 반면, 이 장에서는 클래스 라벨이 주어지지 않는 비지도 학습(unsupervised learning) 맥락에서의 차원 축소에 초점을 맞춘다.    
- 대표적인 접근 방법으로는 Principal Component Analysis(PCA)와 Independent Component Analysis(ICA)가 있다.

- LDA는 지도학습 기반임. 
	- 분리도를 최대화하는 방향으로 차원을 직교하여 축소함.
- PCA는 비지도 학습
	- 레이블 정보 없음
	- 클래스를 보고 데이터를 보존하는 방향으로 축소소

### Principal Component Analysis
- 비지도 차원 축소에서 가장 중요하고 널리 사용되는 기법 중 하나는 분산(variance)을 보존하는 아이디어이며, 이는 Principal Component Analysis(PCA)로 이어진다.

- data가 2차원에 놓여 있다고 할때 어떻게 축소하면 원래 데이터간 차이가 가장 유지가 될까?
- PCA의 핵심은 데이터의 분산을 가장 잘 보존하는게 PCA의 핵심심

- PCA는 동일한 알고리즘으로 이어지는 두 가지 동등한 관점으로 이해할 수 있다.    
- 1. PCA는 projected data의 분산이 최대화되도록 데이터를 저차원 선형 공간으로 직교 투영(orthogonal projection)하는 방법으로 정의할 수 있다.        
- 2. 동등하게, 데이터 점들과 그 projection 사이의 평균 제곱 거리(mean squared distance)로 정의되는 평균 projection cost를 최소화하는 선형 projection으로 정의할 수도 있다.


- 데이터를 직교 투영 후 분산이 최대화 되는 방법, 데이터를 투영했을때 실제 값과 투영된 값의 차이가 가장 작도록 하는 2가지 방법이 있음.
- 두가지 방법의 결과는 같고 풀이와 철학의 차이가 있을뿐임.
- 첫번째 방법이 조금 더 직관적이라 쉬움.

### Maximum Variance Formulation (분산을 최대화 하는 방법)
- 관측값 데이터셋 $\mathbf{x}^{(n)}$를 생각하자. 여기서 $n = 1, \dots, N$이며, 각 $\mathbf{x}^{(n)}$는 차원 $D$를 가지는 Euclidean variable이다.    
- 우리의 목표는 projected data의 분산을 최대화하면서 데이터를 차원 $M < D$인 공간으로 projection하는 것이다.    
- 현재는 $M$이 주어졌다고 가정한다. 이후에는 데이터로부터 적절한 $M$ 값을 결정하는 방법들을 논의할 것이다.    
- [eigenvector 설명 자료](https://wiki.pathmind.com/eigenvector?utm_source=chatgpt.com)

- 분산을 최대화 하는 방법임.
-  $\mathbf{x}^{(n)}$은 벡터 임.
- D 차원을 M 차원으로 축소
- 그때 분산이 최대화 되도록 축소


- 우선, 1차원 공간으로의 projection($M = 1$)을 고려하자.    
- 우리는 이 공간의 방향을 $D$차원 벡터 $\mathbf{u}_1$로 정의할 수 있으며, 편의를 위해 $\mathbf{u}_1^T \mathbf{u}_1 = 1$을 만족하는 단위 벡터(unit vector)로 선택한다(중요한 것은 $\mathbf{u}_1$의 크기가 아니라 그것이 정의하는 방향이다).    
- 그러면 각 데이터 점 $\mathbf{x}^{(n)}$는 스칼라 값 $\mathbf{u}_1^T \mathbf{x}^{(n)}$로 projection된다.

- 디멘전의 방향에 관심이 있음.
- 수식을 풀때 투영 벡터는 크기가 1인 유닛 벡터로 제한함.(condition)
- 그러기 위해 $u$를 찾아야 함.

- projected data의 평균은 $\mathbf{u}_1^T \bar{\mathbf{x}}$이며, 여기서 $\bar{\mathbf{x}}$는 다음과 같이 정의되는 sample set mean이다.
  
$$  
\bar{\mathbf{x}} = \frac{1}{N} \sum_{n=1}^{N} \mathbf{x}^{(n)}  
$$

- projected data의 분산은 다음과 같이 주어지며, 여기서 $\mathbf{S}$는 데이터의 covariance matrix이다.  

$$  
\begin{align}
\frac{1}{N} \sum_{n=1}^{N} \left( \mathbf{u}_1^T \mathbf{x}^{(n)} - \mathbf{u}_1^T \bar{\mathbf{x}} \right)^2  
&= \frac{1}{N} \sum_{n=1}^{N} \left( \mathbf{u}_1^T \left( \mathbf{x}^{(n)} - \bar{\mathbf{x}} \right) \right)^2  \\  
&= \frac{1}{N} \sum_{n=1}^{N} \mathbf{u}_1^T \left( \mathbf{x}^{(n)} - \bar{\mathbf{x}} \right)\left( \mathbf{x}^{(n)} - \bar{\mathbf{x}} \right)^T \mathbf{u}_1 \\ 
&= \mathbf{u}_1^T \mathbf{S} \mathbf{u}_1  
\end{align}
$$

- covariance matrix $\mathbf{S}$는 다음과 같이 정의된다.  

$$  
\mathbf{S} = \frac{1}{N} \sum_{n=1}^{N} \left( \mathbf{x}^{(n)} - \bar{\mathbf{x}} \right)\left( \mathbf{x}^{(n)} - \bar{\mathbf{x}} \right)^T  
$$


- 투영된 데이터의 분산을 계산해야 함. S는 오리지널 데이터의 분산임.


- 이제 projected variance $\mathbf{u}_1^T \mathbf{S} \mathbf{u}_1$을 $\mathbf{u}_1$에 대해 최대화한다.
- 그러나 이 최대화는 제약 조건이 필요하다. 그렇지 않으면 단순히 $\mathbf{u}_1$을 스케일링하여 분산을 임의로 크게 만들 수 있기 때문이다.
- 앞서 간단히 언급했듯이, trivial solution을 피하기 위해 normalization constraint $\mathbf{u}_1^T \mathbf{u}_1 = 1$을 부과하며, 이는 $\mathbf{u}_1$을 unit vector로 제한한다.
- 이 제약 조건을 적용하기 위해 Lagrange multiplier $\lambda_1$을 도입하고, 다음의 $\mathcal{L}$에 대해 unconstrained maximization을 수행한다.  

$$  
\mathcal{L} = \mathbf{u}_1^T \mathbf{S} \mathbf{u}_1 + \lambda_1 \left(1 - \mathbf{u}_1^T \mathbf{u}_1\right)  
$$

- 최적화는 ML과 동일
- 분산을 최대화 하는게 목표
- → 분산을 최대화 하는 u1을 찾아야 함.
- $\mathbf{u}_1^T \mathbf{u}_1 = 1$ 같이 이런 제한 조건이 있을때 최적화는 라그랑주를 자주 사용하게 됨.
- 별건 아니고 원래의 목적함수를 계산하기 쉽게 라그랑주 멀티플라이어 $\lambda_1 $을 도입해서 새로운 목적함수를 만들어서 계산하는 행동임.



- $\mathbf{u}_1$에 대한 미분을 0으로 두면, 다음 조건에서 stationary point가 존재함을 알 수 있다.  

$$  
\frac{\partial \mathcal{L}}{\partial \mathbf{u}_1}  =  
2 \mathbf{S} \mathbf{u}_1- 2 \lambda_1 \mathbf{u}_1
= 0  
$$  

$$  
\mathbf{S} \mathbf{u}_1=
\lambda_1 \mathbf{u}_1  
$$

- 이는 $\mathbf{u}_1$이 $\mathbf{S}$의 eigenvector여야 함을 의미한다.
- 이제 양변의 왼쪽에 $\mathbf{u}_1^T$를 곱하고 $\mathbf{u}_1^T \mathbf{u}_1 = 1$을 이용하면, projected variance는 다음과 같이 주어진다.  

$$  
\mathbf{u}_1^T \mathbf{S} \mathbf{u}_1  = \lambda_1  
$$


- 선형대수에서 매우 익숙한 수식임.
- 아이겐 밸류로 계산 됨
- PCA를 이해하려면 eigenvector(아이겐 벡터)와 eigenvalue(아이겐 밸류)에 대한 이해가 필요하긴 함.


- S의 아이겐 벡터가 무엇을 의미하는지 공부할 것 !!!


- 이는 $\mathbf{u}_1$을 가장 큰 eigenvalue $\lambda_1$에 대응하는 eigenvector로 설정할 때 variance가 최대가 됨을 의미한다.    
- 이 eigenvector를 first principal component라고 한다.

- 다차원의 경우 첫번째 주성분을 찾고 두번째 주성분도 찾아야 함.



- first principal component를 찾은 후에는 가능한 한 많은 variance를 포착하는 추가 방향들을 찾고자 한다.    
- 그러나 아무런 제한을 부과하지 않으면, 다음 방향은 다시 첫 번째 방향과 정렬되어 동일한 해를 줄 수 있다.    
- 각 새로운 component가 새로운 정보를 포착하도록 하기 위해, 이전에 선택된 방향들과 orthogonal직교하도록 요구한다.

- 첫번째 component와 두번째 component가 직각(직교가 되도록) 두번째  component를 찾아야 함.
- 그냥 다 되는 것은 아니고 데이터가 대칭형일때 이렇게 직교 되도록 데이터를 봅을 수 있음. (아래 슬라이드 설명)

- **이러한 직교성(orthogonality)은 임의로 imposed된 것이 아니라, 문제의 수학적 구조로부터 자연스럽게 나타난다.**    
- Lagrange multiplier를 사용하여 constrained variance maximization 문제를 풀면 covariance matrix $\mathbf{S}$에 대한 eigenvalue problem을 얻게 된다.    
- 그 해는 $\mathbf{S}$의 eigenvector들이며, $\mathbf{S}$와 같은 symmetric matrix의 중요한 성질 중 하나는 서로 다른 eigenvalue에 대응하는 eigenvector들이 서로 직교한다는 것이다.

- eigenvalue는 분산값임. 
- d개의 차원에서는 d개의 eigenvalue가 나옴.

- 일반적인 $M$차원 projection space의 경우, 최적의 선형 projection은 covariance matrix $\mathbf{S}$의 eigenvector $\mathbf{u}_1, \dots, \mathbf{u}_M$으로 주어지며, 이들은 가장 큰 $M$개의 eigenvalue $\lambda_1, \dots, \lambda_M$에 대응한다.    
- 이러한 eigenvector들이 principal component를 정의하며, 대응되는 eigenvalue들은 각 방향이 포착하는 variance의 양을 나타낸다.

### Minimum Error Formulation
- 이제 projection error 최소화에 기반한 PCA의 대안적 formulation을 논의한다.
- 첫번째 방법은 투영후 분산을 최대화
- 두번째 방법은 투영 후 residuals의 최소화

- 첫번째 방법보다 조금 더 복잡함.
- 철학은 다르지만 결과는 첫번째와 같음.

- 이를 위해, 다음 조건을 만족하는 $D$차원 basis vector들의 complete orthonormal set $\mathbf{u}_i$를 도입한다. 여기서 $i = 1, \dots, D$이다.  

$$  
\mathbf{u}_i^T \mathbf{u}_j = \delta_{ij}  
$$ 

$$  
\delta_{ij} =  \begin{cases}  
1 & \text{if } i=j \\  
0 & \text{otherwise}  
\end{cases}  
$$
- orthonormality란 벡터들이 서로 직교(mutually orthogonal)하여 서로 수직이며, 동시에 각 벡터의 길이가 1인 것을 의미한다.


- $D$차원 basis vector를 정의 해야 함.
- mutually orthogonal: 서로 수직이고 벡터의 길이는 1

- 이 basis는 complete하므로, 각 데이터 점은 basis vector들의 선형 결합으로 표현될 수 있으며, 계수 $\alpha_i^{(n)}$는 데이터 점마다 달라진다.  

$$  
\mathbf{x}^{(n)}  =  \sum_{i=1}^{D} \alpha_i^{(n)} \mathbf{u}_i  
$$
- 개념적으로 이는 단순한 좌표계의 회전에 해당한다. 즉, 데이터 점을 기존 축 대신 $\mathbf{u}_i$가 정의하는 새로운 축들에 대해 표현하는 것이다.


- 이 수식은 차원 축소가 된것이 아니고 차원을 재 정의 함.

- 계수 $\alpha_i^{(n)}$를 구하기 위해, 데이터 점 $\mathbf{x}^{(n)}$를 각 basis vector $\mathbf{u}_i$에 dot product를 사용하여 projection한다.
- $\mathbf{x}^{(n)}$의 전개식을 대입하면 다음을 얻는다.  

$$  
\mathbf{u}_i^T \mathbf{x}^{(n)}  =  \mathbf{u}_i^T  
\sum_{j=1}^{D}  
\alpha_j^{(n)} \mathbf{u}_j  =  \sum_{j=1}^{D}  
\alpha_j^{(n)}  
\mathbf{u}_i^T \mathbf{u}_j  
$$

- $\mathbf{u}_i^T \mathbf{u}_j = 0$ when $i \neq j$이고, $1$ when $i=j$이므로, 다음만 남게 된다.  

$$  
\alpha_i^{(n)} = \mathbf{u}_i^T \mathbf{x}^{(n)}  
$$

- 알파는 뮤와 엑스의 곲으로 표현 할 수 있음.

- 그러나 **우리의 목표는 데이터를 정확히 표현하는 것만이 아니라, 더 적은 차원을 사용하여 데이터를 근사하는 것**이다.
- 구체적으로, 데이터의 중요한 구조를 포착하는 차원 $M < D$의 저차원 공간을 찾고자 한다.
- 이를 위해 각 데이터 점 $\mathbf{x}^{(n)}$를 처음 $M$개의 basis vector에 대한 projection만 유지하여 다음과 같이 근사한다.  

$$  
\tilde{\mathbf{x}}^{(n)}  =  \sum_{i=1}^{M}  
z_i^{(n)} \mathbf{u}_i+\sum_{i=M+1}^{D}  
b_i \mathbf{u}_i  
$$
- 여기서 $z_i^{(n)}$는 저차원 subspace에서의 새로운 좌표이며, $b_i$는 나머지 차원들에 대해 모든 데이터 점에서 동일하게 유지되는 상수이다.


- 이 수식이 D개의 차원에서 M개의 차원을 남기는 수식.
- 1~M까지는 z를 곱해줌
- M+1~D까지는 같은 상수 b값을 곱해줌.

- 즉, $z_i^{(n)}$는 데이터 점마다 달라지며, 축소된 subspace 안에서 데이터 점들 사이의 의미 있는 차이를 포착한다.    
- 반면 $b_i$는 모든 데이터 점에 공통으로 적용되는 고정 상수이며, 더 이상 개별적인 variability를 모델링하지 않는 나머지 $D-M$개 방향의 기여를 나타낸다.

- 최적의 근사를 찾기 위해, 원래 데이터 점 $\mathbf{x}^{(n)}$와 그 근사값 $\tilde{\mathbf{x}}^{(n)}$ 사이의 평균 제곱 거리(mean squared distance)인 “distortion”을 최소화하고자 한다.
- 이 distortion은 $J$라는 양으로 표현되며, 우리의 목표는 $J$를 최소화하는 것이다.  

$$  
J  =  \frac{1}{N}  
\sum_{n=1}^{N}  
\left|  
\mathbf{x}^{(n)}-\tilde{\mathbf{x}}^{(n)}  
\right|^2  
$$
- 여기에는 $z_i^{(n)}$, $b_i$, 그리고 $\mathbf{u}_i$라는 세 종류의 parameter가 존재하지만, distortion measure $J$를 좌표 $z_i^{(n)}$, $b_i$, 그리고 basis vector $\mathbf{u}_i$에 대해 동시에 최소화하는 것은 문제를 직접 풀기 훨씬 어렵게 만든다.

- 대신, 우리는 문제를 두 단계로 나누어 과정을 단순화한다.
- 먼저 basis vector $\mathbf{u}_i$를 고정한 뒤, $J$를 최소화하는 최적의 좌표 $z_i^{(n)}$와 $b_i$를 구한다.
- 좌표들이 결정된 이후에는, basis vector들이 orthonormal 상태를 유지한다는 제약 아래에서 $\mathbf{u}_i$의 선택을 최적화한다.
- 즉, 먼저 좌표 $z_i^{(n)}$에 대해 $J$를 최소화한다.  

$$  
\frac{\partial J}{\partial z_i^{(n)}} = 0  
$$

- z, u, b 3가지 값을 찾아야 하고 그 값은 목적함수 J를 최소화 해야 함.
- 찾아야 하는 변수가 많아서 첫번째 방법 보다 어려움.
- 이런 다변수의 값을 찾을때는 2개값을 고정해서 각각 값을 구하는 방법을 사용 (지난 강의 참고)

- $J$를 $z_i^{(n)}$에 대해 미분한 뒤 0으로 두고, orthonormality 조건을 이용하면 다음과 같은 간단한 해를 얻는다(증명은 생략).  

$$  
z_i^{(n)} = (\mathbf{x}^{(n)})^T \mathbf{u}_i,  
\quad i = 1, \dots, M  
$$
- 마찬가지로, $J$를 $b_i$에 대해 미분하여 0으로 두면 다음을 얻는다.  

$$  
b_i =  
\bar{\mathbf{x}}^T \mathbf{u}_i,  
\quad i = M+1, \dots, D  
$$
- 여기서 $\bar{\mathbf{x}}$는 모든 데이터 점의 평균이다.

- 이 결과들을 다시 $\tilde{\mathbf{x}}^{(n)}$에 대입하면 다음을 얻는다.  

$$  
\tilde{\mathbf{x}}^{(n)} =  
\sum_{i=1}^{M}  
((\mathbf{x}^{(n)})^T\mathbf{u}_i )\mathbf{u}_i+\sum_{i=M+1}^{D}  
(\bar{\mathbf{x}}^T \mathbf{u}_i) \mathbf{u}_i  
$$

- 이제 reconstruction error $\mathbf{x}^{(n)} - \tilde{\mathbf{x}}^{(n)}$를 다시 살펴보면 다음과 같다.  

$$  
\mathbf{x}^{(n)}- \left(  
\sum_{i=1}^{M}  
\left(  
(\mathbf{x}^{(n)})^T\mathbf{u}_i  
\right)\mathbf{u}_i  +  
\sum_{i=M+1}^{D}  
\left(  
\bar{\mathbf{x}}^T\mathbf{u}_i
\right)\mathbf{u}_i  
\right)= \left(\mathbf{x}^{(n)} - \sum_{i=1}^{M}  
\left(  
(\mathbf{x}^{(n)})^T\mathbf{u}_i  
\right)\mathbf{u}_i  
\right)-\sum_{i=M+1}^{D}  
\left(  
\bar{\mathbf{x}}^T\mathbf{u}_i  
\right)\mathbf{u}_i  
$$

- $\mathbf{x}^{(n)}$ 자체는 complete orthonormal basis를 사용하여 정확하게 다음과 같이 전개될 수 있음을 기억하자.  

$$  
\mathbf{x}^{(n)}  =  \sum_{i=1}^{D}  
\mathbf{x}^{(n)T}\mathbf{u}_i \mathbf{u}_i  
$$

- 따라서 첫 번째 항의 $\mathbf{x}^{(n)}$를 다음과 같이 치환할 수 있다.  

$$  
\mathbf{x}^{(n)} - \tilde{\mathbf{x}}^{(n)}
= \left(  
\sum_{i=1}^{D}  
\left(  
(\mathbf{x}^{(n)})^T\mathbf{u}_i  
\right)\mathbf{u}_i- \sum_{i=1}^{M}  
\left(  
(\mathbf{x}^{(n)})^T\mathbf{u}_i  
\right)\mathbf{u}_i  
\right)-\sum_{i=M+1}^{D}  
\left(  
\bar{\mathbf{x}}^T\mathbf{u}_i  
\right)\mathbf{u}_i  
$$

$$
=\left(  
\sum_{i=1}^{D}  
\left(  
(\mathbf{x}^{(n)})^T\mathbf{u}_i  
\right)\mathbf{u}_i- \sum_{i=1}^{M}  
\left(  
(\mathbf{x}^{(n)})^T\mathbf{u}_i  
\right)\mathbf{u}_i  
\right)-\sum_{i=M+1}^{D}  
\left(  
\bar{\mathbf{x}}^T\mathbf{u}_i  
\right)\mathbf{u}_i 
$$
  
$$
= \sum_{i=M+1}^{D}  
\left(  
(\mathbf{x}^{(n)})^T\mathbf{u}_i  
\right)\mathbf{u}_i- \sum_{i=M+1}^{D}  
\left(  \bar{\mathbf{x}}^T\mathbf{u}_i  
\right)\mathbf{u}_i  
$$  

$$
= \sum_{i=M+1}^{D}  
\left(  (\mathbf{x}^{(n)})^T\mathbf{u}_i-\bar{\mathbf{x}}^T\mathbf{u}_i  
\right)\mathbf{u}_i  
$$

- 이제 전체 distortion을 정량화해보자.  

$$  
J  =  \frac{1}{N}  
\sum_{n=1}^{N}  
\left|  
\mathbf{x}^{(n)}- \tilde{\mathbf{x}}^{(n)}  
\right|^2  
$$  

$$
= \frac{1}{N}  
\sum_{n=1}^{N}  
\left|  
\sum_{i=M+1}^{D}  
\left(  (\mathbf{x}^{(n)})^T\mathbf{u}_i- \bar{\mathbf{x}}^T\mathbf{u}_i  
\right)\mathbf{u}_i  
\right|^2  
$$  

$$
= \frac{1}{N}  
\sum_{n=1}^{N}  
\sum_{i=M+1}^{D}  
\left(  (\mathbf{x}^{(n)})^T\mathbf{u}_i-\bar{\mathbf{x}}^T\mathbf{u}_i  
\right)^2  
$$

- basis vector $\mathbf{u}_i$들이 orthonormal이므로, 전체 합의 squared length는 각 coefficient 제곱의 합과 같아진다.

- 이 식은 다음과 같이 더 단순화된다:
  
$$  
J=\frac{1}{N}\sum_{n=1}^{N}\sum_{i=M+1}^{D}\left(u_i^T(x^{(n)}-\bar{x})\right)^2  
$$ 

$$  
=\frac{1}{N}\sum_{n=1}^{N}\sum_{i=M+1}^{D}\left(u_i^T(x^{(n)}-\bar{x})\right)\left(u_i^T(x^{(n)}-\bar{x})\right)  
$$  

$$  
=\frac{1}{N}\sum_{n=1}^{N}\sum_{i=M+1}^{D}u_i^T(x^{(n)}-\bar{x})(x^{(n)}-\bar{x})^Tu_i  
$$

- 이 식은 다음과 같이 쓸 수 있다:
- 
$$  
J=\frac{1}{N}\sum_{n=1}^{N}\sum_{i=M+1}^{D}u_i^T(x^{(n)}-\bar{x})(x^{(n)}-\bar{x})^Tu_i=\sum_{i=M+1}^{D}u_i^TSu_i,  
$$

- 여기서 $S$는 데이터의 공분산 행렬이다:
- 
$$  
S=\frac{1}{N}\sum_{n=1}^{N}(x^{(n)}-\bar{x})(x^{(n)}-\bar{x})^T.  
$$

- 이 결과가 PCA의 최대 분산(maximum variance) 공식과 유사함을 확인할 수 있다.

- 따라서 최적의 좌표가 결정되면, 다음 단계는 왜곡 척도 $J$를 최소화하는 최적의 기저 벡터 집합 ${u_i}$를 찾는 것이다.
- 이는 기저 벡터들이 직교정규 조건을 유지해야 하는 제약 최소화 문제로 이어진다.
- 
$$  
u_i^Tu_j=\delta_{ij}  
$$  
- 해는 다시 공분산 행렬의 고유값 문제를 풂으로써 얻어진다:
- 
$$  
Su_i=\lambda_i u_i  
$$

- 여기서 $\lambda_i$는 고유값(eigenvalue)이고, $u_i$는 이에 대응하는 고유벡터(eigenvector)이다.
- 따라서 $J$의 최소값은 가장 작은 $D-M$개의 고유값에 대응하는 고유벡터들을 선택하고, 동시에 가장 큰 고유값들에 대응하는 $M$개의 고유벡터를 보존함으로써 얻어진다.


### Applications of Principal Component Analysis
- PCA를 데이터 압축에 사용하는 예로 숫자(digits) 데이터셋을 고려할 수 있다.    
- 공분산 행렬의 각 고유벡터는 원래의 $D$차원 공간에 있는 벡터이므로, 고유벡터들을 데이터 포인트와 동일한 크기의 이미지로 표현할 수 있다.    
- 처음 다섯 개의 고유벡터와 대응하는 고유값은 아래 왼쪽 그림에 나타나 있다.    
- 또한 고유값 전체 스펙트럼을 큰 값부터 내림차순으로 정렬한 결과는 아래 오른쪽 그림에 나타나 있다.
- 평균 벡터 $\bar{x}$와 오프라인 숫자 데이터셋에 대한 첫 네 개의 PCA 고유벡터 $u_1,\ldots,u_4$, 그리고 이에 대응하는 고유값들이 함께 나타나 있다.

- PCA는 데이터를 압축할 수도 있고 저차원으로 보내 시각화 하기에도 좋음
- 오른쪽 그래프는 아이겐 차트라고 할 수 있고 M 값을 몇으로 하면 좋을지 판단 하는 근거로 사용 될 수 있음.


- PCA를 얼굴 이미지에 적용한 또 다른 예시는 eigenfaces(고유 얼굴)라고 알려진 결과를 만들어낸다.

- 구체적으로, 각 $D$차원 데이터 포인트 $x^{(n)}$는 $M$개의 주성분(principal component)에 투영(projection)함으로써 압축된다. 여기서 $M<D$이다.
- $i$번째 주성분 $u_i\in\mathbb{R}^D$에 대한 스칼라 투투영 계수는 다음과 같다:
- 
$$  
z_i^{(n)}=(x^{(n)}-\bar{x})^Tu_i  
$$
- 여기서 $\bar{x}\in\mathbb{R}^D$는 데이터셋의 평균(mean)이다. 즉, $z_i^{(n)}$는 단순히 $x^{(n)}$를 $i$번째 주성분 방향으로 표현한 좌표값이다.
- 전체 $M$차원 압축 표현은 다음과 같다:
- 
$$  
z^{(n)}=\left(z_1^{(n)},z_2^{(n)},\ldots,z_M^{(n)}\right)^T\in\mathbb{R}^M  
$$

- 원래 데이터 포인트의 근사값을 복원하기 위해서는 투영 과정을 반대로 수행한다:
- 
$$  
\hat{x}^{(n)}=\bar{x}+\sum_{i=1}^{M}z_i^{(n)}u_i  
$$
- 따라서 복원된 벡터 $\hat{x}^{(n)}$은 원래 데이터와 동일한 차원 $D$를 가지지만, 실제로는 $M$개의 성분 정보만 사용한다.
- $M$이 작을수록 압축 정도는 커지지만, 동시에 더 많은 정보가 손실된다.

### Independent Component Analysis
- 독립 성분 분석(Independent Component Analysis, ICA)은 다변량 신호를 통계적으로 서로 독립인 가산 성분들로 분리하는 계산 방법이다.    
- **ICA는 주로 source separation(원천 신호 분리)에 사용**되지만, 추정되는 독립 성분의 수를 원래 변수의 수보다 적게 설정하면 특징 추출(feature extraction) 및 차원 축소(dimensionality reduction)에도 적용할 수 있다.



- 교수님도 처음 ICA를 접했을때는 어려웠지만 컨셉만 이해하면 크게 어렵지도 않음
- ICA는 독립이 포인트, PCA는 주성분
- 관심없는 성분들은 지워버리면 됨.

- ICA의 중심 가정은 숨겨진 원천 신호(hidden sources)들이 통계적으로 서로 독립(statistically independent)이라는 것이다.    
- 통계적 독립성은 단순한 비상관성(uncorrelatedness)보다 더 강한 조건이다.    
- 두 변수가 **비상관이라는 것은 선형 관계가 없음을 의미**하지만, 여전히 다른 방식(예: 비선형 관계)으로는 서로 관련될 수 있다.    
- **반면 두 변수가 독립이라면, 한 변수의 값을 알더라도 다른 변수에 대한 어떠한 정보도 얻을 수 없다.**

- 독립과 상관관계가 없다는 다른 말임.

**독립(independence)** 이 더 강한 조건이고, **상관관계가 없음(uncorrelated)** 은 더 약한 조건입니다.

#### 1. 상관관계가 없다는 뜻

두 변수 X, Y의 **공분산이 0**이라는 뜻입니다.

$\operatorname{Cov}(X,Y)=0$

즉, **선형 관계가 없다**는 의미입니다.

예를 들어 X가 증가할 때 Y가 일정하게 증가하거나 감소하는 **직선형 경향**이 없으면 상관관계가 없다고 말할 수 있습니다.

#### 2. 독립이라는 뜻

X와 Y가 서로 아무런 확률적 영향을 주지 않는다는 뜻입니다.
즉, X를 알아도 Y의 분포가 변하지 않습니다.

$P(Y \mid X)=P(Y)$

또는 연속형 변수에서는

$f_{X,Y}(x,y)=f_X(x)f_Y(y)$

라고 표현합니다.





- PCA는 데이터를 직교(orthogonal) 성분들로 변환하며, 이를 통해 성분들이 서로 비상관(uncorrelated)임은 보장한다. 그러나 이것이 성분들이 완전히 독립(independent)임을 의미하지는 않는다.    
- 반면 ICA는 데이터를 통계적으로 독립인 성분들로 분리하는 데 초점을 두며, 성분들이 서로 직교할 필요는 없다.

- **ICA는 숨겨진 원천 신호들이 비가우시안(non-Gaussian)이라는 가정을 이용하여 독립 성분들을 분리한다.**    
- 가우시안 가정은 모델을 수학적으로 단순하게 만들기 때문에 자주 사용되지만, 실제 신호들은 종종 비가우시안 패턴을 보인다.

- ICA에서는 모든 소스는 가우시안이 아니다라는 가정에서 시작함.
	- 가우시안 분포를 따른다고 가정하면 분리가 어려움.
	- 가우시안은 합치면 다시 가우시안이 됨.

- 만약 잠재 원천(latent sources)들이 가우시안(Gaussian)이라면, 원래의 원천 신호를 식별하는 것은 어려워진다. 왜냐하면 가우시안 변수들의 선형 결합 역시 가우시안이기 때문이다.    
- 그 결과 서로 다른 혼합(mixture)들이 통계적으로 유사하게 보일 수 있으므로, 원천 신호들을 구별하기가 어려워진다.

- 초록색 분포가 2개의 가우시안을 합친 분포인데 이것만 보면 가우시안 2개를 합친건지 1개의 원래 가우시안 분포인지 알 수 없음.

- ICA의 대표적인 동기 부여 예시는 cocktail party problem(칵테일 파티 문제), 또는 blind source separation problem(맹목적 원천 분리 문제)이다.    
- 여러 사람이 한 방에서 동시에 말하고 있고, 서로 다른 위치에 놓인 여러 마이크가 각 음성들의 서로 다른 혼합 신호를 녹음한다고 가정하자.    
- 목표는 신호들이 어떤 방식으로 혼합되었는지 알지 못한 상태에서, 이 녹음들로부터 원래의 서로 독립인 음성 신호들을 복원하는 것이다.


- 여러 사람이 이야기 해도 사람들은 그렇게 헷갈리지 않고 잘 분리하고 이해 함.
- 이 원리를 컴퓨터적으로 한것이 ICA
- 2개의 마이크에 2명의 사람 소리가 녹음 되어도 ICA로 분리 해 낼 수 있음.

- 형식적으로, $d$차원 데이터 $x\in\mathbb{R}^d$가 $d$개의 서로 독립인 원천 신호 $s\in\mathbb{R}^d$의 선형 혼합(linear mixture)이라고 가정하자. 이 관계는 다음과 같이 표현된다:  

$$  
x=As  
$$

- 여기서 $A$는 알려지지 않은 $d\times d$ 혼합 행렬(mixing matrix)이고, $s$는 잠재 독립 원천(latent independent sources) 벡터이다.
- ICA의 목표는 관측된 혼합 신호 $x$로부터 $A$와 $s$를 모두 복원하는 것이다.
- 보다 구체적으로, $N$개의 관측값 ${x^{(n)}}_{n=1}^{N}$이 주어졌을 때, 다음을 만족하는 행렬 $W=A^{-1}$  
를 찾고자 한다. 여기서 $W$는 unmixing matrix라고 불린다.
- 그러면 원천 신호 $s$는 다음과 같이 복원할 수 있다:  

$$  
s=Wx  
$$

- ICA에서 핵심 가정은 원래의 원천 신호들이 반드시 비가우시안(non-Gaussian)이어야 한다는 것이다.
- 다시 말해, 원천 신호들이 가우시안이라면 서로 다른 원천 신호들의 혼합이 매우 유사하게 보일 수 있으므로, 이를 유일하게 분리하는 것이 불가능해진다. 반면 비가우시안 분포, 예를 들어 뾰족한 피크를 갖는 신호들은 혼합된 후에도 구별되는 특성을 유지하므로 ICA가 이를 분리할 수 있다.
- 수학적으로 원천 신호 $s$의 확률은 각 독립 원천 신호의 개별 확률들의 곱으로 모델링된다:  

$$  
p(s)=p(s_1,s_2,\ldots,s_d)=\prod_{i=1}^{d}p(s_i)  
$$
- 여기서 $p(s_i)$는 $i$번째 원천 신호의 확률 밀도이다.

- 각 확률이 독립이면 파이를 이용해서 각 확률을 곱해서 계산할 수 있음.

- ICA에서 우리의 목표는 독립 원천 신호를 복원할 수 있게 하는 unmixing matrix $W$를 추정하는 것이다.
- $W$를 추정하면 원천 신호는 다음과 같이 계산할 수 있다:  

$$  
s^{(n)}=Wx^{(n)}  
$$
- 여기서 $s^{(n)}$은 $n$번째 관측값에 대해 복원된 원천 신호를 나타낸다.
- $w_i^T$를 $W$의 $i$번째 행이라고 하면, 각 원천 신호 $s_i^{(n)}$은 다음과 같이 표현된다:  

$$  
s_i^{(n)}=w_i^Tx^{(n)}  
$$
- 어려운 점은 우리가 혼합된 데이터 $x$만 관측한다는 것이다. 즉, 원래의 혼합 행렬이나 실제 원천 신호를 알지 못하므로, 데이터로부터 직접 $W$를 추정해야 한다.

- $W$를 추정하기 위해 우리는 최대우도추정(maximum likelihood estimation)을 사용한다. 즉, 관측 데이터의 likelihood $p(x)$를 정의하고, 이를 최대화하는 매개변수 $W$를 찾고자 한다.
- 우리의 모델은 관측 신호 $x$가 통계적으로 독립인 원천 신호들의 선형 혼합이며, $s=Wx$ 라고 가정하므로, $s$의 확률분포를 이용해 $x$의 likelihood를 표현할 수 있다.
- 그러나 변수 $x$를 $s$로 변환할 때에는, 그 변환이 공간과 확률 밀도를 어떻게 변화시키는지를 반드시 고려해야 한다.

- 이 변환은 공간을 늘리거나, 압축하거나, 회전하거나, 뒤집을 수 있다.
- 이러한 변화를 정량화하기 위해 변환 행렬 $W$의 행렬식(determinant)을 사용한다.
- 행렬식은 스케일링 계수와 같다:
- $|\det(W)|>1$이면 공간이 확장된다. 즉, 데이터 포인트들이 더 멀리 퍼진다.
- $|\det(W)|<1$이면 공간이 수축된다. 즉, 데이터 포인트들이 더 가까워진다.
- $|\det(W)|=1$이면 공간의 부피가 그대로 유지된다.

- 따라서 확률들이 여전히 올바른 값을 가지도록(즉, 전체 확률의 합이 1이 되도록) 하기 위해, 일반적으로 다음과 같이 $\det(W)$를 곱하여 보정한다:  

$$  
p(x)=p(s)\cdot |\det(W)|  
$$

- 이 식은 다음을 보장한다:
- 공간이 확장될 때($\det(W)>1$), 전체 확률을 일정하게 유지하기 위해 확률 밀도(probability density)는 감소한다.
- 공간이 수축될 때($\det(W)<1$), 이에 맞추어 확률 밀도는 증가한다.

- ICA는 원천 신호 $s_1,s_2,\ldots,s_d$가 통계적으로 서로 독립이라고 가정한다는 점을 다시 상기하자.
- 따라서 $x$의 확률밀도함수(pdf)는 다음과 같이 표현된다:  

$$
\begin{align}
p(x)&=p(s)\det(W)\\  
&=\prod_{i=1}^{d}p_s(s_i)\det(W)\\  
&=\prod_{i=1}^{d}p_s(w_i^Tx)\det(W)  
\end{align}
$$

- 여기서 $w_i^Tx$는 $x$를 $W$의 $i$번째 행 방향으로 선형 사영(linear projection)한 값이며, 이는 $i$번째 원천 성분 $s_i$의 추정값을 의미한다.

- $N$개의 관측 데이터 ${x^{(n)}}_{n=1}^{N}$가 주어졌을 때, 데이터의 로그 우도(log-likelihood)는 다음과 같다:  

$$  
L(W)=\log\left(\prod_{n=1}^{N}p(x^{(n)})\right)=\sum_{n=1}^{N}\log p(x^{(n)})  
$$
- 위에서 구한 $p(x)$의 식을 대입하면 다음을 얻는다:  

$$  
L(W)=\sum_{n=1}^{N}\left(\sum_{i=1}^{d}\log p_s\left(w_i^Tx^{(n)}\right)+\log |\det(W)|\right)  
$$

- $p_s$, 즉 독립 원천 신호의 확률을 계산하기 위해서는 각 원천값이 얼마나 가능성이 높은지를 설명하는 함수를 선택해야 한다.
- 원천 신호들은 비가우시안(non-Gaussian)이라고 가정되므로, pdf를 근사하기 위해 비이차 함수(non-quadratic function)를 자주 사용한다.
- 원천 밀도(source density)에 대한 일반적인 선택은 누적분포함수(CDF)에 sigmoid 함수를 사용하는 것이다:  

$$  
p_s(s_i)\approx g'(s_i)  
$$

- 여기서  

$$  
g(s_i)=\frac{1}{1+e^{-s_i}}  
$$  
이고, 그 도함수는 다음과 같다:  

$$  
g'(s_i)=g(s_i)(1-g(s_i))  
$$

- 여기서 sigmoid 함수의 도함수 $g'(s_i)$는 가우시안과 유사한 형태를 가지면서도, 비가우시안 원천 분포를 근사하기 위한 매끄럽고 계산하기 쉬운 PDF를 제공한다.    
- sigmoid 함수의 도함수는 다음과 같은 형태를 가진다.

- 시그모이드를 사용하면 도함수 계산이 쉽고 가우시안 분포와 유사하지만 가우시안 분포가 아니게 사용 할 수 있음.

- 이를 로그 우도(log-likelihood)에 대입하면 다음을 얻는다:  

$$  
L(W)=\sum_{n=1}^{N}(\sum_{i=1}^{d}\log g'\left(w_i^Tx^{(n)}\right)+\log |\det(W)|)  
$$

- 이것이 ICA에서 최대화하고자 하는 로그 우도 함수이다.

- 우리의 목표는 $W$에 대해 로그 우도 함수를 최대화하는 것이다.
- 첫 번째 항에 대해:  

$$
\begin{align}
\nabla_{w_i}\log g'\left(w_i^Tx^{(n)}\right)  
&=\frac{g''\left(w_i^Tx^{(n)}\right)}{g'\left(w_i^Tx^{(n)}\right)}x^{(n)}\\
&=\left(1-2g\left(w_i^Tx^{(n)}\right)\right)x^{(n)}  
\end{align}
$$

- 이는 sigmoid 함수 $g(s)$의 성질,  

$$  
\frac{g''(s)}{g'(s)}=1-2g(s)  
$$  
을 이용한 결과이다.
- 두 번째 항에 대해:  

$$
\begin{align}
\nabla_W\log \det(W)  
&=\frac{1}{\det(W)}\frac{\partial}{\partial W}\det(W)  \\
&=\frac{1}{\det(W)}\det(W)(W^{-1})^T  \\  
&=(W^{-1})^T  
\end{align}
$$

- 이제 gradient ascent를 적용하면 unmixing matrix를 갱신하는 다음과 같은 학습 규칙(learning rule)을 얻는다:  

$$  
W\leftarrow W+\alpha\left[\frac{1}{N}\sum_{n=1}^{N}x^{(n)}\left(1-2g(Wx^{(n)})\right)^T+(W^T)^{-1}\right]  
$$

- 여기서 $\alpha$는 학습률(learning rate)이고, $g(s)$는 비선형 함수이다. 여기서는 sigmoid 함수와 그 도함수를 사용하며, sigmoid 함수는 비가우시안성(non-Gaussianity)을 잘 포착할 수 있다.
- 이 업데이트를 반복적으로 적용하면, 행렬 $W$는 점차 독립 원천 신호들을 분리하는 해로 수렴하게 된다.

- ICA가 혼합 관계 $x=As$를 완벽하게 복원하더라도, 관측 데이터만으로는 해결할 수 없는 몇 가지 본질적인 모호성이 남아 있다.    
	- 1. 순열 모호성(permutation ambiguity): **복원된 원천 신호들은 서로 다른 순서로 나타날 수 있다**. 이는 혼합 행렬 $A$의 열을 바꾸는 것이 단순히 원천 신호의 순서를 바꾸는 것에 해당하며, 데이터 안에는 어떤 순서가 “올바른” 순서인지를 알려주는 정보가 없기 때문이다.    
	- 2. 스케일링 모호성(scaling ambiguity): 각 원천 신호는 어떤 상수로 곱해질 수 있으며, 이때 혼합 행렬의 대응되는 열을 같은 상수로 나누면 곱 $As$는 변하지 않는다.    
- 실제로 이러한 모호성은 보통 큰 문제가 되지 않는다. 복원된 원천 신호의 절대적인 스케일과 순서는 종종 해석이나 활용에 큰 영향을 주지 않기 때문이다.

- ICA는 순서를 고려 하지 않음 → 순서의 모호성.
- ICA는 소스의 크기를 고려 하지 않음. → 스케일링의 모호성

- 위쪽 행은 원래의 원천 비디오(source videos)를 보여준다.    
- 가운데 행은 ICA 알고리즘의 입력으로 사용된 네 개의 임의 혼합(random mixtures)을 보여준다.    
- 아래쪽 행은 ICA를 통해 복원된 비디오(reconstructed videos)를 보여준다.



- ICA는 fMRI 및 EEG 분석에서도 널리 사용되며, 측정된 데이터로부터 기저의 뇌 활동 신호를 분리하고 artifact(잡음 및 인공 신호)를 제거하는 데 활용된다.


- ICA는 정렬이 안됨. → 매뉴얼하게 체크를 해야 함.
- ICA는 다양한 방법이 있음.
- ICA 를 이용한 차원축소는 조금 애매할 수 있음. 원래 목적은 노이즈 제거등에 많이 사용.
- ICA는 non-Gaussianity를 최대화 하는 방안으로 수식화 → 라이클리 후드와 비교해서 편한 방법으로 이해 하면 됨.


