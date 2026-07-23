2026-05-07 08:20
## 20강 Beta and Normal




### Learning Goals
- 베타 분포의 2-parameter family와와 그 정규화에 익숙해지기.
- 켤레 사전분포의 장점을 이해하기.
- 베르누이, 이항, 기하 가능도가 주어졌을 때 베타 사전분포를 업데이트할 수 있기.
- 분산이 알려진 정규 가능도가 주어졌을 때 정규 사전분포를 업데이트하는 공식을 이해하고 사용할 수 있기.

### Introduction
- 여기서 우리의 주요 목표는 conjugate prior(켤레 사전분포)의 아이디어를 소개하고 몇 가지 구체적인 conjugate pair(켤레쌍)을 살펴보는 것이다.    
- 이것들은 **베이즈 업데이트 작업을 단순한 산술로 단순화**한다.    
- 먼저 베타 분포를 소개하고 이를 이항 가능도에 대한 켤레 사전분포로 사용해 볼 것이다.    
- 그다음 다른 켤레쌍들을 살펴볼 것이다.
-  AI 모델에 매우 많이 사용됨.

### Beta distribution
- 베타 분포 $\mathrm{Beta}(a,b)$는 구간 $[0,1]$을 범위로 가지는 2-모수 분포이며, 확률밀도함수는 다음과 같다.  

$$  
f(\theta)=\frac{(a+b-1)!}{(a-1)!(b-1)!}\;\theta^{a-1}(1-\theta)^{b-1}  
$$

- 매개변수를 변화시키면서 베타 분포의 형태를 탐색할 수 있는 애플릿:
- [beta distribution applet](https://mathlets.org/mathlets/beta-distribution/?utm_source=chatgpt.com)
- 애플릿에서 볼 수 있듯이, 베타 분포는 임의의 실수 $a>0$, $b>0$에 대해 정의될 수 있다.

- beta distribution(베타 분포)는 2개의 파라미터를 갖고 범위는 0~1 사이
- a가 커지면 1에 가까워짐(커질 확률이 올라감.)
- b가 커지면 0에 가까워짐 (작아질 확률이 올라감.)
- 둘다 커지면 가운데로 값이 몰림
- a가 b보다 크면 1 쪽으로
- b가 a보다 크면 0 쪽으로 치우치고,  
- a,b가 모두 커지면 평균 $\frac{a}{a+b}$ 주변으로 더 좁게 몰린다.
- a,b 가 둘다 0이면 세타에 관한 값이 다 사라짐.


- 우리는 정수 $a$와 $b$만 다룰 것이지만, 전체 내용은 여기서 볼 수 있다:
- [https://en.wikipedia.org/wiki/Beta_distribution](https://en.wikipedia.org/wiki/Beta_distribution)
- 베이즈 업데이트의 맥락에서 $a$와 $b$는 우리의 가설을 나타내는 미지의 매개변수 $\theta$와 구별하기 위해 종종 하이퍼파라미터라고 불린다.
- 어떤 의미에서 $a$와 $b$는 $\theta$보다 한 단계 위에 있는데, 이는 그것들이 $\theta$의 확률밀도함수를 매개변수화하기 때문이다.
- Beta distribution는 prior, 이고 세타는 파라미터, a,b는 하이퍼파라미터
- (베이지안 확률모형에서는)프라이어의 파라미터를 하이퍼 파라미터라고 정의함.
- 요즘은 AI 발전으로 하이퍼 파라미터를 변수 또는 모델이 데이터로부터 직접 학습하지 않고, 학습 과정 전에 사람이 정하거나 별도의 절차로 선택하는 값으로 정의하기도 하지만 확률분포에서 엄밀한 정의는 위와 같다.

### A simple but important observation!
- 구간 $[0,1]$에서 정의된 확률밀도함수 $f(\theta)$가 $c\theta^{a-1}(1-\theta)^{b-1}$ 형태라면, $f(\theta)$는 $\mathrm{Beta}(a,b)$ 분포이고 정규화 상수는 다음과 같아야 한다.  

$$  
c=\frac{(a+b-1)!}{(a-1)!(b-1)!}  
$$

- 이는 상수 $c$가 확률밀도함수의 전체 확률이 $1$이 되도록 정규화해야 하기 때문이다.
- 그런 상수는 하나뿐이며, 베타 분포의 공식에서 주어진다.
- 정규분포, 지수분포 등에도 비슷한 관찰이 성립한다.


### Beta priors and posteriors for binomial random variables
#### Example
- 앞면이 나올 미지의 확률이 $\theta$인 휘어진 동전이 있다고 하자. 이 동전을 $12$번 던져서 앞면 $8$번, 뒷면 $4$번이 나왔다.    
- 평평한 사전분포에서 시작하여 사후 확률밀도함수가 $\mathrm{Beta}(9,5)$ 분포임을 보여라.  
#### Solution
- 이것은 이전 수업의 예제들과 거의 동일하다.    
- $12$번의 동전 던지기에서 얻은 데이터를 $x_1$이라고 부르자.    
- 다음 표에서 사후분포 열의 앞에 붙는 상수 계수를 $c_2$라고 부른다.    
- 우리의 단순한 관찰은 그것이 베타 확률밀도함수의 상수 계수여야 함을 알려줄 것이다.




- 데이터는 앞면 $8$번과 뒷면 $4$번이다. 이것은 이항분포 $\mathrm{Binomial}(12,\theta)$에서 나오므로 가능도는 다음과 같다.  

$$  
p(x_1\mid \theta)=\binom{12}{8}\theta^8(1-\theta)^4  
$$

- 따라서 베이즈 업데이트 표는 다음과 같다.  

| hypothesis | prior            | likelihood                          | Bayes numerator                                         | posterior                         |
| ---------- | ---------------- | ----------------------------------- | ------------------------------------------------------- | --------------------------------- |
| $\theta$   | $1\cdot d\theta$ | $\binom{12}{8}\theta^8(1-\theta)^4$ | $\binom{12}{8}\theta^8(1-\theta)^4,d\theta$             | $c_2\theta^8(1-\theta)^4,d\theta$ |
| total      | $1$              |                                     | $T=\binom{12}{8}\int_0^1 \theta^8(1-\theta)^4\,d\theta$ | $1$                               |

- 사후 확률밀도함수에 대해 우리의 단순한 관찰은 $a=9$, $b=5$일 때 성립한다.
- 따라서 사후 확률밀도함수는 $\mathrm{Beta}(9,5)$ 분포를 따르며 다음을 얻는다.  

$$  
f(\theta\mid x_1)=c_2\theta^8(1-\theta)^4  
$$  
여기서  

$$  
c_2=\frac{13!}{8!4!}  
$$


#### Note.
- 우리는 가능도에 이항계수 $\binom{12}{8}$를 명시적으로 포함했다.
- 이를 예를 들어 $c_1$이라고 이름 붙이고 그 값을 명시하지 않아도 똑같이 할 수 있었다.  
#### Example
- 이제 같은 동전을 다시 던져서 앞면 $n$번과 뒷면 $m$번을 얻었다고 하자.
- 이전 예제의 사후 확률밀도함수를 새로운 사전 확률밀도함수로 사용하여, 새로운 사후 확률밀도함수가 $\mathrm{Beta}(9+n,5+m)$ 분포임을 보여라.
- 이 추가된 $n+m$번의 동전 던지기 데이터를 $x_2$라고 부르자.
- 이번에는 이항계수를 명시적으로 쓰지 않을 것이다.
- 대신 단순히 $c_3$라고 부르겠다.
- 새로운 기호가 필요할 때마다 단지 새로운 아래첨자를 붙인 $c$를 사용할 것이다.  

| hyp.     | prior                             | likelihood                | Bayes numerator                                         | posterior                                 |     |
| -------- | --------------------------------- | ------------------------- | ------------------------------------------------------- | ----------------------------------------- | --- |
| $\theta$ | $c_2\theta^8(1-\theta)^4,d\theta$ | $c_3\theta^n(1-\theta)^m$ | $c_2c_3\theta^{n+8}(1-\theta)^{m+4},d\theta$            | $c_4\theta^{n+8}(1-\theta)^{m+4},d\theta$ |     |
| total    | $1$                               |                           | $T=\int_0^1 c_2c_3\theta^{n+8}(1-\theta)^{m+4},d\theta$ | $1$                                       |     |

- 다시 우리의 단순한 관찰이 성립하므로 사후 확률밀도함수  

$$  
f(\theta\mid x_1,x_2)=c_4\theta^{n+8}(1-\theta)^{m+4}  
$$ 
는 $\mathrm{Beta}(n+9,m+5)$ 분포를 따른다.


#### Note.
- Flat beta.: $\mathrm{Beta}(1,1)$ 분포는 구간 $[0,1]$에서의 균등분포와 같으며, 이를 $\theta$에 대한 uniform distribution라고도 불렀다.    
- 이는 베타 분포의 정의에 $a=1$과 $b=1$을 대입하면 $f(\theta)=1$이 되기 때문이다.


#### Summary.
- 앞면이 나올 확률이 $\theta$라면, $n+m$번의 동전 던지기에서 앞면의 개수는 이항분포 $\mathrm{Binomial}(n+m,\theta)$를 따른다.
- 우리는 $\theta$에 대한 사전분포가 베타분포이면 사후분포 역시 베타분포가 되며, 오직 베타분포의 매개변수 $a,b$만 변한다는 것을 보았다.
- 이제 이 변화가 정확히 어떻게 일어나는지를 표로 요약한다.
- 데이터는 $n+m$번의 시행에서 앞면 $n$번, 뒷면 $m$번이라고 가정한다.  

| hypothesis | data    | prior                                     | likelihood                      | posterior                                      |     |
| ---------- | ------- | ----------------------------------------- | ------------------------------- | ---------------------------------------------- | --- |
| $\theta$   | $x=n,m$ | $\mathrm{Beta}(a,b)$                      | $\mathrm{Binomial}(n+m,\theta)$ | $\mathrm{Beta}(a+n,b+m)$                       |     |
| $\theta$   | $x=n,m$ | $c_1\theta^{a-1}(1-\theta)^{b-1},d\theta$ | $c_2\theta^n(1-\theta)^m$       | $c_3\theta^{a+n-1}(1-\theta)^{b+m-1}\,d\theta$ |     |


### Conjugate priors
- 베타분포는 이항분포에 대한 켤레 사전분포라고 불린다.    
- 이는 가능도 함수가 이항분포이면 베타 사전분포가 베타 사후분포를 준다는 뜻이며, 이것이 이전 예제들에서 본 내용이다.    
- 사실 베타분포는 베르누이분포와 기하분포에 대해서도 켤레 사전분포이다.    
- 곧 또 다른 중요한 예를 볼 것이다. 정규분포는 자기 자신의 켤레 사전분포이다.    
- 특히 가능도 함수가 알려진 분산을 갖는 정규분포이면 정규 사전분포는 정규 사후분포를 준다.


- 켤레 사전분포는 베이즈 업데이트를 적분 계산이 아니라 사전분포의 매개변수, 즉 하이퍼파라미터를 수정하는 작업으로 줄여 주기 때문에 유용하다.
- 우리는 지난 표에서 베타분포에 대해 이것을 보았다.
- 더 많은 예시는 다음을 참고하라:
- [https://en.wikipedia.org/wiki/Conjugate_prior_distribution](https://en.wikipedia.org/wiki/Conjugate_prior_distribution)

- 이제 켤레 사전분포의 정의를 제시한다.
- 아래 예시들을 통해 이해하는 것이 가장 좋다.  
#### Definition
- 매개변수 $\theta$에 의존하는 가능도 함수 $\phi(x\mid\theta)$를 갖는 데이터가 있다고 하자.
- 또한 $\theta$에 대한 사전분포가 매개변수화된 분포족 중 하나라고 하자.
- $\theta$에 대한 사후분포가 이 분포족 안에 있으면, 그 사전분포족을 해당 가능도에 대한 켤레 사전분포라고 한다.
- 아래에서 베타분포가 이항, 베르누이, 기하 가능도에 대한 켤레 사전분포임을 보일 것이다.




### Beta prior - Binomial likelihood
- 위에서 베타분포가 이항분포에 대한 켤레 사전분포임을 보았다.    
- 이는 가능도 함수가 이항분포이고 사전분포가 베타분포이면 사후분포도 베타분포라는 뜻이다.    
- 더 구체적으로, 가능도가 이항분포 $\mathrm{Binomial}(N,\theta)$를 따른다고 하자. 여기서 $N$은 알려져 있고 $\theta$는 관심 있는 미지의 매개변수이다.    
- 또한 한 번의 시행에서 얻은 데이터 $x$는 $0$과 $N$ 사이의 정수이다.



- 그러면 베타 사전분포에 대해 다음 표를 얻는다.  

| hypoth.  | data | prior                                       | likelihood                                    | posterior                                               |     |
| -------- | ---- | ------------------------------------------- | --------------------------------------------- | ------------------------------------------------------- | --- |
| $\theta$ | $x$  | $\mathrm{Beta}(a,b)$                        | $\mathrm{Binomial}(N,\theta)$                 | $\mathrm{Beta}(a+x,b+N-x)$                              |     |
|          |      | $f(\theta)=c_1\theta^{a-1}(1-\theta)^{b-1}$ | $p(x\mid \theta)=c_2\theta^x(1-\theta)^{N-x}$ | $f(\theta\mid x)=c_3\theta^{a+x-1}(1-\theta)^{b+N-x-1}$ |     |


- 이 표는 정규화 계수를 각각 $c_1$, $c_2$, $c_3$로 표기하여 단순화한 것이다.
- 필요하다면 베타분포와 이항분포의 정규화를 기억하거나 찾아봄으로써 $c_1$과 $c_2$의 값을 복원할 수 있다.  

$$  
c_1=\frac{(a+b-1)!}{(a-1)!(b-1)!}  
$$  

$$  
c_2=\binom{N}{x}=\frac{N!}{x!(N-x)!}  
$$  

$$  
c_3=\frac{(a+b+N-1)!}{(a+x-1)!(b+N-x-1)!}  
$$


- 베타분포는 베르누이분포에 대한 켤레 사전분포이다.    
- 이것은 사실 이항분포의 특수한 경우인데, $\mathrm{Bernoulli}(\theta)$는 $\mathrm{Binomial}(1,\theta)$와 같기 때문이다.    
- 베르누이분포는 약간 더 단순하고 특별히 중요하므로 따로 다룬다.


- 아래 표에서는 성공 $(x=1)$과 실패 $(x=0)$에 대응하는 업데이트를 서로 다른 행에 나타낸다.  

| hypothesis | data | prior | likelihood | posterior |  
|---|---|---|---|---|  
| $\theta$ | $x$ | $\mathrm{Beta}(a,b)$ | $\mathrm{Bernoulli}(\theta)$ | $\mathrm{Beta}(a+1,b)$ 또는 $\mathrm{Beta}(a,b+1)$ |  
| $\theta$ | $x=1$ |  $f(\theta)=c_1\theta^{a-1}(1-\theta)^{b-1}$  |  $p(x\mid \theta)=\theta$  |  $\mathrm{Beta}(a+1,b):\quad f(\theta\mid x)=c_3\theta^a(1-\theta)^{b-1}$  |  
| $\theta$ | $x=0$ |  $f(\theta)=c_1\theta^{a-1}(1-\theta)^{b-1}$  |  $p(x\mid \theta)=1-\theta$  |  $\mathrm{Beta}(a,b+1):\quad f(\theta\mid x)=c_4\theta^{a-1}(1-\theta)^b$  |

- 상수 $c_1$, $c_3$, $c_4$는 이전의 이항 가능도 경우에서 $N=1$인 경우와 같은 공식을 가진다.


- 기하분포 $\mathrm{Geometric}(\theta)$는 각 독립 시행에서 성공 확률이 $\theta$일 때 첫 번째 실패 전 성공 횟수 $x$의 확률을 나타낸다는 것을 떠올리자.
- 대응하는 확률질량함수는 다음과 같다.  

$$  
p(x)=\theta^x(1-\theta)  
$$
- 이제 데이터 점 $x$가 있고, 우리의 가설 $\theta$는 $x$가 기하분포 $\mathrm{Geometric}(\theta)$에서 추출되었다는 것이라고 하자.


- 표에서 우리는 베타분포가 기하 가능도에 대해서도 켤레 사전분포임을 알 수 있다.  

| hypothesis | data | prior | likelihood | posterior |  
|---|---|---|---|---|  
| $\theta$ | $x$ |$\mathrm{Beta}(a,b),\quad f(\theta)=c_1\theta^{a-1}(1-\theta)^{b-1}$|$\mathrm{Geometric}(\theta),\quad p(x\mid \theta)=\theta^x(1-\theta)$|$\mathrm{Beta}(a+x,b+1),\quad f(\theta\mid x)=c_3\theta^{a+x-1}(1-\theta)^b$|

- 처음에는 베타분포가 이항분포와 기하분포 둘 다에 대한 켤레 사전분포라는 점이 이상하게 보일 수 있다.
- 핵심 이유는 기하 가능도가 $\theta$의 함수로 볼 때 이항 가능도에 비례하기 때문이다.


- 이를 구체적인 예로 설명해 보자.  
#### Example
- 버섯 왕국을 여행하던 중 마리오와 루이지는 꽤 특이한 동전들을 발견한다.
- 그들은 앞면이 나올 확률에 대해 사전분포 $f(\theta)\sim\mathrm{Beta}(5,5)$로 합의하지만, $\theta$를 더 조사하기 위해 어떤 실험을 할지에 대해서는 의견이 다르다.
- 마리오는 동전을 $5$번 던지기로 한다. 그는 $5$번 중 앞면을 $4$번 얻는다.
- 루이지는 첫 번째 뒷면이 나올 때까지 동전을 던지기로 한다. 그는 첫 번째 뒷면 전까지 앞면을 $4$번 얻는다.
- 마리오와 루이지가 $\theta$에 대해 같은 사후분포에 도달함을 보이고, 이 사후분포를 계산하라.

#### Solution

- 마리오와 루이지 모두 $\theta$에 대한 사후 확률밀도함수가 $\mathrm{Beta}(9,6)$ 분포임을 보일 것이다.
- Mario의 표:  

| hypothesis | data | prior | likelihood | posterior |  
|---|---|---|---|---|  
| $\theta$ | $x=4$ | $\mathrm{Beta}(5,5)=c_1\theta^4(1-\theta)^4$ | $\mathrm{Binomial}(5,\theta)=\binom{5}{4}\theta^4(1-\theta)$ | $=c_3\theta^8(1-\theta)^5$ |

- Luigi의 표:  

| hypothesis | data | prior | likelihood | posterior |  
|---|---|---|---|---|  
| $\theta$ | $x=4$ | $\mathrm{Beta}(5,5)=c_1\theta^4(1-\theta)^4$ | $\mathrm{Geometric}(\theta)=\theta^4(1-\theta)$ | $=c_3\theta^8(1-\theta)^5$ |

- 마리오와 루이지의 사후분포가 모두 $\mathrm{Beta}(9,6)$ 분포의 형태를 가지므로, 둘의 사후분포는 동일해야 한다.
- 정규화 상수도 전체 확률이 $1$이 되어야 한다는 조건에 의해 결정되므로 두 경우에서 동일해야 한다.

### Bayesian updating with continuous hypotheses and continuous data
- 여기서의 아이디어는 본질적으로 우리가 이미 수행한 베이즈 업데이트와 동일하다.    
- 유일한 차이는, 연속형 가능도의 경우 데이터의 전체 확률(즉 Bayes numerator 열의 합, 즉 정규화 인자)을 합이 아니라 적분으로 계산해야 한다는 점이다.    
- 이에 대해서는 간단히 다룰 것이다.

#### Notation.

- Hypotheses 가설 $\theta$. 연속형 가설의 경우, 이는 실제로 매개변수가 $\theta$ 주변의 크기 $d\theta$인 작은 구간 안에 있다고 가정한다는 뜻이다.
- Data 데이터 $x$. 연속형 데이터의 경우, 이는 실제로 데이터가 $x$ 주변의 크기 $dx$인 작은 구간 안에 있다는 뜻이다.
- Prior 사전분포 $f(\theta),d\theta$. 이는 매개변수가 $\theta$ 주변의 크기 $d\theta$인 작은 구간 안에 있을 확률에 대한 우리의 초기 믿음이다.
- Likelihood 가능도 $\phi(x\mid\theta)$. 따라서 가설 $\theta$를 가정할 때, 데이터가 $x$ 주변의 크기 $dx$인 작은 구간 안에 있을 확률은 $\phi(x\mid\theta)\,dx$이다.
- Posterior 사후분포 $f(\theta\mid x),d\theta$. 이는 데이터 $x$가 주어졌을 때, 매개변수가 $\theta$ 주변의 크기 $d\theta$인 작은 구간 안에 있을 계산된 확률이다.


|hypoth.|prior|likelihood|Bayes numerator|posterior|
|---|---|---|---|---|
|$\theta$|$f(\theta),d\theta$|$\phi(x\mid\theta)$|$\phi(x\mid\theta)f(\theta),d\theta$|$f(\theta\mid x),d\theta=\dfrac{\phi(x\mid\theta)f(\theta),d\theta}{\phi(x)}$|
|total (integrate over $\theta$)|$1$|no sum|$\phi(x)=\int \phi(x\mid\theta)f(\theta),d\theta$|$1$|

- Figure 1: 연속형-연속형 베이즈 업데이트 표    
#### To summarize:
- 가설의 사전확률과 가설이 주어졌을 때 데이터의 가능도가 주어진다.    
- Bayes numerator는 사전분포와 가능도의 곱이다.    
- 전체 가능도 $\phi(x)$는 Bayes numerator 열에 있는 확률들을 적분한 값이다.    
- Bayes numerator를 정규화하기 위해 $\phi(x)$로 나눈다.


### Normal begets normal
- 이제 연속-연속 업데이트의 중요한 예로 넘어간다: 정규분포는 자기 자신의 켤레 사전분포이다.  
- 특히 우도함수가 알려진 분산을 가진 정규분포라면, 정규 사전분포는 정규 사후분포를 준다.    
- 이제 가설과 데이터가 모두 연속적이다.    
- 분산 $\sigma^2$가 알려진 측정값 $x \sim N(\theta,\sigma^2)$가 있다고 하자.    
- 즉, 평균 $\theta$가 관심 있는 미지의 모수이고, 우도가 분산 $\sigma^2$인 정규분포에서 온다는 것이 주어져 있다.


- 정규 사전 확률밀도함수 $f(\theta) \sim N(\mu_{\text{prior}}, \sigma_{\text{prior}}^2)$를 선택하면 사후 확률밀도함수도 정규분포를 따른다: $f(\theta \mid x) \sim N(\mu_{\text{post}}, \sigma_{\text{post}}^2)$, 여기서  

$$  
\frac{\mu_{\text{post}}}{\sigma_{\text{post}}^2}=\frac{\mu_{\text{prior}}}{\sigma_{\text{prior}}^2}+\frac{x}{\sigma^2}, \quad \frac{1}{\sigma_{\text{post}}^2}=\frac{1}{\sigma_{\text{prior}}^2}+\frac{1}{\sigma^2}  
$$

- 다음 형태의 공식은 더 읽기 쉽고, $\mu_{\text{post}}$가 $\mu_{\text{prior}}$와 데이터 $x$ 사이의 가중평균임을 보여준다.  

$$  
a=\frac{1}{\sigma_{\text{prior}}^2}, \quad b=\frac{1}{\sigma^2}, \quad \mu_{\text{post}}=\frac{a\mu_{\text{prior}}+bx}{a+b}, \quad \sigma_{\text{post}}^2=\frac{1}{a+b}.  
$$


- 이 공식들을 염두에 두면, 업데이트를 다음 표로 표현할 수 있다:  

| 가설       | 데이터 | 사전분포                                                                                                                                              | 우도                                                                                             | 사후분포                                                                                                                                                |     |
| -------- | --- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| $\theta$ | $x$ | $f(\theta)\sim N(\mu_{\text{prior}},\sigma_{\text{prior}}^2)=c_1\exp\left(-\frac{(\theta-\mu_{\text{prior}})^2}{2\sigma_{\text{prior}}^2}\right)$ | $\phi(x\mid\theta)\sim N(\theta,\sigma^2)=c_2\exp\left(-\frac{(x-\theta)^2}{2\sigma^2}\right)$ | $f(\theta\mid x)\sim N(\mu_{\text{post}},\sigma_{\text{post}}^2)=c_3\exp\left(-\frac{(\theta-\mu_{\text{post}})^2}{2\sigma_{\text{post}}^2}\right)$ |     |

- 일반 공식의 증명은 직접 해보도록 남겨둔다.
- 이는 복잡한 대수적 조작이며, 본질적으로 다음 수치 예제와 같다.


#### Example
- 사전분포가 $\theta \sim N(4,8)$이고, 우도함수가 $x \sim N(\theta,5)$라고 하자.
- 또한 하나의 측정값 $x_1=3$이 있다고 하자.
- 사후분포가 정규분포임을 보여라.
#### Solution
- 완전제곱을 포함하는 대수 계산을 직접 수행하여 이를 보일 것이다.
- 사전분포:  

$$  
f(\theta)=c_1e^{-\frac{(\theta-4)^2}{16}}  
$$

- 우도:  

$$  
\phi(x_1\mid\theta)=c_2e^{-\frac{(x_1-\theta)^2}{10}}=c_2e^{-\frac{(3-\theta)^2}{10}}  
$$

#### Solution
- 사전분포와 우도를 곱하여 사후분포를 얻는다:  

$$  
f(\theta\mid x_1)=c_3e^{-\frac{(\theta-4)^2}{16}}e^{-\frac{(3-\theta)^2}{10}}=c_3\exp\left(-\frac{(\theta-4)^2}{16}-\frac{(3-\theta)^2}{10}\right)  
$$

- 지수에서 완전제곱을 한다:  

$$
\begin{aligned}
&-\frac{(\theta-4)^2}{16}-\frac{(3-\theta)^2}{10}\\  
&=-\frac{5(\theta-4)^2+8(3-\theta)^2}{80}  
=-\frac{13\theta^2-88\theta+152}{80}\\  
&=-\frac{\theta^2-\frac{88}{13}\theta+\frac{152}{13}}{80/13}  
=-\frac{\left(\theta-\frac{44}{13}\right)^2+\frac{152}{13}-\left(\frac{44}{13}\right)^2}{80/13}  
\end{aligned}
$$

- 따라서 사후분포는  

$$  
f(\theta\mid x_1)=c_3e^{-\frac{\left(\theta-\frac{44}{13}\right)^2+\frac{152}{13}-\left(\frac{44}{13}\right)^2}{80/13}}=c_4e^{-\frac{\left(\theta-\frac{44}{13}\right)^2}{80/13}}  
$$

- 이는 $N\left(\frac{44}{13},\frac{40}{13}\right)$의 확률밀도함수 형태이다. 증명 완료.

- 연습으로 이를 두 번째 공식들과 비교해 확인한다.  

$$  
\mu_{\text{prior}}=4,\quad \sigma_{\text{prior}}^2=8,\quad \sigma^2=5 \Rightarrow a=\frac{1}{8},\quad b=\frac{1}{5}  
$$

- 따라서  

$$  
\mu_{\text{post}}=\frac{a\mu_{\text{prior}}+bx}{a+b}=\frac{44}{13}=3.38,\quad \sigma_{\text{post}}^2=\frac{1}{a+b}=\frac{40}{13}=3.08  
$$

### A word on weighted averages
- 두 번째 업데이트 공식은 $\mu_{\text{post}}$를 $\mu_{\text{prior}}$와 데이터의 가중평균으로 제공한다.
- $\mu_{\text{prior}}$에 대한 가중치는 $\frac{a}{a+b}$이고, 데이터에 대한 가중치는 $\frac{b}{a+b}$이다.
- 이 가중치들은 항상 양수이며 합이 $1$이다.
- $b$가 매우 크다면, 즉 데이터의 분산이 매우 작다면, 대부분의 가중치는 데이터에 놓인다.
- $a$가 매우 크다면, 즉 $\sigma_{\text{prior}}^2$가 작다면, 다시 말해 사전분포에 매우 확신이 있다면, 대부분의 가중치는 사전분포에 놓인다.
- 위 예제에서 사전분포의 분산은 데이터의 분산보다 컸으므로 $a$는 $b$보다 작았다. 따라서 가중치는 대부분 데이터에 놓였다.
- 평균에 대한 사후분포의 값 $3.38$은 사전분포의 평균 $4$보다 데이터 $3$에 더 가까웠다.

#### Example
- 데이터가 $x\sim N\left(\theta,\frac{4}{9}\right)$임을 알고 있고, 사전분포가 $N(0,1)$이라고 하자.
- 하나의 데이터 값 $x=6.5$를 얻었다.
- 사전분포에서 사후분포로 업데이트할 때 $\theta$의 확률밀도함수가 어떻게 변하는지 설명하라.
#### Solution

$$  
\mu_{\text{prior}}=0,\quad \sigma_{\text{prior}}^2=1,\quad \sigma^2=\frac{4}{9}  
$$
- 따라서 두 번째 업데이트 공식을 사용하면  

$$  
a=1,\quad b=\frac{1}{4/9}=\frac{9}{4},\quad \mu_{\text{post}}=\frac{a\mu_{\text{prior}}+bx}{a+b}=4.5,\quad \sigma_{\text{post}}^2=\frac{1}{a+b}=\frac{4}{13}  
$$

- 다음은 사전 확률밀도함수와 사후 확률밀도함수의 그래프이며, 데이터 점은 빨간선으로 표시되어 있다.
- 그림 2: 사전분포는 파란색, 사후분포는 주황색, 데이터는 빨간선
- 사후평균이 사전평균보다 데이터 점에 더 가까움을 볼 수 있다.
- 또한 사후분포는 사전분포보다 더 높고 더 좁다. 즉, 분산이 더 작다.
- 분산이 더 작다는 것은 이제 $\theta$의 값이 어디에 있는지에 대해 우리가 더 확신하게 되었음을 의미한다.

#### Example
- 두 번째 공식을 사용하여 정규-정규 베이즈 업데이트에서 다음을 보여라:    
- 사후평균은 항상 데이터 점과 사전평균 사이에 있다.    
- 사후분산은 사전분산과 $\sigma^2$보다 모두 작다.    
- 즉, 우리의 사후 불확실성은 사전 불확실성과 데이터의 불확실성보다 모두 작다.

#### Solution
- 두 번째 업데이트 공식을 사용하면, 사후평균은 사전평균과 데이터의 가중평균이므로 반드시 사전평균과 데이터 사이에 있다.
- 또한 사후분산은  

$$  
\sigma_{\text{post}}^2=\frac{1}{a+b}<\frac{1}{a}=\sigma_{\text{prior}}^2  
$$

- 즉, 사후분포는 사전분포보다 더 작은 분산을 가진다. 다시 말해 데이터는 $\theta$가 그 범위 안에서 어디에 있는지에 대해 우리를 더 확신하게 만든다.
- 마찬가지로  

$$  
\sigma_{\text{post}}^2=\frac{1}{a+b}<\frac{1}{b}=\sigma^2  
$$
- 따라서 사후분산은 $\sigma^2$보다 작다.

### More than one data point
#### Example
- 데이터 $x_1,x_2,x_3$가 있다고 하자.
- 첫 번째 공식을 사용하여 순차적으로 업데이트하라.
#### Solution
- 사전평균과 사전분산을 각각 $\mu_0,\sigma_0^2$라고 하자.
- 업데이트된 평균과 분산은 각각 $\mu_i,\sigma_i^2$로 표기한다.
- 순서대로 계산하면 다음과 같다.  

$$  
\frac{1}{\sigma_1^2}=\frac{1}{\sigma_0^2}+\frac{1}{\sigma^2},\quad \frac{\mu_1}{\sigma_1^2}=\frac{\mu_0}{\sigma_0^2}+\frac{x_1}{\sigma^2}  
$$  

$$  
\frac{1}{\sigma_2^2}=\frac{1}{\sigma_1^2}+\frac{1}{\sigma^2}=\frac{1}{\sigma_0^2}+\frac{2}{\sigma^2},\quad \frac{\mu_2}{\sigma_2^2}=\frac{\mu_1}{\sigma_1^2}+\frac{x_2}{\sigma^2}=\frac{\mu_0}{\sigma_0^2}+\frac{x_1+x_2}{\sigma^2}  
$$  

$$  
\frac{1}{\sigma_3^2}=\frac{1}{\sigma_2^2}+\frac{1}{\sigma^2}=\frac{1}{\sigma_0^2}+\frac{3}{\sigma^2},\quad \frac{\mu_3}{\sigma_3^2}=\frac{\mu_2}{\sigma_2^2}+\frac{x_3}{\sigma^2}=\frac{\mu_0}{\sigma_0^2}+\frac{x_1+x_2+x_3}{\sigma^2}  
$$

- 위 예제는 $n$개의 데이터 값 $x_1,\ldots,x_n$으로 일반화된다.
- $n$개의 데이터 점에 대한 정규-정규 업데이트 공식:  

$$  
\frac{\mu_{\text{post}}}{\sigma_{\text{post}}^2}=\frac{\mu_{\text{prior}}}{\sigma_{\text{prior}}^2}+\frac{n\bar{x}}{\sigma^2},\quad \frac{1}{\sigma_{\text{post}}^2}=\frac{1}{\sigma_{\text{prior}}^2}+\frac{n}{\sigma^2},\quad \bar{x}=\frac{x_1+\cdots+x_n}{n}  
$$

- 다시 말해, $\mu_{\text{post}}$가 $\mu_{\text{prior}}$와 표본평균 $\bar{x}$의 가중평균임을 보여주는 더 읽기 쉬운 형태는 다음과 같다:  

$$  
a=\frac{1}{\sigma_{\text{prior}}^2},\quad b=\frac{n}{\sigma^2},\quad \mu_{\text{post}}=\frac{a\mu_{\text{prior}}+b\bar{x}}{a+b},\quad \sigma_{\text{post}}^2=\frac{1}{a+b}  
$$

#### Interpretation
- $\mu_{\text{post}}$는 $\mu_{\text{prior}}$와 $\bar{x}$의 가중평균이다.    
- 데이터의 개수 $n$이 크다면 가중치 $b$가 커지고, $\bar{x}$가 사후분포에 강한 영향을 미친다.    
- $\sigma_{\text{prior}}^2$가 작다면 가중치 $a$가 커지고, $\mu_{\text{prior}}$가 사후분포에 강한 영향을 미친다.    
#### To summarize:
- 많은 데이터는 사후분포에 큰 영향을 준다.    
- 사전분포에 대한 높은 확신(작은 분산)은 사후분포에 큰 영향을 준다.    
- 실제 사후분포는 이 두 영향 사이의 균형이다.

