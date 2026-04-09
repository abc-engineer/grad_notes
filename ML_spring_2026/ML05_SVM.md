2026-04-07 08:20
## 5강 SVM

- 머신 러닝에서는 매우 많이 사용되고 거의 가장 좋은게 SVM
- 많이 어려움.
- 분류 모델 중에서 인공신경 나오기 전에 가장 많이 사용
- 성능이 좋고, 작은 모델에도 좋고, 일반화 성능이 매우 뛰어 남.
- SVM 의 파라미터는 매우 단순함.
- 하지만 깊게 파보면 여러가지 수학기법이 많이 나옴.
	- 교수님도 공부하실때 어려움이 있었음
- 여러 컨셉을 이해 해야 함.
- Margin이 중요 키워드 임.
	- 마진 (여백) 기반 방법이라는 것을 인지 해야 함.

### Functional and Geometric Margins
- 이진 분류에서는 데이터를 단순히 두 그룹으로 나누는 것만으로는 충분하지 않은 경우가 많다. 
- 훈련 예시를 올바르게 분류하는 결정 경계는 여러 개 있을 수 있지만, 그중 일부는 다른 것들보다 더 신뢰롭고 확신 있는 예측을 만든다.    
- 이러한 직관을 형식화하는 데 도움이 되는 유용한 개념 중 하나가 마진(margin)이며, 이는 분리가 얼마나 좋은지를 측정한다.
- 마진이 무엇인지 알아야 함.
- 지난 수업은 nonparametric이었는데 다시 파라메트릭으로 돌아 옴
- 2가지를 잘 나누는 선을 그어야 하니 W,b를 구해야 함.
- SVM의 포인트는 여백을 가장 크게 만드는게 모델의 목표

- 로지스틱 회귀를 고려하자. 여기서 확률 $p(y=1 \mid \mathbf{x}; \boldsymbol{\theta})$는 $h_{\boldsymbol{\theta}}(\mathbf{x}) = g(\boldsymbol{\theta}^T \mathbf{x})$로 모델링되며, $g$는 로지스틱 함수(시그모이드 함수)이다.    
- $\boldsymbol{\theta}^T \mathbf{x}$ 값이 클수록 $h_{\boldsymbol{\theta}}(\mathbf{x}) = p(y=1 \mid \mathbf{x}; \boldsymbol{\theta})$도 커지며, 따라서 레이블이 1일 것이라는 우리의 확신 정도도 높아진다.    
- 따라서 비형식적으로 $\boldsymbol{\theta}^T \mathbf{x} \gg 0$이면 $y=1$이라고 매우 높은 확신을 가지고 예측한다고 볼 수 있다.

- $\boldsymbol{\theta}^T \mathbf{x}$ 값을 구했을때 0보다 크면 클수록 결과 값이 맞다고 확신하게 됨.
- 이때의 거리 값을 마진이라 고함.

- 마찬가지로 $\boldsymbol{\theta}^T \mathbf{x} \ll 0$이면 로지스틱 회귀는 $y=0$을 매우 확신 있게 예측한다고 볼 수 있다.    
- 주어진 훈련 데이터에 대해, 분류를 위한 한 가지 유용한 접근은 다음을 만족하는 $\boldsymbol{\theta}$를 찾는 것이다: $y^{(i)}=1$일 때는 $\boldsymbol{\theta}^T \mathbf{x}^{(i)} \gg 0$, 그리고 $y^{(i)}=0$일 때는 $\boldsymbol{\theta}^T \mathbf{x}^{(i)} \ll 0$.    
- 본질적으로 이는 두 클래스를 큰 마진으로 분리하는 $\boldsymbol{\theta}$를 찾는 것에 해당한다.


- 마진은  중간값에서 얼마나 떨어져 있는지 수치화 한 것. ?????

- 이 아이디어는 1차원 입력을 넘어 고차원 설정으로 자연스럽게 확장된다.
- 이를 형식화하기 위해, 이진 분류를 위한 선형 분류기를 고려하자. 여기서 레이블은 $y \in {-1,1}$이고, 특징은 $\mathbf{x}$로 주어진다.
- 그림에서 X는 양의 훈련 예시($y=1$)를, O는 음의 훈련 예시($y=-1$)를 나타낸다.
- $\boldsymbol{\theta}$ 대신 $\mathbf{w}$와 $b$로 모델을 매개변수화하며, 분류기는 다음과 같이 정의된다:  
$$h_{\mathbf{w}, b}(\mathbf{x}) = \mathbf{w}^T \mathbf{x} + b.$$

- 결정 경계(또는 분리 초평면)는 다음과 같이 주어진다:  
$$\mathbf{w}^T \mathbf{x} + b = 0.$$
- $\mathbf{w}^T \mathbf{x} + b$ 0보다 크면 직선 윗 구역 작으면 아래 구역
- 점 A에서 예측을 해야 한다면, 이는 X들과 같은 클래스에 속한다고 상당히 높은 확신을 가질 수 있다.
- 반면 점 C에서의 예측은 그보다 확신이 낮다.
- 따라서 A에서의 예측에 대한 확신이 C에서보다 훨씬 높다고 말할 수 있다.
- 이러한 확신의 개념은 마진(margin)으로 표현할 수 있으며, 이는 해당 점이 결정 경계로부터 얼마나 떨어져 있는지를 측정한다.

- $\mathbf{w}^T \mathbf{x} + b$ 값이 클수록 직선에서 멀어짐 -> 이 깂을 마진이라고 생각 하면 됨.
- 마진이 크면 그 클래스일 확률이 크다라고 판단 할 수 있음.
	- 직선에서 멀리 있으니까 

- 구체적으로, 훈련 예시 $(\mathbf{x}^{(i)}, y^{(i)})$에 대한 함수적 마진(functional margin)을 $(\mathbf{w}, b)$에 대해 다음과 같이 정의할 수 있다:  
$$\hat{\gamma}^{(i)} = y^{(i)} \left( \mathbf{w}^T \mathbf{x}^{(i)} + b \right).$$
- 이 값은 예측의 정답 여부와 그에 대한 확신 정도를 모두 반영한다.
- 예를 들어, $y^{(i)}=1$이고 $\mathbf{w}^T \mathbf{x}^{(i)} + b$가 매우 큰 양수라면, $\hat{\gamma}^{(i)}$도 크고 양수가 되며 이는 모델이 정답을 매우 확신 있게 예측하고 있음을 의미한다.

- 마진을 수학적으로 정의
	- 직선 식에 y 값을 곱하는데 y 값은 클래스 1, -1로 해서 마이너스 값일때 -1일 곱해서 마진을 양수로 만ㄷ르어 주면 됨.
- 그리고 마진값을 최대로 해주는 값을 찾으면 됨.
	- 최적화 계산산

- 함수적 마진은 점이 얼마나 확신 있게 분류되는지를 어느 정도 나타내지만, 가중치 벡터 $\mathbf{w}$의 스케일에 민감하다.    
- 예를 들어, $2x_1 + 3x_2 + 1 = 0$과 $4x_1 + 6x_2 + 2 = 0$은 같은 직선을 나타내지만, 점 $(2,1)$에 대한 함수적 마진 값은 서로 다르다 (예: 각각 8과 16).

- 마진은 weight vector 𝒘에 매우 민감함.
- $2x_1 + 3x_2 + 1 = 0$과 $4x_1 + 6x_2 + 2 = 0$은 같은 직선인데 마진을 계산하면 4x 수식의 값이 더 커짐
- 이걸 functional margins이라 함.
- 이 문제를 보완한게 Geometric Margins
- 이를 해결하기 위해 기하학적 마진(geometric margin) 개념을 도입한다. 함수적 마진과 달리, 기하학적 마진은 점의 분류 상태뿐 아니라 분리 초평면으로부터의 실제 거리까지 제공한다.
- 이 거리는 가중치 벡터 $\mathbf{w}$의 노름(norm)에 대해 정규화되어 측정되므로, 결정 경계로부터 얼마나 잘 분리되어 있는지를 더 해석 가능하고 정확하게 나타낸다.
- 구체적으로, 훈련 예시 $(\mathbf{x}^{(i)}, y^{(i)})$에 대한 $(\mathbf{w}, b)$의 기하학적 마진은 다음과 같이 정의된다:  
$$\gamma^{(i)} = \frac{y^{(i)}\left(\mathbf{w}^T \mathbf{x}^{(i)} + b\right)}{|\mathbf{w}|}.$$
- $\mathbf{w}$의 노름이 1인 경우, 함수적 마진과 기하학적 마진은 같아져 $\gamma^{(i)} = \hat{\gamma}^{(i)}$가 된다.

- 서포트 벡터 머신(Support Vector Machines, SVM)의 맥락에서 목표는 이 Geometric Margins기하학적 마진을 최대화하는 분류기classifier 를 찾는 것이다.

- 그냥 봐도 H3이 더 분류를 잘함.
	- 일반화가 잘되어 있다고 볼 수 있음.


- 보다 구체적으로, 훈련 집합 $S = {(\mathbf{x}^{(i)}, y^{(i)})}_{i=1}^{n}$가 주어졌을 때, SVM의 목표는 모든 훈련 예시에 대한 기하학적 마진 중 최솟값을 최대화하는 것이다:  

$$\gamma = \min_{i=1,\ldots,n} \gamma^{(i)}.$$
- 여기서 결정 경계에 가장 가까이 위치한 데이터 포인트들을 서포트 벡터(support vectors)라고 한다.

- 중요 포인트는 smallest geometric margin을 크게 만드는 것임.
	- 이때의 W,b를 구하는게 SVM
- 선에서 가장 가까운 값들을 서포트 벡터라고 부름
	- 이 가까운 값들의 중간값을 지나는 선이 서포트 벡터의 마진을 가장 최대화 할 수 있음

### Support Vector Machines
- 기하학적 마진을 최대화하는 결정 경계를 찾기 위해 다음과 같은 최적화 문제를 설정한다:  

$$\max_{\gamma, \mathbf{w}, b} \ \gamma$$  

$$\text{subject to } \ \frac{y^{(i)}\left(\mathbf{w}^T \mathbf{x}^{(i)} + b\right)}{|\mathbf{w}|} \ge \gamma \quad \text{for } i=1,\ldots,n$$

- 여기서 $y^{(i)} \in {-1,1}$은 클래스 레이블이다.

- 최적화 문제는 smalist geometric margin을 최대화 하는게 목표
- 이 수식이 서포트 벡터를 수식화 한것이라 볼 수 있음.

- 그러나 기하학적 마진 $\gamma$는 분모에 $|\mathbf{w}| = \sqrt{w_1^2 + \cdots + w_n^2}$를 포함하고 있어, 함수가 비선형이고 비볼록(non-convex)해진다.
- 이를 단순화하기 위해 $\gamma = \frac{\hat{\gamma}}{|\mathbf{w}|}$ 관계를 이용하여 함수적 마진으로 문제를 재구성할 수 있다:  

$$\max_{\hat{\gamma}, \mathbf{w}, b} \ \frac{\hat{\gamma}}{||\mathbf{w}||}$$  

$$\text{subject to } \ y^{(i)}\left(\mathbf{w}^T \mathbf{x}^{(i)} + b\right) \ge \hat{\gamma} \quad \text{for } i=1,\ldots,n$$

- 분모에 W가 있으면 계산이 어려워서 그냥 지우고 founctional margin으로 바꿈.

- 문제를 더욱 단순화하기 위해 founctional 마진 $\hat{\gamma}$를 상수로 고정할 수 있으며, 일반적으로 $\hat{\gamma} = 1$로 둔다. 이는 $\mathbf{w}$와 $b$를 스케일링해도 해의 타당성이 변하지 않기 때문에 가능하다.
- 이때 최적화 문제는 다음과 같이 변한다:  

$$\max_{\mathbf{w}, b} \ \frac{1}{|\mathbf{w}|}$$  

$$\text{subject to } \ y^{(i)}\left(\mathbf{w}^T \mathbf{x}^{(i)} + b\right) \ge 1 \quad \text{for } i=1,\ldots,n$$

- 마지막으로, 이를 볼록 최적화 문제로 만들기 위해 $\frac{1}{|\mathbf{w}|}$을 최대화하는 대신 $\frac{1}{2}|\mathbf{w}|^2$을 최소화하는 형태로 바꾼다:  
$$\min_{\mathbf{w}, b} \ \frac{1}{2}|\mathbf{w}|^2$$  
$$\text{subject to } \ y^{(i)}\left(\mathbf{w}^T \mathbf{x}^{(i)} + b\right) \ge 1 \quad \text{for } i=1,\ldots,n$$

- r=1로 만들고 w를 분모로 올려서 제곱곱


- 이 형태에서는 $|\mathbf{w}|^2$을 최소화하면서, 모든 훈련 예시가 함수적 마진이 최소 1 이상이 되도록 올바르게 분류되도록 한다.    
- 이는 제약 조건이 있는 최적화 문제로, 매개변수가 반드시 만족해야 하는 조건을 두면서 목적 함수를 최소화하는 문제이다.

### Constrained Optimization via Lagrange Duality
- 이러한 제약 최적화 문제는 라그랑주 이중성(Lagrange duality)을 사용하여 해결할 수 있으며, 이를 통해 원래 문제를 더 다루기 쉬운 이중 문제(dual form)로 재작성할 수 있다.    
- 이러한 재구성은 이론적 분석에 유용할 뿐만 아니라, 커널 방법(kernel methods)과 같은 고급 기법을 가능하게 하는 데에도 중요한 역할을 한다.

- 함수 $f(\mathbf{w})$를 최소화하되, 등식 제약 조건 $h_i(\mathbf{w}) = 0$을 만족해야 하는 최적화 문제를 고려하자:  

$$\min_{\mathbf{w}} \ f(\mathbf{w})\quad\text{subject to } \ h_i(\mathbf{w}) = 0 \quad \text{for } i=1,\ldots,l$$  

- 이러한 문제를 해결하는 일반적인 방법 중 하나는 라그랑주 승수법(Lagrange multiplier method)을 사용하는 것이다:  

$$\mathcal{L}(\mathbf{w}, \boldsymbol{\beta}) = f(\mathbf{w}) + \sum_{i=1}^{l} \beta_i h_i(\mathbf{w})$$
- 여기서 $\boldsymbol{\beta}$는 각 등식 제약 조건에 대응하는 라그랑주 승수이다.

- 해를 구하기 위해 $\mathcal{L}(\mathbf{w}, \boldsymbol{\beta})$를 $\mathbf{w}$와 $\boldsymbol{\beta}$ 각각에 대해 편미분한 뒤, 이를 0으로 둔다:  

$$\frac{\partial \mathcal{L}}{\partial w_i} = 0, \quad \frac{\partial \mathcal{L}}{\partial \beta_i} = 0.$$
- 이 방법은 등식 제약뿐만 아니라 부등식 제약이 포함된 문제로도 일반화할 수 있다.

- 다음과 같은 최적화 문제를 고려하자:  

$$\min_{\mathbf{w}} \ f(\mathbf{w})$$  $$\text{subject to } \ g_i(\mathbf{w}) \le 0 \quad \text{for } i=1,\ldots,k,$$  $$\qquad\qquad\ \ h_i(\mathbf{w}) = 0 \quad \text{for } i=1,\ldots,l$$
- 이 경우의 일반화된 라그랑지안 함수는 다음과 같이 정의된다:  

$$\mathcal{L}(\mathbf{w}, \boldsymbol{\alpha}, \boldsymbol{\beta}) = f(\mathbf{w}) + \sum_{i=1}^{k} \alpha_i g_i(\mathbf{w}) + \sum_{i=1}^{l} \beta_i h_i(\mathbf{w})$$  

$$\alpha_i \ge 0 \quad \text{for } i=1,\ldots,k$$

- 여기서 $\boldsymbol{\alpha}$와 $\boldsymbol{\beta}$는 각각 부등식 제약과 등식 제약에 대응하는 라그랑주 승수이다.

- 각 승수 $\alpha_i \ge 0$이어야 한다는 점이 중요하다. 이 조건은 부등식 제약이 올바르게 반영되도록 보장한다.    
- 어떤 후보 해가 $g_i(\mathbf{w}) \le 0$을 만족하면, $\alpha_i g_i(\mathbf{w})$ 항은 목적 함수 값을 증가시키지 않는다.    
- 반대로 제약을 위반하여 $g_i(\mathbf{w}) > 0$이면, $\alpha_i \ge 0$이므로 $\alpha_i g_i(\mathbf{w})$는 양수가 되어 라그랑지안 값을 증가시킨다.    
- 우리는 최소화를 수행하므로, 이러한 비실현 가능(infeasible)한 점들은 덜 선호되게 된다.    
- 한편 등식 제약에 대한 승수 $\beta_i$는 부호에 제한이 없으며, 이는 $h_i(\mathbf{w}) = 0$에서의 편차가 양쪽 방향 모두에서 보정되어야 하기 때문이다.

- 일반화된 라그랑지안은 다음과 같다:  

$$\mathcal{L}(\mathbf{w}, \boldsymbol{\alpha}, \boldsymbol{\beta}) = f(\mathbf{w}) + \sum_{i=1}^{k} \alpha_i g_i(\mathbf{w}) + \sum_{i=1}^{l} \beta_i h_i(\mathbf{w}), \quad \alpha_i \ge 0$$
- 이 제약 최적화 문제를 직접 푸는 대신, 이를 두 주체 간의 상호작용으로 볼 수 있다:
- 한쪽(원문제 변수, primal variable)은 목적 함수를 작게 만들기 위해 $\mathbf{w}$를 선택한다.
- 다른 한쪽(이중 변수, dual variables)은 제약 위반을 최대한 강하게 벌주기 위해 $\boldsymbol{\alpha}, \boldsymbol{\beta}$를 선택한다.
- 이러한 관점은 최적화를 구성하는 두 가지 자연스러운 방식으로 이어진다.

- 프라이멀 접근(primal approach)에서는, 고정된 $\mathbf{w}$에 대해 먼저 라그랑주 승수들을 선택하여 이를 최대한 크게 벌주도록 한다:  

$$\theta_P(\mathbf{w}) = \max_{\boldsymbol{\alpha}, \boldsymbol{\beta} : \alpha_i \ge 0} \ \mathcal{L}(\mathbf{w}, \boldsymbol{\alpha}, \boldsymbol{\beta})$$
- 이후 $\boldsymbol{\alpha}, \boldsymbol{\beta}$에 대해 라그랑지안을 최대화한 값을 $\mathbf{w}$에 대해 최소화한다:  

$$p^* = \min_{\mathbf{w}} \ \theta_P(\mathbf{w}) = \min_{\mathbf{w}} \max_{\boldsymbol{\alpha}, \boldsymbol{\beta} : \alpha_i \ge 0} \ \mathcal{L}(\mathbf{w}, \boldsymbol{\alpha}, \boldsymbol{\beta})$$
- 이 프라이멀 문제의 최적값을 $p^*$로 표기한다.

- 순서를 반대로 하면 어떻게 될까?    
- 즉, 먼저 라그랑주 승수에 대해 최대화하고 그다음 $\mathbf{w}$에 대해 최소화하는 대신, 먼저 $\mathbf{w}$에 대해 라그랑지안을 최소화한다:  

$$\theta_D(\boldsymbol{\alpha}, \boldsymbol{\beta}) = \min_{\mathbf{w}} \ \mathcal{L}(\mathbf{w}, \boldsymbol{\alpha}, \boldsymbol{\beta})$$
- 그런 다음 이 값을 $\boldsymbol{\alpha}, \boldsymbol{\beta}$에 대해 최대화한다 ($\alpha_i \ge 0$ 조건 하에서):  

$$d^* = \max_{\boldsymbol{\alpha}, \boldsymbol{\beta} : \alpha_i \ge 0} \ \theta_D(\boldsymbol{\alpha}, \boldsymbol{\beta}) = \max_{\boldsymbol{\alpha}, \boldsymbol{\beta} : \alpha_i \ge 0} \min_{\mathbf{w}} \ \mathcal{L}(\mathbf{w}, \boldsymbol{\alpha}, \boldsymbol{\beta})$$
- 이를 이중 문제(dual problem)라고 하며, 이 문제의 최적값을 $d^*$로 표기한다.

- 모든 최적화 문제(볼록이든 아니든)에 대해 다음의 중요한 부등식이 항상 성립한다:  

$$d^* \le p^*.$$
- 이를 약한 이중성(weak duality)이라고 하며, 이중 문제의 해는 프라이멀 문제 최적값의 하한(lower bound)을 제공한다.
- 볼록 최적화에서는, 비교적 완화된 조건 하에서 더 강한 결과가 성립한다:  

$$d^* = p^*.$$
- 이를 강한 이중성(strong duality)이라고 한다.


- SVM에서 주요한 개념임 따로 공부 해보면 좋을 것.

- 강한 이중성이 성립하는 경우(예: SVM과 같은 볼록 최적화 문제), 카루시-쿤-터커 조건(Karush–Kuhn–Tucker conditions, KKT)은 최적성에 대해 필요충분조건이 된다.

- 따라서 KKT 조건을 만족하는 임의의 점 $(\mathbf{w}^*, \boldsymbol{\alpha}^*, \boldsymbol{\beta}^*)$는 프라이멀-듀얼 최적해이다.  

$$\frac{\partial}{\partial w_i} \mathcal{L}(\mathbf{w}^*, \boldsymbol{\alpha}^*, \boldsymbol{\beta}^*) = 0 \quad \text{(Stationarity)}$$  

$$g_i(\mathbf{w}^*) \le 0 \ \text{and} \ h_i(\mathbf{w}^*) = 0 \quad \text{(Primal feasibility)}$$

$$\alpha_i^* \ge 0 \quad \text{(Dual feasibility)}$$  

$$\alpha_i^* g_i(\mathbf{w}^*) = 0 \quad \text{(Complementary slackness)}$$

- 특히 마지막 상보적 여유 조건(complementary slackness)은 승수와 제약 조건이 어떻게 상호작용하는지를 설명해주기 때문에 매우 중요하다.
- 식 $\alpha_i^* g_i(\mathbf{w}^*) = 0$은 각 부등식 제약에 대해 두 항 중 적어도 하나는 0이어야 함을 의미한다.
- 만약 $\alpha_i^* > 0$이라면, 곱이 0이 되기 위해서는 반드시 $g_i(\mathbf{w}^*) = 0$이어야 한다. 이는 해당 제약이 경계(boundary)에 정확히 위치하며 최적해를 직접적으로 결정함을 의미한다.
- 반대로 $g_i(\mathbf{w}^*) < 0$이라면, 곱이 0이 되기 위해서는 $\alpha_i^* = 0$이어야 한다. 이는 해당 제약이 비활성(inactive) 상태이며 최종 해에 영향을 주지 않음을 의미한다.
- 서포트 벡터 머신에서는 이로 인해 일부 훈련 데이터(서포트 벡터)만이 최종 결정 경계를 결정하고, 나머지 데이터는 영향을 주지 않게 된다.

- 이 시점에서 자연스럽게 다음과 같은 질문이 생길 수 있다: 왜 이러한 과정을 거치는가?
- 많은 문제에서 원래의 제약 최적화 문제를 직접 푸는 것은 어렵다. 제약 조건이 복잡하거나 변수의 수가 매우 클 수 있기 때문이다.
- 라그랑지안을 이용해 문제를 재구성하고 최적화 순서를 바꾸면, 승수들만으로 표현된 새로운 문제를 얻게 된다.
- 이 새로운 문제는 종종 더 단순한 구조를 가지며, 경우에 따라 변수의 수가 더 적거나 제약 조건이 더 다루기 쉬워진다.
- 또한 강한 이중성이 성립하면, 이 대체 문제의 최적값은 원래 문제의 최적값과 정확히 같다:  

$$d^* = p^*.$$
- 이는 우리가 더 풀기 쉬운 동등한 문제를 대신 해결하면 된다는 것을 의미한다.

### Support Vector Machines: The Dual Form
- SVM으로 돌아가서, 우리는 다음 함수를 최소화하고자 한다:  

$$\min_{\mathbf{w},b}\ \frac{1}{2}|\mathbf{w}|^2 \quad \text{subject to} \quad y_i(\mathbf{w}^T\mathbf{x}_i+b)\ge 1,\quad i=1,\ldots,n.$$
- 제약조건은 다음과 같이 쓸 수 있다:  

$$g_i(\mathbf{w},b)=-y_i(\mathbf{w}^T\mathbf{x}_i+b)+1\le 0.$$


- 원문제의 라그랑지안을 구성하면 다음과 같다:  

$$\mathcal{L}(\mathbf{w},b,\boldsymbol{\alpha})=\frac{1}{2}|\mathbf{w}|^2-\sum_{i=1}^n \alpha_i\left(y_i(\mathbf{w}^T\mathbf{x}_i+b)-1\right).$$

- 여기서 $\alpha_i\ge 0$는 부등식 제약조건에 대응하는 라그랑주 승수이다.
- 이 문제에는 부등식 제약조건만 있으므로, 등식 제약조건에 대한 라그랑주 승수 $\beta_i$는 존재하지 않는다.

- 쌍대 문제를 구하기 위해, 먼저 라그랑지안 $\mathcal{L}$을 $\mathbf{w}$와 $b$에 대해 최소화하고, $\alpha_i$는 상수로 취급한다.
- $\mathbf{w}$에 대한 $\mathcal{L}$의 기울기를 0으로 두면 다음을 얻는다:  

$$\nabla_{\mathbf{w}}\mathcal{L}(\mathbf{w},b,\boldsymbol{\alpha})=\mathbf{w}-\sum_{i=1}^n \alpha_i y_i \mathbf{x}_i=\mathbf{0}.$$
- 이를 $\mathbf{w}$에 대해 풀면 다음과 같다:  

$$\mathbf{w}=\sum_{i=1}^n \alpha_i y_i \mathbf{x}_i.$$

- 마찬가지로, $b$에 대한 $\mathcal{L}$의 도함수를 0으로 두면 다음을 얻는다: 

$$\frac{\partial \mathcal{L}}{\partial b}=-\sum_{i=1}^n \alpha_i y_i=0.$$

- 이는 다음의 등식 제약조건으로 단순화된다:  

$$\sum_{i=1}^n \alpha_i y_i=0.$$


- $\mathbf{w}$의 식을 다시 라그랑지안에 대입하면, $\mathcal{L}$은 다음과 같이 정리된다:  

$$\mathcal{L}(\mathbf{w},b,\boldsymbol{\alpha})=\frac{1}{2}|\mathbf{w}|^2-\sum_{i=1}^n \alpha_i\left(y_i(\mathbf{w}^T\mathbf{x}_i+b)-1\right).$$

- 첫 번째 항에 대해, 다음과 같이 전개할 수 있다:  

$$\frac{1}{2}|\mathbf{w}|^2=\frac{1}{2}\left|\sum_{i=1}^n \alpha_i y_i \mathbf{x}_i\right|^2=\frac{1}{2}\left(\sum_{i=1}^n \alpha_i y_i \mathbf{x}_i\right)^T\left(\sum_{j=1}^n \alpha_j y_j \mathbf{x}_j\right).$$


- 이를 전개하면 다음을 얻는다:  

$$\frac{1}{2}|\mathbf{w}|^2=\frac{1}{2}\sum_{i=1}^n\sum_{j=1}^n \alpha_i \alpha_j y_i y_j , \mathbf{x}_i^T \mathbf{x}_j.$$

- 여기서 $\mathbf{x}_i^T \mathbf{x}_j$는 $\mathbf{x}_i$와 $\mathbf{x}_j$ 사이의 내적(inner product)을 의미한다.

- 다음으로 두 번째 항을 정리하면:  

$$-\sum_{i=1}^n \alpha_i\left(y_i(\mathbf{w}^T\mathbf{x}_i+b)-1\right)=-\sum_{i=1}^n \alpha_i y_i\left(\sum_{j=1}^n \alpha_j y_j \mathbf{x}_j^T\mathbf{x}_i+b\right)+\sum_{i=1}^n \alpha_i.$$

- 즉,  

$$-\sum_{i=1}^n \alpha_i y_i \sum_{j=1}^n \alpha_j y_j \mathbf{x}_j^T\mathbf{x}_i-b\sum_{i=1}^n \alpha_i y_i+\sum_{i=1}^n \alpha_i.$$

- 여기서 앞서 얻은 등식 제약조건  

$$\sum_{i=1}^n \alpha_i y_i=0$$

- 을 사용하면, $b$가 포함된 항은 사라진다.

- 따라서 위 식은 다음과 같이 정리된다:  

$$-\sum_{i=1}^n\sum_{j=1}^n \alpha_i\alpha_j y_i y_j , \mathbf{x}_i^T\mathbf{x}_j-b\sum_{i=1}^n \alpha_i y_i+\sum_{i=1}^n \alpha_i=-\sum_{i=1}^n\sum_{j=1}^n \alpha_i\alpha_j y_i y_j , \mathbf{x}_i^T\mathbf{x}_j+\sum_{i=1}^n \alpha_i.$$

- 마지막 등식은 다음 제약조건  

$$\sum_{i=1}^n \alpha_i y_i=0$$

- 을 사용했기 때문에 성립한다.

- 이를 모두 합치면 다음과 같다:  

$$\mathcal{L}(\mathbf{w},b,\boldsymbol{\alpha})=\frac{1}{2}\sum_{i=1}^n\sum_{j=1}^n \alpha_i\alpha_j y_i y_j , \mathbf{x}_i^T\mathbf{x}_j-\sum_{i=1}^n\sum_{j=1}^n \alpha_i\alpha_j y_i y_j , \mathbf{x}_i^T\mathbf{x}_j+\sum_{i=1}^n \alpha_i=\sum_{i=1}^n \alpha_i-\frac{1}{2}\sum_{i=1}^n\sum_{j=1}^n \alpha_i\alpha_j y_i y_j , \mathbf{x}_i^T\mathbf{x}_j.$$

- 우리의 목표는 $\mathcal{L}(\boldsymbol{\alpha})$를 $\alpha_i$에 대해 최대화하는 것이며, 제약조건은 다음과 같다:  

$$\alpha_i\ge 0 \quad \text{for all } i,\qquad \sum_{i=1}^n \alpha_i y_i=0.$$

- 따라서 쌍대 최적화 문제는 다음과 같다:  

$$\max_{\boldsymbol{\alpha}}\ \sum_{i=1}^n \alpha_i-\frac{1}{2}\sum_{i=1}^n\sum_{j=1}^n \alpha_i\alpha_j y_i y_j , \mathbf{x}_i^T\mathbf{x}_j$$

$$\text{subject to} \quad \alpha_i\ge 0 \quad \text{for all } i,\qquad \sum_{i=1}^n \alpha_i y_i=0.$$

- 이 SVM의 쌍대 문제는 선형 등식 및 부등식 제약조건을 가지는 볼록 이차계획(Quadratic Programming, QP) 문제이다.
- 볼록 문제이기 때문에 전역 최적해가 유일하게 존재하며, 따라서 최적의 라그랑주 승수 $\boldsymbol{\alpha}^*$를 안정적으로 구할 수 있다.
- 실제로는 표준 QP 솔버나 Sequential Minimal Optimization(SMO)와 같은 특화된 알고리즘을 사용하여 효율적으로 해결한다.

- 최적의 라그랑주 승수 $\boldsymbol{\alpha}^*$를 구한 이후에는 Karush-Kuhn-Tucker(KKT) 조건을 이용하여 분류기의 나머지 파라미터를 복원할 수 있다.
- 특히, 최적의 가중치 벡터는 다음과 같이 주어진다:  

$$\mathbf{w}^*=\sum_{i=1}^n \alpha_i^* y_i \mathbf{x}_i.$$
- 마찬가지로, 최적의 바이어스 항 $b^*$는 $\alpha_i>0$을 만족하는 서포트 벡터 $\mathbf{x}_i$를 사용하여 구할 수 있으며, 마진에서의 등식 조건 을 이용한다.

$$y_i\left((\mathbf{w}^*)^T\mathbf{x}_i+b^*\right)=1$$
- 서포트 벡터의 마진이 커지면 일반화 성능이 올라감.



- 이 시점에서 KKT의 상보성 슬랙 조건은 매우 중요해지는데, 이는 어떤 훈련 예제가 최종 분류기에 실제로 영향을 주는지를 정확히 알려주기 때문이다.
- 각 훈련 예제는 최적화 문제에 하나의 제약조건을 추가한다:  

$$g_i(\mathbf{w},b)=-y_i(\mathbf{w}^T\mathbf{x}_i+b)+1\le 0$$

- KKT 상보성 슬랙 조건은 다음을 만족해야 한다:  

$$\alpha_i g_i(\mathbf{w}^*)=0$$
- 이 조건은 각 훈련 예제에 대해 두 항 중 적어도 하나는 반드시 0이어야 함을 의미한다.

- 만약 $\alpha_i^*>0$이면, 해당 제약조건은 활성(active) 상태여야 하므로 다음이 성립한다:  

$$g_i(\mathbf{w}^*,b^*)=0,\quad y_i(\mathbf{w}^{_T}\mathbf{x}_i+b^*)=1$$
- 따라서 이러한 점들은 마진 위에 정확히 놓이며, 최적 결정 경계를 직접적으로 결정한다.
- 이들을 “서포트 벡터(support vectors)”라고 한다.

- 반대로, 어떤 훈련 예제가 마진 밖에 엄격하게 위치한다면 $g_i(\mathbf{w}^*,b^*)<0$이며, 상보성 슬랙 조건에 의해 $\alpha_i^*=0$이 된다.
- 이러한 점들은 가중치 벡터에 기여하지 않으므로 최종 분류기에 영향을 주지 않는다:  

$$\mathbf{w}^*=\sum_{i=1}^{n}\alpha_i^* y_i \mathbf{x}_i$$

### Regularization
- 지금까지의 SVM 정식화는 훈련 데이터가 마진이 최소 1인 초평면에 의해 완벽하게 분리 가능하다고 가정하였다.
- 이 설정에서는 다음 조건을 요구한다:  

$$y_i(\mathbf{w}^T\mathbf{x}_i+b)\ge 1,\quad i=1,\ldots,n$$
- 정규화 방법 소개

- 그러나 실제 데이터에서는 완벽한 분리가 비현실적인 경우가 많다. 클래스가 약간 겹칠 수 있고, 레이블에 노이즈가 존재할 수도 있다.
- 예를 들어, 오른쪽 그림의 좌측 상단 영역에 있는 하나의 이상치(outlier)만으로도 결정 경계가 크게 이동하게 되어, 훨씬 작은 마진을 갖는 분류기가 만들어질 수 있다.

- 실제 데이터는 뜬금없이 outlier 데이터가 들어가는 경우가 많음
- 이런 값 때문에 서포트 벡터가 바뀌고 직선이 바뀜.
- 만약에 이 아웃라이어가 가짜 값이면 훈련 값이 떨어짐. 
- 덜 민감하게 하려면 정규화가 필요

- 이러한 문제를 해결하기 위해, 데이터가 완벽하게 분리되지 않는 경우에도 동작하고 이상치에 덜 민감하도록 SVM을 수정한다.
- 이를 위해 슬랙 변수 $\xi_i$를 도입하고 최적화 문제를 다음과 같이 재정식화한다:  

$$\min_{\mathbf{w},b}\ \frac{1}{2}|\mathbf{w}|^2 + C\sum_{i=1}^{n}\xi_i$$ 

$$\text{subject to}\quad y_i(\mathbf{w}^T\mathbf{x}_i+b)\ge 1-\xi_i,\quad i=1,\ldots,n$$  $$\xi_i\ge 0,\quad i=1,\ldots,n$$

- 여기서 슬랙 변수 $\xi_i$는 $i$번째 데이터가 마진 조건을 위반하는 정도를 나타낸다.

- 𝜉: 슬랙
- 마진값 1에 슬렉 값을 배서 조금 더 여유 있게 직선을 구할 수 있음

- 구체적으로, $\xi_i=0$이면 해당 점은 원래의 제약조건을 만족한다.
- $\xi_i>0$이면 해당 점은 마진 내부에 있거나, $\xi_i>1$인 경우에는 잘못 분류된 것이다.
- 따라서 모든 점이 반드시 마진의 올바른 쪽에 위치하도록 강제하는 대신, 일부 유연성을 허용하며 목적 함수는 $\sum_{i=1}^{n}\xi_i$를 패널티로 부과하여 $\xi_i$들이 가능한 한 작아지도록 유도한다.
- 여기서 매개변수 $C$는 $|\mathbf{w}|^2$를 최소화하는 것과 슬랙 변수 $\xi_i$를 통해 일부 오분류를 허용하는 것 사이의 균형(trade-off)을 조절한다.
- $C$ 값이 클수록 오분류를 덜 허용하고, $C$ 값이 작을수록 더 많은 유연성을 허용한다.

- 수식보다 이 슬라이드의 개념을 이해하고 가면 좋음.
- 이 𝜉정도는 틀려도 된다는 것을 모델에게 여유를 주는 것임.

- 이전과 마찬가지로 라그랑지안을 다음과 같이 구성할 수 있다:  

$$\mathcal{L}(\mathbf{w},b,\boldsymbol{\xi},\boldsymbol{\alpha},\mathbf{r})=\frac{1}{2}\mathbf{w}^T\mathbf{w}+C\sum_{i=1}^{n}\xi_i-\sum_{i=1}^{n}\alpha_i\left(y_i(\mathbf{w}^T\mathbf{x}_i+b)-1+\xi_i\right)-\sum_{i=1}^{n}r_i\xi_i$$
- 여기서 $\alpha_i$와 $r_i$는 라그랑주 승수이며, 모두 $0$ 이상으로 제한된다.
- 또한, 원시 변수 $\mathbf{w}, b, \boldsymbol{\xi}$에 대해 라그랑지안을 최소화하고, 이후 승수들에 대해 최대화한다.

- 𝜉을 컨트롤 해주는 값이 C 값임. trade-off를 컨트롤 함.
- C 가 크면 모델을 더 정확하게 fit 하게 만드는 것.

- $\mathbf{w}$와 $b$에 대한 미분을 0으로 두면 다음을 얻는다:  

$$\mathbf{w}=\sum_{i=1}^{n}\alpha_i y_i \mathbf{x}^{(i)},\quad \sum_{i=1}^{n}\alpha_i y_i=0$$
- $\xi_i$에 대해 미분하면 다음을 얻는다:  

$$C-\alpha_i-r_i=0,\quad r_i=C-\alpha_i$$
- 이 시점에서 $r_i$는 $\alpha_i$에 의해 결정된다. 또한 $r_i\ge 0$이므로 다음이 성립한다:

$$0\le \alpha_i\le C$$

- 이 조건들을 라그랑지안에 다시 대입하면 $\mathbf{w}, b, \boldsymbol{\xi}$가 제거되고, $\boldsymbol{\alpha}$에 대해서만 표현된 문제가 남는다.
- 그 결과 얻어지는 쌍대 문제는 다음과 같다:  

$$\max_{\boldsymbol{\alpha}}\ \sum_{i=1}^{n}\alpha_i-\frac{1}{2}\sum_{i,j=1}^{n}y_i y_j \alpha_i \alpha_j \mathbf{x}_i^T\mathbf{x}_j$$  

$$\text{subject to}\quad 0\le \alpha_i\le C,\quad i=1,\ldots,n$$  

$$\sum_{i=1}^{n}\alpha_i y_i=0$$

### Kernel Methods
- 지금까지 우리는 결정 경계가 입력에 대한 선형 함수라고 가정하였다.
- 즉, 분류기는 다음과 같은 형태를 가진다:  

$$f(\mathbf{x})=\mathbf{w}^T\mathbf{x}+b$$
- 그리고 결정 경계는 다음과 같다:  

$$\mathbf{w}^T\mathbf{x}+b=0$$

- 커널 방법이 SVM에 대표적인 방법임.
- 커널도 꽤 어려운 내용임.
- 피쳐들이 선형적으로 분포 되어 있으면 비교적 쉬움. 선만 구하면 됨.

- 그러나 많은 실제 데이터셋은 선형적으로 분리되지 않는다.    
- 예를 들어, 한 클래스가 다른 클래스 내부에 원형 클러스터 형태로 존재한다면, 직선(또는 초평면)으로는 이를 올바르게 분리할 수 없다.    
- 이를 해결하기 위해서는 비선형 결정 경계가 필요하다.    
- 비선형 분류기는 결정 경계를 곡선 형태(예: 이차식, 다항식 또는 더 복잡한 형태)로 만들 수 있으며, 원래 입력 변수에 대해 선형으로 제한되지 않는다.

- 이런 데이터는 리니어 모델로 구할 수 없음
- 사실 딥러닝모델은 레이어를 쌓을때 non linear 를 사용 해서 최종으로 가면 linear 한 식으로 만들 어줌.
- 머신러닝에서는 커널 트릭을 사용 

- 이를 달성하는 한 가지 방법은 원래 입력 $\mathbf{x}$를 사상 $\phi(\mathbf{x})$를 통해 더 높은 차원의 특징 공간으로 변환한 뒤, 그 공간에서 선형 분류기를 적용하는 것이다: 

$$f(\mathbf{x})=\mathbf{w}^T\phi(\mathbf{x})+b$$
- 이러한 아이디어는 커널 방법(kernel method)으로 이어진다.

- 데이터의 스페이스를 변경 하고 리니어 방법을 적용.
- 커널 트릴을 쓸 수 있는 이유가 듀얼 수식을 사용하다 보면 커널 수식으로 쉽게 바꿀 수 있음음

- 커널이 실제로 어떻게 작동하는지 이해하기 위해, 먼저 회귀(regression)의 간단한 예를 살펴보자.
- 다음과 같은 3차 함수(cubic function)를 고려하자:  

$$y=\theta_3 x^3+\theta_2 x^2+\theta_1 x+\theta_0$$
- 겉보기에는 비선형처럼 보이지만, 다음과 같은 특징 사상을 정의하면:  

$$\phi(\mathbf{x})=\begin{bmatrix}1, x, x^2, x^3\end{bmatrix}^T\in\mathbb{R}^4,\quad \boldsymbol{\theta}=\begin{bmatrix}\theta_0, \theta_1, \theta_2, \theta_3\end{bmatrix}^T$$
- 3차 함수는 다음과 같이 쓸 수 있다:  

$$y=\boldsymbol{\theta}^T\phi(\mathbf{x})$$

- 여기서 핵심 아이디어는, 원래 입력 공간에서는 비선형 모델이 특징 변환 이후에는 선형 모델로 표현될 수 있다는 것이다.

- 이제 데이터로부터 매개변수 $\boldsymbol{\theta}$를 학습한다고 가정하자.
- 일반적인 방법은 경사하강법(gradient descent)을 사용하여 제곱 오차를 최소화하는 것이다.
- 보통의 선형 모델 $y=\boldsymbol{\theta}^T\mathbf{x}$에 대해, 경사하강법의 업데이트 규칙은 다음과 같다: 

$$\boldsymbol{\theta}=\boldsymbol{\theta}+\alpha\sum_{i=1}^{n}\left(y_i-\boldsymbol{\theta}^T\mathbf{x}_i\right)\mathbf{x}_i$$

- 여기서 $\alpha$는 학습률(learning rate)이다.

- 각 입력 $\mathbf{x}_i$를 변환된 특징 벡터 $\phi(\mathbf{x}_i)$로 대체하면, 학습 규칙의 구조는 변하지 않는다. 단지 다음과 같이 된다:  

$$\boldsymbol{\theta}=\boldsymbol{\theta}+\alpha\sum_{i=1}^{n}\left(y_i-\boldsymbol{\theta}^T\phi(\mathbf{x}_i)\right)\phi(\mathbf{x}_i)$$

- 따라서 특징 사상 $\phi$를 정의하면, 동일한 학습 알고리즘을 그대로 사용하면서 입력 공간 대신 특징 공간에서 작업할 수 있다.

- 여기서 각 훈련 예제마다 특징 벡터 $\phi(\mathbf{x}^{(i)})=\begin{bmatrix}1, x^{(i)}, (x^{(i)})^2, (x^{(i)})^3\end{bmatrix}$를 계산해야 한다.
- 이 간단한 3차 예제에서도, 원래의 선형 경우보다 계산량이 이미 더 커진다. 단순히 $\mathbf{x}$만 사용하는 대신, $\mathbf{x}$의 거듭제곱들을 반복적으로 계산하고, 추가 항들을 저장하며, 더 큰 차원의 매개변수 벡터를 업데이트해야 한다.
- 이제 특징의 개수가 4개가 아니라 50개, 100개, 또는 1000개라고 상상해보자. 동일한 학습 규칙은 여전히 적용되지만, 훨씬 더 큰 특징 벡터를 다뤄야 하므로 각 업데이트의 계산 비용이 증가한다.

- 그렇다면 과연 $\phi(\mathbf{x})$를 명시적으로 모두 계산할 필요가 있을까? 이러한 질문이 커널 트릭(kernel trick)의 동기가 된다.

- $\phi(\mathbf{x})$를 명시적으로 구성하지 않는 방법을 이해하기 위해, 경사하강법 업데이트 규칙을 다시 보자:  

$$\boldsymbol{\theta}=\boldsymbol{\theta}+\alpha\sum_{i=1}^{n}\left(y_i-\boldsymbol{\theta}^T\phi(\mathbf{x}_i)\right)\phi(\mathbf{x}_i)$$
- 만약 $\boldsymbol{\theta}=\mathbf{0}$으로 초기화하고 이 업데이트를 반복 적용하면, 다음과 같은 형태를 갖게 됨을 알 수 있다:  

$$\boldsymbol{\theta}=\sum_{j=1}^{n}\beta_j\phi(\mathbf{x}_j)$$

- 여기서 $\beta_j$는 각 훈련 예제의 특징 벡터 $\phi(\mathbf{x}_j)$가 $\boldsymbol{\theta}$에 얼마나 기여하는지를 결정하는 스칼라 계수이다.

- 다음으로, 이 표현을 예측 항에 대입하면:  

$$\boldsymbol{\theta}^T\phi(\mathbf{x}_i)=\sum_{j=1}^{n}\beta_j \phi(\mathbf{x}_j)^T\phi(\mathbf{x}_i)=\sum_{j=1}^{n}\beta_j\langle \phi(\mathbf{x}_j),\phi(\mathbf{x}_i)\rangle$$
- 이를 업데이트 규칙에 다시 대입하면, 모든 항이 동일한 특징 벡터 $\phi(\mathbf{x}_i)$의 선형 결합으로 표현되므로 $\beta_i$만 갱신하면 된다. 그 결과 계수 업데이트 식은 다음과 같다:  

$$\beta_i=\beta_i+\alpha\left(y_i-\sum_{j=1}^{n}\beta_j\langle \phi(\mathbf{x}_j),\phi(\mathbf{x}_i)\rangle\right)$$

- 여기서 커널 함수(kernel function)를 다음과 같이 정의할 수 있다:  

$$K(\mathbf{x},\mathbf{z})=\langle \phi(\mathbf{x}),\phi(\mathbf{z})\rangle$$
- 커널 함수는 변환된 두 특징 벡터의 내적을 계산하지만, 이를 원래 입력 $\mathbf{x}$와 $\mathbf{z}$만을 사용하여 직접 계산한다.
- 이제 3차 예제를 다시 살펴보고, 다음과 같은 3차 특징 사상을 선택한다고 가정하자:  

$$\phi(\mathbf{x})=\begin{bmatrix}1, 3x, 3x^2, x^3\end{bmatrix}^T$$

- 두 입력 $\mathbf{x}$와 $\mathbf{z}$를 취하면, 변환된 특징 벡터는 다음과 같다:  

$$\phi(\mathbf{x})=\begin{bmatrix}1, 3x, 3x^2, x^3\end{bmatrix}^T,\quad \phi(\mathbf{z})=\begin{bmatrix}1, 3z, 3z^2, z^3\end{bmatrix}^T$$
- 이제 이들의 내적을 계산하면:  

$$\langle \phi(\mathbf{x}),\phi(\mathbf{z})\rangle=1+3xz+3x^2z^2+x^3 z^3=(1+xz)^3$$
- 따라서 4차원의 특징을 직접 계산하는 대신, 다음과 같이 간단히 계산할 수 있다:  

$$K(\mathbf{x},\mathbf{z})=(1+xz)^3$$

- 커널은 고차원 특징을 명시적으로 계산하지 않고도 강력한 표현을 사용할 수 있게 해주기 때문에 유용하다.
- 복잡한 특징으로 데이터를 변환하는 대신, 두 입력 간의 유사도를 측정하는 함수 $K(\mathbf{x},\mathbf{z})$만 계산하면 된다.
- 그러나 모든 유사도 함수가 유효한 커널은 아니며, 어떤 함수가 특정 특징 공간에서의 내적처럼 동작하는지 판단할 필요가 있다.
- 어떤 함수가 유효한 커널이 되기 위해서는, 임의의 유한한 데이터 집합에 대해 $K(\mathbf{x},\mathbf{z})$로 구성된 행렬이 대칭(symmetric)이고 양의 준정부호(positive semidefinite)여야 한다.
- 유효한 커널의 예로는 선형 커널, 다항 커널, 그리고 가우시안(RBF) 커널이 있다.

### Support Vector Machines with Kernel Trick
- 다시 SVM으로 돌아가면, 목표는 두 클래스의 데이터 포인트를 분리하는 최적의 초평면을 찾는 것이다.

- 데이터가 선형적으로 분리 가능하다면, SVM은 원래 입력 공간에서 선형 결정 경계를 찾는다.

- 선형 SVM의 결정 함수는 다음과 같이 표현된다:  

$$f(\mathbf{x})=\mathbf{w}^T\mathbf{x}+b$$
- 여기서 $\mathbf{w}$는 초평면에 수직인 법선 벡터이고, $b$는 바이어스(bias) 항이다.



- 최적화 문제를 풀고 나면, 결정 함수는 다음과 같이 표현할 수 있다:  

$$f(\mathbf{x})=\mathbf{w}^T\mathbf{x}+b=\sum_{i=1}^{n}\alpha_i y_i \mathbf{x}_i^T\mathbf{x}+b=\sum_{i=1}^{n}\alpha_i y_i \langle \mathbf{x}_i,\mathbf{x}\rangle + b$$
- 여기서 $\alpha_i$는 라그랑주 승수이다.

- 데이터가 원래 공간에서 선형 분리되지 않는 경우, 특징 사상 $\phi$를 사용하여 더 높은 차원의 특징 공간으로 매핑한다.

- 이때 결정 함수는 다음과 같이 표현된다:  

$$f(\mathbf{x})=\mathbf{w}^T\phi(\mathbf{x})+b=\sum_{i=1}^{n}\alpha_i y_i \phi(\mathbf{x}_i)^T\phi(\mathbf{x})+b=\sum_{i=1}^{n}\alpha_i y_i \langle \phi(\mathbf{x}_i),\phi(\mathbf{x})\rangle + b$$

- 여기서 커널 함수 $K$를 사용하면 다음과 같이 쓸 수 있다:  

$$f(\mathbf{x})=\sum_{i=1}^{n}\alpha_i y_i K(\mathbf{x}_i,\mathbf{x})+b$$



- 이 접근법을 통해 SVM은 계산 효율성을 유지하면서도 비선형 결정 경계를 학습할 수 있다.    
- 앞서 언급했듯이, SVM은 다양한 비선형 커널 함수를 사용할 수 있으며, 대표적으로 다항 커널(polynomial kernel), 방사 기저 함수(RBF, Gaussian) 커널, 시그모이드 커널 등이 있다.

- 보통 커널을 사용하면 고차원으로 데이터 분포를 만듦.
- 커널의 종류 매우 다양 함.
- 이 2d 데이터를  Radial Basis Function (RBF) 등을 사용해서 3d로 만들는데 모양을 벨커브 형태의 오목하게 만듦.



- 커널을 이용해서 곡선을 만들수가 있음.
- 데이터가 복잡하면 RBF 커널 많이 사용함. 

### Multi-Class Support Vector Machines
- 지금까지 우리는 이진 분류(binary classification)를 위한 SVM을 다루었으며, 이때 레이블은 보통 다음과 같이 주어진다:  

$$y\in{-1,+1}$$

- 그러나 많은 실제 문제는 두 개 이상의 클래스를 포함한다.
- 표준 SVM은 이진 분류를 위해 설계되었기 때문에, 이를 다중 클래스 문제로 확장하기 위한 전략이 필요하다.
- 이전까지 SVM을 바이너리만 알아봤는데 멀티 클래스도 가능

- SVM을 다중 클래스 문제로 확장하는 간단한 방법 중 하나는 문제를 여러 개의 이진 분류 문제로 나누는 것이다.
    
- one-versus-rest 방식에서는 클래스가 $K$개일 때, $K$개의 서로 다른 SVM을 학습한다. 각 클래스 $k$에 대해 해당 클래스의 데이터는 $+1$, 나머지는 $-1$로 라벨링한다.
    
- 예측 단계에서는 모든 $K$개의 분류기를 평가한 뒤, 입력 $\mathbf{x}$에 대해 가장 큰 결정 함수 값을 가지는 클래스로 할당한다.

- one-versus-rest approach: 
	- 첫번째 classfier를 독립적으로 학습 다음에 다른 classfier를 학습함.
	- 총 k개의 classfier를 만들게 됨.
	- 이 k개의 classfier를 합침


- 또 다른 일반적인 전략은 one-versus-one 방식이다.

- 이 방법에서는 모든 클래스 쌍에 대해 이진 SVM을 학습하며, 총 분류기의 개수는 다음과 같다:  

$$\frac{K(K-1)}{2}$$

- 각 분류기는 두 특정 클래스만을 구분한다.

- 예측 단계에서는 모든 분류기가 투표를 수행하고, 가장 많은 표를 얻은 클래스가 최종 선택된다.

- one-versus-one
- 첫번째 classfier를만들때 초록은 무시하고 빨강 파랑만 분류
- 그 다음 조합으로 학습습

- 그렇다면 어떤 방법이 더 나을까?
    
- one-versus-rest 방식에서는 각 분류기가 하나의 클래스와 나머지 모든 클래스를 구분해야 하므로, 크고 불균형한 음성(negative) 데이터 집합을 다뤄야 한다. 이는 학습을 더 어렵게 만들 수 있다.
    
- 반면 one-versus-one 방식은 클래스 쌍마다 분류기를 학습하므로, 각 문제는 더 단순하고 더 정확한 결정 경계를 만들 수 있는 경우가 많다. 하지만 모델의 수가 많아지기 때문에 학습과 예측 시간이 증가하는 단점이 있다.
    
- 실제로 scikit-learn에서는 두 방법의 성능이 대체로 비슷하지만, one-versus-rest 방식이 훨씬 빠르기 때문에 자주 선호된다고 언급한다.

 - one-versus-rest
	 - 클래스가 많아 질 수록 복잡해짐
	 - classfier가 적다는 장점이 잇음.
	 - 계산이 빨라서 좀 더 선호
- 싸이킷 런 홈페이지 보면 거의 성능은 비슷하다고 되어 있음.



