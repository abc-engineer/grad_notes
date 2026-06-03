2026-05-21 08:20
## 22강 Null Hypothesis Significance Testing 2

## Contents / Memo



- 비슷한데 좀더 다양한 test에 대해 이야기 할 것.

### Learning Goals
- 모든 귀무가설 유의성 검정(null hypothesis significance test)에 공통적인 단계들을 나열할 수 있어야 한다.    
- 제1종 오류(type I error)와 제2종 오류(type II error)의 확률을 정의하고 계산할 수 있어야 한다.    
- 일표본(one-sample) 및 이표본(two-sample) t-test를 찾아보고 적용할 수 있어야 한다.

### Introduction
- 우리는 유의성 검정에 대한 공부를 계속한다.    
- 이 노트에서는 두 가지 새로운 검정인 일표본 t-검정과 이표본 t-검정을 소개한다.    
- 모든 검정은 데이터에 대한 몇 가지 가정을 한다는 점에 주의해야 하며, 이는 종종 데이터가 정규분포에서 추출되었다는 가정이다.    
- 또한 모든 검정이 같은 패턴을 따른다는 점도 알아야 한다.    
- 달라지는 것은 검정통계량의 계산 방식과 귀무분포의 유형뿐이다.


### Review: Setting up and running a significance tes
- 귀무가설 유의성 검정(null hypothesis significance test)을 설정하고 수행하기 위해 따르는 상당히 표준적인 단계들이 있다.    
- 1. 데이터를 수집하기 위한 실험을 설계하고, 데이터로부터 계산할 검정통계량 $x$를 선택한다.        
	- 여기서 핵심 요구사항은 귀무분포 $\phi(x \mid H_0)$를 아는 것이다.    
	- 검정력(power)을 계산하려면 대립분포 $\phi(x \mid H_A)$도 알아야 한다.    
- 2. $H_A$와 귀무분포의 형태를 바탕으로 검정이 단측(one-sided)인지 양측(two-sided)인지 결정한다.       
- 3. 귀무가설(null hypothesis)을 기각하기 위한 유의수준 $\alpha$를 선택한다.


- 4. 검정에서 원하는 검정력(power)을 달성하기 위해 얼마나 많은 데이터를 수집해야 하는지 결정한다.
- 5. 실험을 수행하여 데이터 $x_1,x_2,\ldots,x_n$을 수집한다.
- 6. 검정통계량 $x$를 계산한다.
- 7. 귀무분포(null distribution)를 사용하여 $x$에 대응하는 p-value를 계산한다.
- 8. 만약 $p<\alpha$이면, 대립가설(alternative hypothesis)을 지지하며 귀무가설(null hypothesis)을 기각한다.

#### Note 1
- 유의수준(significance level)을 선택하는 대신 기각역(rejection region)을 직접 선택하고, $x$가 이 영역에 속하면 $H_0$를 기각할 수도 있다.
- 이때 대응되는 유의수준은 $H_0$를 가정했을 때 $x$가 기각역에 속할 확률이다.
#### Note 2
- 귀무가설(null hypothesis)은 종종 “보수적인 가설(cautious hypothesis)”이다.
- 유의수준을 더 낮게 설정할수록, 더 자극적인 대립가설(alternative hypothesis)을 지지하며 보수적인 가설을 기각하기 위해 더 많은 “증거(evidence)”를 요구하게 된다.
- 다른 사람들이 스스로 결론을 내릴 수 있도록 p-value 자체를 함께 공개하는 것이 표준적인 관행이다.

#### Note 3
- 중요한 혼동 지점: 유의수준(significance level)이 $0.05$라는 것은 검정이 단지 $5\%$만 실수한다는 뜻이 아니다.
- 이는 귀무가설(null hypothesis)이 참일 때, 검정이 이를 잘못 기각할 확률이 $5$라는 의미이다.
- 검정력(power)은 대립가설(alternative hypothesis)이 참일 때 검정의 정확성을 측정한다.
- 즉, 검정력은 대립가설이 참일 때 귀무가설을 기각할 확률이다.
- 따라서 귀무가설을 잘못 기각하지 못할 확률(false failure to reject the null hypothesis)은 $1-\text{power}$이다.

#### Note 4
- 또 다른 중요한 혼동 지점: 우리는 p-value를 사용하지만, 개념적으로 p-value는 단지 계산상의 편의(computational trick)에 불과하다.
- 검정통계량(test statistic)을 선택한 뒤의 개념적 순서는 다음과 같다.
- 먼저 유의수준(significance level)을 선택한다.
- 그다음 이를 사용하여 기각역(rejection region)을 정의한다.
- 검정통계량이 기각역에 있으면 귀무가설(null hypothesis)을 기각한다.
- p-value의 역할은 단지 하나의 계산으로 검정통계량이 기각역 안에 있는지 여부를 알려주는 것뿐이다.

#### Errors
- 이 두 가지 오류와 그 확률은 다음과 같이 요약할 수 있다. 

$$
\begin{align}
\text{Type I error}&=\text{$H_0$가 참일 때 $H_0$를 기각하는 것}\\ 
\text{Type II error}&=\text{$H_A$가 참일 때 $H_0$를 기각하지 못하는 것}\\  
P(\text{type I error})&=P(\text{$H_0$를 잘못 기각})\\  
&=P(\text{검정통계량이 기각역에 있음}\mid H_0)\\  
&=\text{significance level of the test\, (검정의 유의수준)}  \\  
P(\text{type II error})&=P(\text{$H_0$를 잘못 기각하지 않음})\\  
&=P(\text{검정통계량이 수락역에 있음}\mid H_A)\\
&=1-\text{power} 
\end{align}
$$  


#### helpful analogies(유용한 비유)    
- 질병에 대한 의학적 검사로 말하면, 제1종 오류(type I error)는 거짓 양성(false positive)이고 제2종 오류(type II error)는 거짓 음성(false negative)이다.    
- 배심 재판에서 제1종 오류는 무고한 피고인에게 유죄를 선고하는 것이고, 제2종 오류는 유죄인 피고인에게 무죄를 선고하는 것이다.

### Review: Power
- 검정력(power)은 귀무가설(null hypothesis)을 올바르게 기각할 확률이다.
- 이는 고려하고 있는 대립가설(alternative hypothesis) $H_A$에 의존한다.
- 이상적인 검정은 검정력이 $1.0$이고 유의수준(significance)이 $0.0$인 경우이다.
- 물론 일반적으로 이는 불가능하다.
- 따라서 우리는 검정력은 높고 유의수준은 낮은 어떤 절충(compromise)을 찾고자 한다.
- 기호로 쓰면 다음과 같다.  

$$  
\text{power}=P(\text{데이터가 기각역에 있음}\mid H_A)  
$$
- 이를 다음과 비교하라.  

$$  
\text{significance}=P(\text{데이터가 기각역에 있음}\mid H_0)  
$$

### Understanding a significance test
- 질문해야 할 사항들
- 1. 데이터를 어떻게 수집했는가? 실험 설계(experimental setup)는 무엇인가?
- 2. 귀무가설(null hypothesis)과 대립가설(alternative hypothesis)은 무엇인가?
- 3. 어떤 종류의 유의성 검정(significance test)이 사용되었는가?
	- 데이터가 이러한 종류의 검정을 사용하기 위한 조건(criteria)에 부합하는가?
	- 검정은 이러한 조건에서 벗어나는 경우에 대해 얼마나 강건한가(robust)?
- 4. 예를 들어, 두 집단의 데이터를 비교하는 일부 검정은 두 집단이 동일한 분산(variance)을 가진 분포로부터 추출되었다고 가정한다.
	- 따라서 검정을 적용하기 전에 이를 확인해야 한다.
	- 이러한 확인은 종종 두 집단 데이터의 분산을 비교하도록 설계된 또 다른 유의성 검정을 사용하여 수행된다.

- 5. p-value는 어떻게 계산되는가?
	- 유의성 검정(significance test)은 검정통계량(test statistic)과 귀무분포(null distribution)를 함께 가진다.
	- 대부분의 검정에서 p-value는 다음과 같다. 

$$  
p=P(\text{우리가 얻은 것만큼 극단적인 데이터}\mid H_0)  
$$
	- “우리가 관측한 데이터만큼 극단적인 데이터(data at least as extreme as the data we saw)”란 무엇을 의미하는가?
		- 간단한 실험에서는 극단적인 데이터의 레벨을 정하기 쉽지만 실험이 복잡해지면 이것을 정하는게 쉽지 않음.
	- 예를 들어, 검정은 단측(one-sided)인가 양측(two-sided)인가?
- 6. 이 검정의 유의수준(significance level) $\alpha$는 무엇인가?
	- 만약 $p<\alpha$이면 실험자는 $H_A$를 지지하며 $H_0$를 기각한다.
- 7. 검정의 검정력(power)은 얼마인가?

### t tests
- 많은 유의성 검정(significance test)은 데이터가 정규분포(normal distribution)로부터 추출되었다고 가정하므로, 그러한 검정을 사용하기 전에 정규성 가정(normality assumption)이 합리적인지 확인하기 위해 데이터를 살펴보아야 한다.    
- z-test와 마찬가지로, 아래에서 다룰 one-sample 및 two-sample t-test도 이러한 정규성 가정에서 출발한다.    
- 앞으로 나오는 검정들의 모든 계산 세부사항을 암기할 필요는 없다.    
- 실제 생활에서는 교과서, Google, Wikipedia를 사용할 수 있다.    
- 대신 t-test가 언제 적절한지 식별하고, 세부사항을 찾아본 뒤 이 검정을 적용할 수 있어야 한다.


### z-test
- 먼저 z-test를 복습하자.
- 데이터: $x_1,x_2,\ldots,x_n \sim N(\mu,\sigma^2)$라고 가정하며, 여기서 $\mu$는 미지이고 $\sigma$는 알려져 있다.
- 귀무가설(null hypothesis): 어떤 특정 값 $\mu_0$에 대해 $\mu=\mu_0$
	- IQ 테스트에서 $\mu_0$는 100 이었음.
- 검정통계량(test statistic):  

$$  
z=\frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}  
$$

- 이는 표준화된 평균(standardized mean)이다.
- 귀무분포(null distribution): $$\phi(z \mid H_0)$$는 $Z\sim N(0,1)$의 확률밀도함수(pdf)이다.
- 단측 p-value(오른쪽):  

$$  
p=P(Z\geq z\mid H_0)  
$$

- 단측 p-value(왼쪽):  

$$  
p=P(Z\leq z\mid H_0)  
$$

- 양측 p-value:  

$$  
p=  
\begin{cases}  
2P(Z\geq z), & z>0\\  
2P(Z\leq z), & z<0  
\end{cases}  
$$
- 분포가 $0$을 중심으로 대칭이므로 이를 다음과 같이 쓸 수도 있다.  

$$  
p=P(|Z|\geq |z|)  
$$


#### Example 1
- 평균 $\mu$는 미지이고 분산 $4$는 알려진 정규분포를 따르는 데이터가 있다고 하자.
- 귀무가설 $H_0$는 $\mu=2$이다.
- 대립가설 $H_A$는 $\mu>2$이다.
- 다음 데이터를 수집했다고 하자.  

$$  
3,2,5,7,1  
$$
- 유의수준 $\alpha=0.05$에서 귀무가설을 기각해야 하는가?

- 데이터는 $5$개이며 평균은  $\bar{x}=3.6$ 이다.
- 데이터가 정규분포(normal distribution)를 따르고 분산이 알려져 있으므로 z-test를 사용해야 한다.
- z-통계량(z statistic)은 다음과 같다.  

$$  
z=\frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}  
=\frac{3.6-2}{2/\sqrt{5}}  
=1.79  
$$

- 대립가설(alternative hypothesis)이 단측(one-sided)이므로 검정 역시 단측 검정이다.
- 따라서 (Python을 사용하면) p-value는 다음과 같다.  

$$  
\begin{align}
p&=P(Z>z)=P(Z>1.79) \\  
&=1-\texttt{scipy.stats.norm.cdf}(1.79,0,1)  \\
&=0.037  
\end{align}
$$
- $p<\alpha=0.05$이므로 $\mu>2$라는 대립가설을 지지하며 귀무가설(null hypothesis)을 기각한다.



- 우리는 이 검정을 다음과 같이 시각화할 수 있다.
- 귀무분포(null distribution)는$\phi(z \mid H_0)\sim N(0,1)$ 이다.
- 기각역(rejection region)은 오른쪽 꼬리(right tail)에 위치하며,  $q_{0.95}=z_{0.05}=1.64$ 에서 시작한다.
- 주황색 음영 영역은 유의수준(significance level)  $\alpha=0.05$ 를 나타낸다.
- 검정통계량(test statistic)은  $z=1.79$ 이며 그림의 검은 점으로 표시된다.
- 파란 줄무늬 영역은 p-value를 나타내며,  $p=0.037$이다.
- $z=1.79$가 기각역 안에 있으므로,  $p<\alpha$이고 따라서 귀무가설 $H_0$를 기각한다.


#### Example 2
- 예제 1을 양측(two-sided) 검정, 즉 $H_A$가 $\mu \neq 2$인 경우로 다시 수행하라.
#### Solution  3
- 먼저 검정을 수행한 뒤 p-value 계산의 근거를 설명하겠다.
- $z>0$이므로  $p=2P(Z>z)=0.074$ 이다.
- $p>\alpha=0.05$이므로 데이터는 $H_A$를 지지하며 귀무가설(null hypothesis)을 기각할 충분한 근거를 제공하지 않는다.

- p 계산에서 $2$가 곱해지는 이유
- 그 이유는 본질적으로 산술적(arithmetic)이다.
- p-value의 목적은  $p \leq \alpha$가 검정통계량(test statistic)이 기각역(rejection region)에 있음을 나타내는 데 있다는 점을 기억하자.
- 아래 그림은 다음 내용을 보여준다.
	- 양측(two-sided) 검정에서는 기각역의 각 측면이  $\alpha/2$의 확률을 가진다.
	- 따라서 검정통계량이 오른쪽에 있다면,  $P(Z>z)\leq \alpha/2$일 때 기각역에 있게 된다.
	- 즉,  $p=2P(Z>z)\leq \alpha$일 때 기각역에 있다는 의미이다.
- 그림에서:
	- 왼쪽 기각역(left rejection region)은  $q_{0.025}=z_{0.975}=-1.96$ 에서 시작한다.
	- 오른쪽 기각역(right rejection region)은 $q_{0.975}=z_{0.025}=1.96$  에서 시작한다.
	- 각 꼬리의 면적은  $\alpha/2=0.025$이다.
	- 검정통계량은  $z=1.79$ 이다.
	- 각 꼬리의 파란 줄무늬 영역은  $p/2=0.037$ 이다.
	- 따라서 전체 p-value는  $p=0.074$ 가 된다.



### The Student t distribution
- ‘Student’는 이 검정과 분포를 처음 설명한 William Gosset이 사용한 필명이다.
- 참고: [https://en.wikipedia.org/wiki/Student’s_t-test](https://en.wikipedia.org/wiki/Student%E2%80%99s_t-test)
- t-분포(t-distribution)는 정규분포(normal distribution)처럼 대칭적이고 종 모양이다.
- t-분포는 자유도(degrees of freedom)를 의미하는 parameter $df$를 가진다.
- $df$가 작을 때 t-분포는 표준정규분포(standard normal distribution)보다 **꼬리에 더 많은 확률**을 가진다.
- $df$가 **증가할수록 $t(df)$는 표준정규분포와 점점 더 비슷**해진다.
- 다음은 $t(df)$를 보여주고 표준정규분포와 비교하는 간단한 애플릿이다: [https://mathlets.org/mathlets/t-distribution/](https://mathlets.org/mathlets/t-distribution/)

- 노말 디스트리부션과 비슷하게 좌우대칭이고 종 모양
- 노말 디스트리부션과 다르게 파라미터 df가 있음

- 그림 1: 자유도(degrees of freedom)가 증가할수록 t-분포(t-distribution)는 정규분포(normal distribution)에 가까워진다.
- 자유도 df가 50정도 되면 거의 정규분포와 비슷해짐.

### One sample t-test
- **z-test에서는 데이터의 기저 분포(underlying distribution)의 분산(variance)이 알려져 있다고 가정했다.**    
- 그러나 실제로는 $\sigma$를 알지 못하는 경우가 많으며, 따라서 데이터를 사용하여 이를 추정해야 한다.    
- 이러한 경우($\sigma$를 알지 못하는 경우)에는 z-test 대신 일표본 t-test(one sample t-test)를 사용하며, 표준화된 평균(standardized mean) 대신 **studentized mean을 사용**한다.

- Student t distribution가 사용되는게 t 테스트
- underlying distribution
	- 통계에서 보통 **“자료가 실제로 따라간다고 가정하는 근본 분포”** 또는 **“데이터 뒤에 깔려 있는 모집단 분포”** 라는 뜻
	- 통계에서는 이 데이터들이 그냥 아무렇게나 나온 것이 아니라, 어떤 보이지 않는 확률분포에서 나온 것이라고 가정
		- 예를 들어:$X \sim N(7.0, 0.1^2)$이라고 하면, 이 말은:
			- pH 측정값 XXX는 평균 7.0, 표준편차 0.1인 정규분포에서 나온다고 본다는 뜻.
			- 이때 N(7.0,0.12)N(7.0, 0.1^2)N(7.0,0.12)가 바로 **underlying distribution**입니다.

- 데이터: $x_1,x_2,\ldots,x_n \sim N(\mu,\sigma^2)$라고 가정하며, 여기서 $\mu$와 $\sigma$는 모두 미지이다.
- 귀무가설(null hypothesis): 어떤 특정 값 $\mu_0$에 대해  $\mu=\mu_0$
- 검정통계량(test statistic):  

$$  
t=\frac{\bar{x}-\mu_0}{s/\sqrt{n}}  
$$  
- **시그마가 아니라 s로 나눠주는게 차이.→헷갈리면 안됨.**
	- $\sigma$: 모집단 표준편차 
	- $s$: 표본 표준편차 


$$  
s^2=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2  
$$  
- **분산이랑 비슷한데 기대값 대신 $\bar x$, $1/n$ 대신 $1/(n-1)$** 

- 여기서 $t$는 Studentized mean이라고 부르며, $s^2$는 표본분산(sample variance)이라고 부른다.
- $s^2$는 실제 분산 $\sigma^2$의 추정값(estimator)이다.
- 귀무분포(null distribution): $\phi(t \mid H_0)$는 자유도(degrees of freedom)가 $n-1$인 t-분포  $T\sim t(n-1)$ 의 확률밀도함수(pdf)이다.

- 실제평균이 아닌 샘플 평균을 사용할 경우는 1/n이 아니고 1/n-1 써야 함.
- 왜냐면 x bar를 추정하는데 $x_i$를 사용하기 때문에 1개를 빼야 함.
- 주사위를 예를 들면 샘플을 적게 뽑을 수록 이론적 기대값보다 샘플의 값에 가까워지게 됨
	- 1,2 가 나오면 평균은 1.5 임 기대값 3.5와 차이가 있음

- 단측 p-value(오른쪽): $p=P(T\geq t\mid H_0)$
- 단측 p-value(왼쪽):  $p=P(T\leq t\mid H_0)$
- 양측 p-value:  

$$
p=  
\begin{cases}  
2P(T\geq t), & t>0\\  
2P(T\leq t), & t<0  
\end{cases} 
$$

- 분포가 $0$을 중심으로 대칭이므로 이를 다음과 같이 쓸 수도 있다.  

$$  
p=P(|T|\geq |t|)  
$$

#### Note
- 검정통계량(test statistic)의 분포를 알게 되면, 모든 검정은 동일한 기본 형태를 가진다.
- 이 경우 우리는 “정규분포 데이터를 사용하면 Studentized mean이 t-분포를 따른다”는 정리를 사용한다.
- 원한다면 증명을 찾아볼 수 있다:  [https://en.wikipedia.org/wiki/Student%E2%80%99s_t-distribution#Derivation](https://en.wikipedia.org/wiki/Student%E2%80%99s_t-distribution#Derivation)

#### Example 4
- 이제 예제 1에서 분산이 미지라고 가정하자.
- 즉, 평균 $\mu$와 분산 $\sigma^2$가 모두 미지인 정규분포를 따르는 데이터가 있다.
- 이전과 같은 데이터를 수집했다고 하자.  

$$  
1,2,3,6,-1  
$$

- 위와 같이 귀무가설 $H_0$는 $\mu=0$이고, 대립가설 $H_A$는 $\mu>0$이다.
- 유의수준 $\alpha=0.05$에서 귀무가설을 기각해야 하는가?

#### Solution 5
- 데이터는 $5$개이며 평균은  $\bar{x}=2.2$이다.
- 데이터가 평균과 분산이 모두 미지인 정규분포(normal distribution)를 따른다고 가정하므로, 일표본 t-test(one-sample t-test)를 사용해야 한다.
- 표본분산(sample variance)을 계산하면 다음과 같다.  

$$  
\begin{align}
s^2&=\frac{1}{4}\left((1-2.2)^2+(2-2.2)^2+(3-2.2)^2+(6-2.2)^2+(-1-2.2)^2\right)\\
&=6.7
\end{align}
$$ 
- t-통계량(t-statistic)은 Studentized mean이다.  

$$  
t=\frac{\bar{x}-\mu_0}{s/\sqrt{n}}   
=\frac{2.2-0}{\sqrt{6.7}/\sqrt{5}}   
=1.901  
$$

- 검정은 대립가설(alternative hypothesis)이 단측(one-sided)이므로 단측 검정이다.
- 따라서 (Python을 사용하면) p-value는 다음과 같다.  

$$
\begin{align}
p&=P(T>t)=P(T>1.901)  \\  
&=1-\texttt{scipy.stats.t.cdf}(1.901,4)   
=0.065  
\end{align}
$$
- $p>0.05$이므로 귀무가설(null hypothesis)을 기각하지 않는다.
- 이 검정은 다음과 같이 시각화할 수 있다.
- 귀무분포(null distribution)는  $\phi(t\mid H_0)\sim t(4)$이다.
- 기각역(rejection region)은 오른쪽 꼬리(right tail)에 있으며 $t_{0.05}=2.13$에서 시작한다.
- 주황색 음영 영역은 유의수준(significance level)  $\alpha=0.05$를 나타낸다.
- 검정통계량은  $t=1.90$이다.
- 파란 줄무늬 영역은 p-value $p=0.065$를 나타낸다.
- $t=1.90$은 기각역에 속하지 않으므로 $H_0$를 기각하지 않는다.

- 다음으로 두 표본의 평균을 비교하는 경우를 고려한다.
	- 예를 들어, 두 가지 의학적 치료의 평균 효과(mean efficacy)를 비교하는 데 관심이 있을 수 있다.
- 데이터: 정규분포에서 추출된 두 데이터 집합이 있다고 가정한다. 

$$  
x_1,x_2,\ldots,x_n\sim N(\mu_1,\sigma^2)  
$$ 

$$  
y_1,y_2,\ldots,y_m\sim N(\mu_2,\sigma^2)  
$$

- 여기서 평균 $\mu_1$, $\mu_2$와 분산 $\sigma^2$는 모두 미지이다.
	- 분산 $\sigma^2$는 미지지만 같음.
- 두 분포가 동일한 분산을 가진다고 가정한다는 점에 주의하라.
- 또한 첫 번째 집단에는 $n$개의 표본이 있고 두 번째 집단에는 $m$개의 표본이 있다는 점에도 주의하라.
- 귀무가설(null hypothesis):  

$$  
\mu_1=\mu_2  
$$

- 이때 $\mu_1$과 $\mu_2$의 값은 지정되지 않는다. (무슨 값인지 모른다.)

- 검정통계량(test statistic):  
	- 두 표본평균의 차이가, 귀무가설에서 기대하는 차이 0으로부터 표준오차 몇 개만큼 떨어져 있는가

$$  
t=\frac{\bar{x}-\bar{y}}{s_p}  
$$
- $\bar x$ 에서 평균을 빼는게 아니라 y 값이랑 비교해야 하기 때문에 분모에서 $\bar y$를 빼줌
- 여기서 $s_p^2$는 합동분산(pooled variance)이며 다음과 같다.  

$$  
s_p^2=\frac{(n-1)s_x^2+(m-1)s_y^2}{n+m-2}\left(\frac{1}{n}+\frac{1}{m}\right)  
$$

- 여기서 $s_x^2$와 $s_y^2$는 각각 $x_i$와 $y_j$의 표본분산(sample variance)이다.
- $t$의 식은 다소 복잡하지만, 기본 아이디어는 동일하며 여전히 알려진 귀무분포(null distribution)를 갖는다.
- 귀무분포:  $\phi(t\mid H_0)$는 다음 분포의 확률밀도함수(pdf)이다.  
$$T\sim t(n+m-2)$$
- 단측 p-value(오른쪽):  $p=P(T>t\mid H_0)$
- 단측 p-value(왼쪽): $p=P(T<t\mid H_0)$
- 양측 p-value: $p=P(|T|>|t|)$


- 합동분산(pooled variance) 대강 평균을 구해서 더하하고 샘플수로 나눈다고 생각하고 수식을 보면 이해가 쉬움.

#### Note 1
- 일부 저자들은 다른 표기법을 사용한다.
- 그들은 합동분산(pooled variance)을 다음과 같이 정의한다.  
	- 아래 수식이 더 엄밀한 정의에 가까움.
$$  
s_{p-\text{other authors}}^2=\frac{(n-1)s_x^2+(m-1)s_y^2}{n+m-2}  
$$

- 그리고 우리가 합동분산이라고 부른 것은 $\bar{x}-\bar{y}$의 추정분산(estimated variance)이라고 지적한다.
- 즉,  

$$  
s_p^2=s_{p-\text{other authors}}^2\left(\frac{1}{n}+\frac{1}{m}\right)\approx s_{\bar{x}-\bar{y}}^2  
$$

#### Note 2
- 두 집단이 서로 다른 분산(variance)을 가질 수 있도록 허용하는 이표본 t-test(two-sample t-test)의 한 버전이 있다.
- 이 경우 검정통계량(test statistic)은 조금 더 복잡하지만, 컴퓨터는 이를 똑같이 쉽게 처리할 수 있다.
#### Note 3
- 위의 참고사항을 다시 강조한다.
- 데이터에 대한 가정, 즉 독립표본(independent samples), 정규 데이터(normal data), 동일분산(equal variances) 아래에서 귀무분포(null distribution)가 t-분포(t-distribution)임을 증명할 수 있다.
- 이를 알고 있으면, 다른 유의성 검정(significance test)을 이해하는 것과 정확히 같은 방식으로 이표본 t-test(two-sample t-test)의 핵심을 다루고 이해할 수 있다.

#### Example 6
- 다음 데이터는 $1408$명의 여성이 산부인과 병원에 입원한 실제 연구에서 나온 것이다.
- 입원 사유는 (i) 의학적 이유(medical reasons) 또는 (ii) 예약되지 않은 응급 입원(unbooked emergency admission)이었다.
- 임신 기간(duration of pregnancy)은 마지막 월경 시작일부터 완료된 주(complete weeks) 단위로 측정된다.
- 데이터는 다음과 같이 요약할 수 있다.
- Medical:  

$$  
775\text{ observations with }\overline{x_M}=39.08\text{ and }s_M^2=7.77  
$$
- Emergency:  

$$  
633\text{ observations with }\overline{x_E}=39.60\text{ and }s_E^2=4.95  
$$

- 두 집단의 평균 임신 기간이 다른지 조사하기 위해 이표본 t-test(two-sample t-test)를 설정하고 수행하라.
- 어떤 가정을 했는가?

#### Solution 7
- 이 데이터에 대한 합동분산(pooled variance)은 다음과 같다.  

$$  
s_p^2=\frac{774(7.77)+632(4.95)}{1406}\left(\frac{1}{775}+\frac{1}{633}\right)=0.0187  
$$

- 귀무분포(null distribution)에 대한 t-통계량은 다음과 같다.  

$$  
\frac{\bar{x}_M-\bar{y}_E}{s_p}=-3.8064  
$$

- 자유도(degrees of freedom)는 $1406$이다.
- Python을 사용하여 양측 p-value를 계산하면 다음과 같다.  

$$  
\begin{align}
p&=P(|T|>|t|)=2\cdot\texttt{scipy.stats.t.cdf}(-3.8064,1406)\\  
&=0.00015  
\end{align}
$$

#### Solution 8
- $p$는 매우 작으며, $\alpha=0.05$나 $\alpha=0.01$보다 훨씬 작다.
- 따라서 평균 임신 기간에 차이가 있다는 대립가설(alternative hypothesis)을 지지하며 귀무가설(null hypothesis)을 기각한다.
- 양측 p-value를 t-분포를 사용하여 정확히 계산하는 대신, 자유도가 $1406$이면 t-분포가 사실상 표준정규분포(standard normal distribution)와 거의 같다는 점을 이용할 수도 있다.
- 또한 $3.8064$는 거의 $4$ 표준편차에 해당한다.  

$$  
P(|t|\geq3.8064)\approx P(|z|\geq3.8064)<0.001  
$$
- 우리는 데이터가 정규분포(normal)이고 두 집단이 동일한 분산(equal variances)을 가진다고 가정했다.
- 표본분산(sample variance) 사이에 큰 차이가 있다는 점을 고려하면, 이 가정은 정당화되기 어려울 수 있다.
## Comment

—
6/4일 강의 있음
take home exame: 6/4~11 까지 
	배웠던 예시 문제의 심화버전으로 10~15개 정도 예
마지막주 휴강
—
## Conclusion



