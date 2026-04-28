2026-04-23 08:20
## 15강 Maximum Likelihood Estimates



### Learning Goals
- 주어진 데이터에 대해 모수적 모형(parametric model)의 우도함수(likelihood function)를 정의할 수 있어야 한다.    
- 미지의 모수(parameter)에 대한 최대우도추정량(maximum likelihood estimate)을 계산할 수 있어야 한다.


### Introduction
- 값 $x_1,\dots,x_n$으로 이루어진 데이터가 지수분포(exponential distribution)에서 추출되었다고 알고 있다고 하자.    
- 그러나 여전히 질문은 남는다. 어느 지수분포인가?    
- 우리는 흔히 지수분포, 이항분포(binomial distribution), 정규분포(normal distribution)라고 가볍게 말한다.    
	- 사실 $\operatorname{exp}(\lambda)$는 하나의 단일 분포가 아니라, 하나의 parameter를 가진 분포족(family of distributions)이다.    
	- 각 $\lambda$ 값은 그 분포족 안에서 서로 다른 분포를 정의하며, 확률밀도함수(pdf)는 다음과 같다.  
$$f_\lambda(x)=\lambda e^{-\lambda x},\quad x\in[0,\infty)$$
- 마찬가지로 이항분포 $\operatorname{bin}(n,p)$는 두 parameter $n,p$에 의해 결정된다.
- 정규분포 $N(\mu,\sigma^2)$는 두 parameter $\mu,\sigma^2$에 의해 결정된다.
- 이처럼 parameter(모수)로 표현되는 분포족을 보통 모수적 분포(parametric distributions) 또는 모수적 모형(parametric models)이라 한다.

- 다양한 통계적 추론을 배우게 될 것.
- 지수분포에서 추론한다고 해도 어떤 지수분포인지 확인하는 과정이 남아있음
- 보통 람다를 추론해야함.
- 어떤 분포인지 알아도 파라미터를 추론하는것이 중요한 과정임.


- 우리는 종종 무작위 데이터가 어떤 모수적 모형(parametric model)에서 나왔다고 알고 있거나 그렇게 믿지만, 그 parameter의 값은 알지 못하는 상황에 놓인다.    
- 예를 들어 두 후보가 경쟁하는 선거에서, 여론조사 데이터는 미지의 모수 $p$를 가진 $Bernoulli(p)$ 분포에서 나온 표본으로 볼 수 있다.    
- 이 경우 $p$는 선거 결과를 예측하므로, 데이터를 이용해 모수 $p$의 값을 추정하고자 한다.    
- 마찬가지로 임신 기간이 정규분포를 따른다고 가정하면, 무작위로 추출한 임신 사례들의 기간 데이터를 사용하여 모수 $\mu$와 $\sigma^2$의 값에 대해 추론하고자 한다.


- 지금까지 우리의 초점은 parameter가 알려진 모수적 모형(parametric model)에서 데이터가 발생할 확률을 계산하는 데 있었다.    
- 통계적 추론(statistical inference)은 이를 거꾸로 뒤집는다. 즉, 주어진 모수적 모형과 관측된 데이터를 바탕으로 모수에 대한 확률을 추정한다.    
- 앞으로 배우게 되겠지만, 모수값은 자연스럽게 가설(hypotheses)로 해석될 수 있다.    
- 따라서 우리는 실제로 데이터가 주어졌을 때 다양한 가설들의 확률을 추정하고 있는 것이다.

- 확률은 파라미터가 알려진 모형에서 데이터가 발생활 확률 → 통계는 관측된 데이터를 바탕으로 파라미터를 추론론



### Maximum Likelihood Estimates
- 데이터로부터 미지의 모수를 추정하는 방법은 많이 있다.    
- 우리는 먼저 최대우도추정(maximum likelihood estimate, MLE)을 살펴볼 것이다.    
	- MLE는 "어떤 parameter 값에서 관측된 데이터가 가장 큰 확률을 가지는가?"라는 질문에 답한다.  
- MLE는 미지의 모수에 대해 하나의 값만 제시하므로 점추정(point estimate)의 한 예이다.    
- (이후에는 구간(interval)과 확률(probabilities)을 포함하는 추정도 다루게 된다.)    
- MLE의 두 가지 장점은, 계산이 쉬운 경우가 많고 간단한 예제에서 우리의 직관과 잘 맞는다는 점이다.    
- 우리는 일련의 예제를 통해 MLE를 설명할 것이다.

- MLE는 계산하기 쉽고 직관이랑 잘 맞는다는 장점이 있음.


#### Example
- 동전을 100번 던졌다.
- 앞면이 55번 나왔을 때, 한 번 던질 때 앞면이 나올 확률 $p$의 최대우도추정량(MLE)을 구하라.
- 실제로 문제를 풀기 전에 몇 가지 기호와 용어를 정하자.
- 100번 던져서 앞면의 개수를 세는 과정을 하나의 실험(experiment)으로 볼 수 있다.
- 주어진 $p$ 값에 대해, 이 실험에서 앞면이 55번 나올 확률은 이항확률(binomial probability)이다.  
$$P(\text{55 heads})=\binom{100}{55}p^{55}(1-p)^{45}$$


- 실험: 100번 동전을 던지는 것
- 데이터: 55번 앞면이 나오는 것
- 확률: 데이터의 결과로 계산

- 55번 앞면이 나올 확률은 $p$의 값에 따라 달라지므로, 조건부확률 표기를 사용하여 $p$를 포함시키자.  
$$P(\text{55 heads}\mid p)=\binom{100}{55}p^{55}(1-p)^{45}$$

- $P(\text{55 heads}\mid p)$는 다음과 같이 읽는다.
- "$p$가 주어졌을 때 55번 앞면이 나올 확률"
- 더 정확히는 "한 번 던질 때 앞면이 나올 확률이 $p$라고 할 때, 55번 앞면이 나올 확률"


- 통계를 공부하면서 사용할 몇 가지 표준 용어를 정리하자.    
- 실험(Experiment): 동전을 100번 던져 앞면의 개수를 센다.    
- 데이터(Data): 실험의 결과이다.    
- 이 경우 데이터는 "앞면 55번"이다.    
- 관심 있는 모수(Parameter(s) of interest): 우리는 미지의 모수 $p$의 값에 관심이 있다.    
- 우도(Likelihood), 또는 Likelihood함수(likelihood function): 이것은 $P(\text{data}\mid p)$이다.    
- 이는 데이터와 모수 $p$ 둘 다의 함수라는 점에 유의하라.    
- 이 경우 Likelihood는 다음과 같다.  
$$P(\text{55 heads}\mid p)=\binom{100}{55}p^{55}(1-p)^{45}$$

#### Note
- 우도 $P(\text{data}\mid p)$는 관심 있는 모수 $p$가 변함에 따라 함께 변한다.    
- 정의를 주의 깊게 보아라.    
- 흔한 혼동 중 하나는 우도 $P(\text{data}\mid p)$를 $P(p\mid \text{data})$와 혼동하는 것이다.    
- 우리는 앞서 Bayes' theorem을 통해 $P(\text{data}\mid p)$와 $P(p\mid \text{data})$가 보통 매우 다르다는 것을 알고 있다.

#### Definition    
- 주어진 데이터에 대해 모수 $p$의 최대우도추정량(maximum likelihood estimate, MLE)은 우도 $P(\text{data}\mid p)$를 **최대화하는 $p$의 값**이다.    
- 즉, MLE는 주어진 데이터가 가장 그럴듯하게 발생하도록 만드는 $p$의 값이다.


#### Solution
- 현재 문제에서 우도는 다음과 같다.  
$$P(55\text{ heads}\mid p)=\binom{100}{55}p^{55}(1-p)^{45}$$

- MLE는 $\hat{p}$로 표기하자.
- 우도함수를 미분한 뒤 $0$으로 두어 값을 구한다.  
$$\frac{d}{dp}P(\text{data}\mid p)=\binom{100}{55}\left(55p^{54}(1-p)^{45}-45p^{55}(1-p)^{44}\right)=0$$


#### Solution
- 이를 $p$에 대해 풀면 다음과 같다.  
$$55p^{54}(1-p)^{45}=45p^{55}(1-p)^{44}$$  
$$55(1-p)=45p$$  
$$55=100p$$

- 따라서 최대우도추정량은  
$$\hat{p}=0.55$$

#### Note
- 1. $p$의 MLE는 데이터에서 관측한 앞면의 비율과 정확히 일치한다.
- 2. **MLE는 데이터로부터 계산되므로 하나의 통계량(statistic)** 이다.




- 3. 공식적으로는 이 임계점이 실제로 최댓값인지 확인해야 한다.
- 이를 위해 이계도함수 판정(second derivative test)을 사용할 수 있다.
- 또 다른 방법은 우리가 관심 있는 범위가 $0\le p\le 1$뿐이라는 점을 이용하는 것이다. 
- $0<p<1$에서는 확률이 $0$보다 크고, $p=0$ 또는 $p=1$에서는 확률이 $0$이 된다.    
- 따라서 이 사실들로부터, 구한 임계점이 유일한 최댓값임을 알 수 있다.

- 미분한 값을 0으로 계산 했을때 이 값이 실제 최대인지 확인을 해야함.
- convex 인지확인 해야 하고, 최대 값이 1개만 있는지 확인 해야 함.

### Log likelihood
- 우도함수 자체보다 그 자연로그를 사용하는 것이 더 쉬운 경우가 많다.    
- 이를 간단히 로그우도(log likelihood)라고 한다.    
- $\ln(x)$는 증가함수이므로, 우도함수의 최댓값과 로그우도함수의 최댓값은 서로 일치한다.

- MLE보다 log likelihood 가 더 편함.
- 로그 함수는 증가 함수여서 MLE와 둘다 최대값이 일치 함.


#### Example
- 이전 예제를 로그우도를 사용하여 다시 풀어보자.
#### Solution
- 이전에 우도는 다음과 같았다.  
$$P(55\text{ heads}\mid p)=\binom{100}{55}p^{55}(1-p)^{45}$$

- 따라서 로그우도는 다음과 같다.  
$$\ln\!\big(P(55\text{ heads}\mid p)\big)=\ln\!(\binom{100}{55})+55\ln(p)+45\ln(1-p)$$

#### Solution
- 우도를 최대화하는 것은 로그우도를 최대화하는 것과 같다.
- 미적분을 사용하면 이전과 같은 답을 얻는다.  
$$\frac{d}{dp}(\text{log likelihood})=\frac{d}{dp}\left[\ln\binom{100}{55}+55\ln(p)+45\ln(1-p)\right]$$  
$$=\frac{55}{p}-\frac{45}{1-p}=0$$  
$$55(1-p)=45p$$  
$$\hat{p}=0.55$$

### Maximum likelihood for continuous distributions
- 연속형 분포(continuous distributions)에서는 우도를 정의할 때 확률질량함수 대신 확률밀도함수(probability density function)를 사용한다.    
- 몇 가지 예제를 통해 이를 살펴보겠다.    
- 아래에서는 이것이 이산형 경우에 했던 것과 어떻게 대응되는지도 설명할 것이다.    
#### Example (Light bulbs)
- 전구의 수명이 미지의 모수 $\lambda$를 가진 지수분포(exponential distribution)로 모형화된다고 하자.    
- 전구 5개를 시험했더니 수명이 각각 $2,3,1,3,4$년이었다.    
- $\lambda$의 최대우도추정량(MLE)을 구하여라.


#### Solution
- 표기에 주의해야 한다.
- 값이 다섯 개이므로 아래첨자를 사용하는 것이 가장 좋다.
- $X_i$를 $i$번째 전구의 수명이라 하고, $x_i$를 $X_i$가 실제로 가진 값이라 하자.
- 그러면 각 $X_i$의 확률밀도함수는 다음과 같다.  
$$f_{X_i}(x_i)=\lambda e^{-\lambda x_i}$$

- 전구들의 수명이 서로 독립(independent)이라고 가정하면, 결합확률밀도함수(joint pdf)는 각 밀도의 곱이다.  
$$f(x_1,x_2,x_3,x_4,x_5\mid \lambda)=(\lambda e^{-\lambda x_1})(\lambda e^{-\lambda x_2})(\lambda e^{-\lambda x_3})(\lambda e^{-\lambda x_4})(\lambda e^{-\lambda x_5})$$  
$$=\lambda^5 e^{-\lambda(x_1+x_2+x_3+x_4+x_5)}$$


- 대문자 X는 확률변수
- 소문자 x는 확률변수 X가 갖을수 있는 값값


- 이것이 $\lambda$에 의존하므로 조건부 밀도(conditional density) 형태로 쓴다는 점에 주의하라.
- 데이터를 고정하고 $\lambda$를 변수로 보면, 이 밀도함수가 바로 우도함수(likelihood function)이다.
- 주어진 데이터는 $x_1=2,\;x_2=3,\;x_3=1,\;x_4=3,\;x_5=4$이다.
- 따라서 우도함수와 로그우도함수는 다음과 같다.  
$$f(2,3,1,3,4\mid \lambda)=\lambda^5 e^{-13\lambda}$$  
$$\ln\!\big(f(2,3,1,3,4\mid \lambda)\big)=5\ln(\lambda)-13\lambda$$

- 이제 미적분을 사용하여 MLE를 구하면,  
$$\frac{d}{d\lambda}(\text{log likelihood})=\frac{5}{\lambda}-13=0$$  
$$\hat{\lambda}=\frac{5}{13}$$

#### Note
- 이 예제에서는 확률변수(random variable)를 대문자로, 그 변수가 실제로 취한 값을 대응되는 소문자로 나타냈다.
- 이것은 앞으로의 기본 표기법으로 사용할 것이다.
- $\lambda$의 MLE는 표본평균 $\bar{x}$의 역수로 나타난다.  
$$\hat{\lambda}=\frac{1}{\bar{x}}$$

- 따라서 $X\sim \operatorname{exp}(\hat{\lambda})$라면  satisfies $E[X]=\bar{x}$

- 다음 예제는 최대우도법(maximum likelihood)을 사용하여 여러 모수를 동시에 추정하는 방법을 보여준다.
#### Example(Normal distribution)
- 데이터 $x_1,x_2,\dots,x_n$이 $N(\mu,\sigma^2)$ 분포에서 나왔다고 하자.
- 여기서 $\mu$와 $\sigma$는 미지이다.
- 쌍 $(\mu,\sigma^2)$의 최대우도추정량(MLE)을 구하여라.
#### Solution
- 이를 확률변수와 밀도의 언어로 정확히 표현하자.
- 대문자 $X_1,\dots,X_n$을 서로 독립이고 동일분포(i.i.d.)인 $N(\mu,\sigma^2)$ 확률변수라 하자.
- 소문자 $x_i$는 $X_i$가 실제로 취한 값이다.


- 각 $X_i$의 확률밀도함수는 다음과 같다.  
$$f_{X_i}(x_i)=\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{(x_i-\mu)^2}{2\sigma^2}}$$

- $X_i$들이 서로 독립이므로, 결합확률밀도함수(joint pdf)는 각 확률밀도함수의 곱이다.  
$$f(x_1,\dots,x_n\mid \mu,\sigma)=\left(\frac{1}{\sqrt{2\pi}\sigma}\right)^n e^{-\frac{\sum_{i=1}^{n}(x_i-\mu)^2}{2\sigma^2}}$$

- 상수에 n제곱, 지수를 n까지 sum


- 고정된 데이터 $x_1,\dots,x_n$에 대해 우도함수와 로그우도함수는 다음과 같다.  
$$f(x_1,\dots,x_n\mid \mu,\sigma)=\left(\frac{1}{\sqrt{2\pi}\sigma}\right)^n e^{-\frac{\sum_{i=1}^{n}(x_i-\mu)^2}{2\sigma^2}}$$  
$$\ln!\big(f(x_1,\dots,x_n\mid \mu,\sigma)\big)=-n\ln(\sqrt{2\pi})-n\ln(\sigma)-\frac{\sum_{i=1}^{n}(x_i-\mu)^2}{2\sigma^2}$$

- $\ln(f(x_1,\dots,x_n\mid \mu,\sigma))$는 두 변수 $\mu,\sigma$의 함수이므로, MLE를 구하기 위해 편미분(partial derivatives)을 사용한다.
- 먼저 쉽게 구할 수 있는 값은 $\hat{\mu}$이다.  
$$\frac{\partial}{\partial \mu}\ln(f(x_1,\dots,x_n\mid \mu,\sigma))=\frac{\sum_{i=1}^{n}(x_i-\mu)}{\sigma^2}=0$$  
$$\sum_{i=1}^{n}x_i=n\mu$$  
$$\hat{\mu}=\frac{\sum_{i=1}^{n}x_i}{n}=\bar{x}$$

- $\hat{\sigma}$를 구하기 위해 $\sigma$에 대해 미분하고 풀면 된다.  
$$\frac{\partial}{\partial \sigma}\ln(f(x_1,\dots,x_n\mid \mu,\sigma))=-\frac{n}{\sigma}+\frac{\sum_{i=1}^{n}(x_i-\mu)^2}{\sigma^3}=0$$  
$$\hat{\sigma}^2=\frac{\sum_{i=1}^{n}(x_i-\mu)^2}{n}$$

- 이미 $\hat{\mu}=\bar{x}$임을 알고 있으므로, $\hat{\sigma}$의 식에서 $\mu$ 대신 그 값을 대입한다.
- 따라서 최대우도추정량은 다음과 같다.  
$$\hat{\mu}=\bar{x}=\text{데이터의 평균}$$  
$$\hat{\sigma}^2=\frac{1}{n}\sum_{i=1}^{n}(x_i-\hat{\mu})^2=\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2=\text{unadjusted variance데이터의 비보정 분산}$$

- 나중에 배우겠지만, 표본분산(sample variance)은  
$$\frac{\sum_{i=1}^{n}(x_i-\hat{\mu})^2}{n-1}$$



#### Example (Uniform distributions_균등분포)
- 데이터 $x_1,\dots,x_n$이 서로 독립적으로 균등분포 $U(a,b)$에서 추출되었다고 하자.
- $a$와 $b$의 최대우도추정량(MLE)을 구하여라.
#### Solution
- 이 예제는 앞선 예제들과 달리, 미적분을 사용하지 않고 MLE를 구한다.
- $U(a,b)$의 확률밀도함수는 구간 $[a,b]$에서 다음과 같다.  
$$\frac{1}{b-a}$$

- 따라서 우도함수는 다음과 같다.  
$$f(x_1,\dots,x_n\mid a,b)=\begin{cases}\left(\frac{1}{b-a}\right)^n,&\text{모든 }x_i\text{가 }[a,b]\text{에 있을 때}\\0,&\text{그 외의 경우}\end{cases}$$
$$  
f(x_1,\dots,x_n\mid a,b)=  
\begin{cases}  
\left(\frac{1}{b-a}\right)^n, & \text{if all } x_i \text{ are in the interval } [a,b] \\  
0, & \text{otherwise}  
\end{cases}  
$$

- 이 값은 $b-a$를 가능한 한 작게 만들 때 최대가 된다.


- 유일한 조건은 구간 $[a,b]$가 모든 데이터를 포함해야 한다는 것이다.
- 따라서 쌍 $(a,b)$의 최대우도추정량은 다음과 같다.  
$$\hat{a}=\min(x_1,\dots,x_n) \quad \hat{b}=\max(x_1,\dots,x_n)$$


#### Example (Capture/recapture method)
- 포획-재포획 방법은 야생 개체군(population)의 크기를 추정하는 방법이다.    
- 이 방법은 개체군의 각 동물이 덫에 잡힐 가능성이 모두 같다고 가정한다.    
- 먼저 동물 10마리를 포획하여 표식을 붙인 뒤 다시 풀어준다.    
- 몇 달 후 동물 20마리를 다시 포획하여 조사한 뒤 풀어준다.    
- 이 20마리 중 4마리가 표식이 있는 것으로 확인되었다.    
- 표식이 있는 동물이 포획될 확률의 MLE를 이용하여 전체 개체군의 크기를 추정하여라.
#### 참고) GPT_Solution
- 전체 개체군의 크기를 $N$이라 하자.    
- 표식이 있는 동물은 10마리이므로, 임의의 동물이 표식되어 있을 확률은  
$$p=\frac{10}{N}$$

- 두 번째 포획에서 20마리 중 4마리가 표식되어 있었으므로, 이는 $Binomial(20,p)$ 모형으로 볼 수 있다. 
- 이항분포에서 성공확률의 MLE는 표본비율이므로  
$$\hat{p}=\frac{4}{20}=0.2$$

- 따라서  
$$\frac{10}{N}=0.2$$  
$$N=\frac{10}{0.2}=50$$

- 그러므로 야생 개체군의 크기에 대한 추정값은  
$$\hat{N}=50$$

#### Solution
- 미지의 모수 $n$은 야생에 존재하는 전체 동물의 수이다.
- 데이터는 재포획한 20마리 중 4마리가 표식되어 있었다는 사실(그리고 표식된 동물이 총 10마리라는 사실)이다.
- 우도함수는 다음과 같다.  
$$P(\text{data}\mid n\text{ animals})=\frac{\binom{n-10}{16}\binom{10}{4}}{\binom{n}{20}}$$

- 분자의 의미는 다음과 같다.
- 표식이 없는 $n-10$마리 중에서 16마리를 고르는 경우의 수
- 표식된 10마리 중에서 4마리를 고르는 경우의 수
- 이 둘을 곱하면, 재포획된 20마리 중 정확히 4마리가 표식된 경우의 수가 된다.
- 분모는 전체 $n$마리 중에서 20마리를 고르는 전체 경우의 수이다.


- 베이시안 룰로 풀면됨. 분모는 데이터가 안주어졌을 때 경우의수 분자는 각각 상황의 경우의수를 곱해주면 됨.

#### Solution
- Python을 사용해 계산해 보면, 우도함수는 $n=50$일 때 최대가 된다.    
- 이는 어느 정도 직관적으로도 이해할 수 있다.    
- 즉, 전체 동물 중 표식된 동물의 비율에 대한 최선의 추정값은  $\frac{10}{50}$ 이고, 이것은 재포획된 동물 중 표식된 비율과 같다.


#### Example (Hardy-Weinberg)

- 어떤 특정 유전자가 두 대립유전자(alleles) $A$와 $a$ 중 하나로 존재한다고 하자.
- 대립유전자 $A$의 집단 내 빈도는 $\theta$이다.
- 즉, 유전자의 무작위 복사본 하나가 $A$일 확률은 $\theta$, $a$일 확률은 $1-\theta$이다.
- 이배체(diploid) 유전자형은 두 개의 유전자로 이루어지므로, 각 유전자형의 확률은 다음과 같다.  

| genotype    | AA         | Aa                  | aa             |
| ----------- | ---------- | ------------------- | -------------- |
| probability | $\theta^2$ | $2\theta(1-\theta)$ | $(1-\theta)^2$ |

- 사람들을 무작위 표본으로 검사했더니, $k_1$명은 $AA$, $k_2$명은 $Aa$, $k_3$명은 $aa$였다.
- $\theta$의 최대우도추정량(MLE)을 구하여라.


#### Solution
- 우도함수(likelihood function)는 다음과 같다.  
$$  
P(k_1,k_2,k_3\mid \theta)=\binom{k_1+k_2+k_3}{k_1}\binom{k_2+k_3}{k_2}\binom{k_3}{k_3}\theta^{2k_1}\big(2\theta(1-\theta)\big)^{k_2}(1-\theta)^{2k_3}  
$$

- 따라서 로그우도(log likelihood)는 다음과 같다.  
$$  
\text{constant}+2k_1\ln(\theta)+k_2\ln(\theta)+k_2\ln(1-\theta)+2k_3\ln(1-\theta)  
$$


- 도함수를 $0$으로 두면 다음과 같다.  
$$\frac{2k_1+k_2}{\theta}-\frac{k_2+2k_3}{1-\theta}=0$$
- 이를 $\theta$에 대해 풀면, 최대우도추정량은 다음과 같다.  
$$\hat{\theta}=\frac{2k_1+k_2}{2k_1+2k_2+2k_3}$$

- 이는 표본으로 뽑은 집단의 모든 유전자들 중에서 대립유전자 $A$가 차지하는 비율과 정확히 같다.


- 분모는 모든 유전자형의 사람의의 합
- 분자는 대립유전자가 해당하는 사람의 수


- 최대우도추정(maximum likelihood estimate)의 핵심 아이디어는, 주어진 데이터가 가장 높은 확률을 갖도록 만드는 모수값을 찾는 것이다.    
- 아래에서는 밀도함수(density)를 사용할 때도 본질적으로 같은 일을 하고 있음을 보게 된다.    
- 이를 위해 전구 예제를 더 작은 규모로 살펴보자.    
#### Example
- 수명이 지수분포 $\operatorname{exp}(\lambda)$를 따르는 전구 두 개가 있다고 하자.    
- 두 전구의 수명을 서로 독립적으로 측정했더니, 데이터가 $x_1=2$년, $x_2=3$년이었다.    
- 이 데이터의 확률(밀도)을 최대화하는 $\lambda$의 값을 구하여라.

- 연속의 경우도 같은지 확인 해봐야 함.


#### Solution
- 먼저 해결해야 할 핵심 역설은, 연속형 분포에서는 특정한 하나의 값, 예를 들어 $x_1=2$일 확률이 $0$이라는 점이다.    
- 이 역설은 실제 측정값이 정확한 한 점이 아니라 어떤 구간(range)을 의미한다고 생각하면 해결된다.    
- 예를 들어 이 경우 전구를 하루에 한 번씩 점검한다고 하자.    
- 그러면 데이터 $x_1=2$년은 실제로 $x_1$이 2년을 중심으로 한 약 1일 정도의 구간 어딘가에 있다는 뜻이다.


#### Solution
- 그 구간이 매우 작다면 이를 $dx_1$이라 하자.    
- 그러면 $X_1$이 그 구간 안에 있을 확률은 다음과 같이 근사된다.  
$$f_{X_1}(x_1\mid \lambda)\,dx_1$$
- 이는 확률밀도함수 값에 작은 구간의 길이를 곱한 것이다.
- 데이터 값 $x_2$도 정확히 같은 방식으로 다룬다.

#### Solution
- 데이터가 서로 독립적으로 수집되었으므로, 결합확률은 각 확률의 곱이다.
- 정확히 쓰면 다음과 같다.  
$$P(X_1\text{ in range},X_2\text{ in range}\mid \lambda)\approx f_{X_1}(x_1\mid \lambda),dx_1\cdot f_{X_2}(x_2\mid \lambda),dx_2$$
- 이제 $x_1=2,\;x_2=3$과 지수분포의 확률밀도함수를 대입하면,  
$$P(X_1\text{ in range},X_2\text{ in range}\mid \lambda)\approx \lambda e^{-2\lambda}dx_1\cdot \lambda e^{-3\lambda}dx_2$$  
$$=\lambda^2 e^{-5\lambda}dx_1dx_2$$

- 이제 실제 확률을 얻었으므로, 이를 최대화하는 $\lambda$ 값을 찾을 수 있다.    
- 위 식을 보면 $dx_1dx_2$ 항은 최댓값을 찾는 데 아무 역할을 하지 않는다.    
- 따라서 MLE를 구할 때는 이를 제외하고 밀도함수를 그대로 우도(likelihood)라 부른다.  
$$\text{likelihood}=f(x_1,x_2\mid \lambda)=\lambda^2e^{-5\lambda}$$

- 이를 최대화하는 $\lambda$는 앞선 예제와 같은 방식으로 구한다.  
$$\hat{\lambda}=\frac{2}{5}$$

- 관심 있는 학생들을 위해, 최대우도추정량(MLE)의 몇 가지 좋은 성질을 소개한다.    
- MLE는 변환(transformations)에 대해 좋은 성질을 가진다.    
- 즉, $\hat{p}$가 $p$의 MLE이고, $g$가 일대일 함수(one-to-one function)라면 $g(\hat{p})$는 $g(p)$의 MLE이다.    
- 예를 들어, $\hat{\sigma}$가 표준편차 $\sigma$의 MLE라면  $(\hat{\sigma})^2$ 는 분산 $\sigma^2$의 MLE이다.

- 더 나아가, 몇 가지 기술적인 매끄러움 조건(smoothness assumptions) 아래에서 MLE는 점근적으로 불편향(asymptotically unbiased)이며 점근적으로 최소 분산(asymptotically minimal variance)을 가진다.
- 이 개념들을 설명하기 위해, **MLE 자체도 하나의 확률변수(random variable)** 라는 점에 주의하자.
- 데이터가 무작위이고, MLE는 그 데이터로부터 계산되기 때문이다.
- 모수 $p$를 가진 분포에서 나온 무한한 표본열 $x_1,x_2,\dots$를 생각하자.
- 그리고 데이터 $x_1,\dots,x_n$을 바탕으로 계산한 $p$의 MLE를 $\hat{p}_n$이라 하자.




- 점근적으로 불편향(asymptotically unbiased)이라는 것은 데이터의 양이 증가할수록 MLE의 평균이 $p$에 수렴한다는 뜻이다.
- 기호로 쓰면 다음과 같다.  
$$E[\hat{p}_n]\to p\quad\text{as }n\to\infty$$
- 물론 우리는 단지 평균적으로만이 아니라, 높은 확률로 MLE가 $p$에 가까워지기를 원한다.
- 따라서 MLE의 분산(variance)은 작을수록 좋다.
- 점근적으로 최소 분산(asymptotically minimal variance)이란 데이터의 양이 커질수록, MLE가 $p$의 모든 불편추정량(unbiased estimators) 가운데 가장 작은 분산을 가진다는 뜻이다.
- 기호로 쓰면, 임의의 불편추정량 $\tilde{p}_n$과 모든 $\epsilon>0$에 대하여  
$$\operatorname{Var}(\tilde{p}_n)+\epsilon>\operatorname{Var}(\hat{p}_n)\quad\text{as }n\to\infty$$


- 문제는 우리가 데이터가 충분히 무한에 가까운 경우는 거의 없음


