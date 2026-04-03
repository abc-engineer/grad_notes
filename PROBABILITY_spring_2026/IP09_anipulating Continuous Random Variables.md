2026-04-02 08:20
## 9강 Manipulating Continuous Random Variables

### Learning Goals
- 알려진 pdf와 cdf를 가진 확률변수로 정의된 새로운 확률변수의 pdf와 cdf를 구할 수 있다.

### Transformations of Random Variables
- 우리는 종종 알려진 확률변수에 어떤 공식을 적용하여 새로운 확률변수를 만든다.
	- 예를 들어 $Y = aX + b$ 또는 $Y = X^2$ 와 같은 변환을 고려할 수 있다.
	- 우리는 $X$의 pdf와 cdf로부터 $Y$의 확률밀도함수(pdf)와 누적분포함수(cdf)를 구하는 방법을 살펴볼 것이다.
- 이산 확률변수의 경우에는 확률표를 이용하여 이를 구하는 것이 가능했다.
	- 연속 확률변수의 경우에는 체계적인 대수적 기법을 사용해야 한다.
- pdf의 변환은 미적분에서의 변수변환(치환적분, ‘u-substitution’)과 동일한 원리임을 보게 된다.
- cdf를 직접 변환할 때는 확률로서의 정의를 이용한다.
	- 복습:
	- $X$의 누적분포함수(cdf)는 $F_X(x) = P(X \le x)$ 이다.
	- $X$의 확률밀도함수(pdf)는 다음 관계를 만족한다.  

$$  
f_X(x) = F'_X(x)  
$$

- random variable은 수식을 쓸 수 있음
	- $Y = aX + b or Y = X^2$
	- 이럴때 Y의 pdf, cdf등은 어떻게 되는지 계산하는 것이 Manipulating
- discrete random variable일때는 테이블 그려서 값을 구하면 되었음 (지난 수업들)
- 연속일 경우 대수적 계산이 필요함.
	- pdf 예를 들면 미적분
	- cdf는 정의를 보고 계산 해야 함.
		- $F_X (x) = P(X ≤ x)$
		- cdf를 미분하면 pdf

### Transforming the cdf
#### Example
- $X$의 범위가 $[0,2]$이고 cdf가 $F_X(x)=\dfrac{x^2}{4}$ 라고 하자. 이때 $Y=X^2$의 범위, pdf, cdf는 무엇인가?    
#### Solution    
- 범위는 쉽게 구할 수 있다: $[0,4]$.    
- cdf를 구하기 위해 정의에서부터 체계적으로 시작한다.    
- 이 예제에서는 사고 과정을 자세히 볼 수 있도록 매우 작은 단계들로 나누어 설명할 것이다.
- X has range \[0, 2\]
- $F_X (x) = x^2/4$ 일때 $Y = X ^2$의범위와 pdf, cdf 구하기


#### Example
- $X$의 범위가 $[0,2]$이고 cdf가 $F_X(x)=\dfrac{x^2}{4}$ 라고 하자. $Y=X^2$의 범위, pdf, cdf를 구하라.    
#### Solution   
- 1. 정의를 사용한다: $F_Y(y)=P(Y \le y)$        
- 2. $Y$를 $X$에 대한 식으로 바꾼다: $P(Y \le y)=P(X^2 \le y)$        
- 3. $X$를 분리하도록 대수적으로 변형한다: $P(X^2 \le y)=P(X \le \sqrt{y})$        
- 4. 이것이 정확히 $F_X$의 정의임을 확인한다: $P(X \le \sqrt{y})=F_X(\sqrt{y})$
-  5. $F_X$의 알려진 공식을 사용한다: $F_X(\sqrt{y})=\dfrac{(\sqrt{y})^2}{4}=\dfrac{y}{4}$        
- 6. 1단계부터 5단계까지를 종합하면 cdf는 다음과 같다: $F_Y(y)=P(Y \le y)=P(X^2 \le y)=P(X \le \sqrt{y})=F_X(\sqrt{y})=\dfrac{y}{4}$	
- 7. 마지막으로 pdf는 cdf를 미분하여 구한다:  

$$  
f_Y(y)=\frac{d}{dy}F_Y(y)=\frac{1}{4}  
$$
- cdf는 그냥 수식 대입으로 계산하면 됨.
- pdf는 cdf 미분하면됨.

### Transforming the pdf directly
- pdf를 직접 구하는 또 다른 방법은 변수변환(change of variables)을 사용하는 것이다.    
- 이 방법은 완전성을 위해, 그리고 이를 선호하는 사람들을 위해 제시한다.    
- 일반적으로는 cdf를 변환하는 것이 더 쉽다고 느끼는 경우가 많다.    
- 미적분에서 배운 ‘u-치환(u-substitution)’을 떠올리자.    
- 먼저 이를 상기하기 위한 미적분 예제를 살펴본 뒤, pdf에 적용할 것이다.
-  change of variable를 쓰면 cdf가지 않고 pdf를 미적분해서 구할 수 있음 -> 치환적분분

#### Example
- (미적분 예제): 적분 $\int (x^2+1)^7 , dx$ 를 $u=x^2+1$에 대한 적분으로 변환하라.
#### Solution
- 적분의 각 부분을 $x$에서 $u$로 변환해야 한다.
- $u=x^2+1$ 이므로 $(x^2+1)^7 = u^7$
- 미분하면 $du=2x,dx$ 이다.
- 따라서 $dx=\dfrac{du}{2x}=\dfrac{du}{2\sqrt{u-1}}$
- 이제 적분의 각 항을 치환하면 다음을 얻는다:  

$$  
\int (x^2+1)^7 , dx = \int \frac{u^7}{2\sqrt{u-1}} , du  
$$



#### Example
- $X$의 범위가 $[0,2]$, cdf가 $F_X(x)=\dfrac{x^2}{4}$ 일 때, $Y=X^2$의 pdf를 ‘u-치환’ 방법으로 직접 구하라. (이 경우 $u$는 실제로 $y$가 된다.)    
#### Solution
- 확률은 적분 $\int f_X(x),dx$ 로 주어진다는 것을 기억하자.
- 변수변환 $y=x^2$ 가 주어졌으므로, 적분을 $x$에서 $y$로 바꾼다.
- $y=x^2 \Rightarrow dy=2x,dx$ 이므로 $dx=\dfrac{dy}{2\sqrt{y}}$
- $F_X(x)=\dfrac{x^2}{4}$ 이므로 이를 미분하면 pdf는 다음과 같다:  

$$  
f_X(x)=F'_X(x)=\frac{x}{2}  
$$



#### Example
- $X$의 범위가 $[0,2]$, cdf가 $F_X(x)=\dfrac{x^2}{4}$ 일 때, $Y=X^2$의 pdf를 ‘u-치환’으로 구하라.
#### Solution
- $y=x^2$ 이므로 $x=\sqrt{y}$ 이고, 따라서 $f_X(x)=\dfrac{x}{2}=\dfrac{\sqrt{y}}{2}$
- 앞에서 구한 $dx=\dfrac{dy}{2\sqrt{y}}$ 를 이용한다.
- 두 식을 결합하면 다음과 같다:  

$$  
f_X(x),dx=\frac{\sqrt{y}}{2}\cdot \frac{dy}{2\sqrt{y}}=\frac{1}{4},dy  
$$
- 이는 확률을 나타내는 적분의 형태이므로, $dy$ 앞의 계수가 pdf가 된다.
- 따라서  

$$  
f_Y(y)=\frac{1}{4}  
$$
- 이전에 cdf를 이용해 구한 결과와 정확히 일치한다.


#### Example
- $X \sim \mathrm{exp}(\lambda)$, 즉 $f_X(x)=\lambda e^{-\lambda x}$ (구간 $[0,\infty]$)일 때, $Y=X^2$의 pdf를 구하라.    
#### Solution
- pdf의 변수변환 방법을 사용한다.
- $y=x^2 \Rightarrow dy=2x,dx$ 이므로 $dx=\dfrac{dy}{2\sqrt{y}}$
- $f_X(x)=\lambda e^{-\lambda x}$ 이고, $x=\sqrt{y}$ 를 대입하면 $f_X(x)=\lambda e^{-\lambda \sqrt{y}}$
- 이를 결합하면 다음을 얻는다:  

$$  
f_X(x),dx=\lambda e^{-\lambda \sqrt{y}} \cdot \frac{dy}{2\sqrt{y}}=f_Y(y),dy  
$$
- 따라서 pdf는  

$$  
f_Y(y)=\frac{\lambda}{2\sqrt{y}} e^{-\lambda \sqrt{y}}  
$$



#### Example
- 이전 예제를 cdf를 이용하여 다시 풀어보자.
#### Solution
- $X \sim \mathrm{exp}(\lambda)$ 의 cdf는 $F_X(x)=1-e^{-\lambda x}$ 이다.
- 따라서 $Y=X^2$ 에 대해
- $F_Y(y)=P(Y \le y)=P(X^2 \le y)=P(X \le \sqrt{y})=F_X(\sqrt{y})=1-e^{-\lambda \sqrt{y}}$
- 즉,  

$$  
F_Y(y)=1-e^{-\lambda \sqrt{y}}  
$$
- 만약 pdf를 구하고 싶다면 이를 미분하면 된다.
- 그러면 이전 예제에서 구한 것과 동일한 결과를 얻는다: 

$$  
f_Y(y)=\frac{\lambda}{2\sqrt{y}} e^{-\lambda \sqrt{y}}  
$$



#### Example
- $X \sim N(5,3^2)$ 일 때, $Z=\dfrac{X-5}{3}$ 는 표준정규분포, 즉 $Z \sim N(0,1)$ 임을 보여라.
#### Solution
- 변수변환과 $f_X(x)$의 공식을 사용한다.

$$z=\dfrac{x-5}{3} \Rightarrow dz=\dfrac{dx}{3}$ 이므로 $dx=3,dz$$

- 이 예제에서는 $f_X(x),dx$ 를 한 줄로 변환한다:  

$$  
f_X(x),dx=\frac{1}{3\sqrt{2\pi}} e^{-\frac{(x-5)^2}{2\cdot 3^2}} dx  
=\frac{1}{3\sqrt{2\pi}} e^{-\frac{z^2}{2}} \cdot 3,dz  
=\frac{1}{\sqrt{2\pi}} e^{-\frac{z^2}{2}} dz  
= f_Z(z),dz  
$$
- 따라서  

$$  
f_Z(z)=\frac{1}{\sqrt{2\pi}} e^{-\frac{z^2}{2}}  
$$
- 이는 표준정규분포의 확률밀도함수이다.

### Standardization of normal random variables
- 마지막 예제는 정규확률변수의 중요한 일반 성질을 보여준다.
- 이를 정리로 서술하면 다음과 같다.
- 정리 (정규확률변수의 표준화)
- $X \sim N(\mu,\sigma^2)$ 라고 하자.
- 이때 다음과 같이 정의된 변수  

$$  
Z=\frac{X-\mu}{\sigma}  
$$
- 는 표준정규분포를 따른다. 즉,  

$$  
Z \sim N(0,1)  
$$
- Standardization 을 하면 일반 정규분포가 표준화 되어 표준정규 분포가 됨.


#### Proof    
- 이는 이전 예제와 동일한 계산이며, $5$를 $\mu$로, $3$을 $\sigma$로 바꾼 것과 같다.

$$z=\dfrac{x-\mu}{\sigma} \Rightarrow dz=\dfrac{dx}{\sigma} \Rightarrow dx=\sigma,dz$$
- 이를 이용하여 $f_X(x),dx$ 를 변환하면 다음과 같다:  

$$  
f_X(x),dx=\frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}} dx  
=\frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{z^2}{2}} \cdot \sigma,dz  
=\frac{1}{\sqrt{2\pi}} e^{-\frac{z^2}{2}} dz  
= f_Z(z),dz  
$$
- 따라서  

$$  
f_Z(z)=\frac{1}{\sqrt{2\pi}} e^{-\frac{z^2}{2}}  
$$

- 이는 $Z$가 표준정규분포를 따름을 의미한다.
- 이 정리에서 $X$를 $Z$로 변환하는 과정을 표준화(standardization)라고 하며, 이는 임의의 정규확률변수를 표준정규확률변수로 변환하는 과정이다.

