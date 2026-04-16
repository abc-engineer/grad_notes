2026-04-02 08:20
## 10강 Expectation, Variance and Standard Deviation for Continuous Random Variables
- Continuous Random Variables의 기대값 분산, 표준편차를 구하는 방법 

### Learning Goals
- 연속 확률변수에 대해 기댓값(expectation), 분산(variance), 표준편차(standard deviation)를 계산하고 해석할 수 있어야 한다.    
- 이산 및 연속 확률변수에 대해 분위수(quantile)를 계산하고 해석할 수 있어야 한다.

### Introduction
- 지금까지 우리는 이산 확률변수에 대한 기댓값, 표준편차, 분산을 살펴보았다.    
- 이러한 요약 통계량은 연속 확률변수에서도 동일한 의미를 가진다.    
	- 기댓값 $\mu=E[X]$ 는 위치(location) 또는 중심 경향(central tendency)을 나타내는 척도이다.  
	- 표준편차 $\sigma$ 는 퍼짐(spread) 또는 규모(scale)를 나타내는 척도이다.    
	- 분산 $\sigma^2=\mathrm{Var}(X)$ 는 표준편차의 제곱이다.    
- 이산에서 연속으로 넘어갈 때는 공식에서 합(sum)을 적분(integral)으로 바꾸면 된다.    
- 다음 절에서는 또 다른 요약 통계량인 분위수(quantile)를 소개한다.    
	- 예를 들어 $0.5$ 분위수는 중앙값(median), 즉 50번째 백분위수(percentile)로 알려져 있다.
- 기대값, 분산, 표준편차등은 통계를 요약하는 대표적인 값들
- continuous random variables도 같음.
- discrete 을 continuous에 적용하려면 적분만 하면 됨.
- 다른 개념으로 quantiles이 등장 할 예정정

### Expected value of a continuous random variable
#### Definition (Expected value_기댓값)
- $X$가 구간 $[a,b]$에서 정의된 연속 확률변수이고 확률밀도함수가 $f(x)$라고 하자.
- 이때 $X$의 기댓값은 다음과 같이 정의된다:  

$$  
E[X]=\int_a^b x f(x)dx  
$$

#### Remark
- 이산 확률변수의 공식과 비교하면 다음과 같다:  

$$  
E[X]=\sum_{i=1}^n x_i p(x_i)  
$$
- X be a continuous random variable with range \[a, b]이고 pdf f(x)면 적분하면 됨.
- 그냥 sum을 하는것인데 적분기호로 바뀌었다고 생각해도 됨.

- 다음 두 식은 서로 대응된다:  

$$  
E[X]=\int_a^b x f(x)dx \quad \Longleftrightarrow \quad E[X]=\sum_{i=1}^n x_i p(x_i)  
$$
- 이산형 공식은 $X$의 값 $x_i$들을 확률 $p(x_i)$를 가중치로 하여 가중합(weighted sum)을 취하는 것이다.
- $f(x)$는 확률밀도(probability density)임을 기억하자.
	- 그 단위는 $\text{prob}/(\text{X의 단위})$ 이다.
	- 따라서 $f(x)dx$ 는 $x$ 주변의 아주 작은 구간(폭 $dx$)에서 $X$가 가질 확률을 의미한다.
- 그러므로 $E[X]$ 공식은 $X$의 값 $x$들을 확률 $f(x)dx$를 가중치로 하는 가중적분(weighted integral)으로 해석할 수 있다.
- 이전과 마찬가지로 기댓값은 평균(mean) 또는 average라고도 불린다.

- sum에 dx가 없는건 적분하면 생기는 dx를 없애기 위함.
- dx는 x 주변 아주 작은 범위
- $p (x_i )=f (x)dx$ 임
- 기대값은 동일하게 평균이나 중간값을 의미미

#### Example: 
- $X \sim \mathrm{uniform}(0,1)$ 일 때 $E[X]$ 를 구하라.
#### Solution
- $X$의 범위는 $[0,1]$ 이고 pdf는 $f(x)=1$ 이다.
- 따라서  

$$  
E[X]=\int_0^1 xdx=\left[\frac{x^2}{2}\right]_0^1=\frac{1}{2}  
$$

- 예상대로 평균은 구간의 중간값에 위치한다.

#### Example: 
- $X$의 범위가 $[0,2]$이고 pdf가 $f(x)=\dfrac{3}{8}x^2$ 일 때 $E[X]$ 를 구하라.
#### Solution
- 기댓값은 다음과 같이 계산한다:  

$$  
E[X]=\int_0^2 x f(x)dx=\int_0^2 \frac{3}{8} x^3 dx=\left[\frac{3x^4}{32}\right]_0^2=\frac{3}{2}  
$$

#### Integration by parts
- 부분적분 (Integration by parts)
- 정리 (부분적분 공식)

$$  
\int_a^b u(x)v'(x)dx=[u(x)v(x)]_a^b-\int_a^b u'(x)v(x)dx  
$$
##### Proof
- 곱의 미분법은 다음과 같다:  

$$  
(u(x)v(x))'=v(x)u'(x)+u(x)v'(x)  
$$
- 양변을 $x$에 대해 적분하면  

$$  
\int (u(x)v(x))'dx=\int u'(x)v(x)dx+\int u(x)v'(x)dx  
$$

- 부정적분은 원시함수이므로  

$$  
u(x)v(x)=\int u'(x)v(x)dx+\int u(x)v'(x)dx  
$$

#### Example
- $X \sim \mathrm{exp}(\lambda)$ 일 때 $E[X]$ 를 구하라.
#### Solution
- $X$의 범위는 $[0,\infty)$ 이고 pdf는 $f(x)=\lambda e^{-\lambda x}$ 이다.
- 따라서  

$$  
E[X]=\int_0^\infty x f(x)dx=\int_0^\infty \lambda x e^{-\lambda x}dx  
$$
- 부분적분을 사용한다: $u=x$, $v'=\lambda e^{-\lambda x} \Rightarrow u'=1$, $v=-e^{-\lambda x}$  

$$  
=\left[-x e^{-\lambda x}\right]_0^\infty+\int_0^\infty e^{-\lambda x}dx  
$$
- 이제 각 항을 계산하면  

$$  
=0-\left[\frac{-e^{-\lambda x}}{\lambda}\right]_0^\infty=\frac{1}{\lambda}  
$$
- 여기서 $x e^{-\lambda x}$ 와 $e^{-\lambda x}$ 는 $x \to \infty$ 일 때 $0$으로 수렴함을 사용하였다.
- exp(λ)구할때 부분 적분 필요


#### Example
- $X \sim \mathrm{exp}(\lambda)$ 일 때 $E[X]$ 를 구하라.
#### Solution
- $X$의 범위는 $[0,\infty)$ 이고 pdf는 다음과 같다:  

$$  
f(x)=\lambda e^{-\lambda x}  
$$

- geometric distributyion과 유사함.

#### Example
- $Z \sim N(0,1)$ 일 때 $E[Z]$ 를 구하라.
#### Solution
- $Z$의 범위는 $(-\infty,\infty)$ 이고 pdf는  

$$  
\phi(z)=\frac{1}{\sqrt{2\pi}}e^{-z^2/2}  
$$
- 대칭성에 의해 평균은 반드시 $0$이다.
- 수학적으로 까다로운 유일한 부분은 이 적분이 수렴하는지, 즉 평균이 실제로 존재하는지를 확인하는 것이다. 어떤 확률변수는 평균이 존재하지 않지만, 여기서는 그런 경우를 자주 다루지 않는다.
- random variable 중 일부는 평균이 없는 경우도 있음.

#### Example
- $Z \sim N(0,1)$ 일 때 $E[Z]$ 를 구하라.
#### Solution
- 먼저 $0$부터 $\infty$까지의 적분을 계산한다:  

$$  
\int_0^\infty z\phi(z)dz=\frac{1}{\sqrt{2\pi}}\int_0^\infty z e^{-z^2/2}dz  
$$
- 치환 $u=\frac{z^2}{2}$ 를 사용하면 $du=zdz$ 이다.  

$$  
=\frac{1}{\sqrt{2\pi}}\int_0^\infty e^{-u}du=\frac{1}{\sqrt{2\pi}}\left[-e^{-u}\right]_0^\infty=\frac{1}{\sqrt{2\pi}}  
$$
- 마찬가지로  

$$  
\int_{-\infty}^0 z\phi(z)dz=-\frac{1}{\sqrt{2\pi}}  
$$
- 두 값을 더하면  

$$  
E[Z]=0  
$$
- 표준 정규분포는 0~무한대로 가면 1, 0~-무한대로 가면 -1 그래서 기대값 E\[Z]=0

#### Example
- $Z \sim N(0,1)$ 일 때 $E[Z]$ 를 구하라.
#### Solution
- $Z$의 범위는 $(-\infty,\infty)$ 이고 pdf는 다음과 같다: 

$$  
\phi(z)=\frac{1}{\sqrt{2\pi}} e^{-z^2/2}  
$$

### Properties of $E [X ]$
- discrete와 동일한 특성임.
- 연속 확률변수에 대한 $E[X]$의 성질은 이산 확률변수의 경우와 동일하다.
#### linearity Proerty I
- 1. $X, Y$가 표본공간 $\Omega$ 위의 확률변수이면  

$$  
E[X+Y]=E[X]+E[Y]  
$$
#### linearity Proerty II
- 2. $a, b$가 상수이면  

$$  
E[aX+b]=aE[X]+b  
$$

#### Example
- $X \sim N(\mu,\sigma^2)$ 일 때 $E[X]=\mu$ 임을 보여라.
#### Solution
- 이전 예제에서 표준정규변수 $Z$에 대해 $E[Z]=0$ 임을 보였다.
- 같은 계산을 반복하여 직접 증명할 수도 있지만, 여기서는 기댓값의 선형성을 이용한다.
- 정규분포의 표준화에 의해  

$$  
Z=\frac{X-\mu}{\sigma} \sim N(0,1)  
$$
- 이를 $X$에 대해 정리하면  

$$  
X=\sigma Z+\mu  
$$
- 이제 기댓값의 선형성을 적용하면  

$$  
E[X]=E[\sigma Z+\mu]=\sigma E[Z]+\mu=\mu  
$$
- 이는 이산 경우와 정확히 동일하게 작동한다.

#### 확률변수의 함수의 기댓값
- $h(x)$가 함수이면 $Y=h(X)$ 는 확률변수가 된다.
- 이때 기댓값은 다음과 같이 주어진다:  

$$  
E[Y]=E[h(X)]=\int_{-\infty}^{\infty} h(x) f_X(x)dx  
$$

#### Example
- $X \sim \mathrm{exp}(\lambda)$ 일 때 $E[X^2]$ 를 구하라.
#### Solution
- 기댓값은 다음과 같다:  

$$  
E[X^2]=\int_0^\infty x^2 f(x)dx=\int_0^\infty \lambda x^2 e^{-\lambda x}dx  
$$
- 부분적분을 사용한다: $u=x^2$, $v'=\lambda e^{-\lambda x} \Rightarrow u'=2x$, $v=-e^{-\lambda x}$  

$$  
=\left[-x^2 e^{-\lambda x}\right]_0^\infty+\int_0^\infty 2x e^{-\lambda x}dx  
$$
- 앞 단계에서  

$$  
E[X^2]=\left[-x^2 e^{-\lambda x}\right]_0^\infty+\int_0^\infty 2x e^{-\lambda x}dx  
$$
- 첫 번째 항은 $0$이 된다.
- 두 번째 적분에 대해 다시 부분적분을 사용한다: $u=2x$, $v'=e^{-\lambda x} \Rightarrow u'=2$, $v=-\dfrac{e^{-\lambda x}}{\lambda}$  

$$  
\int_0^\infty 2x e^{-\lambda x}dx=\left[-\frac{2x e^{-\lambda x}}{\lambda}\right]_0^\infty+\int_0^\infty \frac{2}{\lambda} e^{-\lambda x}dx  
$$  

$$  
=0+\frac{2}{\lambda}\int_0^\infty e^{-\lambda x}dx=\frac{2}{\lambda}\left[\frac{-e^{-\lambda x}}{\lambda}\right]_0^\infty=\frac{2}{\lambda^2}  
$$
- 따라서  

$$  
E[X^2]=\frac{2}{\lambda^2}  
$$

### Variance
- 연속 확률변수에 대해 기댓값을 정의했으므로, 분산의 정의는 이산 경우와 동일하다.
#### Definition

- $X$가 평균 $\mu$를 갖는 연속 확률변수라고 하자.
- 이때 분산은 다음과 같이 정의된다:  

$$  
\mathrm{Var}(X)=E[(X-\mu)^2]  
$$

### Properties of Variance
- 이는 이산 경우와 정확히 동일하다.
- 1. $X$와 $Y$가 독립이면  

$$  
\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)  
$$

- 2. 상수 $a,b$에 대해  

$$  
\mathrm{Var}(aX+b)=a^2 \mathrm{Var}(X)  
$$

- 3. Theorem(정리):  

$$  
\mathrm{Var}(X)=E[X^2]-E[X]^2=E[X^2]-\mu^2  
$$

#### Remark
- 성질 1에서는 $X$와 $Y$가 독립이라는 조건이 중요하다.
- 성질 3은 손계산에서 분산을 구할 때 더 쉽게 사용할 수 있는 공식이다.
- 성질 2와 3의 증명은 이산 경우와 본질적으로 동일하므로 여기서는 생략한다.



#### Example
- $X \sim \mathrm{uniform}(0,1)$ 일 때 $\mathrm{Var}(X)$ 와 $\sigma_X$ 를 구하라.
#### Solution
- 이전 예제에서 $\mu=\dfrac{1}{2}$ 임을 구했다.
- 이제 분산을 계산하면  

$$  
\mathrm{Var}(X)=E[(X-\mu)^2]=\int_0^1 \left(x-\frac{1}{2}\right)^2 \, dx=\frac{1}{12}  
$$
- 따라서 표준편차는  

$$  
\sigma_X=\sqrt{\mathrm{Var}(X)}=\sqrt{\frac{1}{12}}=\frac{1}{\sqrt{12}}  
$$


#### Example
- $X \sim \mathrm{exp}(\lambda)$ 일 때 $\mathrm{Var}(X)$ 와 $\sigma_X$ 를 구하라.
#### Solution
- 이전 계산에서  

$$  
E[X]=\frac{1}{\lambda}, \quad E[X^2]=\frac{2}{\lambda^2}  
$$
- 성질 3을 사용하면  

$$  
\mathrm{Var}(X)=E[X^2]-E[X]^2=\frac{2}{\lambda^2}-\frac{1}{\lambda^2}=\frac{1}{\lambda^2}  
$$
- 따라서 표준편차는  

$$  
\sigma_X=\frac{1}{\lambda}  
$$
- 또는 다음 정의를 직접 사용하여 계산할 수도 있다:  

$$  
\mathrm{Var}(X)=\int_0^\infty \left(x-\frac{1}{\lambda}\right)^2 \lambda e^{-\lambda x}\, dx  
$$



#### Example
- $Z \sim N(0,1)$ 일 때 $\mathrm{Var}(Z)=1$ 임을 보여라.
#### Note
- 정규분포의 표기법은 $X \sim N(\mu,\sigma^2)$ 이다.
- 이는 직관적으로 $E[X]=\mu$, $\mathrm{Var}(X)=\sigma^2$ 를 의미하는 것처럼 보이지만, 이를 실제로 증명해야 한다.
- 앞에서 $E[X]=\mu$ 임을 보였다.
- 이제 이 예제에서는 $Z \sim N(0,1)$ 에 대해 $\mathrm{Var}(Z)=1$ 임을 보인다.
- 다음 예제에서는 일반적인 경우 $\mathrm{Var}(X)=\sigma^2$ 임을 증명할 것이다.



#### Example
- $Z \sim N(0,1)$ 일 때 $\mathrm{Var}(Z)=1$ 임을 보여라.
#### Solution
- $E[Z]=0$ 이므로  

$$  
\mathrm{Var}(Z)=E[Z^2]=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty} z^2 e^{-z^2/2}\, dz  
$$
- 부분적분을 사용한다: $u=z$, $v'=z e^{-z^2/2} \Rightarrow u'=1$, $v=-e^{-z^2/2}$  

$$  
\mathrm{Var}(Z)=\frac{1}{\sqrt{2\pi}}\left(\left[-z e^{-z^2/2}\right]_{-\infty}^{\infty}+\int_{-\infty}^{\infty} e^{-z^2/2}\, dz\right)  
$$
- 첫 번째 항은 지수함수 $e^{-z^2/2}$ 가 $z$의 증가보다 훨씬 빠르게 $0$으로 가므로 $0$이다.
- 두 번째 항은 $N(0,1)$의 pdf $\phi(z)$의 전체 적분과 정확히 같으므로 $1$이다.
- 따라서  

$$  
\mathrm{Var}(Z)=1  
$$


- #### Example
- $X \sim N(\mu,\sigma^2)$ 일 때 $\mathrm{Var}(X)=\sigma^2$ 임을 보여라.
#### Solution
- 변수변환을 사용한다. $z=\dfrac{x-\mu}{\sigma}$ 로 두면  

$$\begin{align}  
\mathrm{Var}(X)=E[(X-\mu)^2]&=\frac{1}{\sqrt{2\pi}\sigma}\int_{-\infty}^{\infty} (x-\mu)^2 e^{-\frac{(x-\mu)^2}{2\sigma^2}} \, dx \\  
&=\frac{\sigma^2}{\sqrt{2\pi}}\int_{-\infty}^{\infty} z^2 e^{-z^2/2}\, dz=\sigma^2 
\end{align}
$$
- 마지막 적분은 이전에 $\mathrm{Var}(Z)$ 를 구할 때 계산한 것과 동일하다.

### Quantiles
#### Definition
- $X$의 중앙값(median)은 $P(X \le x)=0.5$ 를 만족하는 값 $x$이다.    
	- 즉 $P(X \le x)=P(X \ge x)=\dfrac{1}{2}$ 가 되는 값이다.    
- 다시 말해, 중앙값을 기준으로 위와 아래에 있을 확률이 각각 $\dfrac{1}{2}$ 이다.    
- cdf $F(x)=P(X \le x)$ 를 이용하면 중앙값은 다음을 만족하는 값이다:   

$$  
F(x)=0.5  
$$
- 생각해보기: $Z \sim N(0,1)$ 의 중앙값은 무엇인가? 
- 해답: 대칭성에 의해 중앙값은 $0$이다.


#### Example
- $X \sim \mathrm{exp}(\lambda)$ 의 중앙값을 구하라.
### Solution
- $X$의 cdf는  

$$  
F(x)=1-e^{-\lambda x}  
$$
- 중앙값은 $F(x)=0.5$ 를 만족하는 $x$ 이므로  

$$  
1-e^{-\lambda x}=0.5  
$$
- 이를 풀면  

$$  
e^{-\lambda x}=0.5 \Rightarrow -\lambda x=\ln(0.5)=-\ln 2 \Rightarrow x=\frac{\ln 2}{\lambda}  
$$
- 따라서 중앙값은  

$$  
\frac{\ln 2}{\lambda}  
$$
#### Think
- 이 경우 중앙값은 평균 $\mu=\dfrac{1}{\lambda}$ 와 같지 않다.
- 지수분포의 pdf는 오른쪽으로 긴 꼬리를 가지므로(오른쪽으로 치우침), 큰 값들이 평균을 끌어올린다.
- 따라서 중앙값은 평균보다 왼쪽에 위치한다.

- 좌우 대칭일때만 평균과 중앙값이 같음.
- 중앙값은 평균이 0.5면 됨.

#### Definition
- $X$의 $p$ 분위수(quantile)는 $P(X \le q_p)=p$ 를 만족하는 값 $q_p$ 이다.
#### Note
- 1. 이 표기에서 중앙값은 $q_{0.5}$ 이다.
- 2. 보통 cdf를 이용하여 다음과 같이 쓴다:  

$$  
F(q_p)=p  
$$
- 3. pdf $f(x)$의 관점에서 보면, $q_p$ 는 왼쪽 면적이 $p$, 오른쪽 면적이 $1-p$ 가 되도록 하는 값이다.

- quantile는 median을 좀 더 일반화 한 값임.
- median은 0.5 quantile임. = q0.5
- $q_p$ 는 왼쪽 면적이 $p$, 오른쪽 면적이 $1-p$ 가 되도록 하는 값


- 아래 예제들에서는 분위수를 pdf의 면적 또는 cdf의 높이로 그래프적으로 표현할 수 있음을 확인하자.
#### Example
- $X \sim U(0,1)$ 의 $0.6$ 분위수를 구하라.
#### Solution
- $X$의 cdf는 $[0,1]$ 구간에서 $F(x)=x$ 이다.
- 따라서 $F(q_{0.6})=0.6$ 이므로  

$$  
q_{0.6}=0.6  
$$



#### Example
- 표준정규분포 $Z \sim N(0,1)$ 의 $0.6$ 분위수를 구하라.
#### Solution
- 표준정규분포의 cdf는 닫힌 형태의 식이 없으므로 표 또는 계산 도구를 사용해야 한다.
- 따라서  

$$  
q_{0.6} \approx 0.25335  
$$
- 분위수(quantile)는 확률변수의 위치(location)를 나타내는 유용한 척도이다.    
- 이후 강의에서 이를 더 많이 활용하게 될 것이다.


### Percentiles, deciles, quartiles
- 편의를 위해 분위수는 종종 백분위수(percentiles), 십분위수(deciles), 사분위수(quartiles)로 표현된다.    
- 60번째 백분위수는 $0.6$ 분위수와 같다.    
- 예를 들어 키가 60번째 백분위수에 있다면, 이는 전체 인구의 60%보다 크다는 의미이며, 임의로 선택한 사람보다 클 확률이 60%라는 뜻이다.    
- deciles십분위수는 $\dfrac{1}{10}$ 단위로 나뉜다.    
- 세 번째 십분위수는 $0.3$ 분위수이다.    
- quartiles사분위수는 $\dfrac{1}{4}$ 단위로 나뉜다.    
- 세 번째 사분위수는 $0.75$ 분위수이며, 75번째 백분위수이다.

