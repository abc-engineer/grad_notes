2026-04-27 08:20
## 7강 LLM & In-Context Learning


### Prompting
- 프롬프트: 텍스트 생성을 안내하기 위해 모델에 제공되는 초기 사용자 입력/지시   
	- LLM에만 사용 되는 것은 아님.
- 예시(감성 분석): 프롬프트 
	- P(positive | The sentiment of the sentence “I like Jackie Chan” is:)
	-  P(negaitive | The sentiment of the sentence “I like Jackie Chan” is:)
- 예시(질문 응답): 프롬프트   
	- P(w | Q: Who wrote the book “The Origin of Species”? A:)
- 프롬프팅: 사용자 프롬프트가 주어졌을 때 학습된 LM을 직접 사용하여 텍스트를 생성하는 것(파인튜닝 없음)  
    좋은 프롬프팅 성능을 위해서는 instruction-tuning이 필요하다(이후 강의)  
    예시 출처: [https://web.stanford.edu/~jurafsky/slp3/10.pdf](https://web.stanford.edu/~jurafsky/slp3/10.pdf)

- 파인튜닝(파라메트릭 업데이트)과 프롬프팅(추론 시점에 입력을 조절해서 모델 출력을 유도하는 방법.)은 차이가 있음.


### Prompt Engineering
- 일부 LM(특히 작은 모델)은 프롬프트의 특정 형식에 민감할 수 있다    
- 동일한 작업에 대해 여러 프롬프트가 가능하지만, 결과 모델 성능은 달라질 수 있다    
- 모델은 마스킹된 단어를 예측한다    
- BERT 감성 분류를 위한 프롬프트 템플릿    
- 프롬프트 엔지니어링: LM으로부터 원하는 결과를 얻기 위해 프롬프트를 설계하고 개선(designing and refining)하는 것(예: 검증 세트에서 수동 튜닝)    
- 프롬프트 엔지니어링 가이드: [https://www.promptingguide.ai/](https://www.promptingguide.ai/)    
- 그림 출처: [https://aclanthology.org/2021.eacl-main.20.pdf](https://aclanthology.org/2021.eacl-main.20.pdf)

- 거대모델은 영향이 적지만 작은 모델에서는 프롬프트 영향이 큼.


### Prompt Tuning
- 프롬프트 튜닝: 프롬프트 설계를 수동으로 시험하는 대신, 프롬프트 토큰을 학습 가능한 모델 파라미터(“soft prompts”)로 간주하는 방법    
	- 프롬프트를 자연어 기반으로 하는 것이 아니라 토큰을 학습 하도록 하는 것.
- LM은 고정(frozen)한 상태로 유지하면서 소량의 프롬프트 토큰 임베딩만 최적화한다    
- 프롬프트 튜닝은 **parameter-efficient fine-tuning(PEFT)** 방법이다    
- 그림 출처: [https://www.googblogs.com/guiding-frozen-language-models-with-learned-soft-prompts/](https://www.googblogs.com/guiding-frozen-language-models-with-learned-soft-prompts/)


- hard prompts: 자연어를 이용.
- soft prompts: 학습가능한 벡터를 이용
	- 모델 튜닝과 프롬프트 디자인 사이에 있는 것이 프롬프트 튜닝(soft prompts)
	- 모델튜닝은 비용이 크고 학습된 지식을 잃을 수도 있음.
		- 언어모델은 건들지 않고 프롬프트만 업데이트 해서 학습하게 함.
	- 프롬프트를 벡터로 변환하여 학습에 사용되도록 함. → 사실 확인 필요!
		- 사람이 쓴 프롬프트를 벡터로 변환하기보다**처음부터 학습 가능한 벡터 프롬프트를 만든다**고 보는 것이 좋음
		- `p1`, `p2`, `p3` 같은 벡터들이 **가상의 토큰 embedding**처럼 입력 앞에 붙고, 학습 과정에서 이 벡터 값만 업데이트


### Parameter Efficient Fine-tuning (PEFT)
- 모든 모델 파라미터를 파인튜닝하는 것은 비용이 크다    
- 사전학습 가중치(어떤 모듈이든 표현 가능)  

$$  
W_0 \in \mathbb{R}^{d \times d}  
$$

- 파인튜닝된 가중치  

$$  
W^* = W_0 + \Delta W, \quad \Delta W \in \mathbb{R}^{d \times d}  
$$

- 파인튜닝 데이터에서 모델 파라미터의 일부만 업데이트할 수 있을까?
- 파인튜닝은 모델 파라미터를 업데이트 하는 것임. 
- 하지만 비싸기 때문에 기존 모델 파라미터는 그대로 두고 파인튜닝하는 방법을 찾게 됨.

- transfer learning → DNN 시절 코어 파라미터는 고정하고 윗 레이어들만 튜닝하는 기법이 있었음.


### Parameter Efficient Fine-tuning: LoRA
- 파라미터 업데이트가 low-rank라고 가정하자
- 과매개변수화(overparameterization): 대규모 언어 모델은 일반적으로 학습 데이터에 정확히 필요한 것보다 훨씬 많은 파라미터를 가진다
- 경험적 관찰: 신경망의 파라미터 업데이트는 실제로 low-rank인 경향이 있다
- 해결책: 가중치 업데이트를 low-rank 분해로 근사한다  

$$  
\Delta W \approx BA, \quad B \in \mathbb{R}^{d \times r}, \quad A \in \mathbb{R}^{r \times d}, \quad r \ll d  
$$

- 사전학습 가중치는 고정(freeze)한다
- low-rank 근사
- LoRA: [https://arxiv.org/pdf/2106.09685](https://arxiv.org/pdf/2106.09685)

- **가장 많이 사용됨.**
- **꼭 이해 해야 하는 내용**
- 현재 LLM 파인튜닝은 그냥 LoRA 파인튜닝이라고 보면 됨.
- 추가해야 하는 새로운 지식들은 몇개의 기저백터로 충분하다고 생각함.
	- 대부분 학습된 내용은 유지해도 무방함.
- d by d 매트릭스를 작은 차원 로우랭크A,B로 변화함.
	- 그 후 A,B를 업데이트해서 전체 업데이트를 모방하는 효과를 낼 수 있음.
	- B: d by r
	- A: d by r
	- 정도로 축약해서 r(보통 8 정도)을 이용
	- 다운스트림 테스크에서는 1% 수준에 업데이트인데도 full 파인 튜닝과 유사한 결과를 얻음.


###  LoRA in Frontier Research
- LoRA 파인튜닝은 frontier LLM의 사후 학습(post-training)에 효과적이다(예: 강화학습)



### Q&A
- PEFT는 full finetuning만큼 효과는 안나옴.
- LoRA의 하이퍼 파라미터는 개발자의 판단에 따라 달라짐. 보통 가용자원에 맞춰 최대한 사용 하게 됨.
	- r은 8~16정도 사용.
- Prompt tuning은 사람이 하는것이 아님.
	- 세타를 소프트 프롬프트로 넣고 경사하강법을 이용해서 미분 후 연산 하도록 설계
	- 인풋 레벨의 최적화임.
	- 소프트 프롬프트의 크기 만큼 인풋의 크기가 커지게 됨.




###  Large Language Models (LLMs)
- LLM 분야는 빠르게 발전하고 있다!    
- 2018년에는 3억 4천만 개 파라미터를 가진 BERT-large가 큰 모델로 간주되었다    
- 2019년에는 15억 개 파라미터를 가진 GPT-2가 매우 큰 모델로 간주되었다    
- 2020년에는 1,750억 개 파라미터를 가진 GPT-3가 “large”의 새로운 기준을 세웠다    
- 2026년에는 LLM을 어떻게 정의해야 할까?    
- 일반적 정의:    
	- 텍스트를 생성할 수 있는 Transformer-decoder 아키텍처(또는 변형)   
		- 생성 특화화
	- 방대하고 다양한 일반 도메인 말뭉치로 사전학습됨    
	- 적어도 수십억 개의 파라미터를 가짐    
	- 광범위한 NLP 작업 및 그 이상을 위한 범용 해결기

### Decoding with LLMs
- 디코딩(decoding): Transformer 표현을 자연어 토큰으로 변환하는 과정
- 자기회귀(autoregressive) 디코딩은 일반적으로 LM의 출력 분포에서 반복적으로 샘플링하며, \[EOS] 토큰이 생성될 때까지 진행된다  

$$  
p_\theta(w_i \mid x_1, x_2, \ldots, x_{i-1})  
=  
\mathrm{softmax}(U h_{i-1})  
=  
\left[  
\frac{\exp(u_1 \cdot h_{i-1})}{\sum_{j=1}^{|V|} \exp(u_j \cdot h_{i-1})},  
\ldots,  
\frac{\exp(u_{|V|} \cdot h_{i-1})}{\sum_{j=1}^{|V|} \exp(u_j \cdot h_{i-1})}  
\right]  
$$
- 모델 파라미터
- 언임베딩(unembedding) 행렬
- 토큰 (i-1)에서의 은닉 상태(hidden states)
- 그림 출처: [https://web.stanford.edu/~jurafsky/slp3/8.pdf](https://web.stanford.edu/~jurafsky/slp3/8.pdf)

- 인풋하고 →트랜스포머 블록을 지나고 → 마지막 h가 언임베딩 레이어로 들어가고 → 소프트 맥스를 해서 → 확률 높은 답변을 하게 됨.


### Greedy Decoding
- 각 단계마다 LM이 추정한 가장 높은 확률의 토큰을 항상 선택한다  

$$  
x_i \leftarrow \arg\max_w p_\theta(w \mid x_1, x_2, \ldots, x_{i-1})  
$$

#### 장점:
- 단순성: 구현과 이해가 쉽다
- 결정론적(deterministic): 동일한 입력에 대해 항상 동일한 출력을 보장한다
- 효율적: 각 단계에서 추가 연산 없이 하나의(단순한) 결정만 수행한다
#### 단점:
- 부분 최적 해(suboptimal solutions): 전역적으로 최적의 시퀀스를 찾지 못할 수 있다
- 다양성 부족: 동일한 입력에 대해 여러 출력을 생성할 수 없다


### Top-𝑘 Sampling
- 동기(motivation): 생성할 단일 최고 확률 단어를 선택하는 대신, 확률이 가장 높은 상위 (k)개의 토큰(후보)에서 샘플링한다 — 낮은 확률 토큰 생성을 방지
- (k)는 하이퍼파라미터이다(일반적으로 5–10)
- 확률 분포는 상위 (k)개 토큰에 대해서만 계산한다  

$$  
p_\theta(w \mid x_1, x_2, \ldots, x_{i-1})  
=  
\mathrm{softmax}(U_{\mathrm{top}\text{-}k} h_{i-1})  
=  
\left[  
\frac{\exp(u_1 \cdot h_{i-1})}{\sum_{j=1}^{k} \exp(u_{\mathrm{top}\text{-}j} \cdot h_{i-1})},  
\ldots,  
\frac{\exp(u_{\mathrm{top}\text{-}k} \cdot h_{i-1})}{\sum_{j=1}^{k} \exp(u_{\mathrm{top}\text{-}j} \cdot h_{i-1})}  
\right]  
$$

- 상위 (k)개 토큰에서 샘플링한다  

$$  
x_i \sim p_\theta(w \mid x_1, x_2, \ldots, x_{i-1})  
$$

- (k = 1)인 경우, top-(k) 샘플링은 greedy decoding과 동일하다
- 효과
	- k 개 내에 샘플링 되지 않는다면 그 답변이 채택될 확률은 0이 되기 때문에 엉뚱한 답변이 나올 확률을 원천적으로 배제 하게 됨.


### Nucleus (Top-𝑝) sampling
- **Top-$k$ 샘플링은 확률 분포의 형태를 고려하지 않는다**
	- 항상 고정된 k 값을 갖게 됨.
	- “the 46th US president Joe”의 다음 토큰 분포에서는 Top-$k$ 샘플링이 필요한 것보다 더 많은 토큰을 고려할 수 있다
	- “the spacecraft”의 다음 토큰 분포에서는 Top-$k$ 샘플링이 필요한 것보다 더 적은 토큰을 고려할 수 있다
- Nucleus 샘플링은 **확률 질량의 상위 $p$ 퍼센트를 기준으로 컷오프**를 설정한다
	- $p$는 하이퍼파라미터이다(일반적으로 $0.9$)
- Top-$p$ 어휘는 다음을 만족하는 가장 작은 단어 집합이다  

$$  
\sum_{w \in V_{\mathrm{top}\text{-}p}} p(w \mid x_1, x_2, \ldots, x_{i-1}) \ge p  
$$

- Top-$p$ 어휘에서 Top-$k$ 샘플링과 유사한 방식으로 샘플링한다


###  Temperature Sampling
- 직관(intuition)은 열역학(thermodynamics)에서 비롯된다
- 높은 온도의 시스템은 유연하며 많은 가능한 상태를 탐색할 수 있다
- 낮은 온도의 시스템은 더 낮은 에너지(더 나은) 상태의 부분집합을 탐색하는 경향이 있다
- temperature 하이퍼파라미터를 도입하여 확률 분포를 재구성한다 

$$  
p_\theta(w \mid x_1, x_2, \ldots, x_{i-1})  
=  
\mathrm{softmax}(U h_{i-1} / \tau)  
=  
\left[  
\frac{\exp(u_1 \cdot h_{i-1} / \tau)}{\sum_{j=1}^{|V|} \exp(u_j \cdot h_{i-1} / \tau)},  
\ldots,  
\frac{\exp(u_{|V|} \cdot h_{i-1} / \tau)}{\sum_{j=1}^{|V|} \exp(u_j \cdot h_{i-1} / \tau)}  
\right]  
$$

- $\tau \to 0$이면, temperature sampling은 greedy decoding에 가까워진다

- 그림 출처: [https://arxiv.org/pdf/1611.01144v5](https://arxiv.org/pdf/1611.01144v5)

- 확률분포를 원하는 대로 조절하는 기법임.
- 소프트 맥스 전에 T라는 스칼라 값으로 나눠준 후 소프트 맥스 함.
- t=1이면 원래 분포.
- t<1 원래 큰값이 더 커지고 나머지는 더 적어짐 → 그리딩 방식과 유사해짐.
- t>1 모든 로직들이 비슷해짐.
- 언제나 원하는 답이 나오길 원하면 t를 낮게, 여러 답을 듣고 싶으면 t를 높게 하면 됨.
- 오픈소스 LLM에서는 많이 조절 하게 됨.

### Practical Considerations of Decoding Algorithms
- **단순성과 효율성을 목표로 하며 다양성이 필요하지 않다면 greedy decoding**을 사용한다
- 동일한 입력에 대해 여러 응답이 필요하다면 sampling-based decoding을 사용한다
- Top-(p)는 일반적으로 Top-(k)보다 더 좋다
- Temperature sampling은 흔히 사용된다
- Top-(p)는 temperature sampling과 함께 사용할 수 있다





###  In-context Learning
- In-context learning은 few-shot learning의 한 종류이다
- 사용자는 프롬프트 안에 입력-출력 쌍의 몇 가지 예시를 제공한다
- 모델은 주어진 예시를 사용하여 새로운 유사 입력에 대한 출력을 예측한다
- 처음에는 GPT-3 논문에서 연구되었다
- 모델 파라미터 업데이트는 없다
- 그림 출처: [https://arxiv.org/pdf/2005.14165](https://arxiv.org/pdf/2005.14165)

- 일종의 few-shot러닝임. 인풋 아웃풋의 예시 몇개를 제공하면 이런 스타일로 출력이 유도 됨.
- 파인튜닝은 파라미터 업데이트 또는 In-context Learning 
	- In-context Learning는 파라미터 업데이트 없음.


### In-context Learning Demo
- 프롬프트만 주어진 경우 잘못된 생성이 발생할 수 있다
- 예시 프롬프트:  

$$  
\text{Swap the second and the penultimate letter of the following word: pothyn}  
$$
- 모델은 “pothyn”의 두 번째 글자와 끝에서 두 번째 글자를 교환해야 하지만, 잘못된 결과를 생성했다
- 이러한 사례는 LM이 문자 수준(letter-level) 조작 작업에서 오류를 낼 수 있음을 보여준다
- 그림 출처: [https://lmarena.ai/](https://lmarena.ai/)


- In-context 예시로부터 올바른 패턴을 학습할 수 있다

- 예시 프롬프트:  

$$  
\text{Directly answer the last one (swapping the second and the penultimate letter of the following words): tarehd } \rightarrow \text{ thread, revir } \rightarrow \text{ river, pothyn } \rightarrow  
$$

- 모델은 앞선 예시들로부터 규칙을 학습하여 다음과 같이 올바르게 생성한다  

$$  
\text{pothyn } \rightarrow \text{ python}  
$$

- 이는 in-context learning이 새로운 입력에 대한 규칙 일반화에 도움을 줄 수 있음을 보여준다
- 그림 출처: [https://lmarena.ai/](https://lmarena.ai/)

- 프롬프트만 주어진 경우 잘못된 생성이 발생할 수 있다
- 예시 프롬프트:  

$$  
\text{How many 'r' letters are there in the following word: "strawberry"}  
$$

- 모델은 “strawberry”에 ‘r’이 2개 있다고 잘못 답변했지만, 실제로는 3개이다
- 이러한 사례는 LM이 문자 수준 계산이나 counting 작업에서 오류를 낼 수 있음을 보여준다
- 그림 출처: [https://lmarena.ai/](https://lmarena.ai/)

- In-context 예시를 통해 올바른 counting 규칙을 학습할 수 있다
- 예시 프롬프트:  

$$  
\text{Count how many 'r' letters are there in the following words: "red": 1, "roar": 2, "strawberry":}  
$$

- 모델은 앞선 예시들로부터 패턴을 학습하여 “strawberry”의 ‘r’ 개수를 올바르게 3개라고 계산한다
- 이는 in-context learning이 문자 수준 counting 작업에서도 성능을 향상시킬 수 있음을 보여준다
- 그림 출처: [https://lmarena.ai/](https://lmarena.ai/)



### Scaling Up Pretraining Data
- The Pile: 22개의 하위 데이터셋(800GB 이상)으로 구성된, 사전학습 말뭉치(pretraining corpus)로 널리 사용되는 데이터셋
- 다양한 LLM에 공개데이터들이 학습됨.


### Scaling Up Model Sizes Scaling Up Model Sizes
- GPT-1 (2018): 12개 레이어, 1억 1,700만 개 파라미터, 약 1주 동안 학습  
- GPT-2 (2019): 48개 레이어, 15억 개 파라미터, 약 1개월 동안 학습    
- GPT-3 (2020): 96개 레이어, 1,750억 개 파라미터, 수개월 동안 학습


### Emergent Ability
- 더 큰 모델은 emergent abilities(창발 능력)를 발달시킨다    
	- **emergent abilities은 명시적으로 학습되지 않았지만, 모델의 용량(capacity) 증가의 결과로 나타나는 기술이나 능력**이다    
	- 더 큰 모델은 해당 작업을 위해 명시적으로 학습되지 않았더라도 어려운 작업에서 놀라운 능력을 보인다    
- emergent abilities은 **일반적으로 모델 크기가 특정 임계값(threshold)에 도달했을 때만 두드러지게 나타난다**    
- 따라서 작은 모델의 성능만으로는 이러한 능력을 예측할 수 없다

- 이게 모델의 크기를 키우는 대표적 이유 중 하나. 


###  Experiment Setting
- Few-shot in-context learning 패러다임을 고려한다
	- 파라미터 업데이트 없이 예시를 이용해서 파인튜닝을 진행.
- 모델이 특정 규모에 도달하기 전까지는 무작위 성능을 보이다가, 그 이후 성능이 무작위보다 훨씬 높게 증가할 때 해당 능력을 emergent ability로 간주한다
- 테스트할 능력:
	- 산술: 덧셈, 뺄셈, 곱셈
	- 음역(transliteration)
	- 뒤섞인 글자에서 단어 복원
	- 페르시아어 질의응답
	- 질의응답(진실하게 답하기)
	- 근거 기반 개념 매핑(grounded conceptual mappings)
	- 멀티태스크 이해(수학, 역사, 법률 등)
	- 문맥화된 의미 이해(contextualized semantic understanding)

### Performance vs. Model Scale
- **모델은 특정 규모에 도달하기 전까지 무작위(random) 수준의 성능을 보이다가, 이후 성능이 급격히 증가하는 경향**을 보인다    
- 이러한 현상은 emergent abilities의 특징이다    
- 평가 작업 예시:    
	- 모듈러 산술(modular arithmetic)    
	- IPA 음역(IPA transliteration)    
	- 단어 복원(word unscramble)    
	- 페르시아어 질의응답(Persian QA)    
	- TruthfulQA    
	- grounded mappings    
	- 멀티태스크 자연어 이해(multi-task NLU)    
	- 문맥 내 단어 이해(word in context)    
- 작은 모델의 성능만으로는 대규모 모델의 능력을 예측하기 어렵다
- 거의 모든 모델에서 발견된 현상.

### Scaling Laws of LLMs
- (사전학습된) LLM 성능은 주로 3가지 요인에 의해 결정된다
	- 모델 크기: 파라미터 수
	- 데이터셋 크기: 학습 데이터의 양
	- 컴퓨트(연산): 학습에 사용된 floating point operations(FLOPs)의 양 → GPU 및 시간에 영향을 받음.
- LLM 스케일링은 위 3가지 요인을 확장하는 것을 포함한다
	- 더 많은 파라미터 추가(더 많은 레이어 추가, 더 큰 모델 차원 사용, 또는 둘 다)
	- 더 많은 데이터 추가
	- 더 많은 반복 학습
- 스케일링 법칙(scaling laws): cross-entropy language modeling loss와 위 세 요인 사이의 상관관계를 연구한다
- **고정된 컴퓨트 예산을 어떻게 최적으로 할당**할 것인가?

- 다른 두 요인이 병목이 되지 않을 때, 성능은 세 가지 스케일 요인(모델 크기, 데이터셋 크기, 컴퓨트) 각각과 power-law(롱테일한 관계) 관계를 가진다
- 3번재 표를 보면 테스트 로스를 4→2.4로 낮추는데 파라미터를 10의 5승에서 9승으로 10,000 배 늘어남. 더 낮추려면 갈수록 더 많은 자원이 필요함.

### Scaling Model Parameters
- 언어 모델 loss와 제한된 수의 파라미터를 가진 모델((N))의 관계
- 임베딩이 아닌(non-embedding) 파라미터만 계산한다
- 무한한 컴퓨트: 수렴할 때까지 학습
- 무한한 데이터셋: 충분히 큰 데이터셋으로 학습
- 성능은 모델 형태(shape)(깊이 vs. 너비)보다는 스케일에 강하게 의존한다  

$$  
\mathcal{L}(N)  
=  
\left(\frac{N_c}{N}\right)^{\alpha_N},  
\quad  
\alpha_N \approx 0.076,  
\quad  
N_c \approx 8.8 \times 10^{13}  
$$
- 여기서 (N)은 모델 파라미터 수(non-embedding)이다

### Scaling Dataset Size
- 언어 모델 loss와 제한된 데이터셋 크기$(D)$의 관계
- 무한한 모델 크기: 충분히 큰 모델
- 적절한 early stopping 사용: 학습 데이터에 대한 과적합(overfitting) 방지  

$$  
\mathcal{L}(D)  
=  
\left(\frac{D_c}{D}\right)^{\alpha_D},  
\quad  
\alpha_D \approx 0.095,  
\quad  
D_c \approx 5.4 \times 10^{13}  
$$
- 여기서 (D)는 데이터셋 크기(토큰 수)이다

### Scaling Training Compute
- 언어 모델 loss와 제한된 컴퓨트 양$(C)$의 관계
- 무한한 데이터셋 크기: 충분히 큰 학습 corpus
- 최적 모델 크기: 데이터를 효과적으로 학습하면서도 과도한 컴퓨트를 사용하지 않음  

$$  
\mathcal{L}(C)  
=  
\left(\frac{C_c}{C}\right)^{\alpha_C},  
\quad  
\alpha_C \approx 0.050,  
\quad  
C_c \approx 3.1 \times 10^8  
$$

- 여기서 (C)는 컴퓨트 양(Peta-FLOP days)이다

### Optimal Model Size
- 주어진 학습 컴퓨트 $C$에 대해, 언어 모델링 loss를 최소화하는 최적 모델 크기 $N(C)$는 무엇인가?
- $N(C)$는 $C$에 대한 power-law로 피팅할 수 있다
- 모델 크기가 최적이 아닐 때는 추가 컴퓨트를 사용해야 한다  

- 이정도를 이용해서 기업에서 자원이 한정되어 있을때 어느정도 자원을 할당하면 될지 추정할 수 있다는 의의를 갖는 논문.


