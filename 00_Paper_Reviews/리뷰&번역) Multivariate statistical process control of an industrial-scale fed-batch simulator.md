
# 산업 규모 유가식(fed-batch) 시뮬레이터의 다변량 통계적 공정 관리 (Multivariate statistical process control of an industrial-scale fed-batch simulator)

**출처:** _Computers and Chemical Engineering_ 132 (2020) 106620 저널 홈페이지: www.elsevier.com/locate/compchemeng DOI: https://doi.org/10.1016/j.compchemeng.2019.106620

---

## 저자

**Carlos A. Duran-Villalobos** ᵃ,*, **Stephen Goldrick** ᵇ, **Barry Lennox** ᵃ

ᵃ 전기전자공학부(School of Electrical and Electronic Engineering), 맨체스터 대학교(The University of Manchester), Manchester M13 9PL, UK ᵇ 생화학공학부(Department of Biochemical Engineering), 유니버시티 칼리지 런던(University College London), London WC1E 6BT, UK

* 교신저자. E-mail: carlos.duran@manchester.ac.uk (C.A. Duran-Villalobos), s.goldrick@ucl.ac.uk (S. Goldrick)

---

## 논문 정보 (Article info)

**논문 이력 (Article history)**

- 접수(Received): 2019년 4월 25일
- 수정(Revised): 2019년 10월 6일
- 채택(Accepted): 2019년 10월 21일
- 온라인 게재(Available online): 2019년 10월 24일

**키워드 (Keywords)**

- 최적 제어(Optimal control)
- 배치 대 배치 최적화(Batch to batch optimisation)
- 모델 예측 제어(Model predictive control)
- 데이터 기반 모델링(Data-driven modelling)
- 결측 데이터 방법(Missing data methods)
- 부분 최소제곱 회귀(Partial least square regression)

저작권: Crown Copyright © 2019 Published by Elsevier Ltd. 본 논문은 CC BY 라이선스(http://creativecommons.org/licenses/by/4.0/)에 따른 오픈 액세스 논문이다.

---

## 초록 (Abstract)

본 논문은 개선된 배치 대 배치(batch-to-batch) 최적화 기법을 제시하며, 이 기법이 한 배치에서 다음 배치로 넘어가면서 수율(yield)을 설정값(set-point)에 더 가깝게 접근시킬 수 있음을 보인다. 또한, 원료 물성의 무작위 변동과 배치 내 공정 변동으로 인해 발생하는 수율의 변동성을 여러 배치에 걸쳐 감소시키는 혁신적인 모델 예측 제어(Model Predictive Control, MPC) 기법을 제안한다. 제안된 제어기는 유효성 제약(validity constraints)을 사용하여, 공정의 적응형 다중경로 부분 최소제곱(adaptive multi-way partial least squares, MPLS) 모델을 개발하는 데 사용된 식별 데이터셋(identification dataset)이 기술하는 영역으로 의사결정 공간(decisional space)을 제한한다. 본 논문의 또 다른 기여는 모델 유효성에 부과된 경성 제약(hard constraints) 내에서 신뢰구간(confidence intervals)을 결정하기 위한 부트스트랩(bootstrap) 계산의 정식화이다. 제안된 제어 전략은 현실적인 산업 규모 유가식 페니실린 시뮬레이터에 적용되었으며, 명목 운전(nominal operation)과 비교했을 때 향상된 일관성과 수율을 제공하는 성능을 입증하였다.

---

## 1. 서론 (Introduction)

제약 산업에서 미국 식품의약국(Food and Drugs Agency, FDA)과 같은 규제 당국은 향상된 공정 관리를 통해 제품 품질을 개선하는 설계 기반 품질(Quality by Design, QbD)의 도입을 장려하고 있다(Yu et al., 2014). 최적 제어(optimal control) 전략은 제품의 변동성과 결함을 줄임으로써 제품 품질을 극대화할 수 있다.

제약 제품과 같은 특수 화학물질(specialty chemicals) 생산에서 이러한 전략을 구현하기 위해, Bonvin et al. (2006)에는 여러 접근법이 제시되어 있다. 이러한 접근법들은 정상 상태(steady state)의 부재와 강한 비선형 거동과 같이 산업 현장에서 흔히 발견되는 운영상의 문제를 다룬다. 추가적인 과제로는 제품 품질의 드물거나 지연된 온라인 측정(on-line measurements)이 있으며, 이는 대부분의 제약 공정에서 전형적으로 나타난다.

배치 운전을 개선하기 위해 다양한 모델링 접근법이 제안되어 왔으며, 여기에는 Birol et al., 2002 및 Goldrick et al. (2015)에서와 같은 기계론적 기반(mechanistic based) 접근법이 포함된다. 이들 연구에서 저자들은 서로 다른 페니실린 생산 사례 연구에서 최적의 유가식(fed-batch) 전략을 찾기 위해 제일원리 모델(first principle models)을 사용하였다. 또 다른 접근법은 배치 대 배치(Batch-to-Batch, B2B) 또는 런 대 런(run-to-run) 최적화라고 불린다. B2B는 한 배치에서 다음 배치로 조건을 조작하며, 그 목적은 경제적 비용 함수(economic cost function)를 점진적으로 증가시키거나 외란(disturbances)이 존재하는 상황에서 종점 품질(end-point quality)을 원하는 설정값에 더 가깝게 접근시키는 것이다. 최근 연구들은 산업적 응용에서 B2B를 사용하는 이점을 입증하였는데, 예를 들어 이 분야의 검토를 제공하는 (Liu et al., 2018)을 참조할 수 있다. 본 논문에서 제안하는 연구와 특히 관련이 있는 것은 Yabuki et al. (2000)의 연구로, 저자들은 지식 기반(knowledge-based) 접근법으로 개발된 예측 모델을 사용하여 최종 품질을 제어하기 위해 중간 보정(mid-correction) 정책을 사용하였다. 관련 연구로 Camacho et al. (2007)은 B2B 진화적 최적화(evolutionary optimization) 방법론을 제안하였으며, 이 방법론이 지식 기반 접근법과 비교했을 때 모의 발효(fermentation) 공정의 종점 품질을 유의하게 증가시킬 수 있음을 입증하였다. 그러나 외란의 거동이 배치마다 변화하는 경우, 공정의 종점 품질이 원하는 값을 만족하도록 보장하는 데에는 모델 예측 제어(model predictive control, MPC)가 더 효과적인 기법으로 나타났다(Flores-Cerrillo and MacGregor, 2003).

종점(end-point) 또는 런종점(run-end) MPC는 사용 가능한 온라인 측정값을 사용하여 배치 진행 중 일정한 간격으로 예상 종점 품질의 추정치를 제공한다. 그런 다음 제어기는 필요할 때마다 교정 조치(corrective action)를 적용하여 배치 종료 시 제품 품질이 목표를 달성하도록 보장한다. MPC가 적용하는 교정 조치는 조작 변수 궤적(manipulated variable trajectories, MVTs)의 조정이 될 것이다. 이러한 궤적은 현재 시점부터 배치의 예상 종점까지 조작될 수 있다. 화학공학 응용에 특별히 초점을 맞춘 MPC에 대한 광범위한 검토는 Kumar and Ahmad (2012)에 의해 보고되었다. 화학 공정 시스템에 대해 제안된 많은 MPC 전략이 있어 왔는데, 여기에는 품질 예측을 제공하기 위해 고전적인 상태공간 모델(state-space models)을 사용하는 것이 포함된다. 예를 들어 Sheng et al. (2002)이 제시한 논문에서 저자들은 샘플링이 비균일한(non-uniform) 시스템을 위한 새로운 일반화 예측 제어기(generalised predictive controller)를 제안하였다. 대안적인 접근법으로는 다변량 통계적 공정 관리(Multivariate Statistical Process Control, MSPC) 모델의 사용이 있으며, **그 예로 Flores-Cerrillo and MacGregor (2003)가 유화 중합(emulsion polymerization) 공정에서 입자 크기 분포(particle-size distribution)를 조절하기 위해 종점 제어기에 구현한 모델이 있다.**

MSPC는 다수의 센서 측정값에 담긴 정보를 소수의 복합 변수(composite variables)로 응축하려는 통계 기반 기법들의 집합을 지칭한다. 배치 제어 응용에서 다중경로 부분 최소제곱(Multi-way Partial Least Squares, MPLS)은 강력한 회귀 도구로 나타났으며, 적응형 기법(adaptive techniques)과 결합하면 제한된 양의 데이터만으로 배치 공정의 동적 특성에 대한 근사치를 제공하는 데 사용될 수 있다(Joe Qin, 1998). 예를 들어, Flores-Cerrillo and Macgregor (2004)는 축합 중합(condensation polymerization) 공정에 대해 MPLS 모델을 식별한 다음, 이를 비용 함수 내에서 사용하여 이차 계획법(Quadratic Programming, QP) 최적화 접근법으로 풀었을 때 공정의 일관성을 향상시키기 위해 MVT를 조정할 수 있음을 입증하였다. MPLS 모델을 사용하는 주된 장점은 모델의 잠재 변수 공간(latent variable space)에서 최적화가 이루어질 수 있어 계산 부담이 크게 줄어든다는 점이다. 유사한 접근법이 Wan et al. (2012)에 의해 배치 공정의 최종 품질 제어에 사용되었으나, 이들의 접근법은 또한 QP 문제에서 경성(hard) 및 연성(soft) 조작 변수 제약을 고려하고 외란 제거 제어(disturbance rejection control)를 적용하였다. 그들의 결과는 MPLS 기반 제어기 내의 외란 모델이 최종 품질을 향상시켰으며, 최적화 문제에서 조작 변수 제약을 포함시킴으로써 상한과 하한이 준수되도록 보장했음을 보여주었다. 제안된 제어 시스템의 한계는 QP 최적화 정식화 내에서 사용된 연성 제약(soft constraints)이 최종 품질 예측이 식별 데이터셋으로 정의된 스코어 공간(score space) 내에 유지되도록 튜닝(tuning)되어야 한다는 점이었다.

Laurí et al. (2013)은 발효 공정에 대한 종점 MPC 응용에서 경성 유효성 제약(hard validity constraints)의 포함으로부터 상당한 이점이 있음을 입증하였다. 이러한 제약은 제어기 비용 함수의 최적화 중에 MPLS 모델의 호텔링(Hotelling's) $T^2$ 및 제곱 예측 오차(Square Prediction Error, SPE)에 적용되어, 모델이 식별에 사용된 조건으로부터 너무 멀리 외삽(extrapolate)하지 않도록 보장하였다. 동일한 제약이 B2B 최적화 전략에 맞게 적응되어 (Duran-Villalobos et al., 2016)에서 B2B 최적화에 적용되었으며, 이는 Wan et al. (2012)이 제시한 제어 전략을 수정하고, 미래 MVT 변화의 '잠재(latent)' 공간으로의 투영 효과를 포함하면서 실공간(real space)에서 QP를 풀었다. 제어 전략에 이러한 항들을 추가함으로써 성능이 크게 향상되었다. 그러나 제약에 사용된 신뢰한계(confidence limits)(Laurí et al., 2013; Nomikos and Macgregor, 1995a,b; Ündey et al., 2003)는 명확하게 규정되지 않았으며, $T^2$와 SPE에 대해 각각 데이터가 정규 분포(normal distribution) 및 카이제곱 분포(chi-squared distribution)로 근사될 수 있다고 가정하였는데, 이는 특정 응용에서만 참이었다.

본 논문에서 제안하는 MPLS 기반 종점 제어 전략은 Duran-Villalobos et al. (2016)이 사용한 경성 유효성 제약에 적용되는 신뢰한계를 정의하며, 이는 유사한 제어 전략에서 사용될 때 제안된 제약과 관련하여 발생한 한계(Laurí et al., 2013; Nomikos and Macgregor, 1995a,b; Ündey et al., 2003)를 해결한다. 본 논문에서 제안하는 연구와 유사한 접근법(Flores-Cerrillo and MacGregor, 2005, 2004; Wan et al., 2012) 사이의 주요 차이점은, 현재 접근법이 한 배치에서 다음 배치로 모델을 개선하기 위해 적응형 기법을 사용하고, MVT 최적화가 스코어 공간이 아니라 실공간에서 풀린다는 점이다. 부록 A(Appendix A)는 이전 전략들의 결과를 제안된 접근법과 비교하여 보여준다.

MPLS 기반 종점 제어는 공정의 미래 진행이 추정될 것을 요구한다. 이를 달성하기 위해 제안된 다양한 접근법이 있으며, 결과적인 제어기의 정확도는 선택된 기법에 크게 의존한다. 공정 변수의 미래 추정치는 잠재 변수 공간에서 결정되며, 이를 위해 일반적으로 '결측 데이터(missing data)' 기법이 사용된다. 본 논문에서는 이러한 두 가지 기법의 능력을 비교하고, 다중 배치 실행의 조절을 위해 두 가지 제어 목표를 통합하는 새로운 접근법을 제안한다. 제안된 제어기의 능력은 산업용 페니실린 유가식 발효 공정의 벤치마크 시뮬레이션(Goldrick et al., 2015)을 사용하여 입증된다. 이전 연구들은 이 모의 공정에 결함 검출 및 진단(fault detection and diagnosis) 도구가 어떻게 적용될 수 있는지 입증하였다(Luo and Bao, 2018). 그러나 이 공정에 모델 기반 제어(model-based control) 기법을 적용한 연구는 없었다.

본 논문에서 제안하는 제어기의 두 가지 목표는 다음과 같다. 1. 주(primary) 조작 변수(글루코스 공급, glucose feed)에 대한 사전(a-priori) 궤적으로 시작하여, B2B 최적화 캠페인에서 최적의 최종 페니실린 농도(final penicillin concentration)에 도달하는 것; 2. MPC를 사용하여 배치 내에서 글루코스 공급 궤적을 조정함으로써 최종 페니실린 농도의 변동성을 줄이는 것.

본 논문의 구조는 다음과 같다. 산업용 페니실린 시뮬레이션과 운전 방법론의 개요는 2절에서 시작한다. MPLS 및 한 배치에서 다음 배치로의 식별과 적응은 3절에서 정의한다. 이후 두 가지 제어 목표는 4절에서 정식화하고, 비용 함수와 QP 해법은 5절에서 기술한다. 시뮬레이션에 적용된 B2B 최적화 및 종점 MPC 제어의 결과는 6절에서 제시하고 논의한다. 마지막으로 결론은 7절에 제공한다.

---

## 2. 사례 연구 (Case study)

산업 제어를 위한 대안 전략의 시험과 비교에 관하여, Bonvin (1998)은 현실적인 벤치마크(benchmarks)가 확실히 필요하며, 개발된 제어 전략은 과대 선전(oversold)되어서는 안 되고 오히려 파일럿 플랜트(pilot-plant)와 산업용 반응기에서 실험적으로 평가되어야 한다는 견해를 견지한다. 산업용 발효 공정의 현실적인 시뮬레이션의 주목할 만한 예는 Goldrick et al. (2015)에 제시되어 있다. 이 시뮬레이션(IndPenSim: www.industrialpenicillinsimulation.com)은 MATLAB에서 사용 가능하며, 산업 공정에서 수집한 데이터를 사용하여 검증된 페니실린 발효 공정의 복잡한 기계론적 모델을 기술한다. 그 산업 공정은 100,000 l 규모의 생물반응기(bioreactor)로, _Penicillium chrysogenum_ 균주(strain)를 생산하였다.

본 논문에서 기술한 B2B 및 MPC 캠페인 모두에 사용된 주요 시뮬레이션 매개변수는 표 1(Table 1)에 제공되어 있다.

IndPenSim은 초기 부피(initial volume)와 종균 농도(seed concentrations)를 포함한 여러 변수의 초기 조건에 무작위 변동을 포함한다. 시뮬레이션은 또한 페니실린 비생산속도(specific production rate), 바이오매스 비성장속도(biomass specific growth rate), 기질 농도(substrate concentration), 산/염기 농도(acid/base concentration), 페닐아세트산 농도(phenylacetic acid concentration), 냉각수 입구 온도(coolant inlet temperature), 산소 입구 농도(oxygen inlet concentration)에 배치 내 변동(within-batch variation)을 포함한다. 시뮬레이션에 외란을 추가하는 것은 산업 운전에서 전형적으로 마주치는 것과 유사한 공정 매개변수의 변동성을 갖춘 보다 현실적인 도전 과제를 제시하기 위함이다.

**표 1 (Table 1).** B2B 및 MPC 캠페인을 위한 IndPenSim 시뮬레이션 매개변수.

|시뮬레이션 매개변수 (Simulation parameter)|B2B|MPC|
|---|---|---|
|총 배치 시간 (Batch total time)|230 h|230 h|
|제어 조치 간격 (Control action interval)|230 h|10 h|
|제어 조치 시작 시점 (Start of the control action)|1 h|50 h|
|최적 페니실린 농도 (Optimal Penicillin conc.)|30 g/L|30 g/L|
|캠페인 길이 (Campaign length)|50 배치(batches)|80 배치(batches)|
|측정 간격 (Measurements interval)|1 h|1 h|

**표 2 (Table 2).** MPLS 모델에 사용된 IndPenSim 시뮬레이션 매개변수.

|입력 변수 (Input variable)|초기 조건 (Initial condition)|초기 변동성 (Initial variability, +/−)|
|---|---|---|
|CO₂ 농도, 배출 가스 (CO2 conc. Off gas)|0.038%|0.001%|
|용존 산소 농도 (DO2 conc., 용존 산소)|15 mg/l|0.5 mg/l|
|O₂ 농도, 배출 가스 (O2 conc. Off gas)|0.02%|0.05%|
|페니실린 농도 (Penicillin conc.)|0 g/l|0 g/l|
|pH|6.5 (−)|0.1 (−)|
|온도 (Temperature)|297 (K)|0.5 (K)|
|부피 (Volume)|5.8e4 l|500 l|

표 2(Table 2)는 본 연구에서 MPLS 모델을 식별하는 데 사용된 공정 매개변수의 명목값(nominal values)을 보여준다.

B2B 및 MPC 캠페인을 위한 시뮬레이션과 제어 전략은 전역 최적화(Global Optimization) 및 최적화(Optimization) 툴박스를 활용하여 Matlab R2017a에서 구현되었다.

---

## 3. MPLS 모델 식별 (MPLS model identification)

본 논문에서 제시하는 제어 전략은 Duran-Villalobos et al. (2016)에 광범위하게 기술된 MPLS 모델을 사용한다. 다만 이 절에서는 명확성을 위해 모델 식별 과정에 대한 간략한 설명을 제시한다.

### 3.1. PLS 회귀 (PLS regression)

PLS 회귀는 예측 변수(predictor) $X$와 응답 변수(response) $Y$를 '잠재 변수(Latent Variable, LV)' 공간의 정규직교(orthonormal) 벡터로 투영하여 선형 회귀 모델을 찾는 다변량 통계 기법으로, $X$와 $Y$ 사이의 공분산(covariance)을 최대로 설명한다. 표준 회귀 기법과 대조적으로, 이 회귀는 예측 변수 행렬 $X$가 그 값들 사이에 높은 다중공선성(multicollinearity)을 나타낼 때 특히 적합한데, 이는 전형적인 발효 공정의 시간에 따른 측정값과 같은 경우이다.

식 (1)과 (2)는 Martens and Naes (1989)가 제안한 이중대각(bi-diagonal) PLS 모델을 보여준다.

$$X = TP^T + E \tag{1}$$

$$Y = TQ^T + F \tag{2}$$

여기서 스코어 행렬(matrix of scores) $T$는 LV 공간에서 $X$의 각 행(관측값, observations)의 값을 담는다. 로딩 행렬(matrix of loadings) $P$와 $Q$는 각각 $X$와 $Y$의 각 열을 LV 공간으로 투영한 값을 담는다. 그리고 잔차 행렬(matrix of residuals) $E$와 $F$는 식별 집합(identification set)에서 회귀와 데이터 사이의 잔차 행렬이다.

응답 행렬 $Y$는 최종 페니실린 농도와 같은 종점 품질에 대해 벡터 $y$로 정의될 수 있다. 본 논문에서 제시하는 연구는 응답 변수의 측정값이 배치 종료 시에만 사용 가능하다고 가정한다. 결과적으로 새로운 배치 $i$에 대한 응답의 추정값은 식 (3)과 같이 기술될 수 있다.

$$\hat{y}_i = t_i Q^T \tag{3}$$

여기서 새로운 배치에 대한 스코어 벡터 $t_i$는 새로운 측정값 벡터 $x_i$를 투영 가중치 행렬(projection weight matrix) $W$로 투영하여 얻을 수 있으며, 이는 식 (4)에 나타난다.

$$t_i = x_i W \tag{4}$$

참고 [[02. PLSR (PLS regression)]]

### 3.2. 데이터 구조 (Data structure)

측정 변수(크기 $J$), 시간 간격(크기 $K$), 배치 번호(크기 $I$)를 포함하는 식별 데이터셋의 측정 변수들은 식 (5)에 나타난 것처럼 2차원 배열로 변환된다. 이 변환은 PLS 모델이 다변량 데이터 내의 시간 가변 동특성(time varying dynamics)을 포착할 수 있게 한다(Nomikos and MacGregor, 1995a).

$$X_{3D} \in \mathbb{R}^{I \times J \times K} \rightarrow X_{2D} \in \mathbb{R}^{I \times JK} \tag{5}$$

또한, 각 새로운 배치에서의 측정값 벡터 $x_i$, 가중치 행렬 $W$, 로딩 행렬 $P$는 식 (6)–(8)에 나타난 것처럼 분할된다.

$$x_i = \begin{bmatrix} x_p  u_n + \Delta u  x_f \end{bmatrix} = \begin{bmatrix} x_{pu} & x_f \end{bmatrix} \tag{6}$$

$$W = \begin{bmatrix} W_p \\ W_u \\ W_f \end{bmatrix} = \begin{bmatrix} W_{pu} \\ W_f \end{bmatrix} \tag{7}$$

$$P = \begin{bmatrix} P_p \\ P_u \\ P_f \end{bmatrix} = \begin{bmatrix} P_{pu} \\ P_f \end{bmatrix} \tag{8}$$

여기서 $u_n$은 MVT의 명목값을 담는 벡터이고, $\Delta u$는 MVT의 최적 변화량을 담는 벡터이다. 아래첨자는 다음을 나타낸다: $p$는 측정값의 과거 구간(past horizon), $u$는 MVT의 제어 구간(control horizon), $pu$는 MVT의 과거 및 제어 구간(past and control horizon), $f$는 측정값의 예측/미래 구간(prediction/future horizon).

[[Multivariate SPC charts for monitoring batch processes.pdf]]
[[번역) Multivariate SPC Charts for Monitoring Batch Processes]]

### 3.3. 모델 적응 (Model adaptation)

본 연구에서 사용된 MPLS 모델은 제어 시스템이 적용되는 각 배치의 종료 시에 갱신된다. 이 갱신의 목적은, Dayal and MacGregor (1997) 및 Joe Qin (1998)이 제안한 재귀 기법(recursive techniques)을 사용하여 달성되며, B2B 최적화기가 부과하는 변화의 결과로 운전 조건이 변함에 따라 제어기가 공정의 동특성을 추적할 수 있게 하고, MPC 내에서 사용되는 MPLS 모델을 '정제(refine)'하는 것이다. 이러한 적응이 필요한 이유는 PLS 회귀가 모델을 식별하는 데 사용된 운전 영역 국소(local)의 선형 동특성만을 표현할 수 있기 때문이다. 본 논문에서 사용된 재귀 기법은 식 (9)에 나타나 있다.

$$X = \begin{bmatrix} \lambda X_{i-1} \\ x_i \end{bmatrix} \quad \text{and} \quad y = \begin{bmatrix} \lambda y_{i-1} \\ y_i \end{bmatrix} \tag{9}$$

여기서 망각 인자(forgetting factor) $\lambda$가 이전 배치에서 수집된 데이터에 적용되어, 모델이 역사적(historical) 배치의 거동은 잊되 가장 최근 배치는 기억하도록 보장한다. 이는 제어기가 비선형일 수 있는 공정 동특성의 실질적인 변화를 따를 수 있게 한다. 적절한 $\lambda$ 값을 선택하는 접근법은 Duran-Villalobos et al. (2016)에 정식화되어 있으며, 배치 수가 공정이 현재 운전되고 있는 조건과 관련성이 있도록 선택되어야 한다. 본 논문에서 제시하는 연구에서는 B2B 및 MPC 캠페인 전반에 걸쳐 공정의 동특성이 실질적으로 변화하는 것으로 보이지 않았는데, $\lambda$ 값의 변경이 MPLS 모델의 예측 정확도에 유의한 개선을 제공하지 않았기 때문이다. 따라서 본 논문에서 제시하는 **모든 연구에서 $\lambda$는 1의 값으로 설정**되었다.

#### forgetting factor $\lambda$
- **$\lambda$가 클 때 (1에 가까울 때):** 모델이 과거의 데이터를 잊지 않고 무겁게 간직합니다. 공정이 전반적으로 안정적일 때 유리하지만, 상황이 갑자기 바뀌면 예전 기억에 얽매여 둔감하게 반응합니다. 이 논문의 시뮬레이션에서는 공정 특성이 크게 변하지 않았다고 판단하여 $\lambda$를 1로 고정해 모든 과거 데이터를 기억하도록 했습니다.    
- **$\lambda$가 작을 때 (0에 가까울 때):** 모델이 과거 데이터를 빨리 잊어버리고, 방금 수집된 새로운 데이터에 훨씬 더 큰 가중치를 둡니다. 상황이 변했을 때 아주 민첩하게 궤도를 수정합니다.    

따라서 기계를 완전히 교체하여 반응 속도 등 공정의 특성이 급격하게 달라진 상황이라면, **망각 계수를 훨씬 작은 숫자로 줄여주는 것이 정답입니다.** 그래야 더 이상 유효하지 않은 과거 기계의 데이터를 빨리 지우고, 새로운 기계의 작동 패턴을 신속하게 학습할 수 있기 때문입니다.

망각 계수 $\lambda$가 반영되어 합쳐진 데이터 행렬($X, y$)은 **MPLS 모델의 핵심 뼈대인 가중치($W$)와 로딩 행렬($P, Q$)을 새로 계산하는 PLS 알고리즘**에 입력됩니다.
수학적으로 공정 데이터 사이의 숨겨진 패턴을 찾으려면 행렬의 곱셈을 통해 변수들의 공분산(Covariance)을 구해야 합니다. 이 과정에서 $\lambda$가 어떻게 다시 연산되는지 수식으로 보면 다음과 같습니다:
1. **과거 데이터의 행렬 곱셈 🔄**: 데이터 행렬을 서로 곱하는 과정($X^T X$ 및 $X^T y$)이 일어날 때, 과거 데이터에 곱해져 있던 $\lambda$끼리 만나면서 결과적으로 **$\lambda^2$ (제곱)** 형태가 됩니다.    
2. **최종 패턴 업데이트 📊**:    
    - 업데이트된 전체 $X$ 패턴 = $\lambda^2 \times (\text{과거 } X \text{ 패턴}) + (\text{새로운 } X \text{ 패턴})$        
    - 업데이트된 $X$와 $y$의 관계 패턴 = $\lambda^2 \times (\text{과거 관계 패턴}) + (\text{새로운 관계 패턴})$      
즉, $\lambda$가 반영된 과거의 기억 데이터 패턴에 방금 공정이 끝난 최신 데이터 패턴을 더해서 **새로운 공분산 행렬**을 만들어내는 데 사용됩니다. 이 결과물을 바탕으로 모델의 매개변수들이 새로 짜여 피드백 제어에 쓰이게 됩니다.

### 3.4. 잠재 변수의 개수 (Number of latent variables)

LV 공간의 차원은 일반적으로 교차 검증(cross-validation, CV)에 의해 결정되어, 결과 모델이 응답 변수에 대한 강건한(robust) 예측을 제공하도록 보장한다(Camacho et al., 2007). PLS 모델의 LV 공간 차원을 결정하는 데 일반적으로 적용되는 방법은 leave-one-out 교차 검증(Martens and Naes, 1989)이다. 그러나 이 방법은 불필요하게 큰 모델을 초래할 수 있으며, 이는 과적합(overfitting)의 위험을 증가시킬 수 있다. 이는 Xu and Liang (2001)에 의해 입증되었는데, 다변량 시뮬레이션 연구에서 얻은 결과는 **몬테카를로 교차 검증(Monte Carlo Cross-Validation, MCCV)** 으로 알려진 방법이 leave-one-out 교차 검증과 비교했을 때 향상된 성능을 제공함을 보여주었다.

이러한 결과의 결과로, 본 연구에서 사용된 각 모델의 LV 개수를 찾기 위해 MCCV가 사용되었다. MCCV 접근법은 크기 $v$의 관측값 집합을 무작위로 추출하고 이 관측값들을 사용하여 PLS 모델을 식별함으로써 적절한 LV 개수 $A$를 결정한다. 이 과정은 각 LV 개수 $a$에 대해 $N$번 반복되며, 이는 식 (10)에 나타나 있다. 그런 다음 각 $a$ 값에 대한 결과를 비교하여 최소값을 갖는 것을 $A$로 선택한다. $v$와 $N$의 값을 선택하는 기준은 Xu and Liang (2001)에 제시되어 있다.

$$MCCV(a) = \frac{1}{Nv} \sum_{i=n}^{N} \left| y_{v,,n} - \hat{y}_{v,,n} \right| \tag{10}$$


| 구분        | MCCV                     | LOOCV                    |
| --------- | ------------------------ | ------------------------ |
| 분할 방식     | 학습·검증 세트를 무작위로 반복 분할     | 매번 관측치 1개만 검증에 사용        |
| 반복 횟수     | 사용자가 지정, 예: 50회, 100회    | 데이터 수와 동일한 (n)회          |
| 학습 데이터 크기 | 보통 전체의 70～90%            | 항상 (n-1)개                |
| 검증 데이터 크기 | 여러 개                     | 1개                       |
| 무작위성      | 있음                       | 없음                       |
| 결과 재현성    | 난수 시드에 따라 달라질 수 있음       | 동일 데이터에서는 항상 동일          |
| 계산량       | 반복 횟수에 따라 조절 가능          | 데이터가 많으면 매우 큼            |
| 오차 추정 편향  | 학습 비율이 작으면 다소 높을 수 있음    | 일반적으로 낮음                 |
| 오차 추정 분산  | 반복 횟수가 충분하면 비교적 안정적      | 상대적으로 높을 수 있음            |
| 데이터 활용도   | 일부 데이터가 검증에 사용되지 않을 수 있음 | 모든 데이터가 정확히 한 번씩 검증에 사용됨 |


---

## 4. 제어 목표 (Control objectives)

### 4.1. B2B 최적화 (B2B optimisation)

본 연구에 적용된 첫 번째 제어 목표는 처음에 Duran-Villalobos et al. (2016) 
[[Multivariate batch to batch optimisation of fermentation processes incorporating validity constraints.pdf]]의 논문에서 정식화되었다. 이 기법은 B2B 최적화기가 MVT*(본 연구에서는 글루코스 공급 속도)를 조정할 수 있게 함으로써, 종점 품질(본 연구의 사례에서는 최종 페니실린 농도)을 원하는 설정값에 더 가깝게 접근시키려 한다. 이러한 MVT 조정은 이전 배치에서 수집된 데이터의 고려를 통해 이루어졌으며, 이 데이터는 적응형 MPLS 모델의 정확도를 향상시키는 데 사용되었다.

* MVT **Manipulated Variable Trajectory**, 즉 **조작변수의 시간에 따른 변화 경로**

![[Pasted image 20260713104603.png]]

그림 1(Fig. 1)은 B2B 최적화기 내에서 사용되는 반복 제어 전략(iterative control strategy)의 단순화된 흐름도(flowchart)를 보여준다. 먼저, 저역 통과 필터(low-pass filter)를 통과한 후 사전 최적화된 MVT에 더해진 의사 무작위 이진 신호(Pseudo Random Binary Signal, PRBS)로 소수의 배치에 걸쳐 플랜트를 여기(excite)시킨다. Duran-Villalobos et al. (2016)은 3–8개의 배치가 충분한 정확도의 MPLS 모델을 얻기에 충분한 데이터를 제공함을 보였으며, 본 연구에서도 유사한 결과가 얻어졌으나, 이는 문제에 따라 달라질 가능성이 높을 것으로 예상된다. 그런 다음 MPLS 모델은 QP 비용 함수 내에서 사용되어, 원하는 종점 품질과 예측된 종점 품질 사이의 차이를 최소화하는 최적 MVT를 찾기 위해 풀린다. 최적화된 MVT는 최대 주파수의 10% 차단 주파수(cut-off frequency)를 갖는 저역 통과 유한 임펄스 응답(Finite Impulse Response, FIR) 필터를 사용하여 필터링되는데, 이는 이전 연구에서 유익한 것으로 나타났다(Camacho et al., 2015, 2007; Duran-Villalobos et al., 2016). 이 필터링된 MVT는 저진폭 PRBS(3%)로 여기되어 후속 배치 전체에 걸쳐 사용되며, 마지막으로 이 새로운 배치에서 수집된 데이터가 모델과 다음 배치 실행을 갱신하는 데 사용된다.¹

#### 설명
- **최적화된 MVT (The optimised MVT):** 알고리즘이 "이 타이밍에 포도당을 이만큼 넣으세요!"라고 계산해 낸 궤적입니다. 하지만 컴퓨터가 계산한 날것 그대로의 결과값은 종종 위아래로 뾰족뾰족하게 튀는(거친) 형태를 띱니다.    
- **저역통과 필터 (Low-pass filter):** 오디오에서 '저음'만 통과시키는 것처럼, 데이터에서는 '천천히 부드럽게 변하는 흐름(저주파)'만 통과시키고 '갑작스럽고 뾰족하게 변하는 흐름(고주파)'은 깎아내서 없애버리는 수학적 도구입니다. FIR(유한 임펄스 응답)은 이 필터를 구현하는 방식 중 하나입니다.    
- **최대 주파수의 10% 차단 (cut-off frequency of 10%):** 변화의 속도를 0부터 100까지 놓았을 때, 가장 천천히 변하는 하위 10%의 부드러운 움직임만 남기고, 나머지 90%의 자잘하고 빠른 변동은 전부 잘라내 버린다는 뜻입니다.
결과적으로 이 과정을 거치면, 위아래로 심하게 요동치던 그래프가 아주 매끄럽고 완만한 곡선으로 변하게 됩니다. 이전 연구들에서도 이렇게 부드럽게 깎아주는 것이 공정에 훨씬 유리하다고 밝혀졌기 때문에 이 방식을 채택


Duran-Villalobos et al. (2016)이 제안한 기법과 비교하여 본 연구에서 적용된 접근법의 주요 차이점은, 제안된 접근법이 현재 최적화된 MVT가 종점 제품 품질의 설정값에 공정을 더 가깝게 가져올 것인지 여부를 결정한다는 점이다. 이 추가는 B2B 최적화기의 수렴 속도(convergence speed)를 유의하게 개선하는 것으로 나타났다. 식 (11)–(13)은 배치에서 배치로 어떻게 결정이 수행되는지를 보여준다.

$$e_{past} = \min\left( (y - y_{sp})^2 \right) \tag{11}$$

$$e_i = (y_i - y_{sp})^2 \tag{12}$$

$$u_{i+1} = \begin{cases} u_i & \text{if } e_i < e_{past} \ u_{e_{past}} & \text{if } e_i > e_{past} \end{cases} \tag{13}$$

여기서 $e_{past}$는 측정된 종점 품질 $y$와 원하는 설정값 $y_{sp}$ 사이에서 발견된 최소 이차 오차(minimum quadratic error)이고, $e_i$는 $i$번째 종점 품질 $y_i$와 설정값 $y_{sp}$ 사이의 이차 오차이며, $u_i$는 $i$번째 배치에 대한 MVT이고, $u_{e_{past}}$는 $e_{past}$에 대응하는 MVT이다.

#### 설명 요약
- $e_{past} = \min\left( (y - y_{sp})^2 \right)$: 이번 배치 오차
- $e_i = (y_i - y_{sp})^2$: 역대 제일 결과가 좋았던 최소 오차
- $e_i < e_{past}$ 이면 새 궤적($u_i$) 유지, $e_i > e_{past}$ 이면 역대 최고였던 과거 궤적($u_{epast}$)으로 롤백


산업 제어 전략의 주요 과제 중 하나는 외란이 존재하는 상황과 잠재적으로 공정 동특성의 변화가 있는 상황에서 설정값을 전달하는 것이다. 외란 중 어느 것이라도 한 배치에서 다음 배치로 높은 상관관계를 갖는다면, 이전 배치의 정보가 B2B 최적화에서 사용되어 현재 배치가 유사한 외란을 완화하기 위해 어떻게 운전되어야 하는지를 결정할 수 있다. 그러나 외란의 거동이 확률적(stochastic)이고 배치마다 변화한다면, MPC와 같은 기법을 사용하는 배치 내 제어(within-batch control)가 권장된다(Flores-Cerrillo and MacGregor, 2003).

### 4.2. MPC (model predictive control)

설정값이 충족되고 제품 품질의 변동이 감소하도록 보장하기 위해 MPC가 적용된다. MPC 전략은 배치 진행 중 서로 다른 제어 조치 지점(control action points)에서 MVT를 조정하며, B2B 최적화기와 동일한 QP 문제를 풀고 유사한 데이터 기반 적응형 MPLS 모델을 사용한다.

그림 2(Fig. 2)는 MPC를 위한 반복 제어 전략의 단순화된 흐름도를 보여준다. 먼저, 반복 과정은 B2B 최적화기와 동일한 전략을 사용한다. 즉, 낮은 필터링된 PRBS로 플랜트를 여기시키고 MPLS 모델을 식별한다. 그러나 MPC가 적용될 때는 이전에 최적화된 '골든(golden)' 궤적에 PRBS가 적용된다. 그런 다음 MPC 전략은 중첩 루프(nested loop) 구조를 사용하여 실행된다.

> ¹ 자세한 내용은 Duran-Villalobos et al. (2016)을 읽어보기를 권한다.

내부 제어 루프(inside control loop)는 배치가 완료될 때까지 각 $m$번째 제어 지점에서 MVT의 미래 최적 변화량 $\Delta u$를 계산한다. 이 계산은 Flores-Cerrillo and MacGregor (2005)에 제시된 전략과 유사하며, 여기서 QP는 스코어의 변화를 식별 데이터셋에서 사용된 것에 더 가깝게 유지하는 스코어 값을 탐색한다. 그런 다음 이 새롭게 최적화된 스코어를 다변량 주성분 분석(Multivariate Principal Component Analysis, MPCA) 모델로 투영하여 MVT를 얻는다. 대조적으로, 본 논문에서 기술하는 MPC 전략은 QP 내에서 MVT에 적용되어야 할 필요한 변화량을 직접 계산한다. 5절에서 기술하는 이 QP는 미래 예측 종점 품질과 그 설정값 사이의 차이를 최소화하는 목표를 갖는 비용 함수를 포함한다. 또한, QP에 부과된 제약은 MVT의 변화가 플랜트의 물리적 능력과 MPLS 모델을 식별하는 데 사용된 스코어 공간 영역 내에 유지되도록 보장한다.

MVT의 최적 단계가 계산되면, 제어 지점에서 배치가 다음 제어 지점 $m+1$까지 실행되고, 종점 품질을 예측하는 데 사용되는 데이터 벡터 $x_i$가 새로운 공정 측정값으로 갱신되어 $m+1$ 제어 지점에서의 미래 최적 단계를 계산한다. 이 과정은 배치가 끝날 때까지 각 제어 지점에서 반복된다.

각 배치의 끝에서 외부 제어 루프(outer control loop)가 구현된다. 배치 $i$의 데이터가 수집되고 MPLS 모델이 갱신된다. 그런 다음 배치 $i+1$이 동일한 '골든' 궤적을 MVT로 사용하여 첫 번째 제어 지점까지 실행된다. 이 단계에서 제어 루프가 다시 실행되어 배치 $i+1$의 끝까지 각 제어 지점에서 최적 MVT를 얻는다. 이 과정은 MPC 캠페인이 끝날 때까지 각 배치에 대해 반복된다.

MPC 실험 중, 각 제어 지점에서 사용 가능한 측정값이 모든 배치 동안 모델 예측의 품질을 향상시키는 것으로 나타났다. 또한 제어 조치에서 더 긴 간격이 사용될 때 모델의 예측 정확도가 감소하는 것으로 나타났는데, 이는 예상된 것이다(Bonvin et al., 2006).

**본 논문에서 제시하는 결과에서 제어 간격은 10 h로 설정되었다. 이 아래로 제어 간격을 줄이는 것은 제어 시스템의 성능을 향상시키지 못하는 것으로 나타났다. 제어 간격에 가장 적합한 값은 연구되는 공정의 동특성에 따라 달라질 것**이다.

---

## 5. QP 최적화 (QP optimisation)

### 5.1. 비용 함수 (Cost function)

4절에서 설명한 바와 같이, MVP의 최적화는 MPLS 모델을 식별하는 데 사용된 데이터가 정의하는 의사결정 공간의 한계를 존중하면서 종점 품질을 설정값에 더 가깝게 가져오려 한다. 이 목표는 Duran-Villalobos et al. (2016)에서 정식화되었으며, 여기서 최소화될 널리 사용되는 비용 함수(Qin and Badgwell, 2003)는 설정값과 예측 출력 사이 오차의 제곱과 MVT에 가해진 변화의 제곱 사이의 절충(trade-off)으로 정의된다. 이 비용 함수는 식 (14)에 제시되어 있다.

$$\min_{\Delta u} \left(\hat{y}_i - y_{sp}\right)^T \left(\hat{y}_i - y_{sp}\right) + \Delta u^T M \Delta u$$

$$\text{s.t.} \begin{cases} \hat{y}_i = t_i Q^T \\
lb \leq u_n + \Delta u \leq ub \\
Vol_{ini} + \Delta_{Vol} \leq Vol_{max} \\
J_e \leq 1 \ \text{and} \ J_t \leq 1 \end{cases} \tag{14}$$

- **$\hat{y}_i - y_{sp}$:** 모델이 예측한 최종 농도($\hat{y}_i$)와 목표치($y_{sp}$, 30g/L) 사이의 차이(오차)입니다. "목표에 최대한 가깝게 맞춰라!"라는 뜻입니다.    
- **$\Delta u$:** 우리가 기존에서 새롭게 바꾸려는 포도당 공급 궤적의 '변화량'입니다.    
- **$M$:** 궤적을 너무 급격하게 바꾸지 못하도록 브레이크를 거는 가중치(페널티) 행렬
- $(\hat{y}_i - y_{sp})^T (\hat{y}_i - y_{sp})$: 
	- 최소제곱법(Least Squares) -> 벡터 행렬의 곱셈이라 형태가 조금 다를 뿐, $(x-y)^2$과 같은 의미
- $\Delta u^T M \Delta u$
	- **기원:** 수학적 안정성을 확보하기 위한 **'티호노프 정규화(Tikhonov Regularization)'** 또는 '리지 회귀(Ridge Regression)'라는 기법에서 차용한 개념입니다. 제어공학에서는 이를 '이동 억제(Move Suppression)'라고 부릅니다.
	- **의미:** 포도당 밸브의 조작 변화량($\Delta u$)을 제곱하고, 거기에 벌금 가중치($M$)를 곱함. 패널티 항임. 이 패널티 항이 없으면 계속 포도당 공급밸브를 100% 열었다가 0%로 잠궜다가 반복(뱅뱅(Bang-Bang) 제어)
	- $\Delta u^T M \Delta u$는 첫 번째 항과 완전히 동일한 논리를 가진 '벡터 형태의 제곱' ($M$은 가중치 행렬), 제곱형태로 가중치를 주기 때문에 무조건 양수가 패널티로 누적

`s.t.` (subject to, ~라는 조건 하에): 어겨서는 안 되는 '철칙(Hard Constraints)'을 의미

**1. 예측 모델의 수학적 규칙


$$\hat{y}_i = t_i Q^T$$

- **의미:** 모델이 예측한 수율($\hat{y}_i$)은 반드시 학습된 MPLS 모델의 공식(잠재 변수 점수 $t_i$와 로딩 행렬 $Q^T$의 곱)을 통해서만 계산되어야 한다는 뜻입니다.    
- **역할:** 최적화 알고리즘이 공식을 무시하고 임의로 유리한 수율 수치를 지어내는 것을 원천 차단합니다.    

**2. 펌프의 물리적 속도 한계**

$$lb \leq u_n + \Delta u \leq ub$$

- **의미:** 현재 투입 속도($u_n$)에 새로운 변화량($\Delta u$)을 더한 최종 포도당 투입 속도는, 기계가 작동할 수 있는 최소 한계($lb$, Lower Bound, 보통 0)와 최대 한계($ub$, Upper Bound, 최대 펌프 파워) 사이에 있어야 합니다.    
- **역할:** 펌프가 물리적으로 뿜어낼 수 없는 비현실적인 속도로 작동하라는 명령을 내리지 못하게 막습니다.    

**3. 발효 탱크의 용량 한계**

$$Vol_{ini} + \Delta_{Vol} \leq Vol_{max}$$

- **의미:** 현재 탱크에 들어있는 부피($Vol_{ini}$)에 새롭게 추가할 포도당의 부피($\Delta_{Vol}$)를 더했을 때, 탱크의 최대 용량($Vol_{max}$, 100,000 리터)을 넘어서는 안 됩니다.    
- **역할:** 앞서 이야기했던 것처럼 공장에 포도당 액체가 넘쳐흐르는 대형 사고를 방지하는 가장 직관적인 물리적 안전장치입니다.  

**4. 데이터 기반의 모델 안전구역**

$$J_e \leq 1 \ \text{and} \ J_t \leq 1$$

- **의미:** 바로 우리가 앞서 살펴본 '부트스트랩 안전 울타리'입니다. 예측 오차($J_e$)와 모델 중심으로부터의 거리($J_t$)가 허용된 최대치(비율상 1)를 넘지 않아야 합니다.    
- **역할:** 모델이 과거에 학습한 적 없는 낯설고 위험한 데이터 영역으로 예측 범위를 벗어나는 것을 막아줍니다.
- $J_e$는 통계적 공정 관리(SPC)에서 모델의 예측이 얼마나 정확한지 측정하는 SPE(Squared Prediction Error, 제곱 예측 오차)를 기반으로 합니다. 수식으로 풀어서 쓰면 다음과 같습니다.

$$J_e = \frac{\text{현재 시점의 SPE (예측 오차)}}{\text{부트스트랩으로 구한 SPE 한계치 } (SPE_{limit})}$$

- $J_t$는 다변량 통계학에서 사용하는 호텔링의 $T^2$ 통계량(Hotelling's $T^2$)을 기반으로 만들어졌습니다. 수식의 구조는 $J_e$와 똑같이 분수 형태를 띱니다.

$$J_t = \frac{\text{현재 상태가 정상 중심에서 벗어난 거리 (Hotelling's } T^2)}{\text{부트스트랩으로 구한 거리 허용 한계치 } (T^2_{limit})}$$




여기서:

- 비용 함수는 QP 최적화에 의해 MVT에 가해지는 변화를 조절하는 데 사용되는 대각 가중치 행렬(diagonal matrix of weights) $M$을 포함한다. 가중치 행렬 $M$의 대각 원소는 0.01의 값으로 설정되었다. 이 값은 MPC에서 수렴 속도와 제어 조치의 공격성(aggressiveness) 사이의 좋은 절충으로 나타났다. 그러나 B2B 최적화에서는 0.1보다 작은 어떤 값이라도 동일한 수렴 속도에 도달하는 것으로 나타났다.
- 비용 함수는 첫 번째 제약에 표현된 추정 종점 품질의 계산을 조건으로 한다. 그러나 미래 공정 측정값의 값을 알 수 없으므로, 제어 조치가 구현될 때 현재 배치의 스코어 값은 5.2절에서 기술하는 결측 데이터 기법을 사용하여 추정되어야 한다. 두 번째 제약은 MVT에 한계를 도입하며, 이는 공급 속도(feed-rate)의 크기에 대한 물리적 제한을 통해 부과된다. 평균 중심화(mean-centred)된 이러한 제약은 하한 및 상한 경계 벡터 $lb$와 $ub$로 표현된다.
- 세 번째 제약은 공급 속도가 반응기 내 최대 부피를 용기에 의해 부과된 물리적 한계 아래로 제한하도록 보장하며, 본 연구에서 이 한계는 100,000 리터였다. 이 제약은 5.3절에서 간략히 기술한다.
- 마지막으로, 유효성 제약 한계 $J_e$와 $J_t$는 QP 최적화가 탐색하는 해 공간(solution space)을 제한하여, 해가 MPLS 모델을 식별하는 데 사용된 데이터의 공간 내에 있도록 보장한다. 유효성 제약은 Duran-Villalobos et al. (2016)과 Laurí et al. (2013)에서 제안되었다. 그러나 **본 논문에서 적용된 신뢰한계는 데이터가 정규 분포를 따른다고 가정하지 않으며**, 이는 5.4절에서 더 설명한다.

Duran-Villalobos et al. (2016)에서 제시된 연구에서는 미래 측정값의 예측값이 MVT의 변화가 예측 출력에 미치는 영향을 계산하는 데 사용되었다. 대조적으로, 본 연구에서 최적화된 배치의 스코어는 과거 측정값에 대한 추정 스코어 벡터 $\hat{t}_i$의 합과 MVT의 스코어 변화 효과로 정의되며, 이는 식 (15)에 나타난다. 이 전략을 사용하면 예측 출력의 계산에 미래 측정값의 값이 불필요하다.

$$t_i = \hat{t}_i + \Delta u W_u \tag{15}$$

#### 참고
수식은 우리가 밸브를 조작했을 때($\Delta u$), 미래의 결과가 어떻게 달라질지 계산하는 '다리' 역할을 합니다.
- **$t_i$**: 새로운 조작이 반영된 후의 '업데이트된 최종 상태(점수)'입니다.    
- **$\hat{t}_i$**: 우리가 아무런 추가 조작을 하지 않았을 때 예상되는 '기본 예측 상태'입니다.    
- **$\Delta u W_u$**: 우리의 새로운 밸브 조작량($\Delta u$)이 모델의 가중치($W_u$)를 거쳐 '결과에 미치는 추가적인 영향력'입니다.  
즉, "새로운 미래 = 가만히 있을 때의 미래 + 내 행동이 만들 변화"라는 아주 상식적인 논리를 수학적으로 쓴 것

식 (15)를 식 (14) ($\min_{\Delta u} \left(\hat{y}_i - y_{sp}\right)^T \left(\hat{y}_i - y_{sp}\right) + \Delta u^T M \Delta u$)에 대입하면, MVT를 최적화하기 위한 QP 문제는 식 (16)에 나타난 것처럼 표현될 수 있다.

$$\min_{\Delta u} \frac{1}{2} \Delta u^T H \Delta u + f^T \Delta u$$

$$\text{s.t.} \begin{cases} H = W_u Q^T Q W_u^T + M \\
f^T = \left( \hat{t}_i Q^T - y_{sp} \right) Q W_u^T \\
lb - u_n \leq \Delta u \leq ub - u_n \\
Vol_{ini} + \Delta_{Vol} \leq Vol_{max} \\
J_e \leq 1 \ \text{and} \ J_t \leq 1 \end{cases} \tag{16}$$

#### 참고
컴퓨터의 최적화 알고리즘(Solver)들은 주로 위와 같은 $\frac{1}{2}x^T H x + f^Tx$ 형태를 가장 빠르게 풀도록 설계되어 있습니다. 그래서 앞서 보았던 직관적인 목적 함수에 식 (15)를 대입하여 전개(가로풀기)하면, 복잡한 덩어리들이 $H$와 $f^T$라는 두 개의 깔끔한 부품으로 정리됩니다.

**1. 대입하기**
14번 수식: $\hat{y}_i = t_i Q^T$
여기에 15번 수식($t_i = \hat{t}_i + \Delta u W_u$)을 그대로 쏙 집어넣습니다.

$$\hat{y}_i = (\hat{t}_i + \Delta u W_u) Q^T$$

**2. 괄호 풀기 (분배법칙)**
괄호 밖의 $Q^T$를 안쪽의 두 항에 각각 곱해주면 다음과 같이 두 덩어리로 깔끔하게 나뉩니다.

$$\hat{y}_i = \hat{t}_i Q^T + \Delta u W_u Q^T$$

이 수식은 아주 직관적인 의미를 담고 있습니다.
- **$\hat{t}_i Q^T$**: 아무것도 하지 않고 가만히 놔뒀을 때의 **기본 예상 수율**
- **$\Delta u W_u Q^T$**: 우리의 밸브 조작($\Delta u$)으로 인해 **추가로 변하는 수율**
이제 이 결과를 원래 목적 함수의 첫 번째 항, 즉 '오차'를 나타내는 부분인 $(\hat{y}_i - y_{sp})$ 에 대입할 차례입니다.
방금 구한 $\hat{y}_i$를 오차 식에 대입하면 다음과 같이 됩니다.

$$(\hat{t}_i Q^T + \Delta u W_u Q^T - y_{sp})$$

수식에서 $\Delta u$가 없는 부분(우리가 통제할 수 없는 고정값)과 $\Delta u$가 있는 부분(우리가 통제할 변화량)으로 괄호를 치면 이런 모양이 됩니다.

$$( \hat{t}_i Q^T - y_{sp} ) + ( \Delta u W_u Q^T )$$

여기서 두 덩어리의 의미를 명확히 짚고 넘어갈게요.
- **앞 덩어리 $A$**: $( \hat{t}_i Q^T - y_{sp} )$
    가만히 두었을 때 예상되는 '기본 오차'입니다. 지금 당장은 기계가 바꿀 수 없는 고정된 상수 역할을 합니다. (앞서 $f^T$를 설명할 때 보았던 그 나침반의 뼈대네요!)
- **뒤 덩어리 $B$**: $( \Delta u W_u Q^T )$
    우리가 밸브를 조작($\Delta u$)해서 만들어낼 '수율의 변화량'입니다.

자, 이제 거의 다 왔습니다! 원래 비용 함수의 첫 번째 항은 오차를 '제곱'하는 형태였죠. 즉, 방금 우리가 나눈 $(A + B)$ 전체를 자신과 곱하는 $(A + B)^T (A + B)$ 계산을 해야 합니다.

이 식을 곱셈 공식처럼 전개하면 크게 $A^2 + 2AB + B^2$ 와 같은 3개의 항으로 나뉘게 됩니다. (행렬의 전개도 기본 원리는 같습니다.)
**3. $A^2$ 에 해당하는 항 ($\Delta u$가 없는 상수항)**

$$(\hat{t}_i Q^T - y_{sp})^T (\hat{t}_i Q^T - y_{sp})$$

- 우리의 행동($\Delta u$)과 무관하게 이미 고정되어 있는 순수한 초기 오차의 제곱입니다.

**4. $2AB$ 에 해당하는 항 ($\Delta u$가 한 번 곱해진 1차항)**

$$2 (\hat{t}_i Q^T - y_{sp}) Q W_u^T \Delta u$$

- 행렬 곱셈의 규칙에 따라 $A$와 $B$가 섞인 형태입니다.
- 이 부분을 자세히 보면, 16번 수식에 등장했던 나침반 $f^T$가 바로 이 1차항에서 만들어졌음을 알 수 있습니다.

**5. $B^2$ 에 해당하는 항 ($\Delta u$가 두 번 곱해진 2차항)**

$$(\Delta u W_u Q^T)^T (\Delta u W_u Q^T) = \Delta u^T (W_u Q^T Q W_u^T) \Delta u$$

- $\Delta u$가 양쪽에 배치되고 그 사이에 시스템의 민감도가 끼어있는 형태가 됩니다.

이제 여기에 우리가 원래 목적 함수 뒤에 달아두었던 '변화에 대한 벌금', 즉 $\Delta u^T M \Delta u$를 3번 항목($B^2$ 항)과 합쳐보겠습니다.

$$\Delta u^T (W_u Q^T Q W_u^T + M) \Delta u$$

(16)번 수식에서 시스템의 저항력과 브레이크를 의미하던 **$H$** 행렬이 바로 여기서 탄생했습니다!
그리고 $\Delta u$가 전혀 없는 상수항($A^2$)은 미분값이 0이 되어 완전히 사라져 버림.
$\frac{1}{2}$도 미분하면 생기는 2와 상쇄되도록 미리 곱함.


- **$H$ (이차항 계수, 시스템의 민감도와 브레이크):**
	- 행동($W_u$)이 결과($Q^T$)로 이어지는 민감도에 우리가 설정한 벌금($M$)을 더한 값입니다. 그래프의 '그릇 모양(곡률)'을 결정하여, 정답이 너무 튀지 않게 잡아줍니다.
		- **$W_u$**: 포도당 투입($\Delta u$)이 시스템 내부 상태(점수)를 어떻게 바꾸는지 나타내는 **'입력 가중치'**
		- **$Q$**: 그 내부 상태(점수)가 최종 페니실린 수율($y$)로 어떻게 변환되는지 나타내는 **'출력 가중치'**
		- **$M$**: 앞서 우리가 설정했던 '밸브 조작에 대한 패널티

$$H = W_u Q^T Q W_u^T + M$$

- **$f^T$ (일차항 계수, 현재의 오차 방향):**
	- 자세히 보시면 앞부분에 $(\text{현재 예상 수율} - \text{목표 수율})$이 들어있습니다. 즉, 지금 목표에서 얼마나 떨어져 있는지(오차), 그리고 목표를 향해 어느 방향으로 움직여야 하는지 알려주는 나침반 역할을 합니다.
	- **$\hat{t}_i Q^T - y_{sp}$**: 가만히 놔두었을 때 예상되는 수율과 목표 수율(30g/L) 간의 '순수한 오차'입니다.
	- **$Q W_u^T$**: 오차를 확인했으니, 이를 줄이기 위해 밸브 조작($\Delta u$)과 수율 사이의 관계를 역산해서 곱해주는 부분

$$f^T = (\hat{t}_i Q^T - y_{sp}) Q W_u^T$$



### 5.2. 결측 데이터에 의한 추정 (Estimation with missing data)

MVT를 최적화하려면 미래 종점 품질을 추정하는 것이 필요하다. 그러나 스코어 벡터 $t_i$를 얻는 데 필요한 미래 측정값의 값은 각 제어 지점에서 사용할 수 없다. 이 문제를 해결하기 위해, Flores-Cerrillo and MacGregor (2004)는 기존 MPCA 또는 MPLS 모델을 사용하여 스코어를 추정하는 결측 데이터 알고리즘(missing data algorithms)의 사용을 제안하였다. 이러한 예측이 가능한 것은 그러한 모델이 측정값 벡터의 공분산으로 기술되는, 전체 배치 궤적에 걸친 데이터의 시간 가변 구조를 포착하기 때문이다.

제안된 많은 결측 데이터 추정 기법이 있어 왔으며(Arteaga and Ferrer, 2002), 모달 평면 투영(Projection to the Modal Plane, PMP)과 트림된 스코어 회귀(Trimmed Score Regression, TSR)가 가장 적합한 방법으로 자주 인용된다(Arteaga and Ferrer, 2002; Ed, 2013; García-Muñoz et al., 2004; Gins et al., 2009; Vanlaer et al., 2011).

PMP 방법에서는 알려진 측정값 벡터와 MVT의 명목값을 식별 데이터셋에서 각각의 로딩 행렬 값 $P_{pu}$가 정의하는 스코어 공간으로 회귀하여 스코어를 추정한다. PMP를 사용하여 스코어 값의 예측을 얻는 식은 식 (17)에 나타나 있다.

$$\hat t_i = \begin{bmatrix} x_p & u_n \end{bmatrix} P_{pu} \left( P_{pu}^T P_{pu} \right)^{-1} \tag{17}$$

만약 MPLS 모델이 Martens (2001)가 제안한 이중대각(bi-diagonal) 방법 대신 Wold et al. (1987)이 제안한 대각(diagonal) 방법을 사용하여 식별된다면, 로딩 행렬 $P$ 대신 가중치 행렬 $W$가 사용되어야 한다(Nelson and Taylor, 1996).

#### 참고
- $\begin{bmatrix} x_p & u_n \end{bmatrix}$: 가로 방향으로 concat, 즉 horizontal concatenation 각 원소를 가로 방향으로 이어 붙리는 것

[[02. PMP (Projection to the Model Plane) 이론 및 수식 정리]]
#### Projection to the Model Plane (PMP) 이론 및 수식 정리
##### 1. PMP가 필요한 이유
MPLS 모델에서는 새로운 배치 $i$의 전체 측정 벡터 $\mathbf{x}_i$가 주어지면, 일반적으로 다음과 같이 잠재 스코어(Latent Score) $\mathbf{t}_i$를 계산할 수 있습니다.

$$\mathbf{t}_i = \mathbf{x}_i \mathbf{W}$$

그러나 **배치가 현재 진행 중(On-line)**이라면, 아직 도달하지 않은 미래 시점의 공정 측정값 $\mathbf{x}_f$는 본질적으로 알 수 없습니다. 논문에서는 현재 진행 중인 배치의 전체 측정 벡터 $\mathbf{x}_i$를 다음과 같이 구분합니다.

$$\mathbf{x}_i = \begin{bmatrix} \mathbf{x}_p & \mathbf{u}_n + \Delta\mathbf{u} & \mathbf{x}_f \end{bmatrix}$$

* **$\mathbf{x}_p$**: 현재(현재 샘플링 시점)까지 측정된 과거 공정 변수 (Past process variables)
* **$\mathbf{u}_n$**: Nominal MVT (Manipulated Variable Trajectory, 기준 조작 변수 궤적)
* **$\Delta\mathbf{u}$**: 실시간 최적화(MPC)를 통해 앞으로 계산 및 변경할 MVT 변경량
* **$\mathbf{x}_f$**: 아직 측정되지 않은 미래 시점의 공정 변수 (Future process variables)

여기서 미래 변수인 $\mathbf{x}_f$를 모르기 때문에 전체 벡터 $\mathbf{x}_i$를 이용한 전통적인 스코어 계산이 불가능합니다.

PMP를 통해 추정된 스코어 $\hat{\mathbf{t}}_i$는 다음과 같이 정의됩니다.

$$\hat{\mathbf{t}}_i = \begin{bmatrix} \mathbf{x}_p & \mathbf{u}_n \end{bmatrix} \mathbf{P}_{pu} \left( \mathbf{P}_{pu}^{T}\mathbf{P}_{pu} \right)^{-1}$$

이 수식을 간결하게 다루기 위해, 현재 시점에서 가용한(알고 있는) 정보 벡터를 $\mathbf{z}_i$로 정의하겠습니다.

$$\mathbf{z}_i = \begin{bmatrix} \mathbf{x}_p & \mathbf{u}_n \end{bmatrix}$$

이를 대입하면 PMP 수식은 아래와 같이 단순화됩니다.

$$\hat{\mathbf{t}}_i = \mathbf{z}_i \mathbf{P}_{pu} \left( \mathbf{P}_{pu}^{T}\mathbf{P}_{pu} \right)^{-1}$$

##### 2. 알려진 정보 벡터 ($\mathbf{z}_i$)

$$\mathbf{z}_i = \begin{bmatrix} \text{현재까지의 공정 측정값 } (\mathbf{x}_p) & \text{기준 MVT 값 } (\mathbf{u}_n) \end{bmatrix}$$

- **예시 (100시간 배치 공정에서 현재 40시간 경과 시점):    
    - $0 \sim 40$시간 동안 수집된 온도, pH, DO(용존산소량), 배양액 부피 등은 이미 측정되어 $\mathbf{x}_p$에 저장되어 있습니다.        
    - 전체 운전 동안의 기준 기질 공급 궤적(Nominal Glucose Feed Trajectory, $\mathbf{u}_n$)은 사전에 설정되어 알고 있습니다.        
    - 아직 지나지 않은 $40 \sim 100$시간의 공정 측정값($\mathbf{x}_f$)은 미상의 결측값입니다.        
    - 즉, PMP는 실제로 측정된 부분($\mathbf{x}_p$)과 사전에 정의된 운전 기준($\mathbf{u}_n$)만을 결합하여 가용 정보 $\mathbf{z}_i$를 구성합니다.       

#####  3. 축소된 로딩 행렬 ($\mathbf{P}_{pu}$)
전체 로딩 행렬(Loading Matrix) $\mathbf{P}$ 중에서 현재 관측 가능한 변수들에 대응하는 행(Row)만 슬라이싱하여 추출한 부분 행렬입니다. 전체 로딩 행렬 $\mathbf{P}$는 다음과 같이 분할할 수 있습니다.

$$\mathbf{P} = \begin{bmatrix} \mathbf{P}_p \\ \mathbf{P}_u \\ \mathbf{P}_f \end{bmatrix} = \begin{bmatrix} \mathbf{P}_{pu} \\ \mathbf{P}_f \end{bmatrix}$$

따라서 가용 로딩 행렬 $\mathbf{P}_{pu}$는 아래와 같습니다.

$$\mathbf{P}_{pu} = \begin{bmatrix} \mathbf{P}_p \\ \mathbf{P}_u \end{bmatrix}$$

- **$\mathbf{P}_p$**: 과거 측정 공정 변수($\mathbf{x}_p$)에 대응하는 로딩 벡터/행렬    
- **$\mathbf{P}_u$**: 조작 변수 궤적($\mathbf{u}_n$)에 대응하는 로딩 벡터/행렬    
- **$\mathbf{P}_f$**: 미래 미측정 공정 변수($\mathbf{x}_f$)에 대응하는 로딩 벡터/행렬    
- **의미**: $\mathbf{P}_{pu}$는 알려진 변수들($\mathbf{z}_i$)이 저차원 Latent Space 상의 Score $\mathbf{t}_i$와 어떤 통계적 관계를 갖는지를 나타내는 가교 역할을 합니다.    

##### 4. 행렬 차원(Dimension) 분석

PMP 수식의 수학적 정합성을 확인하기 위해 각 행렬과 벡터의 차원을 분석합니다.
- 현재 알고 있는 변수의 총 개수를 $M_{pu}$라 하고,    
- MPLS 모델이 정의하는 Latent Variable(주성분)의 개수를 $A$라고 가정합니다.    

|**기호**|**설명**|**차원 (Dimension)**|
|---|---|---|
|$\mathbf{z}_i$|가용 측정값 및 기준 벡터|$1 \times M_{pu}$|
|$\mathbf{P}_{pu}$|가용 로딩 행렬|$M_{pu} \times A$|
|$\mathbf{z}_i \mathbf{P}_{pu}$|단순 투영 벡터|$1 \times A$|
|$\mathbf{P}_{pu}^T \mathbf{P}_{pu}$|가용 로딩의 Gram Matrix|$A \times A$|
|$(\mathbf{P}_{pu}^T \mathbf{P}_{pu})^{-1}$|Gram Matrix의 역행렬|$A \times A$|
|$\hat{\mathbf{t}}_i$|**추정된 Latent Score 벡터**|**$1 \times A$**|

- **결론**: 수많은 공정 측정 변수($M_{pu}$개)가 PMP 투영을 거쳐 정해진 소수의 주성분 개수($A$개)를 가진 컴팩트한 잠재 스코어 벡터 $\hat{\mathbf{t}}_i$로 차원 축소 및 압축됩니다.

##### 5. 최소제곱법(Least Squares Method)을 통한 수학적 유도

PMP 식은 임의로 고안된 경험식이 아니라, **최소제곱법(Least Squares)** 기준 하에서 오차를 최소화하도록 유도된 통계적 최적해입니다.
MPLS 모델의 $X$-블록 기본 관계식은 다음과 같습니다.

$$\mathbf{X} = \mathbf{T}\mathbf{P}^T + \mathbf{E}$$

새로운 개별 배치 $i$에 대해 잔차 오차를 제외한 구조적 관계는 다음과 같이 나타납니다.

$$\mathbf{x}_i \approx \mathbf{t}_i \mathbf{P}^T$$

현재 시점에서는 전체 $\mathbf{x}_i$를 알지 못하고 관측 정보 $\mathbf{z}_i$와 이에 대응하는 로딩 $\mathbf{P}_{pu}$만 존재하므로, 관계식은 다음과 같이 축소됩니다.

$$\mathbf{z}_i \approx \hat{\mathbf{t}}_i \mathbf{P}_{pu}^T$$

PMP의 목표는 실제 관측치 $\mathbf{z}_i$와 모델 기반 역산치 $\hat{\mathbf{t}}_i \mathbf{P}_{pu}^T$ 사이의 오차(잔차 제곱합)를 최소화하는 $\hat{\mathbf{t}}_i$를 찾는 것입니다.

$$\min_{\hat{\mathbf{t}}_i} \left\Vert{} \mathbf{z}_i - \hat{\mathbf{t}}_i \mathbf{P}_{pu}^T \right\Vert{}^2$$

최적화 목적함수 $J$를 다음과 같이 잔차의 제곱합으로 정의합니다.

$$J = \left( \mathbf{z}_i - \hat{\mathbf{t}}_i \mathbf{P}_{pu}^T \right) \left( \mathbf{z}_i - \hat{\mathbf{t}}_i \mathbf{P}_{pu}^T \right)^T$$

이를 최적화하기 위해 추정 대상 벡터인 $\hat{\mathbf{t}}_i$에 대해 편미분을 수행합니다.

$$\frac{\partial J}{\partial \hat{\mathbf{t}}_i} = -2 \left( \mathbf{z}_i - \hat{\mathbf{t}}_i \mathbf{P}_{pu}^T \right) \mathbf{P}_{pu}$$

극소점(최적해)을 찾기 위해 이 편미분 값을 $0$으로 둡니다.

$$\left( \mathbf{z}_i - \hat{\mathbf{t}}_i \mathbf{P}_{pu}^T \right) \mathbf{P}_{pu} = 0$$

괄호를 전개하여 정리합니다.

$$\mathbf{z}_i \mathbf{P}_{pu} - \hat{\mathbf{t}}_i \mathbf{P}_{pu}^T \mathbf{P}_{pu} = 0$$

$$\mathbf{z}_i \mathbf{P}_{pu} = \hat{\mathbf{t}}_i \left( \mathbf{P}_{pu}^T \mathbf{P}_{pu} \right)$$

우변의 $\left(\mathbf{P}_{pu}^T \mathbf{P}_{pu}\right)$에 대한 역행렬을 양변의 오른쪽에 곱해주면 최종적으로 우리가 원하는 PMP 추정식을 얻게 됩니다.

$$\hat{\mathbf{t}}_i = \mathbf{z}_i \mathbf{P}_{pu} \left( \mathbf{P}_{pu}^T \mathbf{P}_{pu} \right)^{-1}$$

##### 6. 왜 $(\mathbf{P}_{pu}^T \mathbf{P}_{pu})^{-1}$ 보정이 필수적인가?

단순히 상식적인 투영을 생각하면 다음과 같은 식을 떠올리기 쉽습니다.

$$\hat{\mathbf{t}}_i = \mathbf{z}_i \mathbf{P}_{pu}$$

하지만 이 단순 투영이 최적해가 되기 위해서는 **$\mathbf{P}_{pu}$의 열벡터들이 서로 직교(Orthogonal)하고 크기가 1인 정규직교(Orthonormal) 상태**여야만 합니다. 즉, 다음 조건이 만족되어야 합니다.

$$\mathbf{P}_{pu}^T \mathbf{P}_{pu} = \mathbf{I} \quad \Longrightarrow \quad \left(\mathbf{P}_{pu}^T \mathbf{P}_{pu}\right)^{-1} = \mathbf{I}$$

전체 로딩 행렬 $\mathbf{P}$는 전체 변수 공간에 대해 서로 직교하도록 학습되어 구축됩니다 ($\mathbf{P}^T \mathbf{P} = \mathbf{I}$).

그러나 미래 미측정 변수 행들을 잘라내고 남겨진 **일부 가용 행렬 $\mathbf{P}_{pu}$는 더 이상 열벡터 간의 직교성이 유지되지 않습니다.** 따라서 축소로 인해 발생하는 변수 간의 정보 중복 및 공선성(Collinearity) 문제를 수학적으로 보정하기 위해 Gram Matrix의 역행렬인 $\left(\mathbf{P}_{pu}^T \mathbf{P}_{pu}\right)^{-1}$을 반드시 곱해주어야 합니다.

#### PMP 기반 MPC 예측 알고리즘 흐름

-  **현재 정보 주입 및 기본 스코어 추정 (PMP 단계):**    
	- 현재 시점의 공정 정보($\mathbf{x}_p$)와 사전에 약속된 기본 운전 기준($\mathbf{u}_n$)을 기반으로 기본 스코어 $\hat{\mathbf{t}}_i$를 추정합니다.    

$$\hat{\mathbf{t}}_i = \begin{bmatrix} \mathbf{x}_p & \mathbf{u}_n \end{bmatrix} \mathbf{P}_{pu} \left( \mathbf{P}_{pu}^{T}\mathbf{P}_{pu} \right)^{-1}$$

- **제어 입력 변경량 ($\Delta\mathbf{u}$) 영향 반영:**    
	- MPC가 최적화 변수로 결정할 MVT 제어 변경량 $\Delta\mathbf{u}$가 스코어에 미치는 영향을 스코어 공간의 가중치 $\mathbf{W}_u$를 사용해 더해줌으로써, 최종 예측 스코어 $\mathbf{t}_i$를 산출합니다.

$$\mathbf{t}_i = \hat{\mathbf{t}}_i + \Delta\mathbf{u} \mathbf{W}_u$$

- **품질 예측 및 제어 목적함수 계산:**
- 완성된 최종 예측 스코어 $\mathbf{t}_i$에 품질 로딩 행렬 $\mathbf{Q}^T$를 곱하여 최종 배치 품질 $\hat{\mathbf{y}}_i$를 예측하고, 이를 바탕으로 목적함수를 최적화하는 최적의 제어 변경량 $\Delta\mathbf{u}^*$를 구합니다.

$$\hat{\mathbf{y}}_i = \mathbf{t}_i \mathbf{Q}^T$$

---


대조적으로, TSR 방법은 트림된 스코어 $T_{pu}$로부터 최소제곱 추정 행렬(least squares estimator matrix) $B$를 통해 스코어 $T$를 재구성하려 하며, 이는 식 (18)에 나타난다.

$$T = T_{pu} B = X_{pu} W_{pu} B \tag{18}$$

- **트림된(Trimmed) 데이터 $X_{pu}$와 스코어 $T_{pu}$:**    
    - 과거의 완벽한 모델링 데이터 $X$ 중에서, 우리가 새로운 배치에서 **현재 알 수 있는 변수(과거 측정값 $x_p$와 조작변수 $u_n$)에 해당하는 열(Column)만 잘라낸(Trimmed) 데이터 행렬**을 $X_{pu}$라고 합니다.        
    - 마찬가지로 전체 가중치 행렬 $W$에서 해당 변수 부분만 잘라낸 것을 $W_{pu}$라고 합니다.        
    - 이 잘라낸 데이터만 곱해서 만든 임시 스코어를 트림된 스코어($T_{pu} = X_{pu} W_{pu}$)라고 부릅니다. 이 값은 불완전한 정보를 바탕으로 계산되었기 때문에 진짜 스코어 $T$와는 다릅니다.        
- **최소제곱 추정 행렬 $B$:**    
    - TSR의 핵심 아이디어는 "불완전한 스코어($T_{pu}$)를 입력하면 진짜 스코어($T$)가 나오게 하는 변환 공식($B$)을 만들자!"는 것입니다.        
    - 즉, $T \approx T_{pu} B$ 가 되도록 과거 데이터를 이용해 다중 선형 회귀(Multiple Linear Regression) 모델인 행렬 $B$를 학습시킵니다.


그런 다음 이 회귀 모델은 식 (19)에 나타난 것처럼 측정값이 결측된 새로운 배치의 스코어 벡터를 추정하는 데 사용될 수 있다.

$$t_i = \begin{bmatrix} x_p & u_n \end{bmatrix} W_{pu} \left( W_{pu}^T X_{pu}^T X_{pu} W_{pu} \right)^{-1} \times W_{pu}^T X_{pu}^T X W \tag{19}$$

#### 참고
이 길고 복잡해 보이는 수식은 사실 **새로운 데이터에 앞서 만든 회귀 모델 $B$를 곱해주는 과정**을 풀어쓴 것에 불과합니다.
1. **현재 배치의 불완전한 스코어 계산:**    
    - 현재 관측된 데이터 $\begin{bmatrix} x_p & u_n \end{bmatrix}$에 가중치 $W_{pu}$를 곱해 현재 배치의 트림된 스코어를 구합니다.        
    - $t_{pu, i} = \begin{bmatrix} x_p & u_n \end{bmatrix} W_{pu}$        
2. **행렬 $B$의 정체 (수학적 도출):**    
    - 회귀 분석에서 최소제곱법으로 $T \approx T_{pu} B$ 의 해를 구하면, $B = (T_{pu}^T T_{pu})^{-1} T_{pu}^T T$ 가 됩니다.        
    - 여기에 $T_{pu} = X_{pu} W_{pu}$ 이고 진짜 스코어 $T = X W$ 임을 대입하여 전개하면 식 (19)의 뒷부분이 만들어집니다.   

$$B = \left( (X_{pu} W_{pu})^T (X_{pu} W_{pu}) \right)^{-1} (X_{pu} W_{pu})^T (X W)$$

$$B = \left( W_{pu}^T X_{pu}^T X_{pu} W_{pu} \right)^{-1} W_{pu}^T X_{pu}^T X W$$

3. **최종 결론:**    
    - 새로운 배치의 예측 스코어 $t_i = t_{pu, i} \times B$ 입니다. 이를 합치면 논문의 식 (19)와 완전히 똑같아집니다.

--- 

이 방법은 데이터 행렬 $X$가 랭크(rank) $A$이고 모든 LV를 추출한 후 남은 오차가 없을 때 PMP 방법과 동등하다(Arteaga and Ferrer, 2002).

#### 참고
- **PMP와 TSR의 차이점:**    
    - **PMP**는 로딩 행렬($P$)의 기하학적 직교성을 이용해 관측된 데이터를 모델 평면에 투영(Projection)합니다.        
    - **TSR**은 가중치 행렬($W$)을 이용해 임시 스코어를 만든 뒤, 통계적인 회귀(Regression)를 통해 진짜 스코어를 예측합니다.        
    - 일반적인 상황(데이터에 노이즈가 있는 현실적인 상황)에서는 두 방법이 계산하는 $t_i$ 값이 미세하게 다릅니다.        
- **동등해지는 조건:**    
    - 만약 추출한 잠재 변수(LV, 주성분)의 개수 $A$가 실제 데이터 행렬 $X$의 정보(Rank)를 100% 완벽하게 설명할 수 있다면 어떨까요? (즉, PLS 모델의 잔차 오차 $E=0$ 인 완벽한 이상적 상태)        
    - 이러한 수학적 이상 조건에서는 PMP의 투영 계산과 TSR의 회귀 계산 결과가 수식적으로 완전히 일치(Equivalent)하게 된다는 것을 Arteaga와 Ferrer가 2002년 논문에서 증명했습니다.

#### TSR (Trimmed Score Regression)
- 배치 공정 제어(또는 다변량 통계 제어)에서 결측치가 발생했을 때, 이를 처리하여 **잠재 스코어(Latent Score)를 추정하는 또 다른 대표적 방법**
- PMP (Projection to the Model Plane)가 '현재 알고 있는 로딩 공간'에 데이터를 투영하는 방식이었다면, **TSR은 '부분 데이터로 구한 가짜 스코어'를 '진짜 스코어'로 변환하는 회귀 모델을 구축하는 방식**





### 5.3. 부피 제약 (Volume constraints)

부피를 최대 용량 아래로 유지하기 위한 제약은 Duran-Villalobos et al. (2016)에서 제안한 것과 유사하다. 그러나 사례 연구 시뮬레이션은 증발 속도(evaporation rate)에 더해 다수의 공급 및 배출 속도를 포함하며, 이들 모두가 부피에 영향을 미친다. 결과적으로, 부피에 영향을 미치는 다른 변수들의 영향 $E(V)$도 고려되었으며, 이는 식 (20)에 나타난다.

$$\sum_{k=1}^{K} \left[ u_n(k) + \Delta u(k) \right] \leq V_{max} - V_{ini} - E(V) \tag{20}$$

여기서 부피에 영향을 미치는 다른 변수들의 기댓값 $E(V)$는 초기 식별 데이터셋에서 최종 부피의 평균값으로 정의된다. 그 이유는, 실제 응용에서 증발 속도와 같이 부피에 영향을 미치는 일부 변수의 정확한 값을 알 수 없을 수 있기 때문이다.

MPLS 모델 식별 전 데이터의 평균 중심화에 따라, 식 (20)은 식 (21)과 같이 쓸 수 있다.

$$i_u \Delta u S_u \leq V_{max} - V_{ini} - \mu_V - i_u (\mu_u + S_u u_n) \tag{21}$$

여기서 $i_u$는 MVT와 동일한 길이를 갖는 1로 이루어진 벡터이고, $S_u$는 식별 데이터셋에서 MVT의 표준편차(standard deviation)로 이루어진 대각 행렬이며, $\mu_V$는 식별 데이터셋에서 최종 부피의 평균값이다.

$E(V)$를 식별 데이터셋의 평균값 $\mu_V$로 정의함으로써 계산에 작은 오차가 도입된다. 그러나 이에도 불구하고, 제안된 방법론은 본 논문에서 조사한 사례 연구에서 부피의 좋은 근사치를 얻었으며, 제약이 준수되도록 보장하였다. 이는 그림 3(Fig. 3)에서 예시될 수 있는데, 이 그림은 B2B 캠페인의 일부였던 50개 배치에 대한 용기 내 최종 부피를 보여준다.

### 5.4. 유효성 제약 (Validity constraints)

유효성 제약은 QP 해의 스코어 공간을, MPLS 모델을 식별하는 데 사용된 배치들로부터 수집된 데이터가 기술하는 영역으로 제한하기 위해 포함되었다. 이 목적에 유용한 방법론은 Laurí et al. (2014)에 제시된 경성 유효성 제약으로, 여기서 제약은 호텔링 $T^2$ 및 $Q$ 통계량에 부과된다.

$T^2$-통계량 기반 유효성 지표(validity indicator) $J_t$는 식 (22)에 나타나 있다. 이 유효성 지표는 식별 데이터셋이 포괄하는 스코어 영역으로부터 $t_i$의 편차(deviation)를 측정한다.

$$J_t = \frac{t_i \left( S_\alpha^2 \right)^{-1} t_i^T}{J_{t,max}} \tag{22}$$

여기서 $(S_\alpha^2)^{-1}$은 스코어 행렬 $T$에서 각 LV의 공분산을 담는 대각 행렬이고, $J_{t,max}$는 식별 데이터셋에서 $J_t$에 대한 정규화(normalization) 변수를 제공한다.

$Q$-통계량 기반 유효성 지표 $J_e$는 식 (23)에 나타나 있다. 이 유효성 지표는 예측 변수 벡터 $x_i$와 MPLS 모델로부터 재구성된 값 사이의 오차 측정치를 제공한다.

$$J_e = \frac{e_i e_i^T}{J_{e,max}} \tag{23}$$

여기서 $e_i$는 예측 변수의 투영 제곱 오차(squared error of projection)이고, $J_{e,max}$는 식별 데이터셋에서 $J_e$에 대한 정규화 변수를 제공한다.

Duran-Villalobos et al. (2016)에서 정식화된 QP 최적화를 위한 투영 제곱 오차는 미래 측정값에 대한 $\Delta u$의 효과를 추가함으로써 식 (24)에 나타난 것처럼 재정식화될 수 있다.

$$e_i = x'_i \left( I - W P^T \right) + \Delta u \left( I - W_u P_u^T \right) + \Delta u \theta \left( I - W_f P_f^T \right) \tag{24}$$

---
#### 수식 전개
- "새로운 제어 입력($\Delta u$)을 가했을 때, 공정이 정상 상태 모델(Model Plane)에서 얼마나 벗어나는가(Error)?"를 계산하는 식

##### 1. 기본 개념 및 변수 정의
PLS 모델에서 임의의 데이터 벡터 $x$가 주어졌을 때, 잠재 공간(Latent Space)에 투영하고 남은 잔차 오차 벡터 $e$는 다음과 같이 정의됩니다.

$$e = x - \hat{x} = x - t P^T$$

여기서 스코어 $t = x W$ 이므로, 이를 대입하면 투영 행렬(Projection Matrix)을 이용해 다음과 같이 쓸 수 있습니다.

$$e = x (I - W P^T)$$

현재 진행 중인 배치(Batch) $i$의 전체 궤적 벡터 $x_i$는 크게 세 부분으로 나눌 수 있습니다.
-  **$x_p$**: 과거부터 현재까지 측정된 변수    
- **$u$**: 조작 변수 (현재 및 미래의 제어 입력)    
- **$x_f$**: 미래의 공정 측정 변수    
##### 2. 제어 입력 변화($\Delta u$)에 따른 궤적 분해
MPC에서는 현재 설정된 기준 입력(Nominal MVT) $u_n$에 제어 변경량 $\Delta u$를 더하여 최적의 입력을 찾습니다.
이에 따라 미래 측정값 $x_f$ 역시 영향을 받아 변하게 됩니다. 이 동적 관계를 선형 모델인 $\theta$ (Step-response matrix 등)로 나타내면, 미래 측정값의 변화량은 **$\Delta x_f = \Delta u \theta$** 가 됩니다.
따라서 실제 전체 궤적 $x_i$는 명목상 궤적(Nominal Trajectory, $x'_i$)과 변화량 궤적($\Delta x$)의 합으로 분해할 수 있습니다.
- **명목상 궤적 ($x'_i$)**: 제어 변경이 없을 때의 기본 상태    $$x'_i = \begin{bmatrix} x_p & u_n & x_f \end{bmatrix}$$
- **실제 궤적 ($x_i$)**: 최적화가 반영된 상태

$$x_i = \begin{bmatrix} x_p & u_n + \Delta u & x_f + \Delta u \theta \end{bmatrix}$$

$$x_i = x'_i + \begin{bmatrix} 0 & \Delta u & \Delta u \theta \end{bmatrix}$$

##### 3. 투영 오차 식에 대입
이제 위에서 정의한 $x_i$를 PLS 오차 식 $e_i = x_i (I - W P^T)$에 대입합니다.

$$e_i = \left( x'_i + \begin{bmatrix} 0 & \Delta u & \Delta u \theta \end{bmatrix} \right) \left( I - W P^T \right)$$

이를 전개하면 다음과 같이 명목상 오차와 제어량 변화에 의한 오차 부분으로 나뉩니다.

$$e_i = x'_i (I - W P^T) + \begin{bmatrix} 0 & \Delta u & \Delta u \theta \end{bmatrix} (I - W P^T)$$

##### 4. 블록 행렬 분해 (Block-wise Decomposition)
가중치 행렬 $W$와 로딩 행렬 $P$ 역시 변수의 종류에 따라 과거($p$), 조작입력($u$), 미래($f$) 블록으로 나눌 수 있습니다.

$$W = \begin{bmatrix} W_p \\ W_u \\ W_f \end{bmatrix}, \quad P = \begin{bmatrix} P_p \\ P_u \\ P_f \end{bmatrix}$$

수학적 단순화와 QP 문제 구성을 위해, Duran-Villalobos et al. (2016) 논문에서는 제어 입력의 변화 $\Delta u$와 그 결과인 $\Delta u \theta$가 각각 자신이 속한 데이터 블록($u$ 블록과 $f$ 블록)의 투영 오차에 독립적으로 기여한다고 근사/분해(Decomposition)합니다.
- **$\Delta u$ 부분의 기여**: 조작 변수 공간에서의 투영 오차    
    $\Delta u \rightarrow \Delta u (I_u - W_u P_u^T)$    
- **$\Delta u \theta$ 부분의 기여**: 미래 측정 변수 공간에서의 투영 오차    
    $\Delta u \theta \rightarrow \Delta u \theta (I_f - W_f P_f^T)$
이를 앞서 전개한 식에 조합하면 최종 수식 유도 됨

---

여기서 미래 측정값은 결측 데이터 알고리즘으로부터 얻은 추정 스코어 벡터를 미래 측정값에 대응하는 로딩 값으로 투영하여 추정될 수 있다. 결과적으로, 예측 변수 벡터 $x'_i$는 식 (25)에 나타난 것처럼 구성될 수 있다.

$$\hat x_t = \begin{bmatrix} \hat x_t & u_n & \hat t_i P_f^T \end{bmatrix} \tag{25}$$

미래 측정값에 대한 $\Delta u$의 효과를 나타내는 추정기(estimator) $\theta$는 식 (26)에 나타난 것처럼 PMP 및 TSR 결측 데이터 알고리즘으로부터 얻어진다.

$$\theta_{PMP} = P_u \left( P_u^T P_u \right)^{-1} P_f^T$$

$$\text{Or}$$

$$\theta_{TSR} = W_u \left( W_u^T X_u^T X_u W_u \right)^{-1} W_u^T X_u^T X W P_f^T \tag{26}$$

앞서 언급한 바와 같이, $J_{t,max}$는 $T^2$-통계량 기반 유효성 지표에 대한 정규화 매개변수를 제공한다. 이 정규화는 QP 최적화에서 의사결정 공간을 유지하고자 하는 신뢰구간으로 표현될 수 있다. $T^2$-통계량에 대한 잘 알려진 상측 신뢰한계(upper confidence limit)는 Qin (2003)에 기술되어 있으며, 여기서 저자는 카이제곱 분포로 잘 근사될 수 있는 상측 관리한계(upper control limit)를 제시하였다. 이 근사는 데이터가 다변량 정규 분포(multivariate normal distribution)를 따른다는 조건에서만 가능하다. 그러면 정규화 변수 $J_{t,max}$는 식 (27)로 정의될 수 있다.

$$J_{t,max} = \chi^2_{A,\alpha} \tag{27}$$

여기서 $\chi^2$은 $A$ 자유도(degrees of freedom)와 유의 수준(significance level) $\alpha$(허용 오차, tolerance는 $1-\alpha$)를 갖는 카이제곱 분포이다.

한편, $J_{e,max}$는 $Q$-통계량 기반 유효성 지표에 대한 정규화 매개변수를 제공한다. 이 정규화도 QP 최적화에서 의사결정 공간을 유지하고자 하는 신뢰구간으로 표현될 수 있다. $Q$에 대한 상측 관리한계의 좋은 예는 Jackson et al. (1979)에 정식화되어 있다. 데이터가 정규 분포를 따른다는 가정 하에서, 이 관리한계는 정규 분포의 가우시안 근사(Gaussian approximation)로부터 계산되었다. 따라서 정규화 변수 $J_{e,max}$는 식 (28)로 정의될 수 있다.

$$J_{e\,max} = \delta^2_{A,\alpha} \tag{28}$$

여기서 $\chi^2$은 Qin (2003)에 정의된 정규 분포의 근사이다.

데이터가 정규 분포를 따른다는 가정은 이러한 관리한계의 단점인데, 모든 공정 데이터가 이 특성을 나타내지는 않기 때문이다. 예를 들어, 본 논문에서 제시하는 B2B 최적화 캠페인에서는 종점 품질이 한 배치에서 다음 배치로 변화하기 때문에 데이터의 확률 분포가 지속적으로 변화한다. 관측값의 이러한 변화는 무작위가 아니며, 데이터가 비정규(non-normal) 분포를 갖게 한다. 본 연구에서는 이를 콜모고로프-스미르노프 검정(Kolmogorov-Smirnov test)을 사용하여 확인하였다(Ramani, 1974).

데이터의 분포에 대한 가정을 하지 않는, 신뢰구간을 정의하는 보다 일반적인 접근법은 Desharnais et al. (2015)에 기술되어 있으며, 여기서 저자는 부트스트랩 재표본추출(bootstrap-resampling) 기법을 사용하여 비정규 데이터셋에서 신뢰구간을 계산한다. 이 기법은 경험적 분포 함수(empirical distribution function)로부터 신뢰구간을 추론하며, 모집단으로부터 추출된 수집 데이터가 모집단의 가장 좋은 이용 가능한 대표(representatives)라고 가정한다. 신뢰구간은 원본 데이터셋으로부터 개별적으로 무작위 선택된 표본으로 형성되는 '재표본추출된(resampled)' 데이터셋으로부터 추정된다.

정규화 변수 $J_{t,max}$와 $J_{e,max}$는 각각 식 (29)와 (30)에 나타난 것처럼 정의될 수 있다.

$$J_{t,max} = \beta_{nb,\alpha} \, \text{diag}\left( T \left( S_\alpha^2 \right)^{-1} T^T \right) \tag{29}$$

$$J_{e,max} = \beta_{nb,\alpha} \, \text{diag}\left( E E^T \right) \tag{30}$$

여기서 $\beta$는 부트스트랩 재표본추출을 사용한 상측 신뢰구간 계산이고(Desharnais et al., 2015), $nb$는 재표본 데이터셋의 개수(일반적으로 1000–10,000)이다.

식 (27)–(30)을 사용하면, 유효성 제약은 식 (31)과 (32)에 나타난 비선형 부등식 제약(nonlinear inequality constraints)으로 정식화될 수 있다.

$$\frac{J_t}{J_{t,max}} \leq 1 \tag{31}$$

$$\frac{J_e}{J_{e,max}} \leq 1 \tag{32}$$

$Q$ 및 $T^2$ 통계량 모두 공정 모니터링에 사용되지만, 이들이 공정 모니터링에서 서로 다른 역할을 제공한다는 점을 지적할 필요가 있다. $Q$-통계량은 특정 배치의 예측 변수 상관 일관성(correlation consistency)을 식별 데이터셋과 비교하여 측정하는 반면, $T^2$-통계량은 LV 부분공간(subspace)에서 원점까지의 거리를 측정한다.

---
#### 참고
- 위의 내용은 **통계적 공정 관리(Statistical Process Control, SPC)** 또는 다변량 데이터 분석 모델(예: PCA, PLS)에서, 데이터가 정규분포를 따르지 않을 때 관리 한계선(Control Limits, 또는 신뢰구간)을 어떻게 설정할 것인지에 대한 방법론을 설명
- **부트스트랩(Bootstrap) 기법**을 사용하여 비모수적(Non-parametric, 데이터 분포에 대한 가정 없음)으로 신뢰구간을 구하는 과정 설명

##### 1. 왜 부트스트랩(Bootstrap)을 사용하는가?
전통적인 통계 공정 관리에서는 보통 데이터가 **정규분포(종 모양의 곡선)를 따른다고 가정**합니다. 그래야 $T^2$ 통계량이나 $Q$ 통계량(또는 잔차 오차 $E$)에 대한 관리 한계선을 수학적(예: $F$-분포나 $\chi^2$ 분포)으로 쉽게 계산할 수 있기 때문입니다.
하지만 실제 현장의 데이터는 한쪽으로 쏠려있거나(Skewed) 극단값이 많아 정규분포를 따르지 않는 경우가 많습니다.
- **해결책: 부트스트랩 재표본추출 (Bootstrap-resampling)**    
	- 부트스트랩 기법은 "우리가 수집한 현재의 데이터(표본)가 실제 전체 데이터(모집단)의 특성을 가장 잘 대표한다"고 가정합니다.
	- 따라서 복잡한 수학적 분포를 가정하는 대신, 우리가 가진 원본 데이터 안에서 '무작위 복원 추출(중복 허용)'을 수천 번 반복하여 수많은 '가짜 데이터셋(Resampled datasets)'을 만들어냅니다.
	- 이 수많은 가짜 데이터셋들을 바탕으로 통계량의 '경험적인 분포(Empirical distribution)'를 직접 그리고, 그 분포에서 상위 95% 또는 99% 위치를 찾아내어 그것을 관리 한계선(신뢰구간)으로 삼는 것입니다.
##### 2. $J_{t,max}$ 와 $J_{e,max}$ 의 의미
주어진 수식은 스코어 공간(Score space)과 잔차 공간(Residual space)에서 정상 상태의 최대 허용치를 정의하는 식입니다. 보통 $Hotelling's T^2$ 통계량 관리상한과 $SPE$ (또는 $Q$) 통계량 관리상한과 같은 역할을 합니다.
###### 식 (29) 스코어 공간의 최대 한계: $J_{t,max}$

$$J_{t,max} = \beta_{nb,\alpha} \, \text{diag}\left( T \left( S_\alpha^2 \right)^{-1} T^T \right) \tag{29}$$

- **$T \left( S_\alpha^2 \right)^{-1} T^T$**: 모델에서 얻은 스코어 행렬 $T$와 그 공분산 행렬 $S_\alpha^2$를 이용해 계산된 일종의 거리를 나타냅니다. 정규분포 가정 하에서의 마할라노비스 거리($Hotelling's T^2$의 핵심 부분)와 유사합니다.
- **$\text{diag}( \dots )$**: 행렬의 대각 성분만 추출합니다. 즉, 각 관측치(샘플)별로 계산된 자기 자신의 거리 값들만 가져옵니다.
###### 식 (30) 잔차 공간의 최대 한계: $J_{e,max}$

$$J_{e,max} = \beta_{nb,\alpha} \, \text{diag}\left( E E^T \right) \tag{30}$$

- **$E E^T$**: 모델이 설명하지 못하고 남은 잔차 오차 행렬 $E$의 제곱 합을 의미합니다. 스코어 공간으로 설명되지 않는 나머지 노이즈나 이상 변동의 크기를 나타냅니다 (보통 $Q$ 통계량이나 $SPE$로 불림).
- **$\text{diag}( \dots )$**: 각 관측치별 잔차의 크기(에러의 분산)를 나타냅니다.

##### 3. 부트스트랩 연산자 $\beta_{nb,\alpha}$의 역할 (베타 분포(Beta distribution) 아님)
가장 중요한 부분은 두 수식 앞에 공통으로 붙어있는 **$\beta_{nb,\alpha}$** 입니다.
- 이 기호는 단순한 숫자가 아니라, 괄호 안의 데이터 배열(행렬의 대각 성분들)을 입력받아 부트스트랩 상측 신뢰구간(Upper confidence limit)을 계산해 내는 수학적 함수(작업)를 의미합니다.    
- **$nb$**: 재표본추출(Resampling)을 몇 번 반복할 것인지를 나타냅니다. 본문에서는 "일반적으로 1000 ~ 10,000번"이라고 설명하고 있습니다. 무작위 뽑기를 만 번 반복해서 신뢰성 있는 분포를 만든다는 뜻입니다.    
- **$\alpha$**: 유의수준(Significance level)입니다. 예를 들어 $\alpha = 0.05$ (또는 5%)라면, 부트스트랩으로 만든 10,000개의 값들 중에서 가장 큰 쪽에서 5% 위치에 해당하는 컷오프(Cut-off) 값을 찾는다는 의미입니다. (상위 95% 백분위수)

확률 밀도 함수인 베타 분포: $Beta(a, b)$


---

## 6. 결과 및 논의 (Results and discussion)

이 절에 제시된 결과는 공정에 변동성을 도입하기 위해 Matlab에서 사용된 것과 동일한 시작 시드(starting seed)를 난수 생성기에 사용한다. 이는 생성된 난수가 각 접근법에 대해 동일하기 때문에, 주어진 제어 캠페인에 대해 서로 다른 접근법을 정확하게 비교할 수 있게 한다.

초기 MPLS 모델을 식별하는 데 사용된 초기 사전 최적화 공급(initial pre-optimised feed)은 B2B 및 MPC 캠페인 모두에 대해 명목 공급 궤적(nominal feed trajectory)을 갖는 5개 배치로 구성되었다. 이 명목 공급 궤적은 처음 4 h 동안 0 l/h에서 50 l/h로 점진적으로 증가한 다음, 배치의 나머지 동안 50 l/h의 일정한 값으로 구성되었다. 그런 다음 필터링된(Duran-Villalobos et al., 2016) +/−25 l/h의 PRBS가 일정한 공급에 더해졌다.

실험에 사용된 기타 매개변수는 다음과 같다.

- 저역 통과 필터 특성: 최대 주파수(나이퀴스트 주파수, Nyquist frequency)의 10% 차단 주파수를 갖는 영위상(Zero-phase) 저역 통과 유한 임펄스 응답(FIR) 필터.
- 액추에이터(actuator)에 대한 하한 제약 = 0 l/h.
- 상한 제약 = 200 l/h.
- 부트스트랩 계산을 위한 $nb$ = 2000.
- 신뢰 허용 오차 97%, 따라서 $\alpha = 0.03$.

### 6.1. B2B 캠페인의 유효성 제약 (Validity constraints in the B2B campaign)

B2B 최적화의 목표는 설탕 공급 유량(sugar feed flow rate, 조작 변수)의 궤적을 한 배치에서 다음 배치로 최적화함으로써, 최종 페니실린 농도(종점 품질)를 사전 설정된 설정값(30 g/l)으로 가져오는 것이었다. 본 논문에서 제시하는 연구의 중요한 측면은 B2B 캠페인에서 유효성 제약의 효과를 관찰하는 것이었다.

그림 4(Fig. 4)는 전형적인 B2B 캠페인 동안 기질 공급(substrate feed)의 궤적이 어떻게 변화했는지를 보여준다. 이 그림에서 두드러지는 점은 최적화 초기(배치 1에서 6, 그리고 배치 6에서 10)의 MVT 진폭의 급격한 변화와 그 이후(배치 20에서 50)의 매우 완만한 변화이다. 다시 말해, 궤적은 처음 10개 배치에 대해 비교적 빠르게 수렴한다.

B2B 캠페인의 최종 페니실린 농도에 대한 결과는 수율 향상의 진행에서 무작위 변동성의 효과를 관찰하기 위해 30회 반복 실험(replicated experiments)에서 수집되었다. 각 반복은 서로 다른 초기 난수 시드를 가지고 50개 배치에서 결과를 수집하였다.

그림 5(Fig. 5)는 TSR 결측 데이터 기법을 사용한 B2B 최적화 캠페인에 대해, 명목 실행(nominal run)과 3가지 서로 다른 유효성 제약 배열의 30회 반복 평균 최종 페니실린 농도를 보여준다. 이 그림에서 $Q$-통계량에 대한 유효성 지표 $J_e$만 적용될 때 가장 빠른 수렴과 가장 높은 수율이 달성됨을 관찰할 수 있다. 그림 5는 또한 이 유효성 제약을 통해 최종 페니실린 농도가 약 30 g/l까지 점진적으로 증가함을 보여준다.

표 3(Table 3)은 그림 5에 표시된 결과에서 취한 몇 가지 중요한 평가 매개변수를 보여주고, 이를 개루프(open-loop) 제어가 적용된 경우의 결과와 비교한다. 두 번째 열은 50번째 배치에 대해 30회 반복 각각에 걸쳐 평균한 최종 페니실린 농도의 평균을 보여준다. 세 번째 열은 50번째 배치에 대한 30회 반복의 최종 페니실린 농도 표준편차를 보여준다. 마지막으로, 네 번째 열은 최종 페니실린 농도가 최대 정규값(maximum regular value)으로 수렴하는 배치를 보여준다.

그림 5와 표 3의 결과로부터, $J_e$만 사용할 때 공정이 다른 제약이 사용되었을 때나 공정이 개루프로 운전되었을 때보다 설정값(30 g/l)에 더 가까운 값으로 수렴함을 관찰할 수 있다. 이 구성은 또한 캠페인 종료 시 가장 낮은 표준편차를 갖는다. 대조적으로, 두 유효성 제약을 모두 포함하는 구성은 가장 낮은 수렴 속도와 가장 높은 표준편차를 갖는다.

$T^2$-통계량에 부과된 유효성 제약 $J_t$에 의해 야기되는 이 높은 변동성은 각 MPLS 모델 갱신에서 사용되는 식별 데이터의 넓은 비정상(non-stationary) 범위로 설명될 수 있다. 이는 또한 Qin (2012)에 의해서도 관찰되었는데, 그는 공정 데이터의 스코어가 다변량 정규성(multivariate normality)의 가정을 따르지 않을 때 $T^2$에 대한 한계가 실제로 신뢰할 수 없다고 진술한다. 따라서 $Q$에 대한 한계는 $T^2$에 대한 한계와 비교하여 제1종 및 제2종 오류(type I and type II errors)를 줄일 수 있다(Qin, 2003). 이는 이 유해한 효과를 보이지 않은 MPC의 실험 결과로 입증되었다.

데이터셋에서 정규 분포를 가정할 때 신뢰구간의 사용과 관련하여, 그림 6(Fig. 6)은 TSR을 사용하여 3가지 서로 다른 신뢰구간이 B2B 최적화 캠페인에 적용되었을 때 30회 반복의 평균 최종 페니실린 농도를 보여준다. 정규 분포를 가정한 방법론은 신뢰구간에 식 (27)과 (28)을 사용하였으며, 정규 분포를 가정하지 않은 방법론은 식 (29)와 (30)을 사용하였다.

표 4(Table 4)는 그림 6에 표시된 결과에서 취한, 서로 다른 신뢰구간 방법론 하의 B2B-TSR 캠페인에 대해 표 3과 동일한 평가 매개변수를 보여준다.

그림 6과 표 3으로부터, 데이터셋이 정규 분포를 갖는다고 가정하고 유효성 제약 $J_e < 1$을 갖는 구성의 결과가, 데이터셋이 정규 분포를 갖는다고 가정하지 않은 구성의 결과보다 훨씬 낮은 수렴 속도와 높은 표준편차를 가짐을 관찰할 수 있다. 후자의 결과는 유효성 제약 $J_e < 4$를 갖고 데이터셋이 정규 분포를 갖는다고 가정한 결과와 유사하다. 이 결과는 데이터가 다변량 정규 분포를 따른다는 가정으로 인해 QP 최적화 공간이 지나치게 제약됨을 시사한다.

B2B 최적화에서 유효성 제약을 사용하는 문제는 종종 MVT 최적화에서 실행 불가능한 문제(infeasible problems)로 이어질 수 있다는 점이다. 이는 부록 B(Appendix B)에 제시된 두 번째 사례 연구와 이전 연구(Duran-Villalobos et al., 2016)에서 유효성 제약을 사용할 때 관찰된 저조한 성능과 실패한 최적화를 살펴봄으로써 발견되었다. 이 문제에 대한 가능한 설명은 스코어 공간의 변화하는 조건과 한 배치에서 다음 배치로의 원료 변동성으로 인해 문제가 지나치게 제약된다는 것이다.

**표 3 (Table 3).** 서로 다른 유효성 제약 구성 하의 B2B-TSR 캠페인에 대한 평가 매개변수.

| 제어 방법론 (Control methodology)                             | 수율: 배치 50 평균 (Yield: mean of batch 50) | 산포: 배치 50 표준편차 (Dispersion: standard deviation of batch 50) | 수렴이 달성된 배치 (Batch at which convergence achieved) |
| -------------------------------------------------------- | -------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------ |
| 명목 실행(오픈루프) (Nominal run, Open-loop)                     | 21.84 g/l                              | 1.22 g/l                                                    | 해당 없음(n/a)                                       |
| 유효성 제약 없는 B2B-TSR (B2B-TSR without validity constraints) | 29.31 g/l                              | 1.83 g/l                                                    | ≈배치 20                                           |
| B2B-TSR $J_e < 1$                                        | 30.12 g/l                              | 1.63 g/l                                                    | ≈배치 15                                           |
| B2B-TSR $J_e < 1$, $J_t < 1$                             | 27.16 g/l                              | 4.98 g/l                                                    | ≈배치 30                                           |

**표 4 (Table 4).** 서로 다른 신뢰구간 방법론 하의 B2B-TSR 캠페인에 대한 평가 매개변수.

|제어 방법론 (Control methodology)|수율: 배치 50 평균 (Yield: mean of batch 50)|산포: 배치 50 표준편차 (Dispersion: standard deviation of batch 50)|수렴이 달성된 배치 (Batch at which convergence achieved)|
|---|---|---|---|
|B2B-TSR $J_e < 1$|30.12 g/l|1.63 g/l|≈배치 15|
|B2B-TSR 정규 분포(Normal dist.) $J_e < 1$|27.00 g/l|4.80 g/l|≈배치 35|
|B2B-TSR 정규 분포(Normal dist.) $J_e < 4$|30.10 g/l|1.64 g/l|≈배치 15|

### 6.2. B2B 최적화 캠페인의 결측 데이터 알고리즘 (Missing data algorithms in the B2B optimisation campaign)

본 논문에서 제시하는 연구의 또 다른 관심사는 B2B 최적화 캠페인에 걸쳐 종점 품질의 추정에서 서로 다른 결측 데이터 알고리즘의 사용을 비교하는 것이다.

그림 7(Fig. 7)은 IndPenSim B2B 최적화 캠페인에 대해 2가지 서로 다른 결측 데이터 알고리즘(PMP 및 TSR)의 30회 반복 평균 최종 페니실린 농도를 보여준다. 두 방법론 모두 데이터셋에서 다변량 정규 분포의 가정 없이 유효성 제약 $J_e < 1$을 사용한다. 추가로, 표 5(Table 5)는 그림 7에 표시된 결과와 관련된 일련의 지표(metrics)를 보여준다.

그림 7과 표 5는 B2B 캠페인에서 QP 최적화기에 적용되었을 때 PMP 또는 TSR을 사용하여 얻은 결과에 유의한 차이가 없음을 보여준다. 이러한 결과의 유사성은 잔차가 무시할 만할 때 두 방법의 동등성에 기인할 수 있다.

B2B 캠페인의 결과는 수율에서 유의한 향상을 보인다. 이 향상은 평균값 21.84 g/l에서 약 30 g/l로 나아간다. 또한 이 향상은 매우 빠르게 일어나는데, B2B 캠페인이 시작된 후(제어 조치가 시작된 후 5개 배치) 처음 10개 배치에 대해 수율이 급격히 증가한 다음, 여러 배치에 걸쳐 수율이 점진적으로 향상된다. 마찬가지로, 그림 3에서 부피는 배치 10까지 최적화가 허용하는 최대 부피에 도달한다. 이는 MVT의 부피와 수율 사이의 강한 연결을 시사하며, 이는 예상되는 바이다.

**표 5 (Table 5).** 서로 다른 결측 데이터 알고리즘 하의 B2B 캠페인에 대한 평가 매개변수.

|제어 방법론 (Control methodology)|수율: 배치 50 평균 (Yield: mean of batch 50)|산포: 배치 50 표준편차 (Dispersion: standard deviation of batch 50)|수렴이 달성된 배치 (Batch at which convergence achieved)|
|---|---|---|---|
|B2B-PMP|30.13 g/l|1.64 g/l|≈배치 15|
|B2B-TSR|30.12 g/l|1.63 g/l|≈배치 15|

### 6.3. MPC 캠페인의 결측 데이터 알고리즘 (Missing data algorithms in the MPC campaign)

앞서 언급한 바와 같이, MPC 캠페인은 원료의 초기 변동성과 공정의 배치 내 변동이 존재하는 상황에서 최종 페니실린 농도의 배치 대 배치 변동을 줄이는 목표를 가졌다. 이 목표는 배치 진행 중 설탕 공급 유량의 궤적을 반복적으로 측정하고 최적화함으로써 달성되었다. 예를 들어, 그림 8(Fig. 8)은 MPC 캠페인의 전형적인 배치 동안 기질 공급 속도의 진행을 보여준다. 이 그래프는 이 배치 동안 '골든 궤적(golden trajectory)'에 작은 변화만 이루어졌음을 보여준다. 골든 궤적은 (Goldrick et al., 2015)에서 제안된 최적 공급 프로파일(feeding profile)이었다.

MPC가 적용되었을 때 80개 배치 동안 이루어진 최종 페니실린 농도 측정값이 수집되었다. 각 배치에서 18개의 제어 지점이 적용되었다. 제어 조치는 각 배치 시작 후 50 h에 시작되어 배치가 끝날 때까지 10 h마다 반복되었다. 각 제어 지점에서 사용된 QP 최적화는 $T^2$와 $Q$ 모두에 유효성 제약을 사용하였는데, B2B 캠페인에 존재했던 $T^2$-통계량 기반 유효성 제약의 유해한 효과가 MPC 캠페인에서는 관찰되지 않았기 때문이다. 유효성 제약은 데이터셋에 다변량 정규 분포가 있다고 가정하지 않고 정의되었다.

그림 9(Fig. 9)는 전형적인 배치에 대해 두 결측 데이터 알고리즘(PMP 및 TSR)이 모두 적용되었을 때 IndPenSim MPC 캠페인의 최종 페니실린 농도를 보여준다. 이 그래프는 MPC 캠페인에 걸쳐 최종 페니실린 농도의 변동성이 점진적으로 감소함을 보여준다.

표 6(Table 6)은 그림 9에 표시된 결과에서 취한 몇 가지 지표를 강조한다. 첫 번째 열은 MPC 캠페인 동안의 최종 페니실린 농도를 제시한다. 이 지표는 MPC 캠페인 동안 존재할 수 있는 설정값으로부터의 편향(bias)을 기록한다. 두 번째 열은 MPC 캠페인 동안 실제 종점 품질의 설정값 대비 평균 제곱 오차(Mean Square Error, MSE)를 제시한다. 이 매개변수는 MPC 캠페인 동안 설정값으로부터의 산포(dispersion) 측정치이다.

표 6의 결과는 그림 9의 결과와 함께, QP 최적화에서 PMP 또는 TSR 알고리즘을 사용하는 데 유의한 차이가 없음을 드러낸다. 결과는 또한 MPC가 적용된 캠페인에서 평균 수율과 MSE의 명확한 향상을 보여준다.

**표 6 (Table 6).** 서로 다른 결측 데이터 알고리즘 하의 B2B 캠페인에 대한 평가 매개변수.

|제어 방법론 (Control methodology)|평균 수율 (Yield average)|설정값 대비 MSE (MSE from the set-point)|
|---|---|---|
|제어 없음 (No control)|29.48 g/l|1.32 g/l|
|MPC-PMP|30.05 g/l|0.99 g/l|
|MPC-TSR|29.99 g/l|1.08 g/l|

_(역자 주: 표 6의 표제는 원문에 "B2B campaign under different missing data algorithms"로 표기되어 있으나, 본문 내용에 따르면 MPC 캠페인의 결측 데이터 알고리즘 비교 결과이다. 두 번째 열은 원문 본문 설명상 MPC 캠페인 동안의 최종 페니실린 농도(평균 수율)를, 세 번째 열은 설정값 대비 MSE를 나타낸다.)_

### 6.4. B2B 캠페인 이후의 MPC 캠페인 (MPC campaign after B2B campaign)

이 절에 제시된 결과는 Goldrick et al. (2015)에서 식별된 '골든 궤적'을 사용한 MPC 캠페인의 성능을, B2B-TSR 캠페인에 따라 결정된 최종 궤적과 비교한다. 이 비교의 목표는 광범위한 배치 집합을 갖는 MPLS 모델을 사용하는 효과와 서로 다른 '골든' 궤적을 사용할 때 MPC 성능의 재현성(reproducibility)을 관찰하는 것이다.

그림 10(Fig. 10)은 6.3절의 '골든 궤적' 공급을 사용한 IndPenSim MPC 캠페인의 최종 페니실린 농도를, B2B-TSR 접근법을 사용하여 최적화된 공급 궤적과 비교한다. 난수 생성기에 동일한 시드를 사용하여 접근법을 비교하기 위해, MPC-TSR이 모델을 초기화하는 데 5개 배치의 데이터를 필요로 하므로 그림 10에 표시된 배치 번호는 배치 6부터 시작한다. 그래프는 B2B-TSR 기법을 사용하여 공정이 최적화된 후 MPC 캠페인 초기에 변동성이 약간 적음을 보여준다.

표 7(Table 7)은 그림 10에 표시된 결과에서 취한, 표 6과 동일한 평가 매개변수를 보여준다. 이 표는 두 접근법의 수율에 유의한 차이가 없음을 보여준다. 그러나 이 표는 B2B-TSR 최적화 이후에 나타나는 MSE의 감소를 강조한다.

MPC 캠페인 결과에서 두드러지는 점은 최종 페니실린 농도 평균의 약간의 향상으로, 명목 실행의 29.48 g/l 값에서 30 g/l에 매우 가까운 값으로 이동한다. 마찬가지로, MPC를 적용했을 때의 일관성은 설정값 대비 MSE를 명목 실행의 1.32 g/l 값에서 MPC가 적용되었을 때 1 g/l에 가까운 값으로 줄임으로써 상당히 향상되었다.

MSE는 B2B 캠페인의 데이터셋을 사전에 사용했을 때 0.69 g/l로 더욱 향상되었다. 이에 대한 가능한 설명은 MPLS 모델이 첫 MPC 실행에 대해 훨씬 더 정확하다는 것이다. 이는 그림 10에서 추론할 수 있는데, 여기서 MPC-TSR 기법이 B2B-TSR 캠페인 데이터셋을 사용할 때, B2B-TSR 캠페인 없이 사용할 때보다 훨씬 적은 변동성을 보이는 반면, MPC 캠페인 종료 시의 변동성은 두 접근법에서 거의 차이를 보이지 않는다.

**표 7 (Table 7).** 서로 다른 결측 데이터 알고리즘 하의 B2B 캠페인에 대한 평가 매개변수.

|제어 방법론 (Control methodology)|평균 수율 (Yield average)|설정값 대비 MSE (MSE to the set-point)|
|---|---|---|
|MPC-TSR|29.99 g/l|1.08 g/l|
|MPC-TSR + B2B-TSR|29.92 g/l|0.69 g/l|

---

## 7. 결론 (Conclusions)

본 논문에서는 개선된 B2B 최적화 전략이 산업용 유가식 페니실린 시뮬레이션에 성공적으로 구현되어, 명목 사전 최적화 공급 궤적으로부터 수율을 크게 향상시켰다. 결과는 이 제어 전략이 최적 MVT로 수렴하여, 초기 모델을 식별하는 데 단 5개의 배치만 사용하고도 10개 배치 후에 원하는 종점 품질에 일관되게 도달함을 보여주었다.

혁신적인 모델 예측 제어(MPC) 전략이 동일한 시뮬레이션에 성공적으로 적용되었다. 이 제어기는 수율의 값을 설정값에 더 가깝게 가져오고 여러 실행에 걸쳐 공정 변동성을 줄였다. 이 제어 전략의 주요 장점은 배치를 따라 여러 시점에서 공급 전략 속도의 조정을 통해 원료 품질의 B2B 변동과 공정 변동의 영향을 줄일 수 있는 능력이었다.

QP를 사용하여 MVT를 최적화할 때 적용된 서로 다른 결측 데이터 알고리즘의 성능과 관련하여, 배치를 통한 종점 품질을 추정하는 데 TSR 또는 PMP를 사용할 때 결과는 상당한 차이를 보이지 않았다. 그러나 PMP는 보다 직관적인 해석을 가지며 더 적은 계산 능력을 요구한다.

QP의 유효성 제약에 제안된 신뢰한계를 적용하는 이점과 관련하여, 부트스트랩 계산을 사용했을 때 B2B 캠페인의 결과가, 데이터셋이 다변량 정규 분포를 갖는다고 고려한 다른 문헌의 접근법을 사용했을 때보다 향상되었다. 이 발견은 유효성 제약에 부트스트랩 계산을 적용하는 것이, 일반적으로 튜닝을 요구하는 다른 기법보다 더 강건한 접근법을 제공함을 시사한다. 이러한 결과에도 불구하고, 이전의 발견과 부록 B에 제시된 두 번째 사례 연구는 B2B 최적화에서의 유효성 제약 사용과 원료의 변화하는 초기 조건이 실행 불가능한 QP 문제로 이어질 수 있음을 시사한다.

본 연구는 제안된 제어 전략을 함께 또는 개별적으로 산업용 유가식 공정에 적용하는 것이, 플랜트 및 원료 변동성이 존재하는 상황에서 향상된 일관성과 수율로 이어질 것임을 시사한다.

---

## 자금 지원 (Funding)

본 연구는 영국 공학및물리과학연구위원회(UK Engineering & Physical Sciences Research Council, EPSRC) [EP/P006485/1]와, UCL 생화학공학부(UCL Biochemical Engineering)가 영국 대학들과 협력하여 주관하는 미래 표적 헬스케어 제조 허브(Future Targeted Healthcare Manufacturing Hub)의 산업 사용자 및 부문 조직 컨소시엄의 지원을 받았다.

## 이해 상충 선언 (Declaration of Competing Interest)

없음(None).

## 보충 자료 (Supplementary material)

본 논문과 관련된 보충 자료는 온라인 버전에서 doi:10.1016/j.compchemeng.2019.106620 에서 찾을 수 있다.

---

## 그림 설명 (Figure captions)

- **그림 1 (Fig. 1).** 배치 대 배치(B2B) 최적화 흐름도(flowchart). _(흐름도 내용: ① 초기 데이터셋을 수집하고 MPLS 모델을 구축한다 → ② $i$번째 배치의 초기 조건을 측정하고 최적 MVT를 계산한다 → ③ $i$번째 배치를 실행하고 데이터를 수집하여 MPLS 모델을 갱신한다 → ④ 다음 반복에 사용할 명목 MVT를 찾는다(식 13). 이후 ②로 되돌아가 반복한다.)_
- **그림 2 (Fig. 2).** 모델 예측 제어(MPC) 흐름도. _(흐름도 내용: ① 초기 데이터셋을 수집하고 MPLS 모델을 구축한다 → ② $i$번째 배치에서 $m$번째 제어 지점의 측정값을 얻고 최적 MVT를 계산한다 → ③ 다음 제어 지점 $m+1$까지 $i$번째 배치를 실행한다 → 판단 분기(배치가 끝나지 않았으면 ②로 되돌아감) → ④ $i$번째 배치 종료 시 데이터를 수집하고 MPLS 모델을 갱신하며, 첫 번째 제어 지점까지 다음 배치를 실행한다.)_
- **그림 3 (Fig. 3).** B2B 최적화 캠페인에 대한 부피 제약. _(50개 배치에 대한 용기 내 최종 부피[l]를 배치 번호에 따라 표시. 부피 제약이 있는 B2B 최적화와 부피 제약이 없는 B2B 최적화 두 곡선을 비교하며, 두 경우 모두 약 배치 10까지 최대 부피에 도달함.)_
- **그림 4 (Fig. 4).** B2B-TSR 최적화 캠페인에 대한 MVT 진행. _(시간[h]에 따른 설탕 유량[l/h]을 배치 1, 6, 10, 20, 50에 대해 비교.)_
- **그림 5 (Fig. 5).** 서로 다른 유효성 제약 구성 하의 B2B-TSR 캠페인에 대한 최종 페니실린 농도 평균.
- **그림 6 (Fig. 6).** 서로 다른 신뢰구간 방법론 하의 B2B-TSR 캠페인에 대한 최종 페니실린 농도 평균.
- **그림 7 (Fig. 7).** 서로 다른 결측 데이터 알고리즘 하의 B2B 캠페인에 대한 최종 페니실린 농도 평균.
- **그림 8 (Fig. 8).** MPC를 사용한 전형적인 배치에 대한 '골든' MVT 진행. _(시간[h]에 따른 설탕 유량[l/h]을 초기(Initial), 제어 50h·80h·100h·220h에 대해 비교.)_
- **그림 9 (Fig. 9).** 서로 다른 결측 데이터 알고리즘 하의 MPC 캠페인에 대한 최종 페니실린 농도. _(배치 번호에 따른 최종 페니실린 농도[g/l]. MPC 시작 지점, 설정값(Set-point), 비제어(Non controlled), MPC-PMP, MPC-TSR을 비교.)_
- **그림 10 (Fig. 10).** 서로 다른 제어 전략 하의 MPC 캠페인에 대한 최종 페니실린 농도. _(배치 번호에 따른 최종 페니실린 농도[g/l]. 설정값(Set-point), MPC-TSR, B2B-TSR 이후의 MPC-TSR(MPC-TSR after B2B-TSR)을 비교.)_

_(역자 주: 사용자 요청 형식에 따라 그림 자체는 본문에 삽입하지 않았으며, 그림 설명만 번역하여 정리하였다. 흐름도(그림 1, 2)의 상자 내 텍스트는 원문에서 판독 가능한 범위 내에서 요약 없이 옮겼다.)_

---

## 참고문헌 (References)

Arteaga, F., Ferrer, A., 2002. Dealing with missing data in MSPC: several methods, different interpretations, some examples. _J. Chemom._ 408–418. doi:10.1002/cem.750.

Birol, G., Undey, C., Cinar, A., 2002. A modular simulation package for fed-batch fermentation: penicillin production. _Computers and Chemical Engineering_ 26, 1553–1565. doi:10.1016/S0098-1354(02)00127-8.

Bonvin, D., 1998. Optimal operation of batch reactors - a personal view. _J. Process Control_ 8, 355–368.

Bonvin, D., Srinivasan, B., Hunkeler, D., 2006. Control and optimization of batch processes: improvement of process operation in the production of specialty chemicals. _IEEE Control Syst. Mag._ 34–45. doi:10.1109/MCS.2006.252831.

Camacho, J., Lauri, D., Lennox, B., Escabias, M., Valderrama, M., 2015. Evaluation of smoothing techniques in the run to run optimization of fed-batch processes with u-PLS. _J. Chemom._ 29, 338–348. doi:10.1002/cem.2711.

Camacho, J., Pico, J., Ferrer, A., 2007. Self-tuning run to run optimization of fed batch processes using unfold PLS. _AIChE J._ 53. doi:10.1002/aic.

Dayal, B.S., MacGregor, J.F., 1997. Recursive exponentially weighted PLS and its applications to adaptive control and prediction. _J. Process Control_ 7, 169–179. doi:10.1016/S0959-1524(97)80001-7.

Desharnais, B., Camirand-Lemyre, F., Mireault, P., Skinner, C.D., 2015. Determination of confidence intervals in non-normal data: application of the bootstrap to cocaine concentration in femoral blood. _J. Anal. Toxicol._ 39, 113–117. doi:10.1093/jat/bku127.

Duran-Villalobos, C.A., Lennox, B., Lauri, D., 2016. Multivariate batch to batch optimisation of fermentation processes incorporating validity constraints. _J. Process Control_ 46, 24–42. doi:10.1016/j.jprocont.2016.07.002.

Ed, P.P., 2013. LNAI 7987- Advances in data mining. 13th Industrial Conference, ICDM. doi:10.1007/978-3-642-39736-3.

Flores-Cerrillo, J., MacGregor, J.F., 2003. Within-batch and batch-to-batch inferential-adaptive control of semibatch reactors: a partial least squares approach. _Ind. Eng. Chem. Res._ 42, 3334–3345. doi:10.1021/ie020596u.

Flores-Cerrillo, J., MacGregor, J.F., 2004. Control of batch product quality by trajectory manipulation using latent variable models. _J. Process Control_ 14, 539–553. doi:10.1016/j.jprocont.2003.09.008.

Flores-Cerrillo, J., MacGregor, J.F., 2005. Latent variable MPC for trajectory tracking in batch processes. _J. Process Control_ 15, 651–663. doi:10.1016/j.jprocont.2005.01.004.

García-Muñoz, S., Kourti, T., MacGregor, J.F., 2004. Model predictive monitoring for batch processes. _Ind. Eng. Chem. Res._ 43, 5929–5941. doi:10.1021/ie034020w.

Gins, G., Vanlaer, J., Van Impe, J.F.M., 2009. Online batch-end quality estimation: does laziness pay off? _IFAC Proc. Vol._ doi:10.3182/20090630-4-ES-2003.0321.

Goldrick, S., Andrei, S., Lovett, D., Montague, G., Lennox, B., 2015. The development of an industrial-scale fed-batch fermentation simulation. _J. Biotechnol._ 193, 70–82. doi:10.1016/j.jbiotec.2014.10.029.

Jackson, J.E., Mudholkar, G.S., Edward, J., 1979. Control procedures for residuals associated with principal component analysis. _Technometrics_ 21, 341–349. doi:10.2307/1267757.

Joe Qin, S., 1998. Recursive PLS algorithms for adaptive data modeling. _Comput. Chem. Eng._ 22, 503–514. doi:10.1016/S0098-1354(97)00262-7.

Kumar, A.S., Ahmad, Z., 2012. Model predictive control (MPC) and its current issues in chemical engineering. _Chem. Eng. Commun._ 199, 472–511. doi:10.1080/00986445.2011.592446.

Laurí, D., Lennox, B., Camacho, J., 2014. Model predictive control for batch processes: ensuring validity of predictions. _J. Process Control_ 24, 239–249. doi:10.1016/j.jprocont.2013.11.005.

Laurí, D., Sanchis, J., Martínez, M., Hilario, a, 2013. Latent variable based model predictive control: ensuring validity of predictions. _J. Process Control_ 23, 12–22. doi:10.1016/j.jprocont.2012.11.001.

Liu, K., Chen, Y., Zhang, T., Tian, S., Zhang, X., 2018. A survey of run-to-run control for batch processes. _ISA Trans._ doi:10.1016/j.isatra.2018.09.005.

Luo, L., Bao, S., 2018. Knowledge-data-integrated sparse modeling for batch process monitoring. _Chem. Eng. Sci._ 189, 221–232. doi:10.1016/j.ces.2018.05.055.

Martens, H., 2001. Reliable and relevant modelling of real world data: a personal account of the development of PLS regression. _Chemom. Intell. Lab. Syst._ 58, 85–95. doi:10.1016/S0169-7439(01)00153-8.

Martens, H., Naes, T., 1989. _Multivariate Calibration._ Wiley.

Nelson, P., Taylor, P., 1996. Missing data methods in PCA and PLS: score calculations with incomplete observations. _Chemom. Intell. Lab. Syst._ 35, 45–65. doi:10.1016/S0169-7439(96)00007-X.

Nomikos, P., Macgregor, J.F., 1995a. Multivariate SPC charts for batch monitoring processes. _Technometrics_ 37, 41–59. doi:10.1080/00401706.1995.10485888.

Nomikos, P., MacGregor, J.F., 1995b. Multi-way partial least squares in monitoring batch processes. _Chemom. Intell. Lab. Syst._ 30, 97–108. doi:10.1016/0169-7439(95)00043-7.

Qin, S.J., 2003. Statistical process monitoring: basics and beyond. _J. Chemom._ 17, 480–502. doi:10.1002/cem.800.

Qin, S.J., 2012. Survey on data-driven industrial process monitoring and diagnosis. _Annu. Rev. Control_ 36, 220–234. doi:10.1016/j.arcontrol.2012.09.004.

Ramani, S., 1974. EDF statistics for goodness of fit and some comparisons. _J. Am. Stat. Assoc._ 69, 730–737. doi:10.2307/2286009.

Sheng, J., Chen, T., Shah, S.L., 2002. GPC for non-uniformly sampled systems based on the lifted models. _IFAC Proc. Vol._ 405–410. doi:10.1016/S0959-1524(02)00009-4.

Ündey, C., Ertunç, S., Çinar, A., 2003. Online batch/fed-batch process performance monitoring, quality prediction, and variable-contribution analysis for diagnosis. _Ind. Eng. Chem. Res._ 42, 4645–4658. doi:10.1021/ie0208218.

Vanlaer, J., Van Den Kerkhof, P., Gins, G., Van Impe, J.F.M., 2011. The influence of measurement noise on PLS-based batch-end quality prediction. _IFAC Proc. Vol._ 7156–7161. doi:10.3182/20110828-6-IT-1002.02775.

Wan, J., Marjanovic, O., Lennox, B., 2012. Disturbance rejection for the control of batch end-product quality using latent variable models. _J. Process Control_ 22, 643–652. doi:10.1016/j.jprocont.2011.12.012.

Wold, S., Geladi, P., Esbensen, K., Öhman, J., 1987. Multi-way principal components and PLS-analysis. _J. Chemom._ 1, 41–56. doi:10.1002/cem.1180010107.

Xu, Q.-S., Liang, Y.-Z., 2001. Monte Carlo cross validation. _Chemom. Intell. Lab. Syst._ 56, 1–11. doi:10.1016/S0169-7439(00)00122-2.

Yabuki, Y., Nagasawa, T., Macgregor, J.F., 2000. An industrial experience with product quality control in semi-batch processes. _Comput. Chem. Eng._ 24, 585–590. doi:10.1016/S0098-1354(00)00423-3.

Yu, L.X., Amidon, G., Khan, M.A., Hoag, S.W., Polli, J., Raju, G.K., Woodcock, J., 2014. Understanding pharmaceutical quality by design. _AAPS J._ 16, 771–783. doi:10.1208/s12248-014-9598-3.

---

_역자 주: 본문에서 언급된 부록 A(Appendix A) 및 부록 B(Appendix B)는 제공된 원문(본문 및 참고문헌 범위)에 별도의 본문이 포함되어 있지 않아 번역 대상에서 제외되었다. 해당 내용은 논문의 보충 자료(Supplementary material)에 수록되어 있을 수 있다._


