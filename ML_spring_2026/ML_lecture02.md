2026-03-17 08:20
## 2강

### Linear Discriminative Models
- 입력 x → 출력 y의 조건부 확률 P(y∣x)를 직접 모델링하면서, 결정 경계(decision boundary)가 선형(linear)인 모델
- Discriminative 모델: P(y∣x)를 직접 모델링
- Generative 모델: P(x,y) (참고 P(x,y)=P(x∣y)P(y) ) 또는P(x∣y)를 모델링
- 기계 학습을 여러개 다룰 것
	- 초반 6주 정도는 지도학습
	- 지도 학습에서도 간단한 (그래도 수학은 많이 있음) 선형 모델을 다루혀 함.
	- 선형 중에서도 회귀와 분류 모델델


### Supervised Learning
- 지도학습(Supervised learning)은 입력-출력 쌍으로 이루어진 레이블된 데이터셋을 사용하여 계산 모델을 학습시키는 머신러닝의 한 분야이다.  
- 모델은 입력 데이터(특징)를 원하는 출력(타깃)에 매핑하는 함수를 학습하는 것이 과제이며, 궁극적인 목적은 보지 못한 새로운 데이터에 대해서도 정확한 예측을 수행하는 것이다.
- Lable이 있으면 지도 학습 없으면 비지도 학습
- 인풋과 아웃풋이 pairs인게 지도 학습
	- 집값 모델이면 렌트비용이 lable 나머지가 x 즉 피쳐
- x->function(learning algorithm)->y 로 가는 함수를 구하는게 ML


- 지도학습 문제는 일반적으로 분류와 회귀라는 두 가지 주요 범주로 나뉜다.
- 분류는 범주가 알려진 데이터로 구성된 학습 데이터를 바탕으로, 새로운 관측치가 어떤 범주 또는 클래스에 속하는지를 판단하는 것을 목표로 한다.
- 반면 회귀는 입력 특징과 타깃 변수 간의 관계를 학습하여 연속적인 수치 값을 예측하는 데 초점을 둔다.
- 리그레션은 연속적인 값.
- 분류는 카테고리나 클래스 자료.

- 분류와 회귀는 예측하는 출력의 형태는 다르지만, 두 문제 모두 데이터에서 패턴을 찾아 신뢰할 수 있는 예측을 수행하는 것을 공통된 목표로 가진다. 
- 이러한 관계를 모델링하는 효과적인 방법 중 하나는 결정 함수를 단순하고 구조적인 형태로 가정하는 것이다.
- 선형 판별 모델은 이 함수가 입력 특징에 대해 선형이라고 가정하며, 이로 인해 이해하기 쉽고 실제 적용에서도 효과적인 특성을 가진다.
- 관계 추론은 다양한 방법이 있음
	- 선형이 제일 단순한 모델임
	- 쉽고 빠르게 적용 할 수 있음.
	- 분류에서는 디시전 라인, 회귀에서는 관계 라인을 찾음


### Linear Regression
- 연속적인 값을 출력하는 회귀 문제부터 시작한다. 이 설정에서 선형 판별 모델은 예측을 위해 단순한 함수 형태를 가정한다.  
- 지도학습을 수행하기 위해 가설 f를 입력 특징에 대한 선형 함수로 설정하며, $x_0 = 1$ 절편(intercept) 항을 의미한다:  
- $y = f(\mathbf{x}) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \cdots + \theta_d x_d$
- 선형 함수라고 하면 y에 웨이트를 곱해서 계산
- with $𝑥_0 = 1$ denoting the intercept 이유(x0의 절편을 1로 두는 이유)
	- 그래야 $θ_0$ = 모든 입력 $x_1, \dots, x_d$가 0일 때의 기본값  
		→ 즉, 그래프에서 y축과 만나는 값 (baseline)이 생성
	- 쉽게 말하면 $𝑥_0 = 1$ 이여야 $\theta_0$가 값을 유지
	- 그래야 이렇게 식을 쓸 수 있고 $y = f(\mathbf{x}) = \theta_0 x_0 + \theta_1 x_1 + \theta_2 x_2 + \cdots + \theta_d x_d$ (단, x0=1)
	- 이렇게 하면 전체를 하나로 묶을 수 있음: $y = \boldsymbol{\theta}^T \mathbf{x}$

- x 아래첨자는 피쳐 디멘전 (feature dimension), 서브스크립트 (subscript) 이라고 함.
	- 피쳐 디멘전 (feature dimension)
		- 입력 데이터가 가진 특징(feature)의 개수
		- $\mathbf{x} = (x_1, x_2, x_3)$
		- feature dimension = 3
	- 서브스크립트 (subscript)
	- 변수에 붙는 아래 첨자(index)로, “몇 번째 요소인지”를 나타내는 표시
	- $x_1, x_2, \dots, x_d$
	- 즉, “순서/위치 표시용 번호”

- $y = f(\mathbf{x}) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \cdots + \theta_d x_d$ 이런식은 element 곱 형태라고 함.
- x,y는 값을 알고 있음 𝜃를 구하는 것이 우리 목표


- 이렇게 벡터 형태로 수식을 작성 할 수도 있음
- $\displaystyle f(x) = \sum_{i=0}^{d} \theta_i x_i=\boldsymbol{\theta}^t \boldsymbol{x}$
- 여기서 d는 입력 변수의 개수를 의미하고, x는 특징 벡터를 나타내며, 𝜃는 함수 f의 파라미터 집합을 의미한다.





- 이제 모델 $f(\mathbf{x}) = \boldsymbol{\theta}^T \mathbf{x}$를 정의했으므로, 다음 단계는 파라미터 $\boldsymbol{\theta}$를 어떻게 선택할 것인지 결정하는 것이다.  
- 입력-출력 쌍 $(\mathbf{x}^{(i)}, y^{(i)})$로 이루어진 학습 데이터가 주어졌다고 가정하자.  
- 어떤 파라미터를 선택하더라도 모델은 예측값 $f(\mathbf{x}^{(i)})$을 생성하지만, 일반적으로 이 값은 실제 값 $y^{(i)}$와 정확히 일치하지는 않는다.


- 특정 파라미터 선택을 평가하는 자연스러운 방법은 예측값이 실제 값에 얼마나 가까운지를 살펴보는 것이다.  
- 예측값과 해당 실제 값 사이의 차이를 잔차(residual)라고 한다.  
- 이 차이가 작으면 모델이 잘 작동하는 것이고, 크면 모델의 성능이 좋지 않음을 의미한다.
- 파라메터 𝜃를 구하는 것이 regression 문제를 푸는 것.
- x위의 지수는 슈퍼스크립트
	- $x^i$ :i가 슈퍼스크립
- 좋은 모델을 만드는 가장 쉬운 방법은 실제값과의 차이 residual이용.

#### 참고_슈퍼스크립과 서브스크립 의미
1. $x^{(i)}$ : 데이터 인덱스 (샘플 번호)
    - 의미: **i번째 데이터(샘플)**    
    - 예:    
        $x^{(1)}, x^{(2)}, \dots, x^{(n)}$
    - 전체 데이터 중에서“몇 번째 관측값인지”를 나타냄
2. $x_i$ : 벡터의 요소 (feature index)
    - 의미: **i번째 feature (변수)**    
    - 예:    
        $\mathbf{x} = (x_1, x_2, \dots, x_d)$
    - 하나의 데이터 안에서  “몇 번째 변수인지”를 나타냄
3. 예시
    | 샘플  | 키   | 몸무게 |
    | --- | --- | --- |
    | 1번  | 170 | 65  |
    | 2번  | 180 | 75  |
    - $x^{(1)}$ = (170, 65) → 1번 사람 전체 데이터    
    - $x_1$ = 키    
    - $x^{(2)}_1$ = 180 → 2번 사람의 키
4. 정리
    - $x^{(i)}$ → **데이터 번호 (행)** 
        - “몇 번째 데이터”
    - $x_i$ → **feature 번호 (열)**
        - “몇 번째 변수”

- 하나의 데이터만으로는 모델의 성능을 평가하기에 충분하지 않으며, 대신 모든 학습 데이터에 대해 잔차를 종합하여 전체 오차를 평가해야 한다.  
- 회귀 문제에서 일반적으로 사용되는 방법은 최소제곱오차(least mean squares, 또는 squared error) 함수이다:  
$\displaystyle J(\boldsymbol{\theta}) = \frac{1}{2} \sum_{i=1}^{n} \left( f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) - y^{(i)} \right)^2$


- 이 함수는 비용 함수(cost function) 또는 목적 함수(objective function)라고 하며, 머신러닝에서 중심적인 역할을 한다.  
- 이 함수는 특정한 파라미터 θ\boldsymbol{\theta}θ 선택이 관측된 데이터를 얼마나 잘 설명하는지를 정량적으로 나타낸다.  
- 보다 정확하게는, 우리의 목표는 비용 함수를 최소화하는 파라미터 벡터 $\boldsymbol{\theta}$를 찾는 것이다:  
$\displaystyle\boldsymbol{\theta}^* = \arg\min_{\boldsymbol{\theta}} J(\boldsymbol{\theta})$
- 여기서 $\boldsymbol{\theta}^∗$는 가능한 한 가장 작은 비용을 달성하는 최적의 파라미터를 의미한다.
- 데이터 하나의 차이를 구하는게 아니라 데이터 전체의 차이를 구하는 것이 중요함.
- 함수 값과 실제 값의 차이의 제곱을 더한 것을 $J(𝜃)$
- 이 J값을 코스트 func. or objective func.이라고 함.
- $J(𝜃)$의 최소값을 찾는게 목표고 이때의 $𝜃$는 $𝜃^*$ 라고 함.


- 학습 문제를 비용 함수를 최소화하는 문제로 정식화했으므로, 다음 질문은 실제로 최적의 파라미터 $\boldsymbol{\theta}$를 어떻게 찾을 것인가이다.
- 𝜃값을 가장 작게 구하는 방법
	1. **경사하강법(Gradient descent)**: 비용 함수를 최소화하기 위해 $boldsymbol{\theta}$를 반복적으로 업데이트하는 최적화 알고리즘이다. 
		- 딥러닝도 같은 방법으로 적용 됨.
  
	2. **해석적 해법(Analytical solution)**: 선형 방정식 시스템을 풀어 $\boldsymbol{\theta}$에 대한 닫힌형 해(closed-form solution)를 제공한다.    
	3. **확률적 접근(Probabilistic approach)**: 문제를 통계적 추론의 관점에서 다루며, 일반적으로 오차가 정규분포를 따른다고 가정하고 최대우도추정(maximum likelihood estimation)을 사용한다.


- 경사하강법(Gradient descent)은 머신러닝과 딥러닝에서 가장 널리 사용되는 최적화 방법 중 하나이다.  
- 명시적인 해를 구하기 어렵거나 불가능한 경우에도 모델의 파라미터를 학습할 수 있는 실용적인 방법을 제공한다.
#### Gradient descent:
- 가장 많이 사용됨.
- 한번에 값을 찾기 힘들때 점진적으로 값을 찾아가는 과정
- Cost function을 파라메터 스페이스의 고차원 구조(3D)에 그릴 수 있음
	- x,y는 $\theta$, z축은 cost로 그래프를 그릴 수 있음.
- 이 min 값을 찾는 방법 중 대표적인게 경사 하강법임.


- 비용 함수를 어떻게 최소화하는지 이해하기 위해서는 이를 기하학적으로 생각해보는 것이 도움이 된다. 
- 비용 함수 $J(\boldsymbol{\theta})$는 파라미터 공간 위에 정의된 하나의 곡면으로 볼 수 있다.
- 단순한 경우 이 곡면은 곡선 형태의 그릇(bowl)과 유사한 모양을 가진다.
- 우리의 목표는 이 곡면에서 가장 낮은 지점을 찾는 것이며, 이는 최소 비용에 해당하고 따라서 최적의 파라미터를 의미한다.


- 경사하강법은 이 문제를 반복적인 방식으로 해결한다.
- 곡면 위의 어떤 지점에서든, 비용이 가장 빠르게 증가하는 방향을 나타내는 기울기(gradient)를 계산할 수 있다.
- 비용을 줄이기 위해서는 이와 반대 방향, 즉 아래쪽 방향으로 이동한다.
- 이 과정을 반복적으로 수행하면 비용이 점차 감소하며, 결국 최소값에 수렴하게 된다.

- Gradient(경사)에 대해 알아야 함.
- ML이나 함수 구조를 이해하려면 선형대수, 경사를 이해하려면 미적분이 필요
- Gradient는 기울기임.
	- 최저 코스트의 weight기준(기울기가 min또는 0)으로 왼쪽은 기울기가 음수, 오른쪽은 기울기가 양수

- 형식적으로, 경사하강법은 초기값 $\boldsymbol{\theta}$에서 시작하여 다음과 같은 업데이트를 반복적으로 수행한다:  
$\displaystyle\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\boldsymbol{\theta})$
- 여기서 $\alpha$는 학습률(learning rate)을 의미한다.
- 학습률이 크면 최소값으로 더 빠르게 이동할 수 있지만, 최솟값을 지나쳐버릴 위험이 있다. 반대로 학습률이 작으면 업데이트가 더 점진적으로 이루어지며, 수렴하는 데 더 많은 반복이 필요할 수 있다.

- 현재 𝜃값에서 -값을 빼서 최적의 cost를 구할 수 있음
- $\alpha$:  learning rate
	-  learning rate가 너무 크면 그래프를 벗어남.
	- 작으면 너무 계산이 오래 걸림.



단순화를 위해 하나의 학습 데이터 $(x, y)$만 있는 경우를 먼저 살펴보자. 이 경우 J의 정의에서 합(sum)을 생략할 수 있다.

$$
\begin{aligned}\displaystyle\frac{\partial}{\partial \theta_j} J(\boldsymbol{\theta}) &= \frac{\partial}{\partial \theta_j} \frac{1}{2} \left( f_{\boldsymbol{\theta}}(\mathbf{x}) - y \right)^2\\
\\
&= 2 \cdot \frac{1}{2} \left( f_{\boldsymbol{\theta}}(\mathbf{x}) - y \right) \cdot \frac{\partial}{\partial \theta_j} \left( f_{\boldsymbol{\theta}}(\mathbf{x}) - y \right)\\
\\
&= \left( f_{\boldsymbol{\theta}}(\mathbf{x}) - y \right) \cdot \frac{\partial}{\partial \theta_j} \left( \sum_{i=0}^{d} \theta_i x_i - y \right)\\
\\
&=(fθ(x)−y)x_j\end{aligned}
$$

- 단순하지만 파워풀
- 인공신경망에서도 잘 적용됨.
- 시험문제에 수학 풀이를 출제 하진 않음.

- 따라서 하나의 학습 데이터에 대해서는 다음과 같은 업데이트 규칙을 얻는다:  
	$\theta_j := \theta_j - \alpha \left( f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) - y^{(i)} \right) x_j^{(i)}$

- 아래 식은 여러 학습 데이터를 모두 반영하여 업데이트를 수행하는 경우이다:  
	$\displaystyle\theta_j := \theta_j - \alpha \sum_{i=1}^{n} \left( f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) - y^{(i)} \right) x_j^{(i)}$
- 따라서 회귀 문제는 경사하강법을 반복적으로 적용하여 파라미터를 조정함으로써 비용 함수를 최소화하는 방식으로 해결할 수 있다.




- 경사하강법은 반복적인 과정을 통해 비용 함수 $J(\boldsymbol{\theta})$를 최소화하는 하나의 방법을 제공한다.  
- 그러나 선형 회귀의 경우에는 반복적인 업데이트 없이도 최적의 파라미터를 직접 구할 수 있다.  
- 이는 선형 회귀에서 사용되는 비용 함수가 매끄럽고(smooth), 연속적이며(continuous), 볼록(convex)하기 때문에 하나의 전역 최소값(global minimum)을 가지기 때문이다.



- 이 대안적 접근에서는 각 파라미터 $\theta_j$에 대해 비용 함수 $J(\boldsymbol{\theta})$를 미분한 뒤, 그 값을 0으로 두어 최소값을 구한다.  
- 함수의 최소점에서는 기울기(또는 그래디언트)가 0이 되므로, 이러한 방정식을 푸는 것을 통해 비용을 최소화하는 파라미터 값을 찾을 수 있다.  
- 비용 함수가 $\boldsymbol{\theta}$에 대해 이차식(quadratic)이기 때문에, 이 과정은 닫힌형 해(closed-form solution)를 제공한다.

- 간단하게 2차식이나 최소값이 딱 하나 존재 (convex) 경우는 경사하강법을 쓸 필요 없이 gradient가 0이 되는 지점을 찾으면 됨.



#### 행렬으로 풀이
- 이를 형식적으로 표현하기 위해 다음과 같이 정의한다.  
- $\mathbf{X}$를 $n \times d$ 행렬로 두고, 각 행은 하나의 학습 데이터에 대한 특징 값을 포함한다고 하자. 또한 $\mathbf{y}$는 학습 데이터의 모든 타깃 값을 포함하는 n차원 벡터이다:

$$\mathbf{X} = \begin{bmatrix} (\mathbf{x}^{(1)})^T \\ \vdots \\ (\mathbf{x}^{(n)})^T \end{bmatrix}, \quad \mathbf{y} = \begin{bmatrix} y^{(1)} \\ \vdots \\ y^{(n)} \end{bmatrix}$$

이 표기법을 사용하면 비용 함수는 다음과 같이 더 간결하게 표현할 수 있다:

$$\displaystyle J(\boldsymbol{\theta}) = \frac{1}{2} (\mathbf{X}\boldsymbol{\theta} - \mathbf{y})^T (\mathbf{X}\boldsymbol{\theta} - \mathbf{y})$$



비용 함수 $J$를 최소화하기 위해서는 $\boldsymbol{\theta}$에 대해 미분한 뒤, 그 값을 0으로 두어야 한다:

$$
\begin{aligned}\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})&= \nabla_{\boldsymbol{\theta}} \frac{1}{2} (\mathbf{X}\boldsymbol{\theta} - \mathbf{y})^T (\mathbf{X}\boldsymbol{\theta} - \mathbf{y})\\
&= \frac{1}{2} \nabla_{\boldsymbol{\theta}} \left( \boldsymbol{\theta}^T \mathbf{X}^T \mathbf{X} \boldsymbol{\theta}- \mathbf{y}^T \mathbf{X} \boldsymbol{\theta} - \mathbf{y}^T \mathbf{X} \boldsymbol{\theta}- \mathbf{y}^T \mathbf{y} \right)\\  
&= \frac{1}{2} \nabla_{\boldsymbol{\theta}} \left( \boldsymbol{\theta}^T \mathbf{X}^T \mathbf{X} \boldsymbol{\theta}- 2 (\mathbf{X}^T \mathbf{y})^T \boldsymbol{\theta} \right)\\
&= \frac{1}{2} \left( 2 \mathbf{X}^T \mathbf{X} \boldsymbol{\theta} - 2 \mathbf{X}^T \mathbf{y} \right)\\
&= \mathbf{X}^T \mathbf{X} \boldsymbol{\theta} - \mathbf{X}^T \mathbf{y}=0\\
\\
∴ \mathbf{X}^T \mathbf{X} \boldsymbol{\theta} &= \mathbf{X}^T \mathbf{y}
\end{aligned}
$$


- $\boldsymbol{\theta}$를 구하기 위해서는 양변을 $\mathbf{X}^T \mathbf{X}$로 “나누는” 것이 필요하다.
- 행렬 대수에서는 이는 $\mathbf{X}^T \mathbf{X}$의 역행렬을 곱하는 것으로 수행된다. 이 과정은 $\mathbf{X}^T \mathbf{X}$가 가역(invertible)일 때만 가능하며, 이는 직관적으로 해당 행렬이 모델 파라미터를 유일하게 결정할 수 있을 만큼 충분히 독립적인 정보를 포함하고 있음을 의미한다.
	$\boldsymbol{\theta} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$
- 이 식은 경사하강법과 같은 반복적인 방법 없이도 문제를 직접적으로 해결할 수 있는 해석적 해(analytic solution)를 제공한다.

- 실제 상황에서는 일부 특징들이 중복되거나 강하게 상관되어 있을 경우 $\mathbf{X}^T \mathbf{X}$가 가역이 아닐 수 있다. 이러한 경우에는 정규화(regularization)나 유사역행렬(pseudoinverse)과 같은 대안적인 방법을 사용할 수 있다.



#### probabilistic interpretation
- 선형 회귀를 통계적 추론 문제로 이해할 수 있도록 확률적 해석을 제공할 수도 있다.  
- 이를 위해, 타깃 변수 $y^{(i)}$와 입력 $x^{(i)}$가 다음과 같은 관계를 따른다고 가정하자:
	$𝑦 ^𝑖 = 𝜽^𝑇𝒙 ^𝑖 + 𝜖 ^𝑖$ with $\epsilon^{(i)} \sim \mathcal{N}(0, \sigma^2)$
- 여기서 $\epsilon^{(i)}$는 모델이 설명하지 못한 효과나 무작위 잡음을 나타내는 오차항이다.
- 또한 이 오차항 $\epsilon^{(i)}$들은 서로 독립이고 동일한 분포를 따른다고 가정하며(IID), 평균이 0이고 분산이 $\sigma^2$인 가우시안(정규_Normal) 분포를 따른다고 가정한다.
- 확률론적 접근
	- 같은 문제를 확률적으로 풀이하는 방법
- y는 label, x는 인풋, i는 인덱스
- 확률에서는 앱실론을 추가함.
- y=𝜽x 식으로 쓰는데 현실데이터는 노이즈가 있음 그래서 앱실론을 더해 줘야 함.
- 그래서 $𝑦 ^𝑖 = 𝜽^𝑇𝒙 ^𝑖 + 𝜖 ^𝑖$
- 이때 노이즈는 정규 분포(N)를 따른다고 함.


- 이는 다음을 의미한다:
$y^{(i)} \sim \mathcal{N}(\boldsymbol{\theta}^T \mathbf{x}^{(i)}, \sigma^2)$
- 따라서 $y^{(i)}$가 관측될 우도(likelihood)는 다음과 같이 표현된다:  
$\displaystyle p\left(y^{(i)} \mid \mathbf{x}^{(i)}; \boldsymbol{\theta}\right) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left( - \frac{\left(y^{(i)} - \boldsymbol{\theta}^T \mathbf{x}^{(i)}\right)^2}{2\sigma^2} \right)$
- 이 식은 하나의 데이터 포인트에 대한 우도 함수를 정의한다.
- y도 정규분포를 따른다고 볼수 있음
- y라는 아웃풋이 정규분포를 따른다는 것은, 다양한 y 값들을 랜덤하게 뽑았을때 그 값들은 정규분포 모양을 형성함.
- 그래서 y 확률값은 정규분포식을 따른다.

- 이를 전체 데이터셋으로 확장하면 우도 함수(likelihood function)를 다음과 같이 정의할 수 있다:$L(\boldsymbol{\theta}) = p(\mathbf{y} \mid \mathbf{X}; \boldsymbol{\theta})$
- 오차항 $\epsilon^{(i)}$들이 서로 독립이라고 가정하면, 전체 우도 함수는 각 데이터의 우도의 곱으로 표현된다:

$$
\displaystyle L(\boldsymbol{\theta}) = \prod_{i=1}^{n} p\left(y^{(i)} \mid \mathbf{x}^{(i)}; \boldsymbol{\theta}\right)= \prod_{i=1}^{n} \frac{1}{\sqrt{2\pi}\sigma}  \exp\left(- \frac{\left(y^{(i)} - \boldsymbol{\theta}^T \mathbf{x}^{(i)}\right)^2}{2\sigma^2} \right)$$    

- 파라미터 $\boldsymbol{\theta}$를 추정하기 위해 최대우도추정(maximum likelihood estimation, MLE)의 원리를 적용한다.

- 이것도 여러가지 샘플에 확장하려면 i=1~n 까지 곱을 구해야 함. (확률문제기 때문)
	- $\displaystyle\prod_{i=1}^{n} a_i$
	- i=1부터 n까지 모든 값을 곱하라
- likelihood function라고함. (코스트, 오브젝트 펑션과 유사함.)
- 확률을 최대로 하는 파라미터를 찾는 것으로 문제가 바뀜
	- maximum likelihood estimation (MLE)를 찾는 것,
	- 미분모델에서는 weight가 최소가 되게, 확률에서는 likelihood가 최대가 되는 값을 찾음.

- 최대우도추정(MLE)의 핵심 아이디어는 단순하다: 주어진 모델 하에서 관측된 데이터가 가장 그럴듯하게 나타나도록 만드는 파라미터 값을 선택하는 것이다.  
- 즉, 가능한 모든 $\boldsymbol{\theta}$ 중에서 우도 함수 $L(\boldsymbol{\theta})$를 최대화하는 값을 선택한다:  
  $\displaystyle\boldsymbol{\theta}^* = \arg\max_{\boldsymbol{\theta}} L(\boldsymbol{\theta})$

- 우도 함수 $L(\boldsymbol{\theta})$를 직접 최대화하는 대신, 로그를 취한 로그우도(log-likelihood)를 최대화하는 것이 더 쉽다:

$$
\begin{aligned}\log L(\boldsymbol{\theta})  
&= \log \prod_{i=1}^{n} \frac{1}{\sqrt{2\pi}\sigma}  
\exp\left(- \frac{(y^{(i)} - \boldsymbol{\theta}^T \mathbf{x}^{(i)})^2}{2\sigma^2}\right)\\    
\\
&= \sum_{i=1}^{n} \log \left(  
\frac{1}{\sqrt{2\pi}\sigma}  
\exp\left(- \frac{(y^{(i)} - \boldsymbol{\theta}^T \mathbf{x}^{(i)})^2}{2\sigma^2}\right)\right)\\
\\
&= \sum_{i=1}^{n} \log \frac{1}{\sqrt{2\pi}\sigma}- \sum_{i=1}^{n} \log \exp\left(- \frac{(y^{(i)} - \boldsymbol{\theta}^T \mathbf{x}^{(i)})^2}{2\sigma^2}\right)\\
\\
&= n \log \frac{1}{\sqrt{2\pi}\sigma}- \frac{1}{2\sigma^2} \sum_{i=1}^{n} \left( y^{(i)} - \boldsymbol{\theta}^T \mathbf{x}^{(i)} \right)^2
\end{aligned}
$$

- log 값을 취하면 시그마로 수식이 변함.
- 계산이 용이 함.


- 따라서 $\log L(\boldsymbol{\theta})$를 최대화하는 것은 다음 식을 최소화하는 것과 동일한 결과를 낳는다:  
$\displaystyle\frac{1}{2} \sum_{i=1}^{n} \left( f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) - y^{(i)} \right)^2$
- 이 식은 우리가 앞서 정의한 비용 함수 $J(\boldsymbol{\theta})$, 즉 최소제곱 비용 함수와 동일하다.  
- 즉, 이는 최소제곱 기준(least-squares criterion)과 정확히 같은 식이다.  
- 따라서 앞서 가정한 확률적 모델 하에서는, 최소제곱 회귀를 수행하는 것이 $\boldsymbol{\theta}$의 최대우도추정(MLE)을 구하는 것과 동등하다.


- 최적의 파라미터 벡터 $\boldsymbol{\theta}$를 구한 후에는, 학습된 모델을 사용하여 새로운 보지 못한 데이터에 대해 예측을 수행할 수 있다.
- 새로운 입력 $x_{new}$ 가 주어지면, 예측값은 다음과 같이 간단히 계산된다:
      $f(x_{new}) = \boldsymbol{\theta}^T \mathbf{x}_{\text{new}}$
- 이와 같이 모델은 학습 데이터를 기반으로 일반화하여, 미래의 새로운 데이터에 대해서도 예측을 제공할 수 있다.
- 이렇게 그려진 선을 이용해 새로운 값을 예측할 수 있음.


### Logistic Regression and Binary Classification
- 분류 문제는 회귀 문제와 유사하지만, 한 가지 중요한 차이가 있다.  
- 회귀에서는 출력이 연속적인 값인 반면, 분류에서는 출력이 범주형 값이다.  
- 예를 들어, 이진 분류의 경우 출력은 0 또는 1의 두 가지 값만을 가진다.
- 분류는 y 값이 이산밸류, 카테고리 밸류임
	- 회귀는 연속적 밸류
- 예를 들어 기온 문제는 연속 값이기 때문에 회귀 문제임
- 하지만 기준을 주고 8도 이상이면 핫, 이하면 콜드 분류 문제로 바꿀 수 있음

- 처음에는 분류 문제가 단순히 연속적인 값 대신 클래스 라벨을 예측하는 회귀 문제처럼 보일 수 있다.  
- 그러나 이러한 유사성은 오해를 불러일으킬 수 있다. 회귀는 수치 값을 정확하게 추정하는 데 초점을 두는 반면, 분류는 입력을 올바른 범주에 할당하고 각 클래스에 대한 확률을 추정하는 데 목적이 있다.  
- 이러한 목적의 차이로 인해 분류 문제에서는 이에 특화된 모델과 손실 함수가 사용된다.
- 회귀와 분류는 거의 유사함.
- 미묘한 차이는 분류의 경우 어떤 클래스에 속할 확률을 구하는 것이 목표.
	- 회귀는 예상 값을 찾음.
- 그래서 cost func이 다르게 됨.

- 로지스틱 회귀(Logistic regression)는 입력이 주어졌을 때 출력 변수가 특정 클래스에 속할 확률을 모델링함으로써 이러한 문제를 해결한다.  
- 이를 위해 입력의 선형 결합에 시그모이드(sigmoid, 또는 로지스틱) 함수를 적용하여, 모든 실수 값을 \[0,1] 범위로 매핑하므로 확률을 모델링하는 데 적합하다:  
	$\displaystyle f_{\boldsymbol{\theta}}(\mathbf{x}) = g(\boldsymbol{\theta}^T \mathbf{x})= \frac{1}{1 + e^{-\boldsymbol{\theta}^T \mathbf{x}}}$
	- 여기서 $g(\cdot)$는 로지스틱 함수(시그모이드 함수)를 의미한다.
	- $g(\cdot)$ 기호의 $\cdot$ 자리에는 아무 입력이나 함수가 들어올 수 있음을 뜻함.

- output이 어떤 카테고리에 해당할 확률로 수식을 계산 해야 함.
- 대표적인게 sigmoid func.(logistic function이라고도 함.)
- y값을 0~1로 제한함. -> 확률적으로 바꿀 수 있음
	- 모든 확률은 0~1 사이
- g함수라고 씀
- Classification는 logistic regression이라고도 함.
	- 그 이유는 Classification를 회귀식을 이용해서 풀기 위해 logistic regression 이라함.



- 시그모이드 함수의 중요한 성질 중 하나는 그 미분이 간단한 형태를 가진다는 점이다:
  
$$\begin{aligned}g'(z) &= \frac{d}{dz} \left( \frac{1}{1 + e^{-z}} \right)\\
\\
&= \frac{e^{-z}}{(1 + e^{-z})^2}\\
\\
&= \frac{1}{1 + e^{-z}} \left( 1 - \frac{1}{1 + e^{-z}} \right)\\
\\
&= g(z)(1 - g(z))\end{aligned}  
$$

- 이제 로지스틱 회귀 모델을 정의했으므로, 다음 단계는 데이터를 가장 잘 설명하는 파라미터 $\boldsymbol{\theta}$를 구하는 것이다.  
- 그렇다면 이러한 $\boldsymbol{\theta}$는 어떻게 찾을 수 있을까?
	- 회귀와 동일하게 maximum likelihood estimation (MLE) 을 찾아야 함.
- 계산하기 쉬워지기 때문에 sigmoid를 사용함.
- 시그모이드의 도함수?는 시그모이드 의 곱으로 표현 할 수 있음 → 이게 매우 유용함. 계산이 쉬워짐
	- 도함수는 한 점에서의 미분계수(순간변화율)를 각 점에 대응시켜 만든 함수
	- 정의역의 모든 x에 대해 함수f(x)의 미분계수로 대응시키는 새로운 함수를 f(x)의 도함수



- likelihood 의 정의가 필요함.
- 로지스틱 회귀를 다시 확률적 모델로 볼 수 있으며, 최대우도추정(MLE)을 사용하여 최적의 파라미터를 찾을 수 있다.
- 이진 분류의 경우, 다음과 같은 조건부 확률을 가정한다: 
	-  binary Classification(2개로 분류): y가 1인 경우, 0인 경우로 분류 함.
	𝑝 (𝑦 = 1| 𝒙; 𝜽 )= 𝑓(𝜽) 𝒙 ,    𝑝(𝑦 = 0 𝒙; 𝜽) = 1 − 𝑓𝜽 (𝒙 )

- 이를 더 간결하게 표현하면 다음과 같다:
	$p(y \mid \mathbf{x}; \boldsymbol{\theta})  = \left( f_{\boldsymbol{\theta}}(\mathbf{x}) \right)^y  \left( 1 - f_{\boldsymbol{\theta}}(\mathbf{x}) \right)^{1-y}$
- 이 식은 **베르누이 분포(Bernoulli distribution)의 우도 함수**를 나타낸다.
	- Bernoulli distribution 이라고도 함.



- $n$개의 서로 독립인 학습 데이터가 있다고 가정하면, 주어진 데이터에 대한 파라미터 $\boldsymbol{\theta}$의 우도는 각 데이터에 대한 확률을 모두 곱한 형태로 표현된다:  
	$\displaystyle L(\boldsymbol{\theta}) = p(\mathbf{y} \mid \mathbf{X}; \boldsymbol{\theta})= \prod_{i=1}^{n} p(y^{(i)} \mid \mathbf{x}^{(i)}; \boldsymbol{\theta})$
	$\displaystyle = \prod_{i=1}^{n}  \left( f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) \right)^{y^{(i)}}  \left( 1 - f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) \right)^{1 - y^{(i)}}$
- 여러 식을 파이를 이용해서 합칠수 있음
-  이식이 likelihood의 정의

- 이전과 마찬가지로, 최적화를 더 쉽게 하기 위해 우도 함수 자체가 아니라 로그우도(log-likelihood)를 최대화한다:
	$\displaystyle\log L(\boldsymbol{\theta})  = \sum_{i=1}^{n}   y^{(i)} \log f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)})- (1 - y^{(i)}) \log \left( 1 - f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) \right)$

- 그렇다면 우도는 어떻게 최대화할 수 있을까?  
- 선형 회귀에서의 유도와 유사하게, 경사상승법(gradient ascent)을 사용할 수 있다.  
- 이전과 마찬가지로, 먼저 하나의 학습 데이터 ((x, y))만을 고려하여 시작할 수 있다.
- optimization 위해 log를 취하고 sum
- 로직은 회귀와 같음 다만, 이번에는 gradient ascent(경사 상승법)을 적용
	- 경사하강법의 -를 +로만 바꿔주면 됨.


- 하나의 학습 데이터 (x, y)에 대해 로그우도를 $\theta_j$로 미분하면 다음과 같다:  
	$\displaystyle\frac{\partial}{\partial \theta_j} \log L(\boldsymbol{\theta})= y \cdot \frac{1}{g(\boldsymbol{\theta}^T \mathbf{x})}- (1 - y) \cdot \frac{1}{1 - g(\boldsymbol{\theta}^T \mathbf{x})}  \cdot \frac{\partial}{\partial \theta_j} g(\boldsymbol{\theta}^T \mathbf{x})$

- 시그모이드 함수의 성질 ( g'(z) = g(z)(1 - g(z)) )를 이용하면, 이를 다음과 같이 단순화할 수 있다:  
	$\displaystyle= \left( y \cdot \frac{1}{g(\boldsymbol{\theta}^T \mathbf{x})}- (1 - y) \cdot \frac{1}{1 - g(\boldsymbol{\theta}^T \mathbf{x})} \right)  \cdot g(\boldsymbol{\theta}^T \mathbf{x})(1 - g(\boldsymbol{\theta}^T \mathbf{x})) \cdot \frac{\partial}{\partial \theta_j} (\boldsymbol{\theta}^T \mathbf{x})$
    
    $= \left( y (1 - g(\boldsymbol{\theta}^T \mathbf{x})) - (1 - y) g(\boldsymbol{\theta}^T \mathbf{x}) \right) x_j  = \left( y - f_{\boldsymbol{\theta}}(\mathbf{x}) \right) x_j$



- 따라서 다음과 같은 확률적 경사상승법(stochastic gradient ascent) 업데이트 규칙을 얻는다:
	$\theta_j := \theta_j - \alpha \left( f_{\boldsymbol{\theta}}(\mathbf{x}^{(i)}) - y^{(i)} \right) x_j^{(i)}$
- 이 업데이트 규칙은 선형 회귀에서 사용되는 최소제곱(least mean squares) 업데이트와 수학적으로 동일한 형태를 가진다는 점을 확인할 수 있다.
- 그러나 중요한 차이는 모델의 예측 방식에 있다.  
- 선형 회귀에서는 $f_{\boldsymbol{\theta}}(\mathbf{x})$가 입력의 선형 함수인 반면, 로지스틱 회귀에서는 $f_{\boldsymbol{\theta}}(\mathbf{x})$가 입력의 선형 결합에 시그모이드 함수를 적용한 값으로, 0과 1 사이의 값을 출력한다.
- 회귀식에 시그모이드를 넣은 수식이라고 생각 하면 됨.



- 따라서 로지스틱 회귀에서는 시그모이드 함수의 특성으로 인해 결정 경계(decision boundary) 근처에서는 업데이트가 크게 이루어지고, 이미 확신이 높은 예측 영역에서는 업데이트가 작아진다. 이로 인해 확률적이고 안정적인 분류 동작이 가능해진다.  
- 아래 그래프는 시그모이드 함수가 선형 예측 값을 0과 1 사이의 확률로 매핑하며, 결정 경계 근처에서 부드러운 변화를 생성함을 보여준다.
- 시그모이드 덕분에 decision boundary를 스무스 하게 만들어 줌.


### Logistic Regression and Multiclass Classification
- 지금까지의 논의는 이진 분류에 한정되어 있었지만, 로지스틱 회귀는 다중 클래스 분류 문제로 확장할 수 있다.  
- 이 경우 출력 변수 $y$는 $C$개의 가능한 클래스 중 하나의 값을 가진다.  
- 각 학습 데이터 $\mathbf{x}^{(i)}$에 대해, 해당 데이터가 각 클래스 $c \in {1, 2, \dots, C}$ 에 속할 확률을 모델링하는 것이 목표이다.
- 바이너리에서 멀티 클래스로 확장
- 로직은 동일함.
- 총 𝐶개의 classes가 가능

- 이러한 클래스 소속 확률들은 다항분포(multinomial distribution)를 따른다고 가정하며, 이는 $C$개의 클래스별 확률 $\phi_1, \phi_2, \dots, \phi_C$로 정의된다.  
- 각 파라미터 $\phi_c$는 해당 데이터가 클래스 $c$에 속할 확률을 의미한다. 이러한 확률들은 정의상 모두 더하면 1이 되어야 한다:
$\displaystyle\sum_{c=1}^{C} \phi_c = 1$
- likelihood 함수를 정의 하고
- 각각 확률값을 구하고, 그 값들을 더함.
- 각 확률값이 되려면
	- 모든 클래스의 합은1이 되야 함.
	- 모든 확률값은 음수가 될 수 없다.
- 이런 조건을 만족하는 함수를 찾아보니 softmax 함수가 적합했음
	- input 값이 확률값으로 변함.


- 모델의 원시 클래스 점수, 즉 선형 결합 $\boldsymbol{\theta}_1^T \mathbf{x}^{(i)}, \dots, \boldsymbol{\theta}_C^T \mathbf{x}^{(i)}$를 유효한 확률 분포로 변환하기 위해 일반적으로 소프트맥스(softmax) 함수를 적용한다.  
- 소프트맥스 함수는 모든 출력 확률이 0 이상이면서, 그 합이 1이 되도록 보장한다:  
	$\displaystyle\text{softmax}(t_1, \dots, t_C)\left[\frac{e^{t_1}}{\sum_{k=1}^{C} e^{t_k}},  \dots,  \frac{e^{t_C}}{\sum_{k=1}^{C} e^{t_k}}  \right]$



- 소프트맥스 함수는 지수 함수(exponential)를 사용하기 때문에 점수 간의 차이를 더욱 크게 만든다.  
- 그 결과, 더 큰 점수는 출력 확률 분포에서 훨씬 더 지배적으로 나타난다.  
- 동시에 모든 확률의 합이 1이 되어야 하므로, 다른 클래스들의 확률은 상대적으로 더 작아지게 된다.
- 소프트 맥스 함수를 사용하면, 클래스간의 값 편차를 크게 해주고
- 음수를 없앰.

- 이 프레임워크에서, $i$번째 데이터가 클래스 $c$ 로 분류될 확률은 다음과 같이 주어진다:
$$
\displaystyle p(y^{(i)} = c \mid \mathbf{x}^{(i)}; \boldsymbol{\theta}) = \phi_c^{(i)}  = \frac{\exp\left(\boldsymbol{\theta}_c^T \mathbf{x}^{(i)}\right)}  {\sum_{k=1}^{C} \exp\left(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)}\right)}
$$

- 이 식은 각 클래스에 대해 확률을 할당하는 다중 클래스 로지스틱 회귀 모델을 정의한다.  
- 이러한 확률적 모델이 주어졌으므로, 이제 파라미터 $\boldsymbol{\theta}$를 학습하기 위한 적절한 손실 함수(loss function)를 정의하는 단계로 넘어간다.



- 일반적인 접근 방식은 입력이 주어졌을 때 관측된 레이블의 우도를 최대화하는 것이다.  
- 실제 구현에서는 이는 음의 로그우도(negative log-likelihood)를 최소화하는 것과 동일하며, 계산이 용이하고 안정적인 손실 함수를 제공한다.
- 하나의 학습 데이터 $i$에 대한 손실 함수는 다음과 같이 정의된다:  
$$
L^{(i)}(\boldsymbol{\theta})  
= - \log p(y^{(i)} \mid \mathbf{x}^{(i)}; \boldsymbol{\theta})  
= - \log \left(  
\frac{\exp\left(\boldsymbol{\theta}_{y^{(i)}}^T \mathbf{x}^{(i)}\right)}  
{\sum_{k=1}^{C} \exp\left(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)}\right)}  
\right)  
$$
- -log를 취한다는 것은 경사 하강법을 쓰겠다는 의미 정도로만 보면 됨.
- 네가티브likelihood 함수



- 전체 ( n )개의 학습 데이터에 대해 모델을 평가하기 위해, 평균 음의 로그우도(negative log-likelihood)를 계산한다:
$$  
L(\boldsymbol{\theta})  
= \frac{1}{n} \sum_{i=1}^{n}

- \log p(y^{(i)} \mid \mathbf{x}^{(i)}; \boldsymbol{\theta})  
    = \frac{1}{n} \sum_{i=1}^{n}
    
- \log \left(  
    \frac{\exp\left(\boldsymbol{\theta}_{y^{(i)}}^T \mathbf{x}^{(i)}\right)}  
    {\sum_{k=1}^{C} \exp\left(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)}\right)}  
    \right)  
  $$

- 이 손실 함수는 크로스 엔트로피 손실(cross-entropy loss)로도 알려져 있으며, 다중 클래스 분류 문제에서 널리 사용된다. 이를 원-핫 인코딩(one-hot encoding)된 레이블을 사용하여 다음과 같이 표현할 수도 있다:
$$
- \frac{1}{n} \sum_{i=1}^{n} \sum_{c=1}^{C}  
    y_c^{(i)} \log p_c^{(i)},  
    \quad  
    y_c^{(i)} =  
    \begin{cases}  
    1, & \text{if } c = y^{(i)} \  
    0, & \text{otherwise}  
    \end{cases}  
 $$
- cross entropy loss 정의와 일치 함.
- 그래서 분류 문제에 cross entropy loss 많이 사용.


- 크로스 엔트로피 손실을 경사하강법으로 최소화하기 위해서는 파라미터 $\boldsymbol{\theta}_c$에 대한 손실 함수의 미분을 계산해야 한다.  
- 비록 손실 함수는 겉보기에는 실제 클래스의 확률에만 직접적으로 의존하는 것처럼 보이지만, 소프트맥스 함수에 의해 모든 클래스의 확률은 서로 연결되어 있으며 그 합이 1이 되어야 한다.  
- 따라서 어떤 클래스의 파라미터를 변경하더라도 전체 손실 값에 영향을 미치게 된다.
- 이러한 이유로, 특정 클래스 ( c )에 대해 미분을 계산할 때는 다음 두 가지 경우를 나누어 고려하는 것이 유용하다:
	1. $y^{(i)} = c$ (해당 데이터의 실제 레이블이 클래스 $c$인 경우)
    2. $y^{(i)} \ne c$ (해당 데이터의 실제 레이블이 클래스 $c$가 아닌 경우)

- 경사하강법을 사용 하려면 수식을 미분하면 됨.
- 하지만 이때 정답인 경우, 정답이 아닌경우로 나눠서 계산 해야 함.
	- 소프트 맥스 특징 때문임.
	- 소프트 맥스를 하면 큰값은 더 커지기 때문에 답인경우 아닌경우를 나누는게 필요함.



- 입력 벡터 $\mathbf{x}^{(i)}$가 주어졌을 때, 만약 $y^{(i)} = c$라면 다음과 같이 된다:

$$  
\frac{\partial}{\partial \boldsymbol{\theta}_c}  
\left( - \log \phi_{y^{(i)}}^{(i)} \right)  
= - \frac{1}{\phi_c^{(i)}} \cdot  
\frac{\partial \phi_c^{(i)}}{\partial \boldsymbol{\theta}_c}  
 
= - \frac{1}{\phi_c^{(i)}} \cdot  
\phi_c^{(i)} (1 - \phi_c^{(i)}) \mathbf{x}^{(i)}  
  
= (\phi_c^{(i)} - 1)\mathbf{x}^{(i)}  
$$

- 이는 다음과 같은 이유에서이다:

$$\begin{aligned}
\frac{\partial \phi_c^{(i)}}{\partial \boldsymbol{\theta}_c}  
&= \frac{\partial}{\partial \boldsymbol{\theta}_c}  
\left(  
\frac{\exp(\boldsymbol{\theta}_c^T \mathbf{x}^{(i)})}  
{\sum_{k=1}^{C} \exp(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)})}  
\right)\\
\\
&= \frac{  
\exp(\boldsymbol{\theta}_c^T \mathbf{x}^{(i)}) \mathbf{x}^{(i)} \cdot \sum_{k=1}^{C} \exp(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)})

- \exp(\boldsymbol{\theta}_c^T \mathbf{x}^{(i)}) \cdot \exp(\boldsymbol{\theta}_c^T \mathbf{x}^{(i)}) \mathbf{x}^{(i)}  
    }{  
    \left( \sum_{k=1}^{C} \exp(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)}) \right)^2  
    }\\
\\
&= \phi_c^{(i)} \mathbf{x}^{(i)} - \phi_c^{(i)} \phi_c^{(i)} \mathbf{x}^{(i)}\\
\\
&= \phi_c^{(i)} (1 - \phi_c^{(i)}) \mathbf{x}^{(i)}  
\end{aligned}
$$




- 입력 벡터 ( \mathbf{x}^{(i)} )가 주어졌을 때, 만약 ( y^{(i)} \ne c )라면 다음과 같이 된다:
$$  
\frac{\partial}{\partial \boldsymbol{\theta}_c}  
\left( - \log \phi_{y^{(i)}}^{(i)} \right)  
= - \frac{\partial}{\partial \boldsymbol{\theta}_c}  
\log \phi_{y^{(i)}}^{(i)}  
  
= - \frac{1}{\phi_{y^{(i)}}^{(i)}}  
\cdot  
\frac{\partial \phi_{y^{(i)}}^{(i)}}{\partial \boldsymbol{\theta}_c}  
  
= - \frac{1}{\phi_{y^{(i)}}^{(i)}}  
\cdot \left( - \phi_{y^{(i)}}^{(i)} \phi_c^{(i)} \mathbf{x}^{(i)} \right)  
  
= \phi_c^{(i)} \mathbf{x}^{(i)}  
$$
- 이는 다음과 같이 유도된다:

$$
\frac{\partial \phi_{y^{(i)}}^{(i)}}{\partial \boldsymbol{\theta}_c}  
= \frac{\partial}{\partial \boldsymbol{\theta}_c}  
\left(  
\frac{\exp(\boldsymbol{\theta}_{y^{(i)}}^T \mathbf{x}^{(i)})}  
{\sum_{k=1}^{C} \exp(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)})}  
\right)  
  
= - \frac{  
\exp(\boldsymbol{\theta}_{y^{(i)}}^T \mathbf{x}^{(i)})  
\cdot \exp(\boldsymbol{\theta}_c^T \mathbf{x}^{(i)}) \mathbf{x}^{(i)}  
}{  
\left( \sum_{k=1}^{C} \exp(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)}) \right)^2  
}  
\cdot \exp (\theta_𝑐^ T x^{{i}} )\cdot x^{(i)} 
$$

- 여기서 $c \ne y^{(i)}$이므로, 분자의 미분은 0이고 분모만 영향을 받는다. 몫의 미분을 적용하면:
  $$= - \phi_{y^{(i)}}^{(i)} \phi_c^{(i)} \mathbf{x}^{(i)}$$





- 정리하면 다음과 같다:
- 만약 $y^{(i)} = c$라면,  
   $$  
    \frac{\partial}{\partial \boldsymbol{\theta}_c}  
    \left( - \log \phi_{y^{(i)}}^{(i)} \right)  
    = (\phi_c^{(i)} - 1)\mathbf{x}^{(i)}  
    $$    
- 만약 $y^{(i)} \ne c$라면,  
    $$  
    \frac{\partial}{\partial \boldsymbol{\theta}_c}  
    \left( - \log \phi_{y^{(i)}}^{(i)} \right)  
    = \phi_c^{(i)} \mathbf{x}^{(i)}  
    $$


- 두 경우를 하나로 합치면, 모든 클래스 ( c )와 학습 데이터 ( i )에 대해 다음과 같이 표현할 수 있다:
$$  
\frac{\partial}{\partial \boldsymbol{\theta}_c}  
\left( - \log \phi_{y^{(i)}}^{(i)} \right)  
= \left( \phi_c^{(i)} - \mathbf{1}{y^{(i)} = c} \right)\mathbf{x}^{(i)}  
$$

- 여기서 $\mathbf{1}[{y^{(i)} = c}]$는 지시 함수(indicator function)로,  $y^{(i)} = c$이면 1, 그렇지 않으면 0의 값을 가진다.



- 따라서 모든 학습 데이터에 대해 크로스 엔트로피 손실을 $\boldsymbol{\theta}_c$로 미분한 결과는 다음과 같다:
$$  
\frac{\partial L_{\mathrm{CE}}}{\partial \boldsymbol{\theta}_c}  
= \frac{1}{n} \sum_{i=1}^{n}  
\left( \phi_c^{(i)} - \mathbf{1}{y^{(i)} = c} \right)\mathbf{x}^{(i)}  $$

- 여기서  $\displaystyle\phi_c^{(i)} = \frac{\exp(\boldsymbol{\theta}_c^T \mathbf{x}^{(i)})}  {\sum_{k=1}^{C} \exp(\boldsymbol{\theta}_k^T \mathbf{x}^{(i)})}$는 $i$번째 데이터가 클래스 $c$에 속할 예측 확률을 의미하며,$\mathbf{1}{\cdot}$는 지시 함수로, 해당 데이터의 실제 레이블이 클래스 $c$이면 1, 아니면 0이다.
- 이와 같이 구한 그래디언트를 이용하여 경사하강법을 적용하면 손실 함수를 최소화할 수 있다.



### Generalized Linear Models
- 지금까지 우리는 회귀와 분류라는 두 가지 유형의 문제를 살펴보았다.
- 회귀 문제에서는 입력 $\mathbf{x}$와 파라미터 $\boldsymbol{\theta}$가 주어졌을 때, 타깃 변수 $y$가 다음과 같은 정규분포를 따른다고 가정하는 것이 일반적이다:
$$  
y \mid \mathbf{x}; \boldsymbol{\theta} \sim \mathcal{N}(\mu, \sigma^2)  
$$
- 여기서 평균 $\mu$는 보통 $\mathbf{x}$와 $\boldsymbol{\theta}$의 함수로 모델링된다.
- 회귀와 분류 모두 거의 비슷함.
- 𝑦|𝒙; 𝜽 ~ 𝒩 (𝜇, $𝜎^2$)
	- 입력 x와 파라미터 θ가 주어졌을 때, 출력 y는 평균 μ, 분산 $σ^2$를 갖는 정규분포를 따른다



- 이진 분류 문제에서는 입력 $\mathbf{x}$와 파라미터 $\boldsymbol{\theta}$가 주어졌을 때, 타깃 변수 $y$가 베르누이 분포를 따른다고 가정한다:
$$
y \mid \mathbf{x}; \boldsymbol{\theta} \sim \text{Bernoulli}(\phi)  
$$

- 여기서 $\phi$ (양성 클래스일 확률)는 $\mathbf{x}$와 $\boldsymbol{\theta}$의 함수이다.
- 보다 일반적으로, 다중 클래스 분류에서는 타깃 변수가 다항분포(multinomial distribution)를 따르며, 모델은 각 가능한 클래스에 대한 확률을 추정한다.
- 𝑦|𝒙; 𝜽 ~ Bernoulli 𝜙 
	- 입력 x와 파라미터 θ가 주어지면, y는 확률 ϕ로 1이 되는 베르누이 분포를 따른다.
	- 이진 분류(binary classification)에서 사용하는 조건부 확률 모델
- y 값이 어떤 분포를 따르냐에 따라 regreess, classification, multinomial distribution인지 정해진다고 보면 됨.


- 이러한 모델들은 모두 더 일반적이고 유연한 프레임워크인 일반화 선형 모델(GLMs, generalized linear models)의 특수한 경우들이다.  
- GLM은 출력 변수가 다양한 확률분포를 따를 수 있도록 확장하고, 선형 예측값과 출력의 기댓값을 연결하는 함수를 사용한다.  
- 예를 들어, 선형 회귀는 항등 함수(identity function)를 사용하고, 이진 분류는 로지스틱 함수(logistic function)를 사용하며, 다중 클래스 분류는 소프트맥스 함수(softmax function)를 사용한다.


### Q&A

- 다음주는 확률 모델이어서 수학이 또 나올 것임.
- 어떤경우에 경사하강 어떤 경우 Analytical solution을 쓰나요?
	- 최적화 이론은 엄청나게 두꺼운 책임.
	- 교수님 박사때 보려다가 다 못 보심.
	- 그 중 경사하강등은 매우 일부 챕터임.
	- 실 데이터는 다 경사 하강에 의존한다고 보면 됨
	- 실데이터에 Analytical solution는 거의 없음
- 회귀는 정규분포
- 바이는 베르누이 분포
- 멀티는 멀티노미아(multinomial) 분포를 따름
