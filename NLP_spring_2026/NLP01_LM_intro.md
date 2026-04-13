2026-03-09 08:20
## 1강 LM intro
### Instructor

- 출결과 강의 크게 연관 없음
    - 단, 2/3 이상 출석 필수
SeongKu Kang (seongkukang@korea.ac.kr)

### Grading
- Midterm: 50% 
- Final exam: 50%

### 선행지식
- ML, DL 기본 지식 필요
- 아직 공부 안했다면 따로 공부 필요

### 자연어처리란?
- 전통적 언어학(Linguistics)와 휴먼 랭귀지, ML 의 교집합
- 컴퓨터가 사람의 언어를 해석하기 위한 학문

### The History of NLP
- 1980년대 언어학적 rule기반 연구가 많았음(주어, 동사, 명사 등등)
- 1980~2000년까지는 N-gram model처럼 통계 기반 모델이 많이 연구
- 2000~2018 딥러닝 모델이 활발하게 적용
	- CNN, RNN 등

- 2018~2022 빅테크등에서 BERT등 기학습된 언어 모델 많이 출시
	- 패러다임 쉬프트 생김김

- 2020~ 끝없이 발전 중
	- 현대 ML중 가장 빠르게 발전하는 분야 중 하나

- 이번 학기 수업은 기술의 발전을 빠르게 훑어보는게 목적
- 통계 기반 모델은 깊게 안들어갈 것
- 전반기는 neural network based 모델
- 후반기는 라지 랭귀지 모델(LLM) 중점
	- LLM을 잘 사용하고, RAG, LLM에이전트 까지 간단하게 다룰 예정

### 랭귀지 모델링
- NLP의 가장 중요, 가장 기본이 랭귀지 모델링임.
- 문장의 확률을 계산하는 것이 랭귀지 모델링
- 랭귀지 모델링이 되면 문장을 이해 할 수 있음.
	- 어떤 문장이 더 일상에 활용 될 것 같은지 판단
- 그 다음 단어가 뭐가 나와야 할지도 판단 가능

### Language Modeling: Probability Decomposition
- 그동안은 랭귀지 모델을 다루기 위해 간단하게 decomposisiotn 하는 방법론을 많이 사용 함.
- 어떤 단어가 등장할 확률은 이전 단어를 기반으로 판단 함.
- 이전 단어에 영향을 받는 곱으로 수식을 만들 수 있음.
- 단, 100번째 단어는 앞의 99개의 확률을 다뤄야 하기 때문에 문제가 있었음

### N-gram Language Model: Simplified Assumption
- N-gram은 n-1개의 단어에만 의존적이다라는 가정으로 시작
- 모든 앞 단어를 고려 하지 않음
- Unigram LM 과거 고려 x
- Bigram은 이전 1단어 + 지금 1개
- Trigram 2단어 전+ 지금 1개

### Why Is NLP Challenging?
- 단어를 이해 하는데 맥락에 맞는 해석이 필요함.
- 소비자 의도를 점원이 잘 못 이해하는 예시 
	- 머핀과 초코칩을 사자고 한다 → 캐쉬만 가능합니다.

### How to Understand Human Language?
- 단어를 이해하는 방법론을 다루게 됨
- 텍스트 마이닝 수업 들었다면 수월 함.
	- 마이닝 + 벡터 스페이스 구성 등등

### Word Embeddings
- 방대한 텍스트 코퍼스가 있을 때 벡터 스페이스에 잘 맵핑하는 연구

- Word2Vec 방법론 

### Sequence Modeling & Recurrent Neural Networks (RNNs)
- 자연어는 단어들이 만드는 시퀀스임.
- 시퀀스 모델도 다루게 될 것

### Sequence Modeling
- 텍스트는 단어들의 시퀀스
- 단순 단어나열이 아니라 연결되어 의미를 부여하기도 함.

### Sequence Modeling Architecture: RNN, CNN
- RNN~CNN등 인기 있었던 모델들을 다룰 예정 
- 여기 까지가 전반부 더나가면 트랜스 포머 까지

### Language Modeling with Transformers

- 현대 NLP의 근간을 이루는 모델인 트랜스포머 
- 텍스트 마이닝 수업에서는 인코더만 다뤘는데 이번에는 디코더까지 전체를 다룰 예정

### Large Language Models (LLMs)
- 잘 만들어진 미래 기술 같지만 수년간 쌓인 자연어 처리 연구의 조합 및 고도화임.
- 어떤 동작원리인지 다룰 예정이고,
- 어떻게 다루면 좋은지 수업

### In-Context Learning
- LLM의 답변을 조절하는 방법은 2가지가 있음
	- 답변을 조절하는 방법으로는 LLM의 파라메터를 건들수도 있고
	- 인풋 정보를 조절해서 아웃풋을 조절할 수 있음 → **이게 인콘텍트 러닝**

- 다양한 인-콘텍트 기법들

### Knowledge in LLMs and Retrieval-Augmented Generation (RAG)
- RAG
	- 요즘 핫한 기법
	- 문장을 이해하면 질의 응답을 할 수 있게 개발 할 수 있음
	- 어떤 문장을 듣고 확률적으로 좋은 답변을 얻을 수 있음 
		- 단, 할루시 네이션도 있고 같은 질의에 다른 답을 얻을 수 있음
	- 별도의 리트리거를 사용해서 답변을 받을 수 있는게 RAG

### Language Model Alignment
- LLM의 파라메터를 건드는 방법

### Reinforcement Learning from Human Feedback
- GPT 답변 처럼 2개를 주고 원하는 답변을 선택하게 한 후 피드백을 강화 학습에 사용
