2026-04-15 08:20
## 6강 Evaluation

- 분류모델의 평가 수업 후 회귀 모델 평가 방법

### Evaluating Classification Model Performance
- 분류 문제(classification problem)는 학습된 패턴을 바탕으로 입력 데이터를 미리 정의된 범주에 할당하는 문제이다.
- 지도 학습(supervised learning)에서는 이러한 패턴을 인식하고 새로운 데이터에 대해 예측할 수 있도록, 레이블이 있는 예제로 모델을 학습시킨다.  
	- 분류기 측정 레이블: "사과(Apple)" 또는 "사과 아님(Not apple)"

- 분류 모델은 선형 모델로 쉽게 확장 가능함.
- 얼마나 일반화 성능이 좋은지, 새로운 데이터가 왔을때 값을 잘 예측하는지가 모델의 목표

- 이진 분류(binary classification)에서는 테스트 데이터셋이 두 개의 레이블을 가진다: 양성(positive, 예: "사과")과 음성(negative, 예: "사과 아님"). 
- 바이너리는 positive or negative로 분류하기도 함.

- 이상적인 경우, 완벽한 분류기는 예측 레이블이 실제 레이블과 정확히 일치하는 결과를 만든다.    
- 그러나 현실 세계의 응용에서는 결함 없는 이진 분류기를 얻는 경우는 드물다.    
- 대신, 실제 분류기의 예측은 실제 레이블과 일정한 정도까지만 일치한다.

- 어떤 classifier던 디시전 바운더리를 만들게 됨.
- 위쪽은 양성으로 예측 아래는 음성으로 예측한다고 정의 할 수 있음.
- classifier가 이상적이라면 모두 예측 할 것
- 하지만 100% 성능 발휘하는 것은 불가능 함. 약간의 오차가 생김.

- 그러면 이 분류(또는 예측)는 네 가지 결과를 만든다: 참 양성(True Positive, TP), 참 음성(True Negative, TN), 거짓 양성(False Positive, FP), 거짓 음성(False Negative, FN).

- 여기서 나오는 4가지 case의 outcome 이 발생
	- True Positive, TP
	- True Negative, TN
	- False Positive, FP: 실제는 네가티브인데 트루로로 잘못 예측-파지티브가 아님
		- Type 1 error
	- False Negative, FN: 실제는 참인데 네거티브로 잘못 예측 - 네거티브가 아님.
		-  Type 2 error

- 이러한 결과는 일반적으로 혼동 행렬(confusion matrix)로 요약되며, 이는 분류 성능 평가의 핵심 도구이다.    
- 혼동 행렬은 실제 레이블과 예측 레이블을 구조적으로 비교하며, 이를 바탕으로 다양한 평가 지표를 계산할 수 있다.

- 예를 들어, 아래 혼동 행렬에서 암이 있는 8개의 샘플 중 시스템은 2개를 암이 없다고 판단하였다.    
- 또한 암이 없는 4개의 샘플 중 1개를 암이 있다고 예측하였다.

- 오류율(Error Rate, ERR)은 모든 잘못된 예측의 수를 전체 데이터셋의 수로 나눈 값이다.
- 가장 좋은 오류율은 $0.0$이고, 가장 나쁜 오류율은 $1.0$이다.
- Error Rate:  

$$  
\mathrm{Error\ Rate}=\frac{FP+FN}{FP+FN+TP+TN}  
$$

- 잘못된 false 값 2개가 분자로 감.
- 분모는 전체 합

- 정확도(Accuracy, ACC)는 모든 올바른 예측의 수를 전체 데이터셋의 수로 나눈 값이다.
- 가장 좋은 정확도는 $1.0$이고, 가장 나쁜 정확도는 $0.0$이다.
- Accuracy(정확도):  

$$  
\mathrm{Accuracy}=\frac{TP+TN}{FP+FN+TP+TN}  
$$

- True 값 2개가 분자로 감.
- 분모는 전체 합


- 민감도(Sensitivity, SN)는 올바른 양성 예측의 수($TP$)를 전체 양성의 수($P$)로 나눈 값이다.
- 이는 재현율(Recall, REC) 또는 진양성률(True Positive Rate, TPR)이라고도 한다.
- 가장 좋은 민감도는 $1.0$이고, 가장 나쁜 민감도는 $0.0$이다.
- Sensitivity민감도:  

$$  
\mathrm{Sensitivity}=\frac{TP}{FN+TP}  
$$


- 민감도 Sensitivity는 True이고 positive 인게 분자
- 분모는 실제로 positive(false negative + true positive)

- 정밀도(Precision, PREC)는 참 양성 예측의 수($TP$)를 전체 양성 예측의 수($TP+FP$)로 나눈 값이다.
- 이는 양성 예측도(Positive Predictive Value, PPV)라고도 한다.
- 가장 좋은 정밀도는 $1.0$이고, 가장 나쁜 정밀도는 $0.0$이다.
- Precision정밀도:  

$$  
\mathrm{Precision}=\frac{TP}{FP+TP}  
$$

- 정밀도 Precision는 True이고 positive 인게 분자
- 분모는 실제로 positive로 판정한 것들이 분모(false positive + true positive)

#### F1 score
- 분류 작업에서 재현율(recall)을 우선하면 실제 양성 사례를 놓치는 경우는 줄어들지만 거짓 양성(false positives)은 증가한다.
- 반대로 정밀도(precision)를 강조하면 양성 예측의 정확성은 높아지지만 거짓 음성(false negatives)은 증가한다.
- 이러한 상충 관계를 균형 있게 다루기 위해, 정밀도와 재현율의 **조화평균(harmonic mean)**인 F1-score를 사용한다.  

$$  
F1=2\cdot\frac{\mathrm{PREC}\times\mathrm{REC}}{\mathrm{PREC}+\mathrm{REC}}=\frac{2TP}{2TP+FP+FN}  
$$

- y축은 정밀도 x축은 재현율(재현율은 민감도sensitivity 임.)

- 미검출률(Miss Rate, MR)은 거짓 음성 예측의 수($FN$)를 전체 양성의 수($P$)로 나눈 값이다.
- 가장 좋은 미검출률은 $0.0$이고, 가장 나쁜 미검출률은 $1.0$이다.
- 미검출률:  

$$  
\mathrm{Miss\ Rate}=\frac{FN}{FN+TP}  
$$

- 얼마나 놓쳤는지를 수치화
- 실제 positive중에 놓친 positive 비율임.

- 특이도(Specificity, SP)는 올바른 음성 예측의 수($TN$)를 전체 음성의 수($N$)로 나눈 값이다.
- 이는 진음성률(True Negative Rate, TNR)이라고도 한다.
- 가장 좋은 특이도는 $1.0$이고, 가장 나쁜 특이도는 $0.0$이다.
- 특이도:  

$$  
\mathrm{Specificity}=\frac{TN}{FP+TN}  
$$
- 특이도는 네가티브 중에 진짜 네가티브

- 거짓 양성률(False Positive Rate, FPR)은 거짓 양성 예측의 수($FP$)를 전체 음성의 수($N$)로 나눈 값이다.
- 가장 좋은 거짓 양성률은 $0.0$이고, 가장 나쁜 거짓 양성률은 $1.0$이다.
- 또한 $1-\mathrm{Specificity}$로도 계산할 수 있다.
- 거짓 양성률:  

$$  
\mathrm{False\ Positive\ Rate}=\frac{FP}{FP+TN}  
$$


- 거짓 양성률은 실제로 네거티브 중에 positive로 판정된 것.

- 의료 분류 시나리오에서 실제로 임신한 40명과 임신하지 않은 60명을 포함한 총 100명의 환자 집단이 세 명의 의사를 찾아와 진단을 받는다고 가정하자.
- 각 의사는 환자가 임신했는지 여부를 예측하며, 그 성능은 혼동 행렬(confusion matrix)을 사용하여 평가할 수 있다.

- Dr. Kim says

|실제 상태|예측: Not pregnant|예측: Pregnant|
|---|---|---|
|Not pregnant|0|60|
|Pregnant|0|40|

- Dr. Lee says

|실제 상태|예측: Not pregnant|예측: Pregnant|
|---|---|---|
|Not pregnant|60|0|
|Pregnant|40|0|

- Dr. Park says

| 실제 상태        | 예측: Not pregnant | 예측: Pregnant |
| ------------ | ---------------- | ------------ |
| Not pregnant | 60               | 0            |
| Pregnant     | 0                | 40           |


- 분류기의 성능은 선택한 평가 지표에 따라 다르게 나타나므로, 성능이 좋지 않은 모델도 특정 척도에서는 효과적으로 보일 수 있다.

|평가 지표|Dr. Kim|Dr. Lee|Dr. Park|
|---|---|---|---|
|Error rate|60/100|40/100|0/100|
|Accuracy|40/100|60/100|100/100|
|Sensitivity|40/40|0/40|40/40|
|Specificity|0/60|60/60|60/60|
|Precision|40/100|0/0|40/40|
|False positive rate|60/60|0/60|0/60|

- 오류율(error rate)과 정확도(accuracy)만을 평가 지표로 제한하면 어떨까?

|평가 지표|Dr. Kim|Dr. Lee|Dr. Park|
|---|---|---|---|
|Error rate|60/100|40/100|0/100|
|Accuracy|40/100|60/100|100/100|

- 이러한 지표들은 때때로 오해를 불러일으킬 수 있으며, 특히 클래스 분포가 불균형한 경우 더욱 그렇다.
- 암 진단 시나리오에서 음성 환자 98명과 양성 환자 2명이 있다고 가정하자.
- 완벽한 분류기(Perfect classifier)

|실제 상태|예측: Negative|예측: Positive|
|---|---|---|
|Negative|98|0|
|Positive|0|2|

- 게으른 분류기(Lazy classifier)
	- 무조건 Negative로 분류하는 것.

| 실제 상태    | 예측: Negative | 예측: Positive |
| -------- | ------------ | ------------ |
| Negative | 98           | 0            |
| Positive | 2            | 0            |


- 대부분의 사례를 음성으로 예측하는 모델은 높은 정확도를 얻을 수 있지만, 양성 사례를 신뢰성 있게 탐지하지 못할 수 있다.
- 이는 이러한 상황에서 정확도(accuracy)와 오류율(error rate)의 한계를 보여준다.

|평가 지표|Perfect classifier|Lazy classifier|
|---|---|---|
|Error rate|0.00|0.02|
|Accuracy|1.00|0.98|

- 매튜스 상관계수(Matthews Correlation Coefficient, MCC)는 혼동 행렬의 네 가지 값($TP$, $TN$, $FP$, $FN$)을 모두 반영하여 분류 성능을 평가하는 지표이다.
- 값의 범위는 $-1$에서 $1$까지이며, $-1$은 완전히 잘못된 분류기, $1$은 완벽한 분류기, $0$은 무작위 추측과 다르지 않은 성능을 의미한다.
- 정확도(accuracy)와 달리, MCC는 균형 잡힌 척도를 유지하므로 클래스 분포가 매우 불균형한 경우에도 모델 평가에 적합하다.
- MCC:  

$$  
\mathrm{MCC}=\frac{TP\cdot TN-FP\cdot FN}{\sqrt{(TP+FP)(TP+FN)(TN+FP)(TN+FN)}}  
$$

- 앞선 예제로 돌아가면, MCC는 보다 균형 잡힌 성능 평가를 제공한다.
- 완벽한 분류기(Perfect classifier)

|실제 상태|예측: Negative|예측: Positive|
|---|---|---|
|Negative|98|0|
|Positive|0|2|

- 게으른 분류기(Lazy classifier)

|실제 상태|예측: Negative|예측: Positive|
|---|---|---|
|Negative|98|0|
|Positive|2|0|

- MCC

|평가 지표|Perfect classifier|Lazy classifier|
|---|---|---|
|Error rate|0.00|0.02|
|Accuracy|1.00|0.98|
|MCC|1.00|0.00|


- 이진 분류 모델에서는 예측 확률이 양성인지 음성인지 결정하기 위해 의사결정 임계값(decision threshold)을 자주 사용한다.
- 이 임계값을 변화시키면 참 양성(True Positive)과 거짓 양성(False Positive) 사이의 균형을 조정할 수 있다.

- 시그널 디텍트 theory가 있음
	- 확률 분포로 설명 함.
- ML을 하다보면 임계값을 조정해야 하는 때가 가끔 있음.
- z 축이 의미가 있을까? 
	- 무시해도 됨 시각화 위해 두개의 분포를 나눠서 그림.


- 수신자 조작 특성 곡선(receiver operating characteristic curve), 즉 ROC 곡선은 다양한 임계값(threshold)에서 이진 분류 모델의 성능을 보여주는 그래프이다.
- ROC 곡선은 각 임계값 설정에서 진양성률(True Positive Rate, TPR 또는 Sensitivity)과 거짓 양성률(False Positive Rate, FPR 또는 $1-\mathrm{Specificity}$)을 좌표평면에 나타낸 것이다.

- 한번에 평가 지표를 보기 위해 ROC를 그리기도 함.
	- x축은 False positive rate
	- y축은 True positive reate

- 양성 인스턴스 100개와 음성 인스턴스 100개에 대한 네 가지 예측 결과를 생각해 보자.
- 이는 ROC 공간(ROC space)에서 시각화할 수 있다.

- 반반 맞추면 저 가운데 선에 걸치게 됨
	- Random classifier라고 함.
- 좌측 상단 1에 분류 되면 perfect classifier

- 대각선은 ROC 공간을 나눈다.
- 대각선 위의 점들은 좋은 분류 결과(무작위 추측보다 우수함)를 나타낸다.
- 대각선 아래의 점들은 나쁜 결과(무작위 추측보다 열등함)를 나타낸다.

- 곡선 아래 전체 면적(area under the curve, AUC)은 ROC 곡선 아래의 전체 2차원 면적을 측정한 값이다.
- 이 점수는 분류기가 얼마나 잘 작동할지를 평가하는 데 유용한 기준을 제공한다.

- ROC 커브 그리는 것도 한눈에 들어오지 않아서 ROC 아래 면적을 계산 하는 방법을 고안함.
- 1이하의 수치로 볼 수 있음

- 혼동 행렬(confusion matrix)은 이진 분류를 넘어 확장될 수 있으며, 다중 분류(multi-class classification) 문제에도 동일하게 적용할 수 있다.

- multi class classifier 에도 적용 할 수 있음.

- 혼동 행렬은 오분류 사례, 클래스별 성능 문제, 특정 클래스에 대한 편향, 그리고 반복적으로 나타나는 체계적 오류를 드러내어 오류 패턴을 파악할 수 있게 한다.
- 이를 통해 모델 성능을 개선하기 위한 통찰을 제공한다.

- 표를 그려 에러 패턴이 어떻게 작용하는지 볼 수 있음.

### The Class Imbalance Problem
- 클래스 불균형(class imbalance)은 현실 세계 데이터셋에서 흔히 나타나는 문제로, 특정 클래스가 다른 클래스보다 현저히 많이 포함된 상태를 의미한다.    
- 이러한 문제는 스팸 필터링(spam filtering), 사기 탐지(fraud detection), 질병 선별(disease screening)과 같은 다양한 분야에서 발생한다.    
- 이 경우 일반적으로 양성 사례의 수가 음성 사례보다 훨씬 적다.

- 기계 학습에서는 불균형 문제가 크게 발생 할 수 있음.
- 학습 평가 둘다 영향을 미침

- 이러한 조건에서 학습된 모델이 비슷한 정확도(accuracy)를 얻더라도, 클래스를 구별하지 못한다면 실질적으로 의미 있는 통찰을 제공하지 못한다.
- 예를 들어, 암 진단 시나리오에서 양성 종양이 $90\%$, 악성 종양이 $10\%$인 데이터셋은 모든 사례를 양성 종양으로 예측하기만 해도 $90\%$의 정확도를 얻을 수 있으며, 이는 데이터로부터 실제로 학습한 결과가 아니다.
- 이러한 한계 때문에, 불균형 데이터셋에서는 정확도만으로 모델을 평가하는 것이 대체로 충분하지 않다.
- 대신 정밀도(precision), 재현율(recall), ROC 곡선과 같은 대안적 지표들이 응용 목적에 맞추어 더 많은 정보를 제공한다.

- 평가를 넘어, 클래스 불균형(class imbalance)은 모델 학습 과정 자체에도 영향을 미친다. 
- 대부분의 기계 학습 알고리즘은 모든 학습 인스턴스에 대해 합산된 손실 함수(loss function) 또는 보상 함수(reward function)를 최적화하므로, 전체 오류를 최소화하기 위해 다수 클래스(majority class)를 선호하는 경향이 있다.    
- 그 결과, 의사결정 규칙은 지배적인 클래스 쪽으로 기울어지기 쉽고, 이는 편향된 예측과 소수 클래스(minority class)에 대한 낮은 일반화 성능으로 이어진다.

- 훈련세트에 편향값을 같은 비율로 나누는 방법도 생각 할 수 있음.

- 불균형한 상황에서 신뢰할 수 있는 모델을 구축하려면, 평가 전략을 조정하고 학습 과정에서 편향을 완화하는 기법을 함께 고려해야 한다.
- 이를 통해 모든 클래스가 더 잘 대표되고 학습될 수 있다.
- 모델 학습 중 클래스 불균형을 해결하는 한 가지 방법은 소수 클래스(minority class)를 잘못 분류했을 때 더 큰 패널티를 부여하는 것이다.
- scikit-learn에서는 대부분의 분류기에서 제공되는 `class_weight='balanced'` 매개변수를 사용하여 이를 쉽게 조정할 수 있다.
- 이 설정을 적용하면 알고리즘은 소수 클래스를 올바르게 분류하는 데 더 큰 중요도를 부여하여, 데이터셋의 불균형 영향을 완화하는 데 도움을 준다.

- 실무나 연구에서는 소수 데이터에 웨이트를 주는 방법을 많이 사용함.
- classifier마다 적용하는 방법이 달라서 사용하는 모델마다 확인 필요.
- 데이터를 조절하는 방법은 아님.

- 또 다른 일반적인 방법은 데이터셋 자체를 수정하는 것으로, 소수 클래스(minority class)를 업샘플링(인스턴스를 복제하여 비율 증가)하거나 다수 클래스(majority class)를 다운샘플링(샘플을 무작위 제거하여 크기 감소)하는 방식이 있다.
- 이러한 기법들은 데이터셋의 균형을 맞추어, 모델이 모든 클래스에 걸쳐 의미 있는 패턴을 더 쉽게 학습하도록 돕는다.
- 데이터를 직접 조절하는 방법임.
- 소수 데이터를 비율에 맞게 조절해서 할당 하는 방식

- 더 정교한 접근법으로는 기존 데이터를 단순히 복제하는 대신, 완전히 새로운 학습 예제를 생성하는 합성 데이터 생성(synthetic data generation)을 사용할 수 있다.
- 그 예시로 SMOTE(Synthetic Minority Over-sampling Technique)가 있으며, 이는 기존 소수 클래스 인스턴스를 기반으로 인공적인 데이터 포인트를 생성한다.
- SMOTE에 대한 자세한 내용은 Nitesh Chawla와 동료들의 원 논문(2002)에서 확인할 수 있다.
- 또한 이는 불균형 데이터셋 처리를 위한 다양한 도구를 제공하는 Python 라이브러리 `imbalanced-learn`에 구현되어 있다.

- SMOTE라는 알고리즘 예시
	- 소수의 데이터를 비슷하게 생성해서 수를 어느정도 맞춰주는 방법
	- 약간 interpolation 방식과 유사하다고 생각 하면 됨.


### Evaluating Regression Model Performance
- regression 평가 방식
- 회귀(regression)는 입력 특징(feature)과 연속형 목표값(continuous target) 사이의 관계를 모델링하는 핵심 지도 학습(supervised learning) 기법이다.
- 단변량 선형 회귀(univariate linear regression)는 하나의 입력 변수에 직선을 적합한다.
- 다변량 선형 회귀(multivariate linear regression)는 이를 여러 입력 변수로 확장하며, 더 복잡한 예측을 위해 초평면(hyperplane)을 사용한다.

- 분류와 차이점은 연속적인 값을 예측

- 회귀 모델을 다룰 때는 먼저 변수들이 서로 어떻게 상호작용하는지 탐색하는 것이 중요하다.
- 특징(feature) 간의 의존성을 살펴보는 한 가지 방법은 산점도 행렬(scatterplot matrix)이다.
- 이는 변수 쌍별 상관관계를 시각화하여 패턴, 잠재적 이상치(outlier), 그리고 변수 사이의 선형 관계를 파악하는 데 도움을 준다.

- 평가전에 실제 데이터를 시각화(scatterplot) 해서 확인 하는것이 매우 중요 함.

- 이러한 관계를 더 정량적으로 측정하는 공식적인 방법은 상관계수(correlation coefficient)를 계산하는 것이다.    
- 이는 피어슨 상관계수(Pearson’s correlation coefficient)를 사용하여 특징들 사이의 선형 연관성의 강도를 측정한다.    
- 이 계수는 $-1$에서 $1$ 사이의 값을 가지며, 두 변수가 얼마나 함께 움직이는지를 나타낸다.    
- 양의 값은 같은 방향으로 움직임을, 음의 값은 반대 방향으로 움직임을 의미한다.

- 참고: [https://en.wikipedia.org/wiki/Correlation](https://en.wikipedia.org/wiki/Correlation)  

$$  
r_{xy}=  
\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}  
{\sqrt{\sum_{i=1}^{n}(x_i-\bar{x})^2}\sqrt{\sum_{i=1}^{n}(y_i-\bar{y})^2}}  
$$

- 이런 scatterplot의 상관계수를 구해서 선을 그어 보게 됨
- 유명한게 피어슨 상관계수가 있음.
	- r=1 매우 잘 예측
	- r=0 관계 없음
	- r<0 음의 상관 관계계


- 상관계수가 낮다고 해서 반드시 변수들이 서로 관련이 없다는 뜻은 아니다.
- 이는 실제로 연관성이 없음을 의미할 수도 있고, 전통적인 선형 측정 방식으로는 포착되지 않는 비선형 관계를 반영한 결과일 수도 있다.

- 피어슨 상관계수는 r=1인것은 확인 되어도 기울기는 확인 불가
- 데이터간 상관관계를 직선으로만 확인 가능
	- r=0일때 데이터가 원형일수도 오목 볼록일수도 다양한 모양일 수도 있는데 확인 불가.


- 가장 널리 사용되는 척도인 피어슨 상관계수(Pearson correlation coefficient)는 선형 관계를 평가하도록 설계되었다.
- 반면, 스피어만 순위 상관계수(Spearman’s rank correlation coefficient)와 같은 대안적 척도는 더 강건하며, 보다 넓은 단조 관계(monotonic relationship)를 포착할 수 있다.
- 참고: [https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient](https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient)  

$$  
\rho=1-\frac{6\sum_{i=1}^{n}d_i^2}{n(n^2-1)}  
$$

- $d_i$: $x_i$와 $y_i$의 순위(rank) 차이
- $n$: 관측값의 개수

- 순위기반해서 상관관계를 예측하는 방법이 스피어만 랭크 상관계수
- 선형이 아닌 단조 관계 평가에 좋음.

- 상관관계(correlation)는 두 변수 사이 관계의 강도를 측정하지만, 인과관계(causation)를 의미하지는 않는다.
- 실험 환경에서는 하나의 변수를 조작하고 다른 모든 변수를 일정하게 유지함으로써 인과성을 검토할 수 있다.
- 그러나 상관 연구(correlational study)에서는 이러한 통제가 없으므로, 한 변수의 변화가 다른 변수의 변화를 직접적으로 일으키는지 명확하지 않다.
- 예를 들어, 공룡의 문맹률(dinosaur illiteracy)과 멸종(extinction) 사이에 상관관계가 나타날 수는 있어도, 한쪽이 다른 쪽의 원인이라고 결론내리는 것은 터무니없는 주장이다.

- 상관 관계는 원인과 결과와는 무관하다. 꼭 기억 해야 함.

- 회귀 모델이 학습된 후에는, 보지 않은 데이터(unseen data)에 대해 성능을 평가하여 얼마나 잘 일반화(generalize)하는지 확인하는 것이 중요하다.
- 회귀 모델은 연속적인 값을 예측하므로, 성능은 일반적으로 잔차(residual) 또는 오차(error) 지표를 사용하여 분석된다.

- 정량적 평가를 위해 평균제곱오차(Mean Squared Error, MSE)와 평균절대오차(Mean Absolute Error, MAE)가 널리 사용된다.

- MSE는 실제값과 예측값 사이 차이의 제곱 평균을 측정한다.

- MAE는 절대 오차의 평균을 제공하므로 더 직관적으로 해석할 수 있다.

- MSE는 큰 오차에 민감하므로, 원래 단위 척도에서 오차를 표현하기 위해 평균제곱근오차(Root Mean Squared Error, RMSE)를 자주 사용한다.  

$$  
\mathrm{MSE}=\frac{1}{n}\sum_{i=1}^{n}\left(y^{(i)}-\hat{y}^{(i)}\right)^2  
$$  

$$  
\mathrm{MAE}=\frac{1}{n}\sum_{i=1}^{n}\left|y^{(i)}-\hat{y}^{(i)}\right|  
$$  

$$  
\mathrm{RMSE}=\sqrt{\mathrm{MSE}}  
$$

- 이러한 지표들에 더해, 결정계수(coefficient of determination), 즉 $R^2$는 데이터의 전체 변동성(total variation)까지 고려하여 보완적인 관점을 제공한다.
- 구체적으로 $R^2$는 평균을 예측하는 기준 모델(baseline model)에 비해, 목표 변수(target variable)의 분산 중 모델이 설명하는 비율을 나타낸다.  

$$  
R^2=1-\frac{\sum_{i=1}^{n}\left(y^{(i)}-\hat{y}^{(i)}\right)^2}{\sum_{i=1}^{n}\left(y^{(i)}-\bar{y}\right)^2}  
$$

- $\sum_{i=1}^{n}\left(y^{(i)}-\hat{y}^{(i)}\right)^2$: 잔차제곱합(SSR 또는 SSE)
- $\sum_{i=1}^{n}\left(y^{(i)}-\bar{y}\right)^2$: 전체제곱합(SST)
- $\bar{y}$: 실제값의 평균

- 결정계수(coefficient of determination), 즉 $R^2$
	- MSE보다 한발 더 나감.
	- 에러의 분산값을 고려한 지표임.

- 모델이 데이터를 완벽하게 적합하면 $R^2=1$이 된다.
- 목표 변수의 평균을 예측하는 것보다 더 잘하지 못하면 $R^2=0$이 된다.
- 음의 $R^2$ 값은 모델이 평균에 해당하는 단순한 수평선보다도 성능이 나쁘다는 뜻이다.

- $R^2$가 음수면 평균도 잘 예측 못한다는 의미.

- 수학적으로 $R^2$는 제곱오차합(Sum of Squared Errors, $SSE$)을 전체제곱합(Total Sum of Squares, $SST$)으로 나눈 비율을 $1$에서 뺀 값으로 계산된다.  

$$  
R^2=1-\frac{SSE}{SST}=\frac{SST-SSE}{SST}  
$$  

$$  
SSE=\sum_{i=1}^{n}\left(y^{(i)}-\hat{y}^{(i)}\right)^2  
$$  

$$  
SST=\sum_{i=1}^{n}\left(y^{(i)}-\mu_y\right)^2  
$$

- 여기서 $SSE$는 실제값과 예측값 사이 제곱 오차의 총합을 의미한다.
- $SST$는 목표 변수(target variable)의 전체 분산을 의미한다.
- $\mu_y$는 실제 목표값의 평균이다.

- $SST$는 데이터의 전체 변동성(total variability)을 나타내고, $SSE$는 설명되지 않은 변동성(unexplained variability), 즉 오차(error)를 나타낸다.
- 따라서 $SST-SSE$는 모델이 성공적으로 설명한 분산의 양에 해당한다.
- 이는 설명된 분산(explained variance)이라고도 한다.

- MSE와 MAE는 평균 예측 오차를 절대적인 크기로 정량화하지만, 목표 변수(target variable)의 단위에 의존하므로 맥락 없이 해석하기 어려울 수 있다.
- 반면 $R^2$는 종속 변수(dependent variable)의 분산 중 모델이 설명하는 비율을 나타내므로, 서로 다른 데이터셋이나 모델 사이에서도 더 쉽게 이해하고 비교할 수 있다.


- $R^2$가 다른 평가 방법보다 설명을 잘함.
- y값 크기(unit)에 덜 민감함.
- y값이 커지면 MSE값도 커짐을 확인 할 수 있음

