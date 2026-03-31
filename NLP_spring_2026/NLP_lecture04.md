2026-03-30 08:20
## 4강 Embeddings

### Sparse vs. Dense Vectors
- 둘의 개념을 알아야 함.

### Count-based Vector Limitations
- 지금까지 배운 벡터화 방법은 다 카운트 기반임.
- 카운트 기반 벡터(count-based vectors)는 희소하다(0이 매우 많다)    
	- 벡터 내의 0 값은 의미 정보를 담고 있지 않다    
- 카운트 기반 벡터는 길다(차원이 매우 많다)    
	- 벡터의 차원 수는 어휘 크기와 같으며(보통 $>10{,}000$), 매우 크다    
	- 차원의 저주(curse of dimensionality): 고차원에서는 코사인 유사도와 같은 거리/유사도 척도가 덜 의미 있게 된다
- 의미 없는 0 이 많음 -> 의미없는 차원이 많다.
- 결국 디멘전도 커짐.
- 영어에서 유니크 워드는 10,000개가 넘음.
	- 디멘젼이 1만개 이상이 되어 curse of dimensionality에 걸리고 다루기도 어려워짐.

| 항목          | aardvark | computer | data | result | pie | sugar |
| ----------- | -------- | -------- | ---- | ------ | --- | ----- |
| cherry      | 0        | 2        | 8    | 9      | 442 | 25    |
| strawberry  | 0        | 0        | 0    | 1      | 60  | 19    |
| digital     | 0        | 1670     | 1683 | 85     | 5   | 4     |
| information | 0        | 3325     | 3982 | 378    | 5   | 13    |


### Dense Vectors
- 더 효율적이고 효과적인 벡터 표현 방법
- sparse vector의 반대라고 보면 됨.
- 밀집 벡터(dense vectors)    
	- 벡터의 대부분 또는 모든 차원이 0이 아니다    
	- 일반적으로 부동소수점 값이며, 각 차원은 양수 또는 음수가 될 수 있다    
	- 희소 벡터보다 훨씬 작은 차원을 가진다(즉, $\ll 10{,}000$)    
- 분산 표현(distributed representations)이라고도 불린다    
	- 정보가 여러 차원에 분산되어 표현된다  
		- 주변 디멘전과 여러 디멘전에 걸쳐 값이 분포 되어 있음.
	- 각 차원(unit/dimension)은 여러 정보 표현에 동시에 기여한다    
	- 인간의 뇌와 유사하다: 특정 개념을 하나의 뉴런/영역이 아니라, 여러 뉴런의 네트워크에 걸쳐 분산하여 저장하고 처리한다
- sparse vector와 다르게 값이 거의 다 있음.
- 훨씬 작은 차원을 갖지만 축소하여 벡터를 만듦.

- 하나의 차원은 (부분적으로) 동물(“cat”, “dog”)과 탈것(“car”, “truck”)을 구분하는 데 기여할 수 있다    
- 또 다른 차원은 (부분적으로) 크기와 같은 속성을 포착할 수 있다    
- 다른 차원은 (부분적으로) 격식성이나 감정적 톤을 나타낼 수 있다    
- 이러한 각 차원은 특정 개념 하나만을 전적으로 담당하지 않으며, 함께 결합되어 단어에 대한 풍부하고 정교한 표현을 형성한다  

$$  
v_{\text{good}}=[-1.34,,2.58,,0.37,,4.32,,-3.21,,\dots]  
$$
$$  
v_{\text{nice}}=[-0.58,,1.97,,0.20,,3.13,,-2.58,,\dots]  
$$
   - (일반적으로 부동소수점 값이므로 소수 둘째 자리까지만 표시한 예시이다)
   - 굿이나 나이스는 유사한 의미를 지니기 때문에 각 디멘젼의 값이 유사함을 알 수 있음
	   - 그러면 벡터 평면에서 근처에 위치함.

### Dense Vectors Pros & Cons
- (+) 압축성(compactness): 더 적은 자원으로 많은 개념을 표현할 수 있으며(각 차원이 더 풍부한 의미 정보를 담음), 신경망의 특징(feature)으로 사용하기 쉽다    
- (+) 견고성(robustness): 정보가 여러 차원에 분산되어 있어 개별 차원의 잡음이나 무작위성에 더 강하다    
	- 노이즈에 강함. -> 노이즈가 여러 차원에 분산되어 작용하기 때문에 영향이 작음.
- (+) 확장성 및 일반화(scalability & generalization): 대규모 데이터를 효율적으로 처리하고 다양한 응용으로 일반화할 수 있다    
- (-) 해석 가능성 부족(lack of interpretability): (희소 벡터와 달리) 각 차원에 명확한 의미를 부여하기 어려워 모델 해석이 어렵다
	- 결과론 적으로 해석해야 함.
	- sparse vector는 두개의 단어가 같이 나왔다 이런 식으로 해석이 가능하지만 dense vector는 안됨.

### Distributional Hypothesis
- 유사한 맥락에서 등장하는 단어들은 유사한 의미를 가지는 경향이 있다  -> Word Embeddings의 가장 중요한 가정임.
- 단어의 의미는 그 단어가 함께 등장하는 주변 단어들(맥락)에 의해 크게 정의된다    
- 예시: “Ong choy”의 의미를 모른다고 가정하자    
	- “Ong choy is delicious sautéed with garlic”    
	- “Ong choy is superb over rice”    
	- “… ong choy leaves with salty sauces”    
- 다음과 같은 맥락을 이미 알고 있다고 하자    
	- “… spinach sautéed with garlic over rice”    
	- “… chard stems and leaves are delicious”    
	- “… collard greens and other salty leafy greens”    
- 따라서 “Ong choy” = water spinach(공심채)이다
- 시금치와 비슷한 맥락에서 등장하면 비슷한 채소임을 유추함.

### Word Embeddings: General Idea
- 분포 가설(distributional hypothesis)에 기반하여 단어의 밀집 벡터 표현을 학습한다    
- 의미적으로 유사한 단어(맥락 유사성 기준)는 유사한 벡터 표현을 가진다    
- 임베딩(embedding): 한 공간의 원소를 다른 공간의 표현으로 매핑하는 함수 또는 과정

$$  
\begin{align}  
v_{\text{to}} &= [1,0,0,0,0,0,\dots] \\  
v_{\text{by}} &= [0,1,0,0,0,0,\dots] \\  
v_{\text{that}} &= [0,0,1,0,0,0,\dots] \\ 
v_{\text{good}} &= [0,0,0,1,0,0,\dots] \\  
v_{\text{nice}} &= [0,0,0,0,1,0,\dots] \\  
v_{\text{bad}} &= [0,0,0,0,0,1,\dots]  
\end{align}  
$$
- dense vector representations of words를 구현 하는 것임.
- 비슷한 문맥에서 등장하는 단어는 결과적으로 비슷한 벡터값을 갖게 됨.
- 이를 임베딩이라고 부름.



### Learning Word Embeddings
- 대규모 텍스트 말뭉치(예: Wikipedia)가 있다고 가정한다    
- 유사한 맥락에서 등장하는 단어들에 대해 유사한 단어 임베딩(embeddings)을 학습하고자 한다    
- Construct a prediction task(예측 과제를 구성한다): 중심 단어(center word)의 임베딩을 사용하여 그 주변 맥락을 예측한다    
- 직관: 두 단어의 임베딩이 유사하다면, 유사한 맥락을 예측하게 되고, 따라서 의미적으로도 유사하다  

$$  
v_{\text{ong choy}} \rightarrow {\text{sautéed},\ \text{garlic},\ \text{rice},\ \text{salty},\ \text{leaves},\ \dots}  
$$  
$$  
v_{\text{spinach}} \rightarrow {\text{sautéed},\ \text{garlic},\ \text{rice},\ \text{salty},\ \text{leaves},\ \dots}  
$$



### Word Embedding Is Self-Supervised Learning
- 자기지도 학습(self-supervised learning): 입력의 일부를 사용하여 같은 입력의 다른 부분을 예측하도록 모델을 학습시키는 방법    
	- 입력: “Ong choy is superb over rice”    
	- 예측 과제: “Ong choy” → ${\text{is},\ \text{superb},\ \text{over},\ \text{rice}}$    
- 인풋이 들어왔을때 인풋의 특정 파트를 이용해서 다른 파트를 예측하게 함.
- 이때 사람이 labeling 할 필요 없이 예측함.
- 자기지도 학습 vs. 지도 학습:    
	- 자기지도 학습: 사람에 의해 라벨링된 데이터가 필요 없으며, 데이터 자체의 구조로부터 감독 신호를 생성하여 학습한다    
	- 지도 학습: 사람이 라벨링한 입력-출력 쌍을 사용하여 학습한다
- 워드 임베딩은 현대 언어의 입력을 구성하는 가장 기본 적인 방법임.
- 입력되는 각각의 단어들은 워드 임베딩으로 변환되고 그 다음에 모델에 인풋이 되고 작동 하게 됨.

### Word2Vec 
- 단어를 벡터화 한다는 뜻.

### Word embeddings: general idea

- 목표: 분포 가설(distributional hypothesis)에 기반하여 단어의 밀집 벡터 표현을 학습하는 것이다    
- 의미적으로 유사한 단어(즉, 유사한 맥락에서 등장하는 단어)는 유사한 벡터 표현을 가진다    
- 단어 임베딩(word embeddings): 각 행이 하나의 단어에 대한 밀집 벡터를 나타내는 행렬이다    
- 이는 한 공간(어휘 집합)의 원소를 다른 공간(벡터 공간)의 표현으로 매핑하는 것으로 볼 수 있다
- 임베딩 테이블이 결과 물로 나옴. 행의 개수는 단어의 수임.
	- 958번째 단어는 958번째 행에 나옴.

### Constructing word-context information

- 문맥 윈도우 내에서 한 단어가 다른 특정 단어와 함께 등장하는 빈도를 계산한다    
- 윈도우 크기(window size): 중심 단어(target word)의 좌우에서 고려하는 최대 맥락 단어 수   
- 예시
	- 윈도우 크기 $=2$
	- 중심 단어(target word)=“Taylor"
- 입력 문장: “Taylor releases a new pop album with a hit song”
- word-word co-occurrence 쌍:    
	- $(\text{Taylor}, \text{releases}), (\text{Taylor}, \text{a})$    
	- $(\text{releases}, \text{Taylor}), (\text{releases}, \text{a}), (\text{releases}, \text{new})$    
	- $(\text{a}, \text{Taylor}), (\text{a}, \text{releases}), (\text{a}, \text{new}), (\text{a}, \text{pop})$    
	- $(\text{new}, \text{releases}), (\text{new}, \text{a}), (\text{new}, \text{pop}), (\text{new}, \text{album})$    
	- $\dots$    
	- $(\text{song}, \text{a}), (\text{song}, \text{hit})$

### Constructing word-context information
- 공기어 빈도(co-occurrence count)를 기반으로 단어-단어 공기어 행렬을 구성한다   
	- 행도 V벡터 열도 V벡터
- 행렬의 크기는 $|V|\times |V|$이며, $V$는 어휘 집합의 크기이다    
- 각 원소는 특정 단어(행)가 다른 단어(열)와 문맥 윈도우 내에서 함께 등장한 횟수를 나타낸다  

| term    | wizard | spell | the | magic | and | album | song | release |
| ------- | ------ | ----- | --- | ----- | --- | ----- | ---- | ------- |
| wizard  | 0      | 4     | 7   | 5     | 6   | 0     | 0    | 0       |
| spell   | 4      | 0     | 6   | 3     | 5   | 0     | 0    | 0       |
| the     | 7      | 6     | 0   | 5     | 8   | 5     | 6    | 6       |
| magic   | 5      | 3     | 5   | 0     | 7   | 0     | 0    | 0       |
| and     | 6      | 5     | 8   | 7     | 0   | 6     | 7    | 7       |
| album   | 0      | 0     | 5   | 0     | 6   | 0     | 6    | 3       |
| song    | 0      | 0     | 6   | 0     | 7   | 6     | 0    | 2       |
| release | 0      | 0     | 6   | 0     | 7   | 3     | 2    | 0       |
- 이 테이블도 벡터로 쓸수 있지만 sparse vector 0도 많고 너무 큼

- co-occurrence count를 기반으로  word-word co-occurrence 행렬을 구성한다    
- 행렬의 크기는 $|V|\times |V|$이며, $V$는 어휘 집합의 크기이다    
- 각 원소는 특정 단어(행)가 다른 단어(열)와 문맥 윈도우 내에서 함께 등장한 횟수를 나타낸다


### Generating dense word embeddings
- 이제 이 크고 희소한 행렬을 어떻게 밀집 단어 임베딩으로 변환할 수 있을까?    
- 두 가지 접근 방법을 살펴본다    
	- 1. 차원 축소(dimensionality reduction)        
		- 공기어 행렬을 정규화한 뒤, 절단된 SVD(truncated SVD)를 적용하여 차원을 축소한다    
		- 각 행(필요에 따라 특이값으로 스케일링됨)이 단어 임베딩으로 사용된다    
		- 텍스트 마이닝 수업에서는 소개하지만 자연어 처리에서는 수업 안함.
	- 2. Skip-gram 학습        
		- 행렬을 분해하는 대신, 단어-맥락 쌍으로부터 직접 임베딩을 학습한다    
		- 주어진 중심 단어로부터 주변 맥락 단어를 예측하도록 모델을 학습한다    
- Word2Vec으로 구현된다    
- 실제로 이 두 접근법은 수학적으로 동등한 것으로 볼 수 있다


### Approach 2: Skip-gram learning
- 핵심 아이디어: 중심 단어(center word)를 사용해 주변 맥락 단어(context words)를 예측한다 
- 의미적으로 유사한 중심 단어는 유사한 맥락 단어를 예측하게 된다    
- 예시 문장: “Taylor releases a new pop album with a hit song”    
- 학습용 단어-맥락 쌍(word-context pairs):    
	- $(\text{Taylor}, \text{release}), (\text{Taylor}, \text{a})$    
	- $(\text{release}, \text{Taylor}), (\text{release}, \text{a}), (\text{release}, \text{new})$    
	- $(\text{a}, \text{Taylor}), (\text{a}, \text{release}), (\text{a}, \text{new}), (\text{a}, \text{pop})$    
	- $(\text{new}, \text{release}), (\text{new}, \text{a}), (\text{new}, \text{pop}), (\text{new}, \text{album})$    
	- $(\text{song}, \text{a}), (\text{song}, \text{hit})$
- skip이란 단어가 들어간 이유는 윈도우 사이즈를 벗어나면 그 단어들은 다 skip하기 때문에 네이밍 함.

- 핵심 아이디어: 중심 단어를 사용하여 맥락 단어를 예측한다 (의미적으로 유사한 중심 단어는 유사한 맥락 단어를 예측한다)    
- 목적 함수: 중심 단어 $w$가 주어졌을 때 맥락 단어 $c$를 예측할 확률을 최대화한다  

$$  
\max_{\theta}\ \prod_{(w,c)\in D} p_{\theta}(c \mid w)  
$$
   
- $D$: 공기어 쌍(co-occurrence pairs)의 전체 집합    
- $\theta$: 학습해야 할 단어 임베딩(모델 파라미터)    -> 열벡터 테이블블
- c: context
- w: center word
- -학습용 단어-맥락 쌍(word-context pairs):    
	- $(\text{Taylor}, \text{release}), (\text{Taylor}, \text{a})$    
	- $(\text{release}, \text{Taylor}), (\text{release}, \text{a}), (\text{release}, \text{new})$    
	- $(\text{a}, \text{Taylor}), (\text{a}, \text{release}), (\text{a}, \text{new}), (\text{a}, \text{pop})$    
	- $(\text{new}, \text{release}), (\text{new}, \text{a}), (\text{new}, \text{pop}), (\text{new}, \text{album})$    
	- $(\text{song}, \text{a}), (\text{song}, \text{hit})$  
- 이 확률을 어떻게 표현할 것인가?
- 각 단어는 두 개의 밀집 벡터를 가진다    
- 모델링 할때는 2개의 벡터 테이블을 만들어야 함.
	- 하나는 중심 단어(center word) 역할을 위한 벡터, 다른 하나는 맥락 단어(context word) 역할을 위한 벡터이다    
- 로그 확률이 벡터 내적에 비례한다고 가정한다

$$  
\log p_{\theta}(c \mid w)\propto v_c \cdot v_w  
$$
- 유사도 계산은 벡터의 내적을 사용함.
- 센터벡터와 맥락(context)단어의 벡터를 내적
- log는 계산의 편의를 위해 사용하고 특별한 의미가 있는 것은 아님.


- 목적 함수: 중심 단어 $w$를 사용하여 맥락 단어 $c$를 예측할 확률을 최대화한다  

$$  
\max_{\theta}\ \prod_{(w,c)\in D} p_{\theta}(c \mid w)  
$$

- 로그 확률이 벡터 내적에 비례한다고 가정한다    
- 각 $(w,c)$ 쌍에 대해:  

$$  
\log p_{\theta}(c \mid w)\propto v_c \cdot v_w  
$$
- 다른 모든 맥락 단어 $(c')$에 대해:  

$$  
\log p_{\theta}(c' \mid w)\propto v_{c'} \cdot v_w  
$$

- 테일러와 릴리즈는 같은 context에서 나온 단어인데 다른 context c'에서도 예측을 할 수 있게 됨.

- p(c|w)를 다 계산하면 확률 분포를 얻을 수 있음.
- 최종 확률 분포는 소프트맥스(softmax) 함수로 정의된다  

$$  
p_{\theta}(c \mid w)=\frac{\exp(v_c \cdot v_w)}{\sum_{c' \in V} \exp(v_{c'} \cdot v_w)}  
$$
- 모든 단어를 내적해서 분모에 넣고 normalize를 함.
	- 전체 어휘 집합에 대해 정규화하여 확률 분포를 만든다 

$$  
\sum_{c' \in V} p_{\theta}(c' \mid w)=1  
$$
- 계산 하고 나면 소프트 맥스 형식의 함수를 얻게 됨.
- 소프트맥스 함수:  

$$  
\mathrm{softmax}(x_i)=\frac{\exp(x_i)}{\sum_j \exp(x_j)}=p_i,\quad \sum_i p_i=1  
$$


- 최적화 함수로 사용 할 수 있음.
	- loss를 최소화 함. 
	- 데이터에 등장한 단어들은 높게 안나왔던 단어(c')들은 낮게
- 단어 임베딩 학습을 최적화 문제(negative log)로 정식화할 수 있다  

$$  
\min_{\theta}\ \mathcal{L}(\theta)  
= - \sum_{(w,c)\in D} \log p_{\theta}(c \mid w)  
= - \sum_{(w,c)\in D} \left( v_c \cdot v_w - \log \sum_{c' \in V} \exp(v_{c'} \cdot v_w) \right)  
$$

- $D$: 전체 공기어 쌍의 집합
- $\theta={v_w, v_c}$: 학습해야 할 단어 임베딩
- 확률은 다음과 같이 정의된다  

$$  
p_{\theta}(c \mid w)=\frac{\exp(v_c \cdot v_w)}{\sum_{c' \in V} \exp(v_{c'} \cdot v_w)}  
$$

- 단어 임베딩 학습을 최적화 문제(negative log)로 정식화한다  

$$  
\min_{\theta}\ \mathcal{L}(\theta)  
= - \sum_{(w,c)\in D} \log p_{\theta}(c \mid w)  
= - \sum_{(w,c)\in D} \left( v_c \cdot v_w - \log \sum_{c' \in V} \exp(v_{c'} \cdot v_w) \right)  
$$

- 최적화 방법: 경사 하강법(gradient descent)
- 그래디언트 $\nabla_{\theta}\mathcal{L}(\theta)$는 손실을 가장 크게 증가시키는 방향이다
- 알고리즘:
	- 파라미터 $\theta$를 무작위로 초기화한다
	- 수렴할 때까지 반복한다  

$$  
\theta \leftarrow \theta - \eta \nabla_{\theta}\mathcal{L}(\theta)  
$$

- $\theta$는 학습 파라미터, $\eta$는 학습률(하이퍼파라미터)이다

- $\mathcal{L}(\theta)$ 를 최소화 하려면 기울기를 최소화하는 방향으로 구하면 됨.
	- 기울기는 그래프를 가장 빠르게 증가시키는 값임. - 값으로 해서 기울기가 가장 낮은 값으로 갈 수 있음.
- 목적 함수(손실 함수) $\mathcal{L}(\theta)$가 주어져 있다    
- 경사 하강법(gradient descent)은 $\mathcal{L}(\theta)$를 최소화하기 위한 반복적 최적화 알고리즘이다    
- 동작 방식: 현재 파라미터 $\theta$에서 $\mathcal{L}(\theta)$의 그래디언트를 계산하고, 그 음의 방향으로 작은 스텝을 이동한 뒤 이를 반복한다    
- 알고리즘:    
	- 파라미터 $\theta$를 무작위로 초기화한다    
	- 수렴할 때까지 반복한다  

$$  
\theta \leftarrow \theta - \eta \nabla_{\theta}\mathcal{L}(\theta)  
$$
- $\theta$는 학습 파라미터, $\eta$는 스텝 크기(학습률, hyperparameter)이다
- 우리의 문제로 돌아가면, 손실 함수 $\mathcal{L}(\theta)$를 최소화하도록 파라미터 $\theta$를 업데이트한다  

$$  
\min_{\theta}\ \mathcal{L}(\theta)  
= - \sum_{(w,c)\in D} \left( v_c \cdot v_w - \log \sum_{c' \in V} \exp(v_{c'} \cdot v_w) \right)  
$$

- 예시: $(\text{Taylor}, \text{release})$ 쌍에 대해
	- 양의(실제 문맥에서 나온 단어_Taylor, releas) 쌍 $(w,c)$에 대해서는 내적 $v_c \cdot v_w$를 최대화한다
	- 음의(부정) 샘플(실제 문맥에서 안 나온 단어_zebra, panda) $(w,c')$에 대해서는 내적 $v_{c'} \cdot v_w$를 최소화한다


### Approach 2: Skip-gram learning (with negative sampling)
- Sum over the entire vocabulary – expensive!
- $\displaystyle \sum_{c' \in V}$ 계산하려면 for문 엄청 돌려 야 함.

- 네거티브는 다 고려 할 필요가 없음
	- 네거티브는 일부만 샘플링 함.
	- positive pair가 아닌 것들을 negative pair라고 함.
- 네거티브 샘플링(negative sampling): 전체 어휘를 사용하는 대신, 소수의 “부정 단어(negative words)”만 샘플링하여 업데이트에 사용한다    
- 즉, 모든 $c' \in V$를 고려하지 않고, 작은 부정 집합 $N$만 사용한다    
	- n이 4면 4개만 계산시 업데이트
	- 보통은 랜덤 샘플링 사용, 다른 샘플링 기법 사용 할 수 있음.
	- 그래디언트 디센트는 에폭마다 샘플링을 진행 하기 때문에 sample들이 어느정도 전체를 대표 할 수 있게 됨.
- 학습 시:    
	- 실제(양의) 쌍 $(w,c)$에 대해서는 $v_c \cdot v_w$를 크게 만든다    
	- 샘플링된 부정 쌍 $(w,c')$, $c' \in N$에 대해서는 $v_{c'} \cdot v_w$를 작게 만든다    
	- 이를 통해 계산 비용을 크게 줄이면서도 효과적인 학습이 가능하다


- 따라서 더 최적화하기 쉬운 근사 목적 함수를 사용한다
- 목적 함수를 이진 분류 문제로 재정식화한다: $(w,c)$가 실제 쌍인지 예측한다
	- 전체 단어에서 positive negative 판변이 아니라 단어쌍을 보고 바로 true, false 문제로 바꿈.
- $(w,c)$가 실제 쌍일 확률은 시그모이드 함수로 표현된다  

$$  
p_{\theta}(\text{True}\mid c,w)=\sigma(v_c \cdot v_w)=\frac{1}{1+\exp(-,v_c \cdot v_w)}  
$$

- 시그모이드 함수:  참일 확률

$$  
\sigma(z)=\frac{1}{1+\exp(-z)},\quad 1-\sigma(z)=\sigma(-z)  
$$

- $(w,c)$가 거짓 쌍일 확률:  1- 참일 확률
	- 계산이 단순해서 이진 분류에서 굉장히 선호 됨
    
$$  
p_{\theta}(\text{False}\mid c,w)=1-p_{\theta}(\text{True}\mid c,w)=\sigma(-,v_c \cdot v_w)  
$$

- 소프트 맥스는 모든 케이스를 보는것
- 시그모이드는 페어단위 기반
- an approximate objective
	- 진짜 목적함수(objective)를 직접 다루기 어렵기 때문에, 이를 대신하는 근사 함수
- 소프트 맥스에서 계산이 쉬운 시그모이드 기반 함수로 목적 함수를 바꿈
	- 효과는 비슷하고 계산은 매우 쉬워짐.
	- 전체 단어 비교가 필요 없음.
- 따라서 더 최적화하기 쉬운 근사 목적 함수를 사용한다
- 양의 쌍(실제로 함께 등장한 단어 쌍)의 확률은 최대화한다
- 음의 쌍(무작위로 샘플링된 잡음)의 확률은 최소화한다
- 소프트맥스 기반 목적 함수:  

$$  
\min_{\theta}\ \mathcal{L}(\theta)  
= - \sum_{(w,c)\in D} \left( v_c \cdot v_w - \log \sum_{c' \in V} \exp(v_{c'} \cdot v_w) \right)  
$$

- 시그모이드 기반(네거티브 샘플링) 목적 함수: 

$$  
\min_{\theta}\ \mathcal{L}(\theta)  
= - \sum_{(w,c)\in D} \left( \log \sigma(v_c \cdot v_w) + \sum_{c' \in N} \log \sigma(-,v_{c'} \cdot v_w) \right)  
$$

- $N$: 무작위로 샘플링된 부정 샘플 집합 ($|N|\ll |V|$, 보통 $5\sim10$)