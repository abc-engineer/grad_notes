## Modern day monitoring and control challenges outlined on an industrial-scale benchmark fermentation process

## Contents / Memo

### Abstract
이 논문은 기존에 개발된 산업 규모 페니실린 발효 시뮬레이션인 **IndPenSim**을 확장하여, 현대 바이오의약품 제조시설이 직면하는 실제 공정 제어 문제를 다룬다.
주요 확장 내용에는 바이오기술 시설에 적용 가능한 고도화되고 혁신적인 제어 솔루션을 개발, 평가 및 구현하기 위한 목적으로 **시뮬레이션된 Raman spectroscopy 장치**를 추가한 것이 포함된다.
IndPenSim은 **고정 제어 모드** 또는 **작업자 제어 모드**로 운전할 수 있으며, 각 배치에 대해 사용 가능한 모든 **온라인 데이터**, **오프라인 데이터**, 그리고 **Raman 스펙트럼 데이터**를 생성한다.
IndPenSim의 기능은 처음에 **PAT 프레임워크의 세 단계**를 활용한 **QbD 방법론**의 구현을 통해 입증되었다. 또한 IndPenSim은 연간 캠페인 동안 기록된 여러 배치에서 발생하는 공정 이상을 탐지하기 위해 **이상 탐지 알고리즘**을 평가하였다.
여기서 제시된 시뮬레이터와 모든 데이터는 `www.industrialpenicillinsimulation.com`에서 다운로드할 수 있으며, 연구자들이 해당 시설에 적용된 현재 제어 전략을 분석, 개선 및 최적화할 수 있는 **벤치마크** 역할을 한다.
또한 사용 가능한 모든 공정 측정값과 Raman spectroscopy 측정값을 포함하는 **100개 배치의 매우 가치 있는 데이터 자원**이 무료로 제공된다.
이 데이터는 바이오의약품 산업에 적용 가능한 **빅데이터 분석**, **머신러닝(ML)** 또는 **인공지능(AI)** 알고리즘 개발에 매우 적합하다.

### 1. Introduction
페니실린 발효의 모니터링과 제어는 지난 30년 동안 수행되어 왔다(Mou and Cooney, 1983; Min et al., 1995; Lee et al., 2004a; Luo and Bao, 2018).
그러나 바이오의약품 분야 전체는 여전히 **첨단 공정 제어(APC, Advanced Process Control)** 의 도입 측면에서 다른 산업 분야에 비해 상당히 뒤처져 있다. 특히 **혁신적인 공정분석기술(PAT, Process Analytical Technology)** 솔루션의 활용 측면에서 이러한 경향이 두드러진다(Tomba et al., 2013).
이는 석유·가스, 반도체, 자동차 산업과 같은 고도로 발전된 산업과 비교할 때 더욱 분명하게 나타난다. 이러한 산업에서는 자동화와 린 제조가 기업의 실무와 문화 속에 더 깊이 자리 잡고 있다.
이를 개선하기 위해 산업 규제기관에서는 큰 추진력을 제공해 왔는데, 대표적으로 FDA가 각각 2004년과 2009년에 제시한 **QbD(Quality by Design)** 및 **PAT** 이니셔티브의 시행이 있다(FDA 2004, FDA 2009).
그러나 여전히 남아 있는 주요 과제는 이러한 새로운 제어 솔루션을 산업적 바이오의약품 공정 전반에 도입하고 구현하는 데 필요한 **전문성**과 **확신**이다.
지난 25년 동안 복잡한 산업 공정을 모사하는 **제1원리 기반 수학적 모델(first principles mathematical models)** 의 개발은 **첨단 공정 제어(APC, Advanced Process Control)** 솔루션의 개발과 적용에 도움을 주어 왔다 (Downs and Vogel, 1993; Lyman and Georgakis, 1995; Birol et al., 2002; Jeppsson et al., 2007; Kontoravdi et al., 2010; Kiparissides et al., 2011; Benyahia et al., 2012; Gernaey and Gani, 2010; Goldrick et al., 2014; Papadakis et al., 2018).

새로운 제어 전략을 실제 공정에 적용하기 전에 시뮬레이션상에서 시험하고 검증할 수 있는 능력은, 바이오의약품 분야 전반에서 제어 이론과 고급 제어기의 적용을 혁신적으로 변화시킬 잠재력을 가지고 있다  
(Randek and Mandenius, 2018; Yuan et al., 2009).
현재 바이오의약품 수학적 모델의 한계는, 현대 바이오의약품 제조시설이 직면하고 있는 최신 공정 제어 문제들을 충분히 다루지 못한다는 점이다.
Industry 4.0의 미래 시대에는, 수많은 첨단 **온라인 공정 분석 기술(on-line process analytics)**을 포함하는 고도로 지능화된 **데이터 기반 제조 환경**이 예상된다(Sami Sivri and Oztaysi, 2018).
이러한 환경에서는 **현대 바이오의약품 공정을 모사할 수 있는 시뮬레이션**의 필요성이 매우 중요하다.
이 논문에서 설명하는 시뮬레이션은, **IndPenSim**이라 불리는 매우 복잡한 산업 규모의 페니실린 발효 공정을 확장함으로써 현재와 미래의 바이오의약품 제조 공정이 직면한 문제들을 해결하는 것을 목표로 한다.
이 시뮬레이션은 고수율 산업용 균주인 Penicillium chrysogenum을 이용한 **100,000 리터 규모의 페니실린 발효 공정**의 과거 배치 기록을 기반으로 개발되었으며, 사용 가능한 모든 공정 입력값과 출력값을 정확하게 모사한다(Goldrick et al., 2015).
IndPenSim은 여러 가지 운전 모드로 동작할 수 있어, 대량의 현실적인 발효 데이터를 생성할 수 있다.
또한 이 시뮬레이션은 다음과 같은 요소들을 포함함으로써 실제 공정을 현실감 있게 재현한다.
- 오프라인 분석 측정값의 시간 지연    
- 공급 전략에 대한 작업자의 수동 개입    
- 부정확한 센서 측정값    
- 성장 및 생산 수준의 무작위 편차    
더 나아가, 현실적인 **Raman spectroscopy 장치**가 IndPenSim 내부에 통합되었다.
이 장치의 도입 목적은 바이오의약품 제조시설에서 현재와 미래의 혁신적이고 고도화된 공정 제어 전략 개발을 지원하기 위함이다.
또한 약 100개 배치(약 2.5 GB)를 포함하는 데이터셋이 `www.industrialpenicillinsimulation.com`에서 다운로드 가능하며, 이는 빅데이터 분석, 머신러닝(ML), 인공지능(AI) 접근법을 위한 가치 있는 자원으로 활용되는 것을 목표로 한다.

### 1.1. Overview of IndPenSim
IndPenSim은 독립 실행형 애플리케이션으로 동작하며, `www.industrialpenicillinsimulation.com`에서 무료로 다운로드할 수 있다.
IndPenSim에서 기록되는 모든 공정 입력값과 출력값의 개요는 Fig. 1에 제시되어 있다. 또한 Table 1에서는 주요 공정 변수들의 측정 주기와 기본 제어 전략, 그리고 변수들 사이의 기능적 관계를 설명하고 있다.
자동 제어 변수들, 즉:
- 온도(T)    
- pH    
는 피드백 기반의 **PID(Proportional-Integral-Derivative) 제어 루프**를 사용하여 조절된다.
반면 수동 제어 변수들인:
- substrate flowrate(Fs)    
- 페닐아세트산 유량(FPAA)    
은 레시피 기반(recipe driven) 방식으로 조작된다.
이 방식은 다음 두 형태로 운전될 수 있다.

|제어 방식|설명|
|---|---|
|Recipe driven|배치 전체 동안 고정된 프로파일을 따름|
|Operator dependant|작업자가 배치 중간에 프로파일을 수동 조정|

이러한 제어 모드는 Goldrick et al. (2015)에서 설명된 것처럼, 작업자가 배치 운전 중 Fs와 FPAA를 수동으로 조절하는 실제 공정 동작을 재현한다.
배치 길이(batch length)는 다음 두 방식 중 하나로 설정될 수 있다.

|배치 길이 방식|설명|
|---|---|
|Fixed|일반적으로 230시간으로 고정|
|Variable|후공정(downstream process) 지연 상황에 따라 달라짐|

IndPenSim이 생성한 연간 생산 지표를 요약한 5년간의 캠페인 결과는 Table 2에 정리되어 있다.
각 캠페인은 서로 다른 운전 모드로 수행되었으며, 어떤 캠페인에서도 고급 제어 알고리즘(APC)은 적용되지 않았다.
IndPenSim은 다음 가정을 기반으로 연간 생산 지표를 계산한다.
- 공장은 하루 24시간 운영    
- 연간 336일 가동    
	- 남은 29일은 정기 유지보수를 위한 연간 셧다운 기간으로 사용된다.

또한 각 배치 이후에는:
- 바이오리액터 세척    
- 재접종(reinoculation)  
을 위해 3일의 turnaround 기간이 필요하다.
각 배치에서는 2000 kg의 페니실린 생산 수율을 목표로 하며, 이 기준 이하의 수율을 달성한 배치는 목표 미달(batch below target)로 간주된다.
이 경우 해당 배치의 성능 저하 원인에 대한 조사가 필요하다.

### 1.2. IndPenSim control objectives
IndPenSim은 대규모 _Penicillium chrysogenum_ 발효 공정의:
- 성장(growth)
- 형태학적 변화(morphology)
- 대사산물 생성(metabolic production)
- 퇴화(degeneration)
를 고려하며, 동시에 필요한 모든 온라인 및 오프라인 공정 변수들을 모델링한다.

이 모델의 수학적 구조에 대한 상세 내용은 Goldrick et al. (2015)에서 이미 설명되었다.
이 논문의 주요 목적은, 이 시뮬레이션이 바이오의약품 공정에 적용 가능한 새로운 제어 솔루션의 개발과 검증을 위한 벤치마크 역할을 수행할 수 있음을 보여주는 데 있다.
현재 이 발효 공정에는 고급 공정 제어(APC) 전략이 적용되어 있지 않으며, 따라서 공정 개선의 여지가 매우 크다.
모든 제어 전략의 궁극적인 목표는 일반적으로:
- 생산 수율 증가
- 운영 비용 감소
를 통해 경제적으로 타당한 공정을 확보하는 것이다(Montague et al., 1989).
따라서 다음과 같은 제어 목표(control objectives)가 정의되었다.
- Table 2에 제시된 5개 캠페인과 비교하여, **연간 페니실린 생산량을 최대화**하고 **배치별 수율 변동을 줄이는 제어 전략**을 개발한다.    
- 페니실린 생산에 영향을 미치는 **중요 공정 변수(CPPs, Critical Process Parameters)**와 **중요 품질 특성(CQAs, Critical Quality Attributes)** 을 식별한다.    
- 기존 **PID 제어 루프**와 비교하여 pH와 온도 변수의 변동을 최소화할 수 있는 **개선된 제어 전략**을 개발한다.    
- Table 1에 정의된 허용 범위 내에서 변수를 유지하기 위해, 다음 유량 중 하나 이상을 조작하는 제어 전략을 개발한다.    
    - 기질 유량(substrate flowrate)        
    - 질소 유량(nitrogen flowrate)        
    - 페닐아세트산 유량(phenylacetic acid flowrate)        
- Raman spectroscopy 장치로 기록된 스펙트럼을 활용하여, 페닐아세트산, 바이오매스 또는 페니실린 농도를 실시간 온라인 예측할 수 있는 **소프트 센서(soft-sensor)** 를 개발한다.    
- 연간 캠페인 전체에서 생성되는 페니실린 수율을 최대화하기 위해, 각 배치의 **최적 수확 시점(optimum harvest time)** 을 계산하는 제어 전략을 개발한다.

#### Table 1
![[Pasted image 20260515224437.png]]

이 표는 IndPenSim 공정에서 사용하는 주요 변수들에 대해:
- 얼마나 자주 측정하는지    
- 무엇으로 제어하는지    
- 어떤 변수들과 관련되는지    
- 목표 제어 전략이 무엇인지를 정리한 표입니다.

표 제목:

> Summary of measurement frequency, primary control variables, functional relationships and control strategies for recorded process variables

즉:

> “기록되는 공정 변수들의 측정 주기, 주요 제어 변수, 기능적 관계, 제어 전략 요약”


---

##### 표의 각 컬럼 의미

|컬럼|의미|
|---|---|
|Variable reference|공정 변수|
|Measurement frequency|측정 주기|
|Primary control variables|해당 변수에 영향을 주는 주요 조작 변수|
|Functional relationship|수학 모델에서 관련되는 변수|
|Control strategy|목표 제어 전략|

---
##### 변수별 설명

---

###### 1. Dissolved oxygen (DO₂)

|항목|내용|
|---|---|
|변수|용존산소|
|단위|mg/L|
|측정주기|12분|
|제어변수|`Fg`, `RPM`|
|전략|포화도의 10% 이상 유지|
###### 의미
발효조 안의 산소 농도입니다.
산소가 부족하면 균이 제대로 성장하지 못합니다.
###### 제어 방법

| 변수    | 의미       |
| ----- | -------- |
| `Fg`  | 공기 공급 유량 |
| `RPM` | 교반기 속도   |
공기를 더 넣거나 교반 속도를 높여 산소 전달을 증가시킵니다.

---
###### 2. Weight (W)

|항목|내용|
|---|---|
|변수|배양액 무게|
|단위|kg|
|측정주기|12분|
|제어전략|7×10⁴ ~ 11×10⁴ kg 유지|
###### 의미
발효조 내부 총 질량입니다.
공급(feed) 유량이 너무 많거나 증발이 많으면 변합니다.

---
###### 3. pH

|항목|내용|
|---|---|
|측정주기|12분|
|제어변수|`Fa/b`|
|전략|PID 제어|

###### 의미

산도 조절입니다.

###### 제어 변수

|변수|의미|
|---|---|
|`Fa/b`|산(acid)/염기(base) 투입|

PID controller가 자동으로 산·염기 투입량을 조절합니다.

---

###### 4. Temperature (T)

|항목|내용|
|---|---|
|측정주기|12분|
|제어변수|`Fc`|
|전략|PID 제어|

###### 의미
발효 온도입니다.

###### 제어 변수

|변수|의미|
|---|---|
|`Fc`|냉각수 유량|
냉각수를 조절하여 온도를 유지합니다.

---

###### 5. Off-gas measurements

|항목|내용|
|---|---|
|변수|배출가스 CO₂/O₂|
|측정주기|12분|
|제어전략|제어 안함|

###### 의미
균의 호흡 상태를 간접적으로 보여주는 변수입니다.
산소 소비와 CO₂ 생성량을 확인합니다.

---

###### 6. Penicillin (P)

|항목|내용|
|---|---|
|측정주기|12시간 (+4일 지연)|
|전략|생산량 최대화|

###### 매우 중요

오프라인 분석 결과가 실제로는:

```text
12시간 측정 간격 + 4일 분석 지연
```

이 있다는 뜻입니다.
즉 공정 중 즉시 값을 알 수 없습니다.
→ 이것이 soft sensor/PAT가 필요한 이유입니다.

---

###### 7. Biomass (X)

|항목|내용|
|---|---|
|변수|균체량|
|전략|생산 최대화|

균이 얼마나 성장했는지를 의미합니다.

---

###### 8. Phenylacetic acid (PAA)

|항목|내용|
|---|---|
|전략|600~1800 mg/L 유지|

###### 중요 변수

PAA는 페니실린 precursor입니다.
너무 적으면 생산이 감소하고,  
너무 많으면 균에 독성이 생길 수 있습니다.
그래서 범위 유지가 중요합니다.

---

###### 9. Nitrogen (N)

|항목|내용|
|---|---|
|전략|300 mg/L 이상 유지|

질소원 부족을 방지하기 위한 조건입니다.

---

###### 10. Viscosity (μ)

|항목|내용|
|---|---|
|전략|100 cP 이하 유지|

점도가 너무 높으면:
- 산소 전달 감소    
- 교반 어려움    
- mixing 불량    
문제가 발생합니다.

---

###### 11. Substrate (S)

|항목|내용|
|---|---|
|전략|일정 범위 유지|

균의 탄소원(substrate) 농도입니다.
너무 적으면 성장 저하,  
너무 많으면 대사 이상이 생깁니다.

---

##### 이 표의 핵심 의미

이 표는 사실상:

> “IndPenSim에서 무엇을 제어 문제(control problem)로 삼고 있는가?”

를 보여주는 표입니다.
특히 핵심은:

|핵심 문제|의미|
|---|---|
|측정 지연|Penicillin/PAA/Biomass는 실시간 측정 불가|
|수동 제어|Feed 조절이 작업자 의존적|
|다변수 공정|변수들이 서로 강하게 연결됨|
|목적|생산량 최대화 + 변동 최소화|

입니다.

그래서 논문에서:
- PAT    
- Raman spectroscopy    
- Soft sensor    
- ML/AI    
- APC    
를 도입하려는 이유가 여기서 나옵니다.

#### Table 2
이 표는 IndPenSim을 서로 다른 제어 방식으로 5년 동안 운전했을 때의 연간 생산 성능을 비교한 표입니다.
![[Pasted image 20260623135514.png]]
##### 표 제목:

> A summary of the annual production metrics recorded by IndPenSim operated using different control strategies throughout a five-year production period.

즉:

> “5년 생산 기간 동안 서로 다른 제어 전략으로 운전한 IndPenSim의 연간 생산 성능 요약”

입니다.

---

##### 표의 핵심 목적

이 표는 사실상:

> “현재 제어 방식이 얼마나 비효율적인가?”  
> 그리고  
> “왜 APC/PAT/ML 기반 제어가 필요한가?”

를 보여주기 위한 baseline(기준 성능) 표입니다.

---

###### 컬럼 구조

각 컬럼은 서로 다른 생산 캠페인입니다.

|컬럼|의미|
|---|---|
|Campaign 1|1년차 운전|
|Campaign 2|2년차 운전|
|Campaign 3|3년차 운전|
|Campaign 4|4년차 운전|
|Campaign 5|5년차 운전|

---

##### 각 행 설명

###### 1. Control strategy

|캠페인|제어 방식|
|---|---|
|1|Operator dependant|
|2|Recipe driven|
|3|Operator dependant|
|4|Recipe driven|
|5|Operator dependant|

###### 의미

|방식|의미|
|---|---|
|Operator dependant|작업자가 중간중간 feed를 수동 조정|
|Recipe driven|고정 레시피대로 자동 진행|

즉 현실 공장처럼:
- 어떤 해는 작업자 경험 의존    
- 어떤 해는 고정 recipe 운전    
을 모사한 것입니다.

---

###### 2. Fixed or variable batch length

|종류|의미|
|---|---|
|Fixed|항상 230시간|
|Variable|상황에 따라 batch 종료시간 달라짐|

###### 의미

실제 공장은 downstream 공정 지연 때문에:
- 어떤 batch는 더 오래 돌고    
- 어떤 batch는 빨리 끝납니다.  
IndPenSim도 이를 반영합니다.

---

###### 3. Average batch length (hours)

예시:

```text
239 ± 27
```

의 의미:

|값|의미|
|---|---|
|239|평균 batch 시간|
|±27|batch 간 편차|
즉 batch 길이 variability를 의미합니다.

---

###### 4. Number of batches

|캠페인|batch 수|
|---|---|
|대부분|26|
|Year 2|25|

###### 왜 차이가 나는가?

Batch가 길어지면:

```text
1년 동안 batch 횟수 감소
```

합니다.

즉:
- 공정 효율 감소    
- annual 생산량 감소
로 이어집니다.

---

###### 5. Number of below target batches

매우 중요한 지표입니다.
예시:

|Year|목표 미달 배치|
|---|---|
|1|2|
|2|8|
|3|6|
|4|2|
|5|5|

###### 의미

논문에서 목표 수율은:

```text
2000 kg penicillin / batch
```

입니다.

그 이하 생산 batch는 실패 batch로 간주합니다.

즉:

|값이 크다|의미|
|---|---|
|생산 변동성 큼|batch마다 생산량 차이가 큼|
|공정 안정성 낮음|공정 결과가 일정하지 않음|
|operator 의존성 큼|작업자 숙련도 영향이 큼|
|경제성 나쁨|생산 효율과 수익성이 떨어짐|



입니다.

특히 Campaign 2는:

```text
8개 batch 실패
```

→ 상당히 불안정한 공정입니다.

---

###### 6. Average Penicillin yield per batch

예시:

```text
2882 ± 745 kg
```

###### 의미

|값|의미|
|---|---|
|2882|평균 생산량|
|±745|batch variability|

###### 중요 포인트

표준편차가 매우 큽니다.

즉:

```text
batch마다 생산량 차이가 큼
```

을 의미합니다.

이것이 바이오공정의 대표 문제입니다.

---

###### 7. Annual production

연간 총 생산량입니다.
단위:

```text
kg × 10^3
```

즉:

```text
74,939
=
74,939,000 kg
```

입니다.

---

###### 표 전체의 핵심 해석

이 표가 보여주는 핵심은:

|문제|의미|
|---|---|
|Batch variability 큼|생산 일관성 부족|
|Below-target batch 많음|공정 안정성 부족|
|Operator dependent|사람 경험 의존|
|Variable batch length|downstream 영향 큼|
|수율 편차 큼|경제성 저하|

입니다.

즉 현재 공정은:

```text
“제어 최적화가 충분히 안 된 상태”
```

라는 것을 보여줍니다.

---

###### 논문의 진짜 목적

그래서 논문이 하려는 것은:

|목표|사용 기술|
|---|---|
|생산량 증가|APC|
|Batch variability 감소|ML/AI|
|실시간 예측|Raman + soft sensor|
|자동 최적화|PAT|
|최적 harvest|predictive control|

입니다.

즉 이 표는:

> “기존 공정은 이 정도 수준인데,  
> 새로운 control strategy를 쓰면 얼마나 개선될 수 있는가?”

를 비교하기 위한 baseline 데이터입니다.


### 2. 재료 및 방법(Materials and Methods)

#### 2.1 시뮬레이션 소프트웨어

IndPenSim은 **MATLAB R2018b**로 작성되었으며, `www.industrialpenicillinsimulation.com`에서 무료로 다운로드할 수 있다. 또한 Table 2에 제시된 Campaign 1~5의 과거 배치 데이터도 함께 제공된다.

IndPenSim은 다음과 같은 기능과 특성을 제공한다.

- 바이오매스 농도와 페니실린 농도에 대해 **배치 간(batch-to-batch) 변동성**뿐만 아니라 **동일 배치 내(in-batch) 변동성**도 모사할 수 있다.    
- 기질(substrate, (c_s)), 오일((c_{oil})), 산·염기 몰농도((c_{a/b})), 페닐아세트산(PAA, (c_{PAA}))의 **유입 농도에 교란(disturbance)** 을 추가할 수 있다.    
- 현재 사용 중인 순차적 배치 제어 전략에서 다음 조작 변수들을 사용자가 변경할 수 있다.    
    - 기질 공급 유량 ($F_s$)        
    - 오일 공급 유량 ($F_{oil}$)
    - 공기 공급 유량 ($F_g$)        
    - 교반 속도 (RPM)        
    - 배출 유량 ($F_{dis}$)      
    - 페닐아세트산 공급 유량 ($F_{PAA}$)        
- 다음과 같은 조건에서 성장률 저해(inhibition) 효과를 포함할 수 있다.    
    - 용존산소(DO₂) 부족        
    - 질소(N) 부족        
    - 페닐아세트산(PAA) 부족        
    - 과도한 PAA 농도        
    - 과도한 CO₂ 농도        
    - 비최적 온도(T)        
    - 비최적 pH        
- 다음 오프라인 분석 항목에 대해 **사전에 정의된 4시간의 측정 지연(delay)** 을 포함한다.    
    - 페니실린(P)        
    - 질소(N)        
    - 페닐아세트산(PAA)        
    - 점도$(\mu_{app})$        
- 다음과 같은 공정 이상(Process Fault)을 포함할 수 있다.    
    - 교반기 정지(agitator trip)        
    - 공기 공급 이상(aeration fault)        
    - 기질 공급 이상(substrate fault)        
    - 센서 오류(sensor error)        
- 배치 전 과정에 걸쳐 **Raman 스펙트럼**을 기록할 수 있으며, 이를 통해 실시간으로 중요품질특성(CQA, Critical Quality Attributes)과 중요공정변수(CPP, Critical Process Parameters)를 예측할 수 있다. 단, 이를 위해서는 정확한 보정 모델(calibration model)이 개발되어 있어야 하며, 스펙트럼 전처리(pre-processing)가 적절하게 수행되어야 한다.

### 2.2 Raman Spectroscopy 시뮬레이션 개발

이 절에서는 실제적인 **PAT(Process Analytical Technology) 분석기**, 특히 **Raman 분광기(Raman spectroscopy device)**를 모사하기 위한 경험적 수학 모델(empirical mathematical model)의 개발 과정을 설명한다.
시뮬레이션된 Raman 스펙트럼은 시판 항생제를 생산하는 **5 L 규모의 진균 발효(fungal fermentation)** 공정에서 측정된 실제 Raman 스펙트럼을 상세하게 분석하여 생성하고 검증하였다.
이 발효 공정의 재료 및 실험 방법에 대한 자세한 내용은 Goldrick et al. (2018)에 기술되어 있다.
사용된 Raman 분광기는 **Kaiser 1000 RXN 시스템**으로, 다음과 같은 사양을 갖는다.
- InGaAs(Indium Gallium Arsenide) 검출기 배열 사용    
- 측정 파수 범위: 200~2400 cm⁻¹    
- 분해능(resolution): 3 cm⁻¹    

Raman 분석기는 다음 조건으로 설정되었다.
- 30분마다 스펙트럼 1회 측정    
- 각 스펙트럼은 9회 평균(averaging)    
- 적분 시간(integration time): 180초    

260시간의 발효 과정 동안 총 **540개의 Raman 스펙트럼**이 측정되었으며, 그 결과는 Fig. 2A에 제시되어 있다.
본 연구에서 개발한 시뮬레이션 PAT 분석기는 실제 측정된 Raman 스펙트럼의 주요 특징을 재현하는 것을 목표로 한다.
Bocklitz et al. (2011)에 따르면 Raman 스펙트럼은 다음 세 가지 주요 특성으로 구성된다.
- 형광(fluorescence)에 의한 베이스라인 상승(baseline increase)    
- Raman 스펙트럼 피크(Raman spectrum peaks)    
- 측정 잡음(noise)    

한편 Raman 측정에서 간혹 발생하는 무작위 **Cosmic Spike(우주선 잡음에 의한 이상 피크)** 는 본 연구의 모델링 대상에 포함되지 않았다.

#### 참고
논문에서는 실제 Raman 스펙트럼을 다음과 같이 모델링한 것이다.
$$\text{Spectrum} = \text{Baseline} + \text{Raman Peaks} + \text{Noise}$$
- Baseline = 형광 배경 신호
- Raman Peaks = 실제 화학 성분 정보
- Noise = 측정 오차


Cosmic Spike는 보통 다음과 같은 형태를 가진다.

```
정상 스펙트럼
─────┬─────
     │     
     │
	 ▲ 매우 큰 단일 피크
```

이는 실제 Raman 데이터 전처리 단계에서 제거하는 경우가 많기 때문에 시뮬레이션에는 포함하지 않았다.

### 2.2.1 비선형 스펙트럼 형태와 형광(Fluorescence) 베이스라인 증가

발효 공정에서 측정되는 Raman 스펙트럼은 배지 성분과 세포 배양에 의해 생성되는 특징적인 피크뿐만 아니라, Raman 분광기 자체의 배경 신호에 의해 발생하는 특유의 비선형 형태를 포함하고 있다.

연구진은 이러한 특성을 모델링하기 위해 실험적으로 측정한 Raman 데이터셋의 첫 번째 스펙트럼을 기준 스펙트럼(reference spectrum)으로 사용하였다. 이 기준 스펙트럼은 시뮬레이션 PAT 분석기가 생성하는 모든 Raman 스펙트럼의 템플릿 역할을 하며, Fig. 2B에 제시되어 있다.

실험 Raman 스펙트럼에서 관찰되는 형광 증가(fluorescence increase)는 Fig. 2A에서 확인할 수 있다. 발효 초기(0~45시간)에 측정된 스펙트럼과 발효 말기(215~240시간)에 측정된 스펙트럼을 비교하면, 시간이 지남에 따라 전체 베이스라인 강도가 증가하는 것을 볼 수 있다.

실험 스펙트럼의 형광 증가량 ((\Delta Fluorescence_{Exp}))을 모델링하기 위해, 연구진은 연속된 두 스펙트럼 사이의 평균 강도 변화량을 다음과 같이 계산하였다.

$$  
\Delta Fluorescence_{Exp}(n)=\sum_{v=250}^{2250}
\frac{\left(  
Spectra(n+1)-Spectra(n)  
\right)}  
{2000}  
$$

여기서 $\Delta Fluorescence_{Exp}$는 250~2250 cm⁻¹ 구간에서 두 연속 스펙트럼 사이의 평균 베이스라인 강도 변화량을 의미한다.
계산된 형광 증가량을 누적합(cumulative sum)하면 발효 과정 전체의 평균 형광 프로파일을 얻을 수 있다.
시뮬레이션 Raman 스펙트럼에서는 형광 증가 ($\Delta Fluorescence_{Sim}$)가 발효액 조성의 변화에 의해 발생한다고 가정하였다.
연구진은 다음 네 가지 변수가 형광 증가에 가장 큰 영향을 준다고 가정하였다.
- 바이오매스 농도 (Biomass, (X))    
- 페니실린 농도 (Penicillin, (P))    
- 점도 (Viscosity, (\mu))    
- 배양 시간 (Batch time, (t))
이를 다음과 같은 식으로 표현하였다.

$$
\sum_{t=0}^{240}  
\Delta Fluorescence_{Sim}=
\alpha_1 X  +  
\alpha_2 P  +  
\alpha_3 \mu +  
\alpha_4 t  
$$

계수 $\alpha_1, \alpha_2, \alpha_3, \alpha_4$는 단계적 선형회귀(step-wise linear regression)를 이용하여 추정하였다.
회귀분석의 목적은 실험적으로 계산된 형광 증가량과 시뮬레이션 형광 증가량의 차이를 최소화하는 것이었다.
분석 결과 형광 증가는 위 네 변수만으로도 충분히 설명될 수 있었으며, 특히 **페니실린 농도(P)** 가 실제 형광 증가에 가장 큰 영향을 미치는 변수로 확인되었다.
최종적으로 얻어진 회귀계수는 다음과 같다.

| 변수                |     계수 |
| ----------------- | -----: |
| Biomass ($X$)     | -0.002 |
| Penicillin ($P$)  |   1.05 |
| Viscosity ($\mu$) |  -0.07 |
| Time ($t$)        |  -0.20 |

또한 Fig. 2A를 통해 형광 효과가 모든 파수 영역에 동일하게 나타나지 않는다는 점이 관찰되었다.
구체적으로는,
- 낮은 파수 영역(low wavenumbers)에서는 형광 영향이 큼    
- 높은 파수 영역(high wavenumbers)에서는 형광 영향이 상대적으로 작음
을 확인할 수 있었다.
따라서 연구진은 이러한 비선형성을 반영하기 위해 각 스펙트럼에 지수함수(exponential function)를 곱하는 방식을 사용하였다. 논문에서는 이 지수함수를 $\beta$로 정의하였으며, 이를 통해 실제 Raman 스펙트럼에서 관찰되는 파수별 형광 효과를 재현하였다.
$\beta$ 함수의 구체적인 형태는 논문 후반의 식 (5)에 제시되어 있으며, 보다 자세한 설명은 Goldrick (2015)에 기술되어 있다.

![[Pasted image 20260623141823.png]]
**Fig. 2. Raman spectroscopy 시뮬레이션 개발 과정 요약**
**A)**  993 nm Raman 분광기를 이용하여 실제 발효 공정에서 측정한 실험 Raman 스펙트럼을 나타낸다.
**B)**  본 시뮬레이션의 시작 스펙트럼으로 사용된 비선형 기준 스펙트럼(non-linear reference spectrum)을 나타낸다.
**C)**  발효 과정에서의 조성 변화(compositional changes), 특히 **페니실린(penicillin)**, **기질(substrate)** 및 **페닐아세트산(phenylacetic acid)** 농도 변화와 관련된 비선형 특성 피크(non-linear characteristic peak)의 증가를 나타낸다.
**D)**  각 시뮬레이션 Raman 스펙트럼에 추가된 전형적인 잡음(noise)의 예를 보여준다.
**E)**  본 연구에서 개발된 최종 시뮬레이션 Raman 스펙트럼의 예시를 보여준다.

### 2.2.2 발효 조성과 관련된 비선형 특성 피크 증가

시뮬레이션된 Raman 스펙트럼은 배치(batch) 과정 동안 발생하는 성분 농도 변화와 관련된 **특성 피크(characteristic peaks)** 를 반영해야 한다.

생물학적 공정의 온라인 모니터링을 위한 Raman 분광법 연구에서는 이러한 특성 피크를 **가우시안 함수(Gaussian function)** 로 모델링한 바 있다(Oh et al., 2012).

또한 Raman 분광법을 이용한 화학 분석 분야에서도 가우시안 함수가 특정 분자를 표현하는 데 적합함이 보고되었다(Kneipp et al., 1999).

따라서 본 시뮬레이션에서는 다음 성분들의 농도를 표현하기 위해 가우시안 함수를 사용하였다.

- 기질(Substrate, S)
    
- 페니실린(Penicillin, P)
    
- 페닐아세트산(Phenylacetic Acid, PAA)
    

---

기질과 페닐아세트산의 피크 위치는 Goldrick (2015)에서 설명된 바와 같이, 기질과 페닐아세트산을 고농도로 첨가(spiking)한 배지의 Raman 스펙트럼을 분석하여 결정하였다.

한편 페니실린 피크의 위치는 Clarke et al. (2005)에 제시된 Penicillin G 시료의 Raman 스펙트럼을 바탕으로 선정하였다.

---

이들 피크는 다음과 같은 가우시안 분포 함수로 표현하였다.
$$  
f\bigl(Peak_{(P/S/PAA)\bigr)}=
\frac{1}{\sqrt{2\pi\sigma^2}}  
\exp^{-\frac{\left(Peak(P/S/PAA)-\mu_{P/S/PAA}\right)^2 }  
{2\sigma^2}  }
$$

여기서,
- (Peak(P/S/PAA)) : 페니실린(P), 기질(S), 또는 페닐아세트산(PAA)의 농도 변화와 관련된 특정 Raman 파수(wavenumber)    
- (\sigma) : 해당 피크의 표준편차(peak width)    
- (\mu) : 피크 중심 위치(peak mean)
를 의미한다.
즉 각 화학성분은 Raman 스펙트럼 상의 특정 위치에 종(bell) 모양의 가우시안 피크로 표현되도록 모델링하였다.
이렇게 생성된 성분별 Raman 피크는 Fig. 2C에 제시되어 있다.


### 2.2.3 신호 대 잡음비(Signal-to-Noise Ratio, SNR)

잡음(noise)은 모든 센서에 내재적으로 존재하는 교란 요인이다. Raman 분광법에서 잡음은 일반적으로 열적 효과(thermal effects), 장비의 신호 판독 오류(instrument read-out errors), 또는 무작위 우주선(cosmic ray) 신호에 의해 발생한다.

본 연구에서는 스펙트럼의 **신호 대 잡음비(SNR, Signal-to-Noise Ratio)** 를 계산하여 잡음의 크기를 모델링하였다.

SNR 계산은 다음과 같은 가정에 기반한다.

> 매우 짧은 시간 간격으로 연속 측정된 Raman 스펙트럼은 거의 동일해야 하며, 두 스펙트럼 간 차이의 대부분은 신호 내에 존재하는 잡음 때문이라는 가정이다(Grimbergen et al., 2010).

연속된 스펙트럼의 평균값과 표준편차를 이용하여 SNR을 다음과 같이 계산하였다.

$$
SNR = \frac{\bar{S}}{\sigma_{diff}}  
$$

여기서,
- (\bar{S}) : Raman 스펙트럼의 평균 강도(mean Raman intensity)    
- (\sigma_{diff}) : 두 연속 스펙트럼 차이의 표준편차를 (\sqrt{2})로 나눈 값    

을 의미한다.
10개의 스펙트럼에 대해 SNR을 계산한 결과, 약 **50 counts (intensity)** 로 나타났다.
연구진은 이 값을 이용하여 **Random Walk 방식의 잡음 생성 모델**을 통해 각 시뮬레이션 Raman 스펙트럼에 잡음을 추가하였다. 각 스펙트럼에 추가된 전형적인 잡음의 예는 Fig. 2D에 제시되어 있다.

최종적으로 생성된 시뮬레이션 Raman 스펙트럼(Sim. Spectra)은 다음과 같이 표현된다.

$$
\text{Sim. Spectra}=
\text{Reference Spectra}  +  
\left(\delta_1 \Delta Fluorescence  +  
\delta_2 Peaks(S,P,PAA)  +  
\delta_3 Noise  \right)  
\times \beta  
$$

여기서 (\delta_1), (\delta_2), (\delta_3)는 시뮬레이션 Raman 스펙트럼을 구성하는 각 요소의 강도(intensity)를 조절하는 계수이다.
- (\delta_1) : 바이오매스, 페니실린, 점도 및 배양시간 변화에 따른 형광(Fluorescence) 증가량    
- (\delta_2) : 바이오리액터 내 현재 농도에 따른 Penicillin(P), Substrate(S), Phenylacetic Acid(PAA) 피크 강도    
- (\delta_3) : 각 스펙트럼에 추가되는 잡음의 강도    
- (\beta) : 낮은 파수 영역에서 더 크게 나타나는 비선형 형광 증가를 반영하기 위한 지수함수

### Raman 시뮬레이션의 검증

개발된 Raman 스펙트럼이 정상 운전 및 이상 운전 조건 모두에서 페니실린 농도를 정확하게 예측할 수 있는지를 Fig. 3에서 검증하였다.

총 4개의 배치를 시뮬레이션하였으며, Fig. 3A와 같이 실제 공정의 변동성을 모사하기 위해 기질 공급 유량((F_s))에 저주파 필터가 적용된 **의사난수 이진신호(PRBS, Pseudo Random Binary Signal)** 를 추가하였다.

첫 번째 배치는 PLS(Partial Least Squares) 모델 구축에 사용되었다.

- 입력(X): Raman 스펙트럼 데이터
    
- 출력(Y): 보간(interpolation)된 오프라인 Penicillin 농도
    

스펙트럼 전처리는 Section 4에 기술된 방법을 적용하였다.

PLS 모델은 최적 잠재변수(latent variable)를 4개로 선택하였으며,

- X 데이터(스펙트럼)의 분산 99%
    
- Y 데이터(보간된 Penicillin 농도)의 분산 98%
    

를 설명하였다.

---

이후 검정용 배치(calibration batch)를 시뮬레이션한 결과, PLS 모델은 오프라인 측정 Penicillin 농도와 매우 유사한 예측 결과를 보였다.

예측 오차는$RMSE = \pm 0.1\; g/L$수준이었다.

추가로 두 개의 배치에 대해서는 Fig. 3A와 같이 기질 공급 유량((F_s))에 공정 교란을 발생시켰다.

그 결과 Fig. 3B에서 볼 수 있듯이 Penicillin 농도가 감소하였으며, PLS 모델은 이러한 이상 상황에서도 오프라인 Penicillin 측정값과 매우 유사한 예측 성능을 나타냈다.

---

정상 운전과 이상 운전 모두에서 Raman 스펙트럼을 이용하여 Penicillin 농도를 실시간으로 추정할 수 있다는 점은, 본 벤치마크 시뮬레이션에서 **고급 공정 제어(APC, Advanced Process Control)** 알고리즘을 개발하고 적용할 수 있는 중요한 가능성을 보여준다.

다만 저자들은 다음과 같은 한계를 명시하였다.

> 본 연구의 Raman 시뮬레이션은 5 L 규모 발효기에서 획득한 Raman 스펙트럼을 기반으로 개발되었으며, 실제 100,000 L 산업 규모 발효조에서 발생할 수 있는 공정 불균일성(process heterogeneity)이나 기타 규모 확대(scale-up) 문제는 반영하지 못한다.

따라서 IndPenSim의 Raman 데이터는 매우 현실적이지만, 완전한 산업 규모 Raman 측정 데이터를 그대로 재현한 것은 아니라는 점을 고려해야 한다.

