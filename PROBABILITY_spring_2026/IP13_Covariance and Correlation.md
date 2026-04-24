2026-04-16 08:20
## 13강 Covariance and Correlation

- 독립은 X,Y 가 관계가 없는 것
- 하지만 실생활에서 아주 관계가 없는 경우는 거의 없음
- 주사위나 동전도 끈적이는것이 묻어있으면 1번째 2번째 결과가 관계 없다고 말할 수 없음.
- dependence를 계산 해야 함.

### Learning Goals
- 공분산(covariance)과 상관계수(correlation)의 의미를 이해한다.
- 두 확률변수의 공분산과 상관계수를 계산할 수 있다.


### Covariance
- 공분산(covariance)은 두 확률변수가 함께 얼마나 변하는지를 나타내는 측도이다.
- 예를 들어, 기린의 키와 몸무게는 한 변수가 크면 다른 변수도 큰 경향이 있으므로 양의 공분산을 가진다.
#### Definition
- $X$와 $Y$가 평균 $\mu_X$, $\mu_Y$를 가지는 확률변수라고 하자.
- $X$와 $Y$의 공분산은 다음과 같이 정의된다.  

$$  
\operatorname{Cov}(X,Y)=E\left[(X-\mu_X)(Y-\mu_Y)\right]  
$$

- 이 식은 분산의 식과 매우 유사함.
- 같은걸 제곱하면 분산 공분산은 다른것 2개를 곱합합


### Properties of covariance
- 성질  
- Properties 1. $\operatorname{Cov}(aX+b,;cY+d)=ac,\operatorname{Cov}(X,Y)$ 여기서 $a,b,c,d$는 상수이다.
- Properties 2. $\operatorname{Cov}(X_1+X_2,\;Y)=\operatorname{Cov}(X_1,Y)+\operatorname{Cov}(X_2,Y)$
- Properties 3. $\operatorname{Cov}(X,X)=\operatorname{Var}(X)$
- Properties 4. $\operatorname{Cov}(X,Y)=E[XY]-\mu_X\mu_Y$
- Properties 5. $\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y)$
- Properties 6.
	- 위 식은 임의의 $X,Y$에 대해 성립한다.
	- $X$와 $Y$가 독립이면  
$\operatorname{Cov}(X,Y)=0$

#### Warning
- 역은 일반적으로 성립하지 않는다.
- 즉, 공분산이 $0$이라고 해서 항상 독립인 것은 아니다.
#### Note
- 성질 4는 분산의 공식과 유사하다.
- 실제로 $X=Y$이면 다음 식이 된다.  

$$  
\operatorname{Var}(X)=E[X^2]-\mu_X^2  
$$
- 또한 성질 5에서, $X$와 $Y$가 독립이면 $\operatorname{Cov}(X,Y)=0$이므로  

$$  
\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)  
$$  
가 되어 이전에 배운 공식과 일치한다.



### Proofs of properties of covariance
#### Property of covariance 1 

$$  
\operatorname{Cov}(aX+b,;cY+d)=ac,\operatorname{Cov}(X,Y)  
$$

- 여기서 $a,b,c,d$는 상수이다.

##### Proof.

$$  
\operatorname{Cov}(aX+b,;cY+d)  
=E\left[\bigl((aX+b)-E[aX+b]\bigr)\bigl((cY+d)-E[cY+d]\bigr)\right]  
$$


$$  
=E\left[\bigl(aX+b-(a\mu_X+b)\bigr)\bigl(cY+d-(c\mu_Y+d)\bigr)\right]  
$$

$$  
=E\left[a(X-\mu_X),c(Y-\mu_Y)\right]  
$$

$$  
=E\left[ac(X-\mu_X)(Y-\mu_Y)\right]  
$$

$$  
=ac,E\left[(X-\mu_X)(Y-\mu_Y)\right]  
$$

$$  
=ac,\operatorname{Cov}(X,Y)  
$$


#### Property of covariance  2 

$$  
\operatorname{Cov}(X_1+X_2,;Y)=\operatorname{Cov}(X_1,Y)+\operatorname{Cov}(X_2,Y)  
$$

##### Proof.

$$  
\operatorname{Cov}(X_1+X_2,\;Y)  
=E\left[\bigl((X_1+X_2)-(\mu_{X_1}+\mu_{X_2})\bigr)(Y-\mu_Y)\right]  
$$


$$  
=E\left[(X_1-\mu_{X_1}+X_2-\mu_{X_2})(Y-\mu_Y)\right]  
$$

$$  
=E\left[(X_1-\mu_{X_1})(Y-\mu_Y)\right]+E\left[(X_2-\mu_{X_2})(Y-\mu_Y)\right]  
$$

$$  
=\operatorname{Cov}(X_1,Y)+\operatorname{Cov}(X_2,Y)  
$$

#### Property of covariance  3  

$$  
\operatorname{Cov}(X,X)=\operatorname{Var}(X)  
$$

##### Proof.

- 이는 분산의 정의에서 바로 나온다.  

$$  
\operatorname{Cov}(X,X)=E[(X-\mu_X)(X-\mu_X)]  
$$


$$  
=E[(X-\mu_X)^2]  
$$

$$  
=\operatorname{Var}(X)  
$$



#### Property of covariance   4

$$  
\operatorname{Cov}(X,Y)=E[XY]-\mu_X\mu_Y  
$$

##### Proof.

- 먼저  

$$  
E[X-\mu_X]=0  
$$  
임을 기억하자.


$$  
\operatorname{Cov}(X,Y)=E[(X-\mu_X)(Y-\mu_Y)]  
$$

$$  
=E[XY-\mu_XY-\mu_YX+\mu_X\mu_Y]  
$$

$$  
=E[XY]-\mu_XE[Y]-\mu_YE[X]+\mu_X\mu_Y  
$$

$$  
=E[XY]-\mu_X\mu_Y-\mu_Y\mu_X+\mu_X\mu_Y  
$$

$$  
=E[XY]-\mu_X\mu_Y  
$$

#### Property of covariance   5

$$  
\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y)  
$$

- 이는 임의의 $X,Y$에 대해 성립한다.

##### Proof.

- 성질 3과 성질 2를 이용하면,  

$$  
\operatorname{Var}(X+Y)=\operatorname{Cov}(X+Y,;X+Y)  
$$

$$  
=\operatorname{Cov}(X,X)+\operatorname{Cov}(X,Y)+\operatorname{Cov}(Y,X)+\operatorname{Cov}(Y,Y)  
$$

- 공분산은 대칭이므로  

$$  
\operatorname{Cov}(X,Y)=\operatorname{Cov}(Y,X)  
$$

- 따라서  

$$  
=\operatorname{Cov}(X,X)+2\operatorname{Cov}(X,Y)+\operatorname{Cov}(Y,Y)  
$$


$$  
=\operatorname{Var}(X)+2\operatorname{Cov}(X,Y)+\operatorname{Var}(Y)  
$$

$$  
=\operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y)  
$$

#### Property of covariance   6

- $X$와 $Y$가 독립이면  

$$  
\operatorname{Cov}(X,Y)=0  
$$

##### Proof.

- $X$와 $Y$가 독립이면 결합 pdf는

$$  
f(x,y)=f_X(x)f_Y(y)  
$$  
로 분해된다.

- 따라서  

$$  
\operatorname{Cov}(X,Y)=\iint (x-\mu_X)(y-\mu_Y)f_X(x)f_Y(y),dx,dy  
$$

- 적분을 분리하면  

$$  
=\left(\int (x-\mu_X)f_X(x),dx\right)\left(\int (y-\mu_Y)f_Y(y),dy\right)  
$$


$$  
=E[X-\mu_X];E[Y-\mu_Y]  
$$

- 그런데  

$$  
E[X-\mu_X]=0,\qquad E[Y-\mu_Y]=0  
$$

- 그러므로  

$$  
\operatorname{Cov}(X,Y)=0  
$$

### Sums and integrals for computing covariance

- 공분산은 기댓값(expected value)으로 정의되므로, 평소와 같이 합(sum) 또는 적분(integral)으로 계산한다.

#### Discrete case

- $X$와 $Y$가 결합 pmf $p(x_i,y_j)$를 가지면, 

$$  
\operatorname{Cov}(X,Y)=\sum_{i=1}^{n}\sum_{j=1}^{m} p(x_i,y_j)(x_i-\mu_X)(y_j-\mu_Y)  
$$

- 또한 성질 $\operatorname{Cov}(X,Y)=E[XY]-\mu_X\mu_Y$를 이용하면  

$$  
\operatorname{Cov}(X,Y)=\left(\sum_{i=1}^{n}\sum_{j=1}^{m} p(x_i,y_j)x_i y_j\right)-\mu_X\mu_Y  
$$


- 공분산은 기댓값으로 정의되므로, 연속형의 경우에는 적분으로 계산한다.
#### Continuous case
- $X$와 $Y$가 구간 $[a,b]\times[c,d]$에서 결합 pdf $f(x,y)$를 가지면,  

$$  
\operatorname{Cov}(X,Y)=\int_c^d\int_a^b (x-\mu_X)(y-\mu_Y)f(x,y),dx,dy  
$$

- 또한 성질 $\operatorname{Cov}(X,Y)=E[XY]-\mu_X\mu_Y$를 이용하면  

$$  
\operatorname{Cov}(X,Y)=\left(\int_c^d\int_a^b xy,f(x,y),dx,dy\right)-\mu_X\mu_Y  
$$


#### Example

- 공정한 동전을 3번 던진다.
- $X$를 처음 2번 던짐에서 나온 앞면의 개수, $Y$를 마지막 2번 던짐에서 나온 앞면의 개수라고 하자.
- 즉, 두 변수는 가운데 던짐 결과를 공통으로 포함한다.
- $\operatorname{Cov}(X,Y)$를 구하여라.

#### Solution
- 두 가지 방법으로 구할 수 있다.
- 결합확률표와 정의를 이용하는 방법
- 공분산의 성질을 이용하는 방법
- 3번 던지면 가능한 결과는 총 $8$개이다.  

$$  
{HHH,HHT,HTH,HTT,THH,THT,TTH,TTT}  
$$
- 각 결과에서 $(X,Y)$를 계산하면 다음과 같다.


|결과|$X$|$Y$|
|---|---|---|
|$HHH$|$2$|$2$|
|$HHT$|$2$|$1$|
|$HTH$|$1$|$1$|
|$HTT$|$1$|$0$|
|$THH$|$1$|$2$|
|$THT$|$1$|$1$|
|$TTH$|$0$|$1$|
|$TTT$|$0$|$0$|

- 각 결과의 확률은 모두 $\frac{1}{8}$이다. 따라서  

$$  
E[X]=1,\qquad E[Y]=1  
$$

- 이제  

$$  
E[XY]=\frac{1}{8}(4+2+1+0+2+1+0+0)=\frac{10}{8}=\frac{5}{4}  
$$

- 그러므로  

$$  
\operatorname{Cov}(X,Y)=E[XY]-E[X]E[Y]  
$$


$$  
=\frac{5}{4}-1\cdot 1=\frac{1}{4}  
$$

- 따라서  

$$  
\operatorname{Cov}(X,Y)=\frac{1}{4}  
$$

- 해석

- 공분산이 양수이므로, $X$가 클수록 $Y$도 커지는 경향이 있다.

- 이는 두 변수가 두 번째 동전 결과를 공유하기 때문이다.


- 주변분포로부터  

$$  
E[X]=1,\qquad E[Y]=1  
$$  
임을 계산할 수 있다.

- 이제 공분산의 정의를 사용하면  

$$  
\operatorname{Cov}(X,Y)=E[(X-\mu_X)(Y-\mu_Y)]  
$$


$$  
=\sum_{i,j} p(x_i,y_j)(x_i-1)(y_j-1)  
$$

- 합에서 값이 $0$이 되는 항들은 제외할 수 있다.

- 즉, 다음 경우의 항들은 모두 $0$이다.

- $x_i=1$

- 또는 $y_j=1$

- 또는 해당 확률이 $0$

- 따라서 0이 아닌 항만 남기면  

$$  
\operatorname{Cov}(X,Y)  
=\frac{1}{8}(0-1)(0-1)+\frac{1}{8}(2-1)(2-1)  
$$


$$  
=\frac{1}{8}(1)+\frac{1}{8}(1)  
=\frac{2}{8}  
=\frac{1}{4}  
$$

- 따라서  

$$  
\operatorname{Cov}(X,Y)=\frac{1}{4}  
$$

#### Solution
- 공분산의 성질 4를 이용해서도 계산할 수 있다.  

$$  
\operatorname{Cov}(X,Y)=E[XY]-\mu_X\mu_Y  
$$

- 전체 표에서 $XY$의 기댓값을 계산하면  

$$  
E[XY]  
=1\cdot\frac{2}{8}+2\cdot\frac{1}{8}+2\cdot\frac{1}{8}+4\cdot\frac{1}{8}  
=\frac{10}{8}  
=\frac{5}{4}  
$$

- 그리고  

$$  
\mu_X=E[X]=1,\qquad \mu_Y=E[Y]=1  
$$

- 따라서  

$$  
\operatorname{Cov}(X,Y)=\frac{5}{4}-1\cdot1=\frac{1}{4}  
$$

- 즉,  

$$  
\operatorname{Cov}(X,Y)=\frac{1}{4}  
$$

#### Solution

- 이제 공분산의 성질을 이용하여 $\operatorname{Cov}(X,Y)$를 다시 계산해 보자.
- 앞에서와 같이 $X_i$를 $i$번째 동전 던지기에서 앞면이 나오면 $1$, 뒷면이 나오면 $0$인 변수라고 하자. 그러면 $X_i\sim\operatorname{Bernoulli}(0.5)$이다.

- 이때  

$$  
X=X_1+X_2,\qquad Y=X_2+X_3  
$$

- 또한  

$$  
E[X_i]=\frac{1}{2},\qquad \operatorname{Var}(X_i)=\frac{1}{4}  
$$  
이다.

- 따라서 공분산의 성질 2를 이용하면  

$$  
\operatorname{Cov}(X,Y)=\operatorname{Cov}(X_1+X_2,;X_2+X_3)  
$$  

$$  
=\operatorname{Cov}(X_1,X_2)+\operatorname{Cov}(X_1,X_3)+\operatorname{Cov}(X_2,X_2)+\operatorname{Cov}(X_2,X_3)  
$$

#### Solution
- 서로 다른 동전 던지기들은 독립이므로  

$$  
\operatorname{Cov}(X_1,X_2)=\operatorname{Cov}(X_1,X_3)=\operatorname{Cov}(X_2,X_3)=0  
$$  
- 따라서 $\operatorname{Cov}(X,Y)$의 식에서 0이 아닌 항은 하나뿐이다. 

$$  
\operatorname{Cov}(X,Y)=\operatorname{Cov}(X_2,X_2)  
$$

- 공분산의 성질 3에 의해  

$$  
\operatorname{Cov}(X_2,X_2)=\operatorname{Var}(X_2)  
$$  

$$  
\operatorname{Cov}(X,Y)=\operatorname{Var}(X_2)=\frac{1}{4}  
$$

#### Example (공분산이 0이라고 해서 독립은 아니다.)
- $X$가 다음 값을 각각 확률 $\frac{1}{5}$로 가진다고 하자.  

$$  
-2,-1,0,1,2  
$$

- 그리고  

$$  
Y=X^2  
$$  
라고 하자.

- $\operatorname{Cov}(X,Y)=0$이지만 $X$와 $Y$는 독립이 아님을 보여라.

- 해설

- 먼저 결합확률표를 만들면 다음과 같다.


|$X \backslash Y$|$0$|$1$|$4$|
|---|---|---|---|
|$-2$|$0$|$0$|$\frac{1}{5}$|
|$-1$|$0$|$\frac{1}{5}$|$0$|
|$0$|$\frac{1}{5}$|$0$|$0$|
|$1$|$0$|$\frac{1}{5}$|$0$|
|$2$|$0$|$0$|$\frac{1}{5}$|

- 주변분포로부터 평균은  

$$  
E[X]=0,\qquad E[Y]=2  
$$  
이다.



#### Solution
- 다음으로 $X$와 $Y$가 독립이 아님을 보이자.
- 이를 위해서는 곱셈법칙이 성립하지 않는 경우를 하나만 찾으면 된다. 즉,  

$$  
p(x_i,y_j)\ne p_X(x_i)p_Y(y_j)  
$$  
인 경우를 찾으면 된다.

- 예를 들어  

$$  
P(X=-2,;Y=0)=0  
$$  
이지만  

$$  
P(X=-2)\cdot P(Y=0)=\frac{1}{5}\cdot\frac{1}{5}=\frac{1}{25}  
$$  
이다.

- 이 둘은 같지 않으므로 $X$와 $Y$는 독립이 아니다.
- 마지막으로 성질 4를 이용하여 공분산을 계산하면  

$$  
\operatorname{Cov}(X,Y)=E[XY]-\mu_X\mu_Y  
$$

- 여기서 $\mu_X=0$, $\mu_Y=2$이고,  

$$  
E[XY]=\frac{1}{5}(-8-1+0+1+8)=0  
$$  
이므로  

$$  
\operatorname{Cov}(X,Y)=0-0\cdot 2=0  
$$

- 따라서  

$$  
\operatorname{Cov}(X,Y)=0  
$$  
이지만, $X$와 $Y$는 독립이 아니다.

#### Discussion
- 이 예제는  $\operatorname{Cov}(X,Y)=0$  이라고 해서 $X$와 $Y$가 독립임을 의미하지는 않음을 보여준다.
	- 실제로 $X$와 $X^2$는 매우 강하게 의존한다.
	- 왜냐하면 $X$의 값을 알면 $X^2$의 값도 100% 확실하게 알 수 있기 때문이다.
- 핵심은 공분산 $\operatorname{Cov}(X,Y)$가 $X$와 $Y$ 사이의 선형 관계(linear relationship)를 측정한다는 점이다.
- 위 예제에서 $X$와 $X^2$는 이차 관계(quadratic relationship)를 가진다. 

$$  
Y=X^2  
$$

- 그러나 이러한 비선형 관계는 공분산으로는 완전히 포착되지 않을 수 있다.

- 두 변수의 관계가 선형이 아니면 둘의 관계를 정확히 측정할 수가 없음.


- 연속형 공분산도 같은 방식으로 작동하지만, 계산을 합(sum) 대신 적분(integral)으로 한다.

#### Examples (연속형 공분산)

- $X$와 $Y$가 단위정사각형 $[0,1]\times[0,1]$에서 정의된 결합확률변수이고, 결합 pdf가  

$$  
f(x,y)=2x^3+2y^3  
$$  
라고 하자.

- $f(x,y)$가 올바른 확률밀도함수임을 확인하여라.

- $\mu_X$와 $\mu_Y$를 계산하여라.

- 공분산  

$$  
\operatorname{Cov}(X,Y)  
$$  
을 계산하여라.


#### Solution 1
- 1. $f(x,y)$가 올바른 확률밀도함수인지 확인

- 올바른 pdf가 되려면 두 가지 조건을 만족해야 한다.

- $f(x,y)\ge 0$

- 전체 영역에서의 이중적분값이 $1$

- 음이 아닌 조건은 자명하다.  

$$  
f(x,y)=2x^3+2y^3\ge 0  
$$

- 이제 전체 적분을 계산하면  

$$  
\int_0^1\int_0^1 f(x,y),dx,dy=\int_0^1\int_0^1 (2x^3+2y^3),dx,dy  
$$

- 안쪽 적분:  

$$  
\int_0^1 (2x^3+2y^3),dx=\left[\frac{x^4}{2}+2xy^3\right]_0^1=\frac{1}{2}+2y^3  
$$

- 바깥 적분:  

$$  
\int_0^1 \left(\frac{1}{2}+2y^3\right),dy=\left[\frac{y}{2}+\frac{y^4}{2}\right]_0^1=1  
$$

- 따라서 전체 확률은 $1$이므로 $f(x,y)=2x^3+2y^3$는 올바른 결합확률밀도함수이다.
- 참고: 마지막 문장의 $f(x,y)=x+y$는 오타이고, 올바른 식은 $f(x,y)=2x^3+2y^3$이다.



#### Solution 2
- 평균을 구하려면 적분을 계산해야 한다.

- 여기서는 적분식만 쓰고, 계산 과정은 생략한다.

- 또한 대칭성에 의해 두 평균은 같다는 것도 알 수 있다.


$$  
\mu_X=\int_0^1\int_0^1 x f(x,y)\,dx\,dy  
=\int_0^1\int_0^1 x(2x^3+2y^3)\,dx\,dy  
=\int_0^1\int_0^1 (2x^4+2xy^3)\,dx\,dy  
=\frac{13}{20}  
$$

$$  
\mu_Y=\int_0^1\int_0^1 y f(x,y)\,dx\,dy  
=\int_0^1\int_0^1 y(2x^3+2y^3)\,dx\,dy  
=\int_0^1\int_0^1 (2x^3y+2y^4)\,dx\,dy  
=\frac{13}{20}  
$$


#### Solution 3
- 3. 공분산은 다음과 같이 정의된다. 

$$  
\operatorname{Cov}(X,Y)=E[(X-\mu_X)(Y-\mu_Y)]  
$$

- 따라서 이는 적분으로 계산된다. 여기서도 적분식만 쓰고, 계산 과정의 자세한 전개는 생략한다. 

$$  
\operatorname{Cov}(X,Y)=\int_0^1\int_0^1 \left(x-\frac{13}{20}\right)\left(y-\frac{13}{20}\right)f(x,y)\,dx\,dy  
$$  

$$  
=\int_0^1\int_0^1 \left(x-\frac{13}{20}\right)\left(y-\frac{13}{20}\right)(2x^3+2y^3)\,dx\,dy  
=-\frac{9}{400}  
$$

- 참고로 원문 두 번째 적분식의 $\frac{7}{12}$는 앞에서 구한 평균과 일치하지 않으므로 오타이고, 올바르게는 $\frac{13}{20}$이어야 한다.



- 이 분포에서 생성한 의사난수 표본(pseudo-random samples)의 산점도(plot)는 다음과 같다.
- 또한 더 극단적인 밀도함수(extreme density function)를 사용한 경우의 그래프도 함께 제시한다.

### Correlation
- 공분산 $\operatorname{Cov}(X,Y)$의 단위는 ‘$X$의 단위 $\times$ $Y$의 단위’이다.
- 따라서 공분산의 크기를 직접 비교하기는 어렵다.
- 예를 들어 측정 단위를 바꾸면 공분산 값도 함께 변한다.
- 상관계수(correlation)는 공분산에서 이러한 척도(scale)의 영향을 제거한 값이다.
#### Definition
- $X$와 $Y$ 사이의 상관계수(correlation coefficient)는 다음과 같이 정의된다. 

$$  
\operatorname{Cor}(X,Y)=\rho=\frac{\operatorname{Cov}(X,Y)}{\sigma_X\sigma_Y}  
$$


- 단위의 문제로 공분산은 서로 비교하기 어려운 경우가 생길 수 있음.
- 둘의 관계만 보기위해서 공분산을보는건 조금 적합하지 않음
- 그래서 scale을 제거한 값인 Correlation을 사용하는게 적합

#### Properties of correlation
- Properties 1. $\rho$는 $X$와 $Y$를 표준화(standardization)한 뒤의 공분산이다.
- Properties 2. $\rho$는 단위가 없다(dimensionless).
	- 비율(ratio)이기 때문이다.
	- 유닛(단위)를 갖지 않음 단순한 비율임.
- Properties 3. 항상  $-1\le \rho \le 1$을 만족한다.
	- 또한    $\rho=1$ 인 것은 오직  $Y=aX+b,\quad a>0$ 인 경우와 정확히 일치한다.
	- 그리고  $\rho=-1$인 것은 오직  $Y=aX+b,\quad a<0$인 경우와 정확히 일치한다.
- Properties 3은 $\rho$가 변수들 사이의 선형 관계(linear relationship)를 측정함을 보여준다.
	- 상관계수가 양수이면, $X$가 클 때 $Y$도 큰 경향이 있다.
	- 상관계수가 음수이면, $X$가 클 때 $Y$는 작은 경향이 있다.
- 앞의 “공분산이 0이라고 해서 독립은 아니다” 예제는, 상관계수 역시 고차의 비선형 관계를 완전히 놓칠 수 있음을 보여준다.


#### Proof. (Property 3 of correlation)
- 먼저 분산은 항상 $0$ 이상이므로  

$$  
0\le \operatorname{Var}\left(\frac{X}{\sigma_X}-\frac{Y}{\sigma_Y}\right)  
$$
- 분산 공식을 적용하면  

$$  
=\operatorname{Var}\left(\frac{X}{\sigma_X}\right)+\operatorname{Var}\left(\frac{Y}{\sigma_Y}\right)-2\operatorname{Cov}\left(\frac{X}{\sigma_X},\frac{Y}{\sigma_Y}\right)  
$$

- 표준화된 변수의 분산은 $1$이므로  

$$  
=1+1-2\rho  
=2-2\rho  
$$

- 따라서  

$$  
0\le 2-2\rho  
$$  
이므로  

$$  
\rho\le 1  
$$

- 마찬가지로  

$$  
0\le \operatorname{Var}\left(\frac{X}{\sigma_X}+\frac{Y}{\sigma_Y}\right)  
$$  
를 이용하면  

$$  
-1\le \rho  
$$

- 결국  

$$  
-1\le \rho\le 1  
$$

- 이제 $\rho=1$이라면  

$$  
0=\operatorname{Var}\left(\frac{X}{\sigma_X}-\frac{Y}{\sigma_Y}\right)  
$$

- 분산이 $0$이면 확률변수는 상수이므로  
$$  
\frac{X}{\sigma_X}-\frac{Y}{\sigma_Y}=c  
$$  
인 어떤 상수 $c$가 존재한다.


- 선형일때만 성립.


#### Example

- 공정한 동전을 3번 던진다.
- $X$를 처음 2번 던짐에서 나온 앞면의 개수, $Y$를 마지막 2번 던짐에서 나온 앞면의 개수라고 하자.
- 즉, 가운데 던짐 결과가 두 변수에 공통으로 포함된다.
- $\operatorname{Cor}(X,Y)$를 구하여라.

#### Solution
- 상관계수는 공분산을 표준편차의 곱으로 나눈 값이다.  
$$  
\operatorname{Cor}(X,Y)=\frac{\operatorname{Cov}(X,Y)}{\sigma_X\sigma_Y}  
$$

- 앞에서 구한 값은  
$$  
\operatorname{Cov}(X,Y)=\frac{1}{4}  
$$  
이다.

- 또한 $X=X_1+X_2$이고 각 $X_i\sim\operatorname{Bernoulli}(0.5)$이므로  
$$  
\operatorname{Var}(X)=2\operatorname{Var}(X_i)=2\cdot\frac{1}{4}=\frac{1}{2}  
$$

- 따라서  
$$  
\sigma_X=\sqrt{\frac{1}{2}}=\frac{1}{\sqrt{2}}  
$$

- 같은 이유로  
$$  
\sigma_Y=\frac{1}{\sqrt{2}}  
$$

- 이제 대입하면  
$$  
\operatorname{Cor}(X,Y)=\frac{\frac{1}{4}}{\left(\frac{1}{\sqrt{2}}\right)\left(\frac{1}{\sqrt{2}}\right)}  
$$


$$  
=\frac{\frac{1}{4}}{\frac{1}{2}}=\frac{1}{2}  
$$

- 따라서  
$$  
\operatorname{Cor}(X,Y)=\frac{1}{2}  
$$


#### Example
- 공정한 동전을 3번 던진다.
- $X$를 처음 2번 던짐에서 나온 앞면의 개수, $Y$를 마지막 2번 던짐에서 나온 앞면의 개수라고 하자.
- 즉, 가운데 던짐 결과가 두 변수에 공통으로 포함된다.
- $\operatorname{Cor}(X,Y)$를 구하여라.
#### Solution
- 앞에서 계산한 결과  
$$  
\operatorname{Cor}(X,Y)=\frac{1}{2}  
$$  

- 이는 양의 상관관계(positive correlation)를 의미한다.
- 즉, $X$가 클수록 $Y$도 큰 경향이 있고, $X$가 작을수록 $Y$도 작은 경향이 있다.
- 여기서 이런 현상이 나타나는 이유는 두 번째 던짐 결과가 $X$와 $Y$ 모두에 포함되기 때문이다.
- 따라서 두 번째 던짐이 앞면이면 두 변수의 값이 함께 커지고, 뒷면이면 함께 작아진다.

#### Example (Continuous covariance.
- $X$와 $Y$가 단위정사각형 $[0,1]\times[0,1]$에서 정의된 결합확률변수이고, 결합 pdf가  $f(x,y)=2x^3+2y^3$일때, 상관계수 $\operatorname{Cor}(X,Y)$를 구하라  

#### Solution
- 상관계수는 다음과 같이 정의된다.  
$$  
\operatorname{Cor}(X,Y)=\frac{\operatorname{Cov}(X,Y)}{\sigma_X\sigma_Y}  
$$

- 앞에서 구한 값은  
$$  
\operatorname{Cov}(X,Y)=-\frac{9}{400}  
$$


$$  
\operatorname{Var}(X)=\frac{31}{400}  
$$

- 따라서  
$$  
\sigma_X=\sqrt{\frac{31}{400}}=\frac{\sqrt{31}}{20}\approx 0.28  
$$

- 대칭성에 의해  
$$  
\operatorname{Var}(Y)=\frac{31}{400}  
$$


$$  
\sigma_Y=\frac{\sqrt{31}}{20}\approx 0.28  
$$

- 이제 대입하면  
$$  
\operatorname{Cor}(X,Y)=\frac{-\frac{9}{400}}{\left(\frac{\sqrt{31}}{20}\right)\left(\frac{\sqrt{31}}{20}\right)}  
=\frac{-\frac{9}{400}}{\frac{31}{400}}  
=-\frac{9}{31}  
\approx -0.29  
$$


$$  
\operatorname{Cor}(X,Y)=-\frac{9}{31}\approx -0.29  
$$

- 코릴레이션으로 보면 -1~1사이니까 -0.29면 어느정도인지 감이 옴.


### Bivariate normal distributions
- Bivariate: 변수가 2개 있는 것.
	- uni: 는 변수가 1개
- 이변량 정규분포(bivariate normal distribution)의 밀도함수는 다음과 같다.  
$$  
f(x,y)=\frac{\exp\left(-\frac{1}{2(1-\rho^2)}\left[\frac{(x-\mu_X)^2}{\sigma_X^2}+\frac{(y-\mu_Y)^2}{\sigma_Y^2}-\frac{2\rho(x-\mu_X)(y-\mu_Y)}{\sigma_X\sigma_Y}\right]\right)}{2\pi\sigma_X\sigma_Y\sqrt{1-\rho^2}}  
$$

- 이 분포에서는 $X$와 $Y$의 주변분포가 모두 정규분포이다.
- 또한 $X$와 $Y$ 사이의 상관계수는 $\rho$이다.

- x 에 대해 적분하면 마지널 디스트리부션이 나옴.

- 아래 그림들은 여러 값의 $\rho$에 대해 이변량 정규분포를 시뮬레이션한 결과이다.
	- 각 변수 $X$와 $Y$는 개별적으로 표준정규분포를 따른다.  
	- $\mu_X=\mu_Y=0,\qquad \sigma_X=\sigma_Y=1$
	- 그림들은 생성된 표본들의 산점도(scatter plot)를 보여준다.
- 이 그림들과 다음 예시는 상관계수의 중요한 특징을 보여준다.
	- 데이터를 네 개의 사분면으로 나누기 위해, $x$축과 $y$축에서 각각 평균 위치에 수직선과 수평선을 그린다.
	- 양의 상관관계(positive correlation)는 데이터가 주로 제1사분면과 제3사분면에 모이는 경향을 의미한다.
	- 즉, $X$가 평균보다 크면 $Y$도 평균보다 크고, $X$가 평균보다 작으면 $Y$도 평균보다 작은 경우가 많다.
	- 음의 상관관계(negative correlation)는 데이터가 주로 제2사분면과 제4사분면에 모이는 경향을 의미한다.
	- 즉, 한 변수는 평균보다 크고 다른 변수는 평균보다 작은 경우가 많다.
	- 또한 $|\rho|$가 $1$에 가까워질수록 데이터는 점점 하나의 직선 주변에 모이게 된다.








### Overlapping uniform distributions
- 다음 시뮬레이션 상황을 고려하자.
	- $X_1,X_2,\dots,X_{20}$은 서로 독립이고 동일분포(i.i.d.)이며, 각각 균등분포 $U(0,1)$를 따른다.
	- $X$와 $Y$는 각각 여러 개의 $X_i$를 더한 합(sum)으로 정의된다.
	- $X$와 $Y$에 공통으로 포함되는 $X_i$의 개수를 overlap(겹침 수)라고 부른다.
- 아래 그림의 표기는 각 합에 사용된 변수의 개수와 overlap의 개수를 나타낸다.
	- 예를 들어 $5,3$은 다음을 의미한다.
	- $X$와 $Y$가 각각 5개의 $X_i$의 합이다.
	- 그중 3개의 $X_i$가 두 합에 공통으로 포함된다.
	- 데이터는 난수 생성으로 시뮬레이션되었다.
- 공분산의 선형성(linearity of covariance)을 이용하면 이론적인 상관계수(theoretical correlation)를 쉽게 계산할 수 있다.
	- 각 그림에는 다음 두 값이 함께 제시된다.
	- 이론적 상관계수
	- 시뮬레이션 표본으로부터 계산한 상관계수

- uniform distributions도 동일한 성질을 볼 수 있음.
- overlap은 $X$와 $Y$에 공통으로 포함되는 $X_i$의 개수








## Comment
다음주 부터는 통계 수업으로 넘어감.
중간고사는 없고 다음주 수업 진행함.

