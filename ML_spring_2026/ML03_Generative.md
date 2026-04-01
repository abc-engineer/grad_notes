2026-03-24 08:20
## 3강 Generative
### Intro
- 콘다 환경에서 주피터 노트북 첨부 파일 이용해서 예제 확인 할 것.
- 그라디언트, 아날리틱 솔루션 2가지로 풀수 있는데 둘다 코드 첨부파일로 올림.
- 사실 패키지 이용하면 코드는 한두줄임.
	- 매뉴얼로 하면 얼마나 차이나고 계산을 어떻게 하는지 첨부 파일과 싸이킷런 같은 패키지랑 비교해보면 좋을 것.

### Discriminative and Generative Models
- 결정과 생성모델
- 결정이 무엇인가?
- 생성이 무엇이냐?
- 결정과 생성의 차이를 알아야 함.
- 지금까지 배운것은 결정 모델
- 머신러닝을 데이터를 이해하고 패턴을 이해하는 것인데 결정과 생성모델은 차이가 있음
- 패턴과 관계 학습이란 목표가 같음
- 결정 모델은 예측에 초점
	- 결정 모델은 파랑과 빨강을 구별 또는 판별 할 수 있는가?
	- 새로운 데이터가 파랑이냐 빨강이냐가 초점
	- 그래서 디시전 바운더리를 결정하는게 목표
- 생성 모델은 새로운 데이터 생성에 초점
	- 생성모델은 디시전 바운더리에는 관심없음
	- 데이터 생성에 더 관심이 있음
- 판별 모델과 생성 모델은 데이터를 모델링하는 접근 방식에서 근본적으로 서로 다르다.
- 두 모델 모두 데이터 내부의 패턴과 관계를 학습하는 것을 목표로 한다.    
- 그러나 무엇을 모델링하려는지, 그리고 그 정보를 어떻게 사용해 예측하거나 새로운 샘플을 생성하는지에서 차이가 있다.

### discriminative model
- 조건부 확률을 통해 y값을 예측하는게 목적
- 판별(discriminative) 모델은 서로 다른 클래스나 결과를 구분하는 경계에 집중한다.
- 판별 모델은 조건부 확률 $p(y \mid x)$를 학습한다. 즉, 관측 데이터 $x$에 따라 레이블 $y$가 어떻게 결정되는지를 모델링한다.    
- 다시 말해, 주어진 관측값에 대해 해당 데이터의 클래스나 범주를 직접 예측하는 것이 판별 모델의 목표이다.
- 판별 모델은 데이터가 어떻게 생성되었는지를 설명하려고 하지 않는다.
- 대신 클래스 간을 가장 효과적으로 구분하거나 결과를 예측하는 방법을 찾는 데 집중한다.        
- 이러한 특성 때문에 판별 모델은 분류나 회귀 문제에서 매우 효과적이며, 비교적 적은 모델링 가정으로도 높은 성능을 달성하는 경우가 많다.    
- 판별 모델의 대표적인 예시는 다음과 같다:    
    - 로지스틱 회귀        
    - 서포트 벡터 머신        
    - 일반적인 신경망 모델
- 큰 liklihood를 갖아야 함.
- Generative model은 likelihood $P(x \mid y)$가 직접적으로 중요
- Discriminative model은 likelihood $P(x|y)$가 아니라conditional likelihood $P(y|x)$를 학습에서 최대화하고 예측 할때 $P(y|x)$가 가장 큰 클래스를 선택
- 수식화 하면 결국 연결됨.

### generative model
- 데이터 생성에 관심이 있음
- 조건부 확률이 아니고 joint 확률을 이용
- 생성 모델은 이와 대조적으로 보다 포괄적인 관점을 취한다.
- 생성 모델은 분류 자체에 집중하기보다는, 데이터가 실제로 생성되는 과정을 설명하려고 한다.   
- 지도 학습 맥락에서 생성 모델은 결합 확률 분포 $p(x, y)$를 학습한다.
- 이는 관측값 $x$와 그에 대응하는 레이블 $y$가 함께 어떻게 발생하는지를 표현한다.
- 𝑝 𝒙, 𝑦 = 𝑝 𝒙 𝑦 𝑝 𝑦 
- 𝑝 𝒙 𝑦 : x를 관측해내는 것이 목표
- 𝑝 𝑦 : 분류
- 전체 결합 분포 $p(x, y)$를 모델링하는 것은 데이터에 대한 완전한 확률적 설명을 제공한다는 점에서 유용하다.    
- 이 분포는 다음과 같은 두 가지 핵심 요소로 구성된다:

$$  
p(x, y) = p(x \mid y) p(y)  
$$
- 첫 번째는 조건부 분포 $p(x \mid y)$: 특정 클래스 $y$가 주어졌을 때, 관측 데이터 $x$가 어떻게 생성되는지를 설명한다.
- 두 번째는 사전 분포(prior distribution) $p(y)$: 이는 어떤 데이터도 관측하기 전에 각 클래스나 범주가 얼마나 발생할 가능성이 있는지를 나타낸다.
- 추상적인 개념을 설명할때 베이즈 룰이 나옴.
- 생성과 결정모델이 베이즈 이론으로 만나게 됨.
-  결합 분포 $p(x, y)$를 학습한 이후에는, 베이즈 정리를 통해 사후 확률 $p(y \mid x)$를 구할 수 있다:
  
$$
p(y \mid x) = \frac{p(x \mid y) , p(y)}{p(x)}
$$
- 이 사후 확률(posterior probability)을 통해 생성 모델도 분류나 추론을 수행할 수 있다.
- 즉, 생성 모델의 주된 목표는 데이터 생성 과정의 모델링이지만, 그 결과로 분류 문제에도 활용될 수 있다.
- 생성 모델이지만 판단, 분류 모델에 사용 할 수 있음.
- $\arg\max_y p(y \mid x)$ 는 판단 모델에서
- 생성모델에서는  $p(x \mid y)p(y)$를 먼저 모델링 이후 $\arg\max_y p(x \mid y)p(y)$ 형태로 사용
- 생성모델을 이용해서 판별에 이용할 수 있는 이유임.
- 실제 분류 문제에서는 사후 확률 $p(y \mid x)$의 정확한 값을 계산할 필요는 없다.    
- 대신, 사후 확률을 최대화하는 클래스 $y$를 선택하여 예측을 수행한다.    
- 주변 가능도 $p(x)$는 관측된 데이터 $x$에만 의존하며, 클래스 $y$와는 무관하다.    
    - 따라서 $y$에 대해 최대화를 수행할 때 상수로 작용한다.        
- 이로 인해 분모 $p(x)$는 최대값의 결과에 영향을 주지 않으므로 생략할 수 있다.    
- 결과적으로 분류를 위한 결정 규칙은 다음과 같이 단순화된다:  

$$  
\arg\max_y p(y \mid x)  
= \arg\max_y \frac{p(x \mid y), p(y)}{p(x)}  
= \arg\max_y p(x \mid y), p(y)  
$$

- 결정모델은 선을 찾는것
- 생성모델은 데이터 분포를 찾음
- 데이터 생성 분포나 방식을 알면 새로운 데이터가 어디서 생성 되었는지 예측할 수 있음.
	- 이 방식이Naive Bayes나 Linear Discriminant Analysis (LDA)의 기본 개념임.
- 따라서 생성 분류기는 결정 경계를 직접 학습하는 대신,    
    - 사전 분포 $p(y)$와 조건부 분포 $p(x \mid y)$를 학습하고,        
    - 베이즈 정리를 이용하여 클래스 소속을 결정한다.        
- 이러한 생성 기반 분류기의 대표적인 예는 다음과 같다:    
    - 나이브 베이즈 (Naive Bayes)        
    - 선형 판별 분석 (LDA, Linear Discriminant Analysis)

### Naive Bayes
- 제목에 베이즈가 있음 - > 베이즈 룰을 적극적으로사용하는 분류 모델이라고 보면됨.
- 베이즈룰은 기존에 갖고 있는 확률이 있는데 새로운 정보가 있을대 원래 확률을 바꿀지 말지를 결정하는 과정을 잘 포장 한 것.
- 내일 비확률이 10%라고 믿었는데 일기예보에서 내일 비 확률이 70%라는 정보를 얻음. -> 비가 올지 말지 다시 예측->내일 우산을 가져가야지라고 행동을 업데이트 함.
- 나이브 베이즈는 베이즈 정리에 직접 기반하므로, 먼저 이 정리와 그 해석을 이해하는 것이 중요 
- 베이즈 정리는 새로운 정보가 주어졌을 때 확률을 갱신하는 원리적인 방법을 제공한다.    
- 즉, 사전 지식(prior)과 데이터로부터 얻은 증거(evidence)를 결합하여,관측된 데이터가 주어졌을 때 어떤 가설의 확률을 계산하는 방법을 설명한다.

- y는 비가 오는 이벤트
- 𝑝(𝑦)는 비가올 확률?
- 𝑝 (𝑥|𝑦) 비가 온다고 했을때 예측이 맞을 확률
- 𝑝(x)는 전체 확률을 노말라이즈
- 𝑝 (𝑦|𝑥): 내일 우산을 챙길지 말지 
- 베이즈 정리는 다음과 같이 정의된다:  

$$  
p(y \mid x) = \frac{p(x \mid y), p(y)}{p(x)}  
$$

- 여기서 $y$는 “비가 온다”는 가설을 의미한다.    
    - $p(y)$는 사전 확률로, 어떤 예보도 보기 전 비가 올 확률 (예: 10%)을 나타낸다.        
- 관측값 $x$는 날씨 예보를 의미한다.    
    - $p(x \mid y)$는 비가 올 때 이러한 예보가 나타날 가능도(likelihood)이다.        
- $p(x)$는 주변 가능도(marginal likelihood)로, 전체 확률이 1이 되도록 정규화하는 역할을 한다.   
- 이 모든 요소를 결합하면 사후 확률 $p(y \mid x)$를 얻는다.    
    - 이는 예보를 확인한 이후 비가 올 확률에 대한 갱신된 믿음을 의미하며, 우산을 가져갈지 여부를 결정하는 근거가 된다.
- 어떻게 활용 하는가?
- 일단 지도 학습임. -> x,y 값이 있음
	- x는 벡터로 표시, y는 1인지 0인지를 구분하는 스칼라 값
- 이제 베이즈 정리를 분류 문제에 적용하는 확률적 학습 알고리즘인 나이브 베이즈 분류기로 넘어간다.    
- 지도 학습 분류 문제에서 다음과 같은 학습 데이터가 주어진다고 하자:  

$$  
\{(x^{(1)}, y^{(1)}), \dots, (x^{(n)}, y^{(n)})\}
$$

- 여기서 각 입력 $x_i \in \mathbb{R}^d$는 특징 벡터이고, 각 레이블 $y_i$는 유한한 클래스 집합에 속한다.    
- 분류의 목표는 새로운 입력 $x$가 주어졌을 때, 해당 입력의 레이블 $y$를 예측하는 결정 규칙을 학습하는 것이다.
- x가 주어졌을때 y가 최대로 되는 확률값을 찾는게 목적인데 생성모델을 이용해서 할 수 있음
- -> 베이즈 룰을 이용 𝑝 (𝑥|𝑦) 𝑝(𝑦)해서𝑝(𝑦| 𝑥) 를 구하면 됨.
- 핵심은  class-conditional distribution 𝑝(𝒙|𝑦)
- 베이즈 정리를 적용하면 결정 규칙은 다음과 같이 단순화된다:  

$$  
\arg\max_y p(y \mid x)  
= \arg\max_y p(x \mid y), p(y)  
$$
- 클래스 사전 확률 $p(y)$는 각 클래스가 데이터에서 얼마나 자주 등장하는지를 나타내며, 학습 데이터로부터 쉽게 추정할 수 있다.        
- 주요 어려움은 클래스 조건부 분포 $p(x \mid y)$를 추정하는 것이다.    
- 특징 차원 $d$가 클 경우,가능한 특징 벡터의 수가 $d$에 대해 지수적으로 증가하므로 이를 직접 추정하는 것은 사실상 불가능해진다.        
- 이것이 바로 나이브 베이즈가 해결하고자 하는 핵심 문제이다.
- x의 피쳐 디멘젼은 여러개임.
	- 예를 들어 이미지가 200by 200이면 400디멘젼을 갖게 됨
- 모든 피쳐는 conditionally independent이다른 강력한 전제를 하는것이 Naive Bayes
	- 1번 픽셀과 2번 픽셀이 있다면 사실 연관이 있을 확률이 높지만 Naive Bayes에서는 둘이 독립이라고 생각하고 계산
	- 하지만 실제로 값이 잘 맞음
- 독립이면 조건부 확률을 각각의 곱으로 계산 할 수 있음.
- 학습을 계산 가능하게 만들기 위해, 나이브 베이즈는 강하지만 단순화된 가정을 도입한다:    
    - 클래스 $y$가 주어졌을 때 특징들은 서로 조건부 독립이다.        
- 즉, 다음과 같이 전개된다:  

$$
\begin{align}
p(x \mid y)&= p(x_1, x_2, \dots, x_d \mid y)\\
&= p(x_1 \mid y),  
p(x_2 \mid y, x_1),  
p(x_3 \mid y, x_1, x_2),\cdots,  
p(x_d \mid y, x_1, \dots, x_{d-1})\\
&= p(x_1 \mid y),  
p(x_2 \mid y),  
p(x_3 \mid y),\cdots,  
p(x_d \mid y)\\
&= \prod_{j=1}^{d} p(x_j \mid y)
\end{align}
$$
- 이 가정은 특징들이 항상 독립이라는 것을 의미하지 않는다.    
    - 오직 클래스 $y$가 주어졌을 때만 독립이라고 가정한다.        
- 실제로는 이 가정이 성립하지 않는 경우가 많지만, 그럼에도 불구하고 다양한 문제에서 매우 효과적인 분류 성능을 보인다.
- 곱한 확률에 log를 취해줌
- log를 쓰면 곱을 덧셈으로 바꿀수 있고 다른 장점들이 있음 (0을 피함?)
- 이 가정(조건부 독립성) 하에서 사후 확률은 다음과 같이 표현된다:  

$$  
p(y \mid x)  
= \frac{p(x \mid y), p(y)}{p(x)}  
\propto p(y), \prod_{j=1}^{d} p(x_j \mid y)  
$$

- 계산의 편의를 위해, 실제로는 로그 공간에서 계산하는 것이 일반적이다.    
- 그러면 분류기는 다음과 같이 표현된다:  

$$  
\arg\max_y \left[ \log p(y) + \sum_{j=1}^{d} \log p(x_j \mid y) \right]  
$$
- 이메일을 스팸($y = 1$) 또는 정상 메일($y = 0$)로 분류하는 문제를 생각해보자.    
- 각 특징은 이진값을 가진다고 가정한다.    
    - 즉, $x_j \in {0, 1}$ 이다.        
- 여기서 $x_j = 1$이면 문서에 단어 $j$가 존재함을 의미하고, $x_j = 0$이면 그렇지 않음을 의미한다.
- 𝜙𝑦 : y가 1일 확률
- 𝜙𝑗|1 : 단어가 있을때 y=1
- 𝜙𝑗|0: 단어가 있을때 y=0 ??
- 이진 분류 문제를 가정하자.    
    - 레이블은 $y \in {0,1}$ 이고,        
    - 특징 벡터는 $x \in {0,1}^d$ 이다.        
- 이때 매개변수 $\phi$를 다음과 같이 정의한다:    
	- $\phi_y = p(y = 1)$: 데이터 전체에서 스팸일 확률 (사전 확률, prior)
	- $\phi_{j \mid 1} = p(x_j = 1 \mid y = 1)$: 스팸 메일에서 단어 $j$가 등장할 확률
	- $\phi_{j \mid 0} = p(x_j = 1 \mid y = 0)$: 정상 메일에서 단어 $j$가 등장할 확률
- 나이브 베이즈 가정에 의해 결합분포 $p(x, y)$는 다음과 같이 쓸 수 있다:  

$$  
p(x, y) = p(y), p(x \mid y) = p(y), \prod_{j=1}^{d} p(x_j \mid y)  
$$
- 각 특징 $x_j \in {0,1}$는 $y$가 주어졌을 때 베르누이 분포를 따른다.    
- 따라서 조건부 확률은 다음과 같이 표현된다:  

$$  
p(x_j \mid y = c) = \phi_{j \mid c}^{, x_j}, (1 - \phi_{j \mid c})^{, 1 - x_j}  
$$

- 이를 이용하면 하나의 데이터 $(x, y)$에 대한 결합 확률은 다음과 같다:  

$$  
p(x, y)  
= \phi_y^{, y}, (1 - \phi_y)^{, 1 - y}  
\prod_{j=1}^{d}  
\phi_{j \mid y}^{, x_j},  
(1 - \phi_{j \mid y})^{, 1 - x_j}  
$$
- 여기서 $\phi_{j \mid y}$의 의미는 다음과 같다:  
    - $y = 1$이면 $\phi_{j \mid y} = \phi_{j \mid 1}$        
    - $y = 0$이면 $\phi_{j \mid y} = \phi_{j \mid 0}$
- 해석
	- $\phi_y^{, y} (1 - \phi_y)^{, 1 - y}$  → 레이블 $y$ 자체의 확률 (베르누이 prior)        
	- $\phi_{j \mid y}^{, x_j} (1 - \phi_{j \mid y})^{, 1 - x_j}$ → 각 단어(특징)가 등장/비등장할 확률
	- 전체는"클래스 선택 + 각 특징 생성"을 모두 곱한 형태
   
- log를 취해줌.
- i.i.d. (독립 동일 분포) 데이터가 주어졌을 때, 전체 데이터셋에 대한 우도(likelihood)는 다음과 같이 표현된다:  

$$
\prod_{i=1}^{n} p(x^{(i)}, y^{(i)};, \phi)  
$$
- 로그 우도(log-likelihood)를 취하면 다음과 같다:  

$$
L = \sum_{i=1}^{n} \log p(x^{(i)}, y^{(i)})  
$$
- 핵심 의미
	- 곱(product) 형태의 우도는 계산이 어렵기 때문에 로그를 취한다.
	- 로그를 취하면: 곱 → 합으로 변환되어 계산이 쉬워짐        
    - 수치적으로도 더 안정적
-  표기 설명
	- $x^{(i)}, y^{(i)}$
        - $i$번째 데이터 샘플
	- $\phi$    
	    - 모델 파라미터 (예: $\phi_y$, $\phi_{j|y}$)
- 먼저 사전 확률(prior) 항을 분리하면 다음과 같다:  

$$  
\sum_{i=1}^{n} \log \left( \phi_y^{, y^{(i)}} (1 - \phi_y)^{, 1 - y^{(i)}} \right)
\sum_{i=1}^{n} \left[  
y^{(i)} \log \phi_y + (1 - y^{(i)}) \log(1 - \phi_y)  
\right]  
$$

- 이제 조건부 확률 항을 분리하자.각 데이터 $i$에 대해,

$$
\log p!\left(x^{(i)} \mid y^{(i)}\right)
\sum_{j=1}^{d}  
\left[  
x_j^{(i)} \log \phi_{j \mid y^{(i)}} +  
(1 - x_j^{(i)}) \log(1 - \phi_{j \mid y^{(i)}})  
\right]  
$$
- 첫 번째 항은 레이블 $y$의 사전 확률에 해당하고,        
- 두 번째 항은 주어진 레이블 아래에서 각 특징 $x_j$가 나타날 확률을 더한 형태이다.
- 최종적으로 이 log-likelihood 식이 나옴.
	- 조인트 확률을 다 더해 준 값
- log-likelihood를 최대화해주는 𝜙𝑦, 𝜙𝑗|𝑦를 구하는 것.
- 따라서 전체 로그 우도는 다음과 같이 표현된다:  

$$
\begin{align}
L&= \sum_{i=1}^{n}
\left[y^{(i)} \log \phi_y + (1 - y^{(i)}) \log(1 - \phi_y)  
\right] \ + \sum_{i=1}^{n} \sum_{j=1}^{d}  
\left[x_j^{(i)} \log \phi_{j \mid y^{(i)}} +  
(1 - x_j^{(i)}) \log(1 - \phi_{j \mid y^{(i)}})  
\right]  
\end{align}  
$$

- 핵심 포인트는 로그 우도 $L$이 파라미터별로 분리(separable)된다는 것이다.    
- $\phi_y$는 첫 번째 합에만 등장한다.    
- 각 $\phi_{j \mid c}$는 오직 $y^{(i)} = c$인 항들에서만 등장한다.
- 따라서 각 파라미터를 서로 독립적으로 최적화할 수 있다.    
    - 즉, 하나의 파라미터를 최적화할 때 다른 파라미터에 영향을 주지 않는다.
- 클래스 사전 확률 $\phi_y$를 추정하기 위해, 로그 우도 $L$을 $\phi_y$에 대해 미분하고 0으로 둔다:  

$$  
\frac{\partial L}{\partial \phi_y}
\sum_{i=1}^{n}  
\left[  
\frac{y^{(i)}}{\phi_y}
\frac{1 - y^{(i)}}{1 - \phi_y}  
\right]  
= 0  
$$
- 다음과 같이 정의하자:  

$$  
n_1 = \sum_{i=1}^{n} y^{(i)}, \quad n_0 = n - n_1  
$$
- 그러면 식은 다음과 같이 정리된다:  

$$  
\frac{n_1}{\phi_y} - \frac{n_0}{1 - \phi_y} = 0  
$$
- 양변을 정리하면:  

$$  
n_1 (1 - \phi_y) = n_0 \phi_y  
$$  

$$  
n_1 = (n_0 + n_1), \phi_y = n \phi_y  
$$
- 따라서 최종적으로:  

$$  
\phi_y = \frac{n_1}{n}  
$$
- 해석
	- $\phi_y$는 단순히 전체 데이터 중에서 $y=1$인 비율이다.    
	- 즉, **스팸 클래스의 빈도 = 사전 확률의 MLE**이다.
- 따라서 최대우도추정(MLE)은 다음과 같다:  

$$  
\hat{\phi}_y  
= \frac{n_1}{n}  
= \frac{1}{n} \sum_{i=1}^{n} \mathbf{1}\big(y^{(i)} = 1\big)  
$$
- 여기서 $\mathbf{1}(y^{(i)} = 1)$은 지시 함수(indicator function)이다.    
    - $y^{(i)} = 1$이면 1        
    - $y^{(i)} = 0$이면 0
- 따라서,    
- $p(y = 1)$의 최적 추정값은 레이블이 1인 데이터의 비율과 같다.
- 핵심 해석
	- 나이브 베이즈에서 사전 확률은 복잡한 계산 없이 단순한 **빈도 계산**으로 얻어진다.
- 즉,  

$$  
\hat{p}(y = 1) = \text{(전체 데이터 중 } y=1 \text{의 비율)}  
$$

- 이제 $\phi_{j \mid 1}$을 추정하기 위해, 특정 특징 $j$를 고정하고 $y^{(i)} = 1$인 데이터만 고려한다.
- 로그 우도에서 해당 항만 추출하면:  

$$  
L_{j \mid 1}
\sum_{i:, y^{(i)} = 1}  
\left[  
x_j^{(i)} \log \phi_{j \mid 1}  
+  
(1 - x_j^{(i)}) \log(1 - \phi_{j \mid 1})  
\right]  
$$
- 이를 $\phi_{j \mid 1}$에 대해 미분하고 0으로 두면:  

$$  
\frac{\partial L_{j \mid 1}}{\partial \phi_{j \mid 1}}
=\sum_{i; y^{(i)} = 1}  
\left[  
\frac{x_j^{(i)}}{\phi_{j \mid 1}}
\frac{1 - x_j^{(i)}}{1 - \phi_{j \mid 1}}  
\right]  
= 0  
$$
- 핵심 의미
	- 오직 **$y=1$ 인 데이터만 $\phi_{j \mid 1}$ 추정에 영향을 준다.
	- 이는 파라미터가 클래스별로 분리되어 학습됨을 보여준다.

- 다음과 같이 정의하자:  

$$  
s_{j1} = \sum_{i:, y^{(i)} = 1} x_j^{(i)},  
\quad  
n_1 = \sum_{i=1}^{n} \mathbf{1}(y^{(i)} = 1)  
$$
- 그러면 다음 관계가 성립한다:  

$$  
\sum_{i:, y^{(i)} = 1} (1 - x_j^{(i)})
= \sum_{i:, y^{(i)} = 1} 1
\sum_{i:, y^{(i)} = 1} x_j^{(i)}  
= n_1 - s_{j1}  
$$

- $s_{j1}$: $y=1$인 데이터 중에서 특징 $j$가 등장한 횟수
- $n_1$: $y=1$인 전체 데이터 개수
- $n_1 - s_{j1}$    
    - $y=1$인 데이터 중에서 특징 $j$가 등장하지 않은 횟수
- 전체(스팸) = 등장 + 미등장  

$$  
n_1 = s_{j1} + (n_1 - s_{j1})  
$$

- 그러면 방정식은 다음과 같이 된다:  

$$  
\frac{s_{j1}}{\phi_{j \mid 1}} - \frac{n_1 - s_{j1}}{1 - \phi_{j \mid 1}} = 0  
\quad \Longrightarrow \quad  
s_{j1} = n_1 \phi_{j \mid 1}  
$$
- 따라서 최대우도추정량은 다음과 같다:  

$$  
\hat{\phi}_{j \mid 1}  
= \frac{s_{j1}}{n_1}  
= \frac{\sum_{i=1}^{n} \mathbf{1}!\left(y^{(i)} = 1\right) x_j^{(i)}}{\sum_{i=1}^{n} \mathbf{1}!\left(y^{(i)} = 1\right)}  
$$
- 또한 이를 지시 함수로 다시 쓰면,  

$$  
\hat{\phi}_{j \mid 1}
\frac{  
\sum_{i=1}^{n}  
\mathbf{1}!\left(y^{(i)} = 1 ,\wedge, x_j^{(i)} = 1\right)  
}{  
\sum_{i=1}^{n}  
\mathbf{1}!\left(y^{(i)} = 1\right)  
}  
$$
- 여기서 $\wedge$ 는 논리곱(and) 을 의미
- $\hat{\phi}_{j \mid 1}$은$p(x_j = 1 \mid y = 1)$의 추정값
	- 즉, 클래스가 1인 데이터들 중에서특징 $j$가 1인 비율이다.
- 분모: 
    - $y=1$인 전체 샘플 수        
- 분자:    
    - $y=1$이면서 동시에 $x_j=1$인 샘플 수
- 따라서 클래스 1 안에서 특징 $j$가 나타날 조건부 확률의 빈도 추정치  

$$  
\hat{\phi}_{j \mid 1}
\frac{\text{$y=1$이고 $x_j=1$인 개수}}{\text{$y=1$인 전체 개수}}  
$$

- $\phi_{j \mid 0}$에 대한 유도는 동일하며, 단지 $y^{(i)} = 0$인 데이터만 사용한다.    
- 따라서 최대우도추정량은 다음과 같다:  

$$  
\hat{\phi}_{j \mid 0}  
= \frac{s_{j0}}{n_0}  
= \frac{  
\sum_{i=1}^{n}  
\mathbf{1}!\left(y^{(i)} = 0 ,\wedge, x_j^{(i)} = 1\right)  
}{  
\sum_{i=1}^{n}  
\mathbf{1}!\left(y^{(i)} = 0\right)  
}  
$$

- $\hat{\phi}_{j \mid 0}$은$p(x_j = 1 \mid y = 0)$의 추정값이다.
- 즉, 클래스가 0인 데이터들 중에서특징 $j$가 1인 비율

### 최종 정리 (Bernoulli Naive Bayes MLE)  

$$  
\hat{\phi}_y = \frac{1}{n} \sum_{i=1}^{n} \mathbf{1}(y^{(i)} = 1)  
$$

$$  
\hat{\phi}_{j \mid 1}  
= \frac{  
\sum_{i=1}^{n}  
\mathbf{1}(y^{(i)} = 1 ,\wedge, x_j^{(i)} = 1)  
}{  
\sum_{i=1}^{n}  
\mathbf{1}(y^{(i)} = 1)  
}  
$$

$$  
\hat{\phi}_{j \mid 0}  
= \frac{  
\sum_{i=1}^{n}  
\mathbf{1}(y^{(i)} = 0 ,\wedge, x_j^{(i)} = 1)  
}{  
\sum_{i=1}^{n}  
\mathbf{1}(y^{(i)} = 0)  
}  
$$
- 모든 파라미터는 단순한 빈도 비율로 계산된다.    
- 즉, 나이브 베이즈는 복잡한 최적화 없이 카운팅(counting)만으로 학습이 가능하다.

- Naive Bayes는 각각 확률이 독립이란 전제를 통해 확률의 곱을 이용해 계산을 쉽게 하는게 포인트임.
- 새로운 입력 $x \in {0,1}^d$가 주어졌을 때, 앞에서 구한 최대우도추정값을 대입하면 다음과 같다:  

$$  
p(y = 1) = \hat{\phi}_y  
$$

$$  
p(y = 0) = 1 - \hat{\phi}_y  
$$ 

$$  
p(x_j \mid y = c)
\hat{\phi}_{j \mid c}^{, x_j}  
(1 - \hat{\phi}_{j \mid c})^{, 1 - x_j}  
$$

- 최종적으로 나이브 베이즈 분류기는 다음과 같이 예측한다:  

$$  
h(x)
\arg\max_{y \in {0,1}}  
\hat{\phi}_y^{, y}  
(1 - \hat{\phi}_y)^{, 1-y}  
\prod_{j=1}^{d}  
\hat{\phi}_{j \mid y}^{, x_j}  
(1 - \hat{\phi}_{j \mid y})^{, 1-x_j}  
$$

- 의미
	- 가능한 클래스 $y \in {0,1}$ 각각에 대해 그 클래스의 사전 확률과 각 특징이 나타날 조건부 확률을 모두 곱한 뒤, 더 큰 값을 만드는 클래스를 선택한다.
 - $y=1$일 때의 점수와 $y=0$일 때의 점수를 각각 계산하고, 둘 중 더 큰 쪽으로 분류하는 것이다.
- 즉, 이 식은 “이 입력 $x$가 스팸 클래스에서 생성되었을 가능성”과 “정상 메일 클래스에서 생성되었을 가능성”을 비교하는 규칙
- 바이너리 피쳐가 아니여도 적용이 가능함.
- 카테고리나 연속성 피쳐도 가능
- 피처에 따라 바이너리, 멀티노미아 분포등을 이용해 확률을 계산 할 수 있음.
- 연속성 피쳐는 가우시안이나 노말 분포
- Bernoulli Naive Bayes 모델은 각 특성 $x_j$가 이진값이라고 가정한다.    
- 그러나 Naive Bayes 프레임워크는 각 특성 차원에 대해 적절한 클래스 조건부분포 $p(x_j \mid y)$를 선택함으로써 다른 유형의 특성에도 자연스럽게 확장된다.    
- 핵심 가정은 동일하게 유지된다. 즉, 클래스 레이블이 주어졌을 때 특성들은 조건부 독립이다.
- 예를 들어, 어떤 특성이 두 개보다 많은 유한한 범주 값을 가질 때, 조건부분포 $p(x_j \mid y)$는 범주형(또는 다항) 분포로 모델링할 수 있다.    
- 특성 $j$가 $K_j$개의 가능한 값 중 하나를 취한다고 하면, 다음과 같은 파라미터를 도입한다: $\theta_{j,k,c} = p(x_j = k \mid y = c),; k \in {1, \dots, K_j}$    
- 각 클래스 $c$에 대해 다음의 정규화 조건을 만족해야 한다: $\sum_{k=1}^{K_j} \theta_{j,k,c} = 1$
- Naive Bayes 가정하에서 다음이 성립한다:  

$$
p(\mathbf{x} \mid y = c) = \prod_{j=1}^{d} p(x_j \mid y = c) = \prod_{j=1}^{d} \theta_{j,k,c}
$$
- 학습 데이터 $(\mathbf{x}^{(i)}, y^{(i)})$가 주어졌을 때, $\theta_{j,k,c}$의 최대우도추정(MLE)은 다음과 같다:  

$$
\hat{\theta}_{j,k,c} = \frac{\sum_{i=1}^{n} \mathbf{1}(y^{(i)} = c \land x_j^{(i)} = k)}{\sum_{i=1}^{n} \mathbf{1}(y^{(i)} = c)}
$$

- 특성이 연속적인 실수값(예: 키, 몸무게)인 경우, 각 특성에 대해 클래스 조건부로 가우시안(정규) 분포를 사용하는 것이 자연스럽다.    
- 각 특성 $j$와 클래스 $c$에 대해 다음과 같이 가정한다:  

$$
p(x_j \mid y = c) = \mathcal{N}(x_j; \mu_{j,c}, \sigma_{j,c}^2)
$$
- 정규분포는 다음과 같이 정의된다:  

$$
\mathcal{N}(x; \mu, \sigma^2) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)
$$
- Naive Bayes 가정하에서 다음이 성립한다:  

$$
p(\mathbf{x} \mid y = c) = \prod_{j=1}^{d} \mathcal{N}(x_j; \mu_{j,c}, \sigma_{j,c}^2)
$$

- 학습 데이터를 사용하면 평균과 분산의 최대우도추정(MLE)은 다음과 같다:  

$$\hat{\mu}_{j,c} = \frac{\sum_{i=1}^{n} \mathbf{1}(y^{(i)} = c), x_j^{(i)}}{\sum_{i=1}^{n} \mathbf{1}(y^{(i)} = c)}$$

$$\hat{\sigma}_{j,c}^{2} = \frac{\sum_{i=1}^{n} \mathbf{1}(y^{(i)} = c), \left(x_j^{(i)} - \hat{\mu}_{j,c}\right)^2}{\sum_{i=1}^{n} \mathbf{1}(y^{(i)} = c)}$$
- 이산적인 경우와 마찬가지로, 각 특성의 분포는 각 클래스마다 독립적으로 추정된다.

### Linear Discriminant Analysis(LDA)
- 많이 쓰고 빠르고 나중에 PCA로 확장됨
- 생성 모델 측면에서 다룰 수 있고, 기하학적으로다룰 수 있는데 일반적으로 는 기하학적으로 사용
- 선형 판별 분석(Linear Discriminant Analysis, LDA)은 서로 다른 클래스들을 가장 잘 분리하는 특성들의 선형 결합을 찾는 지도학습 방법이다.    
- 기하학적으로는 클래스 간 분리를 최대화하는 방식으로 데이터를 저차원 부분공간에 투영하는 차원 축소 기법으로 볼 수 있다.    
- 그러나 확률적 관점에서 LDA는 각 클래스 내에서 데이터가 어떻게 분포하는지를 명시적으로 가정하는 생성 모델이다.    
- 이 모델의 의미를 더 잘 이해하기 위해, 가장 단순한 경우인 이진 분류 문제를 고려하자.
- 𝑝(𝒙|𝑦) 구하는게 포인트고 관건임.
- 생성적 관점은 자연스럽게 베이즈 결정 규칙으로 이어진다.    
- 생성적 프레임워크에서 분류는 사후확률을 최대화하는 클래스를 선택하여 수행된다: 

$$\arg\max_{y \in {C_1, C_2}} p(y \mid \mathbf{x}) = \arg\max_{y \in {C_1, C_2}} p(\mathbf{x} \mid y),p(y)$$
- 판별모델은 왼쪽항 생성모델은 오른쪽 항.
- 따라서 분류는 각 클래스 조건부 분포 $p(\mathbf{x} \mid y)$ 하에서 관측된 데이터 벡터 $\mathbf{x}$의 가능도와 클래스 사전확률 $p(y)$에 의해 결정된다.    
- 여기서 클래스 사전확률 $p(y)$는 일반적으로 (예: 클래스 빈도나 개수로부터) 쉽게 추정할 수 있으므로, 핵심 문제는 클래스 조건부 분포 $p(\mathbf{x} \mid y)$를 어떻게 설정할 것인가이다.
- 일반적으로는 가우시안을 이용하는것이 좋음.
- 많은 실제 문제에서 특징 벡터 $\mathbf{x}$는 연속적이며 고차원이다.    
- 연속형 데이터에 대한 생성 모델링에서 매우 일반적이고 강력한 가정은 각 클래스 조건부 분포를 다변량 가우시안(정규) 분포로 모델링하는 것이다.    
- 형식적으로 각 클래스 $C_k$에 대해 데이터는 다음과 같이 생성된다고 가정한다:

$$p(\mathbf{x} \mid y = C_k) = \mathcal{N}(\mathbf{x} \mid \boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k)$$
- 여기서 $\boldsymbol{\mu}_k$는 클래스 $C_k$의 평균 벡터이고 $\boldsymbol{\Sigma}_k$는 공분산 행렬이다.
- 공분산: 퍼져 있는 정도
- 가우시안은 원이나 타원으로 표현
- 중앙값과 어떻게 얼마나 퍼져있는정도가 있어야 가우시안을 할 수 있음
	-  공분산 값을 구해야함.
	- 부드러운 곡선(보라색 선)을 그리게 됨.
- 각 클래스 마다 이 값들을 정해서 새로운 데이터가 어디서 생성될지를 정하게 됨.
- 공분산 $\boldsymbol{\Sigma}_1$, $\boldsymbol{\Sigma}_2$가 일반적으로 다르고 공분산이 다르면(퍼져있는 정도가 다르면) 선이 곡선임.
- LDA는 서로다른 클래스의 공분산이 모두 같을 것이라는 가정을 하고 게산을 함.
- 그러면 곡선인 선이 직선으로 변함.
- 이 단계에서 중요한 관찰을 할 수 있다.    
- 각 클래스가 서로 다른 임의의 공분산 행렬 $\boldsymbol{\Sigma}_1$, $\boldsymbol{\Sigma}_2$를 갖도록 허용하면, 두 클래스 사이의 결정 경계는 일반적으로 비선형이 된다.    
- 이러한 모델은 매우 유연할 수 있지만, 더 복잡하며 데이터로부터 더 많은 수의 파라미터를 추정해야 한다.
- 공분산이 같다고 전제하면 직선으로 됨.
- 모델을 단순화하고 더 명확한 기하학적 해석을 얻기 위해 다음과 같은 핵심 가정을 도입한다: 두 클래스가 동일한 공분산 행렬을 공유한다, 즉 $\boldsymbol{\Sigma}_1 = \boldsymbol{\Sigma}_2 = \boldsymbol{\Sigma}$이다.    
- 이러한 공분산 공유 가우시안 가정 하에서, 가우시안 클래스 조건부 밀도를 베이즈 결정 규칙에 대입하면 $\mathbf{x}$에 대해 선형인 결정 함수가 도출된다.

- 선형 규칙이 되는 이유를 보기 위해 다음을 정의한다:  

$$g_k(\mathbf{x})=\log(p(\mathbf{x}\mid C_k)p(C_k))=\log p(\mathbf{x}\mid C_k)+\log p(C_k).$$

- 이제 가우시안 밀도를 대입한다. 공분산 행렬 $\Sigma$를 공유하면  

$$p(\mathbf{x}\mid C_k)=\frac{1}{(2\pi)^{D/2}|\Sigma|^{1/2}}\exp\left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^T\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu}_k)\right).$$

- 로그를 취하면 다음을 얻는다:  

$$\log p(\mathbf{x}\mid C_k)=-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^T\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu}_k)-\frac{1}{2}\log|\Sigma|-\frac{D}{2}\log(2\pi).$$

- 마지막 두 항은 클래스 인덱스 $k$에 의존하지 않으므로, 클래스를 비교할 때 서로 상쇄된다.    
- 따라서 판별함수는 다음과 같다:  

$$g_k(\mathbf{x})=-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^T\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu}_k)+\log p(C_k).$$

- 이제 두 클래스 간 분류는 다음 결정경계로 결정된다:  

$$g_1(\mathbf{x})-g_2(\mathbf{x})=-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_1)^T\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu}_1)+\log p(C_1)+\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_2)^T\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu}_2)-\log p(C_2)=0.$$

- 이차항을 전개하면  

$$ (\mathbf{x}-\boldsymbol{\mu}_k)^T\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu}_k)=\mathbf{x}^T\Sigma^{-1}\mathbf{x}-2\boldsymbol{\mu}_k^T\Sigma^{-1}\mathbf{x}+\boldsymbol{\mu}_k^T\Sigma^{-1}\boldsymbol{\mu}_k.$$

- 그러면 첫 번째 항 $\mathbf{x}^T\Sigma^{-1}\mathbf{x}$는 두 식에 공통으로 나타나 완전히 상쇄된다.
- 이러한 상쇄는 두 클래스가 동일한 공분산 행렬 $\Sigma$를 사용하기 때문에 발생한다.

- 상쇄 후에는 다음을 얻는다:  

$$g_1(\mathbf{x})-g_2(\mathbf{x})=(\boldsymbol{\mu}_1-\boldsymbol{\mu}_2)^T\Sigma^{-1}\mathbf{x}-\frac{1}{2}\left(\boldsymbol{\mu}_1^T\Sigma^{-1}\boldsymbol{\mu}_1-\boldsymbol{\mu}_2^T\Sigma^{-1}\boldsymbol{\mu}_2\right)+\log\frac{p(C_1)}{p(C_2)}=0.$$

- 따라서 결정경계는 다음과 같이 쓸 수 있다:  

$$\mathbf{w}^T\mathbf{x}+b=0,$$  $$\mathbf{w}=\Sigma^{-1}(\boldsymbol{\mu}_1-\boldsymbol{\mu}_2),$$  $$b=-\frac{1}{2}\left(\boldsymbol{\mu}_1^T\Sigma^{-1}\boldsymbol{\mu}_1-\boldsymbol{\mu}_2^T\Sigma^{-1}\boldsymbol{\mu}_2\right)+\log\frac{p(C_1)}{p(C_2)}.$$
- 공분산이 같다고 가정을 하기 때문에 선형 식이 완성이 됨.
- $w$는 $\boldsymbol{\mu}_1-\boldsymbol{\mu}_2$를 공분산으로 나눠준 값. 중요한 값이 됨.
- 분류기를 실제로 사용하려면, 이제 학습 데이터로부터 미지의 매개변수 $\boldsymbol{\mu}_1$, $\boldsymbol{\mu}_2$, $\Sigma$, 그리고 클래스 사전확률 $p(C_1)$, $p(C_2)$를 추정해야 한다.
- 이것도 최대우도추정(MLE)으로 유사하게 구할 수 있으며, 증명은 생략한다.
- 학습 집합이 

$${(\mathbf{x}^{(n)},y^{(n)})}_{n=1}^N,\quad y^{(n)}\in{C_1,C_2}$$
- 각 클래스의 평균은 해당 클래스에 속한 표본들의 표본평균으로 추정한다:  

$$\hat{\boldsymbol{\mu}}_k=\frac{1}{N_k}\sum_{n\in C_k}\mathbf{x}^{(n)}.$$

- LDA는 두 클래스가 동일한 공분산 행렬을 공유한다고 가정하므로, 각 클래스별로 공분산을 따로 추정할 필요가 없다.
- 대신 다음과 같은 풀드 공분산(pooled covariance) 추정치를 사용한다: 

$$\hat{\Sigma}=\frac{1}{N}\sum_{k=1}^{2}\sum_{n\in C_k}\left(\mathbf{x}^{(n)}-\hat{\boldsymbol{\mu}}_k\right)\left(\mathbf{x}^{(n)}-\hat{\boldsymbol{\mu}}_k\right)^T.$$

- 클래스 사전확률은 클래스 비율로 간단히 추정할 수 있다:  

$$p(C_k)=\frac{N_k}{N}.$$



- 위에서 구한 추정치를 다음 식에 대입하면  

$$\hat{\mathbf{w}}=\hat{\Sigma}^{-1}(\hat{\boldsymbol{\mu}}_1-\hat{\boldsymbol{\mu}}_2),$$  
$$\hat{b}=-\frac{1}{2}\left(\hat{\boldsymbol{\mu}}_1^T\hat{\Sigma}^{-1}\hat{\boldsymbol{\mu}}_1-\hat{\boldsymbol{\mu}}_2^T\hat{\Sigma}^{-1}\hat{\boldsymbol{\mu}}_2\right)+\log\frac{p(C_1)}{p(C_2)}.$$

- 따라서 추정된 선형 결정 규칙은 다음과 같다:
- 새로운 관측치 $\mathbf{x}$에 대해 아래 식이 참이면 $C_1$로 분류한다.

$$\hat{\mathbf{w}}^T\mathbf{x}+\hat{b}>0$$

- 그렇지 않으면 $C_2$로 분류한다.

### Fisher’s Linear Discriminant Analysis
- 기하학적인 해석
	- LDA는 2개의 변수가 그려진 2차 평면에 선을 그었을때 투영된 각각 변수들이 잘 구분되는가를 확인
	- 투영: 90도로 선을 내린것. 아래 슬라이드 확인
- 선형 판별 분석(LDA)의 생성적 해석을 바탕으로, 이제 Ronald A. Fisher가 제안한 Fisher의 선형 판별(Fisher’s Linear Discriminant)을 고려한다.    
- 가우시안–베이지안 접근법은 공분산이 공유된다는 가정 하에 선형 결정경계를 유도하는 반면, Fisher는 문제를 기하학적으로 정식화하였다.    
- 흥미롭게도 동일한 가정(이진 분류의 경우) 하에서, 두 접근법은 동일한 최적 투영 방향을 도출한다.
- LDA는 2차원 평면에 1차원 낮은 1차원 선을 그림
	- 1차원일 필요는 없고 고차원에서는 다른 차원을 낮춰서 그림.
	- PCA와 비슷하지만 조금은 다름. 다만 목적은 같음
	- LDA는 지도학습에 더 특화된 PCA 느낌 정도로 이해
- LDA는 투영되는 최적의 선을 찾는 문제.
	- 선은 어떻게 찾을까? -> 아래 슬라이드
- $\mathbb{R}^D$ 공간의 데이터를 하나의 방향 $\mathbf{w}$로 투영한다고 가정하자.    
- Fisher의 LDA의 핵심 질문은 다음과 같다: 투영 이후 두 클래스가 최대한 잘 분리되도록 하려면 어떤 방향 $\mathbf{w}$를 선택해야 하는가?    
- 차원을 줄이면 정보 손실은 불가피하지만, 적절히 선택된 $\mathbf{w}$는 클래스 분리에 가장 중요한 정보를 최대한 보존한다.
- 두 클래스 문제를 고려하자. 클래스 $C_1$에서 $N_1$개의 샘플, 클래스 $C_2$에서 $N_2$개의 샘플이 있다. 
- 원래 공간에서의 클래스 평균 벡터는 다음과 같다: 

$$\boldsymbol{\mu}_1=\frac{1}{N_1}\sum_{n\in C_1}\mathbf{x}^{(n)},\quad \boldsymbol{\mu}_2=\frac{1}{N_2}\sum_{n\in C_2}\mathbf{x}^{(n)}.$$

- 방향 $\mathbf{w}$로 투영하면 각 데이터는 다음과 같이 변환된다:  

$$y^{(n)}=\mathbf{w}^T\mathbf{x}^{(n)}.$$

- 투영 이후 클래스 평균은 다음과 같이 된다: 
	- m1,m2는 투영된 값의 중간값이라고 생각하면 됨.

$$m_1=\mathbf{w}^T\boldsymbol{\mu}_1,\quad m_2=\mathbf{w}^T\boldsymbol{\mu}_2.$$



- 투영 이후 클래스 분리를 측정하는 간단한 방법은, 투영된 클래스 평균의 차이를 보는 것이다:

$$m_2-m_1=\mathbf{w}^T(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1).$$
- 평균값의 차이가 크면 둘을 잘 구분한다고 볼 수 있음

- 그래서 이에 따라 다음 목적함수(loss 함수라고 해도 됨)를 정의할 수 있다:  

$$\mathcal{L}(\mathbf{w})=\mathbf{w}^T(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1).$$

- 이 값은 $\mathbf{w}$ 방향으로 투영한 뒤 두 클래스 중심이 얼마나 떨어져 있는지를 나타낸다. 이 값을 크게 만들면 투영된 클래스 평균들이 더 멀어지므로, 이는 우리가 원하는 바와 정확히 일치한다.
- 처음에는 단순히 $\mathcal{L}(\mathbf{w})$를 최대화하면 될 것처럼 보인다. 그러나 여기에는 미묘하지만 중요한 문제가 있다.
- $\mathbf{w}$에 임의의 상수 $c>0$를 곱하면 다음을 얻는다:  

$$\mathcal{L}(c\mathbf{w})=(c\mathbf{w})^T(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1)=c\mathbf{w}^T(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1).$$

- 사실 w는 방향이 중요함.
	- 조금 왼쪽에 있으나 오른쪽에 있으나 투영하면 같음.
- 지금까지 w값은 미분해서 0이 되는 값을 찾거나 안되면 경사하강법으로 계산해왔음
- 이번 케이스는 제약이 있는 목적함수 임.
	- 제약이 없으면 C가 무한히 커지면 L도 무한히 커짐
	- $w^𝑇w$ = 1.로 제한함.

- 목적함수는 $\mathbf{w}$의 크기에 대해 선형적으로 증가한다.
- 즉, 방향은 그대로 두고 $\mathbf{w}$의 크기만 크게 하면 값을 임의로 크게 만들 수 있다.
- 다시 말해, 아무 제약 없이 $\mathcal{L}(\mathbf{w})$를 최대화하는 것은 최적의 “방향”을 찾는 데 도움이 되지 않고, 단지 $\mathbf{w}$를 무한히 크게 만드는 결과를 초래한다.
- 이를 해결하기 위해 **$\mathbf{w}$의 길이를 1로 제한**한다:  

$$\mathbf{w}^T\mathbf{w}=1.$$
- 그러면 문제는 다음과 같이 바뀐다:  

$$\max_{\mathbf{w}}\ \mathbf{w}^T(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1)\quad \text{subject to}\quad \mathbf{w}^T\mathbf{w}=1.$$

- 이는 제약 조건이 있는 최적화 문제의 한 예이다.

- 이러한 문제를 체계적으로 풀기 위해 라그랑주 승수법을 사용한다:  

$$\mathcal{L}(\mathbf{w},\lambda)=\mathbf{w}^T(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1)-\lambda(\mathbf{w}^T\mathbf{w}-1).$$

- $\mathbf{w}$에 대해 미분하고 0으로 두면  

$$\boldsymbol{\mu}_2-\boldsymbol{\mu}_1=2\lambda \mathbf{w}.$$

- 따라서  

$$\mathbf{w}\propto \boldsymbol{\mu}_2-\boldsymbol{\mu}_1.$$
- $\mu_1, \mu_2$의 평균값을 그래프에서 이으면 w의 최적 방향이 나온다고 볼 수있음

- 이 결과는 직관적으로도 타당하다: 두 클래스의 평균 벡터를 잇는 방향으로 투영하면 클래스 간 거리가 최대화되므로, 이 방향이 좋은 분리 방향이 될 수 있다.    
- 그러나 여전히 문제가 남아 있다: 원래 공간에서는 잘 분리된 클래스라도, 평균을 잇는 직선으로 투영하면 크게 겹칠 수 있으며, 특히 클래스 분포의 공분산이 큰 경우 더욱 그렇다.    
- 이에 따라 Ronald A. Fisher는 평균 간 분리와 클래스 내부 분산을 동시에 고려하는 기준을 도입하였다.
- 데이터는 같은데 오른쪽 그림이 더 좋은 분류임 -> 피셔의 주장
	- 단순히 투영되었을때 값이 큰것이 답이 아님.
	- 투영되었을 때 내부 분산을 작게 만들어 줘야 더 좋은 분류 모델이 나온다.
	- 이걸 within-class variance라고 함.
- 평균의 차는 크고 within-class variance는 작게 만드는게 Fisher’s Linear 목적

- 클래스 $C_k$에 속한 변환된 데이터의 클래스 내 분산은 다음과 같이 정의된다:  

$$s_k^2=\sum_{n\in C_k}(y^{(n)}-m_k)^2.$$

- 전체 데이터에 대한 클래스 내 분산은 단순히 $s_1^2+s_2^2$로 정의할 수 있다.
- Fisher 기준은 (두 클래스의 경우) 클래스 간 분산과 클래스 내 분산의 비율로 정의되며 다음과 같다:

$$J(\mathbf{w})=\frac{(m_2-m_1)^2}{s_1^2+s_2^2}.$$

- m2-m1에서 목적함수가 바뀜
	- 분모에 $s^2_1+s^2_2$들어감.

- 위의 식을 벡터에 적용하면 이렇게 식을 쓸 수 있음.
- 이 기준은 between-class scatter 행렬 $\mathbf{S}_B$와 within-class scatter 행렬 $\mathbf{S}_W$를 사용하여 다음과 같이 행렬 형태로 쓸 수 있다:  

$$J(\mathbf{w})=\frac{\mathbf{w}^T\mathbf{S}_B\mathbf{w}}{\mathbf{w}^T\mathbf{S}_W\mathbf{w}}.$$

- 여기서  

$$\mathbf{S}_B=(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1)(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1)^T,$$  
$$\mathbf{S}_W=\sum_{n\in C_1}(\mathbf{x}^{(n)}-\boldsymbol{\mu}_1)(\mathbf{x}^{(n)}-\boldsymbol{\mu}_1)^T+\sum_{n\in C_2}(\mathbf{x}^{(n)}-\boldsymbol{\mu}_2)(\mathbf{x}^{(n)}-\boldsymbol{\mu}_2)^T.$$

- 이번에도 미분하고 값이 0이 되는 값을 찾을 것임.
- $J(\mathbf{w})$를 $\mathbf{w}$에 대해 미분하고 0으로 두면 다음을 얻는다:  

$$\frac{\partial J(\mathbf{w})}{\partial \mathbf{w}}=\frac{2\mathbf{S}_B\mathbf{w}(\mathbf{w}^T\mathbf{S}_W\mathbf{w})-2\mathbf{w}^T\mathbf{S}_B\mathbf{w},\mathbf{S}_W\mathbf{w}}{(\mathbf{w}^T\mathbf{S}_W\mathbf{w})^2}=0,$$  

$$\mathbf{w}^T\mathbf{S}_B\mathbf{w},\mathbf{S}_W\mathbf{w}=\mathbf{w}^T\mathbf{S}_W\mathbf{w},\mathbf{S}_B\mathbf{w}.$$

- 따라서 다음을 얻는다:  

$$\frac{\mathbf{w}^T\mathbf{S}_B\mathbf{w}}{\mathbf{w}^T\mathbf{S}_W\mathbf{w}}\mathbf{w}=\mathbf{S}_W^{-1}\mathbf{S}_B\mathbf{w}.$$


- 위에서 얻은 스칼라 값을 대입하면 다음을 얻는다:  
    $$\lambda \mathbf{w}=\mathbf{S}_W^{-1}\mathbf{S}_B\mathbf{w}.$$
    
- 이는 일반화된 고유값 문제(generalized eigenvalue problem)의 형태이다.    
- 따라서 $J(\mathbf{w})$를 최대화하려면, $\mathbf{w}$는 $\mathbf{S}_W^{-1}\mathbf{S}_B$의 가장 큰 고유값 $\lambda$에 대응하는 고유벡터가 되어야 한다.
- eigenvalue problem은 선형대수 마지막챕터에 보통 나오는데 그방법으로 풀면 됨.


- 이진 분류의 경우, 위의 고유값 문제는 크게 단순화된다:  

$$\lambda \mathbf{w}=\mathbf{S}_W^{-1}\mathbf{S}_B\mathbf{w}=\mathbf{S}_W^{-1}(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1)(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1)^T\mathbf{w}.$$

- 이로부터 다음을 얻는다:  

$$\mathbf{w}\propto \mathbf{S}_W^{-1}(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1).$$

- 따라서 이진 분류에서 Fisher의 선형 판별은 닫힌 형태 해를 가지며, 최적의 투영 방향은 클래스 평균 차이에 클래스 내 산포 행렬의 역행렬을 적용하여 얻어진다.


- 이 결과는 생성적 LDA 해석과도 연결된다.    
- 공분산 행렬 $\Sigma$를 공유하는 가우시안 모델에서, 공통 공분산의 최대우도추정치는 클래스 내 산포 행렬에 비례한다: 

$$\Sigma=\frac{1}{N_1+N_2}\mathbf{S}_W.$$

- 따라서 투영 방향은 다음과 같이 된다:  

$$\mathbf{w}\propto \Sigma^{-1}(\boldsymbol{\mu}_2-\boldsymbol{\mu}_1).$$

- 이는 생성적 접근법에서 얻은 결과와 정확히 동일한 방향이다.
- 클래스가 두 개보다 많은 경우에도 Fisher 판별의 기본 아이디어는 동일하다.    
- 즉, 클래스 간 분리는 크게 하고 각 클래스 내부 데이터는 최대한 밀집되도록 하는 방향을 찾고자 한다.    
- 그러나 다중 클래스 문제에서는 데이터가 고차원 공간에서 여러 방향으로 퍼져 있을 수 있다.   
- 따라서 하나의 투영 벡터만으로는 모든 클래스를 효과적으로 분리하기에 충분한 정보를 담지 못할 수 있다.


- 이러한 이유로 Fisher의 방법은 하나의 방향이 아니라 여러 개의 투영 방향을 찾는 방식으로 확장된다. 이러한 방향들을 판별 벡터(discriminant vectors)라고 한다.    
- 이제 데이터는 하나의 직선이 아니라, 이 벡터들로 이루어진 저차원 부분공간으로 투영된다.    
- 클래스가 $K$개일 때, 찾을 수 있는 유효한 판별 방향의 최대 개수는 다음과 같다:  
$$K-1.$$

- between-class scatter 행렬 $\mathbf{S}_B$는 각 클래스 평균이 전체 평균으로부터 얼마나 떨어져 있는지를 측정한다.
- 다중 클래스의 경우 다음과 같이 정의된다:  

$$\mathbf{S}_B=\sum_{k=1}^{K} N_k(\boldsymbol{\mu}_k-\boldsymbol{\mu})(\boldsymbol{\mu}_k-\boldsymbol{\mu})^T.$$
- 여기서 $N_k$는 클래스 $C_k$의 샘플 수, $\boldsymbol{\mu}_k$는 클래스 $C_k$의 평균 벡터, $\boldsymbol{\mu}$는 전체 데이터의 평균 벡터이다.


- within-class scatter 행렬 $\mathbf{S}_W$는 각 클래스 내부에서 데이터가 클래스 평균 주변에 얼마나 퍼져 있는지를 측정한다.
- 다음과 같이 정의된다:  

$$\mathbf{S}_W=\sum_{k=1}^{K}\sum_{n\in C_k}(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)(\mathbf{x}^{(n)}-\boldsymbol{\mu}_k)^T.$$
- 여기서 $n\in C_k$는 클래스 $C_k$에 속한 샘플들을 의미한다.
- 목표는 데이터를 저차원 공간으로 사상하는 투영 행렬 $\mathbf{W}$를 찾아, 클래스 간 산포는 최대화하고 클래스 내 산포는 최소화하는 것이다.
- 이는 다음과 같은 일반화된 고유값 문제로 이어진다:  

$$\mathbf{S}_W^{-1}\mathbf{S}_B\mathbf{w}=\lambda \mathbf{w}.$$

- 여기서 $\lambda$는 고유값, $\mathbf{w}$는 해당 고유값에 대응하는 고유벡터이다.
- 다중 클래스의 경우, 가장 큰 $K-1$개의 고유값에 대응하는 고유벡터들이 클래스 분리를 최대화하는 방향이 되며, 이 벡터들이 $\mathbf{W}$의 열을 이룬다.

- 투영 행렬 $\mathbf{W}$를 구한 후, 데이터를 다음과 같이 새로운 공간으로 투영할 수 있다:  

$$\mathbf{Z}=\mathbf{W}^T\mathbf{X}.$$

- $\mathbf{Z}$의 각 열은 각각의 샘플에 대한 저차원 표현을 의미한다.
- 2차원 문제에선 w가 숫자로 나왔는데, 고차원에서는 W가 매트릭스임. 
	- 그래서 원하는 차원으로 축소 가능
- 이후 이 축소된 공간에서 임계값 기반 분류나 최근접 이웃, Support Vector Machine과 같은 다양한 분류 알고리즘을 적용할 수 있다.

### Linear Discriminant Analysis versus Principal Component Analysis
- LDA(Linear Discriminant Analysis)는 지도학습 기반 차원 축소 기법으로, 클래스 레이블을 활용하여 서로 다른 클래스 평균 간 거리는 크게 하고, 각 클래스 내부의 분산은 작게 만드는 방향을 찾는다.    
- Principal Component Analysis와 같은 방법과 달리, LDA는 데이터의 전체 분산 보존이 아니라 클래스 간 분리도를 향상시키는 데 목적이 있다.
- PCA는 주로 비지도학습에서 많이 사용
	- 차원 축소라는 강력한 기능이 있음
	- maxmizes variance 방법으로 차원을 축소
- LDA는 분류를 잘하기 위한 방법으로 차원을 축소함.
	- maxmizes class separation
	- 그래서 아웃풋이 있어야 함.
	- 그 아웃풋을 토대로 2그룹에 평균도 구하고 분산도 구해서 계산을 할 수 있음.