2026-05-18 08:20
## 8강 RAG


### Introduction to Question Answering
- 질의응답(Question Answering, QA): 인간이 자연어로 제시한 질문에 자동으로 답할 수 있는 시스템을 구축하는 것
- 응용 도메인에 따른 분류: **폐쇄 도메인(closed-domain) QA와 개방 도메인(open-domain) QA**
- closed-domain 폐쇄 도메인 QA: 특정 도메인 내의 질문에 답하는 방식
	- 예: 의료, 법률, 기술 분야
	- 모델은 **해당 도메인 내에서 높은 정확도를 갖도록 전문 지식으로 학습**된다.
	- 도메인특화의 방대한 데이터를 요구하는 경우가 많음.
- open-domain 개방 도메인 QA: 어떤 도메인의 질문에도 답하는 방식
	- 일반 유저 대상의 질의
	- 일반적으로 웹이나 대규모 텍스트 말뭉치 같은 방대한 외부 지식원에 의존한다.
	- 범용 데이터 학습이 유리함.
	- 대부분의 LLM 응용은 개방 도메인 QA 설정을 고려한다.


- 질의응답(Question Answering, QA): 인간이 자연어로 제시한 질문에 자동으로 답할 수 있는 시스템을 구축하는 것
- 모델링 접근 방식에 따른 분류: **추출형(extractive) QA와 생성형(abstractive) QA**
- extractive 추출형 QA: **주어진 문맥(context)에서 직접 추출한 텍스트 범위를 출력**하는 방식
	- 자연어 이해(natural language understanding) 과제이며, 독해(reading comprehension)에 해당한다.
	- 예:
		- 문맥: “The human brain contains approximately 86 billion neurons”
		- 질문: “How many neurons are in the human brain?”
		- 답변: “86 billion”
	- 인코더 전용 언어모델(encoder-only LM), 예를 들어 BERT로 수행할 수 있다.
		- 생성형 언어모델이 아니어도 가능함.
- abstractive 생성형 QA: **답변을 자신의 표현으로 합성하는 방식**이며, 재표현(rephrasing) 또는 요약(summarizing)을 포함한다.
	- 예:
		- 문맥: “Albert Einstein published his theory of special relativity which introduced the famous equation $E=mc^2$, which relates energy $E$ to mass $m$ and the speed of light $c$”
		- 질문: “What did Einstein contribute to physics?”
		- 답변: “Einstein made significant contributions to the theory of special relativity which established the relationship between energy and mass”
		- 생성형 언어모델(generative LM), 예를 들어 GPT를 사용해야 한다.

- 질의응답(Question Answering, QA): 인간이 자연어로 제시한 질문에 자동으로 답할 수 있는 시스템을 구축하는 것
- 외부 소스 접근 여부에 따른 분류: **폐쇄형(closed-book) QA와 개방형(open-book) QA**
- closed-book 폐쇄형 QA: 외부 정보에 접근하지 않고 질문에 답하는 방식
	- 정확도는 학습 데이터가 관련 정보를 얼마나 잘 포함했는지에 크게 의존한다.
	- 사람이 아무것도 찾아보지 않고 기억에 의존해 질문에 답하는 것과 비슷하다.
- open-book 개방형 QA: 질문에 답하기 위해 외부 지식원에 접근할 수 있는 방식
	- 일반적으로 신뢰할 수 있는 외부 소스에서 검색(retrieval)을 사용한다.
	- 사람이 책이나 온라인 자료를 찾아보며 질문에 답하는 것과 비슷하다.



### Prompting LMs: Parametric Knowledge
- 언어모델(Language Models, LMs)은 **사전학습(pretraining) 데이터로부터 많은 사실(facts)을 학습**한다.
- 언어모델은 사실 기반 질문(factoid questions)에 대해 직접 프롬프트(prompt)를 받아 답변을 생성할 수 있다. 이는 폐쇄형 QA(closed-book QA) 설정이다.
- 예:

$$  
P(w \mid Q:\text{“Who wrote the book ‘The Origin of Species’?”},A:)  
$$
- 프롬프팅(prompting)을 사용하는 언어모델은 모델의 매개변수(parameters)에 저장된 정보에만 의존하므로, 이러한 종류의 지식을 매개변수적 지식(parametric knowledge)이라고 부른다.


### Language Model as Knowledge Bases
- 획득(acquisition): 언어모델(LM)의 지식은 방대한 양의 사전학습(pretraining) 데이터로부터 얻어진다.
- 접근(access): 정보는 자연어 프롬프트(natural language prompts)를 통해 접근된다.
- **업데이트/유지관리(update/maintenance): 새로운 데이터로 모델을 재학습(re-training)하거나 미세조정(fine-tuning)** 한다.
- 장점(pros):
	- 문맥 이해(contextual understanding)를 바탕으로 다양한 자연어 질의(natural language queries)를 처리할 수 있다.
	- 학습 중 보지 못한 새로운 질의(unseen queries)에 일반화할 수 있다.
- 단점(cons):
	- **부정확하거나 오래된 정보를 생성할 수 있다.**
	- **해석가능성(interpretability)과 투명성(transparency)이 부족하다.**


### (Real) Knowledge Bases
- 획득(acquisition): 인간 주석자(human annotators)에 의해 수동으로 구축된다.
- 접근(access): 정보는 특정 형식의 질의(queries)를 통해 접근된다.
- 업데이트/유지관리(update/maintenance): 사람이 항목(entries)을 추가, 수정, 삭제하는 방식으로 점진적으로(incrementally) 관리된다.
- 장점(pros):
	- **정확하고 검증 가능하다**(precise & verifiable).
- 단점(cons):
	- **자연어(natural language)를 처리할 수 없다.**
		- 특수한 형태로 쿼리를 처리해서 넣어줘야 함.
	- **구축과 유지관리에 막대한 인간의 노력이 필요**하다.

- Knowledge Graph 진짜 지식기반 모델이라고 볼 수 있음
	- 단테와 피렌체라는 노드가 born-in이라는 엣지로 연결됨
	- 어마어마한 양의 학습데이터가 필요함.


### Feedforward Parameters in Transformer
- Transformer의 FFN(Feed-Forward Network)은 2층 신경망(one hidden layer, two weight matrices)이다.

$$  
\text{FFN}(x_i)=\text{ReLU}(x_iW^1)W^2  
$$
- **FFN은 Transformer 전체 매개변수(parameters)의 약 $\frac{2}{3}$를 차지**한다.
	- 굉장히 큰 비중임. 셀프어텐션은 1/3 밖에 안됨.

- 트랜스포머 모델에는 어느 단계에서 지식이 쌓이는지 의문을 갖게 됨
	- 셀프어텐션으로 기초 지식학습 후 다음 FFN으로 넘어가게 됨
	- FFN에 지식이 쌓인다고 일반적으로 알려짐.
	- 그리고 FFN은 키와 밸류 연산으로 구성됨.


### Feedforward Parameters Are Neural Memories
- **FFN을 key-value 메모리(key-value memories)로 볼 수 있다.**  

$$  
\text{FFN}(x_i)=\text{ReLU}(x_iW_1)W_2  
$$

$$  
x_i\in\mathbb{R}^{d_1}  
$$
- 이를 다음과 같이 쓸 수 있다.  

$$  
\text{FFN}(x_i)=\text{ReLU}(x_iK)V  
$$  

$$
\begin{align}
K\in\mathbb{R}^{d_1\times d_2}\\  
V\in\mathbb{R}^{d_2\times d_1}  
\end{align}
$$  
- $K$의 열벡터(column vectors)는 key vectors이며, 입력 시퀀스(input sequence)에 대한 패턴 탐지기(pattern detectors) 역할을 한다.
	- 행렬 연산때 열 백터와 유사도를 파악하게 됨.
- $V$의 행벡터(row vectors)는 value vectors이며, **출력 어휘(output vocabulary)에 대한 분포(distributions)를 표현**한다.
- 따라서 FFN은 다음과 같이 해석할 수 있다.  

$$  
\text{FFN}(x_i)=\sum_{j=1}^{d_2}\text{ReLU}(x_i\cdot k_j),v_j  
$$
- 여기서 $\text{ReLU}(x_i\cdot k_j)$는 value vector $v_j$에 대한 가중치(weights) 역할을 한다.
	- ReLU(Rectified Linear Unit)는 음수 입력을 $0$으로 만들고 양수 입력은 그대로 유지하는 활성화 함수이다.
- 논문:  [https://arxiv.org/pdf/2012.14913](https://arxiv.org/pdf/2012.14913)

- FFN은 밸류의 중요한 값을 가져오는 역할, 셀프 어텐션은 어떤 정보를 가져오면 되는지(Key 역할)를 파악하는 역할이라고 볼 수 있음.


### Memory Keys Correspond to Input Patterns
- 각각의 개별 key vector는 입력 접두사(input prefix)에 대한 특정 패턴(specific pattern)에 대응한다.

$K^6_{2546}$ 이면 6번째 레이어의 2546 row로 보면 됨.


### Memory Values Correspond to Output Tokens
- 각각의 value vector는 대략적으로 예측된 토큰 분포(predicted token distribution)에 대응한다.


### Memory Aggregation
- “활성(active)” 메모리, **즉 계수가 $0$이 아닌 메모리 벡터(memory vectors)는 일반적으로 희소(sparse)하다.**    
- 잔차 연결(residual connection)은 층(layer)을 거치면서 토큰 예측(token prediction)을 순차적으로 정교화(refine)한다.


- 레이어가 늘어나면서 희소해지고 예측은 정교화 됨.





### Hallucination
- 환각(hallucination): 언어모델(LM)이 그럴듯하거나 설득력 있게 들리더라도 사실적으로 부정확하거나 오해를 일으키거나 조작된 정보를 생성하는 현상    
- 환각은 왜 발생하는가?    
	- 제한된 지식(limited knowledge): LLM은 유한한 데이터셋으로 학습되므로 가능한 모든 정보에 접근할 수 없다. 학습 데이터 밖의 주제에 대해 질문을 받으면 그럴듯하지만 부정확한 응답을 생성할 수 있다.    
	- 과잉 일반화(overgeneralization): LLM은 한 문맥에서 학습한 패턴을 적용되지 않는 다른 문맥에 적용하여 잘못된 결론을 낼 수 있다.    
	- 상식 부족(lack of common sense): LLM은 인간과 유사한 텍스트를 처리하고 생성할 수 있지만, 종종 출력에 상식적 추론(commonsense reasoning)을 적용하는 능력이 부족하다.


### Hallucination Examples
#### (제한된 지식, limited knowledge)
- 질문:  

$$  
\text{“What were the main features of the iPhone 15 Pro Max?”}  
$$
- 2023년 이전에 학습된 LLM의 답변:  

$$  
\text{“The iPhone 15 Pro Max features a revolutionary holographic display, quantum computing chip, and telepathic user interface.”}  
$$
- 이는 존재하지 않는 기능들을 만들어낸 환각(hallucination)의 예이다.
#### (과잉 일반화, overgeneralization)
- 질문:  

$$  
\text{“How do you form the past tense in Japanese?”}  
$$
- LLM의 답변:  

$$  
\text{“In Japanese, you typically add '-ed' to the end of verbs to form the past tense, just like in English.”}  
$$
- 이는 영어의 규칙을 일본어에 잘못 일반화한 사례이며, 사실과 다르다.
#### (상식 부족, lack of common sense)
- 질문:  

$$  
\text{“How many tennis balls can fit in a typical smartphone?”}  
$$
- LLM의 답변:  

$$  
\text{“Approximately 15-20 tennis balls can fit in a typical smartphone, depending on the model and screen size.”}  
$$
- 이는 물리적 크기에 대한 상식적 추론이 부족하여 발생한 오류이다.


컷오프 데이터??????가 무엇인지 확인 필요

### Concerns About Hallucination
- 생성형 AI(Generative AI)는 변호사들의 업무 방식을 기록적인 속도로 변화시키고 있지만, 동시에 법원(courts)에 허위 인용(phantom citations)과 존재하지 않는 판례(invented case law)를 조용히 범람시키고 있다.    
- 최근 몇 달 동안 미국 전역의 여러 판사들은 ChatGPT와 같은 생성형 AI 도구가 만들어낸 허구의 판례(fictitious case law)를 제출한 변호사들에게 제재(sanctions)를 가했다.    
- 이러한 소위 “환각(hallucinations)”은 단순히 난처한 일이 아니라, 직업적 위법행위(professional misconduct)를 구성할 수 있으며, 의뢰인의 이익(interests)을 위태롭게 하고, 이미 회의적인 법률 환경에서 법조계의 신뢰성(credibility)을 손상시킬 수 있다.    
- 실제로 2023년 중반 이후 AI 기반 법률 환각(AI-driven legal “hallucinations”) 사례가 $120$건 이상 확인되었으며, 그중 최소 $58$건은 2025년에 발생했다.






### Non-parametric Knowledge
- non-parametric knowledge: 모델의 매개변수(parameters)에 저장되어 있지는 않지만, 필요할 때 접근하거나 검색(retrieve)할 수 있는 외부 정보
	- 학습에 사용되지 않은 정보를 사용 할 수 있음.
- 예:
	- 외부 지식베이스(knowledge bases) 또는 지식 그래프(knowledge graphs)
	- 사전학습 말뭉치(pretraining corpora)
	- 사용자가 제공한 문서 또는 구절(passages)
- non-parametric knowledge은 일반적으로 더 정확한 사실 기반 질의응답(factoid question answering)을 위해, **주로 검색(retrieval)을 통해 매개변수적 지식(parametric knowledge)을 보강하는 데 사용된다.**
- non-parametric knowledge의 장점:
	- 모델 크기를 늘리지 않고 더 많은 정보를 통합할 수 있다.
	- 지식베이스를 더 쉽게 업데이트하고 수정할 수 있다.
	- 모델 해석가능성(interpretability)을 향상시킨다.


### Overview: Retrieval-Augmented Generation
- 검색기(retriever)를 사용하여 외부 텍스트 컬렉션(external text collection)에서 질의(query)와 관련된 문서들을 가져온다.    
- 가져온 문서들과 프롬프트(prompt)가 주어졌을 때 LLM을 사용하여 답변을 생성한다.

- 질문을 바로 LLM에 넣으면 파라미터 지식
- 질문을 Rertriever을 통해서 답변하면 RAG 
	- 할루시네이션이 줄고 근거 제공이 가능함.

### Overview: Information Retrieval (IR)
- 정보검색(Information Retrieval, IR): 사용자 질의(query)에 응답하여 비정형 데이터(unstructured data)의 대규모 컬렉션, 예를 들어 문서나 웹페이지에서 관련 정보를 찾는 것    
- 질의(query): 사용자가 찾고자 하는 정보를 설명하는 입력, 예를 들어 키워드나 구문    
- 문서/말뭉치(documents/corpus): 시스템이 검색하는 데이터 컬렉션    
- 순위화(ranking): 키워드 매칭(keyword matching), 의미적 유사도(semantic similarity) 같은 특정 지표를 기반으로 검색 결과를 관련성 순서대로 정렬하는 것    
- 웹 검색 엔진, 예를 들어 Google이나 Bing은 IR 시스템이다.

- IR은 원래 컴퓨터 사이언스에서 중요했지만 지금 만큼 중요시 되지 않았음
	- 현재는 IR과 추천시스템이 매우 연구 활발발

### Sparse vs. Dense Retrieval
- 희소 검색(sparse retrieval): 문서와 질의의 표현이 희소한, 즉 **대부분의 벡터 값이 $0$인 전통적인 정보검색(IR)** 기법에 기반한 검색 방식
	- 예: TF-IDF
	- 장점(pros): 단순하고 해석 가능하다.
	- 단점(cons): 의미적 이해(semantic understanding)가 부족하다.
- 밀집 검색(dense retrieval): 심층 신경망(deep neural networks)을 사용하여 문서와 질의를 **밀집 벡터(dense vectors), 즉 임베딩(embeddings)으로 인코딩하는 방식**
	- 예: BERT 기반 인코딩 방법
	- 장점(pros): 의미적이고 문맥화된 이해(semantic & contextualized understanding)가 가능하다.
	- 단점(cons): 계산 비용이 더 크고 해석가능성이 낮다.

- Sparse vs. Dense vector와 동일한 연결성이 있음.




- TF-IDF는 3주차 강의에서 소개되었다.  
$$  
\text{TF-IDF}(w,d)=\text{TF}(w,d)\times \text{IDF}(w)  
$$

- 핵심 아이디어(main idea): 자주 등장하면서도 구별력 있는(distinctive) 단어들로 문서를 표현하는 것이다.
- TF-IDF 가중치(TF-IDF weighted)

|word|As You Like It|Twelfth Night|Julius Caesar|Henry V|
|---|---|---|---|---|
|battle|0.246|0|0.454|0.520|
|good|0|0|0|0|
|fool|0.030|0.033|0.0012|0.0019|
|wit|0.085|0.081|0.048|0.054|

$$  
\cos(v_{d_2},v_{d_3})=0.10  
$$

$$  
\cos(v_{d_3},v_{d_4})=0.99  
$$

- 원시 빈도(raw counts)

|word|As You Like It|Twelfth Night|Julius Caesar|Henry V|
|---|---|---|---|---|
|battle|1|0|7|13|
|good|114|80|62|89|
|fool|36|58|1|4|
|wit|20|15|2|3|

$$  
\cos(v_{d_2},v_{d_3})=0.81  
$$ 

$$  
\cos(v_{d_3},v_{d_4})=0.99  
$$

### Term Frequency (TF)
- 어떤 단어가 문서에 $100$번 등장한다고 해서 그 단어가 문서 의미와 $100$배 더 관련 있다는 뜻은 아니다.
- 따라서 원시 빈도(raw counts)를 그대로 사용하는 대신, 로그 스케일(log scale)을 사용하여 빈도를 압축(squash)한다.  

$$  
\text{TF}(w,d)=  
\begin{cases}  
1+\log_{10}\text{count}(w,d), & \text{count}(w,d)>0\\  
0, & \text{otherwise}  
\end{cases}  
$$


### Inverse Document Frequency (IDF)
- 우리는 판별력이 높은 단어(discriminative words), 즉 DF(document frequency)가 낮은 단어를 강조하고자 한다.
- 역문서빈도(Inverse Document Frequency, IDF)는 전체 문서 수 $N$을 DF로 나눈 뒤 로그 스케일을 적용한 값이다.  

$$  
\text{IDF}(w)=\log_{10}\left(\frac{N}{\text{DF}(w)}\right)  
$$
- 셰익스피어 말뭉치(Shakespeare corpus, 총 $37$개 문서)의 DF 및 IDF 통계

|Word|df|idf|
|---|---|---|
|Romeo|1|1.57|
|salad|2|1.27|
|Falstaff|4|0.967|
|forest|12|0.489|
|battle|21|0.246|
|wit|34|0.037|
|fool|36|0.012|
|good|37|0|
|sweet|37|0|


### TF-IDF for Sparse Retrieval
- 문서-질의 의미적 유사도(document-query semantic similarity)는 코사인 유사도(cosine similarity)로 점수화한다.  

$$  
\cos(q,d)=\frac{q\cdot d}{|q||d|}  
$$
- 문서 벡터와 질의 벡터 모두 TF-IDF 가중치(TF-IDF weighting)를 사용한다.
- 다른 가중치 방식, 예를 들어 BM25도 사용할 수 있다. (수업에서 다룬 내용은 아님 여기서 25는 버전 번호인데 25번이 많이 사용되고 있음.)


### Example: TF-IDF for Sparse Retrieval
- 예시 질의(example query)와 미니 말뭉치(mini-corpus):  

$$  
\text{Query: sweet love}  
$$
- Documents:
	- Doc 1: “Sweet sweet nurse! Love?”
	- Doc 2: “Sweet sorrow”
	- Doc 3: “How sweet is love?”
	- Doc 4: “Nurse!”
- 질의(query) 및 문서 벡터(document vectors)
- Query 벡터

|word|cnt|tf|df|idf|tf-idf|n’ized|
|---|---|---|---|---|---|---|
|sweet|1|1|3|0.125|0.125|0.383|
|nurse|0|0|2|0.301|0|0|
|love|1|1|2|0.301|0.301|0.924|
|how|0|0|1|0.602|0|0|
|sorrow|0|0|1|0.602|0|0|
|is|0|0|1|0.602|0|0|

- Document 1 벡터

|word|cnt|tf|tf-idf|n’ized|
|---|---|---|---|---|
|sweet|2|1.301|0.163|0.357|
|nurse|1|1.000|0.301|0.661|
|love|1|1.000|0.301|0.661|
|how|0|0|0|0|
|sorrow|0|0|0|0|
|is|0|0|0|0|

$$  
\cos(q,d_1)=0.747  
$$

- Document 2 벡터

|word|cnt|tf|tf-idf|n’ized|
|---|---|---|---|---|
|sweet|1|1.000|0.125|0.203|
|nurse|0|0|0|0|
|love|0|0|0|0|
|how|0|0|0|0|
|sorrow|1|1.000|0.602|0.979|
|is|0|0|0|0|

$$  
\cos(q,d_2)=0.078  
$$




### Dense Retrieval
- 동기(motivation): 희소 검색(sparse retrieval), 예를 들어 TF-IDF는 의미적 유사도(semantic similarity)를 고려하지 않고 질의(query)와 문서(document) 사이의 정확한 단어 겹침(exact overlap)에 의존한다.
- 해결책(solution): 언어모델(language model)을 사용하여 질의와 문서의 밀집 분산 표현(dense distributed representations)을 얻는다.
- **검색기 언어모델(retriever language model)은 일반적으로 BERT와 같은 작은 텍스트 인코더(text encoder) 모델**이다.
	- 검색(retrieval)은 자연어 이해(natural language understanding) 과제이다.
	- 인코더 전용 모델(encoder-only models)은 이 목적에서는 LLM보다 더 효율적이다.
- 질의 표현(query representation)과 문서 표현(document representation)은 모두 텍스트 인코더(text encoders)에 의해 계산된다.

- 검색에는 인코더 모델이 더 적합함.
- sparce 는 단어의 겹칩이 있어야 함.

### Dense Retrieval: Bi-encoder
- 질의(query)와 문서(document)를 두 개의 분리된(separate) 인코더 모델을 사용하여 독립적으로(independently) 인코딩한다.
- 다만 실제로는 두 인코더가 동일한(identical) 경우가 많다.
- 질의 벡터(query vector)와 문서 벡터(document vector) 사이의 코사인 유사도(cosine similarity)를 관련성 점수(relevance score)로 사용한다.  

$$  
\cos(q,d)=\frac{q\cdot d}{|q||d|}  
$$

- 장점:
	- 문서 벡터(document vectors)를 미리 사전계산(precomputed)할 수 있다.
- 단점:
	- 질의-문서 상호작용(query-document interactions)을 포착할 수 없다.
	- **질문에 따라 다르게 인코딩 되어야 할 수도 있는데 사전에 학습 되다보니 쿼리의 반영이 낮음**
- 대규모 검색(large-scale retrieval)에서 일반적으로 사용되는 선택 방식이다.


- 바이 인코더는 버트 같은 모델을 연상하면 됨.
- 쿼리나 다큐먼트를 1개의 벡터로 출력할 수 있고 이 둘을 연산할 수 있고 그 연산 결과 중 상위 결과를 제공하는게 바이 인코더
- 다큐먼트는 미리 학습되어 준비 되어 있음 → 인덱스라고 함. 그 다음에 질문만 받아서 연산하면 됨 → 매우 효율적임.
- 대규모의 라지 코퍼스에 일반적으로 사용 됨.

### Dense Retrieval: Cross-encoder
- 질의-문서 쌍(query-document pairs)을 함께 처리한다.
- 관련성 점수(relevance score)는 모델 출력(model output)에 의해 직접 생성된다.
- 장점:
	- 질의(query)와 문서(document) 사이의 복잡한 상호작용(intricate interactions)을 포착할 수 있다.
- 단점:
	- 대규모 검색 말뭉치(large retrieval corpus)에 확장하기 어렵다.
- 작은 문서 집합(small document sets)에 적합하다.

- 바이 인코더의 단점을 보완하기 위해 학습시 **쿼리와 다큐먼트의 쌍을 한번에 학습함**.
- 그러면 쿼리에 이해를 위한 정보를 같이 학습하기 때문에 쿼리와 다큐의 상호과정이 있어 더 좋은 답변을 줌
- 다만 쿼리가 들어오면 다큐먼트에 다 연산해봐야 하는 단점이 있음 → 작은 다큐먼트 세트에 적합함.
- 셀프 어텐션에 의해 쿼리와 관련 있는 다큐먼트의 내용을 잘 찾아 냄.







### Evaluation of IR Systems
- 정보검색(IR) 시스템이 반환하는 각 문서는 우리의 목적에 대해 관련 있음(relevant) 또는 관련 없음(not relevant) 중 하나라고 가정한다.
- 질의(query)가 주어졌을 때, 시스템은 순위가 매겨진 문서 집합(rankded documents) $T$ 를 반환한다고 가정한다.
	- 이 중 부분집합  $R$은 관련 문서이며, 나머지 $N=T-R$은 관련 없는 문서이다.
	- 전체 검색 컬렉션(retrieval collection)에는 이 질의와 관련된 문서가 총  $U$ 개 존재한다고 가정한다.
- 정밀도(Precision): 반환된 문서 중 관련 문서의 비율  

$$  
\text{Precision}=\frac{|R|}{|T|}  
$$
- 재현율(Recall): 전체 관련 문서 중 반환된 문서의 비율  

$$  
\text{Recall}=\frac{|R|}{|U|}  
$$

- 메인 토픽은 아님.
- 리턴 된 다큐먼트는 관련 있음과 없음 0,1 로 나눌수 있다고 가정.
- U: 쿼리와 관련있는 다큐먼트
- T: 쿼리에 대한 답으로 리턴된 값중 순위가 매겨진 문서의 집합.
- R: 관련있는 답변
- N: 관련 없는 답변변


### Precision & Recall @ 𝑘
- 우리는 관련 문서(relevant documents)를 더 높은 순위에 배치하는 검색 시스템(retrieval system)을 구축하고자 한다.    
- 이를 평가하기 위해 순위 목록(ranked list)의 상위 $k$개 항목에 대한 정밀도와 재현율, 즉 precision@k와 recall@k를 사용한다.    
- 아래 예시에서는 검색 말뭉치(retrieval corpus)에 관련 문서가 총 $9$개 있다고 가정한다.
    

| Rank | Judgment | Precision@Rank | Recall@Rank |
| ---- | -------- | -------------- | ----------- |
| 1    | R        | 1.00           | 0.11        |
| 2    | N        | 0.50           | 0.11        |
| 3    | R        | 0.66           | 0.22        |
| 4    | N        | 0.50           | 0.22        |
| 5    | R        | 0.60           | 0.33        |
| 6    | R        | 0.66           | 0.44        |
| 7    | N        | 0.57           | 0.44        |
| 8    | R        | 0.63           | 0.55        |
| 9    | N        | 0.55           | 0.55        |
| 10   | N        | 0.50           | 0.55        |


### Average Precision
- 평균 정밀도(Average Precision, AP): 관련 문서(relevant document)가 검색된 순위 지점들에서의 정밀도(precision) 값들의 평균  

$$  
\text{AP}=\frac{1}{|R|}\sum_{k=1}^{|T|}\left(\text{Precision@k}\times \mathbf{1}_{(d_k\ \text{is relevant})}\right)  
$$

- 여기서  $\mathbf{1}_{(d_k\ \text{is relevant})}$는 문서 $d_k$가 관련 문서인지 여부를 나타내는 지시 함수(indicator function)이다.
- 위 표에서 관련 문서(R)가 등장하는 순위는 $1,3,5,6,8$이다.
- 따라서 사용되는 precision 값들은 다음과 같다.  

$$  
1.0,\ 0.66,\ 0.60,\ 0.66,\ 0.63  
$$
- 이를 평균내어 AP를 계산한다.

- Precision을 평균낸 것이 평균정밀도 AP
- 관련 있는 문서 R의 precision을 구해서 더한뒤 평균을 냄.
- 평균 값이라 상대적으로 안정적 (튀는 값이 덜함.)




### RAG for LLMs
- RAG(Retrieval-Augmented Generation)는 LLM 생성의 사실성(factuality)을 높이고 환각(hallucination)을 완화하기 위한 일반적인 기법이다.

- 최신 아이폰? → LLM이 구글이나 위키에서 서치 후 프롬프트로 넣어 답변하게 됨


### RAG vs. Direct Prompting
- 프롬프팅(prompting)은 언어모델(LM)의 매개변수적 지식(parametric knowledge)에 의존하여 질문에 직접 답한다.  

$$  
P(w\mid Q:\text{“Who wrote the book ‘The Origin of Species’?”},A:)  
$$

- 반면 RAG(Retrieval-Augmented Generation)는 검색된 구절들(retrieved passages)을 질문 앞에 추가(prepend)한다.
- 즉, 검색기(retriever)가 관련 문서나 구절을 먼저 가져오고, LLM은 이를 참고하여 답변을 생성한다.
- RAG 프롬프트의 개략적 구조(schematic)는 다음과 같다.  

$$  
\text{retrieved passage 1}  
$$  

$$  
\text{retrieved passage 2}  
$$  

$$  
\cdots  
$$  

$$  
\text{retrieved passage n}  
$$

- 이후 다음과 같은 형태로 질문을 수행한다.  

$$  
\text{“Based on these texts, answer this question: Q: Who wrote the book ‘The Origin of Species’? A:”}  
$$
- 즉, RAG는 외부 지식(external knowledge)을 활용하여 더 정확하고 사실적인 답변을 생성하도록 돕는다.


- RAG는 일종의 프롬프팅의 한 종류라고 보면 됨.
- RAG는 non parametric knowledge, parametric knowledge 모두 사용할 수 있게 해서 답변.

### RAG in Pretraining
- Retrieval-Augmented Language Model pretraining(REALM)
- RAG를 인코더 사전학습(encoder pretraining), 즉 BERT 방식에 통합하는 것을 연구한 첫 번째 논문이다.
- 핵심 모델은 “지식 보강 인코더(knowledge-augmented encoder)”이다.
- 검색된 내용(retrieved content)에 조건화된 masked language modeling(MLM) 손실로 사전학습한다.

- bert 처럼 프리 트레이닝 하는 중에 검색을 추가해서 보강한다는 측면의 연구
- 원래 사전 트레이닝 값뿐만아니라 z라는 검색 코퍼스를 활용해서 답변되도록 설계
- 검색된 내용이 concat되니 원래 인풋보다 풍성한 내용의 인풋이 생성됨(인풋 = 쿼리 + 다큐먼트)

### RAG for Text Generation
- 텍스트 생성(text generation)을 위한 RAG(Retrieval-Augmented Generation)를 연구한 최초의 논문이다.
- 검색기(retriever)와 생성기(generator)를 모두 함께 학습한다.
- 검색기는 인코더 전용 언어모델(encoder-only LM)이고, 생성기는 LLM이다.
- 논문 제목:  

$$  
\text{Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks}  
$$
- 논문:  
[https://arxiv.org/pdf/2005.11401](https://arxiv.org/pdf/2005.11401)


### A Latent Variable Model
- 검색된 문서(retrieved documents)는 생성(generation)을 위한 잠재변수(latent variables)  $z$  로 취급된다.  

$$  
p(y\mid x)=\sum_{z\in\mathcal{D}}p(z\mid x)\,p(y\mid x,z)  
$$

- $p(z\mid x)$ 는 질의(query)  $x$를 기반으로 문서 $z$를 검색(retrieve)할 확률이다.
- $p(y\mid x,z)$는 질의  $x$와 검색된 문서  $z$를 바탕으로 답변  $y$를 생성(generate)할 확률이다.
- 즉, RAG는 검색된 문서들을 잠재 지식(latent knowledge)처럼 활용하여 답변 생성 확률을 모델링한다.


- x: 쿼리
- y: 쿼리에 대한 답
- $p(y\mid x)$는 z를 활용해서 분해(decompose)
- z는 모든 다큐먼트를 다 사용 할 수 없음 → MIPS 기법을 이용해서 문서 선택
	- 내적값이 큰것들을 사용
	- **MIPS는 내용 꼭 알아 둘 것.**

### RAG-Sequence Model
- 동일한 검색 문서(retrieved document)를 사용하여 전체 시퀀스(sequence)를 생성한다.
- 검색된 문서를 하나의 잠재변수(latent variable)로 취급한다.
- 생성 확률  $p(y\mid x)$를 계산하기 위해 top-$K$ 근사(top-$K$ approximation)를 사용하여 주변화(marginalize)한다.  

$$
\begin{align}
p_{\text{RAG-sequence}}(y\mid x)  
&\approx  
\sum_{z\in\text{top-}K(p(\cdot\mid x))}  
p_\eta(z\mid x),p_\theta(y\mid x,z) \\  
&=\sum_{z\in\text{top-}K(p(\cdot\mid x))}  
p_\eta(z\mid x)\prod_{i=1}^{N}p_\theta(y_i\mid x,z,y_{<i})  
\end{align}
$$

- **top-$K$ 근사는 상위 $K$개의 검색 문서만 고려**한다는 뜻이다.
- 동일한 검색 문서  $z$  를 사용하여 시퀀스의 모든 토큰을 생성한다.
- $p_\eta(z\mid x)$ 는 검색기(retriever)의 확률 모델이고,  $p_\theta(y_i\mid x,z,y_{<i})$ 는 생성기(generator)가 이전 토큰들과 검색 문서를 바탕으로 다음 토큰을 생성할 확률이다.

- y:는 답변인데 여러개의 토큰으로 구성되어 있음.
	- z를 전체 시퀀스생성에 사용할지 문장에 사용할지 정하게 됨.
	- 시퀀스 모델은 z를 전체 시퀀스에 사용함.
- $(y_i\mid x,z,y_{<i})$ 는 x쿼리,z문서y_i →i번째 이전의 y 값이 새로운 y_i에 미치는 영향을 확률로 구함. 이때 $p_\eta(z\mid x)$가 확률 앞에 곱해짐 → z가 전체 확률에 동일한 영향을 미침 


### RAG-Token Model
- 시퀀스(sequence) 안의 서로 다른 토큰을 생성하기 위해 서로 다른 검색 문서(retrieved documents)를 사용할 수 있다.
- 주변화(marginalization)는 시퀀스 수준(sequence level)이 아니라 각 생성 토큰(generated token)마다 수행된다.  

$$
\begin{align}
p_{\text{RAG-token}}(y\mid x)&=\prod_{i=1}^{N}p_\theta(y_i\mid x,y_{<i})  \\  
&\approx \prod_{i=1}^{N}\sum_{z\in\text{top-}K(p(\cdot\mid x,y_{<i}))}p_\eta(z\mid x,y_{<i})\,p_\theta(y_i\mid x,z,y_{<i}) 
\end{align}
$$

- 즉, 서로 다른 검색 문서  $z$ 가 시퀀스의 서로 다른 토큰을 생성하는 데 사용될 수 있다.


- 토큰을 생성할 때마다 z가 시퀀스의 다른 토큰에 사용 될 수 있음
- z의 중요도를 다 다르게 생성하게 됨.
- 시퀀스는 효율적이고 토큰은 세밀한 모델이라고 생각 할 수 있음.
	- 시퀀스는 리트리벌을 1번 함.
	- 토큰은 생성하는 중에 계속 리트리벌을 반복해서 토큰별로 중요도가 다르다는 값을 반영 할 수 있음.
	- 서비스 레벨에서 토큰마다 리트리벌을 하는 것은 불가능하고 이론적 모델임.
	- 답변이 일정 수준 이하의 확률값이 나올경우 품질이 떨어지니 다시 리트리벌하는 정도의 설계를 주로 사용 함.



### RAG-Sequence & RAG-Token Results
- 개방형 질의응답(open-domain QA) 과제에서의 평가 결과(evaluation results)
- 사용된 데이터셋:
	- Natural Questions (NQ)
	- TriviaQA (TQA)
	- WebQuestions (WQ)
	- CuratedTrec (CT)

|Model|NQ|TQA|WQ|CT|
|---|---|---|---|---|
|Closed Book: T5-11B|34.5|- / 50.1|37.4|-|
|Closed Book: T5-11B+SSM|36.6|- / 60.5|44.7|-|
|Open Book: REALM|40.4|- / -|40.7|46.8|
|Open Book: DPR|41.5|57.9 / -|41.1|50.6|
|RAG-Token|44.1|55.2 / 66.1|45.5|50.0|
|RAG-Sequence|44.5|56.8 / 68.0|45.2|52.2|

- 결과를 보면 RAG 기반 모델(RAG-Token, RAG-Sequence)이 대부분의 개방형 QA 과제에서 더 높은 성능을 보인다.
- 특히 RAG-Sequence는 NQ와 CT에서 가장 높은 성능을 기록했다.
- 이는 검색(retrieval)을 통한 외부 지식 활용이 사실 기반 질의응답(factoid QA)의 정확도를 향상시킴을 보여준다.



### Q&A
- RAG는 벡터 DB가 사전에 없이 웹 정보를 이용할 수 있나요?
	- 리트리벌은 closed, open corpus 모두 가능합니다.
	- 클로즈 코퍼스는 미리 벡터 DB를 생성함.

