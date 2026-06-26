# 곰팡이 발효 공정에 대한 라만 분광법 적용에서 입사 파장과 검출기 재료 선택이 형광에 미치는 영향

**Influence of Incident Wavelength and Detector Material Selection on Fluorescence in the Application of Raman Spectroscopy to a Fungal Fermentation Process**

_bioengineering — Article_

---
## 저자

Stephen Goldrick ¹·†, David Lovett ², Gary Montague ³, Barry Lennox ⁴·*

1. Biopharmaceutical Bioprocess Technology Centre, Merz Court, Newcastle University, Newcastle-upon-Tyne NE1 7RU, UK; s.goldrick@ucl.ac.uk
2. Perceptive Engineering Limited, Vanguard House, Keckwick Lane, Daresbury, Cheshire WA4 4AB, UK; dlovett@perceptiveapc.com
3. School of Science, Engineering & Design, Teeside University, Tees Valley TS1 3BX, UK; G.Montague@tees.ac.uk
4. Control Systems Group, School of Electrical and Electronic Engineering, University of Manchester, Manchester M13 9PL, UK

* 교신저자: barry.lennox@manchester.ac.uk; Tel.: +44-0161-306-4661

† 현 주소: Department of Biochemical Engineering, University College London, London WC1H 0AH, UK.

투고일: 2018년 9월 14일 / 수락일: 2018년 9월 21일 / 게재일: 2018년 9월 25일

_Bioengineering_ **2018**, _5_, 79; doi:10.3390/bioengineering5040079

---

## 초록 (Abstract)

라만 분광법은 생물공정(bioprocess)의 온라인 모니터링 및 제어에 사용되는 새로운 도구로서, 분광 분석을 통해 핵심 공정 변수들을 정량적·정성적으로 결정할 수 있게 해준다. 그러나 라만 분광 분석기를 산업용 발효 공정에 광범위하게 적용하는 것은, 생물학적 시료 분석에 수반되는 높은 배경 형광 신호와 관련된 문제들 때문에 저해되어 왔다. 이 문제를 해결하기 위해, 우리는 서로 다른 파장과 검출기를 가진 두 대의 라만 분광 장치를 사용하여 곰팡이 발효 공정의 핵심 공정 인자(critical process parameters, CPPs)와 핵심 품질 속성(critical quality attributes, CQAs) 분석에서 형광이 수집된 스펙트럼에 미치는 영향을 조사하였다. 더 짧은 파장(903 nm)과 전하결합소자(charged coupled device, CCD) 검출기를 사용한 라만 분석기로 수집된 스펙트럼은 높은 형광에 의해 손상되어, 이러한 CPP와 CQA의 예측에 사용할 수 없었다. 이와 대조적으로, 더 긴 파장(993 nm)과 인듐 갈륨 비소(indium gallium arsenide, InGaAs) 검출기를 사용한 라만 분석기로 수집된 스펙트럼은 형광의 영향이 중간 정도에 그쳐, 발효의 핵심 변수들에 대한 정확한 추정치를 생성할 수 있었다. 이 새로운 연구는 동일한 공정에 대해 서로 다른 두 라만 분광 프로브를 직접 비교한 최초의 사례로서, 발효 운전 전반에 걸쳐 기록된 스펙트럼에 높은 형광이 미치는 중대한 악영향을 부각한다. 나아가 본 논문은 생물공정 모니터링 응용에서 형광에 의한 손상을 최소화하기 위해 라만 분광 장치의 입사 파장과 검출기 재료 유형을 모두 올바르게 선택하는 것이 중요함을 보여준다.

**키워드(Keywords):** #Raman_spectroscopy; #fluorescence; #fermentation_monitoring; #PLS
라만 분광법; 형광; 발효 모니터링; PLS 모델링; 핵심 공정 인자; 핵심 품질 속성

---

## 1. 서론 (Introduction)

라만 분광법은 분자 진동을 이용하여 분자를 정성적·정량적으로 분석하는 비침습적(non-invasive)·비파괴적(non-destructive) 분광 기법이다 \[1]. 이 기법은 생물학과 화학 전반에 걸쳐 폭넓은 응용을 가지며, 환경 및 산업 응용에도 적용되어 왔다 \[2]. 생명공학 산업에서 이러한 형태의 분광 분석기에 대한 관심은 2004년 FDA의 공정 분석 기술(Process Analytical Technology, PAT) 이니셔티브 발표에 자극받아 최근 몇 년간 크게 증가하였다 \[3,4]. 생물공정과 관련된 PAT 분석기로서 라만 분광법이 가지는 주요 장점에는 적은 시료량 요구, 시료 전처리 불필요, 수용액 시료 분석 시 물에 의한 간섭이 거의 없음, 유리나 플라스틱을 통한 분석 가능, 그리고 다양한 영양분과 생성물에 대한 높은 특이성 등이 있다 \[5,6]. 최근 생물공정에 라만 분광법을 적용한 사례로는 포유류 세포 배양 운전에서의 영양분 농도 및 생존 세포 밀도의 실시간 모니터링 \[7,8], 사카로마이세스 세레비시에(_Saccharomyces cerevisiae_) 발효에서의 에탄올 생산 \[9,10], 그리고 대장균(_Escherichia coli_) 발효에서의 영양분 및 페닐알라닌 농도 \[11] 등이 있다. 보다 고도화된 사례로는 포유류 세포 배양 중 재조합 항체 역가(titre)의 온라인 모니터링 \[12]과, 더불어 Li 등 \[13]이 보여준 단클론 항체 생산 중 당화(glycosylation)의 실시간 모니터링과 같이 복잡한 번역 후 변형(post-translational modification)을 모니터링하는 라만 분광법의 능력이 있다.

라만 분광법이 생물공정의 실시간 모니터링 및 제어에서 중추적 역할을 하게 되리라는 점은 분명하다. 그러나 이러한 공정 분석기의 광범위한 채택을 저해하는 주요 장애물은, 생물학적 분자 분석 중 관찰되는 높은 형광과 관련되어 있다. 이 형광은 종종 중요한 라만 산란 결합을 덮어버려, 관심 물질을 추정하는 능력을 약화시킨다 \[14,15]. 생물학적 재료 분석에서 형광을 완화하거나 억제하는 다양한 방법이 존재한다. 광표백(photo-bleaching)은 레이저 광원으로부터의 강한 여기(excitation)에 시료를 장시간 노출시켜 시료 형광의 원인이 되는 형광체(fluorophore)를 분해함으로써, 골 조직 분석에서 기록되는 형광을 감소시킨다는 것이 입증되었다 \[16]. 공초점(confocal) 설정의 조정 또한 초점 심도를 줄여 경로 길이를 효과적으로 줄이고, 이를 통해 레이저 초점 외부에서 발생하는 검출 형광을 줄임으로써 형광을 감소시킨다고 보고되었다 \[17]. 시프트 여기 라만 차이 분광법(shifted excitation Raman difference spectroscopy, SERDS)으로 알려진 기법은 약간 다른 두 레이저 파장에서 연속적으로 두 개의 라만 스펙트럼을 수집하고 이를 차감하는 것으로, 생물학적 시료 분석 중 형광을 제거하는 것으로 입증되었다 \[17,18]. 이 기법은 배경 형광 신호가 제거된 미분형 스펙트럼(derivative-like spectrum)을 생성하여, 중요한 라만 특징의 분해능을 향상시킨다 \[19]. 또한 시간 게이팅 라만 분광법(time-gated Raman spectroscopy)으로 알려진 기법은 라만 산란과 형광 흡수 간의 서로 다른 시간 척도를 이용하여 형광을 줄일 수 있다. 라만 산란은 거의 순간적으로(<1 피코초) 완료되는 반면, 형광 방출은 100~1000배 더 오래 걸린다(나노초 범위). 시간 게이팅 라만 분광법은 레이저 펄스를 사용하여 시료를 매우 짧은 시간 동안 조사함으로써 작동한다. 검출 시스템이 처음 수 피코초 동안 산란 또는 방출된 광자만 검출하도록 게이팅되어 있으면, 중요한 라만 광자만 기록되고 원치 않는 형광 광자의 대부분은 거부된다 \[20,21]. 이러한 기법들 외에도, 라만 장치의 여기 파장 선택은 라만 장치의 여기 파장과 시료 형광 발생 확률 간의 반비례 관계에 근거하여, 대부분의 시료에서 관찰되는 형광 수준에 상당한 영향을 미칠 수 있다 \[2]. 예를 들어, 자외선(Ultra-Violet) 라만 분광법은 낮은 파장 덕분에 더 나은 잡음 대 신호비를 가능하게 하며, 대부분의 화학종은 260 nm 이하의 여기 대역에서 형광을 내지 않기 때문에 형광 간섭도 줄일 수 있다 \[15,22]. 장치의 검출기 재료 또한 관찰되는 형광에 매우 큰 영향을 미칠 수 있으나, 발효 모니터링에 라만 분광법을 적용할 때 이 선택 기준의 중요성에 관해서는 연구가 거의 보고되지 않았다.

이 문제를 해결하고 발효 응용에서 이 기술의 활용을 진전시키기 위해, 두 대의 라만 분광 분석기를 형광이 매우 강한 곰팡이 발효 공정에 적용하였다. 한 라만 분석기는 입사 파장이 903 nm이고 실리콘 기반 전하결합소자(CCD) 검출기를 사용하였으며, 두 번째 장치는 993 nm 파장과 인듐 갈륨 비소(InGaAs) 배열 검출기를 사용하였다. 두 분석기 모두 유사한 소규모 곰팡이 발효 공정에 적용되었으며, 발효의 핵심 공정 인자(CPPs)와 핵심 품질 속성(CQAs)을 추정하는 것을 목표로 하였다. 이 공정에서 이들은 각각 포도당(glucose) 농도와 활성 의약 성분(active pharmaceutical ingredient, API) 농도로 이전에 식별된 바 있다. 더 짧은 파장과 CCD 검출기를 사용하는 라만 장치로 수집된 스펙트럼 데이터는 높은 배경 형광 신호에 의해 상당히 손상된 것으로 나타난 반면, InGaAs 검출기를 사용하는 993 nm 라만 장치는 형광의 영향이 중간 정도에 그쳤다. 두 분석기로부터 수집된 스펙트럼은 부분 최소제곱(partial least squares, PLS) 모델링을 사용하여 두 변수의 오프라인 농도와 상관관계를 분석하였다. 993 nm 장치로 기록된 스펙트럼을 사용하여 생성된 회귀 모델만이 포도당과 API 농도를 모두 정확히 예측할 수 있었다. 저자들이 아는 한, 이는 서로 다른 입사 파장과 검출기 재료를 가진 두 라만 분광 장치로 동일한 발효 공정을 모니터링한 최초의 직접 비교이다. 본 연구는 기록된 라만 스펙트럼에 대한 형광의 기본 원리를 더 잘 이해할 필요성을 부각하며, 이 새로운 기술을 생명공학 분야에 향후 적용할 때 올바른 프로브 선택이 중요함을 보여준다.

---

## 2. 실험 부문 (Experimental Section)

### 2.1. 미생물 및 배지 (Microorganism and Media)

화이자(Pfizer)에서 공급한 독점 곰팡이를 사용하여 두 발효를 모두 접종하였으며, 이는 동일하게 해동된 배양 원액(culture stock)에서 증식시키고 독점 영양 공급원으로 보충하였다. 이 곰팡이는 활성 의약 성분(API) 농도로 지칭되는, 상업적으로 이용 가능한 항생제를 고농도로 생산한다.

### 2.2. 생물반응기 조건 (Bioreactor Conditions)

두 번의 유가식(fed-batch) 곰팡이 발효(발효 A 및 발효 B로 지칭)를 작업 용량 약 3.6 L의 5 L 생물반응기에서 수행하였다. 각 생물반응기는 동일한 운전 조건을 갖도록 설정되었으며, 둘 다 온도계, 용존 산소 및 pH 프로브를 갖추었다. 반응기의 온도는 외부 냉각 재킷을 사용하여 28 ℃로 유지하였다. 배양액의 pH는 비례-적분-미분(proportional integral derivative, PID) 제어기를 사용하여 산/염기 용액을 첨가함으로써 6.2로 유지하였다. 혼합은 고정 RPM으로 작동하는 표준 러쉬톤(Ruston) 임펠러를 사용하여 이루어졌다. 공기 유량은 두 발효 모두 상한값으로 고정하였다. 발효 A의 오프라인 측정은 하루에 한 번, 발효 B의 경우 하루에 세 번 기록하였다. 포도당 농도는 오프라인 분석기를 사용하여 측정하였고, 활성 의약 성분(API) 농도는 고압 액체 크로마토그래피(high pressure liquid chromatography, HPLC)를 통해 결정하였다. 배치 전반에 걸쳐 포도당은 볼루스(Bolus) 포도당 첨가를 통해 제어하였다. 소포제(anti-foam)는 필요에 따라 첨가하였다. 미생물, 배지 조성 및 공급업체 선정에 관한 구체적인 사항은 기밀 유지를 이유로 생략하였다.

### 2.3. 라만 분광 장치 (Raman Spectroscopy Devices)

발효 A에서는 스펙트럼 범위 200–2400 cm⁻¹, 분해능 3 cm⁻¹의 인듐 갈륨 비소(InGaAs) 검출기 배열을 가진 993 nm 라만 분광 장치를 적용하였다. 발효 B에서는 라만 장치의 레이저 파장이 903 nm였으며, 스펙트럼 범위 200–2400 cm⁻¹, 분해능 3 cm⁻¹의 실리콘 기반 CCD 검출기를 사용하였다. 각 장치는 휴대용 컴퓨터에 연결되어 스펙트럼을 온라인으로 수집하였으며, 각 발효 전반에 걸쳐 적분 시간(integration time)과 평균 횟수(number of averages)를 수동으로 조정할 수 있었다. 사용 전에 각 라만 장치는 각 픽셀 번호가 분광기에서 올바른 파수(wavenumber)에 대응되도록 교정하였다. 교정은 알려진 물질의 라만 스펙트럼을 분석하고 스펙트럼의 주요 피크의 파수를 시료의 알려진 파수와 비교하여, 이들이 일치하도록 함으로써 수행하였다. 관심 피크를 식별하는 데 도움을 주기 위해 추가 교정 시료를 제작하였으며, 이는 포도당(20 g L⁻¹) 및 API(6 g L⁻¹)를 첨가한 수용액 시료로부터 수집한 라만 스펙트럼을 분석하는 것을 포함하였다.

### 2.4. 라만 스펙트럼 전처리 및 파장 선택 (Raman Spectra Preprocessing and Wavelength Selection)

각 장치로 수집된 스펙트럼은 오프라인 포도당 및 API 측정값과 결합되어 두 개의 PLS 모델을 생성하는 데 사용되었다. 발효 A에서는 10개의 오프라인 포도당 시료가 기록되었고, 발효 B에서는 18개의 오프라인 시료가 기록되었다. 각 발효에 대해 8개의 오프라인 API 농도 시료가 기록되었다. 오프라인 포도당 시료는 3차 스플라인(cubic spline) 근사를 사용하여 보간되었으며, 30분 샘플링 속도를 적용한 결과 발효 A와 B에 대해 각각 522개와 475개의 샘플 포인트가 생성되었다. 오프라인 API 농도도 유사한 방식으로 보간되어 약 360개의 샘플 포인트가 생성되었다. 30분 샘플링 속도는 평균 횟수와 적분 시간 조정을 통해 30분마다 단일 스펙트럼을 생성하도록 설정된 각 라만 장치의 샘플링 빈도에 맞추기 위해 선택되었다. 스펙트럼 전처리는 Mori 등 \[23]에 기술된 디스파이킹(de-spiking) 알고리즘을 활용하였으며, Eilers와 Boelens \[24]에 제시된 대로 기준선 보정(baseline correction)을 수행하였다. 스펙트럼은 Bocklitz 등 \[6]에 기술된 전처리 방법과 유사하게, 폭 15와 다항식 차수 5의 사비츠키-골레이(Savitzky-Golay) 필터를 사용하여 스펙트럼의 1차 미분을 계산함으로써 추가로 전처리되었다. 전처리된 스펙트럼 데이터(X_spec)와 그에 대응하는 오프라인 포도당(Y_Gluc) 및 오프라인 API 농도(Y_API)는, 각 교정(calibration) 데이터 세트가 검증(validation) 데이터 세트에서의 포도당과 API 농도 범위를 모두 적절히 기술하도록 분할되었다. 따라서 각 발효의 처음 75시간이 포도당 측정을 위한 교정 데이터 세트로 사용되었고, 나머지는 모델을 검증하는 데 사용되었다. API 농도 예측에 사용된 교정 데이터는 처음 여섯 개의 오프라인 측정값을 사용하였으며, 추가로 각 오프라인 API 농도 주변의 보간된 데이터 포인트 다섯 개가 발효 A와 B 모두의 교정 데이터 세트에 포함되어 총 30개의 데이터 포인트로 구성되었다. 검증 데이터 세트는 이러한 교정 데이터 포인트들 사이의 데이터와 여섯 번째 오프라인 API 농도 값 이후의 나머지 데이터로 구성되었다.

포도당과 관련된 파장은 고농도 포도당(20 g L⁻¹)을 첨가한 수용액 교정 시료의 분석을 통해 식별되었으며, 다음과 같이 취해졌다: 366:372, 456:476, 477:486, 891:897, 898:919, 1589:1595 cm⁻¹. 교정 시료 분석 중 수집된 스펙트럼은 부록 A의 그림 A1에 제시되어 있다. API 농도에 대한 PLS 모델도 유사한 방식으로 생성되었으며, 파장은 720:732, 786:793, 800:806 cm⁻¹로 취해졌다. 각 PLS 모델의 최적 성분(component) 수는 식 (6)에 정의된 교정 제곱근 평균 제곱 오차(root mean square error of calibration, RMSEC)와 예측 제곱근 평균 제곱 오차(root mean square error of prediction, RMSEP)에 근거하여 선택되었다.

### 2.5. 부분 최소제곱 모델 생성 (Partial Least Model Generation)

PLS 모델은 Wold 등 [25]이 상세히 기술한 비선형 반복 부분 최소제곱(non-linear iterative partial least squares, NIPALS) 알고리즘을 구현하였다. 전처리된 스펙트럼 데이터(X_spec)는 먼저 R개의 잠재 변수(latent variable)로 분해되어 점수(scores) 행렬 T와 적재(loadings) 행렬 P를 생성하고, E를 잔차(residual)로 가진다. 오프라인 포도당 농도(Y_Gluc)도 유사한 방식으로 분해되어 점수 행렬 U와 적재 행렬 Q를 생성하고 F를 잔차로 가지며, 아래와 같이 정의된다:

$$X_{spec} = TP' + E \tag{1}$$

$$Y_{Gluc} = UQ' + F \tag{2}$$

X 블록의 점수를 Y 블록의 점수와 연관시키는 내부 관계 벡터 B는 다음과 같이 생성된다:

$$B = X_{spec}^{T} T (X_{spec}^{T} X_{spec})^{-1} \tag{3}$$

PLS 모델은 각 잠재 변수에 대해 반복적으로 작동하며, 수렴 시 다음과 같이 회귀 계수 행렬 β를 생성할 수 있다:

$$\beta = W(P^{T}W)^{-1},\mathrm{diag}(B) \tag{4}$$

회귀 계수의 누적합은 R개의 잠재 변수를 취하여 X 블록으로부터 응답 변수($\hat{Y}_{Gluc}$)를 예측한다:

$$\hat{Y}_{Gluc} = X_{spec} \sum_{r=1}^{R} \beta \tag{5}$$

활성 의약 성분($\hat{Y}_{API}$) 예측에도 유사한 절차가 수행되었다.

### 2.6. PLS 모델의 검증 (Validation of PLS Model)

PLS 모델에서 선택할 잠재 변수의 수를 정하기 위해 모델의 예측 오차를 계산하였다. 교정 데이터 세트와 관련된 오차는 교정 제곱근 평균 제곱 오차(RMSEC)를 사용하여 계산하였고, 검증 데이터 세트의 경우 예측 제곱근 평균 제곱 오차(RMSEP)를 사용하였다. 이 함수들은 [26]에 기술된 대로 다음과 같이 계산되었다:

$$RMSEC = \left[\frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2\right]^{0.5} \qquad RMSEP = \left[\frac{1}{p}\sum_{i=1}^{p}(y_i - \hat{y}_i)^2\right]^{0.5} \tag{6}$$

여기서:

- _n_: 교정 시료 수
- _p_: 검증 시료 수
- _yᵢ_: i번째 교정 시료
- _ŷᵢ_: i번째 검증 시료

### 2.7. 라만 분광법의 기본 원리 (Raman Spectroscopic Fundamentals)

라만 분광법의 기본 원리는 그림 1에 설명되어 있다. 이 과정은 ν₀와 동일한 고정 주파수를 가진 단색광원(monochromatic light source)을 사용하여 시료를 조사하고, 검출기를 통해 기록되는 산란광을 분석하는 것을 포함한다. 광원의 에너지는 E = hν₀로 주어지며, 여기서 h는 플랑크 상수, ν₀는 그 주파수이다. 빛이 시료와 상호작용하면 작은 주파수 이동(Δν)과 그에 따른 에너지 편차가 발생할 수 있다. 빛과 시료의 상호작용은 그림 1에 강조된 바와 같이 다양한 산란 및 흡수 현상을 일으킨다.

레일리 산란(Rayleigh scattering)은 빛이 시료의 분자와 상호작용하고 순(net) 에너지 교환이 0일 때 발생한다. 즉, 입사광의 에너지(hν₀)가 산란광의 에너지와 같다. 반대로, 시료가 빛으로부터 에너지를 얻어 한 진동 상태 위로 이동하면 산란광의 주파수는 입사빔보다 낮아진다. 즉, 산란광의 에너지(hν₀ − hΔν)가 입사광의 에너지(hν₀)보다 작아지며, 이를 스토크스 산란(Stokes scatter)이라 한다. 만약 상호작용으로 인해 시료가 에너지를 잃으면 산란광의 주파수는 입사광보다 높아진다. 즉, 반사된 빔의 에너지(hν₀ + hΔν)가 입사빔의 에너지(hν₀)보다 커지며, 이를 반(反)스토크스 산란(anti-Stokes scatter)이라 한다. 라만 분광 분석기가 일반적으로 측정하는 것은 스토크스 이동 산란이며, 라만 이동(Raman shift) 또는 라만 산란(Raman scatter)으로 지칭되고, 종종 파수 단위(cm⁻¹)로 측정되며, 일반적으로 200에서 약 3000 cm⁻¹ 범위에 걸쳐 있다.

이 두 산란 현상 모두 시료의 전자를 가상 상태(virtual states)로 여기시키는데, 이 가상 상태는 여기 전자 전이 상태(E')보다 낮은 에너지를 가진다. 순 에너지 편차는 결과 스펙트럼에서 특징적인 피크를 만든다. 이 피크들의 위치는 시료의 분자 구조와 그 화학적 환경에 의해 정의되며, 이를 통해 라만 분광법을 화학적 식별 및 분류에 사용할 수 있다. 더욱이 스펙트럼의 피크 높이(또는 면적)는 분자 농도에 선형적으로 비례한다고 가정되며, 따라서 라만 분석기가 관심 물질을 검출할 수 있는 한, 생물공정의 CPP나 CQA를 모니터링하는 데 사용할 수 있다 [27].

> **그림 1.** 라만 분광법의 기본 원리를 나타낸 개략도로서, 주파수 ν₀의 단색광원으로 여기된 시료의 주요 산란 및 형광 여기를 강조한다. (구성 요소: 시료, 단색광원(레이저), 필터, 검출기, 바닥 전자 상태, 여기 전자 상태, 가상 상태, 레일리 산란, 스토크스 산란, 반스토크스 산란, 공명 산란(resonance scatter), 형광(fluorescence) 등)

라만 산란의 강도($I_{Raman}$)는 매우 약하고 종종 검출하기 어려우며, 이 신호의 약함이 라만 분광법의 주된 한계이다. 이는 라만 산란의 강도를 광원의 강도($I_{Source}$) 및 레일리 산란으로 인해 수신되는 신호($I_{Rayleigh}$)와 비교함으로써 명확해지며, [28]에서 다음 범위로 정의되었다:

$$I_{Raman} \approx 10^{-4} I_{Rayleigh} \approx 10^{-8} I_{Source} \tag{7}$$

따라서 약한 라만 산란 효과를 검출하기 위해서는 레일리 산란광을 걸러내는 것이 필요하다 [29].

약한 라만 산란과 경쟁하는 것이 형광인데, 형광은 입사빔이 광원으로부터 일부 에너지를 흡수하여 전자를 더 높은 양자 상태(E')로 전이될 만큼 충분한 에너지로 일시적으로 여기시킬 때 발생하는 비산란(non-scattering) 과정이다. 여기된 전자가 도달할 수 있는 더 높은 양자 상태는 여러 개가 있으며, 이는 외부 광원의 에너지와 파장에 의존한다. 여기 상태의 전자는 불안정하여 각자의 바닥 상태로 돌아갈 때 그림 1에 강조된 바와 같이 hν₀,₁ ± hΔν와 동일한 에너지를 가진 빛을 방출한다. 형광과 라만 산란의 또 다른 주요 차이는 각 과정에 관여하는 시간 척도로서, 형광 과정은 나노초(10⁻⁹ s) 영역에서 일어나는 반면, 라만 산란 과정은 훨씬 빠르며 피코초(10⁻¹² s)에 완료된다 [28].

가시광선, 자외선 또는 근적외선에 의해 여기될 때 이러한 형광 과정에 취약한 분자를 형광체(fluorophore) 또는 형광 분자라고 하며, 이들은 일반적으로 여러 개의 π 결합을 가진 다환 방향족 탄화수소(polyaromatic hydrocarbon)나 헤테로고리(heterocycle) 분자이다. 발효 모니터링에서는 형광을 내는 알려진 그리고 알려지지 않은 생물학적 화합물이 많이 있다. 일반적으로 단백질, 효소, 비타민, 그리고 미생물 성장에서 나오는 1차 및 2차 대사산물이 이러한 성질을 가지지만 [5], 배양액 형광은 세포 밀도, 점도, 생성물 농도를 포함한 배양 조건과도 관련될 수 있다 [30]. 안타깝게도 발효 모니터링에서 형광의 발생은 주요 문제인데, 산란 광자 10⁴개 중 단 하나만이 라만 산란과 관련되어 있어, 적은 수준의 형광이라도 신호를 가려 분석을 매우 어렵게 하거나 무용하게 만들 수 있다.

---

## 3. 결과 및 고찰 (Results and Discussion)

### 3.1. 형광 관찰 (Fluorescence Observations)

두 라만 분광 장치로 수집된 스펙트럼을 분석하여, 이 소규모 곰팡이 발효의 주요 CPP와 CQA로 이전에 식별된 포도당과 API 농도를 추정하였다. 993 nm 라만 장치로 수집된 스펙트럼은 형광의 영향이 중간 정도였던 반면, 903 nm 라만 장치로 기록된 스펙트럼은 형광에 의해 상당히 영향을 받았다. 그림 2a는 발효의 처음 90.5시간 동안 903 nm 라만 장치로 기록된, 주로 발효 브로스(broth)의 형광에 기인한 큰 기준선 이동(baseline shift)을 강조한다. 기준선 스펙트럼이 0.4 × 10⁴ a.u에서 거의 1.6 × 10⁴ a.u로 이동하면서 강도가 4배 증가하는 것이 관찰된다. 이러한 큰 증가가 비정상적인 것은 아니지만, Cannizzaro 등 [31]은 _Phaffia rhodozyma_ 를 모니터링하는 유가식 공정의 처음 90시간 동안 유사한 기준선 이동 증가를 관찰하였다. 그러나 그림 2a에 관찰되는 일부 중요한 라만 피크는, 초기에 기록된 스펙트럼과 비교했을 때 강한 배경 형광 신호에 의해 왜소해지는 것으로 나타난다. 이 스펙트럼들은 적분 시간 180초, 평균 9회로 기록되었다. 이러한 라만 피크의 분해능을 개선하고 신호 대 잡음비를 향상시키기 위해, 표 1에 정의된 대로 903 nm 라만 장치의 튜닝 파라미터를 배치 전반에 걸쳐 조정하였다. 후속 회귀 모델 생성의 복잡성 때문에 발효 중에 라만 장치의 튜닝 파라미터를 조정하는 것은 권장되지 않는다. 그러나 중요한 라만 피크가 두드러진 광대역 형광 신호에 의해 가려지지 않도록 하기 위해 공정 중 변경이 종종 필요하다. Shih와 Smith [32]는 이전에 에탄올 생산 발효 중 785 nm 라만 장치로 수집된 스펙트럼에서 적분 시간의 증가가 포도당 피크의 분해능을 개선함을 입증하였다. 여기서 수행된 실험에서도 적분 시간을 270초로 늘리고 평균 횟수를 6회로 줄인 후 스펙트럼 강도에서 유사한 증가가 관찰되었으며, 이는 그림 2b에서 볼 수 있다. 그러나 형광의 크기 또한 증가하여 CCD 검출기의 포화 한계(saturation limit)에 도달하게 되었다. 이 장치의 포화 한계는 91.5–97시간 동안 강도가 60,000 카운트에 접근할 때 스펙트럼의 평평한 선으로 나타난다. 이 한계 아래로 강도를 줄이기 위해 적분 시간을 60초로 줄이고 평균 횟수를 27회로 늘렸으며, 이는 그림 2c에 나타나 있다. 스펙트럼 강도의 감소가 관찰되었으나, 약한 라만 신호는 남아 있는 광대역 배경 형광 신호에 의해 효과적으로 가려졌다. 따라서 이 발효에 대해 수집된 나머지 스펙트럼은 광대역 형광 신호의 지배로 인해 정량적 정보를 추출할 수 없어 사실상 사용 불가능하였다(그림 2d).

993 nm 라만 장치로 수집된 스펙트럼은 중간 정도의 형광에만 영향을 받았으며, 그림 3a에서 볼 수 있듯이 전체 배치에 걸쳐 명확한 라만 피크가 보인다. 그 결과, 장치의 튜닝 파라미터는 발효 전반에 걸쳐 일정하게 유지되었다.

> **그림 2.** 903 nm 라만 분광 장치로 서로 다른 튜닝 파라미터에서 수집된 원시 스펙트럼의 일부. (a) 발효 0–90.5시간에 걸쳐 적분 시간 180초, 평균 9회로 기록; (b) 91.5–97시간에 걸쳐 적분 시간 270초, 평균 6회; (c) 98.5–114.5시간에 걸쳐 적분 시간 60초, 평균 27회; (d) 193.5–239시간에 걸쳐 적분 시간 30초, 평균 54회로 기록.

**표 1.** 각 배치 전반에 걸쳐 993 nm 및 903 nm 라만에 대해 선택된 튜닝 파라미터 요약.

|스펙트럼 참조|시작 (h)|종료 (h)|스펙트럼 수|적분 시간 (s)|평균 횟수|발생한 문제|
|---|---|---|---|---|---|---|
|**993 nm 라만 장치**|||||||
|Spec₀₋₂₆₀|0|260|520|180|9|중간 형광|
|**903 nm 라만 장치**|||||||
|Spec₀₋₉₀.₅|0|90.5|181|180|9|중간 형광|
|Spec₉₁.₅₋₉₇|91.5|97|10|270|6|CCD 포화|
|Spec₉₈.₅₋₁₁₄.₅|98.5|114.5|32|60|27|높은 형광|
|Spec₁₁₅.₅₋₁₄₆.₅|115.5|146.5|62|90|18|높은 형광|
|Spec₁₄₆.₅₋₁₉₃|146.5|193|93|60|27|높은 형광|
|Spec₁₉₃.₅₋₂₃₉|193.5|239|91|30|54|높은 형광|

> **그림 3.** 993 nm 및 903 nm 라만 분광 장치로 수집된 원시 스펙트럼은 각각 (a, b)에 나타나 있다. 온라인 포도당 농도와 비교한 해당 PLS 모델 예측은 각각 (c, d)에 나타나 있다. (그림에는 "올바른 프로브 선택 ✔"과 "잘못된 프로브 선택 ✗"이 표시되어 있다.)

### 3.2. 903 nm 및 993 nm 라만 분광 장치의 포도당 예측 (Glucose Predictions)

앞서 논의한 바와 같이 각 장치의 스펙트럼 데이터와 그에 대응하는 오프라인 포도당 측정값을 사용하여 두 개의 별도 PLS 모델을 생성하였다. 각 모델의 성분 수는 식 (6)에 정의된 두 PLS 모델의 RMSEC와 RMSEP에 근거하여 선택되었다. 그림 4는 903 nm 및 993 nm 라만 장치 모두에 대해 각 PLS 모델의 성분 수에 따른 이 오차들을 비교한다. 993 nm 라만 장치의 경우, 가장 낮은 RMSEP에 해당하는 네 개의 성분이 선택되었다. 추가 성분을 취하는 것은 RMSEC와 RMSEP 양쪽 오차를 미미하게 감소시키는 대가로 모델의 복잡성을 불필요하게 증가시킨다. 마찬가지로 903 nm 라만 장치의 경우, 유사한 관찰에 근거하여 세 개의 성분이 선택되었다. 903 nm 라만 장치의 RMSEP는 993 nm 라만 장치에 비해 매우 좋지 않은데, 이는 성분 선택이 PLS 모델의 예측 가능성에 거의 영향을 미치지 않을 것임을 시사한다. 이 PLS 모델의 생성은 그림 3c,d에 요약되어 있으며, 각각 993 nm 및 903 nm 라만 장치의 오프라인 포도당 예측을 보여준다. 993 nm 장치에서 생성된 스펙트럼 데이터는 형광의 영향이 중간 정도였기 때문에, 이 장치는 그림 3c에 강조된 바와 같이 발효의 오프라인 포도당 농도와 비교할 때 정확한 PLS 예측을 생성하였다. Abu-Absi 등 [7]과 Whelan 등 [33]은 유사한 결과를 보여주었는데, 둘 다 785 nm 라만 프로브가 포유류 유가식 세포 배양 전반에 걸쳐 포도당 농도를 온라인으로 예측하는 능력을 부각하였으며, 두 예측 모두 포도당 농도의 오프라인 측정값과 일치하는 것으로 나타났다.

903 nm 라만 장치로 수집된 스펙트럼을 사용한 발효 B의 포도당 농도에 대한 PLS 모델 예측은, 그림 3d에 나타난 바와 같이 오프라인 값과 비교했을 때 매우 좋지 않았다. 이러한 좋지 않은 예측은 배치 진행에 따라 관찰된 형광 증가와 관련된다. 명백히 포도당과 생성물 농도의 변화와 관련된 중요한 라만 피크가 이 형광에 의해 가려져, 이 스펙트럼의 PLS 모델로 생성된 좋지 않은 예측을 설명한다. 추가로, 예측된 포도당 농도의 큰 편차는 표 1에 나타난 적분 시간과 평균 횟수의 변경을 고려함으로써 설명될 수 있다. 이러한 파라미터의 조작은 PLS 모델이 생성한 선형 관계에 반영되지 않으며, 이는 그림 3d에 나타난 포도당 예측에서 관찰될 수 있다.

> **그림 4.** 993 nm 및 903 nm 라만 장치에 대한 RMSEC와 RMSEP. (a)는 잠재 변수 수에 따른 RMSEC, (b)는 잠재 변수 수에 따른 RMSEP를 나타낸다.

### 3.3. 라만 분광 입사 파장 및 검출기가 형광에 미치는 영향 (Influence of Raman Spectroscopic Incident Wavelength and Detector on Fluorescence)

두 라만 분석기로 수집된 스펙트럼에 영향을 미치는 형광 강도의 큰 차이에 기여하는 두 가지 주요 요인은 각 장치의 입사 파장과 사용된 검출기 재료와 관련된다. 여기 파장의 선택은 관찰되는 형광 수준에 상당한 영향을 미칠 수 있다. 라만 분광법에서 광원의 산란 에너지는 다음과 같이 여기 파장의 4제곱에 반비례한다:

$$I_{Raman} \approx (\nu_0)^4 \approx \left(\frac{1}{\lambda_0}\right)^4 \tag{8}$$

여기서:

- $I_{Raman}$: 라만 산란광의 강도
- $\nu_0$: 광원의 주파수
- $\lambda_0$: 광원의 파장

따라서 993 nm 라만 장치의 더 긴 파장은 903 nm에 비해 광원의 에너지를 감소시키며, 이로써 시료의 전자를 양자 상태로 여기시키는 데 사용 가능한 에너지를 낮추어 형광 발생 확률을 줄인다. Frank 등 [34] 또한 406 nm에서 830 nm까지 일곱 가지 서로 다른 여기 파장을 사용하여 인간 유방 생검(breast biopsy) 시료로부터 수집된 라만 스펙트럼을 연구함으로써 입사 파장 선택의 중요성을 강조하였다. 406 nm 입사 파장으로 수집된 스펙트럼은 광대역 형광 피크에 의해 완전히 지배된 반면, 더 높은 입사 파장(784 nm 및 830 nm)을 사용하여 수집된 스펙트럼은 고해상도 스펙트럼을 만들어 스펙트럼 시료로부터 정량적 정보를 추출할 수 있게 하였다. 마찬가지로 Volodin 등 [35]도 비교 가능한 결과를 보여주었는데, 1064 nm 라만 장치가 강한 형광 배경을 포함하는 다크 럼(dark rum) 시료를 올바르게 특성화하는 능력을 부각하였다. 그러나 동일한 시료를 785 nm 라만 장치로 분석했을 때는 신호가 높은 형광에 의해 손상되어 럼 시료를 특성화할 수 없었다. 여기 제시된 결과와 유사하게, 그들의 연구에서 785 nm 라만 장치는 CCD 검출기를 사용했고 1064 nm 라만 장치는 InGaAs 검출기를 사용하였다.

나아가, 903 nm 라만 장치는 800 nm보다 큰 파장에서 낮은 양자 효율(quantum efficiency)을 가지는 것으로 강조된 CCD 검출기를 사용한다 [15,36]. Li 등 [37]은 850 nm 이상의 파장에서 CCD 검출기의 양자 효율이 급격히 감소하는 유사한 현상을 입증하였다. 이러한 영역에서는 광자 에너지가 실리콘 밴드갭(bandgap) 에너지 아래로 떨어져 CCD 검출기가 입사 광자에 대해 투명해진다. 이러한 양자 효율의 감소는 강한 배경 형광 신호와 결합되어 이 903 nm 장치가 약한 라만 피크를 검출하는 능력을 떨어뜨린다. McCreery [2] 또한 850 nm 이상에서 CCD 검출기의 양자 효율이 상당히 떨어진다는 점을 강조하며, CCD 검출기를 가진 라만 장치의 최적 입사 파장이 600–850 nm 범위에 있다고 강조한다. 이와 대조적으로 Adar 등 [36]은 인듐 갈륨 비소(InGaAs) 검출기 배열이 이러한 더 높은 파장에서 높은 양자 효율을 가짐을 입증하였는데, 이는 993 nm 장치가 발효 전반에 걸쳐 명확하게 정의된 라만 피크를 생성하는 능력으로 입증된다. 그림 3은 형광이 강한 발효를 위한 라만 분광 장치를 선택할 때 입사 파장에 더하여 올바른 검출기 재료의 중요성을 부각한다. 그러나 형광은 시료 및 공정에 특이적이라는 점에 유의해야 한다. 낮은 파장의 여기 광원을 사용하는 라만 장치는 낮거나 중간 정도의 형광에 영향을 받는 시료에 대해 성공적으로 적용될 수 있다.

### 3.4. 993 nm 라만 분광 장치의 API 예측 (API Predictions)

이 발효의 API 농도에 대한 온라인 예측 또한 조사하였다. 993 nm 라만 장치로 수집된 스펙트럼을 사용한 API 농도의 PLS 예측과 오프라인 값의 비교는 그림 5에 나타나 있다. 생성물 농도 예측은 오프라인 측정값과 잘 일치한다. 생성물 농도를 온라인으로 추정하는 능력은 생성물 수율을 개선할 수 있는 향상된 제어 전략의 개발을 가능하게 한다. 903 nm 라만을 사용한 발효 B에서의 생성물 예측은 매우 좋지 않았으며, 그 결과 이러한 예측은 제시하지 않았다. 현재까지 발효 공정에서 API 농도를 정확히 모델링하는 라만 분광법의 능력을 보고한 사례는 거의 없다. 그 예로 Cannizzaro 등 [31]은 유가식 _P. rhodozyma_ 발효에서 카로티노이드(carotenoid) 생산의 온라인 생산을 위한 785 nm 라만 장치의 능력을 입증하였으며, 더불어 포유류 세포 배양에서 항체 생성물 농도의 예측도 있다 [12,38]. 이 발효 시스템에서 993 nm 라만 장치가 API 농도를 정확히 예측하는 능력은, 발효 공정 개선을 위한 품질 설계 기반(Quality by Design, QbD) 방법론의 구현에 이 기술을 적용하는 잠재적 이점을 부각한다.

> **그림 5.** 993 nm 라만 장치로 수집된 스펙트럼을 사용하여 생성된 생성물의 PLS 모델 프로파일과 그에 대응하는 API 농도의 오프라인 농도. 점선 수직선은 포도당 첨가 시점을 나타낸다.

---

## 4. 결론 (Conclusions)

형광은 생물의약품 공정을 모니터링하고 제어하기 위해 라만 분광법을 구현하는 많은 과학자와 엔지니어가 겪는 주요 문제이다. 본 논문은 동일한 발효에 대해 서로 다른 두 라만 분광 장치를 직접 비교한 최초의 사례로서, 입사 파장과 검출기 재료가 각 장치로 검출되는 형광 수준에 미치는 중대한 영향을 부각한다. 903 nm 입사 파장과 CCD 검출기를 가진 라만 분광 장치로 기록된 스펙트럼은 높은 형광에 의해 손상되어 회귀 분석에 사용할 수 없게 되었다. 그러나 993 nm 입사 파장과 인듐 갈륨 비소(InGaAs) 검출기를 가진 라만 분광 장치로 기록된 스펙트럼은 중간 정도의 형광 수준만을 가진 스펙트럼을 생성하였다. 이 장치로 기록된 스펙트럼은 PLS 회귀 모델 생성을 통해 포도당과 API 농도를 모두 정확히 추정할 수 있게 하였다. 따라서 본 연구는 더 낮은 입사 파장이 라만 산란 효과를 증가시키지만 동시에 형광 수준도 증가시켜 기록된 스펙트럼을 무용하게 만들 수 있음을 보여준다. 그러나 더 높은 입사 파장에서는 형광 발생 확률이 상당히 감소하며, 더불어 감소하는 라만 산란 효과는 InGaAs 검출기를 가진 993 nm 라만 프로브에서 입증된 바와 같이 더 민감한 검출기 재료로 보상할 수 있다. 따라서 라만 분광법은 생물의약품 처리에서 핵심 공정 인자를 정량화하는 데 매우 적합한 도구이다. 그러나 높은 형광과 관련된 문제가 기록된 스펙트럼의 품질에 영향을 미치지 않도록, 특히 분석기의 적절한 입사 파장과 센서 검출기 재료를 선택할 때 이 새로운 도구를 구현하는 데 주의가 요구된다.

---

## 저자 기여 (Author Contributions)

S.G.는 실험을 수행하고 데이터를 분석하였으며 PLS 모델을 생성하고 원고를 작성하였다. D.L., G.M., B.L.은 모델 생성, 실험 설계를 도왔으며 원고 준비를 도왔다. 모든 저자가 최종 원고를 읽고 승인하였다.

## 연구비 지원 (Funding)

본 연구는 Newcastle University에서 SG의 생물의약품 공정 개발(Biopharmaceutical Process Development) 공학 박사 과정의 일환으로 Perceptive Engineering Ltd.의 재정적 지원 및 협조와 함께 EPSRC 보조금(EP/G037620/1)의 지원을 받았다. 나아가 본 연구는 BL을 위한 Future Targeted Healthcare Manufacturing Hub(EP/P006485/1)의 지원을 통해 도움을 받았다. 본 프로젝트는 또한 지능 기반 생물의약품 제조(Intelligence-based Biopharmaceutical Manufacturing)에 관한 학술 연구를 촉진하기 위해 Advanced Manufacturing Technology Group, Pfizer Global Supply의 학술 파트너십 자금(Academic Partnership Funding)의 지원을 받았다.

## 이해 상충 (Conflicts of Interest)

저자들은 이해 상충이 없음을 선언한다.

---

## 약어 (Abbreviations)

본 원고에서 사용된 약어는 다음과 같다:

|약어|의미|
|---|---|
|API|활성 의약 성분 (Active pharmaceutical ingredient)|
|B|PLS 모델의 내부 관계 행렬|
|CCD|전하결합소자 (Charged couple device)|
|CPP|핵심 공정 인자 (Critical process parameters)|
|CQA|핵심 품질 속성 (Critical quality attributes)|
|E|PLS 모델에서 X-데이터에 대한 잔차 행렬|
|F|PLS 모델에서 Y-데이터에 대한 잔차 행렬|
|FDA|식품의약국 (Food and drug administration)|
|HPLC|고압 액체 크로마토그래피 (High pressure liquid chromatography)|
|InGaAs|인듐 갈륨 비소 (Indium gallium arsenide)|
|n|PLS 모델의 교정 포인트 수|
|NIPALS|비선형 반복 부분 최소제곱 (Non-linear iterative partial least squares)|
|p|PLS 모델의 검증 포인트 수|
|P|PLS 모델의 적재 행렬|
|PAT|공정 분석 기술 (Process analytic technology)|
|PID|비례-적분-미분 (Proportional integral derivative)|
|PLS|부분 최소제곱 (Partial least squares)|
|R|PLS 모델의 잠재 변수 수|
|RMSEC|교정 제곱근 평균 제곱 오차 (Root mean square error of calibration)|
|RMSEP|예측 제곱근 평균 제곱 오차 (Root mean square error of prediction)|
|UV|자외선 (Ultra-violet)|
|U|Y-데이터에 대한 PLS 모델의 점수 행렬|
|Q|Y-데이터에 대한 PLS 모델의 적재 행렬|
|T|X-데이터에 대한 PLS 모델의 점수 행렬|
|X_spec|PLS 모델의 X-데이터 (스펙트럼)|
|yᵢ|PLS 모델의 i번째 교정 포인트|
|ŷᵢ|PLS 모델의 i번째 검증 포인트|
|Y_Gluc|PLS 모델의 Y-데이터 (포도당)|
|Y_API|PLS 모델의 Y-데이터 (API)|
|β|PLS 모델의 회귀 계수|
|ν₀|라만 장치의 입사 파장|
|h|플랑크 상수|

---

## 부록 A. 라만 분광법 운영 (Appendix A. Raman Spectroscopy Operation)

라만 분광 장치의 운영 중에는 조작할 수 있는 두 가지 주요 튜닝 파라미터가 있으며, 이 파라미터들은 수집되는 스펙트럼의 품질에 영향을 미친다:

- **적분 시간(Integration time):** 검출기 노출 시간과 관련되며, 적분 시간이 길수록 라만 스펙트럼의 강도가 커진다. 강도는 단일 픽셀에 기록된 총 누적 전하와 관련된다. 적분 시간이 너무 길면 검출기를 포화시킬 수 있고, 너무 짧으면 라만 피크를 검출 가능한 수준 아래로 감소시킬 수 있으므로 균형이 필요하다.
- **평균 횟수(Number of averages):** 단일 스펙트럼을 얻기 위해 평균을 낸 스펙트럼의 수를 의미하며, 신호 대 잡음비(SNR)를 향상시키는 데 사용된다.

### 스펙트럼 전처리 방법 개요 (Overview of Spectral Preprocessing Methods)

대부분의 분광 분석과 마찬가지로, 라만 스펙트럼은 생성된 분류 및 회귀 모델의 예측 가능성을 향상시키기 위해 전처리되어야 한다. 전처리의 목적은 공정과 상관관계가 없는 모든 원치 않는 물리적 현상을 제거하는 것이다. Bocklitz 등 [6]은 라만 분광법과 관련된 세 가지 주요 교란 요인을 다음과 같이 본다:

1. 형광 및 배경 기준선 증가 (Fluorescence and background Baseline Increase)
2. 잡음 (Noise)
3. 우주선 스파이크 (Cosmic spikes)

이러한 원치 않는 인공물(artifact)들을 아래에서 논의하며, 그 영향을 제거하거나 줄이기 위해 사용되는 주요 전처리 방법을 강조한다.

**1. 형광 및 배경 기준선 증가**

앞서 논의했듯이 형광은 라만 분광법에서 주요 문제로, 기록된 스펙트럼 전반에 걸친 광대역 배경 신호 및/또는 기준선 증가로 종종 나타난다. 이 형광이 관심 물질의 약한 라만 방출을 완전히 압도하지 않는 한, 스펙트럼의 전처리를 통해 이 중간 정도의 형광을 제거하고 개선된 회귀 모델을 생성하는 데 도움을 줄 수 있다. 이용 가능한 다양한 전처리 기법이 있으며, 다항식 피팅(polynomial fitting) 또는 스펙트럼 신호의 미분 계산이 가장 널리 받아들여지는 두 가지 기법이다. 다항식 피팅은 스펙트럼으로부터 최소제곱으로 피팅된 다항식을 차감하는 것을 포함한다. 일반적으로 4차에서 6차 다항식을 사용하여 형광 배경 신호를 근사한 다음 원래 라만 스펙트럼에서 차감한다. 그러나 이 기법은 해석하기 어렵고 비물리적인 음수 기준선 보정 스펙트럼 값을 초래할 수 있다 [39]. 이 기법의 확장은 가중 최소제곱 기준선 보정(weighted least-squares baseline correction)을 수행하는 것으로, 전체 스펙트럼에 걸쳐 최적화 함수를 수행한다. 잔차가 0보다 큰 포인트는 최소제곱 피팅 알고리즘의 각 반복에서 가중치를 부여받아 음수가 아닌 기준선 보정 스펙트럼을 만든다. 수집된 일부 교정 스펙트럼에 이 기법을 적용한 결과는 그림 A1에 나타나 있으며, 알고리즘의 자세한 내용은 [24]에서 찾을 수 있다.

대안적으로, 기준선 이동은 스펙트럼의 1차 또는 2차 미분으로 작업함으로써 보정될 수 있다. 이 변환은 선형적이며, 생성된 곡선은 원래 스펙트럼에 대해 정량적 측면을 유지한다 [26]. 그러나 미분 계산은 때때로 스펙트럼 잡음을 증폭시킬 수 있다. 이는 미분을 계산하기 전에 데이터를 평활화(smoothing)함으로써 방지된다. 사비츠키-골레이(Savitzky-Golay) 필터링 기법은 라만 분광 분석에서 흔히 선택되는 평활화 기법으로, 이 기법은 n차 다항식을 k개의 입력 시료에 반복적으로 피팅하여 스펙트럼 데이터 세트를 평활화한다 [40].

**2. 잡음**

잡음은 모든 센서의 고유한 교란 요인으로, 일반적으로 라만 분광법에서 이 잡음은 열 잡음, 기기 판독 잡음 또는 심지어 우주선(cosmic ray)의 결과일 수 있다. 라만 분광법에서 잡음은 보통 높은 주파수로 특징지어진다. 그 영향을 최소화하기 위해, 잡음은 필터링 또는 평활화 기법의 적용을 통해 감소되거나 제거될 수 있다.

**3. 우주선 피크 (Cosmic Peaks)**

날카롭고 강한 피크는 종종 무작위적인 고에너지 입자(즉, 우주선)가 검출기에 부딪힌 결과이다. 이러한 인공물은 드물게 발생하지만, 일반적으로 검출하기 쉽고 스펙트럼의 육안 검사를 통해 명백히 드러난다. 이 피크들은 특히 데이터 평활화나 스케일링 중에 스펙트럼 분석을 방해할 수 있으므로 제거하는 것이 필요하다. 이러한 피크를 제거하기 위해 디스파이킹(de-spiking) 함수를 적용할 수 있다. 본 연구에서 적용된 디스파이킹 함수는 Mori 등 [23]에 상세히 설명되어 있으며, 그 적용은 그림 A1에 나타나 있다. 이 방법은 스펙트럼을 따라 모든 피크의 평균 각도를 계산하고 어떤 피크가 비정상적으로 큰지(즉, 우주선 피크인지) 판단한다. 이 비정상적인 피크는 식별된 후 제거되고 데이터 보간을 통해 대체된다.

> **그림 A1.** 포도당, API 및 사파이어(배경 스펙트럼) 스펙트로그래프를 강조하는 교정 시료의 라만 스펙트럼. (A)는 원시 스펙트럼을, (B)는 기준선 보정된 스펙트럼을 강조한다.

> **그림 A2.** 우주선을 포함하는 스펙트럼의 예. (A)는 디스파이킹 함수에 의해 식별된 이상치(outlier) 피크를, (B)는 우주선이 제거된 최종 스펙트럼을 강조한다. 560 cm⁻¹에 위치한 우주선은 이상치로 올바르게 식별되었으나, 이 함수는 410 cm⁻¹에 위치한 강한 사파이어 피크 또한 잘못 이상치로 식별하였다. 이는 식별된 각 이상치를 무분별하게 제거하기 전에 검토하는 것의 중요성을 보여준다.

---

## 참고문헌 (References)

1. Smith, E.; Dent, G. _Modern Raman Spectroscopy: A Practical Approach_; John Wiley & Sons: Hoboken, NJ, USA, 2013.
2. McCreery, R.L. _Raman Spectroscopy for Chemical Analysis_; John Wiley & Sons, Inc.: Hoboken, NJ, USA, 2005.
3. Kornecki, M.; Strube, J. Process Analytical Technology for Advanced Process Control in Biologics Manufacturing with the Aid of Macroscopic Kinetic Modeling. _Bioengineering_ **2018**, _5_, 25.
4. FDA. _Guidance for Industry: PAT—A Framework for Innovative Pharmaceutical Development, Manufacturing, and Quality Assurance_; DHHS: Rockville, MD, USA, 2004.
5. Lourenço, N.D.; Lopes, J.A.; Almeida, C.F.; Sarraguça, M.C.; Pinheiro, H.M. Bioreactor monitoring with spectroscopy and chemometrics: A review. _Anal. Bioanal. Chem._ **2012**, _404_, 1211–1237.
6. Bocklitz, T.; Walter, A.; Hartmann, K.; Rösch, P.; Popp, J. How to pre-process Raman spectra for reliable and stable models? _Anal. Chim. Acta_ **2011**, _704_, 47–56.
7. Abu-Absi, N.R.; Kenty, B.M.; Cuellar, M.E.; Borys, M.C.; Sakhamuri, S.; Strachan, D.J.; Hausladen, M.C.; Li, Z.J. Real time monitoring of multiple parameters in mammalian cell culture bioreactors using an in-line Raman spectroscopy probe. _Biotechnol. Bioeng._ **2011**, _108_, 1215–1221.
8. Mehdizadeh, H.; Lauri, D.; Karry, K.M.; Moshgbar, M.; Procopio-Melino, R.; Drapeau, D. Generic Raman-based calibration models enabling real-time monitoring of cell culture bioreactors. _Biotechnol. Prog._ **2015**, _31_, 1004–1013.
9. Picard, A.; Daniel, I.; Montagnac, G.; Oger, P. In situ monitoring by quantitative Raman spectroscopy of alcoholic fermentation by Saccharomyces cerevisiae under high pressure. _Extremophiles_ **2007**, _11_, 445–452.
10. Iversen, J.A.; Berg, R.W.; Ahring, B.K. Quantitative monitoring of yeast fermentation using Raman spectroscopy. _Anal. Bioanal. Chem._ **2014**, _406_, 4911–4919.
11. Lee, H.L.; Boccazzi, P.; Gorret, N.; Ram, R.J.; Sinskey, A.J. In situ bioprocess monitoring of Escherichia coli bioreactions using Raman spectroscopy. _Vib. Spectrosc._ **2004**, _35_, 131–137.
12. André, S.; Saint Cristau, L.; Gaillard, S.; Devos, O.; Calvosa, É.; Duponchel, L. In-line and real-time prediction of recombinant antibody titer by in situ Raman spectroscopy. _Anal. Chim. Acta_ **2015**, _892_, 148–152.
13. Li, M.Y.; Ebel, B.; Paris, C.; Chauchard, F.; Guedon, E.; Marc, A. Real-time monitoring of antibody glycosylation site occupancy by in situ Raman spectroscopy during bioreactor CHO cell cultures. _Biotechnol. Prog._ **2018**, _34_, 486–493.
14. De Beer, T.; Burggraeve, A.; Fonteyne, M.; Saerens, L.; Remon, J.P.; Vervaet, C. Near infrared and Raman spectroscopy for the in-process monitoring of pharmaceutical production processes. _Int. J. Pharm._ **2011**, _417_, 32–47.
15. Hanlon, E.; Manoharan, R.; Koo, T.; Shafer, K.; Motz, J.; Fitzmaurice, M.; Kramer, J.; Itzkan, I.; Dasari, R.; Feld, M. Prospects for in vivo Raman spectroscopy. _Phys. Med. Biol._ **2000**, _45_, R1.
16. Golcuk, K.; Mandair, G.S.; Callender, A.F.; Sahar, N.; Kohn, D.H.; Morris, M.D. Is photobleaching necessary for Raman imaging of bone tissue using a green laser? _Biochim. Biophys. Acta_ **2006**, _1758_, 868–873.
17. Xie, C.; Li, Y.Q. Confocal micro-Raman spectroscopy of single biological cells using optical trapping and shifted excitation difference techniques. _J. Appl. Phys._ **2003**, _93_, 2982–2986.
18. Sowoidnich, K.; Kronfeldt, H.D. Fluorescence rejection by shifted excitation Raman difference spectroscopy at multiple wavelengths for the investigation of biological samples. _ISRN Spectrosc._ **2012**, _2012_, 256326.
19. Shreve, A.P.; Cherepy, N.J.; Mathies, R.A. Effective rejection of fluorescence interference in Raman spectroscopy using a shifted excitation difference technique. _Appl. Spectrosc._ **1992**, _46_, 707–711.
20. Everall, N.; Hahn, T.A.S.; Atousek, P.M.; Parker, A.W. Picosecond time-resolved Raman spectroscopy of solids: Capabilities and limitations for fluorescence rejection and the influence of diffuse reflectance. _Appl. Spectrosc._ **2001**, _55_, 1701–1708.
21. Knorr, F.; Smith, Z.J.; Wachsmann-Hogiu, S. Development of a time-gated system for Raman spectroscopy of biological samples. _Opt. Express_ **2010**, _18_, 20049–20058.
22. Mulvaney, S.P.; Keating, C.D. Raman spectroscopy. _Anal. Chem._ **2000**, _72_, 145–158.
23. Mori, N.; Suzuki, T.; Kakuno, S. Noise of acoustic Doppler velocimeter data in bubbly flow. _J. Eng. Mech._ **2007**, _133_, 122–125.
24. Eilers, P.H.C.; Boelens, H.F.M. Baseline Correction with Asymmetric Least Squares Smoothing. _Leiden Univ. Med. Cent. Rep._ **2005**, _1_, 5.
25. Wold, S.; Geladi, P.; Esbensen, K.; Öhman, J. Multi-way principal components-and PLS-analysis. _J. Chemom._ **1987**, _1_, 41–56.
26. Gemperline, P. _Practical Guide to Chemometrics_; CRC Press: Boca Raton, FL, USA, 2006.
27. Alexander, R. _Advantages of Raman Spectroscopy When Analyzing Materials through Glass or Polymer Containers and in Aqueous Solution_; Technical Report, Perkin Elmer Application Report: Waltham, MA, USA, 2008.
28. Siesler, H.W.; Ozaki, Y.; Kawata, S.; Heise, H.M. _Near-Infrared Spectroscopy: Principles, Instruments, Applications_; John Wiley & Sons: Hoboken, NJ, USA, 2008.
29. Ferraro, J.R.; Nakamoto, K.; Brown, C.W. _Introductory Raman Spectroscopy_; Academic Press: Cambridge, MA, USA, 2003.
30. Goldrick, S. _Application of Multivariate Data Analysis and First Principle Mathematical Modelling to the Biotechnology Industry_. Ph.D. Thesis, Newcastle University, Newcastle upon Tyne, UK, 2015.
31. Cannizzaro, C.; Rhiel, M.; Marison, I.; von Stockar, U. On-line monitoring of Phaffia rhodozyma fed-batch process with in situ dispersive Raman spectroscopy. _Biotechnol. Bioeng._ **2003**, _83_, 668–680.
32. Shih, C.J.; Smith, E.A. Determination of glucose and ethanol after enzymatic hydrolysis and fermentation of biomass using Raman spectroscopy. _Anal. Chim. Acta_ **2009**, _653_, 200–206.
33. Whelan, J.; Craven, S.; Glennon, B. In situ Raman spectroscopy for simultaneous monitoring of multiple process parameters in mammalian cell culture bioreactors. _Biotechnol. Prog._ **2012**, _28_, 1355–1362.
34. Frank, C.J.; Redd, D.C.B.; Gansler, T.S.; McCreery, R.L. Characterization of human breast biopsy specimens with near-IR Raman spectroscopy. _Anal. Chem._ **1994**, _66_, 319–326.
35. Volodin, B.L.; Dolgy, S.; Lieber, C.; Wu, H.; Yang, W. Quantitative and qualitative analysis of fluorescent substances and binary mixtures by use of shifted excitation Raman difference spectroscopy. _SPIE Proc._ **2013**, _8572_, 857211.
36. Adar, F.; Atzeni, S.; Gilchrist, R.; Goldstone, L. _Detectors: Spectroscopy_; Optoelectronics World: Houston, TX, USA, 2002.
37. Li, Z.; Deen, M.; Kumar, S.; Selvaganapathy, P. Raman Spectroscopy for In-Line Water Quality Monitoring—Instrumentation and Potential. _Sensors_ **2014**, _14_, 17275–17303.
38. Li, B.; Ray, B.H.; Leister, K.J.; Ryder, A.G. Performance monitoring of a mammalian cell based bioprocess using Raman spectroscopy. _Anal. Chim. Acta_ **2013**, _796_, 84–91.
39. Beier, B.D.; Berger, A.J. Method for automated background subtraction from Raman spectra containing known contaminants. _Analyst_ **2009**, _134_, 1198–1202.
40. Sivakesava, S.; Irudayaraj, J.; Demirci, A. Monitoring a bioprocess for ethanol production using FT-MIR and FT-Raman spectroscopy. _J. Ind. Microbiol. Biotechnol._ **2001**, _26_, 185–190.

---

_© 2018 by the authors. Licensee MDPI, Basel, Switzerland. 본 논문은 Creative Commons Attribution (CC BY) 라이선스(http://creativecommons.org/licenses/by/4.0/)의 조건에 따라 배포되는 오픈 액세스 논문입니다._

> **번역 참고:** 본 문서는 위 CC BY 라이선스 원문(_Bioengineering_ **2018**, _5_, 79)을 한국어로 번역한 것입니다. 