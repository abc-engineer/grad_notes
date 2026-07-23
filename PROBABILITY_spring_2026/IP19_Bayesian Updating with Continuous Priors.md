2026-05-07 08:20
## 19강 Bayesian Updating with Continuous Priors




### Learning Goals
- 매개변수화된 분포족을 관측 데이터에 대한 연속적인 범위의 가설을 나타내는 것으로 이해한다.
- 연속 밀도에 대한 베이즈 정리와 전체 확률 법칙을 진술할 수 있다.    
- 데이터와 가능도 함수가 주어졌을 때 베이즈 정리를 적용하여 사전 확률밀도함수를 사후 확률밀도함수로 갱신할 수 있다.    
- 사후 예측 확률을 해석하고 계산할 수 있다.

### Introduction
- 지금까지 우리는 **유한**한 수의 가설이 있을 때만 베이즈 갱신을 다루었다. 예를 들어 주사위 예제에는 다섯 가지 가설, 즉 면의 수가 $4, 6, 8, 12, 20$개인 경우가 있었다.  
- 이제 우리는 **continuous range of hypotheses_연속적인 범위의 가설**이 있을 때의 베이즈 갱신을 공부할 것이다.  
- 베이즈 갱신 과정은 본질적으로 이산적인 경우와 동일할 것이다.  
- 늘 그렇듯이 이산에서 연속으로 이동할 때는 확률질량함수를 확률밀도함수로, 합을 적분으로 바꾸어야 한다.

- 개념은 discrete과 유사하지만 수식이 복잡해짐

- 이 수업의 처음 몇 개 섹션은 pdf(probability density function)를 다루는 데 집중한다.    
- 특히 전체 확률의 법칙과 베이즈 정리를 다룰 것이다.    
- 우리는 이것들이 본질적으로 이산(discrete) 버전과 동일하다는 점에 집중할 것을 권장한다.    
- 그 후에는 베이즈 정리와 전체 확률의 법칙을 베이지안 업데이트(Bayesian updating)에 적용할 것이다.

### Examples with continuous ranges of hypotheses
- 다음은 연속적인 가설 범위를 가지는 세 가지 표준 예시이다.    
- 어떤 시스템이 성공하거나 실패할 확률이 $p$라고 하자.    
- 그러면 우리는 $p$가 구간 $[0,1]$ 어디에나 있을 수 있다고 가설을 세울 수 있다.    
- 즉, 우리는 연속적인 가설 범위를 가진다.    
- 우리는 이 예시를 앞면이 나올 확률 $p$를 알 수 없는 ‘치우친(bent)’ 동전으로 자주 모델링한다.

#### Example
- 어떤 동위원소의 수명은 지수분포 $\mathrm{exp}(\lambda)$로 모델링된다.    
- 원칙적으로 평균 수명 $\frac{1}{\lambda}$는 $(0,\infty)$의 어떤 실수도 될 수 있다.
#### Example
- 우리는 하나의 매개변수(parameter)에만 제한되지 않는다.    
- 원칙적으로 정규분포의 매개변수 $\mu$와 $\sigma$는 각각 $(-\infty,\infty)$와 $(0,\infty)$의 어떤 실수도 될 수 있다.    
- 만약 단태아(single births)의 임신 기간을 정규분포로 모델링한다면, 수백만 개의 데이터로부터 $\mu$는 약 40주이고 $\sigma$는 약 1주라는 것을 알고 있다.

- 이 모든 예시에서 우리는 데이터를 생성하는 확률 과정을 매개변수(parameter)를 가지는 분포, 즉 매개변수화된 분포(parameterized distribution)로 모델링하였다.    
- 매개변수의 가능한 모든 선택이 하나의 가설이 된다. 예를 들어 첫 번째 예시에서는 성공 확률이 $p=0.7313$이라고 가설을 세울 수 있다.    
- 우리는 $0$과 $1$ 사이의 어떤 값도 취할 수 있기 때문에 연속적인 가설 집합을 가진다.

### Parameterized models
- 위의 예시들처럼 우리의 가설은 종종 “어떤 매개변수가 값 $\theta$를 가진다( form a certain parameter has value θ.)”의 형태를 가진다.    
- 우리는 arbitrary hypothesis(임의의 가설)을 나타내기 위해 문자 $\theta$를 자주 사용할 것이다.    
- 이렇게 하면 $p$, $f$, $x$ 같은 기호들은 각각 pmf, pdf, 데이터라는 원래 의미로 사용할 수 있다.    
- 또한 “관심 있는 매개변수가 값 $\theta$를 가진다는 가설”이라고 말하는 대신 단순히 “가설 $\theta$”라고 말할 것이다.

- θ는 확률·통계에서 보통 **모르는 parameter** 를 나타낼 때 사용

### Big and little letters
- 우리는 결과와 확률에 대해 서로 대응되는 두 가지 표기법을 가진다.    
- 1. 대문자: Event(사건) $A$, 확률 함수 $P(A)$    
- 2. 소문자: Value $x$, pmf $p(x)$ 또는 pdf $f(x)$    
- 이러한 표기법은  아래와 같이 연결된다. 여기서 $x$는 이산 확률변수 $X$의 값이고, ‘$X=x$’는 그에 대응하는 사건이다.

$$  
P(X=x)=p(x)  
$$  

- 우리는 이러한 표기법을 베이지안 업데이트에 사용되는 확률에도 그대로 적용한다.
- 대문자: 가설 $H$와 데이터 $D$로부터 여러 관련 확률 을 계산한다.
	- 데이터와 가설도 대문자로 씀 → 이벤트에 가깝기 때문

$$  
P(H),\; P(D),\; P(H\mid D),\; P(D\mid H)  
$$


- 동전 예시

$$  
H_{0.6}=\text{‘선택된 동전의 앞면 확률이 }0.6\text{이다’}  
$$  

$$  
D=\text{‘3번 던진 결과가 HHT였다’}  
$$  

$$  
P(D\mid H_{0.6})=(0.6)^2(0.4)  
$$  




- 소문자: 가설 값(Hypothesis values) $\theta$와 데이터 값 $x$는 모두 확률 또는 확률밀도를 가진다.  

$$  
p(\theta),\; p(x),\; p(\theta\mid x),\; p(x\mid \theta)  
$$ 

$$  
f(\theta),\; f(x),\; f(\theta\mid x),\; f(x\mid \theta)  
$$

- 동전 예시에서는 $\theta=0.6$이고 $x$는 수열 $1,1,0$일 수 있다. 따라서  $p(x\mid \theta)=(0.6)^2(0.4)$  가 된다.
- 또한 $\theta$와 $x$의 값을 강조하기 위해  $p(x=1,1,0\mid \theta=0.6)$  라고 쓸 수도 있다.
- 앞으로도 두 종류의 표기법을 모두 사용하겠지만, 이후에는 주로 pmf와 pdf를 사용하는 소문자 표기법을 사용할 것이다.
- 가설은 보통 그리스 문자  로 나타내고

$$  
\theta,\lambda,\mu,\sigma,\dots  
$$  

- 데이터 값은 보통 영어 문자  로 나타낼 것이다.

$$  
x,x_i,y,\dots  
$$  


### Quick review of pdf and probability
- $X$가 pdf $f(x)$를 가지는 확률변수라고 하자.
- $f(x)$는 밀도(density)이며, 단위는 확률/($x$의 단위)임을 떠올리자.
- $X$의 값이 $[c,d]$ 안에 있을 확률은 다음으로 주어진다.  

$$  
\int_c^d f(x),dx  
$$


- $X$가 $x$ 주변의 무한소 범위 $dx$ 안에 있을 확률은 $f(x)\,dx$이다.
- 사실 적분 공식은 이러한 무한소 확률들의 ‘합’일 뿐이다.
- 우리는 적분을 $f(x)$ 그래프 아래의 넓이로 봄으로써 이러한 확률들을 시각화할 수 있다.
- 이후에 밀도 대신 확률을 조작하기 위해, $f(x)\,dx$가 $x$ 주변의 폭 $dx$인 무한소 범위 안에 $X$가 있을 확률이라는 개념을 자주 사용할 것이다.

### Continuous priors, discrete likelihoods
- 베이지안 프레임워크에서는 **가설의 확률**인 사전확률(prior probability)과 사후확률(posterior probability), 그리고 가설이 주어졌을 때 **데이터의 확률**인 가능도(likelihood)를 다룬다.
- 이전 수업들에서는 가설과 데이터 모두 이산적인 값의 범위를 가졌다.
- 서론에서 보았듯이 우리는 연속적인 가설 범위를 가질 수도 있다.
- 데이터에 대해서도 마찬가지이지만, _오늘은 데이터가 오직 이산적인 값들만 가질 수 있다고 가정할 것이다._
- 이 경우 가설 $\theta$가 주어졌을 때 데이터 $x$의 가능도는 pmf를 사용하여  

$$  
p(x\mid \theta)  
$$  

로 쓴다.


#### 참고
- 베이즈 정리 용어는 아래처럼 정리할 수 있다:  

$$  
P(H\mid D)=\frac{P(D\mid H)P(H)}{P(D)}  
$$  

| 기호           | 한국어         | 영어                              | 의미                       |     |
| ------------ | ----------- | ------------------------------- | ------------------------ | --- |
| $H$          | 가설          | Hypothesis                      | 확인하려는 주장                 |     |
| $D$          | 데이터, 증거     | Data / Evidence                 | 관찰된 결과                   |     |
| $P(H)$       | 사전확률        | Prior probability               | 데이터를 보기 전 $H$가 맞다고 믿는 확률 |     |
| $P(D\mid H)$ | 가능도         | Likelihood                      | $H$가 맞다고 할 때 $D$가 나올 확률  |     |
| $P(D)$       | 증거확률 / 주변확률 | Evidence / Marginal probability | 전체적으로 $D$가 나올 확률         |     |
| $P(H\mid D)$ | 사후확률        | Posterior probability           | 데이터를 본 후 $H$가 맞다고 믿는 확률  |     |

- 핵심은 다음이다:  

$$  
\text{Posterior\,\_사후확률}=\frac{\text{Likelihood\,\_가능도}\times\text{Prior\,\_사전확률}}{\text{Data/ Evidence\,\_증거확률}}  
$$

- 즉, 처음 믿음인 사전확률을 새로운 데이터의 가능도로 업데이트한 결과가 사후확률이다.
- 우리는 이러한 개념들을 설명하기 위해 다음 동전 예시를 사용할 것이다.  
- 이어지는 각 섹션에서 이 예시를 계속 사용할 것이다.
#### Example (Bent coin 치우친 동전)
- 앞면이 나올 확률이 알려지지 않은 $\theta$인 치우친 동전이 있다고 하자.
- 이 경우 우리는 그 동전이 ‘$\theta$형(type $\theta$)’이라고 말하고, 임의의 동전이 $\theta$형이라는 가설을 $H_\theta$로 표시할 것이다.
- $\theta$의 값은 무작위이며 $0$과 $1$ 사이 어디에나 있을 수 있다.
- 이 예시와 뒤따르는 예시들에서는 $\theta$의 값이 연속 사전확률밀도 $f(\theta)=2\theta$를 가지는 분포를 따른다고 가정할 것이다.
- 동전을 던지는 것은 앞면에 대해 $x=1$, 뒷면에 대해 $x=0$인 두 결과만 가지므로 이산 가능도를 가진다.  

$$  
p(x=1\mid H_\theta)=\theta,\qquad p(x=0\mid H_\theta)=1-\theta  
$$

- 앞서 말했듯이 우리는 가설 $H_\theta$를 종종 $\theta$로 쓸 것이다.
- 따라서 위의 확률들은 다음과 같이 된다.  

$$  
p(x=1\mid \theta)=\theta,\qquad p(x=0\mid \theta)=1-\theta  
$$

#### Think:
- 우리는 연속적인 동전 유형의 범위를 가진다. 즉, 매개변수 $\theta$의 값으로 유형을 식별한다.
- 우리는 무작위로 동전을 선택할 수 있고, 선택된 유형은 확률밀도 $f(\theta)$를 가진다.
- 이전 수업에서 다룬 이산 예시들이 이와 유사하다는 점을 보면 도움이 될 수 있다.
- 한 예시에서는 앞면이 나올 확률이 $0.5$, $0.6$, 또는 $0.9$인 세 가지 유형의 동전이 있었다.
- 그래서 우리는 가설을 $H_{0.5}$, $H_{0.6}$, $H_{0.9}$라고 불렀고, 이들은 각각 $P(H_{0.5})$ 등의 사전확률을 가졌다.
- 다시 말해, 앞면 확률이 알려지지 않은 동전 유형이 있었고, 그 확률에 대한 가설들이 있었으며, 각 가설은 사전확률을 가졌다.

### The law of total probability
- 연속 확률분포에 대한 전체 확률의 법칙은 본질적으로 이산분포의 경우와 같다.
- 사전 pmf를 사전 pdf로 바꾸고, 합을 적분으로 바꾼다.
- 먼저 이산적인 경우의 법칙을 복습하자.
- 이산적인 가설 집합 $H_1,H_2,\dots,H_n$에 대해 전체 확률의 법칙은 다음과 같다.  

$$  
P(D)=\sum_{i=1}^n P(D\mid H_i)P(H_i)  
$$

- 이것은 prior probability 사전확률 $P(H_i)$를 사용했기 때문에 $D$의 전체 prior probability 사전확률이다.
- 보통 $P(D$)는 prior를 반영해서 계산한 데이터의 사전예측확률(prior predictive probability) 또는 evidence라고 함.
- $P(D$): **각 가설이 맞을 확률** $\times$ **그 가설 아래에서 데이터가 나올 확률**을 모두 더한 것


- 가설에 대해 $\theta_1,\theta_2,\dots,\theta_n$을 쓰고 데이터에 대해 $x$를 쓰는 소문자 표기법에서 전체 확률의 법칙은 다음과 같이 쓴다.  

$$  
p(x)=\sum_{i=1}^n p(x\mid \theta_i)p(\theta_i)  
$$

- 우리는 이것을 가설 $\theta$의 사전확률과 구별하기 위해 결과 $x$의 사전예측확률(prior predictive probability)이라고도 불렀다.

- 마찬가지로 연속 pdf에 대한 전체 확률의 법칙이 있다. 이를 소문자 표기법을 사용하여 정리로 진술하자.
#### Theorem (Law of total probability.) 정리(전체 확률의 법칙)
- 연속 매개변수 $\theta$가 범위 $[a,b]$에 있고, 이산 확률 데이터 $x$가 있다고 하자.
- $\theta$ 자체가 밀도 $f(\theta)$를 가지는 확률변수이고, $x$와 $\theta$가 가능도 $p(x\mid \theta)$를 가진다고 가정하자.
- 이 경우 $x$의 전체 확률은 다음 공식으로 주어진다.  

$$  
p(x)=\int_a^b p(x\mid \theta)f(\theta)\,d\theta  
$$

#### Proof.
- 우리의 증명은 이산 버전과의 유추(analogy)에 기반한다.  

$$  
p(x)=\sum_{i=1}^n p(x\mid \theta_i)p(\theta_i)  
$$

- 확률 항  $p(x\mid \theta)f(\theta)\,d\theta$는 위 식의 항 $p(x\mid \theta_i)p(\theta_i)$와 완전히 대응된다.
- 이러한 유추를 계속 따르면, 위 식의 합은 다음 식의 적분으로 바뀐다.

$$  
p(x)=\int_a^b p(x\mid \theta)f(\theta)\,d\theta  
$$

- 이산적인 경우와 마찬가지로, $\theta$를 데이터의 확률을 설명하는 가설로 생각할 때 우리는 $p(x)$를 $x$의 사전예측확률(prior predictive probability)이라고 부른다.
#### Example (Law of total probability.)
- 치우친 동전 예시를 계속 살펴보자.
- 앞면이 나올 확률이 $\theta$인 치우친 동전이 있다.
- $\theta$의 값은 구간 $[0,1]$에서 사전 pdf  $f(\theta)=2\theta$를 가지는 확률변수이다.
- 이제 동전을 한 번 던지려고 한다고 하자.
- 앞면이 나올 전체 확률, 즉 앞면의 사전예측확률은 무엇인가?

#### Solution
- 치우친 동전 예시에서 우리는 가능도가  $p(x=1\mid \theta)=\theta$  and $p(x=0\mid \theta)=1-\theta$  임을 보았다.
- 따라서 $x=1$의 전체 확률은  

$$  
p(x=1)=\int_0^1 p(x=1\mid \theta)f(\theta)\,d\theta  
$$  

$$  
=\int_0^1 \theta\cdot 2\theta\,d\theta  
$$  

$$  
=\int_0^1 2\theta^2\,d\theta  
$$  

$$  
=\frac{2}{3}  
$$  

- 사전분포가 더 큰 앞면 확률에 가중되어 있으므로, 앞면의 전체 확률 역시 더 크게 나타난다.

### Bayes’ theorem for continuous probability densities
- 연속 pdf에 대한 베이즈 정리의 진술은 본질적으로 pmf의 경우와 동일하다.
- 우리는 실제 확률이 되도록 $d\theta$를 포함하여 이를 진술한다.
#### Theorem(Bayes's Theorem_베이즈 정리)
- 전체 확률의 법칙과 동일한 가정을 사용하자. 즉, $\theta$는 범위 $[a,b]$를 가지는 연속 매개변수이며 pdf $f(\theta)$를 가진다. 또한 $x$는 이산적인 랜덤 데이터이고, 둘은 함께 가능도 $p(x\mid \theta)$를 가진다.
- 이러한 가정하에서:  

$$f(\theta\mid x)\,d\theta=\frac{p(x\mid \theta)f(\theta)\,d\theta}{p(x)}=\frac{p(x\mid \theta)f(\theta)\,d\theta}{\int_a^b p(x\mid \theta)f(\theta)\,d\theta}$$


#### Proof.
- 이것은 확률에 대한 진술이므로, 단순히 베이즈 정리의 일반적인 형태를 사용한 것이다.
- 이는 충분히 중요하므로 조금 더 형식적으로 설명하자.
- $\Theta$를 값 $\theta$를 생성하는 확률변수라고 하자.
- 사건  

$$  
H=\text{‘}\Theta\text{가 값 }\theta\text{ 주변 폭 }d\theta\text{인 구간 안에 있다’}  
$$  

와  

$$  
D=\text{‘데이터의 값이 }x\text{이다’}  
$$  

를 생각하자.

- 그러면  

$$  
P(H)=f(\theta)\,d\theta,\qquad P(D)=p(x),\qquad P(D\mid H)=p(x\mid \theta)  
$$  

- 이제 베이즈 정리의 일반적인 형태는 다음과 같이 된다.  

$$f(\theta\mid x),d\theta=P(H\mid D)=\frac{P(D\mid H)P(H)}{P(D)}=\frac{p(x\mid \theta)f(\theta),d\theta}{p(x)}$$



#### Proof.
- 이 방정식의 첫 항과 마지막 항을 보면 베이즈 정리의 새로운 형태를 볼 수 있다.
- 마지막으로, 우리는 베이즈 정리의 진술에서 $d\theta$ 인자를 유지하는 것이 확률에 대해 신중하게 생각하는 데 더 도움이 된다고 굳게 믿는다.
- 하지만 $d\theta$가 양변의 분자에 나타나기 때문에 많은 사람들은 $d\theta$를 생략하고 베이즈 정리를 밀도에 대한 식으로 다음과 같이 쓴다.  

$$  
f(\theta\mid x)=\frac{p(x\mid \theta)f(\theta)}{p(x)}  
=\frac{p(x\mid \theta)f(\theta)}{\int_a^b p(x\mid \theta)f(\theta),d\theta}  
$$

- 이제 베이즈 정리와 전체 확률의 법칙을 얻었으므로 마침내 베이지안 업데이트로 넘어갈 수 있다.    
- 치우친 동전 예시를 계속하기 전에, 다음 예시에 등장하는 베이지안 업데이트 표의 두 가지 특징을 지적하자.    
#### Notes.
- 연속 사전분포에 대한 표는 매우 단순하다. 무한히 많은 가설 각각에 대해 행을 가질 수 없으므로, 모든 가설 $H_\theta$를 대표하는 변수를 사용하는 하나의 행만 가진다.    
- $d\theta$를 포함하면 표의 모든 항목이 확률이 되며, 우리의 일반적인 확률 규칙이 모두 적용된다.

#### Example (Bayesian updating: Continuing Bent coin examples.)
- 앞면이 나올 확률이 알려지지 않은 $\theta$인 치우친 동전이 있다.
- $\theta$의 값은 사전 pdf  $f(\theta)=2\theta$를 가지는 확률변수이다.
- 동전을 세 번 던져서 수열 HTT를 얻었다고 하자.
- $\theta$에 대한 사후 pdf를 계산하라.
#### Solution
- 우리는 $\theta$가 가질 수 있는 값의 범위를 나타내는 열을 추가하여 일반적인 업데이트 표를 만든다.
- 첫 번째 행은 베이지안 업데이트의 추상적인 형태이고, 두 번째 행은 이 특정 예시에 대한 베이지안 업데이트이다.
- 이후 예시들에서는 이러한 추상적인 형태를 생략할 것이다.

- 해설
- 아래 표에서 베이지안 업데이트를 수행한다.
- $x=1,1,0$은 관측된 데이터 HHT를 의미한다.


| hypothesis | range            | prior                          | likelihood              | Bayes numerator                                     | posterior                       |
| ---------- | ---------------- | ------------------------------ | ----------------------- | --------------------------------------------------- | ------------------------------- |
| $H_\theta$ | $\theta\in[0,1]$ | $f(\theta),d\theta$            | $p(x=1,1,0\mid \theta)$ | $p(x=1,1,0\mid \theta)f(\theta),d\theta$            | $f(\theta\mid x=1,1,0),d\theta$ |
| $H_\theta$ | $[0,1]$          | $2\theta,d\theta$              | $\theta^2(1-\theta)$    | $2\theta^3(1-\theta),d\theta$                       | $20\theta^3(1-\theta),d\theta$  |
| total      | $[0,1]$          | $\int_0^1 f(\theta),d\theta=1$ | no sum                  | $\int_0^1 2\theta^3(1-\theta),d\theta=\frac{1}{10}$ | $1$                             |

- 가능도는  

$$  
p(x=1,1,0\mid \theta)=\theta^2(1-\theta)  
$$  

이다.

- 사전 pdf는  

$$  
f(\theta)=2\theta  
$$  

이므로 베이즈 분자는 

$$  
p(x=1,1,0\mid \theta)f(\theta)  
=\theta^2(1-\theta)\cdot 2\theta  
=2\theta^3(1-\theta)  
$$  

가 된다.

- 전체 확률(정규화 상수)은  

$$  
p(x=1,1,0)  
=\int_0^1 2\theta^3(1-\theta),d\theta  
=\frac{1}{10}  
$$  

이다.

- 따라서 사후 pdf는  

$$  
f(\theta\mid x=1,1,0)  
=\frac{2\theta^3(1-\theta)}{1/10}  
=20\theta^3(1-\theta)  
$$  

가 된다.

- 즉, HHT를 관측한 후의 사후 pdf는  

$$  
f(\theta\mid x)=20\theta^3(1-\theta)  
$$  

이다.



| hypothesis | range            | prior                          | likelihood              | Bayes numerator                                     | posterior                       |
| ---------- | ---------------- | ------------------------------ | ----------------------- | --------------------------------------------------- | ------------------------------- |
| $H_\theta$ | $\theta\in[0,1]$ | $f(\theta),d\theta$            | $p(x=1,1,0\mid \theta)$ | $p(x=1,1,0\mid \theta)f(\theta),d\theta$            | $f(\theta\mid x=1,1,0),d\theta$ |
| $H_\theta$ | $[0,1]$          | $2\theta,d\theta$              | $\theta^2(1-\theta)$    | $2\theta^3(1-\theta),d\theta$                       | $20\theta^3(1-\theta),d\theta$  |
| total      | $[0,1]$          | $\int_0^1 f(\theta),d\theta=1$ | no sum                  | $\int_0^1 2\theta^3(1-\theta),d\theta=\frac{1}{10}$ | $1$                             |


- 우리는 몇 가지 코멘트를 덧붙인다.    
- 사전확률 $f(\theta),d\theta$를 사용했으므로, 실제 가설은 다음과 같아야 한다.  

$$  
\text{‘알려지지 않은 매개변수가 }\theta\text{ 주변 폭 }d\theta\text{인 구간 안에 있다’}  
$$

- 하지만 우리에게도 이것은 쓰기에 너무 길기 때문에, 우리가 가설을 $\theta$ 또는 $H_\theta$라고 쓸 때마다 항상 이러한 의미를 생각해야 한다.


| hypothesis | range            | prior                          | likelihood              | Bayes numerator                                     | posterior                       |
| ---------- | ---------------- | ------------------------------ | ----------------------- | --------------------------------------------------- | ------------------------------- |
| $H_\theta$ | $\theta\in[0,1]$ | $f(\theta),d\theta$            | $p(x=1,1,0\mid \theta)$ | $p(x=1,1,0\mid \theta)f(\theta),d\theta$            | $f(\theta\mid x=1,1,0),d\theta$ |
| $H_\theta$ | $[0,1]$          | $2\theta,d\theta$              | $\theta^2(1-\theta)$    | $2\theta^3(1-\theta),d\theta$                       | $20\theta^3(1-\theta),d\theta$  |
| total      | $[0,1]$          | $\int_0^1 f(\theta),d\theta=1$ | no sum                  | $\int_0^1 2\theta^3(1-\theta),d\theta=\frac{1}{10}$ | $1$                             |
- $\theta$에 대한 사후 pdf는 표의 사후확률에서 $d\theta$를 제거하여 얻는다.  

$$  
f(\theta\mid x)=20\theta^3(1-\theta)  
$$



| hypothesis | range            | prior                          | likelihood              | Bayes numerator                                     | posterior                       |
| ---------- | ---------------- | ------------------------------ | ----------------------- | --------------------------------------------------- | ------------------------------- |
| $H_\theta$ | $\theta\in[0,1]$ | $f(\theta),d\theta$            | $p(x=1,1,0\mid \theta)$ | $p(x=1,1,0\mid \theta)f(\theta),d\theta$            | $f(\theta\mid x=1,1,0),d\theta$ |
| $H_\theta$ | $[0,1]$          | $2\theta,d\theta$              | $\theta^2(1-\theta)$    | $2\theta^3(1-\theta),d\theta$                       | $20\theta^3(1-\theta),d\theta$  |
| total      | $[0,1]$          | $\int_0^1 f(\theta),d\theta=1$ | no sum                  | $\int_0^1 2\theta^3(1-\theta),d\theta=\frac{1}{10}$ | $1$                             |
- 항상 그렇듯이 $p(x)$는 전체 확률이다.    
- 합 대신 연속분포를 다루므로 적분을 계산한다.    
- 표에 $d\theta$를 포함하면, 전체 확률 $p(x)$를 구하기 위해 어떤 적분을 계산해야 하는지 명확해진다는 점에 주목하라.



| hypothesis | range            | prior                          | likelihood              | Bayes numerator                                     | posterior                       |
| ---------- | ---------------- | ------------------------------ | ----------------------- | --------------------------------------------------- | ------------------------------- |
| $H_\theta$ | $\theta\in[0,1]$ | $f(\theta),d\theta$            | $p(x=1,1,0\mid \theta)$ | $p(x=1,1,0\mid \theta)f(\theta),d\theta$            | $f(\theta\mid x=1,1,0),d\theta$ |
| $H_\theta$ | $[0,1]$          | $2\theta,d\theta$              | $\theta^2(1-\theta)$    | $2\theta^3(1-\theta),d\theta$                       | $20\theta^3(1-\theta),d\theta$  |
| total      | $[0,1]$          | $\int_0^1 f(\theta),d\theta=1$ | no sum                  | $\int_0^1 2\theta^3(1-\theta),d\theta=\frac{1}{10}$ | $1$                             |
- 이 표는 연속 버전의 베이즈 정리를 체계적으로 정리해 준다.
- 즉, 사후 pdf는 사전 pdf와 가능도 함수와 다음 관계를 가진다.  

$$f(\theta\mid x),d\theta=\frac{p(x\mid \theta)f(\theta),d\theta}{\int_a^b p(x\mid \theta)f(\theta),d\theta}=\frac{p(x\mid \theta)f(\theta)}{p(x)},d\theta$$

- 양변 분자의 $d\theta$를 제거하면 밀도에 대한 형태를 얻는다.  

$$  
f(\theta\mid x)  
=\frac{p(x\mid \theta)f(\theta)}{\int_a^b p(x\mid \theta)f(\theta),d\theta}  
=\frac{p(x\mid \theta)f(\theta)}{p(x)}  
$$



| hypothesis | range            | prior                          | likelihood              | Bayes numerator                                     | posterior                       |
| ---------- | ---------------- | ------------------------------ | ----------------------- | --------------------------------------------------- | ------------------------------- |
| $H_\theta$ | $\theta\in[0,1]$ | $f(\theta),d\theta$            | $p(x=1,1,0\mid \theta)$ | $p(x=1,1,0\mid \theta)f(\theta),d\theta$            | $f(\theta\mid x=1,1,0),d\theta$ |
| $H_\theta$ | $[0,1]$          | $2\theta,d\theta$              | $\theta^2(1-\theta)$    | $2\theta^3(1-\theta),d\theta$                       | $20\theta^3(1-\theta),d\theta$  |
| total      | $[0,1]$          | $\int_0^1 f(\theta),d\theta=1$ | no sum                  | $\int_0^1 2\theta^3(1-\theta),d\theta=\frac{1}{10}$ | $1$                             |

- 양변을 모두 $\theta$의 함수로 보면, 베이즈 정리를 다시 다음 형태로 표현할 수 있다.  

$$  
f(\theta\mid x)\propto p(x\mid \theta)\cdot f(\theta)  
$$

- 즉,  

$$  
\text{posterior}\propto \text{likelihood}\times \text{prior}  
$$


### Flat priors
- 중요한 사전분포 중 하나는 평평한(flat) 사전분포 또는 균등(uniform) 사전분포라고 불린다.
- 평평한 사전분포는 **모든 가설이 동일하게 가능하다고 가정**한다.
- 예를 들어 $\theta$의 범위가 $[0,1]$이면  

$$  
f(\theta)=1  
$$  

은 평평한 사전분포이다.

- 예시(평평한 사전분포)
- 앞면이 나올 확률이 알려지지 않은 $\theta$인 치우친 동전이 있다.
- 동전을 한 번 던져서 앞면이 나왔다고 하자.
- 평평한 사전분포를 가정하고 $\theta$에 대한 사후확률을 구하라.



#### Solution
- 이는 이전 예시와 유사하지만 사전분포와 데이터가 다르다.
- 데이터는 앞면 한 번이므로  $x=1$ 이다.
- 평평한 사전분포를 사용하므로  $f(\theta)=1$ 이다.
- 가능도는  $p(x=1\mid \theta)=\theta$ 이다.

|hypothesis|range|prior|likelihood|Bayes numerator|posterior|
|---|---|---|---|---|---|
|$\theta$|$[0,1]$|$1\cdot d\theta$|$\theta$|$\theta,d\theta$|$2\theta,d\theta$|
|total|$[0,1]$|$\int_0^1 f(\theta),d\theta=1$|no sum|$\int_0^1 \theta,d\theta=\frac{1}{2}$|$1$|

- 전체 확률은  

$$  
p(x=1)=\int_0^1 \theta,d\theta=\frac{1}{2}  
$$  

- 따라서 사후 pdf는  

$$  
f(\theta\mid x=1)  
=\frac{\theta}{1/2}  
=2\theta  
$$  





### Using the posterior pdf
#### Solution
- 사전확률이 평평하다는 것은  

$$  
f(\theta)=1,\qquad 0\le \theta\le 1  
$$  

임을 의미한다.

- 동전이 앞면 쪽으로 치우쳐 있다는 것은  

$$  
\theta>\frac{1}{2}  
$$  

임을 뜻하고, 뒷면 쪽으로 치우쳐 있다는 것은  

$$  
\theta<\frac{1}{2}  
$$  

임을 뜻한다.

- 사전분포가 균등하므로  

$$  
P\left(\theta>\frac12\right)  
=\int_{1/2}^1 1\,d\theta  
=\frac12  
$$  

이고,  

$$  
P\left(\theta<\frac12\right)  
=\int_0^{1/2} 1\,d\theta  
=\frac12  
$$  


- 따라서 사전적으로(a priori) 동전은 앞면 쪽이나 뒷면 쪽으로 동일하게 치우쳐 있을 가능성을 가진다.
- 이제 앞면이 한 번 관측된 후의 사후 pdf:

$$  
f(\theta\mid x=1)=2\theta  
$$  

.

- 따라서 동전이 앞면 쪽으로 치우쳐 있을 사후확률:  

$$  
P\left(\theta>\frac12\mid x=1\right)  
=\int_{1/2}^1 2\theta\,d\theta  
$$  

$$  
=\left[\theta^2\right]_{1/2}^1  
=1-\frac14  
=\frac34  
$$  


- 즉, 앞면을 한 번 관측한 후 동전이 앞면 쪽으로 치우쳐 있을 확률은  

$$  
\frac34  
$$  



#### Solution
- 매개변수 $\theta$는 동전이 앞면이 나올 확률이므로, 문제의 첫 번째 부분은  $P(\theta>0.5)=0.5$임을 보이는 것이고, 두 번째 부분은  $P(\theta>0.5\mid x=1)$을 구하는 것이다.
- 이들은 각각 사전 pdf와 사후 pdf로부터 쉽게 계산된다.
- 동전이 앞면 쪽으로 치우쳐 있을 사전확률은  

$$  
P(\theta>0.5)  
=\int_{0.5}^1 f(\theta),d\theta  
$$  

$$  
=\int_{0.5}^1 1\cdot d\theta  
$$  

$$  
=\theta\Big|_{0.5}^1  
=\frac12  
$$  


#### Solution
- 확률이 $\frac12$라는 것은 동전이 앞면 쪽이나 뒷면 쪽으로 동일한 가능성으로 치우쳐 있음을 의미한다.
- 동전이 앞면 쪽으로 치우쳐 있을 사후확률은  

$$  
P(\theta>0.5\mid x=1)  
=\int_{0.5}^1 f(\theta\mid x=1),d\theta  
$$  

$$  
=\int_{0.5}^1 2\theta,d\theta  
$$  

$$  
=\theta^2\Big|_{0.5}^1  
=\frac34  
$$  


- 즉, 앞면을 한 번 관측함으로써 동전이 앞면 쪽으로 치우쳐 있을 확률은$\frac12$ 에서  $\frac34$로 증가하였다.

### Predictive probabilities
- 예시(사전예측과 사후예측)
- 치우친 동전 예시를 계속하자.
- 앞면이 나올 확률이 알려지지 않은 $\theta$인 동전이 있고, $\theta$의 사전 pdf는  

$$  
f(\theta)=2\theta  
$$  

- 먼저 앞면의 사전예측확률을 구하자.
- 전체 확률의 법칙을 사용하면  

$$  
P(\text{heads})  
=p(x=1)  
=\int_0^1 p(x=1\mid \theta)f(\theta),d\theta  
$$  

$$  
=\int_0^1 \theta\cdot 2\theta,d\theta  
$$  

$$  
=\int_0^1 2\theta^2,d\theta  
=\frac23  
$$  

- 이제 첫 번째 던짐에서 앞면이 나왔다고 하자.
- 이전 결과에 의해 사후 pdf는  

$$  
f(\theta\mid x=1)=2\theta  
$$  

- 두 번째 던짐에서 앞면이 나올 사후예측확률은  

$$  
P(\text{heads on second flip}\mid x=1)  
=\int_0^1 p(x=1\mid \theta)f(\theta\mid x=1),d\theta  
$$  

$$  
=\int_0^1 \theta\cdot 2\theta,d\theta  
$$  

$$  
=\frac23  
$$  

- 두 번째 던짐에서 뒷면이 나올 사후예측확률은  

$$  
P(\text{tails on second flip}\mid x=1)  
=\int_0^1 (1-\theta)\cdot 2\theta,d\theta  
$$  

$$  
=2\int_0^1 (\theta-\theta^2),d\theta  
$$  

$$  
=2\left(\frac12-\frac13\right)  
=\frac13  
$$  

이다.



#### Solution
- 표기를 위해 첫 번째 던짐의 결과를 $x_1$, 두 번째 던짐의 결과를 $x_2$라고 하자.
- 사전예측확률은 이전에 계산했던 전체 확률과 정확히 같다.  

$$  
p(x_1=1)  
=\int_0^1 p(x_1=1\mid \theta)f(\theta)\,d\theta  
$$  

$$  
=\int_0^1 2\theta^2\,d\theta  
$$  

$$  
=\frac23  
$$

- 사후예측확률은 사후 pdf를 사용하여 계산한 전체 확률이다.
- 우리는 사후 pdf가  $f(\theta\mid x_1=1)=3\theta^2$임을 알고 있다.


- 따라서 사후예측확률은 다음과 같다.  

$$  
p(x_2=1\mid x_1=1)  
=\int_0^1 p(x_2=1\mid \theta,x_1=1)f(\theta\mid x_1=1),d\theta  
$$  

$$  
=\int_0^1 \theta\cdot 3\theta^2,d\theta  
=\frac34  
$$  

$$  
p(x_2=0\mid x_1=1)  
=\int_0^1 p(x_2=0\mid \theta,x_1=1)f(\theta\mid x_1=1),d\theta  
$$  

$$  
=\int_0^1 (1-\theta)\cdot 3\theta^2,d\theta  
=\frac14  
$$

- 더 간단히는 다음과 같이 계산할 수도 있다.  

$$  
p(x_2=0\mid x_1=1)=1-p(x_2=1\mid x_1=1)=\frac14  
$$

### From discrete to continuous Bayesian updating
- 우리는 이산 베이지안 업데이트에서 연속 베이지안 업데이트로 넘어가는 과정에 대한 직관을 발전시키려 한다.    
- 미적분학에서 익숙한 길을 따라갈 것이다. 즉, 우리는 다음을 수행한다.    
- 연속적인 가설 범위를 유한 개의 짧은 구간으로 나눈다.    
- 유한 개의 가설에 대해 이산 업데이트 표를 만든다.    
- 가설의 개수가 무한대로 갈 때 표가 어떻게 변하는지 살펴본다.    
- 이런 방식으로 사전 pmf와 사후 pmf가 사전 pdf와 사후 pdf로 수렴하는 것을 보게 될 것이다.


#### Example
- 구체적으로 살펴보기 위해, 치우친 동전 예시와 같은 사전분포 및 데이터를 사용하자.
- 평평한 사전분포  

$$  
f(\theta)=1  
$$  

을 가지는 ‘치우친’ 동전이 있다.

- 우리의 데이터는 동전을 한 번 던져 앞면이 나왔다는 것이다.
- 우리의 목표는 가설의 수를 늘려 가면서 이산적인 경우에서 연속적인 경우로 넘어가는 것이다.
- 4개의 가설
- 앞면이 나올 확률이 각각 $\frac18$, $\frac38$, $\frac58$, $\frac78$인 네 가지 유형의 동전이 있다고 하자.
- 하나의 동전이 무작위로 선택된다면, 그 유형에 대한 우리의 가설은 다음과 같다.  

$$  
H_1:\theta=\frac18,\qquad H_2:\theta=\frac38,\qquad H_3:\theta=\frac58,\qquad H_4:\theta=\frac78  
$$

- 이를 얻기 위해 우리는 구간 $[0,1]$을 다음과 같이 4개의 동일한 구간으로 나누었다.  

$$  
\left[0,\frac14\right],\quad  
\left[\frac14,\frac12\right],\quad  
\left[\frac12,\frac34\right],\quad  
\left[\frac34,1\right]  
$$

- 각 구간의 폭은  

$$  
\Delta\theta=\frac14  
$$  

- 우리는 각 구간의 중심에 동전 유형에 대한 $\theta$ 값을 배치하였다.
- 미적분에서 리만 합(Riemann sum)을 만들 때와 마찬가지로, 각 구간 안의 어디에서 $\theta$를 선택하는지는 중요하지 않다.
- 중심은 쉬운 선택 중 하나이다.
- 이 값들을  

$$  
\theta_j=\frac{j}{8},\qquad j=1,3,5,7  
$$  

로 나타내자.
- 평평한 사전분포는 각 가설에 대해  

$$  
\frac14=1\cdot \Delta\theta  
$$  

의 확률을 부여한다.


- 우리는 다음과 같은 표를 가진다.

|hypothesis|prior|likelihood|Bayes numerator|posterior|
|---|---|---|---|---|
|$\theta=\theta_1=\frac18$|$\frac14$|$\frac18$|$\frac14\cdot\frac18$|$0.0625$|
|$\theta=\theta_2=\frac38$|$\frac14$|$\frac38$|$\frac14\cdot\frac38$|$0.1875$|
|$\theta=\theta_3=\frac58$|$\frac14$|$\frac58$|$\frac14\cdot\frac58$|$0.3125$|
|$\theta=\theta_4=\frac78$|$\frac14$|$\frac78$|$\frac14\cdot\frac78$|$0.4375$|
|Total|$1$|–|$\sum_{i=1}^n \theta_i\Delta\theta$|$1$|

- 아래에는 사전 pmf와 사후 pmf의 밀도 히스토그램(density histogram)이 나타나 있다.    
- 이전 예시에서 얻은 사전 pdf와 사후 pdf는 히스토그램 위에 빨간색으로 겹쳐서(superimpose) 표시되어 있다.

#### 8개의 가설
- 다음으로 $[0,1]$을 각각 폭  

$$  
\Delta\theta=\frac18  
$$  

인 8개의 구간으로 나누고, 각 구간의 중심을 8개의 가설 $\theta_i$로 사용한다.  

$$  
\theta_1:\theta=\frac{1}{16},\quad  
\theta_2:\theta=\frac{3}{16},\quad  
\theta_3:\theta=\frac{5}{16},\quad  
\theta_4:\theta=\frac{7}{16}  
$$  

$$  
\theta_5:\theta=\frac{9}{16},\quad  
\theta_6:\theta=\frac{11}{16},\quad  
\theta_7:\theta=\frac{13}{16},\quad  
\theta_8:\theta=\frac{15}{16}  
$$

- 평평한 사전분포는 각 가설에 확률  

$$  
\frac18=1\cdot\Delta\theta  
$$  

를 부여한다.


- 다음은 표와 밀도 히스토그램이다.

|hypothesis|prior|likelihood|Bayes numerator|posterior|
|---|---|---|---|---|
|$\theta=\theta_1=\frac{1}{16}$|$\frac18$|$\frac{1}{16}$|$\frac18\cdot\frac{1}{16}$|$0.0156$|
|$\theta=\theta_2=\frac{3}{16}$|$\frac18$|$\frac{3}{16}$|$\frac18\cdot\frac{3}{16}$|$0.0469$|
|$\theta=\theta_3=\frac{5}{16}$|$\frac18$|$\frac{5}{16}$|$\frac18\cdot\frac{5}{16}$|$0.0781$|
|$\theta=\theta_4=\frac{7}{16}$|$\frac18$|$\frac{7}{16}$|$\frac18\cdot\frac{7}{16}$|$0.1094$|
|$\theta=\theta_5=\frac{9}{16}$|$\frac18$|$\frac{9}{16}$|$\frac18\cdot\frac{9}{16}$|$0.1406$|
|$\theta=\theta_6=\frac{11}{16}$|$\frac18$|$\frac{11}{16}$|$\frac18\cdot\frac{11}{16}$|$0.1719$|
|$\theta=\theta_7=\frac{13}{16}$|$\frac18$|$\frac{13}{16}$|$\frac18\cdot\frac{13}{16}$|$0.2031$|
|$\theta=\theta_8=\frac{15}{16}$|$\frac18$|$\frac{15}{16}$|$\frac18\cdot\frac{15}{16}$|$0.2344$|
|Total|$1$|–|$\sum_{i=1}^n \theta_i\Delta\theta$|$1$|



#### 20개의 가설    
- 마지막으로 $[0,1]$을 20개의 조각으로 나눈다.    
- 이는 앞의 두 경우와 본질적으로 동일하다.    
- 그림들의 수열을 보면, 사전 및 사후 밀도 히스토그램이 사전 및 사후 확률밀도함수로 수렴하는 방식을 볼 수 있다.

### Notational conventions

- 확률과 가능도를 설명하기 위해 사용하는 다양한 표기법과 용어를 다룰 수 있어야 한다.

- 우리는 확률, 가설, 데이터에 대해 여러 가지 표기법을 도입하였다.    
- 여기서는 그것들을 한곳에 모아 정리한다.

### Notation and terminology for data and hypotheses
- 데이터와 가설에 이름을 붙이는 문제는 꽤 까다롭다.    
- 수업을 시작했을 때 우리는 앞면(heads)이나 뒷면(tails) 같은 결과(outcome)에 대해 이야기했다.    
- 그다음 확률변수를 도입하면서 결과(outcome)에 수치 값을 부여하였다. 예를 들어 앞면에는 $1$, 뒷면에는 $0$을 부여하였다.    
- 이를 통해 평균이나 분산 같은 것을 계산할 수 있게 되었다.    
- 이제 우리는 비슷한 일을 다시 해야 한다.


- 우리의 표기 관례를 떠올리자.    
	- Events 사건은 대문자로 표시한다. 예를 들어 $A,B,C$이다.    
	- andom variable확률변수는 대문자 $X$이고, 작은 문자 $x$ 값을 가진다.    
	- value과 event의 연결은 다음과 같다. ‘$X=x$’는 $X$가 값 $x$를 가진다는 사건이다.    
	- 사건의 확률은 대문자 $P(A)$로 나타낸다.

- 이산 확률변수는 소문자 $p(x)$로 나타내는 확률질량함수(probability mass function)를 가진다.
- $P$와 $p$의 관계는 다음과 같다.

$$  
P(X=x)=p(x)  
$$

- 연속 확률변수는 확률밀도함수 $f(x)$를 가진다.
- $P$와 $f$의 관계는 다음과 같다.  

$$  
P(a\le X\le b)=\int_a^b f(x)\,dx  
$$

- 연속 확률변수 $X$가 $x$ 주변의 폭 $dx$인 무한소 구간 안에 있을 확률은  

$$  
f(x)\,dx  
$$  


- 베이지안 업데이트의 맥락에서도 비슷한 관례를 사용한다.
- 가설을 나타낼 때는 대문자, 특히 $H$를 사용한다. 예를 들어 $H=\text{‘동전은 공정하다’}$이다.
- 모형 매개변수의 가설 값을 나타낼 때는 소문자, 특히 $\theta$를 사용한다. 예를 들어 동전이 앞면이 나올 확률은 $\theta=0.5$이다.
- 데이터를 사건으로 말할 때는 대문자, 특히 $D$를 사용한다.
- 예를 들어 $D=\text{‘던진 순서가 HTH였다’}$이다.
- 데이터를 값으로 말할 때는 소문자, 특히 $x$를 사용한다.
- 예를 들어 데이터의 수열은  

$$  
x_1,x_2,x_3=1,0,1  
$$  

- 가설 집합이 이산적일 때는 개별 가설의 확률을 사용할 수 있다. 예를 들어 $p(\theta)$이다.
- 가설 집합이 연속적일 때는 가설의 무한소 범위에 대한 확률을 사용해야 한다. 예를 들어  

$$  
f(\theta),d\theta  
$$


- 다음 표는 이산적인 $\theta$와 연속적인 $\theta$의 경우를 요약한다.
- 두 경우 모두 가능한 결과(데이터) $x$의 집합은 이산적이라고 가정한다.
- 이후에는 연속적인 결과 집합도 다룰 것이다.


| |hypothesis|prior|likelihood|Bayes numerator|posterior|
|---|---|---|---|---|---|
| |$\mathcal{H}$|$P(\mathcal{H})$|$P(D\mid \mathcal{H})$|$P(D\mid \mathcal{H})P(\mathcal{H})$|$P(\mathcal{H}\mid D)$|
|Discrete $\theta$|$\theta$|$p(\theta)$|$p(x\mid \theta)$|$p(x\mid \theta)p(\theta)$|$p(\theta\mid x)$|
|Continuous $\theta$|$\theta$|$f(\theta),d\theta$|$p(x\mid \theta)$|$p(x\mid \theta)f(\theta),d\theta$|$f(\theta\mid x),d\theta$|

- 연속 가설 $\theta$는 실제로  

$$  
\text{‘매개변수 }\theta\text{가 }\theta\text{ 주변 폭 }d\theta\text{인 구간 안에 있다’}  
$$  

의 축약 표현이라는 점을 기억하라.

