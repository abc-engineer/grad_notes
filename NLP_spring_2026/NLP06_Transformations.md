2026-04-13 08:20
## 6강 Transformations

### Transformer: Overview
- Transformer는 특정한 시퀀스 모델링 아키텍처의 한 종류로, 심층 신경망(DNN)에 기반한다.   
- RNN의 순환 연산을 대체하기 위해 attention 메커니즘을 사용한다.    
- 언어 모델링에서 가장 중요한 아키텍처이며, 거의 모든 대형 언어 모델(LLM)이 Transformer를 기반으로 한다.

- 시퀀스 모델링을 하기 위한 대표 모델
- 지금 가장 대표적인 모델
- attention만 잘하면 모든 RNN을 대체 할 수 있다는 기념비 적인 논문이 나옴.
- RNN과거 정보와 새정보를 계속 연산
- transformer는 셀프 어텐션에 근간하여 연산함.

## Transformation_details

### Self-attention: The big picture
- 핵심 질문: 각 단어를 표현할 때 문맥(context)을 어떻게 반영할 것인가?    
- 직관: 주변 문맥의 일부 단어들이 타겟 단어의 의미를 이해하는 데 도움을 줌    
- 타겟 단어를 이해하기 위해 해당 문맥 단어들에 “주의(attention)”를 줄 필요가 있음    
- 자기어텐션(self-attention)의 핵심 아이디어: 각 단어는 동일 시퀀스 내의 다른 단어들에 주의를 기울임    
- 예시    
	- “We had a picnic on the grassy river bank.”에서 $\text{bank}$는 “강둑” 의미    
	- “I went to the bank and withdrew some cash.”에서 $\text{bank}$는 “금융기관” 의미    
	- 동일한 단어라도 문맥에 따라 서로 다른 벡터 표현으로 인코딩됨


- Self-attention은 트랜스포머의 가장 중요한 개념
- 일단은 한 단어를 이해 하려면 주변 몇개의 단어를 봐야 함.
- 피크닉, 강, 인출, 현금 등의 단어들이 bank의 뜻을 결정하게 해주는 결정적인 단어 들임.
- 같은 문장에 있는 주요 단어들의 context 에 집중한다는 뜻으로 self attention이라고 하게 됨.

- 정식화(instantiation): 타겟 단어 임베딩을 문맥 임베딩의 가중합으로 표현  

$$  
a_i = \sum_{x_j \in x} \alpha_{ij} x_j  
$$
- $a_i$: (문맥을 반영한) 중심 단어 임베딩
- $x_j$: 문맥 단어 임베딩
- $\alpha_{ij}$: 단어 $j$가 단어 $i$에 주는 어텐션 가중치  

$$  
\sum_{x_j \in x} \alpha_{ij} = 1  
$$

- 어텐션 가중치는 정규화되어 합이 1이 되며(확률분포의 의미 내포), 각 단어가 얼마나 중요한지를 나타냄

- 타겟 워드에 대해 주변 단어의 웨이티드 썸( weighted sum)을 사용 하면 셀프 어텐션을 구현 할 수 있음.
	- 즉 중요한 context에 높은 값을 할당하는 것.
- Static: 정적
	- 워드임베딩의 단어 그 자체
	- 맥락 정보 없음.
- Contextual 
	- 맥락을 반영했음.


- 어텐션 점수(attention score)는 벡터 내적에 softmax 함수를 적용하여 계산됨  

$$  
\alpha_{ij} = \mathrm{Softmax}(x_i \cdot x_j) = \frac{\exp(x_i \cdot x_j)}{\sum_{k} \exp(x_i \cdot x_k)}  
$$

- $\alpha_{ij}$: 단어 $i$가 단어 $j$에 부여하는 어텐션 가중치
- 유사한 단어일수록(내적 값이 클수록) 더 높은 가중치를 가짐
- 직관적으로, 문맥 임베딩은 입력 문장에서 “유사한” 단어들로부터 더 많은 정보를 반영
- 이 가중합은 문장의 모든 단어에 대해 동일하게 적용됨

- 어텐션 스코어는 어떻게 얻을까?
	- 워드 투 벡과 유사
	- 벡터간 내적해서 내적값이 크면 높은 점수
	- 즉 벡터 스페이스에서 가까이 있음.
- 합을 1로 만드는 분포형태로 하고 싶기 때문에 소프트맥스 함수를 사용해서 다 더해서 1이 나오게 함.
- a값이 크다는 것은 i를 이해 하기 위해 j에 더 가중치를 준다는 의미
- 웨이티드 썸은 모든 단어에 적용 함.
- RNN 에 비해 훨씬 유연함.
- RNN은 하나하나하나 다 업데이트 해야 함.
- 셀프 어텐션은 같은 문장을 한번에 봄. 롱텀 디펜던시를 잘 반영할 수 있음.

- 실제로는 추가적인 고려가 필요함    
- 동일한 임베딩 $x$를 사용하여 어텐션을 계산하면, 단어는 자기 자신과의 내적 값이 크기 때문에 거의 항상 자기 자신에 강하게 어텐션을 부여하게 됨

- 그냥 연산을 하면 모델이 잘 돌아 가지 않음
- 자기 자신과 내적이 너무 큰 값을 갖게 됨.
- 맥락 정보가 효과적으로 전달 되지 않음.
	- Query, Key, and Value 디자인이 등장 함.

### Self-attention: Query, Key, and Value
- 자기어텐션에서 각 단어는 세 가지 서로 다른 벡터로 표현됨    
- Word2Vec에서 서로 다른 임베딩을 사용하는 것과 유사한 철학    
- 다양한 관계를 유연하게 학습할 수 있도록 함    
- Query 표현  

$$  
q_i = x_i W^Q  
$$

- Key 표현  

$$  
k_i = x_i W^K  
$$

- Value 표현  

$$  
v_i = x_i W^V  
$$

- 워드 임베딩과 유사한 철학임.
- 각각의 단어는 셀프어텐션에서 3가지 역할을 작용하게 됨.


- 자기어텐션에서 각 단어는 세 가지 서로 다른 벡터로 표현됨    
	- Word2Vec에서 두 가지 임베딩을 사용하는 것과 유사한 철학    
	- 다양한 유형의 관계를 유연하게 학습할 수 있도록 함
-  Query 표현: 타겟 단어가 어떤 정보를 찾고 있는지를 나타냄  
	- 지금 보는 단어가 어디에 집중해야 하는지 질문 하는 역할.

$$  
q_i = x_i W^Q  
$$
- Key 표현: Query가 비교되는 문맥(context)을 나타냄  
	- 질문에 답하는 역할

$$  
k_i = x_i W^K  
$$
- Value 표현: 각 단어의 실제 정보를 나타내며, 어텐션 가중치에 따라 결합됨  
	- 각 단어의 실제 정보보

$$  
v_i = x_i W^V  
$$


- 쿼리는 질문하고 키는 답하고
- 워드투벡은 2가지 벡터를 사용
- 트랜스포머는 3가지 벡터를 사용

### Self-attention: Overall computation
- 입력: 각 단어의 단일 벡터 표현 $x_i$ ( i 라는 단어에 대한 값을 얻는 것이 목적)
- 1. 각 단어에 대해 Query, Key, Value 계산  

$$q_i = x_i W^Q \quad k_i = x_i W^K \quad v_i = x_i W^V$$

- 2. Query와 Key로 어텐션 점수 계산  

$$  
\alpha_{ij} = \mathrm{Softmax}(q_i \cdot k_j) = \frac{\exp(q_i \cdot k_j)}{\sum_{k} \exp(q_i \cdot k_{k})}  
$$
- 3. 어텐션 가중치를 사용하여 Value 벡터를 가중합  

$$  
a_i = \sum_{j} \alpha_{ij} v_j  
$$

- 각단어에 쿼리,키, 밸류 트랜스포머 매트릭스를 곱함
- i 단어에는 쿼리 매트릭스를 곱함
- j는 질문의 답이니가 키의 값을 담아야 함.
- 이 $\alpha_{ij}$값에 상응하는 값인 $v_j$를 곱하면 됨.

- 각 단어들에 쿼리,키,밸류 매트릭스를 각각 곱해서 각각의 값을 얻게 됨.

- 예시: 세 단어로 이루어진 입력 시퀀스  $[x_1, x_2, x_3]$
- 이 그림은 $x_3$의 경우를 보여줌
- 1. Query, Key, Value 계산
- 2. $x_3$의 Query를 모든 단어의 Key와 비교
- 3. softmax를 통해 어텐션 점수 획득  

$$  
\alpha_{ij} = \mathrm{Softmax}(q_i \cdot k_j) = \frac{\exp(q_i \cdot k_j)}{\sum_{k} \exp(q_i \cdot k_{k})}  
$$


- 셀프 어텐션은 자기 자신도 포함 됨.

- 예시: 세 단어로 이루어진 입력 시퀀스  

$$  
[x_1, x_2, x_3]  
$$

- 이 그림은 $x_3$의 경우를 보여줌
- 1. Query, Key, Value 계산
- 2. $x_3$의 Query를 모든 단어의 Key와 비교
- 3. softmax를 통해 어텐션 점수 계산  

$$  
\alpha_{3j} = \frac{\exp(q_3 \cdot k_j)}{\sum_{k} \exp(q_3 \cdot k_k)}  
$$

- 4. Value 벡터들을 어텐션 가중치로 가중합하여 출력 생성  

$$  
a_3 = \sum_{j} \alpha_{3j} v_j  
$$
- 결과: $a_3$는 문맥이 반영된(contextualized) $x_3$의 표현

- 각단어의 밸류 값이 올라가서 곱해지면 최종 벡터가 됨.

### Stacking self-attention layers

- 하나의 자기어텐션 레이어는 문맥을 포착하지만, 주로 얕은 수준(shallow level)에서 이루어짐 
- 유사도는 정적 임베딩의 내적(inner product)으로 결정됨    
- 따라서 정적 임베딩이 포착하지 못한 의미는 충분히 반영되지 못함    
- 예시    
	- “picnic”과 “bank”는 정적 임베딩에서 크게 유사하지 않음    
	- 따라서 하나의 자기어텐션 레이어만으로는 두 단어 간 관계를 충분히 가깝게 만들기 어려움

- RNN은 과거 정보를 잊음.
- 트랜스포머는 문장이 길어져도 그 문장을 다 보고 웨이티드 섬을 하기 때문에 정보 손실이 적음.
- 그래도 메모리 연산양이 늘어나는 문제가 있음
	- 그래서 트랜스 포머를 약간 RNN스럽게 해서 메모리를 절약하는 연구가 활발함.
- 대부분 랭귀지 모델은 인풋의 길이 한도를 두긴 함.
	- 너무 짧으면 패딩, 너무 크면 처리 불가 

- x 에 임베딩이 포착을 잘 못하면 의미가 반영 되지 않음
	- xi의 쿼리 값과 xj의 키 값을 연산하고 거기에 밸류j를 곱하는 것이기 때문.



- 하나의 자기어텐션 레이어는 문맥을 포착하지만, 주로 얕은 수준에서 이루어짐    
- 유사도는 정적 임베딩의 내적(inner product)에 의해 결정됨    
- 따라서 정적 임베딩이 포착하지 못한 의미는 충분히 반영되지 못함    
- 예시    
	- “picnic”과 “bank”는 정적 임베딩에서 크게 유사하지 않음    
	- 따라서 하나의 자기어텐션 레이어만으로는 두 단어를 충분히 가깝게 만들기 어려움    
	- 그러나 여러 레이어를 쌓으면 상황이 달라짐    
	- “picnic”이 “river”와 가깝고, “river”가 “bank”와 가깝다면    
	- 여러 레이어를 통해 이러한 문맥적 관계가 점진적으로 전파(propagate)됨

- 셀프 어텐션 레이어는 1개만 사용 하는 것이 아님.
- 버트는 셀프어텐션을 12, 24번등  쌓아서 사용



- 하나의 자기어텐션 레이어는 문맥을 포착하지만, 주로 얕은 수준에서 이루어짐    
- 유사도는 정적 임베딩의 내적(inner product)에 의해 결정됨    
- 따라서 정적 임베딩이 포착하지 못한 의미는 충분히 반영되지 못함    
- 해결 방법: 여러 레이어를 쌓기(stacking multiple layers)    
- 자기어텐션의 핵심은 시퀀스에서 중요한 부분을 점점 더 잘 반영하는 것    
- 의미적으로 유사한 단어들은 점점 더 가까워지고, 관련 없는 단어들은 멀어짐    
- 문맥 정보가 점진적으로 증폭(amplified)됨

### Further details for Transformer (not our focus)
- 변환(transformations) 추가    
	- 피드포워드 네트워크(FF): 
		- 더 많은 레이어(선형 변환 + 활성화 함수) 적용    
	- 멀티헤드 어텐션(multi-head attention)    
- 최적화 용이성 향상    
	- 잔차 연결(residual connections)    
	- 레이어 정규화(layer normalization)    
- 위치 정보 추가    
	- 위치 인코딩(positional encoding)



- 핵심 질문: 각 단어를 표현할 때 문맥을 어떻게 반영할 것인가?    
- 핵심 아이디어: 특정 단어를 처리할 때, 시퀀스 내 다른 단어들의 중요도를 가중치로 반영    
- 자기어텐션(self-attention) 정식화
    
- 타겟 단어 임베딩을 문맥 임베딩의 가중합으로 계산  
    
$$  
a_i = \sum_{j} \alpha_{ij} v_j  
$$
    
- 각 단어는 세 가지 벡터로 표현됨
    
- Query: 정보를 찾는 현재 단어  
    
$$  
q_i = x_i W^Q  
$$
    
- Key: 정보를 제공하는 문맥 단어  
    
$$  
k_i = x_i W^K  
$$
    
- Value: 최종 표현에 반영될 의미 정보  
    
$$  
v_i = x_i W^V  
$$
    
- 여러 자기어텐션 레이어를 쌓으면 문맥 정보가 더 잘 반영됨


### Next question: How to optimize the parameters?
- 여러 자기어텐션 레이어를 쌓으면 각 단어에 대해 풍부한 문맥 정보를 반영할 수 있음    
- 하지만 이러한 과정이 실제로 잘 동작하도록 하려면 학습이 필요함    
- 모델 파라미터 $\theta = \{X, \{W^Q, W^K, W^V\}_{t}, \dots \}$
- $X$: 입력 임베딩
- $W^Q, W^K, W^V$: 각 레이어의 가중치 행렬
- $L$: 레이어 수
- 핵심 질문: 이러한 파라미터들을 어떻게 최적화하여 문맥 표현을 잘 학습할 것인가?
- 해답: 사전학습(pretraining) + 목적 함수 최적화
- 예: 언어 모델링 목적(다음 토큰 예측)  

$$  
\mathcal{L}(\theta) = - \sum_t \log P(x_t \mid x_{\lt t})  
$$

- 또는 마스크드 언어 모델링(MLM) 등 다양한 자기지도 학습 목표 사용
- 이러한 손실 함수를 최소화하도록 파라미터를 학습하면, 모델이 문맥을 잘 반영하는 표현을 자동으로 학습하게 됨

- 트랜스포머는 각 레이어 별로 쿼리, 키, 밸류 파라미터들이 많음 어떻게 해결할까?



- 사전학습을 시켜서 사용하게만든 딥러닌 모델이 버트라고 보면 됨.
	- 논문 제목 그자체임.

### BERT: The big picture
- BERT의 개요
- BERT는 언어 이해를 위해 사전학습된 트랜스포머 모델이며, 양방향 문맥을 활용하여 표현을 학습
- 입력 단계
	- 정적 임베딩(static embeddings)이 입력으로 주어짐
	- 예: 토큰 임베딩 + 위치 임베딩 등
- 모델 구조
	- 여러 개의 트랜스포머 인코더 레이어를 통과
	- 각 레이어는 자기어텐션과 피드포워드 변환으로 구성됨
- 출력
	- 마지막 레이어의 출력은 문맥이 반영된 임베딩(contextual embeddings)
	- 주변 단어 정보를 반영하여 각 단어의 의미를 표현
- 모델 크기 예시
	- BERT-base: 12 레이어, 약 $110\text{M}$ 파라미터
	- BERT-large: 24 레이어, 약 $340\text{M}$ 파라미터


- 구글에서 미리 트랜스포머를 학습시켜서 공개한게 버트
- 3줄만 코딩하면 사용 할 수 있음.
- Static embeddings으로 인풋이 구성됨
- 그다음 셀프 어텐션을 거침. 12~24번 반복
- 그 후 마지막 벡터가 contextual embeddings가 됨.

### BERT: The input
- 문장 “Thanks for all the”가 주어지면, 먼저 각 토큰을 어휘 인덱스로 변환    
	- 예: $[5, 3000, 10532, 2224]$    
	- 이 과정을 토크나이제이션(tokenization)이라 하며, 토크나이저에 따라 결과는 달라질 수 있음 
- 토크나이제이션 이후, 각 토큰 인덱스는 임베딩 테이블의 벡터로 매핑됨
- 이는 원-핫 벡터(one-hot vector)와 임베딩 행렬의 곱으로 볼 수 있음  

$$  
\text{embedding}(x_i) = \text{one-hot}(x_i) \cdot E  
$$
- 원-핫 벡터는 하나의 위치만 $1$이고 나머지는 모두 $0$인 벡터
- 위 연산은 해당 인덱스에 해당하는 임베딩 벡터를 선택하는 것과 동일
- 임베딩은 Word2Vec과 같은 사전학습 벡터를 사용할 수도 있지만, BERT는 이를 처음부터 학습함


- 토크나이제이션은 본 슬라이드에서 배울 예정.
- 단어 인풋이 있으면 벡터화 하고 토크나이제이션 된 토큰 인덱스는 임베딩 테이블 벡터로 매핑
- 원핫 벡터를 사용해서 행렬 곱을 하면 원하는 벡터만 가져 올 수 있음
	- 5번 벡터만 1이고나머지가 0인 벡터를 곱하면 5번 벡터만 리턴 가능
- 워드 투벡 임베딩을 사용 할 수 있지만 구글 연구소에서는 다시 처음부터 임베딩함.

- 토크나이제이션 이후, 각 토큰 인덱스는 임베딩 테이블의 벡터로 매핑됨    
- 이 과정을 통해 전체 문장은 임베딩 벡터들(정적 임베딩)로 변환되며, 이는 모델의 입력으로 사용됨

### BERT: Stacking Transformer layers
- BERT는 여러 개의 트랜스포머 레이어를 쌓아 구성되며, 각 레이어는 자기어텐션과 변환(FFN)으로 이루어짐    
- 이러한 레이어들을 반복적으로 쌓음으로써, 각 단어에 대해 풍부한 문맥 정보(contextual information)를 점진적으로 반영할 수 있음    
- 초기에는 정적 임베딩이 입력되지만, 여러 레이어를 거치면서 문맥이 반영된 표현으로 점점 정교해짐

- 이 과정은 트랜스 포머와 동일함함

- 마지막 레이어의 출력은 문맥 임베딩(contextual embeddings)이 됨    
- 주변 문맥 정보를 반영하여 각 단어의 의미를 표현함

### BERT: Optimization
- 원칙적으로 최적화 문제를 정의하면, 경사하강법(gradient descent)으로 이를 해결할 수 있음
	- 따라서 핵심 질문은 문맥을 잘 반영하는 최적화 문제를 어떻게 정의할 것인가임
- BERT는 강력한 언어 이해를 위해 두 가지 학습 목표를 사용함
	- 1. 마스크드 언어 모델링(MLM)
		- 주변 문맥을 기반으로 무작위로 가려진 단어를 예측
		- 다음 단어가 나오게 할 것인데 랜덤하게 마스킹을 한 뒤 확률을 맞추게 함.
	- 2. 다음 문장 예측(NSP)
		- 한 문장이 다른 문장 다음에 자연스럽게 이어지는지 여부를 예측
		- 두 문장을 주고 두 문장이 논리적으로 이어지는지 아닌지를 맞춤.


- 

### 1. Masked language modeling (MLM)
- BERT에 들어가는 데이터는 라지 랭귀지임.
- MLM에서는 마스크라는 스페셜 토큰으로 치환 됨.
- 그 다음 가려진 단어가 무엇인지 BERT가 맞춰야 함.


- 셀프 어텐션의 특징은 어떤 단어가 중요한지 찾는 것임.
	- 뱅크를 맞추려면 피크닉과 리버를 알아야 하고 유의미하게 연결 되었다는 것을 찾아야 함.
	- 모델에게 어떤 단어가 중요한지를 가르쳐 주는 모델이라고 볼 수 있음.


- 마스크드 언어 모델링(MLM): 가려진 단어를 예측하는 학습 목표  
$$  
\mathcal{L}_{\mathrm{MLM}} = - \frac{1}{|M|} \sum_{i \in M} \log P(x_i \mid h_i^L)  
$$

- $M$: 마스킹된 위치들의 집합
- 전체 토큰의 약 $15$%를 무작위로 선택하여 특수 토큰 $\text{[MASK]}$로 대체
- 입력 문장: 원래 문장
- 마스킹된 문장: 일부 단어가 $\text{[MASK]}$로 대체된 문장
- 목표: 문맥을 기반으로 원래 단어를 정확히 복원하도록 학습

- 가려진 단어를 맞출 확률이 높아지도록 오브젝트 펑션을 만들고 학습을 진행


- 확률 계산 방법: 선형 레이어와 softmax를 사용
- 먼저, 마지막 레이어의 은닉 표현 $h_i^L$에 선형 변환 적용  
$$  
u = h_i^L W  
$$

- 이후 softmax를 적용하여 확률 분포 계산  
$$  
y = \mathrm{softmax}(u)  
$$

- 각 로짓(logit)은 문맥 임베딩 $h_i^L$와 어휘 임베딩(가중치 행렬 $W$의 각 열) 간의 내적(inner product)으로 해석됨


$$  
\text{softmax}(x_i)= \frac{\exp(x_i)}{\sum_j \exp(x_j)}, \quad \sum_i p_i = 1  
$$


- weight tying은 모델 크기를 줄이고 중복을 방지함
	- 입력 임베딩 행렬 $E$와 출력 가중치 $W$를 공유하여 별도의 파라미터를 두지 않음  
$$  
W = E^{\top}  
$$
- 임베딩 E의 트랜스포즈 한것을 웨이트 벡터로 사용??
- 동일한 단어 표현을 입력과 출력에서 함께 사용하여 파라미터 효율성과 일반화 성능을 향상시킴

- 이진 문제를 풀도록 만듦.

### 2. Next sentence prediction (NSP)
- 아이디어    
	- 두 문장을 동시에 모델에 입력하며, 특수 토큰 $\text{[SEP]}$→ 세퍼레이션 토큰으로 구분    
	- 입력의 맨 앞에 $\text{[CLS]}$ 토큰을 추가하여 전체 문장 정보를 요약   
		- CLS는 BERT의 모든 문장 앞에 추가되도록 함.
	- 모델은 두 번째 문장이 첫 번째 문장 뒤에 실제로 이어지는지 여부를 예측    
- 문맥 학습에 도움이 되는 이유    
	- 문장 간 일관성(coherence)을 학습하도록 유도 (토큰 수준을 넘어선 이해)    
	- 이후 연구에서는 NSP의 필요성에 대한 논쟁이 있었지만, 이 설계는 많은 후속 연구에 영감을 줌


- MLM보다 긴 호흡에서 문맥을 이해하도록 함.

- **현대 검색이나 추천에 기반이 된 개념이기 때문에 모델 디자인은 알아두는 것이 좋음.**


- $y$: 두 문장이 연속적인지 여부(이진 분류)
- $\text{[CLS]}$ 토큰은 전체 입력 문장의 정보를 집약한 표현
- 따라서 $\text{[CLS]}$의 최종 표현 $h_{\mathrm{[CLS]}}^{L}$을 사용하여 두 문장이 이어지는지 예측
- 입력 구성
- 두 문장을 함께 입력으로 사용
- 두 문장 사이에 $\text{[SEP]}$ 토큰을 삽입하여 구분

- \[CLS] token aggregates information from the whole input, not just a single word. So, we use it to predict whether two sentences are consecutive or not
- 문장의 종결을 알려주기 위해 SEP 토큰을 마지막도 추가 하기도 함.
- hCLS가 나오면 이진 분류를 수행해서 O,X 답변

- 다음 문장 예측(NSP, Next Sentence Prediction) 손실 함수  
$$  
\mathcal{L}_{\mathrm{NSP}} = - \log P(y \mid h_{\mathrm{[CLS]}}^{L})  
$$

- linear layer + softmax를 이용함.
$$  
\mathbf{y}=\text{softmax}\left(\mathbf{h}_{\mathrm{CLS}}^{L}\mathbf{W}_{\mathrm{NSP}}\right)  
$$

### BERT optimization = MLM + NSP
- BERT는 두 가지 학습 목표로 사전학습됨  
$$  
\mathcal{L}_{\mathrm{BERT}} = \mathcal{L}_{\mathrm{MLM}} + \mathcal{L}_{\mathrm{NSP}}  
$$

- 마스크드 언어 모델링(MLM)  
$$  
\mathcal{L}_{\mathrm{MLM}} = - \frac{1}{|M|} \sum_{i \in M} \log P(x_i \mid h_i^L)  
$$

- 주변 문맥을 기반으로 마스킹된 단어를 예측
- 다음 문장 예측(NSP)  
$$  
\mathcal{L}_{\mathrm{NSP}} = - \log P(y \mid h_{\mathrm{[CLS]}}^{L})  
$$

- 두 문장이 연속적인지 여부를 예측
- 두 목적 함수는 함께 최적화되며, 문맥 이해 능력을 효과적으로 학습함

- 마스크도 하고 두 문장이 이어지는지 복합적으로 평가를 함.


- BERT는 두 가지 학습 목표로 사전학습됨  
$$  
\mathcal{L}_{\mathrm{BERT}} = \mathcal{L}_{\mathrm{MLM}} + \mathcal{L}_{\mathrm{NSP}}  
$$
- 최적화 방법: 경사하강법(gradient descent)
- 그래디언트 $\nabla_{\theta} \mathcal{L}(\theta)$는 손실을 가장 크게 증가시키는 방향을 나타냄
- 알고리즘
- 파라미터 $\theta$를 무작위로 초기화
- 수렴할 때까지 반복  
$$  
\theta \leftarrow \theta - \eta \nabla_{\theta} \mathcal{L}(\theta)  
$$

- $\theta$: 학습할 파라미터
- $\eta$: 학습률(learning rate, 하이퍼파라미터)

## Transformation 본문
### Transformer: Motivation
- Parallel token(병렬 토큰) 처리:    
	- RNN: 한 번에 하나의 토큰씩 처리 (각 토큰의 계산이 이전 토큰에 의존)    
	- Transformer: 시퀀스의 모든 토큰을 병렬로 처리    
- 장기 의존성:    
	- RNN: 먼 거리의 토큰 간 관계를 잘 포착하지 못함 (기울기 소실 문제)    
	- Transformer: 위치와 상관없이 시퀀스 내 모든 토큰에 직접 접근 가능    
- Bidirectionality(양방향성):    
	- RNN: 한 방향으로만 시퀀스를 모델링 가능    
	- Transformer: attention을 통해 본질적으로 양방향 시퀀스 모델링 가능



### Transformer Layer
- 각 Transformer 층은 다음과 같은 중요한 구성 요소를 포함한다:
    - Self-attention   
	- Feedforward network    
	- Residual connection과 layer normalization



### Self-Attention: Intuition
- Attention: 특정 단어를 처리할 때, 시퀀스 내 다른 단어들의 중요도를 가중치로 계산하는 메커니즘    
	- “이 단어를 이해하기 위해 어떤 다른 단어들에 주목해야 하는가?”    
- Self-attention: 각 단어가 같은 시퀀스 내의 다른 단어들에 주의를 기울인다.    
- 예시: “The quick brown fox jumps over the lazy dog.”    
	- “jumps”라는 단어에 대한 attention을 학습한다고 가정하면:    
	- self-attention을 통해 “jumps”는 자신의 의미를 더 잘 이해하기 위해 어떤 단어에 집중할지 결정한다.    
	- 높은 attention을 줄 수 있는 단어:    
		- “fox” (주어)    
		- “over” (전치사)    
	- 낮은 attention을 줄 수 있는 단어:    
		- “the”, “lazy”



- 중심 단어 표현(center word representation)을 주변 단어 표현(context word representations)의 가중합으로 계산한다.    

$$  
a_i = \sum_{x_j \in x} \alpha_{i,j} x_j,\quad \sum_{x_j \in x} \alpha_{i,j} = 1  
$$

- $\alpha_{i,j}$: 단어 $i$가 단어 $j$에 부여하는 attention 가중치 (합은 1)

### Self-Attention: Attention Score Computation
- attention 점수는 벡터 내적(dot product)에 소프트맥스 함수를 적용하여 계산된다.
	- $x_i$: 중심 단어(query) 표현
	- $x_j$: 문맥 단어(key) 표현


$$  
a_i = \sum_{x_j \in x} \alpha_{i,j} x_j,\quad \sum_{x_j \in x} \alpha_{i,j} = 1  
$$
$$  
\alpha_{i,j} = \text{softmax}(x_i \cdot x_j)  
$$


- attention 계산에서 단어 표현을 두 개 사용하는 이유:
	- 단어가 서로 다른 역할(비교의 기준이 되는 단어 vs 비교 대상 단어)을 반영하기 위함
	- 동일한 표현을 사용할 경우, 자기 자신과의 내적이 커져 대부분 자기 자신에 과도하게 attention을 주는 문제가 발생한다.



### Self-Attention: Query, Key, and Value
- self-attention에서 각 단어는 세 가지 서로 다른 벡터로 표현된다.
	- 이는 토큰 간 다양한 관계를 유연하게 포착할 수 있도록 한다.
- Query (Q):
	- 현재 단어로서, 정보를 얻기 위해 다른 단어들을 탐색하는 역할
- Key (K):
	- Query와 비교되는 기준이 되는 문맥 표현
- Value (V):
	- 각 토큰이 가지는 실제 정보로, 최종 출력에서 가중합으로 결합되는 값



- 각 self-attention 모듈은 입력 단어 벡터에 세 개의 가중치 행렬을 적용하여 세 가지 표현을 생성한다.

### Self-Attention: Overall Computation
- 입력: 각 단어의 벡터 $x_i$
- 각 단어에 대해 $Q, K, V$ 표현 계산:  
$$  
q_i = x_i W^Q,\quad k_i = x_i W^K,\quad v_i = x_i W^V  
$$

- $Q$와 $K$를 사용하여 attention 점수 계산:
- 두 벡터의 내적 크기는 $\sqrt{d}$에 비례하는 경향이 있음
- 소프트맥스에서 값이 과도하게 커지는 것을 방지하기 위해 $\sqrt{d}$로 나눔

$$  
\alpha_{i,j} = \text{softmax}\left(\frac{q_i \cdot k_j}{\sqrt{d}}\right)  
$$

- attention 점수로 가중합하여 값 벡터를 결합:  
$$  
a_i = \sum_{x_j \in x} \alpha_{i,j} v_j  
$$




- 예시: 세 단어로 이루어진 입력 시퀀스 $[x_1, x_2, x_3]$
- $x_3$에 대한 self-attention을 계산한다고 가정
- $Q, K, V$ 계산:  
$$  
q_3 = x_3 W^Q,\quad k_1 = x_1 W^K,\ k_2 = x_2 W^K,\ k_3 = x_3 W^K  
$$  
$$  
v_1 = x_1 W^V,\quad v_2 = x_2 W^V,\quad v_3 = x_3 W^V  
$$

- attention 점수 계산 (query와 모든 key 비교):  
$$  
\alpha_{3,j} = \text{softmax}\left(\frac{q_3 \cdot k_j}{\sqrt{d}}\right),\quad j \in {1,2,3}  
$$

- 값 벡터의 가중합으로 출력 생성:  
$$  
a_3 = \sum_{j=1}^{3} \alpha_{3,j} v_j  
$$
- 즉, $x_3$는 모든 단어($x_1, x_2, x_3$)를 참고하여 자신의 새로운 표현을 생성한다.


### Multi-Head Self-Attention
- Transformer는 각 self-attention 모듈에서 여러 개의 multiple attention head를 사용한다.   
- 직관:    
	- 각 head는 서로 다른 목적(예: 특정 패턴)에 맞게 문맥에 주의를 기울일 수 있다.    
	- 각 head는 서로 다른 언어적 관계를 학습하도록 특화될 수 있다.    
- 여러 head의 출력은 모두 연결(concatenate)되어 하나의 표현으로 결합된다.    
- $h$개의 attention head는 각각 독립적으로 계산된다.

- Wq, Wk,Wv에 어텐션을 주는데 한번만 하는게 아니고 이렇게여러 세트를 만들어서 사요함.
- 이 하나의 묶음을 헤드라고 하고 병렬적으로 연결된 헤드들이 서로 보완 
- 어텐션을 계산하는게 scaled dot - product attention이고 이걸 h번 실시.


### Parallel Computation of QKV
- 각 토큰에 대한 self-attention 계산은 다른 토큰들과 독립적으로 수행된다.
- 전체 연산을 쉽게 병렬화할 수 있으며, GPU의 효율적인 행렬 곱셈을 활용할 수 있다.
- 길이가 $N$인 입력 시퀀스를 병렬로 처리할 수 있다.
- 한 단어에 대한 $Q, K, V$ 계산:  
$$  
q_i = x_i W^Q,\quad k_i = x_i W^K,\quad v_i = x_i W^V \in \mathbb{R}^d  
$$
- $N$개의 입력을 행렬로 쌓기:  
$$  
Q = X W^Q,\quad K = X W^K,\quad V = X W^V \in \mathbb{R}^{N \times d}  
$$


$$  
X =  
\begin{bmatrix}  
x_1 \\  
x_2 \\  
\vdots \\  
x_N  
\end{bmatrix}  
$$

- $x_i$를 스택해서 벡터를 만들어 놓고 한번에 연산 할 수 있도록 하는 스킬
- 이러면 GPU의 병렬 처리를 이용해서 효과적으로 연산 할 수 있음.

### Parallel Computation of Attention
- attention 계산은 행렬 형태로도 표현할 수 있다.
- 하나의 단어에 대한 attention:  
$$  
a_i = \text{softmax}\left(\frac{q_i \cdot k_j}{\sqrt{d}}\right) v_j  
$$

- $N$개의 단어에 대한 attention (행렬 형태):  
$$  
A = \text{softmax}\left(\frac{Q K^T}{\sqrt{d}}\right) V  
$$

- $QK^T$: 모든 query와 key 간의 유사도를 나타내는 attention 행렬
- softmax: 각 행(row)에 대해 정규화되어 확률 분포 생성
- 최종적으로 $V$와 곱하여 각 단어의 새로운 표현을 얻는다.

| |k1|k2|k3|k4|
|---|---|---|---|---|
|q1|q1·k1|q1·k2|q1·k3|q1·k4|
|q2|q2·k1|q2·k2|q2·k3|q2·k4|
|q3|q3·k1|q3·k2|q3·k3|q3·k4|
|q4|q4·k1|q4·k2|q4·k3|q4·k4|
- 어텐션 연산도 매트릭스 연산으로 간단하게 처리됨.
- 병렬로 하나의 행렬곱으로 만들 수 있게 됨.


### Bidirectional vs. Unidirectional Self-Attention
- 셀프 어텐션의 방향에 대한 내용
- self-attention은 다양한 문맥 의존성을 포착할 수 있다.    
- 양방향 self-attention:    
	- 각 위치의 토큰이 입력 시퀀스의 모든 다른 위치에 주의를 기울일 수 있다.    
	- 양방향 self-attention을 사용하는 Transformer는 Transformer 인코더라고 한다 (예: BERT).   
	- 전체 입력이 한 번에 주어지는 자연어 이해(NLU) 작업에 적합하다 (예: 텍스트 분류, 개체명 인식).

- 양방향과 한방향으로 정보를 보내는 셀프 어텐션이 있음
- 버트는 양방향의 bi이 약자를 사용함
- 양방향 셀프어텐션을 사용하면 인코더 기반 모델이라고 함.


- self-attention은 다양한 문맥 의존성을 포착할 수 있다.    
- Unidirectional단방향(또는 causal) self-attention:    
	- 각 위치는 자기 자신을 포함하여 이전 위치의 토큰들에만 주의를 기울일 수 있다.    
	- 단방향 self-attention을 사용하는 Transformer는 Transformer 디코더라고 한다 (예: GPT).    
	- 자연어 생성(NLG)과 같이 모델이 순차적으로 출력을 생성하는 작업에 적합하다.    
	- attention 행렬에서 상삼각(upper triangle) 부분은 $-\infty$로 설정되어 미래 토큰에 대한 attention을 차단한다.

| |k1|k2|k3|k4|
|---|---|---|---|---|
|q1|q1·k1|$-\infty$|$-\infty$|$-\infty$|
|q2|q2·k1|q2·k2|$-\infty$|$-\infty$|
|q3|q3·k1|q3·k2|q3·k3|$-\infty$|
|q4|q4·k1|q4·k2|q4·k3|q4·k4|

- 요즘 GPT등 대부분 랭귀지 모델은 단방향 셀프 어텐션을 활용함.
- 과거 정보를 이용하고 미래 정보는 알 수 없음.
- 자기 자신 이전의 정보만 포함.
- 이런 방식을 디코더 기반 모델이라고 함.(e.g.,GPT)
- 미래 정보는 그냥 -무한대로 바꾸고 소프트맥스 들어가서 0으로 처리 되도록 함.

### Position Encoding
- 동기(motivation): 입력 벡터에 위치 정보를 주입하기 위함


$$  
q_i = x_i W^Q,\quad k_i = x_i W^K,\quad v_i = x_i W^V \in \mathbb{R}^d  
$$

$$  
a_i = \text{softmax}\left(\frac{q_i \cdot k_j}{\sqrt{d}}\right) v_j  
$$

- $x$가 단어 임베딩일 때, $q$와 $k$에는 위치 정보가 포함되지 않는다.    
- 시퀀스에서 단어의 위치를 알기 위한 방법: 위치 인코딩(position encoding)을 사용한다.

- 인풋벡터를 인풋할때 사용되는 스킬임.
- 같은 단어가 앞쪽에 나올수도 뒤쪽에 나올수도 있음. 그동안 배운 내용에는 이런 정보가 들어가는 기술이나 아이디어 없었음.
- 이를 반영한것이 포지셔닝 인코딩임.
- 스태틱 인베딩 다음 포지션 이베딩을 하고 그다음에 워드 임베딩 연산을 해서 인풋하면 위치, 의미 정보 모두 들어가게 됨.


### Position Encoding Methods
- 절대 위치 인코딩(Absolute position encoding, 원래 Transformer 논문):    
	- 각 위치에 대해 위치 임베딩을 학습한다.    
	- 학습 시 보지 못한 더 긴 시퀀스에는 일반화가 잘 되지 않는다.    
	- i자리에 절대값을 할당해서 그 위치 값을 정해 놓음.
		- 0 → sin(0)→ cos(0.5) 등등등
- 상대 위치 인코딩(Relative position encoding):    
	- 절대 위치 대신 단어 간의 상대적 거리 정보를 인코딩한다.    
	- 다양한 길이의 시퀀스에 대해 더 잘 일반화된다.    
- 회전 위치 임베딩(Rotary position embedding, RoPE):    
	- 단어 임베딩에 위치에 따라 회전 변환을 적용한다.    
	- 절대 위치와 상대 위치 정보를 모두 반영한다.    
	- 긴 시퀀스에도 효과적으로 일반화된다.    
	- 최신 대형 언어 모델(LLM)에서 널리 사용된다.


- 어떤 포지션 인코딩이 좋은지도 많이 연구 되었음.
- 붙어 있는 포지션은 먼 포지션보다 유사하다가 기본 개념임.

- 토큰: 인풋의 최소 요소 (단어 벡터) → 뒤의 토픽 토크나이제이션에서 설명.




### Tokenization: Overview
- 토크나이제이션(tokenization): 문자열을 토큰들의 시퀀스로 분할하는 과정    
- 단순한 방법: 공백(whitespace)을 기준으로 시퀀스를 분할    
	- 하나의 토큰 = 하나의 단어    
	- “토큰”과 “단어”를 혼용하여 사용하기도 함    
- 그러나 **공백 기반 분할은 현대의 대형 언어 모델에서는 사용되지 않는다**.    
- OPENAI 설명 (가격 정책 부분에 명시시)
	- 토큰은 단어의 일부 단위로 볼 수 있으며, 대략 1,000 토큰은 약 750 단어에 해당한다.

### Limitation of Word-Based Segmentation
- OOV(Out-of-vocabulary) 문제:    
	- 학습 데이터에서 한 번도 보지 못한 단어를 처리할 수 없다.    
	- 이를 해결하기 위해 보지 못한 단어를 위한 $[\text{UNK}]$ 토큰을 사용하는 방법이 있다.    
- 서브워드(subword) 정보:    
	- 단어의 의미와 구조를 이해하는 데 중요한 서브워드 정보를 잃게 된다.    
	- 예: “unhappiness” $\rightarrow$ “un” + “happy” + “ness”    
- 데이터 희소성(sparsity) 및 어휘 폭발  (exploded vocabulary size)문제:    
	- 큰 어휘 집합(고유 단어 수)이 필요하다.    
	- 각 단어에 대한 학습 데이터가 줄어들어 일반화가 어려워진다.


### Single-Character Segmentation?
- character 단위로 시퀀스를 분할하는 방법: (알파벳 문자 단위로 분할할)    
	- OOV 문제가 발생하지 않는다.    
	- 어휘 크기가 매우 작다.    
- 단점   
- 시퀀스 길이 증가:    
	- 입력 시퀀스 길이가 크게 증가한다.    
	- Transformer의 self-attention은 시퀀스 길이에 대해 이차 복잡도($O(n^2)$)를 가지므로 계산 비용이 커진다.    
- 단어 수준 의미 손실:    
	- 개별 문자는 의미나 언어적 패턴을 충분히 담고 있지 못하다.



### Subword Tokenization
- character 문자 단위와 word 단어 단위 토크나이제이션 사이의 균형을 맞추는 방법:
- 목표:
	- 의미 있는 서브워드 의미를 포착
	- OOV(미등록 단어) 문제를 더 잘 처리
	- 효율적인 시퀀스 모델링 가능
- 대표적인 알고리즘 3가지:
	- **Byte-Pair Encoding** (BPE) → 가장 많이 사용 됨.
	- WordPiece
	- SentencePiece
- 서브워드 토크나이제이션은 일반적으로 두 단계로 구성된다:
	- 토큰 학습기(token learner):
		- 원시 학습 코퍼스를 입력으로 받아 어휘 집합(토큰 집합 a set of tokens)을 생성
	- 토큰 분할기(token segmenter):
		- 새로운 문장을 입력으로 받아, 학습된 어휘에 따라 토큰으로 분할한다.



### Byte-Pair Encoding (BPE) Overview
- BPE(Byte-Pair Encoding)는 **현대 LLM에서 가장 널리 사용되는 토크나이제이션 알고리즘**이다.
- 직관: 문자 단위 어휘에서 시작하여, 가장 자주 등장하는 토큰 쌍을 반복적으로 병합한다.
- Initialization 초기화:
	- 어휘를 모든 문자 집합으로 설정  
$$  
{A, B, C, D, \ldots, a, b, c, d, \ldots}  
$$
- Frequency counting빈도 계산:
	- 학습 코퍼스에서 인접한 모든 심볼 쌍(문자 또는 이미 병합된 토큰)의 빈도를 계산한다.
- Pair merging 쌍 병합:
	- 가장 빈도가 높은 심볼 쌍을 하나의 토큰으로 병합
	- 예: ‘t’, ‘h’ $\rightarrow$ “th”
- Update corpus코퍼스 업데이트:
	- 병합된 토큰으로 기존 코퍼스의 해당 쌍을 모두 치환하고, 쌍의 빈도를 다시 계산한다.
- Repeat 반복:
	- 빈도 계산 → 병합 → 업데이트 과정을, 미리 정한 병합 횟수 또는 어휘 크기에 도달할 때까지 반복한다.

- charater레벨에서 집합을 설정하고 빈도를 계산해서 머지 & 머지 → 업데이트(정해진 단어 크기에 도달 할때 까지) 하는 알고리즘.


### BPE: Token Learner
- BPE의 토큰 학습기(token learner):    
- 함수:    
- BYTE-PAIR ENCODING(strings $C$, 병합 횟수 $k$)는 어휘 집합 $V$를 반환한다.
- 초기화:
- $V \leftarrow C$에 포함된 모든 고유 문자 (초기 토큰 집합은 문자들)
- 반복 ($1$부터 $k$까지):
- $t_L, t_R \leftarrow C$에서 가장 자주 등장하는 인접 토큰 쌍(왼쪽 오른쪽)
- $t_{\text{new}} \leftarrow t_L + t_R$ (두 토큰을 이어붙여(concat) 새로운 토큰 생성)
- $V \leftarrow V + t_{\text{new}}$ (어휘 업데이트)
- $C$에서 모든 $(t_L, t_R)$ 쌍을 $t_{\text{new}}$로 치환 (코퍼스 업데이트)
- 결과:
- 최종 어휘 집합 $V$ 반환


- 다음과 같은 코퍼스가 주어졌다고 가정한다.
- 코퍼스:
- low low low low low lowest lowest newest newer newer newer newer newer newer wider wider wider new new
- 단어 끝을 나타내기 위해 특수 문자 언더바바 $-$ (end-of-word)를 사용한다.
- 이는 서브워드 단위와 전체 단어를 구분하기 위함이다.
- 코퍼스 표현 (빈도 포함):  
```text
Corpus

5 l o w _
2 l o w e s t _
6 n e w e r _
3 w i d e r _
2 n e w_

Vocabulary
- , d, e, i, l, n, o, r, s, t, w
```



- 가장 높은 빈도를 가지는 인접 심볼 쌍은 “er”이며, 빈도는 $9$이다.
- 병합 수행:
- “e”, “r” $\rightarrow$ “er”
- 업데이트:  
```text
Corpus

5 l o w _
2 l o w e s t _
6 n e w er _
3 w i d er _
2 n e w_

Vocabulary
- , d, e, i, l, n, o, r, s, t, w → - , d, e, i, l, n, o, r, s, t, w, er
```





- 가장 높은 빈도를 가지는 인접 심볼 쌍은 “ne”이며, 빈도는 $8$이다.
- 병합 수행:
- “n”, “e” $\rightarrow$ “ne”
- 업데이트:  
```text
Corpus

5 l o w _
2 l o w e s t _
6 ne w er _
3 w i d er _
2 ne w_

Vocabulary
- , d, e, i, l, n, o, r, s, t, w, er → - , d, e, i, l, n, o, r, s, t, w, er, ne
```



- 인접 심볼 병합 과정을 계속 수행한다.
- 병합 순서 및 어휘 변화:
- $(ne, w) \rightarrow \text{new}$  
$$  
{- , d, e, i, l, n, o, r, s, t, w, er, ne} \rightarrow {- , d, e, i, l, n, o, r, s, t, w, er, ne, new}  
$$
- $(l, o) \rightarrow \text{lo}$  
$$  
\ldots \rightarrow \ldots, lo  
$$
- $(lo, w) \rightarrow \text{low}$  
$$  
\ldots \rightarrow \ldots, low  
$$
- $(new, er) \rightarrow \text{newer}$  
$$  
\ldots \rightarrow \ldots, newer  
$$
- $(low, -) \rightarrow \text{low-}$  
$$  
\ldots \rightarrow \ldots, low-  
$$
- 이와 같이 반복적으로 자주 등장하는 쌍을 병합하여 점점 더 긴 서브워드(또는 단어)를 구성한다.
- charater 들이 merge 되어 새로운 단어들이 계속 추가 됨.

### BPE: Token Segmenter
- 어휘(vocabulary)를 학습한 후에는, 보지 못한 문장(test set)을 토크나이즈하기 위한 토큰 분할기(token segmenter)가 필요하다.    
- 학습 데이터에서 얻은 병합 규칙을 그대로 사용하여, 탐욕적(greedy) 방식으로 적용한다.    
- 예시:    
- 병합 규칙: 
$$  
(le, r),\ (er, -),\ (n, e),\ (ne, w),\ (l, o),\ (lo, w),\ (new, er),\ (low, -)  
$$
- 적용 과정:
	- 먼저 “er”를 병합 → 이후 인접한 “ne” 병합 → ... 순차적으로 적용
- 결과:
	- “newer”는 하나의 토큰으로 분할됨
	- “lower”는 “low” + “er”로 분할됨
	- “lower”는 학습 데이터에 없던 단어이지만, 서브워드 단위로 분해되어 처리 가능하다.
	-  “lower-”는 학습 데이터에서 보지 못한 단어이다.
```text
Corpus

low low low low low lowest lowest newer newer newer newer newer newer wider wider wider new new
```

- 코퍼스에서는 lower라는 단어가 없지만 BPE를 통해 코퍼스에 없었던 단어도 이해하고 단어 리스트에 추가할 수있음.
- 모델을 배포할때는 토크나이저도 배포해줘야 모델이 실행이 됨.
- 한글의 경우 약간의 처리가 들어가지만 원리는 유사함.



### Transformer Block
- 트랜스포머 레이어의 구성 요소:
	- Multi-head attention 멀티헤드 어텐션    
	- Layer normalization 레이어 정규화(LayerNorm)    
	- Feedforward network 피드포워드 네트워크(FFN)    
	- 잔차(Residual) connection 연결

### Layer Normalization: Motivation
- Jimmy Lei Ba 등(2016)에서 제안됨    
- DNN의 입력 분포는 학습 중 변화할 수 있음 – “내부 공변량 변화(internal covariate shift)”    
- 학습 속도를 저하시킴: 모델이 계속 변화하는 분포에 적응해야 하기 때문

- 그래서 정규화 기법을 사용하고 레이어에 정규화를 실시하기 때문에 Layer Normalization



### Layer Normalization: Solution
- 입력 벡터 $x$를 정규화
- 입력 벡터 차원에 대해 평균과 표준편차 계산  
$$  
\mu = \frac{1}{d} \sum_{i=1}^{d} x_i  
$$  $$  
\sigma = \sqrt{\frac{1}{d} \sum_{i=1}^{d} (x_i - \mu)^2}  
$$
- 정규화 적용  
$$  
\hat{x} = \frac{x - \mu}{\sigma}  
$$

- 학습 가능한 파라미터로 스케일 및 시프트  
$$  
\mathrm{LayerNorm}(x) = \gamma \frac{x - \mu}{\sigma} + \beta  
$$
- $\gamma, \beta$는 학습 가능한 파라미터(조금 더 학습 잘하라고 파라미터를 추가함. 딥러닝에서 아주 보편적으로 사용)


### Feedforward Network (FFN)
- 트랜스포머의 FFN은 2층 네트워크(하나의 은닉층, 두 개의 가중치 행렬)  
$$  
\mathrm{FFN}(x_i) = \mathrm{ReLU}(x_i W_1) W_2  
$$
- 첫 번째 레이어 이후 비선형 활성화 함수 적용
- 모든 토큰에 동일한 가중치 적용
- 가중치는 서로 다른 트랜스포머 레이어 간에는 서로 다름
- 가중치주고 → 렐루 → 다시 가중치

### Residual Connections
- 서브레이어(예: 어텐션, FFN)의 출력에 원래 입력을 더함  
$$  
y = x + f(x)  
$$

- 장점
	- 기울기 소실 문제를 완화
	- 네트워크 전반에 걸친 정보 흐름을 용이하게 함
	- 모델 확장을 용이하게 함

- 이것도 딥러닝에서 보편적인 기법
- 일종의 우회로임
- LMST에서 cell state를 준것처럼 그래디언트의 배니슁이나 익스프로딩을 방지하기 위한 기법.

### Language Model Head
- 언어 모델 헤드는 최종 레이어에 추가됨
- 일반적으로 weight tying 기법을 적용(입력 임베딩과 출력 임베딩의 가중치 공유)
- 언어 모델 헤드는 $h_N$을 입력으로 받아 어휘 집합 $V$에 대한 확률 분포를 출력  
$$  
\text{logits} = h_N E^{\top}  
$$  
$$  
P(y \mid x) = \mathrm{softmax}(h_N E^{\top})  
$$


### Transformer Language Model: Overview


### Transformer Language Model Training
- 트랜스포머 언어 모델 학습에는 교차 엔트로피 손실(cross-entropy loss)을 사용 (RNN 기반 언어 모델과 동일)  
$$  
\mathcal{L} = - \sum_{t=1}^{T} \log P(y_t \mid y_{<t})  
$$
- 각 시점 $t$에서 정답 토큰 $y_t$에 대한 예측 확률을 최대화하도록 학습
- softmax로 얻은 확률 분포와 실제 정답 분포 간의 차이를 최소화



### Pretraining: Motivation
- 사전학습(pretraining)이 널리 사용되기 전에는 대부분의 NLP 모델이 다운스트림 태스크 데이터로부터 처음부터 학습됨    
- 데이터 부족 문제: 많은 NLP 태스크는 대규모 라벨 데이터셋이 없음(수집 비용이 높음)    
	- 감정분류 등 많은 NLP는 라벨없고 일반화 성능이 약함.
- 일반화 성능 부족: 특정 태스크에 대해 처음부터 학습된 모델은 보지 못한 데이터나 다른 태스크에 잘 일반화되지 않음    
- 노이즈 및 무작위성에 민감: 모델이 허위 상관관계를 학습하거나 어노테이션 오류 및 학습 과정의 무작위성에 영향을 받기 쉬움


- 웹에는 풍부한 텍스트 데이터가 존재하며, 언어적 특징과 세계 지식에 대한 다양한 정보를 포함함    
- 이러한 쉽게 얻을 수 있는 데이터를 활용한 학습은 다양한 다운스트림 태스크에 큰 도움이 됨

- 다운스트림은 스팸분류 감정 분류등 구체적인 task들들

### Pretraining: Multi-Task Learning
- 여가 시간에 나는 ${\text{run}, \text{banana}}$ 중 $\text{run}$을 좋아함 (문법)    
- 나는 동물원에 가서 기린, 사자, 그리고 ${\text{zebras}, \text{spoon}}$ 중 $\text{zebras}$를 봄 (어휘 의미)    
- 덴마크의 수도는 ${\text{Copenhagen}, \text{London}}$ 중 $\text{Copenhagen}$ (세계 지식)    
- 나는 내내 긴장해서 좌석 끝에 앉아 있었음. 그 영화는 ${\text{good}, \text{bad}}$ 중 $\text{good}$ (감정 분석)    
- 스페인어로 “pretty”는 ${\text{bonita}, \text{hola}}$ 중 $\text{bonita}$ (번역)
- $3 + 8 + 4 = 15$ (수학)

- MLM, NSP외에도 다양한 프리트레이닝 방법이 있음.
	- 설계 하기 나름임.


### Pretraining: Self-Supervised Learning
- 사전학습(pretraining)은 자기지도학습(self-supervised learning)의 한 형태    
- 입력의 일부를 모델에게 보이지 않도록 만듦    
- 나머지 입력 정보를 활용하여 가려진(unknown) 부분을 복원하거나 예측하도록 학습

- 마스크드 모델과 비슷함. 
- 가려진 부분을 스스로 만들고 답을 찾는 방법처럼 스스로 데이터를 가공 후 프리트레이닝 하는 방법법을 셀프 슈퍼바이즈드 러닝이라 함.

### Pretraining + Fine-Tuning
- 사전학습(pretraining): 대규모 텍스트 코퍼스에서 프리텍스트 태스크(pretext tasks)를 통해 학습    
- 파인튜닝(fine-tuning, 추가 학습): 사전학습된 모델의 파라미터를 파인튜닝 데이터로 조정    
- 파인튜닝 데이터의 형태    
- 태스크별 라벨 데이터(예: 감성 분류, 개체명 인식)    
- (멀티턴) 대화 데이터(즉, instruction tuning)


### Transformer for Pretraining
- 트랜스포머는 언어 모델 사전학습의 표준 백본 아키텍처    
- 효율성: 시퀀스의 모든 토큰을 동시에 처리 → 특히 대규모 데이터셋에서 빠르고 효율적인 학습 가능    
- 확장성: 모델 크기와 학습 데이터가 증가할수록 성능이 향상되는 뛰어난 스케일링 특성을 보임 
- 범용성: 텍스트뿐만 아니라 비전, 오디오 등 다양한 모달리티 및 멀티모달 태스크에 적용 가능

- 대부분 랭귀지 모델은 트랜스포머 모델을 사용.




### Transformer Architectures
- self-attention의 유형에 따라 트랜스포머는 다음과 같이 구분됨    
- 인코더(Encoder): 양방향 자기어텐션(bidirectional self-attention)    
- 디코더(Decoder): 단방향 자기어텐션(unidirectional self-attention)    
	- 셀프 어텐션 정보를 왼쪽 (이전 토큰)에서만 가져 옴.
- 인코더-디코더(Encoder-Decoder): 인코더와 디코더를 모두 사용



### Applications of Transformer Architectures
- 인코더(예: BERT)    
	- 양방향 문맥을 활용하여 각 토큰의 표현을 학습    
	- 자연어 이해(NLU) 태스크에 적합    
- 디코더(현대 대형 언어 모델, 예: GPT)  → **생성에 집중된 모델**
	- 이전 문맥을 기반으로 다음 토큰을 예측(전통적인 언어 모델링)    
		- 과거 정보만 봄.
	- 자연어 생성(NLG) 태스크에 적합    
	- 클래스 라벨을 토큰으로 생성하는 방식으로 NLU 태스크에도 활용 가능    
- 인코더-디코더(예: BART, T5)    
	- 추천시스템, 시계열 분석등 특수한 어플리케이션에 자주 사용.
	- 인코더로 입력을 처리하고 디코더로 출력을 생성    
	- 인코더/디코더가 수행할 수 있는 모든 태스크를 수행 가능
	- 이전에는 많이 사용되었지만 지금 주류는 아님.
		- 인코더로 정보를 요약후 디코더로 생성하면 좋지 않을까? 했는데 디코더 모델만으로도 충분히 성능이 좋아 잘 사용 되지 않음.
- NLU(자연어 이해)    
	- 텍스트 분류(text classification)    
	- 개체명 인식(named entity recognition)    
	- 관계 추출(relation extraction)    
	- 감성 분석(sentiment analysis)    
- NLG(자연어 생성)    
	- 텍스트 요약(text summarization)    
	- 기계 번역(machine translation)    
	- 대화 시스템(dialogue system)    
	- 질의응답(question answering)

### Decoder Pretraining
- 디코더 아키텍처는 대형 언어 모델에서 주요 선택지
	- 현재 LLM에 가장 많이 사용되는 아키텍쳐
	- GPT가 선구 주자
- 디코더 사전학습은 GPT 모델에서 처음 도입됨(생성 기반 사전학습)
- 표준 언어 모델링 목표(cross-entropy)를 따름  
$$  
\mathcal{L}(\theta) = - \frac{1}{N} \sum_{i=1}^{N} \log p_{\theta}(x_i \mid x_1, x_2, \ldots, x_{i-1})  
$$

- 랭귀지 모델은 본질적으로 classification 모델임.
- 그래서 크로스 엔트로피를 사용
- 이런 방식을 오토 리그레시브 auto regressive 라고도 함.
- 넥스트 토큰을 예측하는게 목표임.

### GPT Series
- GPT-1 (2018): 12개 레이어, 1.17억(117M) 파라미터, 약 1주 학습
- GPT-2 (2019): 48개 레이어, 15억(1.5B) 파라미터, 약 1개월 학습
- GPT-3 (2020): 96개 레이어, 1750억(175B) 파라미터, 수개월 학습

- 현재는 GPT5 까지 나오면서 모델의 크기가 점점 커지고 있음.
- 모델은 기하급수적으로 커지고 학습에 걸리는 시간은 점점 늘어나고 있음.

### Llama Series
- Llama-1 (2023/02): 7B/13B/33B/65B 
- Llama-2 (2023/07): 7B/13B/70B 
- Llama-3 (3.1 & 3.2) (2024/07): 1B/3B/8B/70B/405B w/ multi-modality

- 오픈소스중에서는 라마가 선두주자.
	- 최근에는 Gemma도 많이 사용.(제미나이 기반반)
- 큰 모델이 학습로스를 낮추고 있음을 그래프로 그려 놓음.

### Further Reading on Decoder LMs
- Mistral 7B (2023)    
	- 약 70억(7B) 파라미터 규모의 경량 고성능 언어 모델    
- Qwen (2023)    
	- 다양한 크기와 멀티모달 기능을 지원하는 대규모 언어 모델 계열    
- GPT-4 (2023)    
	- 높은 성능과 추론 능력을 갖춘 대형 언어 모델    
- Gemma (2024)    
	- Gemini 연구 기반으로 개발된 공개(open) 모델 시리즈



### Encoder Pretraining: BERT
- BERT는 양방향성을 활용하여 인코더 모델을 사전학습함    
- 마스크드 언어 모델링(MLM): 전체 단어의 약 15 를 무작위로 마스킹하고, 양방향 문맥 정보를 활용하여 가려진 단어를 예측하도록 학습



### Encoder Pretraining: BERT
- 다음 문장 예측(NSP, Next Sentence Prediction): 모델은 문장 쌍을 입력으로 받음    
- 각 문장 쌍이 학습 코퍼스에서 실제로 이어진 인접 문장인지, 아니면 서로 관련 없는 문장 쌍인지를 예측하도록 학습됨

### BERT Fine-Tuning
- 사전학습된 BERT 모델의 파인튜닝은 태스크 유형에 따라 다양한 형태를 가짐    
- 일반적으로 언어 모델 헤드(LM head)를 제거하고, 태스크별 데이터에 맞게 학습되는 선형 레이어(linear layer)로 대체


### BERT vs. GPT on NLU tasks
- BERT는 다양한 NLU 태스크에서 GPT-1보다 더 높은 성능을 보임    
- 인코더는 양방향 문맥을 포착하여, 이전 단어와 이후 단어를 모두 고려한 더 풍부한 텍스트 이해를 구축    
- 인코더 모델이 최신 대형 디코더 모델보다 여전히 더 나은가?    
- 대형 언어 모델(LLM)은 NLU에서도 인코더 모델만큼 또는 그 이상으로 좋은 성능을 보일 수 있음 (예: ChatGPT)    
- 매우 큰 모델 크기와 방대한 사전학습 데이터가 디코더의 단방향 처리 한계를 보완함

- 현존 GPT5는 모델이 너무 커져서 Bert와 비교하는게 의미가 없음.

### BERT Variant I: RoBERTa
- 더 오랜 시간 동안, 더 큰 배치와 더 많은 데이터로 사전학습 수행    
- **더 긴 시퀀스**에 대해 사전학습 수행    
- 각 에폭(epoch)마다 학습 데이터에 적용되는 마스킹 패턴을 동적으로 변경


### BERT Variant II: ELECTRA
- 작은 MLM 모델을 보조 생성기(auxiliary generator)로 사용(사전학습 후 폐기됨)    
- 메인 모델은 판별기(discriminator)로 사전학습됨    
- 작은 보조 MLM과 메인 판별기를 공동으로 학습    
- 사전학습이 진행될수록 메인 모델의 학습 과제가 점점 더 어려워짐    
- 주요 장점    
	- 샘플 효율성(sample efficiency) 향상    
	- 학습 커리큘럼(learning curriculum) 효과

- 랜덤하게 마스킹하는게 최선인가? → 모델 성능이 올라가면 마스킹 되는 부분이 더 어려워져야 성능이 올라간다고 판단해서 이런 모델이 탄생
- 이런 학습을 커리큐럼 학습방법론이라고 함.
	- 널리 연구되고 있음

### ELECTRA Performance
- ELECTRA는 MLM 대비 더 낮은 계산 비용으로 사전학습 가능    
- 다운스트림 태스크에서 더 우수한 성능을 보임


### Further Reading on Encoder LMs
- XLNet    
	- 순열 기반 언어 모델링(permutation language modeling)을 통해 양방향 문맥을 학습하면서도 자기회귀 방식 유지    
- ALBERT    
	- 파라미터 공유와 임베딩 분해를 통해 모델 크기를 줄이면서 성능 유지    
- DeBERTa    
	- disentangled attention을 통해 내용(content)과 위치(position) 정보를 분리하여 더 정교한 표현 학습    
- COCO-LM    
	- 텍스트 시퀀스를 교정(correcting)하고 대비(contrasting)하는 방식으로 표현 학습 강화


### Encoder-Decoder Pretraining: BART
- 사전학습(pretraining): 입력 시퀀스에 **다양한 노이징(noising) 기법(예: 마스킹, 삭제, 순열 등)을 적용**하고, 원래 시퀀스를 복원하도록 모델을 학습    
	- BERT는 마스킹만 사용했지만 BART는 더 다양한 노이징 방법을 이용해서 모델 학습.
- 파인튜닝(fine-tuning)    
	- NLU 태스크: 동일한 입력을 인코더와 디코더에 함께 넣고, 디코더의 마지막 토큰을 사용하여 분류 수행    
	- NLG 태스크: 인코더가 입력 시퀀스를 처리하고, 디코더는 자기회귀적으로 출력을 생성


### BART Performance
- 인코더 기반 모델과 비교했을 때 NLU 태스크에서도 유사한 성능을 보임    
- NLG 태스크에서는 우수한 성능을 달성



### Encoder-Decoder Pretraining: T5
- T5: Text-to-Text Transfer Transformer    
- 사전학습(pretraining): 텍스트의 일부 구간(span)을 마스킹하고, 해당 원래 구간을 생성하도록 학습    
- 파인튜닝(fine-tuning): 모든 태스크를 시퀀스-투-시퀀스(sequence-to-sequence) 생성 문제로 변환하여 학습    
- 이후 instruction tuning 강의에서 다시 다룰 예정

- 전에 아주 인기가 있었음.
- Q&A느낌이 있음.
	- 텍스트를 가려놓고 생성하도록 모델링을 함.
	- 사전에 학습한 내용을 기반으로 정보전달을 잘 할 수 있도록 학습된 모델.
	- 르즈벨트가 태어난 년도는? → 1882

### T5 Performance
- 다양한 태스크에서 우수한 성능을 보임    
- T5와 BART의 성능 비교는 모델 크기 및 학습 설정 차이로 인해 명확하게 판단하기 어려움


### Encoder-Decoder vs. Decoder-Only
- 현대 대형 언어 모델(LLM)은 대부분 디코더 전용(decoder-only) 트랜스포머 아키텍처를 기반으로 함    
- 단순성(Simplicity)    
	- 디코더 전용 모델은 구조가 더 단순함(하나의 트랜스포머만 사용)    
	- 인코더-디코더 모델은 두 개의 트랜스포머가 필요    
- 효율성(Efficiency)    
	- 디코더 전용 모델은 텍스트 생성에서 파라미터 효율성이 높음    
	- 인코더-디코더 모델의 인코더 부분은 생성 과정에 직접 기여하지 않음    
- 확장성(Scalability)    
	- 디코더 전용 모델은 모델 크기와 데이터가 증가할수록 매우 잘 확장됨    
	- 대규모 환경에서는 인코더-디코더 모델이 디코더 전용 모델보다 성능 우위를 보이지 않음
