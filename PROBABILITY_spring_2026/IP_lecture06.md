2026-03-26 08:20
## 6강

- Discrete Random Variable의 분산을 배울 것.

### Learning Goals
- 확률변수의 분산과 표준편차를 계산할 수 있다.
- 표준편차가 규모 또는 산포를 나타내는 척도임을 이해한다.
- 스케일링과 선형성의 성질을 이용해 분산을 계산할 수 있다.

### Spread
- 확률변수의 기댓값(평균)은 위치 또는 중심 경향을 나타내는 척도이다.
- 하나의 숫자로 확률변수를 요약해야 한다면 평균은 좋은 선택이다.    
- 그러나 평균은 많은 정보를 반영하지 못한다.
- 분산은 Discrete Random Variable이 얼마나 퍼져 있는지
- 기대값은 중간값이 어디있는지를 찾는 것.
- 그래서 Discrete Random Variable을 나타내는 값으로 기대값(평균)은 좋은 지표다
- 하지만 단점도 있음

- 평균은 $X$, $Y$ 둘다 0이지만 흩어진 정도는 다름.
- 예를 들어, 아래의 확률변수 $X$와 $Y$는 모두 평균이 $0$이지만, 평균 주변으로 확률질량이 퍼져 있는 방식은 매우 다르다.
- $X$의 값: $-2,-1,0,1,2$    
- 확률질량함수: $p(x)=\frac{1}{10},\frac{2}{10},\frac{4}{10},\frac{2}{10},\frac{1}{10}$    
- $Y$의 값: $-3,3$    
- 확률질량함수: $p(y)=\frac{1}{2},\frac{1}{2}$


### Variance and standard deviation
- 확률변수의 확률분포에서 평균을 중심으로 볼 때, 분산은 이 중심 주위에 확률질량이 얼마나 퍼져 있는지를 나타내는 척도이다.
- 먼저 분산의 형식적 정의를 제시한 뒤 그 의미를 살펴본다.    
- 정의: 확률변수 $X$의 평균이 $E[X]=\mu$일 때, $X$의 분산은 다음과 같이 정의된다.  

$$\mathrm{Var}(X)=E\big[(X-\mu)^2\big]$$
- $X$의 표준편차 $\sigma$는 다음과 같이 정의된다.  

$$\sigma=\sqrt{\mathrm{Var}(X)}$$

- 분산은 중앙에서 얼마나 퍼져 있는지 (spread out around this center)
- 표준편차(standard deviation)는 분산의 제곱근
- 먼저 정의를 합의 형태로 명시적으로 다시 쓰자.    
- 확률변수 $X$가 값 $x_1,x_2,\ldots,x_n$을 확률질량함수 $p(x_i)$로 가질 때, 분산은 다음과 같다.      

$$\mathrm{Var}(X)=E\big[(X-\mu)^2\big]=\sum_{i=1}^{n} p(x_i),(x_i-\mu)^2$$
- 말로 하면, $\mathrm{Var}(X)$의 공식은 평균으로부터의 거리의 제곱에 대한 가중평균을 취하는 것이다.    
- 제곱을 함으로써 항상 음이 아닌 값을 평균하게 되어, 평균의 왼쪽과 오른쪽으로의 퍼짐이 서로 상쇄되지 않는다.    
- 기댓값을 사용함으로써 확률이 큰 값은 더 크게, 확률이 작은 값은 더 작게 반영된다.
- $X$가 x1~xn 까지일때 p(xi)
- $x_i-\mu$의 제곱을 함
	- 제곱을 안하면 서로 플러스 마이너스 0이 되는 경우가 생김
	- 그래서 제곱을 해서 얼마나 떨어졌는지 계산
- 이  $(x_i-\mu)^2$값에 확률을 곱하면 됨.
- 그 후 이 곱들을 모두 더하면 Variance
- 단위에 대한 참고:
- $\sigma$는 $X$와 동일한 단위를 가진다.    
- $\mathrm{Var}(X)$는 $X$의 단위의 제곱과 동일한 단위를 가진다.    
- 따라서 $X$가 미터 단위라면, $\mathrm{Var}(X)$의 단위는 제곱미터이다.    
- $\sigma$와 $X$가 동일한 단위를 가지므로, 표준편차는 퍼짐(산포)을 나타내는 자연스러운 척도이다.
- 분산은 $X$는 제곱값이 들어가는데 표준편차를 사용하면 이 불편함이 사라짐
- X값에 m단위가 있으면 계산하고 나면 $m^2$ 이 되어 적절하지 않음 (다른 unit을 사용하게 된다는 의미)
- 분산의 개념을 명확히 하기 위해 예제를 살펴보자.
- 예제: 다음과 같은 값과 확률을 가지는 확률변수 $X$의 평균, 분산, 표준편차를 구하라.    
	- 값: $1,3,5$    
	- 확률질량함수: $\displaystyle p(x)=\frac{1}{4},\frac{1}{4},\frac{1}{2}$
- 풀이: 먼저 기댓값을 계산하면  

$$E[X]=\frac{7}{2}$$
- 다음으로 $(X-\frac{7}{2})^2$ 값을 포함하도록 표를 확장한다.    
	- 값: $1,3,5$    
	- $p(x)$: $\displaystyle \frac{1}{4},\frac{1}{4},\frac{1}{2}$    
	- $(x-\frac{7}{2})^2$: $\displaystyle \frac{25}{4},\frac{1}{4},\frac{9}{4}$
- 이제 분산을 계산하면  

$$\mathrm{Var}(X)=\frac{1}{4}\cdot\frac{25}{4}+\frac{1}{4}\cdot\frac{1}{4}+\frac{1}{2}\cdot\frac{9}{4}=\frac{25}{16}+\frac{1}{16}+\frac{9}{8}=\frac{44}{16}=\frac{11}{4}$$
   
- 표준편차는  

$$\sigma=\sqrt{\frac{11}{4}}=\frac{\sqrt{11}}{2}$$

- 분산의 개념을 명확히 하기 위해 예제를 계속 살펴보자.
- 예제: 다음과 같은 값과 확률을 가지는 확률변수 $X$의 평균, 분산, 표준편차를 구하라.    
- 값: $1,3,5$    
- 확률질량함수: $\displaystyle p(x)=\frac{1}{4},\frac{1}{4},\frac{1}{2}$
- 풀이: 분산 계산은 기댓값 계산과 유사하게 진행된다.  

$$\mathrm{Var}(X)=\frac{25}{4}\cdot\frac{1}{4}+\frac{1}{4}\cdot\frac{1}{4}+\frac{9}{4}\cdot\frac{1}{2}=\frac{11}{4}$$
- 제곱근을 취하면 표준편차는 다음과 같다.

$$\sigma=\sqrt{\frac{11}{4}}=\frac{\sqrt{11}}{2}$$
- Variance 계산은 기대값 계산과 유사. 
- 확률에 값을 곱해서 더하면 됨.
- standard deviation는 분산에 루트 씌움.

- 분산의 개념을 명확히 하기 위해 여러 확률변수를 비교해 보자.
- 문제: 확률변수 $X,Y,Z,W$ 각각에 대해 pmf를 그리고 평균과 분산을 구하라. 모든 확률변수는 평균이 $3$으로 같지만, 확률의 퍼짐 정도는 다르다. 
- $X$에 대한 풀이    
	- 값: $1,2,3,4,5$    
	- 확률질량함수: $\displaystyle p(x)=\frac{1}{5},\frac{1}{5},\frac{1}{5},\frac{1}{5},\frac{1}{5}$    
- 평균:   $\mu=E[X]=3$
- $(X-\mu)^2$ 계산:    
	- 값: $1,2,3,4,5$
	- $(x-3)^2$: $4,1,0,1,4$
- 분산:

$$\mathrm{Var}(X)=E[(X-\mu)^2]=\frac{4}{5}+\frac{1}{5}+0+\frac{1}{5}+\frac{4}{5}=2$$   
- 따라서 $X$의 분산은 $2$이다.
- $X,Y,Z,W$ 의 평균은 모두 3일때 각각의 random variable의 분산 계산
- X는 uniform ditribution(모든 확률이 값음)

- Y는 중앙에 값이 몰려 있음.
- 분산의 차이를 비교하기 위해 $Y$에 대해 계산해 보자.
- 값: $1,2,3,4,5$    
- 확률질량함수: $\displaystyle p(y)=\frac{1}{10},\frac{2}{10},\frac{4}{10},\frac{2}{10},\frac{1}{10}$    
- 평균:  $\mu=E[Y]=3$
- $(Y-\mu)^2$ 계산:    
	- 값: $1,2,3,4,5$  
	- $(y-3)^2$: $4,1,0,1,4$
- 분산:  

$$\mathrm{Var}(Y)=\frac{4}{10}+\frac{2}{10}+0+\frac{2}{10}+\frac{4}{10}=1.2$$
   
- 따라서 $Y$의 분산은 $1.2$이다.


- Z는 양 끝에 값이 몰려 있음.
- 확률변수 $Z$에 대해 계산해 보자.
	- 값: $1,2,3,4,5$    
	- 확률질량함수: $\displaystyle p(z)=\frac{5}{10},0,0,0,\frac{5}{10}$
- 평균: $\mu=E[Z]=3$
- $(Z-\mu)^2$ 계산:    
	- 값: $1,2,3,4,5$    
	- $(z-3)^2$: $4,1,0,1,4$    
- 분산: 

$$\mathrm{Var}(Z)=E[(Z-\mu)^2]=\frac{5}{10}\cdot4+\frac{5}{10}\cdot4=\frac{20}{10}+\frac{20}{10}=4$$
- 따라서 $Z$의 분산은 $4$이다.

- W는 평균에 모든 값이 몰려 있음
- 분산의 최소값은 0인데 이런 경우가 분산이 0
- 전혀 퍼져있지 않음.
- 확률변수 $W$에 대해 계산해 보자.
	- 값: $1,2,3,4,5$    
	- 확률질량함수: $p(w)=0,0,1,0,0$    
- 평균:  $\mu=E[W]=3$
- $(W-\mu)^2$ 계산:    
	- 값: $1,2,3,4,5$    
	- $(w-3)^2$: $4,1,0,1,4$
- 분산:  

$$\mathrm{Var}(W)=0$$   
- $W$는 항상 $3$의 값만 가지므로 변하지 않는다.    
- 따라서 분산이 $0$이다.



### The variance of a Bernoulli(p) random variable.
- 베르누이 확률변수는 매우 기본적이므로 그 분산을 알아두는 것이 중요하다.
- 정리: $X\sim \text{Bernoulli}(p)$이면

$$\mathrm{Var}(X)=p(1-p)$$
- 증명:    
- $E[X]=p$임을 알고 있다.    
- 표를 이용하여 분산을 계산하면 다음과 같다.    
	- 값: $0,1$    
	- 확률질량함수: $1-p,p$    
- $(X-\mu)^2$: $(0-p)^2,(1-p)^2$
- 따라서 분산은

$$\mathrm{Var}(X)=(1-p)p^2+p(1-p)^2=(1-p)p(1-p+p)=(1-p)p$$  
- 생각해보기:  $p(1-p)$가 최대가 되는 $p$는 무엇인가?

$$p(1-p)=p-p^2$$
- 이는 아래로 볼록한 이차함수이므로 꼭짓점에서 최대값을 가진다.   $$p=\frac{1}{2}$$
- 따라서 $p=1/2$일 때 분산이 최대가 된다.

- Bernoulli(p)기대 값은 p 임
- $Var(X) = (1-p)p$ 
- 언제 분산이 가장 높은가?
	- 이 값을 미분하면 됨.
	- p-p^2 미분
	- 1-2p=0
	- p=1/2


### A word about independence
#### independent random variable

- 지금까지 우리는 독립 확률변수의 개념을 명확히 정의하지 않고 사용해 왔다.
- 몇 차례 수업 후에는 연속 확률변수와 결합확률함수를 다룰 것이다.    
- 그 이후에 독립성의 완전한 정의를 다룰 준비가 된다.    
- 지금은 이산 확률변수에 대해 직관적이며 유효한 다음 정의를 사용한다.  
- 정의: 이산 확률변수 $X,Y$가 다음을 만족하면 서로 독립이다. 

$$P(X=a,Y=b)=P(X=a)P(Y=b)$$
- 모든 값 $a,b$에 대해 성립해야 한다.    
- 즉, 결합확률이 각각의 확률의 곱으로 표현된다.
- X와 Y가 independent인 경우:
	- 두개의 이벤트가 성립하면 random variable두개가 독립이라고 이야기 할 수 있음.

### Properties of variance
- 분산을 계산할 때 가장 유용한 세 가지 성질은 다음과 같다.
-  Properties1: $X$와 $Y$가 독립이면 

$$\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)$$
- Properties2:  상수 $a,b$에 대하여

$$\mathrm{Var}(aX+b)=a^2\mathrm{Var}(X)$$
- Properties3:

$$\mathrm{Var}(X)=E[X^2]-E[X]^2$$
    
- Properties 1에서는 $X$와 $Y$가 독립이어야 한다는 조건에 특히 주의해야 한다.   
- Properties 3은 계산에서 더 사용하기 쉬운 분산 공식이다.
- Properties of variance를 이야기 하려면 독립의 개념이 나옴
- 기대값 이야기 할때는 독립 이야기가 필요 없었음. 그냥 둘을 나눠서 계산하면 되었음.
- X, Y 가 독립이면 Var(X + Y ) = Var(X ) + Var(Y )
- Var(aX + b)를 계산하면 a는 제곱이되고 b는 사라짐.
- $Var(X ) = E [X^2] − E [X ]^2$  
- $X$와 $Y$가 서로 독립이고 $\mathrm{Var}(X)=3$, $\mathrm{Var}(Y)=5$일 때, $\mathrm{Var}(X+Y)$를 구하라.
- $X$와 $Y$가 독립이므로 분산의 성질을 사용할 수 있다.      $$\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)$$  
- 따라서 

$$\mathrm{Var}(X+Y)=3+5=8$$

- 예제: $X$와 $Y$가 서로 독립이고 $\mathrm{Var}(X)=3$, $\mathrm{Var}(Y)=5$일 때, $\mathrm{Var}(3X+4)$를 구하라.
- 풀이: 분산의 Property 1, 2를 사용하면

$$\mathrm{Var}(3X+4)=3^2\mathrm{Var}(X)$$
- 따라서

$$\mathrm{Var}(3X+4)=9\cdot 3=27$$

- 예제: $X$와 $Y$가 서로 독립이고 $\mathrm{Var}(X)=3$, $\mathrm{Var}(Y)=5$일 때, $\mathrm{Var}(X+X)$를 구하라.
- 풀이: Property 1은 사용할 수 없다. $X$는 자기 자신과 독립이 아니기 때문이다.    
- 만약 Property  1을 잘못 사용하면 $\mathrm{Var}(X)+\mathrm{Var}(X)=6$이라는 잘못된 결과를 얻게 된다.    
- 대신 Property  2를 사용하면

$$\mathrm{Var}(X+X)=\mathrm{Var}(2X)=4\mathrm{Var}(X)$$
- 따라서

$$\mathrm{Var}(X+X)=4\cdot 3=12$$
- Property 1을 적용하면 안됨. 
- X는 자기 자신에게 독립이기 때문에 안됨.
- X, Y가 독립이니까 Properties 1 and 2 사용
- 예제: $X$와 $Y$가 서로 독립이고 $\mathrm{Var}(X)=3$, $\mathrm{Var}(Y)=5$일 때, $\mathrm{Var}(X+3Y)$를 구하라.
- 풀이: 분산의 성질 1과 2를 함께 사용한다.

$$\mathrm{Var}(X+3Y)=\mathrm{Var}(X)+\mathrm{Var}(3Y)$$
- 성질 2에 의해

$$\mathrm{Var}(3Y)=3^2\mathrm{Var}(Y)=9\cdot 5$$
- 따라서

$$\mathrm{Var}(X+3Y)=3+45=48$$

- Property 3으로 X ∼ Bernoulli(p) 구할 수 있음.
- 예제: 성질 3을 이용하여 $X\sim \text{Bernoulli}(p)$의 분산을 구하라.
- 풀이: 표를 이용하면    
	- 값: $0,1$    
	- 확률질량함수: $1-p,p$    
	- $X^2$: $0,1$    
- 따라서

$$E[X^2]=p$$
- 성질 3을 적용하면

$$\mathrm{Var}(X)=E[X^2]-E[X]^2=p-p^2$$
- 정리하면 

$$\mathrm{Var}(X)=p(1-p)$$
- 이는 앞서 구한 결과와 일치한다.
- 예제: 성질 3을 이용하여 예제 1의 $X$의 분산을 구하라.
- 풀이:표를 이용하면    
	- 값: $1,3,5$    
	- 확률질량함수: $\frac{1}{4},\frac{1}{4},\frac{1}{2}$    
	- $X^2$: $1,9,25$    
- 따라서

$$E[X]=\frac{7}{2},\quad E[X^2]=1\cdot\frac{1}{4}+9\cdot\frac{1}{4}+25\cdot\frac{1}{2}=\frac{60}{4}=15$$

- 성질 3을 적용하면

$$\mathrm{Var}(X)=E[X^2]-E[X]^2=15-\left(\frac{7}{2}\right)^2=\frac{11}{4}$$
- 이는 예제 1에서 구한 결과와 같다.


### Variance of binomial (n, p)
- 베르누이의 분산이 p(1-p)니까 거기에 n만 곱하면 됨.
- 정리: $X\sim \mathrm{Binomial}(n,p)$이면 분산은 다음과 같다.

$$\mathrm{Var}(X)=np(1-p)$$

- 설명: 이항분포 확률변수 $X$는 서로 독립인 베르누이 확률변수 $n$개의 합으로 표현된다.

$$X=X_1+X_2+\cdots+X_n,\quad X_i\sim \text{Bernoulli}(p)$$

- 각 $X_i$의 분산은  

$$\mathrm{Var}(X_i)=p(1-p)$$
- 독립이므로 분산의 성질을 적용하면

$$\mathrm{Var}(X)=\sum_{i=1}^{n}\mathrm{Var}(X_i)=n p(1-p)$$

#### Property  2
- 상수 $a,b$에 대하여  

$$\mathrm{Var}(aX+b)=a^2\mathrm{Var}(X)$$
- 증명: 이는 기댓값 $E[X]$의 성질과 간단한 대수 계산으로부터 따른다.    
- $\mu=E[X]$라고 하자.    
- 그러면  

$$E[aX+b]=a\mu+b$$
- 분산의 정의를 적용하면  

$$\mathrm{Var}(aX+b)=E\big[(aX+b-(a\mu+b))^2\big]$$
- 정리하면

$$=E\big[(aX-a\mu)^2\big]=E\big[a^2(X-\mu)^2\big]$$
- 상수를 밖으로 빼면  

$$=a^2E\big[(X-\mu)^2\big]$$
- 따라서  

$$=a^2\mathrm{Var}(X)$$


#### Property  3

$$\mathrm{Var}(X)=E[X^2]-E[X]^2$$
- 증명:기댓값의 성질과 간단한 대수 계산을 이용한다.    
- $\mu=E[X]$는 상수이다.    
- 분산의 정의에서 시작하면 

$$\mathrm{Var}(X)=E[(X-\mu)^2]$$
- 전개하면

$$E[(X-\mu)^2]=E[X^2-2\mu X+\mu^2]$$
- 기댓값의 선형성을 이용하면

$$=E[X^2]-2\mu E[X]+\mu^2$$
- $E[X]=\mu$이므로

$$=E[X^2]-2\mu^2+\mu^2$$
- 정리하면

$$=E[X^2]-\mu^2$$
- 따라서 

$$\mathrm{Var}(X)=E[X^2]-E[X]^2$$


### Table of Distributions
- Distributions 요약

| 분포              | 값의 범위          | 확률질량함수 $p(x)$                     | 평균 $E[X]$       | 분산 $\mathrm{Var}(X)$ |
| --------------- | -------------- | --------------------------------- | --------------- | -------------------- |
| Bernoulli$(p)$  | $0,1$          | $p(0)=1-p,;p(1)=p$                | $p$             | $p(1-p)$             |
| Binomial$(n,p)$ | $0,1,\ldots,n$ | $p(k)=\binom{n}{k}p^k(1-p)^{n-k}$ | $np$            | $np(1-p)$            |
| Uniform$(n)$    | $1,2,\ldots,n$ | $p(k)=\frac{1}{n}$                | $\frac{n+1}{2}$ | $\frac{n^2-1}{12}$   |
| Geometric$(p)$  | $0,1,2,\ldots$ | $p(k)=p(1-p)^k$                   | $\frac{1-p}{p}$ | $\frac{1-p}{p^2}$    |


### Table of Properties
- Properties 요약
- 이산 확률변수 $X$가 값 $x_1,x_2,\ldots$를 가지며 확률질량함수 $p(x_j)$를 가진다고 하자.

| 구분       | 기댓값 (평균)                       | 분산                                                          |
| -------- | ------------------------------ | ----------------------------------------------------------- |
| 표기       | $E[X],\mu$                     | $\mathrm{Var}(X),\sigma^2$                                  |
| 정의       | $E[X]=\sum_j p(x_j)x_j$        | $\mathrm{Var}(X)=E[(X-\mu)^2]=\sum_j p(x_j)(x_j-\mu)^2$     |
| 스케일 및 이동 | $E[aX+b]=aE[X]+b$              | $\mathrm{Var}(aX+b)=a^2\mathrm{Var}(X)$                     |
| 선형성      | (임의의 $X,Y$) $E[X+Y]=E[X]+E[Y]$ | (독립일 때) $\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)$ |
| 함수       | $E[h(X)]=\sum_j p(x_j)h(x_j)$  |                                                             |
| 대안 공식    |                                | $\mathrm{Var}(X)=E[X^2]-E[X]^2=E[X^2]-\mu^2$                |
|          |                                |                                                             |
