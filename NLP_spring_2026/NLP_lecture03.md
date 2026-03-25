2026-03-23 08:20
## 3강 Semantics

### Recap
- 지난주는 랭귀지 모델의 기본
- 이번주는 semantics 수업
- 자연어에서 가장 중요한것은 LM
- LM은 NLP의 기본이 됨됨
- 시퀀스를 관측할 확률을 계산하는게 LM
- Autoregressive assumption 
- 분포를 얻고 나면 샘플링이나 max 값으로 생성
- n-gram은 과거 단어를 n개만 이용하여 연산
- sparsity 문제 발생 및 특징 알아야 함.
- add-one 또는 laplace smoothing
	- 1을 다 더해서 0을 삭제
- Interpolation을 이용해서 smoothing 가능능
- 좋은 랭귀지 모델은 덜놀래고, 새로운 문장 뒤 단어를 잘 assign 또는 예측해야 함.
- Perplexity 모델 평가 방법
- 내제적, 외재적 평가 방법 2개를 사용해서 언어 모델을 평가 함.

### Introduction to Word Senses & Semantics
- 딥러닝까지 안갔기 때문에 전통적 모델 수업이 진행될 것.
- 더 좋은 언어 모델을 만들기 위해서는 단어의 의미를 이해하는것이 중요.
- The 다음에 어떤 단어가 나올지 예측 cat은 2번 mat은 한번 나오기 때문에 확률이 다름.
- 관측되지 않은 조합은 확률이 0이 되는 sparsity 문제가 나옴.
- 다만, dog와 cat이 유사함을 알면 코퍼스에 존재 하지 않아도 충분히 예측이 가능해짐.
- Semantics 은 매우 다양한 종류가 있음
	- Synonyms: 유사어
	- Antonyms: 반의어
	- Hyponyms & hypernyms: 상위 하위 개념
	- Polysemy: 다의어
- 언어학의 전통적인 분야임.
	- 우리는 컨셉만 훑어보게 될 것.
- Lemma: 표제형
	- 딥러닝으로 가도 사용
	- 어떤 단어의 원형이 되는 단어를 lemma라고 함.
	- run: runs, ran의 원형
- Lemmatization: 표제형으로 환원
	- lemma로 만드는 과정
	- ran을 run으로
	- 요즘은 바로 표제형으로 만들기 보다 토큰을 만드는 과정에서 자연스럽게 사용

### Synonyms
- 유의어
- 다른 단어로 대체 될 수 있으면 가능
- 다만 완벽한 유의어는 존재 하지 않음
	- 비슷할 뿐 완벽히 같지 않음.
	- large sister는 부정적
	- child가 kid 보다 더 어린 느낌.

### Antonyms
- 반의어
- Gradable antonyms: 스펙의 양끝단을 나타내는 단어
- Complementary antonyms: 상호 배타, 하나가 존재 하면 다른것은 존재 불가.
- Relational antonyms: 관계에서 생성되는 반의어

### Hyponyms & Hypernyms
- 계층적 단어 관계
- vehicle의 Hyponym는 자동차 배 비행기
- Hypernym/hyponym relationship is usually transitive

### Polysemy & Senses
- Polysemy: 다의어
- Sense: 의미는 문맥에 따라 달라짐.
	- 의미를 이해하려면 단어간 관계를 이해 해야 함.
- Word sense disambiguation (WSD): 이런 문제를 정의 하고 풀이 함.
	- 특정 단어가 문장에서 어떤 의미로 사용되었는지 찾는 문제
	- context가 짧거나 제한 적이면 풀이가 어려움.

### Word Sense Disambiguation
- LM이 멀티모달을 다루지만 WSD는 여전히 어려운 문제임.
- 위 사진은 나노바나나를 이용해서 프롬프트를 이미지 생성 예시
	- bat는 박쥐나 방망이 둘다 되고
	- cave는 동굴이나 아지트 둘다 됨.
- 아직 어려운 문제 중 하나임.

### Word Similarity
- 단어간 유사도 
- 완벽한 유의어는 없지만 유사한 단어는 매우 쉽게 찾을 수 있음.
- 개와 고양이는 문맥에서 유사하게 많이 사용 됨.
- 0~10까지 매뉴얼로 계산 함.
	- 유사하면 10
	- 다른 단어면 0에 가까움.
- 곧 ML을 이용해서 자동으로 단어의 유사도 계산 실습 예정

### Word Relatedness & Semantic Field
- 단어의 유사도는 다양하게 관계를 통해 형성 될 수 있음
- Functional 기능적 관계: 의사는 병원에서 일함. 
- Thematic: 방과 버터
- Conceptual : 선생님 학생
#### Semantic field: 
- 단어의 집합이 특정 필드를 커버 할때를 뜻함.
	- houses: door, roof, kitchen, family, bed

### Connotation
- Connotation: 내포
	- 문자 그대로 뜻이 아닌 내포하고 있는 의미나 관계
	- 문화나 주관이 들어가는 영역
	- 이코노미, cheap은  유의어지만 각각 긍정적 부정적 의미 내포
- Valence (정서적 가치 / 쾌·불쾌 정도):  
	- 긍정적 정도
	- 자극이 얼마나 기분 좋거나 불쾌한지를 나타냄
	- 높음: “행복한 (happy)”, “만족한 (satisfied)”
	- 낮음: “불행한 (unhappy)”, “짜증 난 (annoyed)”
- Arousal (각성도 / 흥분 정도):  자극이 얼마나 감정을 강하게 유발하는지 (강도)
	- 감정의 자극을 나타내는 척도
	- 높음: “흥분한 (excited)”
	- 낮음: “차분한 (calm)”
- Dominance (지배성 / 통제감): 자극이 개인에게 얼마나 통제력을 행사하거나 영향을 주는지
	- 내포하는 의미가 얼마나 상황 억제력이 강한지
	- 높음: “지배적인 / 통제하는 (controlling)”
	- 낮음: “영향받는 (influenced)”

### Classic Word Representations
- 전통적인 단어 나타내는 방법

### WordNet
- 단어의 semantics는 복잡함.
- NLP 초기에는 워드넷이라는 자료 구조에 의존해서 semantics를 사용
- 언어학자들이 직접 데이터 베이스를 만듦
- lemmas, senses들이 다 정리되어 있음
- 굉장히 디테일한 정보들이 담겨 있음.
- 세상에 존재하는 모든 단어의 표제형, 관계, 의미등을 정리하려는 시도 였음.
- 데이터 살펴보면 엄청 디테일하게 정리 되어 있음
- 세상의 모든 단어간의 관계를 표현하고 자 함.
- 초기 LM에서는 월드넷이 모든 연구의 기반

#### WordNet for Word Sense Disambiguation
- 어떤 단어가 있을때 어떤 뜻으로 사용되는지 풀때 초기에는 워드넷을 이용
- bass라고 하면 어떤 뜻으로 사용되었는지 찾기 위해 워드넷 데이터 베이스에서 관계가 가장 많은 순서대로 예측을 실시
	- 그 당시에는 가장 강력한 기준이 됨
	- 하지만 너무 통계적이고 맥락의 이해는 어려 웠음
	- -> 딥러닝을 이용하는 연구로 발전 됨.

#### WordNet Limitations
- 언어학자들의 노력의 산물
- 만들기, 유지, 업데이트가 너무 어려움
- 신규어들 추가 어려움
- 단어들이 특정 도메인에서만 특별히 사용되는 경우도 있음
- 소수민족의 언어들 표현 어려움,
- 단어 레벨로 다루다 보니 표현이나 구 수준 까지 활용 어려움.

### Vector Space Model Basics 

#### Motivation: Representing Texts with Vectors
- 단어를 이해 하기 위해서는 다른 단어와 어떤 관계를 갖고 얼마나 유사한지등의 지표가 필요함
- multi-dimensional vectors(다차원 벡터)를 이용해서 단어의 의미를 다차원적으로 파악할 수 있음.
	- 각각의 벡터 디멘전이 그 역할을 해줌.

#### Vector Semantics
- 단어를 multi-dimensional semantic spac멀티 디멘전널 스페이스에 나타내는 것이 목표
	- 단어가 유사하면 비슷한 위치(가까운 위치)
	- 이런 관계들이 벡터 스페이스에서 보존되길 원함.

#### Vector Space Basics
-  N-dimensional vector을 이용
	- 각각의 원소들이 구성됨.
- 벡터의 내적
- 크기
- 코사인 유사도
- 등을 사용해서 구함.
- Vector notation: an N-dimensional vector $\mathbf{v} = [v_1, v_2, \ldots, v_N] \in \mathbb{R}^N$
- Vector dot product / inner product: 내적  

$$
\text{dot product}(\mathbf{v}, \mathbf{w}) = \mathbf{v} \cdot \mathbf{w} = v_1 w_1 + v_2 w_2 + \cdots + v_N w_N = \sum_{i=1}^{N} v_i w_i  
$$
  - Vector length / norm:  

$$
|\mathbf{v}| = \sqrt{\mathbf{v} \cdot \mathbf{v}} = \sqrt{\sum_{i=1}^{N} v_i^2}  
$$
- Cosine similarity between vectors:  

$$
\cos(\mathbf{v}, \mathbf{w}) = \frac{\mathbf{v} \cdot \mathbf{w}}{|\mathbf{v}| , |\mathbf{w}|}  
= \frac{\sum_{i=1}^{N} v_i w_i}{\sqrt{\sum_{i=1}^{N} v_i^2} \sqrt{\sum_{i=1}^{N} w_i^2}}  
$$


#### Vector Space Basics: Example
- Consider two 4-dimensional vectors  $\mathbf{v} = [1, 0, 1, 0] \in \mathbb{R}^4 \quad  \mathbf{w} = [0, 1, 1, 0] \in \mathbb{R}^4$
- Vector dot product / inner product:  

$$  
\mathbf{v} \cdot \mathbf{w} = \sum_{i=1}^{N} v_i w_i = 1  
$$
- Vector length / norm:  

$$  
|\mathbf{v}| = \sqrt{\sum_{i=1}^{N} v_i^2} = \sqrt{2}  
\quad  
|\mathbf{w}| = \sqrt{\sum_{i=1}^{N} w_i^2} = \sqrt{2}  
$$
- Cosine similarity between vectors:  

$$  
\cos(\mathbf{v}, \mathbf{w}) = \frac{\mathbf{v} \cdot \mathbf{w}}{|\mathbf{v}| |\mathbf{w}|} = \frac{1}{2}  
$$

#### Vector Similarity
- Cosine similarity
	- 대칭적이다: (cos(v, w) = cos(w, v))
	- 벡터 길이의 영향을 안받는게 큰 장점
	- 단위 벡터를 만들고 각을 이용하여 계산.
	- 직관적인 기하학적 해석이 가능
	- 단어를 벡터로 만들면 많은 연산이 가능해짐
		- 그럼 어떻게 단어를 벡터로 만들까?

#### How to Represent Words as Vectors?
- One-hot vector
	- 가장 기본 방법
	- 인덱스를 이용하면 됨.
		- 1의 위치가 단어의 고유성을 나타내는 벡터가 됨.
	
#### Represent Sequences by Word Occurrences
- One-hot vector로 단어를 벡터로 만들고 나면 문장도 벡터로 표현 가능
- 인덱스 정보를 활용하면 documents도 벡터로 만들 수 있음
- 그다음 documents도 코사인 유사도로 계산 가능
- 한계는 단어가 있냐 없나 수준만 파악가능

#### Term-Document Matrix
- 빈도 수도 반영할 수 있도록 matrix 만듦
- 각각 다큐먼트에 이 단어가 몇번 나왔는지 표로 만들고 벡터화 함.
- As You Like It =\[1,114,36,20]
- 더 큰 텍스트 집합에서는 문서 내 단어 빈도가 풍부한 정보를 담고 있다
- → 셰익스피어의 네 개 희곡을 예로 들어 단어 빈도 통계를 구함
- $\mathbf{v}_{d_1} = [1, 114, 36, 20] \quad  \mathbf{v}_{d_2} = [0, 80, 58, 15] \quad  \mathbf{v}_{d_3} = [7, 62, 1, 2] \quad  \mathbf{v}_{d_4} = [13, 89, 4, 3]$

| As You Like It | Twelfth Night | Julius Caesar | Henry V |     |
| -------------- | ------------- | ------------- | ------- | --- |
| **battle**     | 1             | 0             | 7       | 13  |
| **good**       | 114           | 80            | 62      | 89  |
| **fool**       | 36            | 58            | 1       | 4   |
| **wit**        | 20            | 15            | 2       | 3   |

#### Document Similarity
- fool, wit 같은 단어가 많이 나오는 다큐먼트는 실제로 희극
- 간단하지만 합리적인 유사도 판정 방법임.
- 다큐먼트를 각 coulmn에 두고 coulmn을 기준으로 벡터화
- 코사인 유사도 정의: $\cos(\mathbf{v}, \mathbf{w}) = \frac{\mathbf{v} \cdot \mathbf{w}}{|\mathbf{v}|,|\mathbf{w}|}$
- $d_1$ vs $d_2$: 
$\mathbf{v}_{d_1} = (1,114,36,20), \mathbf{v}_{d_2} = (0,80,58,15)$
- 내적  

$$
\mathbf{v}_{d_1} \cdot \mathbf{v}_{d_2}  
= 1\cdot0 + 114\cdot80 + 36\cdot58 + 20\cdot15  
= 0 + 9120 + 2088 + 300 = 11508  
$$
- 노름  

$$
|\mathbf{v}_{d_1}| = \sqrt{1^2+114^2+36^2+20^2} = \sqrt{14693}  
$$ 

$$  
|\mathbf{v}_{d_2}| = \sqrt{0^2+80^2+58^2+15^2} = \sqrt{9989}  
$$
- 코사인 유사도  

$$  
\cos(d_1,d_2) = \frac{11508}{\sqrt{14693}\sqrt{9989}} \approx \mathbf{0.949} $$

#### Words Represented with Documents
- 행벡터를 보면 다큐먼트 관점에서 정보를 파악 할 수 있음
- “Fool”: “the kind of word that occurs in comedies”
- “Battle”:은 전쟁 관련된 책이나 역사 책에 많이 나옴.
- 즉 단어도 벡터화 할 수 있음
- -> 단어와 다큐먼트 모두 벡터화.

#### Words Represented with Documents
- 오른쪽이 원핫벡터
- 왼쪽이 단어-문서간 빈도를 활용하여 벡터화.
- 이런 방법도 한계가 있음
	- 다큐먼트 즉 긴 책하나를 같은 맥락으로봄.
	- 한 다큐먼트 안에서도 같은 단어가 다른 뜻으로 사용되는 경우도 많음.
	- 더 세밀한 콘텍스트가 필요함.

#### Fine-Grained Contexts: Word-Word Matrix
- 기존에는 단어가 문서에 들어있는지를 이용해서 context로 봤음
- 이제는 앞뒤 단어 몇개를 이용해서 context로 하자
	- 훨씬 세밀하게 context로 만듦
	- 맥락을 확 좁힘.
- 이러면 Word-Word Matrix을 만들 수 있음.
	- 체리의 앞 4단어 뒤 4단어를 이용해서 계산
- 중심 단어(center word)를 기준으로 특정 단어들이 몇번 나왔는지 표로 만들 수 있음.
- 디지털, 정보는 컴퓨터, 데이터등 비슷한 문맥에서 자주 등장
- 체리 딸기는 파이나 슈가와 함께 자주 등장
- 여전히 Sparsity이슈가 있음

#### Is Raw Frequency A Good Representation?
- 빈도를 세는것이 좋은 방법인가?에 대한 의문으로 시작
- 어떤 맥락에서 자주 등장하면 의미가 있어서 나오기도 하지만, 관습적으로 많이 나오는 단어들이 있음.
- 굿 같은 단어는 어느 책이나 자주 나옴.
- distinctively high frequency 구분되게 자주 나오는 단어들은 가중치를 주고 의미 없이 자주나오는 단어들은 패널티를 줘야 함. ->rerate하는 방법이 많이 나옴.

#### Term Frequency (TF)
- rerate를 위한 방법
- log 함수를 이용하는 방법을 TF라고 함.
- 100번 더 나온 단어가 100배 중요하진 않음
- 어느정도 많이 나온 단어는 그 차이가 줄어듦
- → 단순 등장 횟수(raw count)를 쓰지 않고,  로그 스케일로 값을 압축(squash) 한다
- log를 이용하면 특정 구간을 넘어설때 마다 증가폭이 줄어드는 특성이 있어 계산이 가능 함.  

$$
\mathrm{TF}(w, d) =  
\begin{cases}  
1 + \log_{10} \text{count}(w, d), & \text{count}(w, d) > 0 \  
0, & \text{otherwise}  
\end{cases}  
$$

#### Document Frequency (DF)
- 모든 다큐먼트에 많이 나오는 단어는 유니크하게 그 단어를 들어내진 않음
- good, the 이런 단어들은 정보값이 없음
- 각각의 단어에 의해 저장되는 정보값이 DF
	- 다큐먼트에 몇번 나왔는지 세서 저장하면 됨.
- 둘다 빈도가 같은데 로미오는 1개의 다큐먼트에서, 액션은 31개의 다큐먼트에서 나왔다면 로미오가 더 특별한 단어일 확률이 높음
- 문서 빈도 (DF):  
	- 특정 단어가 몇 개의 문서에 등장하는지를 세는 값
	- 단어 w가 문서 $d_i$에 등장하면 1, 아니면 0으로 계산  

$$
DF(w) = \sum_{i=1}^{N} \mathbf{1}(w \in d_i)  
$$
- 주의:  
    DF는 전체 문서에서의 총 등장 횟수(컬렉션 빈도)가 아님
	- Rome
        - 컬렉션 빈도: 113
        - 문서 빈도: 1
	- action
        - 컬렉션 빈도: 113
        - 문서 빈도: 31

#### Inverse Document Frequency (IDF)
- DF가 낮으면 소수에 다큐먼트에 나오고 중요도가 높다는 뜻 그래서 분모로 들어가고 log를 씌움.
- 목적:  
    - 문서 구별력이 높은 단어(DF가 낮은 단어)를 강조하기 위함
- 역문서 빈도 (IDF):  
    - 전체 문서 수 (N)을 문서 빈도 (DF)로 나눈 뒤, 로그를 취한 값  

$$
\mathrm{IDF}(w) = \log_{10}\left( \frac{N}{DF(w)} \right)  
$$
- 여러 문서에 자주 등장하는 단어 → IDF 낮음 (중요도 낮음) 
- 소수 문서에만 등장하는 단어 → IDF 높음 (중요도 높음)

#### TF-IDF Weighting
- 요즘도 많이 사용되는 중요도를 나타내는 기법
- $\text{TF-IDF}(w,d)=\text{TF}(w,d) \cdot\text{IDF}(w)$
- TF는 이 단어가 이 다큐먼트에 몇번 나왔는지 로그를 씌워 계산
	- 다큐에 많이 나올 수록 중요
	- 단, 너무 많이나온다고 너무 큰 가중치를 안받게 로그 사용
	- $log(\text{context}(w,d))$
- IDF는 모든 다큐먼트에 다 나오면 패널티, 일부에만 나오면 가중치
	- DF를 분모로 보내고 로그를 씌움.
	- $\displaystyle log \frac{N}{df(w)}$
- 모든 다큐먼트에 나오면 중요도가 낮아지도록 계산
- good 같이 어디서나 많이 나오는 단어는 TF-IDF에서 0이 됨.
	- 스무딩을 쓸수있지만 0으로 사용되기도 함.

#### Q&A
- 벡터의 크기가 조절가능한가요?
	- 지금 소개한 빈도수 기반 벡터들은 크기가 정해져있음.
	- 딥러닝 기반 방법은 벡터를 조절할 수 있음.
		- 벡터가 크면 좋은가요?
			- 벡터별로 크기가 다르다면 가장좋겠지만 유사도등을 비교하려면 디멘젼을 맞춰야 하기때문에 어느정도 맞추게 됨.
- 단어가 유사할때, 단어가 많이 나왔다면 그 유사도가 올라가는데
	- 여러뜻이 있는 경우 정확히 파악 할 수 없음
	- 다다음 수업정도에 트랜스포머 등 딥러닝 기법에서 배우게 됨.
- 현대 LLM은 파라메터를 다 하는게아니고 특정상황을 판별하고 거기에 맞는 에이전트를 호출해서 답하는 방법을 쓰고 있어서 무조건 TF-IDF로 평가한다라고 말하긴 어려움.
	- 사용하긴 함.

#### How to Define Documents?
- 다큐먼트는 무엇인가?(어떻게 정의?)
	- 어플마다 굉장히 다르게 설정
	- 책한권을 다큐로, 한장 또는 챕터를
	- 세분하면 문장이나 문단을 다큐먼트로 설정

#### Probability-Based Weighting
- 2번째로 많이 사용하는 weight 방법
- 확률기반으로 가중치
- TF-IDF weighting은 인간의 판단이 어느정도 들어간 가중치
- 이를 보완하기 위해 우연의 일치로 얼마나 자주 나오는지 계산

#### Word Association Based on Probability
- 두사건이 독립이면 각각의 확률의 곱으로 계산 할수 있음
- 두단어를 동시에 관측할 확률을 계산 했을때 두 단어를 각각 발견할 확률을 곱하면 됨.
- 확률 이론에서 두 확률변수 A와 B가 독립이면 다음이 성립한다:  $p(A, B) = p(A)p(B)$
- 두 단어가 우연히 함께 등장한다면, 다음과 같은 독립성 조건을 만족할 것으로 기대한다: $p(w_1, w_2) = p(w_1)p(w_2)$
- 만약 $p(w_1, w_2) > p(w_1)p(w_2)$ 라면, 두 단어는 우연보다 더 자주 함께 등장한다 
- 즉, 연관성이 있음
	- 독립이면: 같이 나올 확률 = 각자 나올 확률의 곱
	- 실제가 더 크면: **의미적/통계적 연관성이 존재**
- 분모는 두개가 동시에 관측할 확률
- 분자는 Joint probability
- PMI가 1보다 크면 (log를 씌웠으니 0보다 크면) 의미를 갖고 빈번하게 등장
- Positive PMI (PPMI): replaces all negative PMI values with zero
- N: Total word counts
- p(w1)확률: w1이 나온 빈도수/N
- p(w1,w2)=(w1,w2)빈도수 / N
- 분모가 0이 되는경우를 막기 위해 프로그램 구현할때는 스무딩을 이용해서 에러 방지
- PMI는 두 단어가 함께 등장할 확률과, 각각 독립적으로 등장할 확률을 비교하는 지표이다  

$$\text{PMI} = \log_2 \frac{p(w_1, w_2)}{p(w_1)p(w_2)}= \log_2 \frac{\mathrm{count}(w_1, w_2)\cdot N}{\mathrm{count}(w_1)\mathrm{count}(w_2)}$$

$$
\text{PMI} = \log_2 \frac{p(w_1, w_2)}{p(w_1)p(w_2)}
= \log_2 \frac{\#(w_1, w_2)\cdot N}{\#(w_1)\#(w_2)}
$$

- PMI 값 해석
	- **PMI = 0**  
	    - 두 단어가 우연에 의해 기대되는 정도로 함께 등장  
	    - 특별한 연관성 없음
	    - p(w1,w2)≤p(w1)p(w2) 
	- **PMI > 0**  
	     - 두 단어가 우연보다 더 자주 함께 등장 
	     - 값이 클수록 연관성이 강함
    - **PMI < 0**  
	    - 두 단어가 우연보다 덜 함께 등장  
	    - 음의 연관성 (실용적 의미는 크지 않음)
	    - p(w1,w2)<p(w1)p(w2)  
	    - 음수 PMI
- PMI = “같이 나올 확률 ÷ 독립 가정 확률”의 로그 
- 같이 나올수록 값 ↑ → 의미적 연관성 ↑
- Positive PMI (PPMI)
	- 음수 PMI 값을 0으로 치환한 것
	- 너무 낮은 음수값은 의미가 없어서 0으로 치환  

$$  
\text{PPMI} = \max \left( \log_2 \frac{p(w_1, w_2)}{p(w_1)p(w_2)},\ 0 \right)  
$$


### TF-IDF vs. PMI Weighting
#### TF-IDF
- 단어가 특정 문서에서 얼마나 중요한지를, 전체 문서 집합(corpus)과 비교하여 측정하는 방법
- 문맥 단위: 문서 수준
- 경험적 규칙(heuristic)에 기반함
- TF-IDF가 높다 = 해당 문서에서는 자주 등장하지만, 전체 문서에서는 드물게 등장하는 단어
#### PMI
- 두 단어 사이의 연관성 강도를 측정하는 방법
- 문맥 단위: 단어 쌍 수준 (보통 주변 단어 윈도우 기준)
- 확률적 가정에 기반함
- PMI가 높다 = 두 단어가 우연보다 더 자주 함께 등장 → 강한 연관성
#### 핵심 차이 (요약)
- **TF-IDF** → “이 단어가 이 문서에서 얼마나 중요한가”
- **PMI** → “이 두 단어가 얼마나 함께 잘 나오는가”

### Summary: Word Semantics & Senses
- 단어의 의미와 의미(뜻)를 이해하는 것은 더 나은 언어 모델을 만드는 데 도움이 된다
- 단어 의미는 매우 복잡하다
    - 다의성 (Polysemy): 하나의 단어가 여러 의미를 가짐        
    - 다차원적 특성 (Multi-faceted): 단어 의미는 다양한 측면을 포함함  
        (예: 쾌·불쾌(valence), 각성도(arousal), 지배성(dominance))
- 단어 간에는 다양한 관계가 존재한다
    - 동의어(synonyms)        
    - 반의어(antonyms)        
    - 하위어(hyponyms) / 상위어(hypernyms) 등        
- 단어 관계는 보통 이분법적이지 않다    
    - 완전히 동일한 의미의 단어(완전 동의어)는 드물다        
    - 따라서 단어 유사도(word similarity)는 더 유연한 개념으로 사용된다
 
### Summary: Classic Word Representations
- 초기 NLP 발전 단계에서 대규모 어휘 데이터베이스(WordNet)가 구축되었다    
- WordNet은 사람이 수작업으로 만든 동의어 집합(synset)과 이들 간의 관계 연결 구조로 구성되어 있다    
- WordNet은 단어 의미 중의성 해소(Word Sense Disambiguation)를 위한 데이터베이스로 활용될 수 있다 
#### WordNet의 한계
- 구축 및 유지·업데이트에 많은 노력이 필요하다    
- 특정 도메인 용어 및 저자원 언어에 대한 커버리지가 제한적이다    
- 개별 단어와 그 의미만 지원하며, 더 복잡한 표현에는 한계가 있다

### Summary: Vector Space Models
- 벡터 의미 공간:  
    단어의 의미를 벡터 표현을 통해 나타낸다
- 코사인 유사도는 벡터 간 유사도를 측정하는 데 가장 널리 사용되는 방법이다
- 단어-문서, 단어-단어 동시출현(co-occurrence) 통계는  
    의미 정보를 제공하며,  
    → 카운트 기반 벡터 표현도 꽤 잘 작동한다
- 단순 빈도(raw counts)는 좋은 표현이 아니다  
    → 전체적으로 자주 등장하는 단어에 편향됨
- TF-IDF는  
    문서 내에서 중요한 단어를, 다른 문서와 비교하여 강조한다
- PMI는  
    확률적(독립성 가정 기반)으로 두 단어 간 연관성 강도를 측정한다
