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
![[5.1 Transformers details_page-0024.jpg]]
### 1. Masked language modeling (MLM)
- BERT에 들어가는 데이터는 라지 랭귀지임.
- MLM에서는 마스크라는 스페셜 토큰으로 치환 됨.
- 그 다음 가려진 단어가 무엇인지 BERT가 맞춰야 함.
![[5.1 Transformers details_page-0025.jpg]]

- 셀프 어텐션의 특징은 어떤 단어가 중요한지 찾는 것임.
	- 뱅크를 맞추려면 피크닉과 리버를 알아야 하고 유의미하게 연결 되었다는 것을 찾아야 함.
	- 모델에게 어떤 단어가 중요한지를 가르쳐 주는 모델이라고 볼 수 있음.
![[5.1 Transformers details_page-0026.jpg]]

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
![[5.1 Transformers details_page-0027.jpg]]

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

![[5.1 Transformers details_page-0028.jpg]]
- weight tying은 모델 크기를 줄이고 중복을 방지함
	- 입력 임베딩 행렬 $E$와 출력 가중치 $W$를 공유하여 별도의 파라미터를 두지 않음  
$$  
W = E^{\top}  
$$
- 임베딩 E의 트랜스포즈 한것을 웨이트 벡터로 사용??
- 동일한 단어 표현을 입력과 출력에서 함께 사용하여 파라미터 효율성과 일반화 성능을 향상시킴
![[5.1 Transformers details_page-0029.jpg]]
- 이진 문제를 풀도록 만듦.
![[5.1 Transformers details_page-0030.jpg]]
### 2. Next sentence prediction (NSP)
- 아이디어    
	- 두 문장을 동시에 모델에 입력하며, 특수 토큰 $\text{[SEP]}$→ 세퍼레이션 토큰으로 구분    
	- 입력의 맨 앞에 $\text{[CLS]}$ 토큰을 추가하여 전체 문장 정보를 요약   
		- CLS는 BERT의 모든 문장 앞에 추가되도록 함.
	- 모델은 두 번째 문장이 첫 번째 문장 뒤에 실제로 이어지는지 여부를 예측    
- 문맥 학습에 도움이 되는 이유    
	- 문장 간 일관성(coherence)을 학습하도록 유도 (토큰 수준을 넘어선 이해)    
	- 이후 연구에서는 NSP의 필요성에 대한 논쟁이 있었지만, 이 설계는 많은 후속 연구에 영감을 줌
![[Pasted image 20260504204114.png]]

- MLM보다 긴 호흡에서 문맥을 이해하도록 함.

- **현대 검색이나 추천에 기반이 된 개념이기 때문에 모델 디자인은 알아두는 것이 좋음.**
![[5.1 Transformers details_page-0031.jpg]]

- $y$: 두 문장이 연속적인지 여부(이진 분류)
- $\text{[CLS]}$ 토큰은 전체 입력 문장의 정보를 집약한 표현
- 따라서 $\text{[CLS]}$의 최종 표현 $h_{\mathrm{[CLS]}}^{L}$을 사용하여 두 문장이 이어지는지 예측
- 입력 구성
- 두 문장을 함께 입력으로 사용
- 두 문장 사이에 $\text{[SEP]}$ 토큰을 삽입하여 구분

- \[CLS] token aggregates information from the whole input, not just a single word. So, we use it to predict whether two sentences are consecutive or not
- 문장의 종결을 알려주기 위해 SEP 토큰을 마지막도 추가 하기도 함.
- hCLS가 나오면 이진 분류를 수행해서 O,X 답변
![[5.1 Transformers details_page-0032.jpg]]
- 다음 문장 예측(NSP, Next Sentence Prediction) 손실 함수  
$$  
\mathcal{L}_{\mathrm{NSP}} = - \log P(y \mid h_{\mathrm{[CLS]}}^{L})  
$$

- linear layer + softmax를 이용함.
$$  
\mathbf{y}=\operatorname{softmax}\left(\mathbf{h}_{\mathrm{CLS}}^{L}\mathbf{W}_{\mathrm{NSP}}\right)  
$$
![[5.1 Transformers details_page-0033.jpg]]
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
![[5.1 Transformers details_page-0034.jpg]]

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
