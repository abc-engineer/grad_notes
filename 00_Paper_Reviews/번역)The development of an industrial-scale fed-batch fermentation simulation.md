# 산업 규모 유가식(Fed-batch) 발효 시뮬레이션의 개발

**저자:** Stephen Goldrick ^(a,b,c)^, Andrei Ştefan ^b^, David Lovett ^c^, Gary Montague ^(a,1)^, Barry Lennox ^(b,∗)^

- ^a^ Biopharmaceutical Bioprocess Technology Centre, Merz Court, Newcastle University, Newcastle-upon-Tyne, United Kingdom
- ^b^ Control Systems Group, School of Electrical and Electronic Engineering, University of Manchester, Manchester, United Kingdom
- ^c^ Perceptive Engineering Limited, Vanguard House, Keckwick Lane, Daresbury, Cheshire, United Kingdom

∗ 교신저자. Tel.: +44 161 306 4661. E-mail: barry.lennox@manchester.ac.uk (B. Lennox) ^1^ 현 주소: Teesside University, Middlesbrough, Tees Valley, United Kingdom

_출처: Journal of Biotechnology 193 (2015) 70–82_

---

## 논문 정보

**투고 이력**

- 접수: 2014년 7월 3일
- 수정본 접수: 2014년 10월 13일
- 게재 확정: 2014년 10월 23일
- 온라인 공개: 2014년 11월 1일

**키워드:** 산업 발효(Industrial fermentation), 동역학 모델링(Kinetic modelling), 페니실린 생산(Penicillin production), 구조화 모델(Structured model), 시뮬레이션(Simulation)

---

## 초록 (Abstract)

이 논문은 공정 시스템 분석 및 제어 연구에서 벤치마크로 사용할 수 있는 산업 규모 유가식 발효의 시뮬레이션을 기술한다. 이 시뮬레이션은 메커니즘 기반 모델(mechanistic model)을 이용하여 개발되었으며, 산업 규모 페니실린 발효 공정에서 수집된 과거 데이터(historical data)를 사용하여 검증되었다. 각 배치(batch)는 _Penicillium chrysogenum_ 의 산업용 균주를 사용하는 100,000 L 생물반응기(bioreactor)에서 수행되었다. 각 배치 동안 기록된 조작 변수(manipulated variables)는 시뮬레이터의 입력으로 사용되었고, 예측된 출력은 실제 공정에서 기록된 온라인(on-line) 및 오프라인(off-line) 측정값과 비교되었다. 시뮬레이터는 이전에 발표된 구조화 모델(structured model)을 채택하여 페니실린 발효를 기술하였으며, 이를 확장하여 용존 산소(dissolved oxygen), 점도(viscosity), 온도(temperature), pH, 용존 이산화탄소(dissolved carbon dioxide)의 주요 환경 효과를 포함하였다. 또한 질소(nitrogen)와 페닐아세트산(phenylacetic acid) 농도가 균체(biomass) 및 페니실린 생산 속도에 미치는 영향도 포함하였다. 오프가스(off-gas) 분석을 포함한 모든 온라인 및 오프라인 공정 측정값에 대한 시뮬레이션 모델 예측은 배치 기록과 잘 일치하였다. 시뮬레이터와 산업 공정 데이터는 www.industrialpenicillinsimulation.com 에서 다운로드할 수 있으며, 본 설비에 구현된 현재의 제어 전략을 평가, 연구 및 개선하는 데 사용할 수 있다.

_Crown Copyright © 2014 Published by Elsevier B.V. All rights reserved._

---

## 1. 서론 (Introduction)

항생제의 산업 규모 생산은 1940년대 페니실린의 스케일업(scaling up) 과정에서 심부 탱크 발효(deep tank fermentation)의 개발을 통해 개척되었다(Shuler and Kargi, 2002). 이 기술은 심부 탱크 발효를 핵심으로 하여 생명공학 분야를 수십억 달러 규모의 산업으로 변모시켰다. 주요 제약 및 바이오텍 기업들이 대규모 발효에 의존하고 있음에도 불구하고, 규제 제약(regulatory restrictions)으로 인해 혁신이 제한되었고 이 규모에서의 수학적 모델 개발을 포함한 고도화된 공정 제어 전략에 대한 연구개발(R&D)이 위축되었다(Grabowski et al., 1978; Yu, 2008).

발효 공정에 관한 연구의 대부분은 실험실 규모(laboratory-scale) 장비를 사용하여 수행되었으며, 이러한 연구의 일부는 제일원리(first principle) 수학적 모델의 개발에 초점을 맞추었다. 페니실린이 상업적으로 스케일업된 최초의 항생제였기 때문에, 이 공정을 정량적으로 기술하는 데 상당한 양의 연구가 집중되었다. 이러한 유형의 공정에 대해 정의된 모델은, _Penicillium chrysogenum_ 진균의 내부 구조를 고려하는 매우 복잡한 구조화 모델(Paul and Thomas, 1996; Megee et al., 1970; Nestaas and Wang, 1983; Nielsen, 1993)부터, 페니실린과 균체의 성장 프로파일에 대한 동역학적 표현에 기반한 보다 단순한 비구조화 모델(unstructured models)(Righelato et al., 1968; Birol et al., 2002; Bajpai and Reul, 1980)까지 다양하다.

지난 10년 동안 산업 응용에 더 자주 적용되어 온 것은 보다 단순한 비구조화 모델이었다(Menezes and Alves, 1994). 가장 주목할 만한 비구조화 모델은 Bajpai and Reul (1980)이 개발한 것으로, Birol et al. (2002)에 의해 확장되어 다변량 통계적 공정 모니터링 및 제어(Lee et al., 2004; Ündey and Ertunç, 2003), 회귀 모델 분석(Zhang and Lennox, 2004), 공급 전략 최적화(Ashoori et al., 2009)를 포함한 거의 모든 측면의 바이오공정 제어에 대한 표준 테스트베드(test bed)로 사용되었다. 그러나 산업에서의 제한된 모델 적용에 비추어 볼 때, 유용한 학술적 발효 모델과 실용적인 산업용 모델 사이에는 명확한 분리가 존재한다. Patnaik (2001)은 모델이 포함하는 정보가 많을수록 모델이 더 복잡해지며, 이는 모니터링 및 제어 연구에서의 "유용성(usefulness)"을 감소시킨다고 강조하였다. 그러나 단순한 비구조화 모델이 복잡한 공정 동역학을 포착하기에 충분하지 않다는 점을 고려할 때, 향상된 제어 전략의 개발을 촉진하기 위해서는 구조화 모델을 활용하여 산업 공정에 적용할 필요가 있다.

본 연구의 목적은 공정 제어 및 최적화 연구에서 벤치마크로 사용될 산업 발효의 현실적인 시뮬레이션을 개발하는 것이다. 본 연구는 Paul and Thomas (1996)가 개발한 구조화 페니실린 발효 모델의 확장을 기술하며, 공정 변수와 관련된 모든 성분 수지(component balances)를 기술한다. 시뮬레이션은 이후 10회의 100,000 L 유가식 페니실린 발효의 배치 기록을 사용하여 검증되었다. 이 시뮬레이터는 대규모 발효에서 흔히 마주치는 전형적인 문제들 — 고점도 발효 중 용존 산소 제어와 관련된 어려움, 지연된 오프라인 측정값을 이용한 핵심 영양분 제어 — 을 고려한다는 점에서 이전의 유가식 시뮬레이션을 개선한다. 시뮬레이터와 산업 공정 데이터는 www.industrialpenicillinsimulation.com 에서 다운로드할 수 있다. 이 시뮬레이터는 배치 간 변동(batch to batch variation), 입력 농도와 관련된 편차, 그리고 거품 발생(foaming), 교반기 정지(agitator tripping), 부정확한 센서와 관련된 문제 등 전형적인 공정 결함(process faults)을 포함하는 독립 실행형(stand alone) 애플리케이션으로도 사용할 수 있다. 개발된 시뮬레이터는 연구자들에게 복잡한 산업 규모 페니실린 발효 시뮬레이션에 적용 가능한 견고한(robust) 모니터링 및 제어 전략을 개발하는 도전 과제를 제공한다.

---

## 2. 산업 규모 페니실린 모델 (Industrial-scale penicillin model)

Paul and Thomas (1996)가 개발한 구조화 모델은, 다른 10개의 페니실린 모델과 비교했을 때 발효 거동을 가장 잘 기술하는 것으로 나타났기 때문에(Syndall, 1998), 본 연구에서 채택되어 구현되었다. 이 시뮬레이션은 침지(submerged) _P. chrysogenum_ 발효 동안의 균체의 성장, 형태(morphology), 대사 생산 및 퇴화(degeneration)를 고려한다. 시뮬레이션은 균체 또는 균사(hyphae)의 내부 구조를 네 개의 별개 영역으로 나눈다: 활발히 성장하는 영역(A0), 비성장 영역(A1), 액포화(vacuolation)를 통해 형성되는 퇴화 영역(A3), 그리고 자가분해(autolysed) 영역(A4)으로, 이는 Fig. 1에 나타나 있다. 본 논문은 균사의 영양분 고갈 영역을 나타내는 액포(vacuole)의 형성에 대한 기술은 생략하는데, 이 액포의 성장이 퇴화 영역(A3)의 형성을 담당한다. 액포는 Paul and Thomas (1996)에 의해 액포 영역(A2)으로 정의되었다. Paul and Thomas (1996)는 이러한 개별 영역의 형성과 성장에 대한 완전한 기술을 제공한다.

발효조(fermenter)에 대한 성분 수지가 수행되어 여기에 제시된다. 본 시뮬레이션과 관련된 매개변수는 Table 1과 Table 2에 제공되며, 구조화 페니실린 모델과 관련된 매개변수는 Table 1A에 제공된다.

**성장 영역 (Growing regions, A0):**


$$\frac{dA_0}{dt} = \underbrace{r_b}_{\text{분지(branching)}} - \underbrace{r_{diff}}_{\text{분화(differentiation)}} - \underbrace{\frac{F_{in}A_0}{V}}_{\text{희석(dilution)}} \tag{1}$$

**비성장 영역 (Non-growing regions, A1):**

$$\frac{dA_1}{dt} = \underbrace{r_e}_{\text{신장(extension)}} - \underbrace{r_b}_{\text{분지}} + \underbrace{r_{diff}}_{\text{분화}} - \underbrace{r_{deg}}_{\text{퇴화}} - \underbrace{\frac{F_{in}A_1}{V}}_{\text{희석}} \tag{2}$$

**퇴화 영역 (Degenerated regions, A3):**

$$\frac{dA_3}{dt} = \underbrace{r_{deg}}_{\text{퇴화}} - \underbrace{r_a}_{\text{자가분해(autolysis)}} - \underbrace{\frac{F_{in}A_3}{V}}_{\text{희석}} \tag{3}$$

**자가분해 영역 (Autolysed regions, A4):**

$$\frac{dA_4}{dt} = \underbrace{r_a}_{\text{자가분해}} - \underbrace{\frac{F_{in}A_4}{V}}_{\text{희석}} \tag{4}$$

**총 균체 (Total biomass, X):**

$$X = A_0 + A_1 + A_3 + A_4 \tag{5}$$

**생성물 형성 (Product formation, P):**

$$\frac{dP}{dt} = \underbrace{r_P}_{\text{생산(production)}} - \underbrace{r_h}_{\text{가수분해(hydrolysis)}} - \underbrace{\frac{F_{in}P}{V}}_{\text{희석}} \tag{6}$$

**기질 소비 (Substrate consumption, s):**

$$\frac{ds}{dt} = -\underbrace{Y_{s/X},r_e}_{\text{신장}} - \underbrace{Y_{s/X},r_b}_{\text{분지}} - \underbrace{m_s r_m}_{\text{유지(maintenance)}} - \underbrace{Y_{s/P},r_P}_{\text{생산}} + \underbrace{\frac{F_s c_s}{V} + \frac{F_{oil}c_{oil}}{V}}_{\text{공급(feed in)}} - \underbrace{\frac{F_{in}s}{V}}_{\text{희석}} \tag{7}$$

여기서 $r_{b, diff, e, deg, a, P, h, m}$ 은 각각 분지, 분화, 신장, 퇴화, 자가분해, 생성물 형성, 생성물 가수분해 및 유지의 속도이다. 배치 시간은 $t$로 표현된다. $Y_{s/X}$ 와 $Y_{s/P}$ 는 각각 균체와 페니실린의 기질 수율 계수(substrate yield coefficient)를 나타내며, $m_s$ 는 기질 유지 항(substrate maintenance term)이다. $F_s$, $F_{oil}$, $c_s$, $c_{oil}$ 은 각각 당(sugar)과 대두유(soybean oil) 공급 속도 및 농도를 나타낸다. 단순화를 위해 오일의 첨가는 당과 결합되어 대표적인 단일 기질 $s$로 형성되었다. $F_{in}$ 은 모든 공정 입력(Fdis 제외)을 나타낸다.

본 사례 연구에 특정한 발효조 부피(V) 변화는 다음과 같이 기술된다:

$$\frac{dV}{dt} = F_s + F_{oil} + F_{PAA} + F_a + F_b + F_w - F_{evp} - F_{dis} \tag{8}$$

여기서 $F_{PAA}$ 는 페닐아세트산의 유량이며, $F_a$ 와 $F_b$ 는 각각 산(acid)과 염기(base)의 유량이다. $F_w$ 는 주입용수(water for injection)의 유량으로, 일반적으로 발효액(broth) 점도를 낮추는 데 사용된다. $F_{evp}$ 는 발효조의 증발 속도이며, $F_{dis}$ 는 부피를 최대 작동 용량 내로 유지하기 위해 생산 중 용기에서 배출되는 부피이다.

시뮬레이션에 대한 수정 사항은 활발히 성장하는 영역(A0)에서 비성장 영역(A1)으로의 분화 속도($r_{diff}$)와 관련되며, 이는 원래 Megee et al. (1970)에 의해 제안되었고 Paul and Thomas (1996)에서 다음과 같이 기술되었다:

$$r_{diff} = \frac{\mu_{diff} A_0}{K_{diff} + s} \tag{9}$$

여기서 $\mu_{diff}$ 는 분화의 비속도(specific rate)이고, $s$ 는 기질 농도, $A_0$ 는 성장 영역의 농도, $K_{diff}$ 는 분화 포화 상수(differentiation saturation constant)이다. 식 (9)는 A0에서 A1로의 전이가 기질에 의해 억제되지만 매우 낮은 기질 농도(예: 생산 단계 동안)에서는 선형으로 가정할 수 있음을 의미한다. 이 제안된 메커니즘은 식 (7)의 기질 유지 항을 통해 통합되는 기질의 상당 부분을 활용한다. 이는 특히 배치의 초기 단계에서 성장과 생산에 사용 가능한 기질을 감소시킨다.

분화 속도를 Tiller et al. (1994)에서 정의된 바와 같이 평균 세포 배양 연령(mean cell culture age, $A_t$)에 비례하도록 정의함으로써 향상된 예측이 얻어졌다. 이는 분화에 대한 포화 상수를 시간 의존적 항으로 기술함으로써 모델링되었다:

$$K_{diff} = \begin{cases} 0.75 - \beta_1 A_t & K_{diff} > 0.09 \ 0.09 & K_{diff} \leq 0.09 \end{cases} \tag{10}$$

여기서 $K_{diff}$ 는 포화 상수이고 $\beta_1$ 은 상수이다. 이 수정은 분화의 비속도가 배치의 초기 단계에서는 무시할 수 있지만, 배치가 진행됨에 따라 여기서 0.09로 정의된 최소값에 도달할 때까지 점점 더 큰 영향을 미친다는 것을 의미한다.

모델에 적용된 두 번째 조정은 페니실린 생산 속도($\mu_P$)에 대한 기질 억제 효과가 가우시안 분포(Gaussian distribution)를 따른다고 가정하며, 다음과 같이 정의된다:

$$\mu_P = 2.5,\mu_{P_{max}},\sigma_P \left( \frac{e^{-\frac{1}{2}\left(\frac{s - s_{maxP}}{\sigma_P}\right)^2}}{\sigma_P \sqrt{2\pi}} \right) \tag{11}$$

여기서 $\sigma_P$ 는 페니실린 생산이 발생하는 기질 농도 범위와 관련되며, 최적 생산은 $s_{maxP}$ 로 정의된 기질 농도에서 발생한다. 이 억제 곡선은 페니실린의 최대 이론적 비생산 속도($\mu_{P_{max}}$)에 도달하는 것을 허용하는데, 이는 이론적 최대값의 70%를 얻도록 허용하는 Paul and Thomas (1996)에서 제안된 억제 곡선과 대조된다.

기술된 페니실린 모델에 더하여, 다음의 성분 수지가 시뮬레이션에 포함되었다. 다음 절에서 정의된 모든 매개변수의 값은 Table 1과 2에 제공된다.

### 2.1. 용존 산소 (Dissolved oxygen)

용존 산소(DO2)는 미생물이 성장, 유지 및 대사 생산에 사용하는 핵심 거대 영양소(macro-nutrient)로, Bajpai and Reul (1980)에 의해 다음과 같이 모델링되었다:

$$\frac{dDO_2}{dt} = -\mu_X X Y_{O_2/X} - \mu_P P Y_{O_2/P} - m_{O_2} X + k_L a(DO_2^* - DO_2) - \frac{DO_2}{V}\frac{dV}{dt} \tag{12}$$

처음 세 항은 균체 성장($\mu_X X$), 유지($m_{O_2}X$), 페니실린 생산($\mu_P P$) 동안 소비되는 산소를 나타내는 산소 소비 속도(oxygen uptake rate, OUR)를 나타낸다. $Y_{O_2/X}$ 와 $Y_{O_2/P}$ 는 각각 균체와 페니실린에 대한 산소 수율 계수이다. $\mu_X$ 는 성장, 비성장, 퇴화 및 자가분해 영역의 변화율을 나타낸다. 산소 전달 속도(oxygen transfer rate)는 부피 물질 전달 계수(volumetric mass transfer coefficient, $k_L a$)와 용존 산소 농도(DO2)와 산소 포화 농도(DO2*) 간의 차이의 곱이다. $k_L a$ 는 대두유의 효과를 고려하기 위해 Garcia-Ochoa and Gomez (2009)에서 수정되었으며 다음과 같이 정의된다:

$$k_L a = \alpha_{k_L a} V_s^a \left(\frac{P_w}{V_m}\right)^b \mu_{app}^c \left(1 - \frac{F_{oil}}{V}\right)^d \tag{13}$$

여기서 $\alpha_{k_L a}$ 는 용기와 사용된 교반기의 기하학적 매개변수에 기반한 상수이며, $V_s$ 는 표면 가스 속도(superficial gas velocity)로 $F_g/\pi r^2$ 로 취해지고, $F_g$ 는 공기의 부피 유량, $r$ 은 탱크 반경이다. 지수($a$, $b$, $c$)는 경험적 값으로, Garcia-Ochoa and Gomez (2009)에 의해 $0.4 \leq a \leq 1$, $0.3 \leq b \leq 0.7$, $-0.4 \leq c \leq -0.7$ 범위에 있는 것으로 나타났다. 지수 $d$ 는 0.25로 취해졌는데, 이는 후술하는 사례 연구에서 강조된 바와 같이 대두유의 유량이 증가함에 따라 관찰된 $k_L a$ 의 감소를 고려하기 위한 것이다. 유사한 결과가 Chern et al. (2001)에 의해 보고되었는데, 이들은 500 L 탱크에서 대두유 첨가에 따른 $k_L a$ 의 감소를 발견하였다. 이 $k_L a$ 항은 생물반응기에서 산소의 물질 전달에 대한 오일 및 소포제(antifoam agents)의 잘 알려진 효과를 고려한다(Junker, 2007; Kawase and Moo-Young, 1990; Routledge, 2012).

산소 포화 농도(DO2*)는 다음과 같이 헨리의 법칙(Henry's law)을 사용하여 계산되었다:

$$DO_2^* = \frac{O_{2,in} P_{lm}}{H_{O_2}} \tag{14}$$

여기서 $O_{2,in}$ 은 용기로 들어가는 공기 중의 산소 농도이고, $P_{lm}$ 은 용기의 로그 평균 압력(log mean pressure)이며, $H_{O_2}$ 는 헨리 평형 상수로 Scragg (1991)에서 얻어졌다. 총 동력 소비(total power consumption, $P_w$)는 교반(agitation, $P_{ag}$)에 필요한 동력 — Albaek et al. (2012)에서 가져옴 — 과 통기(aeration, $P_{air}$)에 필요한 동력 — Roels and Heijnen (1980)에서 가져옴 — 의 합으로 취해졌다.

$$P_{ag} = \frac{n P_o \rho_b N_{rpm}^3 D^5 (P_{ag}/P_{ungassed})}{1000} \tag{15}$$

여기서 $n$ 은 임펠러 수, $P_o$ 는 Uhl and Gray (1966)에서 러시턴 임펠러(Ruston impeller)를 사용하는 용기 내 난류 조건을 가정하여 약 5로 근사한 비통기 임펠러 동력 수(unaerated impeller power number)이며, $N_{rpm}$ 은 rpm, $D$ 는 임펠러의 직경이다. 발효액 밀도는 매질의 밀도와 균체 및 페니실린 농도를 모두 고려하여 동적으로 모델링되었으며 $\rho_b = 1100 + X + P$ 로 취해졌다. 상대 동력 소모(relative power draw, $P_{ag}/P_{ungassed}$)는 Scragg (1991)에서 통기 동력 소비($P_{ag}$)와 비통기 동력 소비($P_{ungassed}$)의 비율로 계산되며, 이는 통기 속도의 함수로 0.4에서 0.6 범위로 나타났다. 통기 동력 요구량은 다음과 같이 계산된다:

$$P_{air} = \frac{V_s R T_b V_m}{22.4 Z} \ln\left(1 + \frac{\rho_b g Z}{P_0}\right) \tag{16}$$

여기서 $R$ 은 보편 기체 상수(universal gas constant), $T_b$ 는 용기 온도, $g$ 는 중력 상수, $P_0$ 는 용기 바닥의 압력으로 다음과 같이 계산된다:

$$P_0 = P_1 + \rho_b g(1 - \varepsilon)Z \tag{17}$$

여기서 $P_1$ 은 용기 배압(back pressure), $Z$ 는 비통기 액체 높이(ungassed liquid height), $\varepsilon$ 은 일정하다고 가정된 가스 홀드업 계수(gas hold-up coefficient)이다.

DO2 농도의 제어는 호기성 발효에서 매우 중요하며, 임계 농도(DO2crit) 이상으로 유지되는 한 모든 미생물 활동은 영향을 받지 않는다고 가정할 수 있다(Finn, 1954). 그러나 이 임계 한계 미만의 DO2 농도는 균체 성장 및 대사 생산의 급격한 감소를 초래하며, 이것이 신속히 시정되지 않으면 일반적으로 배치 실패가 임박한다. 페니실린 발효에서 세포 성장 및 대사 생산에 대한 산소 억제의 임계값은 Vardar and Lilly (1982)에 의해 조사되었으며 두 개의 구별되는 값으로 나타났다. 이들은 공기 포화도 30% 미만에서 페니실린의 비성장 속도가 급격히 감소하고, 공기 포화도 10% 미만에서는 페니실린 생산이 비가역적으로 손상됨을 관찰하였으며, 유사한 결과가 Rolinson (1952)에 의해서도 보고되었다.

이러한 물리적 현상을 고려하기 위해, 시뮬레이션은 균체 및 페니실린의 비성장 속도를 쌍곡 탄젠트 함수(hyperbolic tangent function)를 사용하여 DO2 농도와 연관시킨다. 페니실린 생산($\mu_P$)의 경우, 이 관계는 DO2 농도가 임계값인 공기 포화도 30%(Vardar and Lilly (1982)에서 가져옴) 이상인 경우 $\mu_P$ 가 영향을 받지 않는다고 가정한다. 그러나 DO2가 이 값 아래로 떨어지면 $\mu_P$ 는 사실상 0이 된다. 이 관계는 0에서 1까지 범위를 갖는 쌍곡 탄젠트 함수를 사용하여 모델링되었으며, 다음과 같이 기술된다:

$$\mu_P \approx 0.5,\mu_P \left(1 - \tanh\left(A_{inhib}(DO_{2critP} - DO_2)\right)\right) \tag{18}$$

여기서 $DO_{2critP}$ 는 임계 DO2 농도이고 $A_{inhib}$ 는 DO2 농도가 $DO_{2critP}$ 의 임계값 아래로 떨어질 때 $\mu_P = \mu_P$ 에서 $\mu_P = 0$ 으로의 전이 가파름(steepness)과 관련된 상수이다. 이러한 유형의 관계는 Hegewald et al. (1981)에 의해서도 DO2가 임계값 아래로 떨어진 결과 관찰된 페니실린 생산 감소를 성공적으로 모델링하는 것으로 나타났다.

Vardar and Lilly (1982)에서 논의된 바와 같이 DO2가 공기 포화도 10% 미만으로 떨어지는 효과를 고려하기 위해, 본 시뮬레이션은 이 값 미만의 DO2 농도에서는 모든 세포 대사가 중단된다고 가정하고, DO2를 균체의 비성장 속도($\mu_X$)와 연관시켜 모델링하였으며 다음과 같이 정의된다:

$$\mu_X \approx 0.5,\mu_X \left(1 - \tanh\left(A_{inhib}(DO_{2critX} - DO_2)\right)\right) \tag{19}$$

여기서 $DO_{2critX}$ 는 균체에 대한 DO2 농도의 임계값을 나타낸다. 식 (19)는 DO2가 $DO_{2critX}$ 이상이면 $\mu_X = \mu_X$ 이지만, DO2가 $DO_{2critX}$ 미만이면 $\mu_X$ 가 사실상 0이 됨을 가정하며, $A_{inhib}$ 는 식 (18)에서와 같이 정의된다.

### 2.2. 용존 이산화탄소 (Dissolved carbon dioxide)

용존 이산화탄소(CO2,L)는 발효 모델링에서 중요하지만 종종 간과되는 변수로, 발효액 내 CO2,L의 축적이 세포 성장 및 생산성에 해로운 것으로 보고되었다(Frick and Junker, 1999). 그러나 정확하고 견고한 분석기의 부족으로 인해 그 광범위한 온라인 측정이 제한되어 왔다. 발효에서의 용존 이산화탄소는 Royce (1992)에 의해 $k_L a$ 뿐만 아니라 pH 및 용기 압력의 환경 조건에 의해 영향을 받는 것으로 나타났다. 여기서 제안된 모델은 pH가 일반적으로 일정하게 유지되므로 pH 효과가 무시할 만하다고 가정하고 다음과 같이 모델링한다:

$$\frac{dCO_{2,L}}{dt} = \delta_{c/o} k_L a(CO_{2,L}^* - CO_{2,L}) - \frac{CO_{2,L}}{V}\frac{dV}{dt} \tag{20}$$

여기서 $\delta_{c/o}$ 는 이산화탄소 대 산소 물질 전달 계수의 비율이다. $C_{LCO_2}^*$ 는 최대 용존 이산화탄소 농도로, CO2의 오프가스 측정값에 비례한다고 가정되며 다음과 같이 취해진다(Royce, 1992):

$$C_{LCO_2}^* = \frac{P_{lm} CO_{2out}}{H_{CO_2}} \tag{21}$$

여기서 $CO_{2out}$ 은 오프가스 내 CO2의 백분율 농도, $P_{lm}$ 은 로그 평균 압력, $H_{CO_2}$ 는 이산화탄소에 대한 헨리의 법칙 상수이다.

사례 연구에서 CO2,L은 측정되지 않았지만, 운전자들은 오프가스 분석의 $CO_{2out}$ 을 사용하여 이를 근사하였다. 이 근사는 운전자들이 CO2,L이 너무 높은 기간을 판단하고 균체에 대한 해로운 영향과 생성물 형성에 대한 영향을 피하기 위해 시정 조치를 취할 수 있게 하였다. 이 관계를 모델링하기 위해, 시뮬레이션은 CO2,L 농도가 임계값($CO_{2,LcritX}$) 미만인 경우 비성장 속도($\mu_X$)가 영향을 받지 않는다고 가정하였다. 그러나 이 값 이상의 CO2,L 농도에서는 $\mu_X$ 가 0이 된다. 이는 0에서 1까지 범위를 갖는 쌍곡 탄젠트 함수를 사용하여 모델링되었으며 다음과 같이 정의된다:

$$\mu_X \approx 0.5,\mu_X \left(1 + \tanh\left(A_{inhib}(CO_{2,LcritX} - CO_{2,L})\right)\right) \tag{22}$$

여기서 $CO_{2,LcritX}$ 는 CO2,L의 임계값을 나타내며 $A_{inhib}$ 는 식 (18)에서와 같이 정의된다.

### 2.3. 질소 (Nitrogen)

발효 매질에서 두 번째로 풍부한 영양소는 일반적으로 질소원(nitrogen source)이며, 이는 성장에 필수적이고 생성물의 대사 생산에 요구된다(Vogel and Todaro, 1997). 각 배치에 대한 주요 질소원은 일반적으로 초기 매질에 함유되어 있으며 배치 전반에 걸쳐 소비된다. 이 소비는 균체 성장 및 유지 동안 소비되는 질소와 페니실린 생산에 활용되는 질소를 고려한 물질 수지를 사용하여 모델링되며, 다음과 같이 정의된다:

$$\frac{dN}{dt} = \frac{F_{oil}c_{Noil} + F_{PAA}c_{NPAA} + N_{shots}c_{Nshots}}{V} - \mu_X X Y_{N/X} - \mu_P X Y_{N/P} - m_N X - \frac{N}{V}\frac{dV}{dt} \tag{23}$$

시뮬레이션은 입력 공급물 $F_{oil}$ 과 $F_{PAA}$ 의 질소 조성과, 질소 농도를 빠르게 증가시키기 위해 첨가되는 황산암모늄 염($N_{shots}$)을 고려한다. 이러한 입력의 질소 농도($i$)는 $c_{Ni}$ 로 표현된다. 질소 대 균체 및 페니실린의 수율 계수는 각각 $Y_{N/X}$ 와 $Y_{N/P}$ 로 표현되었다.

산업 페니실린 생산에 대한 핵심 거대 분자로서의 질소의 중요성은 McIntyre et al. (1999)에서 입증되었는데, 이들은 질소 제한 기간 동안 균체 성장의 감소를 관찰하였다. 유사한 결과가 사례 연구에서도 관찰되었는데, 200 mg L⁻¹ 미만의 질소 농도에서 균체 성장 속도가 감소하는 것으로 나타났다. 이 관계를 모델링하기 위해, 시뮬레이션은 질소 농도가 임계값($N_{critX}$) 이상인 경우 비성장 속도($\mu_X$)가 영향을 받지 않는다고 가정하였다. 그러나 이 값 미만의 질소 농도에서는 $\mu_X$ 가 0이 된다. 이는 0에서 1까지 범위를 갖는 쌍곡 탄젠트 함수를 사용하여 모델링되었으며 다음과 같이 정의된다:

$$\mu_X \approx 0.5,\mu_X \left(1 - \tanh\left(A_{inhib}(N_{critX} - N)\right)\right) \tag{24}$$

여기서 $N_{critX}$ 는 균체 성장에 대한 질소의 임계 농도이고 $A_{inhib}$ 는 식 (18)에서와 같이 정의된다.

### 2.4. 전구체 첨가 (Precursor addition)

일부 발효는 원하는 생성물의 대사 생산을 보장하기 위해 전구체(precursor)의 첨가를 필요로 한다. 이는 여기서 제시된 산업 사례 연구에서 특히 중요한데, 페니실린 합성을 위한 원하는 측쇄(side chain)를 공급하기 위해 페닐아세트산(PAA)이 첨가된다. Hillenga et al. (1995)는 이 흡수 속도를 조사하여 PAA가 수동 확산(passive diffusion)을 통해 세포막을 가로질러 흡수되며 pH를 포함한 환경 조건에 의해 영향을 받는다는 것을 발견하였다. 그러나 Fernandez-canon et al. (1989)은 PAA의 흡수 속도가 특정 수송 시스템을 통하며 탄소원과 엄격하게 관련된다고 보고하였다. 본 연구에서 이용 가능한 제한된 데이터에 기반하여, 개발된 시뮬레이션은 환경 조건을 무시하고 균체 성장, 페니실린 생산 및 페니실린 유지에 기반한 단순화된 PAA 흡수 속도를 제안하며, 다음과 같이 모델링된다:

$$\frac{dPAA}{dt} = \frac{F_{PAA}c_{PAA}}{V} - Y_{PAA/P}\mu_p P - Y_{PAA/X}\mu_X X - m_{PAA}P - \frac{PAA}{V}\frac{dV}{dt} \tag{25}$$

여기서 $F_{PAA}$ 는 PAA의 유량이고 $c_{PAA}$ 는 공급 용액 농도이다. $Y_{PAA/P}$ 와 $Y_{PAA/X}$ 는 각각 페니실린과 균체에 대한 PAA의 수율 계수이며, $m_{PAA}$ 는 페니실린 농도와 관련된 유지 항이다.

$F_{PAA}$ 의 최적 제어는 페니실린 발효에서 주요 과제인데, 배양액 내 높은 수준의 PAA가 성장과 페니실린 생산을 억제하여 균체에 독성이 있는 것으로 알려져 있기 때문이다(Hillenga et al., 1995). 더욱이 PAA는 가장 비싼 원료 중 하나로 모든 원료 비용의 11%를 차지하므로(Herschbach et al., 1984), 그 첨가는 신중하게 모니터링되어야 한다. 산업 사례 연구에서 PAA 농도는 $F_{PAA}$ 의 조작을 통해 10개 배치 모두에서 200~2000 mg L⁻¹ 의 최적 범위 사이로 제어되는 것으로 나타났다. 유사한 최적 범위가 Herschbach et al. (1984)에서 보고되었다. PAA를 이 범위 내로 유지하는 것은 Hillenga et al. (1995)에 의해 강조된 높고 낮은 PAA 농도의 억제 효과를 완화하는 것으로 가정되었다. 이 관계를 모델링하기 위해, 시뮬레이션은 두 가지 억제 항을 포함하였다: 첫 번째는 $PAA_{critX}$(2000 mg L⁻¹) 이상의 PAA 농도에서 균체 성장 속도의 감소를 가정하고, 두 번째는 $PAA_{critP}$(200 mg L⁻¹) 미만의 PAA 농도에서 페니실린 성장 속도의 감소를 가정한다. 이러한 억제 항들은 0에서 1까지 범위를 갖는 쌍곡 탄젠트 함수를 사용하여 다음과 같이 모델링되었다:

$$\mu_X \approx 0.5,\mu_X \left(1 + \tanh\left(A_{inhib}(PAA_{critX} - PAA)\right)\right) \tag{26}$$

$$\mu_P \approx 0.5,\mu_P \left(1 + \tanh\left(A_{inhib}(PAA - PAA_{critP})\right)\right) \tag{27}$$

이 관계는 PAA > $PAA_{critX}$ 인 경우 $\mu_X$ 가 사실상 0이고 이 값 미만의 PAA 농도에서는 $\mu_X$ 가 영향을 받지 않음을 가정한다. 유사하게 PAA < $PAA_{critP}$ 인 경우 $\mu_P$ 가 사실상 0이고 이 값 이상의 PAA 농도에서는 $\mu_P$ 가 영향을 받지 않는다. 두 식 모두에서 $A_{inhib}$ 는 식 (18)에서와 같이 정의된다.

### 2.5. 점도 (Viscosity)

점도는 발효액의 유변학적(rheological) 특성의 함수이다. 사상균(filamentous fungi)의 경우, 이는 펠릿(pellet) 또는 사상(filamentous) 형태로 특징지어지는 형태에 의존한다(Olsvik and Kristiansen, 1994). 펠릿 형태는 분지하는 균사가 서로 얽혀 안정적인 응집체를 형성한 결과이다. 이 형태는 점도가 낮아 선호되지만, 펠릿 내 영양분 제한이 문제가 될 수 있다. 두 번째 형태는 사상형으로, 길게 분지하는 균사가 신장하여 복잡한 3차원 구조를 형성하는 결과이다. 각 발효 동안의 우세한 형태는 균주 유형, 포자 접종(spore inoculum) 농도 및 품질, 그리고 교반을 포함한 여러 요인에 의존한다(Posch et al., 2013).

본 연구에서 이 복잡한 과정을 모델링하기 위해, 분지(A0) 영역의 농도가 사상 형태와 관련되며 점도와 관련된 유일한 요인이라고 가정하였다. A0 영역의 성장을 점도와 연관시키기 위해, 이 형태의 성장이 Metz and Kossen (1977)에서 논의된 진균 펠릿의 성장을 기술하는 데 사용된 성장 패턴인 "세제곱근(cube root)" 성장 관계를 사용하여 기술될 수 있다고 가정하였다. 이 공정에서 기록된 점도의 관찰된 지연(lag)을 더 잘 고려하기 위해 이 관계에 성장 지연이 추가되었다. 여기에 추가된 지연 성장 모델은 Lin et al. (2000)에 의해 배치 배양에서 미생물 세포 성장을 정확하게 모델링하는 것으로 나타났다. 추가적으로, 배치 기록에서 기록된 점도는 주입용수(Fw)의 첨가에 따라 감소하는 것으로 나타났다. 그 결과, 이 효과가 모델에 포함되었다. 이는 다른 곳에서 보고되지 않았지만, 대량의 물 첨가가 점성이 있는 사상 형태를 더 작은 응집체나 펠릿으로 분해하는 데 도움을 주어 점도를 감소시킬 수 있다.

여기서 개발된 점도 관계는 경험적 관계로 간주될 수 있으며 발효액 점도에 기여하는 근본적인 현상을 설명하는 것을 목표로 하지 않는다. 이 관계는 다음과 같이 정의된다:

$$\frac{d\mu_{vis}}{dt} \approx A_0^{\frac{1}{3}} \left( \frac{1}{1 + e^{-k_{in}(t - t_{in})}} \cdot \frac{1}{1 + e^{k_{de}(t - t_{de})}} \right) - k_{water}F_w \tag{28}$$

여기서 $\mu_{vis}$ 는 겉보기 점도(apparent viscosity)이고 $k_{water}$ 는 물 첨가의 결과로 사상 형태가 분해되는 정도와 관련된 상수이다. 상수 $k_{in}$, $t_{in}$, $k_{de}$, $t_{de}$ 는 Lin et al. (2000)에서 정의된 지연 성장 모델과 관련되며 $t$ 는 배치 시간이다. 이 값들은 Table 2에서 이용 가능하다.

### 2.6. 온도와 pH (Temperature and pH)

온도와 pH는 모두 산업 규모 생물반응기에서 기록되는 핵심 공정 매개변수이다. 이 변수들의 모델링과 그 제어는 부록 A, 보충 자료(Supplementary data)에서 논의된다.

### 2.7. 생성물 가수분해 (Product hydrolysis)

정확한 온도 및 pH 제어는 지속적인 세포 성장 및 생성물 형성에 필요할 뿐만 아니라 생성물 가수분해 속도($k$)에도 영향을 미칠 수 있다. 가수분해 속도는 이전에 상수로 모델링되었다(Bajpai and Reul, 1980; Birol et al., 2002; Tiller et al., 1994; Paul and Thomas, 1996). 그러나 페니실린의 분해가 온도와 pH 모두의 함수임이 밝혀졌으며(Kheirolomoom et al., 1999; Lu et al., 2008), Kheirolomoom et al. (1999)에 의해 정의된 바와 같이 2차 다항식을 사용하여 모델링될 수 있다:

$$\log(k) = B_1 + B_2 ,pH + B_3 T_b + B_4 ,pH^2 + B_5 T_b^2 \tag{29}$$

여기서 상수 $B_{1,2,3,4,5}$(Table 2에서 이용 가능)는 Paul and Thomas (1996)에서 원래 제안된 값과 동일하도록, pH 6.5와 온도 298K에서 ≈ 0.003 h⁻¹ 의 가수분해 속도를 제공하도록 시뮬레이션에서 수정되었다.

### 2.8. 오프가스 분석 (Off-gas analysis)

오프가스 분석은 발효조의 헤드스페이스(head space)를 떠나는 배기 가스를 모니터링하는 것을 포함한다. 이는 배양의 무균성(sterility)을 손상시키지 않는 비침습적(non-invasive) 공정으로, 발효액과 접촉하는 인-시추(in-situ) 프로브에 비해 명확한 이점을 제공한다. 이 기술은 입구 및 출구 가스 흐름에서 CO2와 O2의 농도를 모니터링하는 것을 포함한다. 오프가스 산소 농도($O_{2out}$)는 여기서 % 단위로 측정되었으며 Scragg (1991)에서 다음과 같이 채택되었다:

$$\frac{dO_{2out}}{dt} = \frac{Q_{gin}O_{2,in} - Q_{gout}O_{2,out} - k_L a(DO_2^* - DO_2)V_L}{29V_g/22.4} \tag{30}$$

여기서 $Q_{gin}$ 과 $Q_{gout}$ 은 각각 입구와 출구의 공기 질량 유량으로 취해진다. $Q_{gout}$ 은 식 (32)에서와 같이 불활성 가스인 질소에 대한 물질 수지를 수행하여 결정되었다. $O_{2in}$ 과 $O_{2out}$ 은 각각 입구와 가스 출구의 산소 농도이다. $V_g$ 는 용기 내 가스의 부피로 $\varepsilon V_L$ 로 취해지며, $O_{2out}$ 을 % 단위로 산출하기 위해 여기서 질량으로 변환된다. 유사하게, CO2의 오프가스 계산은 다음과 같이 계산되었다:

$$\frac{dCO_{2out}}{dt} = \frac{Q_{gin}CO_{2,in} - Q_{gout}CO_{2,out} + CER_X}{29V_g/22.4} \tag{31}$$

여기서 $CER_X$ 는 균체와 직접 관련된 것으로 취해진 탄소 발생 속도(carbon evolution rate)이다: $CER_X = V\mu_X/Y_{CO_2-X}$, 여기서 $Y_{CO_2-X}$ 는 CO2의 수율 계수이다(Scragg, 1991). 오프가스 분석에서 CO2와 O2 농도를 측정하면 발효의 실시간 모니터링에서 유용한 도구인 산소 소비 속도(OUR)와 탄소 발생 속도(CER)를 계산할 수 있으며, Scragg (1991)에서 다음과 같이 계산된다:

$$OUR = \frac{32}{22.4}F_{gin}\left(O_{2in} - O_{2out}\frac{N_{2in}}{1 - O_{2out} - CO_{2out}}\right)$$

$$CER = \frac{44}{22.4}F_{gin}\left(CO_{2out}\frac{N_{2in}}{1 - O_{2out} - CO_{2out}} - CO_{2in}\right) \tag{32}$$

### 2.9. 성장 억제 항의 요약 (Summary of growth inhibition terms)

최종 균체의 비성장은 다음과 같이 정의된다:

$$\mu_X = \mu_X (DO_{2Xinhib})(dCO_{2inhib})(N_{inhib})(PAA_{Xinhib})(T_{inhib})(pH_{inhib}) \tag{33}$$

여기서 $DO_{2Xinhib}$ 는 식 (19)에서 정의된 균체 비성장 속도에 대한 용존 산소의 억제 효과이다. 유사하게, $dCO_{2inhib}$ 는 식 (22), $N_{inhib}$ 는 식 (24), $PAA_{Xinhib}$ 는 식 (26), $T_{inhib}$ 는 식 (A-3), $pH_{inhib}$ 는 식 (A-10)에 의해 정의된다.

마찬가지로 최종 페니실린의 비생산 속도는 다음과 같이 정의된다:

$$\mu_P = \mu_P (DO_{2Pinhib})(PAA_{Pinhib}) \tag{34}$$

여기서 $DO_{2Pinhib}$ 는 식 (18)에서 정의된 페니실린 생산 속도에 대한 용존 산소의 억제 효과이며, $PAA_{Pinhib}$ 는 식 (27)에 의해 정의된다.

---

## 3. 사례 연구: 산업 규모 페니실린 생산 (Case study: industrial-scale penicillin production)

시뮬레이션은 산업 규모 생물반응기에서 수행된 10회의 페니실린 발효의 배치 기록으로 구성된 사례 연구를 사용하여 검증되었다.

### 3.1. 재료 및 방법 (Materials and methods)

산업 페니실린 발효는 _P. chrysogenum_의 산업용 균주를 사용하여 100,000 L 생물반응기에서 수행되었다. 이 생산 설비의 초기 접종(inoculum) 충전은 1차(1000 L) 및 2차(10,000 L) 종균(seed) 용기의 두 종균 단계를 사용하여 생성되었다. 균주 선택, 매질 조성 및 분석 방법에 관한 구체적인 세부 사항은 기밀상의 이유로 생략되었다.

### 3.2. 공정 설명 및 운전 (Process description and operation)

생물반응기의 구성은 Shuler and Kargi (2002)에서 이용 가능한 전통적인 100,000 L 생물반응기와 일치하며, Fig. 2에 나타나 있다. 생물반응기는 탱크 반경(r) 2.1 m, 내부 반경(rimp) 0.85 m의 러시턴 임펠러 3개를 가지며 100 rpm의 고정 교반으로 운전되었다. 용기에는 pH, 온도, 용존 산소, 거품 발생 및 압력 센서가 장착되었다. 페니실린, 질소 및 점도의 오프라인 측정값은 24시간마다 샘플링 및 수집되었고, 오프라인 페닐아세트산 측정값은 12시간마다 취해졌다. 이 외에도, 산소와 이산화탄소의 농도는 오프가스 분석을 통해 모니터링되었다. 대두유와 기질의 공급 속도는 사전 결정된 최적 프로파일을 사용하는 순차 배치 제어(sequential batch control)를 통해 제어되었으며, 배치 전반에 걸쳐 공정 거동에 대응하여 운전자에 의해 수동으로 조정되었다. 유사하게, 통기 속도와 용기 배압 모두 원하는 용존 산소 농도 수준을 유지하고 거품 발생 및 높은 $CO_{2out}$ 수준을 포함한 공정 문제에 대응하기 위해 순차 배치 제어를 사용하여 조작되었다. 대두유는 2차 탄소원으로 활용되었을 뿐만 아니라 소포제(anti-foaming agent)로도 작용하였다. 페닐아세트산 유량은 그 농도의 오프라인 측정값에 기반하여 수동으로 조정되었다. 질소는 각 배치의 초기 배지에 존재하였으며 오프라인 측정값을 사용하여 전반에 걸쳐 모니터링되었다. 낮은 질소 수준은 황산암모늄 샷(shots)의 첨가를 통해 시정되었다. 내부 냉각 코일을 통한 냉각수와 산/염기 용액의 첨가는 PID 제어기를 사용하여 온도를 298K, pH를 6.5로 각각 제어하는 데 사용되었다. 용기 중량은 로드 셀(load cell)을 사용하여 온라인으로 기록되었으며, 이는 생물반응기의 용량이 초과되지 않도록 배출을 스케줄링하는 데 사용되었다. 이러한 배출은 또한 더 긴 배치를 달성할 수 있게 한다.

### 3.3. 발효 데이터 (Fermentation data)

Table 3에 요약된 배치 기록은 매개변수 추정과 시뮬레이션 검증에 사용되었다. 이 기록들은 이 설비에서 발견되는 전형적인 배치 간 변동과 흔히 마주치는 일부 공정 관련 문제들을 강조한다. 따라서 이 사례 연구는 시뮬레이션을 검증하기에 이상적인 데이터를 제공한다. 배치 길이는 현재 배치 진행 상황과 하류 처리(downstream processing) 단위 공정의 가용성에 따라 결정되었다. 균체의 최대 비성장 속도($\mu_{Xmax}$)는 탄소 발생 속도(CER)를 사용하여 추정된 균체($X_{est}$)로부터 계산되었으며, 다음과 같이 정의된다:

$$\frac{dX_{est}}{dt} = \frac{CER - m_{CO_2}X_{est}}{Y_{CO_2/X}} \tag{35}$$

여기서 $m_{CO_2}$ 는 CO2에 대한 유지 생산 항이고 $Y_{CO_2/X}$ 는 CO2 수율 계수이다. 탄소 발생 속도(CER)와 산소 소비 속도(OUR) 모두 균체의 온라인 추정에 사용될 수 있다. 그러나 발효 기술자들 사이에서는 CER 측정값의 사용이 선호된다(Royce, 1992). 추가로, Table 3은 각 배치의 처음 세 개 오프라인 페니실린 측정값으로부터 계산된 페니실린의 최대 비성장 속도($\mu_{Pmax}$)와 관련된 변동을 강조한다. Fig. 2에 강조된 주요 공정 입력과 출력은 각 배치 동안 시간별로 기록되었다. 냉각수와 산/염기 유량은 본 연구에서 이용할 수 없었다.

### 3.4. 매개변수 추정 (Parameter estimation)

시뮬레이션의 매개변수는 균주에 강하게 의존하고 공정 특이적일 것으로 예상된다. 그러나 일부 매개변수는 배치 기록에서 추정할 수 없었기 때문에 관련 문헌 출처에서 이러한 매개변수를 추정하는 것이 충분하다고 간주되었다. 산소, 질소 및 페닐아세트산의 임계 한계를 포함한 일부 매개변수는 이 설비의 운전자로부터 수집한 공정 정보에 기반하였다. 페니실린 모델과 관련된 매개변수는 Table 1A에 요약되어 있고, 환경 조건과 관련된 공정 매개변수는 Table 2에 요약되어 있으며, 나머지는 Table 2A에서 이용 가능하다. PID 제어기 한계 및 게인(gain)은 Table 3A에서 이용 가능하다. 이 매개변수들이 사례 연구의 10개 배치 모두에 대해 기록된 값과 비교하여 주요 공정 출력의 합리적인 예측을 제공하는 것으로 나타났기 때문에, 주어진 매개변수 집합을 최적화하려는 시도는 이루어지지 않았다.

### 3.5. 민감도 분석 (Sensitivity analysis)

모든 시뮬레이션 매개변수에 대해 민감도 분석을 수행하여 이러한 입력의 불확실성이 시뮬레이션에 미치는 영향을 연구하였다. 민감도 측도(sensitivity measure) $\delta^{msqr}$ 은 Sin et al. (2009)에 설명된 바와 같이 각 매개변수 $\theta$ 의 유의성을 순위화하는 데 사용되었다. 시뮬레이션의 6개 주요 출력에 영향을 미친 상위 10개 순위 매개변수는 Table 4에 요약되어 있다.

특정 매개변수들은 많은 수의 출력에 매우 큰 영향을 미치는 것으로 나타났다. 이러한 매개변수 중에는 기질의 입구 농도 $c_s$ 와 오일의 입구 농도 $c_{oil}$ 이 있었는데, 입력 농도의 측정값이 없었기 때문에 본 연구에서는 이를 일정하다고 가정하였다. $\mu_{Xmax}$ 와 $\mu_{Pmax}$ 는 각 배치에 대해 계산되었으며 이 매개변수들은 기질 및 페니실린 농도 모두에 유의한 영향을 미치는 것으로 나타났다. 흥미롭게도, $\mu_{Xmax}$ 는 균체에 유의한 영향을 미치지 않는 것으로 나타났는데, 이는 Table 3에 강조된 바와 같이 이 매개변수 값의 큰 변동에도 불구하고 각 배치의 균체 프로파일이 상대적으로 유사했던 이유를 설명할 수 있다. Table 4는 또한 입구 냉각수 온도 $T_{cin}$ 과 살포된 산소 입구 가스 농도 $O_{2in}$ 같은 조작 변수의 중요성과 그것들이 각각 온도와 용존 산소의 공정 출력에 미치는 큰 영향을 강조한다. 더욱이 용기 치수가 특정 모델 출력에 영향을 미치는 것으로 나타났는데, 임펠러 반경(rimp)과 용기 반경(r)이 용존 산소 농도(DO2)에 영향을 미쳤다.

### 3.6. 산업 페니실린 시뮬레이션 (Industrial penicillin simulation)

시뮬레이션은 산업 사례 연구의 배치 기록을 사용하여 검증되었다. 이는 각 배치 기록에서 정의된 용존 산소, 온도, pH, 페닐아세트산, 질소, 페니실린, 용기 중량, 점도, 산소 및 이산화탄소 오프가스 농도의 초기 조건으로 시뮬레이션을 초기화하여 수행되었다. 초기 기질 농도는 1 g L⁻¹, 초기 용존 이산화탄소는 0 g L⁻¹ 로 취해졌다. 초기 균체 농도는 각 배치에 대해 일정하다고 가정하였으며 0.5 g L⁻¹ 로 취해졌다. Table 3에 제공된 균체($\mu_{Xmax}$)와 페니실린($\mu_{Pmax}$)의 최대 비성장 속도는 각 배치의 모델 입력으로 사용되었다. 배치 기록에 의해 결정된 배치 길이($t$)는 시뮬레이션 실행 시간을 정의하는 데 사용되었다.

조작 변수는 당 유량($F_s$), 대두유 유량($F_{oil}$), 주입용수($F_w$), 통기 속도($F_g$), 용기 배압($P_1$), 배출 속도($F_{dis}$)였다. 이 변수들은 0.2 h의 샘플링 속도를 사용하여 보간(interpolate)되어 시뮬레이션 입력으로 사용되었다. 시뮬레이션은 용기가 산업 공정의 정상 운전과 일치하는 100 rpm의 고정 교반으로 운전된다고 가정하였다. 산/염기 및 냉각수 유량은 본 연구에서 이용할 수 없었으므로, 이들은 최적 pH 6.5와 온도 298K에서 공정을 유지하기 위해 폐루프(closed loop)로 작동하는 PID 제어기의 출력으로 취해졌다.

시뮬레이션의 출력은 균체(X), 페니실린(P), 기질(s), 용존 산소(DO2), 온도(T), pH, 중량(W), 점도($\mu_{app}$), 페닐아세트산(PAA), 질소(NH3), 용존 이산화탄소(CO2,L) 및 산소($O_{2out}$)와 이산화탄소($CO_{2,out}$)의 오프가스 농도였다. 오프가스 농도는 식 (32)를 사용하여 이산화탄소 발생 속도(CER)와 산소 소비 속도(OUR)를 계산하는 데 사용되었다. 이용 가능한 경우 시뮬레이터의 모든 예측은 배치 기록에 기록된 것과 비교되었다.

---

## 4. 결과 및 논의 (Results and discussion)

Fig. 3은 공칭(nominal) 매개변수 집합을 사용하여 Batch 3(이용 가능한 가장 긴 배치)에서 선택된 6개 출력을 배치 기록과 비교함으로써 시뮬레이션의 예측 능력을 강조한다. 상대적으로 작은 부피에서 수행된 발효 데이터를 사용하여 검증된 이전 시뮬레이션(Paul and Thomas (1996)와 Paul et al. (1998)에서 V = 2 L, Menezes and Alves (1994)에서 V = 1000 L)과 대조적으로, 여기에 나타난 시뮬레이션 예측은 산업 규모 생물반응기(부피 = 100,000 L)에서 수행된 발효에 유효하다. 추가로, 시뮬레이션은 더 짧은 배치 길이의 데이터를 사용하여 검증된 이전 시뮬레이션(Paul and Thomas (1996)에서 t = 160, Megee et al. (1970)에서 t = 90, Tiller et al. (1994)에서 t = 200)에 비해 320시간까지의 배치에 대해 정확한 예측을 제공하는 것으로 나타났다. 나머지 9개 배치에 대해서도 유사한 예측이 기록되었다.

본 논문에서 제안된 페니실린 모델은 산업 공정에서 기록된 측정값과 비교했을 때 균체(X)와 페니실린(P)의 정확한 예측을 제공한다. 식 (10)에서 정의된 $K_{diff}$ 의 결정은 배치 시작 시 균체 성장 속도의 증가와 150시간 이후 관찰된 감소를 초래한다. 이 거동은 Fig. 3A에 나타난(식 (35)를 사용하여 추정된) 균체 프로파일과 일치하는 것으로 나타났다.

이전에 발표된 대부분의 페니실린 시뮬레이션(Paul and Thomas (1996), Tiller et al. (1994), Megee et al. (1970), Birol et al. (2002))은 주로 균체, 페니실린 및 기질의 모델링에 초점을 맞추었다. 여기서 제안된 시뮬레이션은 Fig. 3(C)와 (D)에 각각 나타난 질소(N)와 페닐아세트산(PAA)의 예측도 포함한다. 이 변수들의 예측은 배치 기록에 기록된 오프라인 측정값에 적절히 부합하는 것으로 나타났다. 그러나 식 (23)과 (25)에 정의된 이러한 핵심 영양분의 소비 속도는 페닐아세트산 공급물($F_{PAA}$) 내의 질소($c_{NPAA}$) 및 페닐아세트산 조성에 매우 민감한 것으로 나타났다. 10개 배치 모두에 대해 이러한 영양분의 정확한 예측을 얻기 위해, Table 2에 정의된 바와 같이 페닐아세트산 공급물의 입구 농도에 편차가 가정되었다. 이러한 원료 조성의 편차는 산업 발효에서 예상된다(Posch et al., 2012). 그러나 이러한 원료에 대한 측정값이 없었으므로 이러한 가정된 편차는 검증될 수 없었다. 이러한 핵심 영양분의 포함은 영양분이 오프라인 측정값을 사용하여 제어될 때 직면하는 현실적인 과제를 고려하는 제어기를 이 시뮬레이션에 대해 개발할 수 있게 한다. 이는 생명공학 분야의 핵심 과제로 강조되어 왔다(Alford, 2006).

시뮬레이션은 산소($O_{2out}$) 및 이산화탄소($CO_{2out}$)의 오프가스 농도의 포함을 통해 바이오공정 제어에서 소프트 센서(soft sensors) 응용에 대한 증가하는 관심을 고려한다(Luttmann et al., 2012). 시뮬레이션은 2.8절에서 논의된 바와 같이 용기로 들어가고 나가는 가스 유량의 효과를 고려함으로써 Birol et al. (2002)에서 개발된 $CO_{2out}$ 을 개선한다. 이러한 예측은 Fig. 3E에 나타난 $CO_{2out}$ 측정의 정확성으로 입증되듯이 배치 기록에 기록된 것과 잘 일치한다.

주로 유가식 공정으로 운전되었던 이전 발효 시뮬레이션과 달리, 여기서 제안된 시뮬레이션은 Fig. 3F에 강조된 바와 같이 반복 유가식 운전(repeated fed-batch operation)을 사용하여 운전되는 것으로 나타났다. 이러한 유형의 운전은 산업 페니실린 발효의 일반적인 운전 전략이다(Pirt, 1974). 이 전략은 생물반응기의 용량이 초과되지 않도록 하고 페니실린 생산 시간을 연장하기 위해 용기 중량에 기반하여 발효조에서 예정된 배출을 포함한다. Fig. 3F에 나타난 중량 프로파일은 식 (8)과 Table 2A에 정의된 공정 입력 및 출력의 밀도를 사용하여 계산되었다.

Fig. 4는 균체 및 페니실린의 비성장 속도(Table 3에서 가져옴)를 제외하고 공칭 매개변수 집합을 사용하여 Batch 1, 3, 8, 10의 모델 예측을 배치 기록에 기록된 것과 비교한다. 이 설비에 구현된 제어 전략은 주로 순차 배치 제어였다. 이 제어 전략은 사전 정의된 최적 프로파일에 기반하여 입력 유량을 표준화한다. 모든 배치에서 20시간에 관찰된 $F_s$ 의 급격한 증가는 기질 농도가 과잉 상태가 되도록 하고 각 배치 시작 시 균체가 "급속 성장(rapid-growth)" 단계에 머무르도록 보장한다. 이후 $F_s$ 의 감소는 배치를 생산 단계로 전환하는데, 여기서 기질 농도는 페니실린 생산을 최대화하기 위해 최소로 유지되며, 유사한 운전이 Montague et al. (1986)에 보고되었다. 페니실린 프로파일을 예측하는 시뮬레이션의 정확성은 $\mu_{Pmax}$ 를 모델 입력으로 사용함으로써 향상된다. 이 매개변수는 민감도 분석에서 페니실린 생산에 가장 큰 영향을 미치는 것으로 나타났다.

제안된 시뮬레이션의 한계는 용존 산소(DO2)와 점도($\mu_{app}$)를 정확하게 예측하는 능력이다. 이 두 변수에 영향을 미치는 주요 공정 입력은 Fig. 5에 강조되어 있다. 기록된 측정값과 비교한 DO2의 예측은 Fig. 5C에 나타나 있다. 이 그림은 예측이 합리적으로 정확함을 보여주지만, 특히 배치 시작 시 편차가 분명하다. 이 편차는 시뮬레이션된 점도와 산업 공정에서 오프라인으로 기록된 점도 사이의 큰 불일치에 기인할 수 있다. 기록된 점도를 시뮬레이션의 공정 입력으로 사용하면 DO2의 향상된 예측이 얻어진다. 그러나 점도가 이 설비에서 기록되지 않은 많은 수의 요인(2.5절에서 논의됨)과 관련되어 있으므로, 식 (28)에 주어진 제안된 점도 모델은 시뮬레이션의 목적에 충분하다. 이 점도 항은 고점도 발효 중 용존 산소 제어와 관련된 전형적인 과제를 시뮬레이션하는 데 사용될 수 있다.

여기서 논의된 결과 외에도, 시뮬레이션은 온도와 pH를 조절하기 위한 PID 제어기도 포함하였다. 결과적으로 온도와 pH의 예측은 부록 Fig. 3A에 나타난 바와 같이 배치 기록에 기록된 프로파일과 잘 일치하는 것으로 나타났다. 산업 규모 생물반응기의 큰 작동 부피(<100 m³)와 사상균 발효액의 매우 점성이 높은 특성으로 인해, 이러한 발효 내의 혼합 시간(mixing times)은 1분에서 수 분 범위로 보고되었다는 점에 유의해야 한다(De Jonge et al., 2011). 이는 pH, 온도 및 DO2의 불균일한 분포를 초래할 수 있다. 따라서 단일 센서를 사용하여 기록된 이러한 공정 측정값은 전체 생물반응기의 정확한 표현을 제공하지 못할 수 있으며, 이는 완전 혼합(perfectly mixed) 용기를 가정하는 모델에 오차를 도입했을 수 있다.

용존 이산화탄소(CO2,L)는 2.2절에서 논의된 바와 같이 균체에 대한 높은 CO2,L의 억제 효과를 고려하기 위해 시뮬레이션에 의해 예측되었다. 이 억제의 예는 Batch 5에 나타나 있다.

구조화 모델은 안정적이고 매우 민감하며 정확한 측정이 가능한 고도로 계측된 실험실 규모 생물반응기에서만 적용 가능하다는 주장이 종종 제기된다(Menezes and Alves, 1994). 이 시뮬레이션은 통상적이고 일반적으로 기록되는 측정값을 사용하여 복잡한 산업 공정을 기술하는 구조화 모델의 능력을 명확하게 입증한다.

---

## 5. 산업 규모 페니실린 시뮬레이션 – IndPenSim (Industrial scale penicillin simulation – IndPenSim)

IndPenSim이라고 명명된 이 시뮬레이션은 Matlab R2013b로 코딩되었으며 www.industrialpenicillinsimulation.com 에서 다운로드할 수 있고, 그곳에서 배치 기록도 이용 가능하다. IndPenSim은 또한 독립 실행형 애플리케이션으로 사용될 수 있으며 다음의 기능을 포함하여 산업 규모 페니실린 발효의 운전을 복제하는 것을 목표로 한다:

- $\mu_{Xmax}$ 와 $\mu_{Pmax}$ 의 배치 간 변동 및 배치 내 변동.
- 기질($c_s$), 오일($c_{oil}$), 산/염기 몰 농도($c_{a/b}$) 및 페닐아세트산 농도($c_{PAA}$)의 입구 농도에 대한 교란(disturbances)을 추가하는 옵션.
- $F_s$, $F_{oil}$, $F_g$, RPM, $F_{dis}$, $F_{PAA}$ 에 대한 현재의 순차 배치 제어 전략을 조정하는 능력.
- DO2, N 및 PAA 제한 동안, 그리고 과도한 PAA 및 CO2,L 농도와 최적이 아닌 T 및 pH 범위 동안 성장 속도에 대한 억제 효과를 포함하는 옵션.
- P, N, PAA 및 $\mu_{app}$ 의 오프라인 측정에 사전 정의된 지연(3시간)을 포함.
- 최적이 아닌 pH 및 온도 조건이 지속되는 기간 이후 균체 및 페니실린의 성장 속도가 정상으로 돌아오지 못하는 무능력을 포함하는 옵션.
- 교반기 정지(agitator trip), 통기 결함(aeration faults) 및 센서 오류(sensor errors)를 포함한 공정 결함을 포함하는 옵션.

이 시뮬레이션은 산업 발효 공정을 위한 견고한 제어 및 모니터링 전략 개발에 사용할 플랫폼을 제공하는 것을 목표로 한다.

---

## 6. 결론 (Conclusion)

도전적인 산업 규모 발효에 대한 제일원리 수학적 시뮬레이션의 성공적인 구현이 제시되었다. 이 시뮬레이션은 복잡한 공정 동역학을 포착하고 현대 생명공학 설비와 관련된 일부 전형적인 결함을 고려하는 것으로 나타났다. 시뮬레이션은 균체와 페니실린뿐만 아니라 산업 규모 발효 공정의 주요 공정 변수를 정확하게 모델링하는 시변(time varying) 구조화 동역학 모델을 통합하였다. 여기서 개발된 모델은 산업 발효를 위한 향상된 제어 전략 개발에 가치 있는 도구로 사용될 수 있으며, 모니터링, 제어 및 최적화 연구에서 연구 및 교육 활동에도 사용될 수 있다.

---

## 감사의 글 (Acknowledgements)

이 연구는 Perceptive Engineering Ltd의 재정적 지원과 지원으로 Newcastle University에서 SG의 바이오제약 공정 개발(Biopharmaceutical Process Development) 공학 박사(Engineering Doctorate)의 일환으로 EPSRC 보조금(EP/G037620/1)의 지원을 받았다.

## 부록 A. 보충 자료 (Appendix A. Supplementary data)

이 논문과 관련된 보충 자료는 온라인 버전에서 다음 주소에서 찾을 수 있다: http://dx.doi.org/10.1016/j.jbiotec.2014.10.029

---

## 표 (Tables)

### Table 1. 모델 매개변수 요약 (Summary of model parameters)

|매개변수|설명|단위|
|---|---|---|
|t|배치 시간|h|
|A0|성장 균체 농도|g L⁻¹|
|A1|비성장 균체 농도|g L⁻¹|
|A3|퇴화 균체 농도|g L⁻¹|
|A4|자가분해 균체 농도|g L⁻¹|
|X|총 균체 농도|g L⁻¹|
|P|페니실린 농도|g L⁻¹|
|s|기질 농도|g L⁻¹|
|V|용기 부피|L|
|Vm|용기 부피|m³|
|Fin|총 유입량|L h⁻¹|
|Fdis|배출 속도|L h⁻¹|
|Fs|당 유량|L h⁻¹|
|FPAA|페닐아세트산 유량|L h⁻¹|
|Foil|대두유 유량|L h⁻¹|
|Fw|주입용수 유량|L h⁻¹|
|Fa/b|산/염기 유량|L h⁻¹|
|Fevp|증발 유량|L h⁻¹|
|DO2|용존 산소 농도|mg L⁻¹|
|kLa|부피 물질 전달 계수|h⁻¹|
|μapp|겉보기 점도|cP|
|Fg|통기 속도|m³ min⁻¹|
|Pag|교반기 동력|kW|
|Pair|통기로 소산된 동력|kW|
|P1|용기 배압|Pa|
|ρb|발효액 밀도|kg m⁻³|
|P0|용기 바닥 압력|Pa|
|Z|비통기 액체 높이|m|
|Tb|발효액 온도|K|
|H⁺|수소 이온 농도|mol L⁻¹|
|Nshots|질소 샷|kg|
|PAA|페닐아세트산 농도|mg L⁻¹|
|N|질소 농도|mg L⁻¹|
|O2out|산소 오프가스 농도|%|
|CO2out|이산화탄소 오프가스 농도|%|
|CO2,L|용존 이산화탄소 농도|g L⁻¹|

### Table 2. 시뮬레이션 매개변수 요약 (Summary of simulation parameters)

|매개변수|값 (단위)|참고문헌|
|---|---|---|
|균체 기질 수율 계수 (Ys/X)|1.85 g g⁻¹|Paul et al. (1998)|
|페니실린 기질 수율 계수 (Ys/P)|0.9 g g⁻¹|Bajpai and Reul (1980)|
|기질 유지 항 (ms)|0.029 g g⁻¹ h⁻¹|Paul and Thomas (1996)|
|오일 공급 농도 (coil)|1000 g L⁻¹|산업 사례 연구에서 추정|
|당 공급 농도 (cs)|600 g L⁻¹|산업 사례 연구에서 추정|
|균체 산소 수율 계수 (YO2/X)|650 mg O2 (g X)⁻¹|Christensen et al. (1995)|
|페니실린 산소 수율 계수 (YO2/P)|160 mg O2 (g X)⁻¹|Bajpai and Reul (1980)|
|유지 산소 계수 (mO2)|17.5 mg O2 (g X)⁻¹|Christensen et al. (1995)에서 수정|
|kLa 상수 (αkLa)|85 ± 14|산업 사례 연구에서 추정|
|kLa 상수 (a, b, c, d)|0.38, 0.34, −0.38, 0.25|산업 사례 연구에서 추정|
|헨리의 법칙 상수 (HO2)|0.0251 bar L mg⁻¹|Green and Perry (2008)|
|임펠러 수 (n)|3|Shuler and Kargi (2002)|
|탱크 반경 (r)|2.1 m|Shuler and Kargi (2002)|
|임펠러 반경 (rimp)|0.85 m|Shuler and Kargi (2002)|
|통기/비통기 동력 비 (Pg/Pungassed)|0.4–0.6|산업 사례 연구에서 추정|
|동력 수 (Po)|5|Uhl and Gray (1966)|
|RPM (NRPM)|100|산업 사례 연구에서 추정|
|가스 홀드업 (ε)|0.1|산업 사례 연구에서 추정|
|중력 상수 (g)|9.81 m s⁻²|Green and Perry (2008)|
|보편 기체 상수 (R)|8.314 J K⁻¹ mol⁻¹|Green and Perry (2008)|
|페니실린 임계 용존 산소 수준 (DO2critP)|30%|Vardar and Lilly (1982)|
|균체 임계 용존 산소 수준 (DO2critX)|10%|Vardar and Lilly (1982)|
|억제 상수 (Ainhib)|1|산업 사례 연구에서 추정|
|기질 및 냉각수 온도 (Ts, Tw)|288K|산업 사례 연구에서 추정|
|온수 온도 (Th)|333K|산업 사례 연구에서 추정|
|공기 온도 (Tair)|290K|산업 사례 연구에서 추정|
|기질 비열 용량 (CPs)|5.8 kJ (kg K)⁻¹|Green and Perry (2008)|
|물 및 발효액 비열 용량 (CPw, CPb)|4.18 kJ (kg K)⁻¹|Green and Perry (2008)|
|증발열 (Hevp)|2430.7 kJ kg⁻¹|Green and Perry (2008)|
|용기 벽 열 전달 계수 (Ujacket)|36 kW m²|산업 사례 연구에서 추정|
|냉각 코일 면적 (Ac)|105 m²|Vogel and Todaro (1997)|
|세포 성장에 대한 아레니우스 상수 (kg)|450 J gX|Birol et al. (2002)에서 수정|
|세포 사멸에 대한 아레니우스 상수 (kd)|0.25 × 10³⁰ J gX|산업 사례 연구에서 추정|
|세포 성장 활성화 에너지 (Eg)|1.5 × 10⁴ J mol⁻¹|산업 사례 연구에서 추정|
|세포 사멸 활성화 에너지 (Ed)|1.75 × 10⁵ J mol⁻¹|산업 사례 연구에서 추정|
|열 수율 계수, 균체 및 페니실린 (YQ/X, YQ/X)|25 kJ g⁻¹|산업 사례 연구에서 추정|
|산/염기 입구 농도 (abc)|0.033 mol L⁻¹|산업 사례 연구에서 추정|
|수소 이온 생성 항 (γ1)|3.25 × 10⁻³|산업 사례 연구에서 추정|
|수소 이온 공정 입력 항 (γ2)|2.5 × 10⁻¹¹|산업 사례 연구에서 추정|
|수소 이온 유지 항 (mpH)|0.0025|산업 사례 연구에서 추정|
|수소 이온 억제 항 (K1/K2)|1 × 10⁻⁵ / 2.5 × 10⁻⁸ mol L⁻¹|산업 사례 연구에서 추정|
|오일 공급물 내 질소 농도 (cNoil)|20 g L⁻¹|산업 사례 연구에서 추정|
|PAA 공급물 내 질소 농도 (cNPAA)|80 ± 28 g L⁻¹|산업 사례 연구에서 추정|
|질소 샷 (cNshot)|400 g kg⁻¹|산업 사례 연구에서 추정|
|N, 페니실린 수율 계수 (YN/P)|80 mg g⁻¹|산업 사례 연구에서 추정|
|N, 균체 수율 계수 (YN/X)|10 mg g⁻¹|산업 사례 연구에서 추정|
|유지 N 항 (mN)|0.03 mg g⁻¹ hr⁻¹|산업 사례 연구에서 추정|
|균체에 대한 임계 N 농도 (NcritX)|150 mg L⁻¹|산업 사례 연구에서 추정|
|PAA 공급 용액 농도 (cPAA)|530 ± 35 g L⁻¹|산업 사례 연구에서 추정|
|PAA, 균체 수율 계수 (YPAA/X)|37.5 mg g⁻¹|산업 사례 연구에서 추정|
|PAA, 페니실린 수율 계수 (YPAA/P)|187.5 mg g⁻¹|산업 사례 연구에서 추정|
|유지 PAA 항 (mPAA)|1.2 mg g⁻¹ h⁻¹|산업 사례 연구에서 추정|
|균체에 대한 임계 PAA 농도 (PAAcritX)|2000 mg L⁻¹|산업 사례 연구에서 추정|
|페니실린에 대한 임계 PAA 농도 (PAAcritP)|200 mg L⁻¹|산업 사례 연구에서 추정|
|페니실린 가수분해 상수 (B1, B2)|−67.8, −1.82|Kheirolomoom et al. (1999)|
|페니실린 가수분해 상수 (B3, B4, B5)|0.36, 0.12, −4.9 × 10⁻⁴|Kheirolomoom et al. (1999)|
|부피 물질 전달 비 (δc/o)|0.89|Royce (1992)|
|사상 형태 분해 관련 상수 (kwater)|0.005|산업 사례 연구에서 추정|
|점도 계수 (kin, kde)|0.001, 0.0001|산업 사례 연구에서 추정|
|점도 계수 (tin, tde)|1, 250 h|산업 사례 연구에서 추정|
|CO2 수율 계수 (YCO2/X)|850 mg CO2 (g X)⁻¹|Christensen et al. (1995)|
|유지 이산화탄소 계수 (mCO2)|66 mg CO2 (g X)⁻¹ h⁻¹|Christensen et al. (1995)에서 수정|
|균체에 대한 임계 CO2 농도 (CO2,LcritX)|35 mg L⁻¹|산업 사례 연구에서 추정|

### Table 3. 본 연구에서 조사된 10회의 산업 규모 페니실린 발효 요약

배치 길이($t$), 균체의 최대 비성장 속도($\mu_{Xmax}$), 페니실린의 최대 비성장 속도($\mu_{Pmax}$)에 대한 평균 및 표준편차가 표시됨.

|실행 (Run)|용기|t (h)|μXmax (h⁻¹)|μPmax (h⁻¹)|관찰 사항|
|---|---|---|---|---|---|
|Batch 1|V-1|211|0.4136|0.0504|전형적 발효|
|Batch 2|V-3|286|0.4360|0.0479|거품 발생|
|Batch 3|V-1|317|0.4196|0.0444|전형적 발효|
|Batch 4|V-3|133|0.4282|0.0414|기질 펌프 고장|
|Batch 5|V-3|257|0.3234|0.0409|높은 CO2|
|Batch 6|V-3|241|0.4168|0.0480|살포기 파손 및 거품 발생|
|Batch 7|V-5|217|0.4529|0.0489|NH3 제한|
|Batch 8|V-4|218|0.4201|0.0439|전형적 발효|
|Batch 9|V-1|272|0.4106|0.0374|부실한 온도 제어|
|Batch 10|V-2|209|0.2773|0.0459|NH3 제한|
|**평균**||**236.1 ± 48**|**0.400 ± 0.0521**|**0.0449 ± 0.00389**||

### Table 4. 민감도 측도 δ^msqr 에 기반한 6개 모델 출력의 상위 10개 순위 매개변수

|순위|균체 (θ / δmsqr)|페니실린 (θ / δmsqr)|기질 (θ / δmsqr)|DO2 (θ / δmsqr)|온도 (θ / δmsqr)|CO2 오프가스 (θ / δmsqr)|
|---|---|---|---|---|---|---|
|1|cs / 0.41|μPmax / 0.83|μXmax / 25.21|HO2 / 0.15|Tcin / 0.34|YCO2/X / 0.66|
|2|Kd / 0.30|cs / 0.41|Ys/X / 14.42|O2,in / 0.15|β1 / 0.24|cs / 0.35|
|3|Ys/X / 0.29|Ys/X / 0.31|coil / 0.46|r / 0.14|YQ/X / 0.23|Kd / 0.32|
|4|β1 / 0.27|eb / 0.31|eb / 0.07|rimp / 0.07|μXmax / 0.22|Ys/X / 0.08|
|5|μpmax / 0.21|Kb / 0.22|cs / 0.07|d / 0.51|rimp / 0.16|β1 / 0.06|
|6|ms / 0.10|ms / 0.18|Kb / 0.009|a / 0.05|Kd / 0.084|μPmax / 0.55|
|7|coil / 0.09|smaxP / 0.15|ms / 0.009|αkLa / 0.02|Ys/X / 0.06|ms / 0.04|
|8|Ys/P / 0.05|coil / 0.14|Ke / 0.006|mO2X / 0.02|βT / 0.04|coil / 0.04|
|9|Ke / 0.02|μXmax / 0.13|Kd / 0.004|ρb / 0.02|eb / 0.01|Ys/P / 0.03|
|10|eb ≈ 0|Kv / 0.001|β1 ≈ 0|Kd / 0.01|coil / 0.001|Ke / 0.004|

---

## 그림 설명 (Figure captions)

**Fig. 1.** (A) 영양분의 흐름이 강조된 _Penicillium chrysogenum_ 진균의 네 개의 별개 영역을 나타내는 모식도. (B) 각 영역의 형성 메커니즘. Paul and Thomas (1996)에서 수정.

**Fig. 2.** 사용된 100,000 L 생물반응기의 모식도로, 모든 공정 입력과 출력 포함. 별표(asterisk)로 표시된 변수는 배치 기록에 기록되지 않은 변수를 나타낸다.

**Fig. 3.** Batch 3의 주요 공정 매개변수에 대한 시뮬레이션 예측. (A) 네 개의 균체 영역: 성장 영역(A0), 비성장 영역(A1), 퇴화 영역(A3), 자가분해 영역(A4), 총 균체 $X = A_0 + A_1 + A_3 + A_4$, 그리고 CER로부터 추정된 균체($X_{est}$). (B)~(F) 페니실린(P), 질소(N), 페닐아세트산(PAA), CO2 오프가스($CO_{2out}$), 중량(W)에 대한 모델 예측과 배치 기록의 비교. 그래프 B), C), D)에서는 페니실린, 질소, 페닐아세트산의 오프라인 측정값도 표시됨.

**Fig. 4.** 4개 배치에 대한 시뮬레이션의 예측 능력. (A) Batch 1, (B) Batch 3, (C) Batch 8, (D) Batch 10. 기질 공급($F_s$), 대두유 공급 속도($F_{oil}$), 오프라인 페니실린 측정값, 시뮬레이션된 페니실린(P) 및 기질 농도(s)의 결과 표시.

**Fig. 5.** 용존 산소(DO2)와 점도($\mu_{app}$)와 관련된 입력 변수(Batch 1). 통기 속도($F_g$), 용기 배압($P_1$), 주입용수($F_w$), 대두유 공급 속도($F_{oil}$). 용존 산소와 점도에 대해 모델 예측과 산업 데이터, 점도의 오프라인 측정값 표시.

---

## 참고문헌 (References)

- Albaek, M.O., Gernaey, K.V., Hansen, M.S., Stocks, S.M., 2012. Evaluation of the energy efficiency of enzyme fermentation by mechanistic modeling. _Biotechnol. Bioeng._ 109, 950–961.
- Alford, J.S., 2006. Bioprocess control: advances and challenges. _Comput. Chem. Eng._ 30, 1464–1475.
- Ashoori, A., Moshiri, B., Khaki-Sedigh, A., Bakhtiari, M.R., 2009. Optimal control of a nonlinear fed-batch fermentation process using model predictive approach. _J. Process Control_ 19, 1162–1173.
- Bajpai, R.K., Reul, M., 1980. A mechanistic model for penicillin production. _J. Chem. Technol. Biotechnol._ 30, 332–344.
- Birol, G., Ündey, C., Çinar, A., 2002. A modular simulation package for fed-batch fermentation: penicillin production. _Comput. Chem. Eng._ 26, 1553–1565.
- Chern, J.-M., Chou, S.-R., Shang, C.-S., 2001. Effects of impurities on oxygen transfer rates in diffused aeration systems. _Water Res._ 35, 3041–3048.
- Christensen, L.H., Henriksen, C., Nielsen, J., Villadsen, J., Egel-Mitani, M., 1995. Continuous cultivation of Penicillium chrysogenum. Growth on glucose and penicillin production. _J. Biotechnol._ 42, 95–107.
- De Jonge, Lodewijk, P., Buijs, N.A.A., ten Pierick, A., Deshmukh, A., Zhao, Z., Kiel, J.A.K.W., Heijnen, J.J., van Gulik, W.M., 2011. Scale-down of penicillin production in Penicillium chrysogenum. _Biotechnol. J._ 6, 944–958.
- Fernandez-canon, J.M., Reglero, A., Martinez-blanco, H., Luengo, J.M., 1989. Uptake of phenylacetic acid by Penicillium chrysogenum Wis54-1255: a critical regulatory point in benzylpenicillin biosynthesis. _J. Antibiot._ 42, 1398–1409.
- Finn, R.K., 1954. Agitation–aeration in the laboratory and in the industry. _Bact. Rev._ 18, 254–274.
- Frick, R., Junker, B., 1999. Indirect methods for characterization of carbon dioxide levels in fermentation broth. _J. Biosci. Bioeng._ 87, 344–351.
- Garcia-Ochoa, F., Gomez, E., 2009. Bioreactor scale-up and oxygen transfer rate in microbial processes: an overview. _Biotechnol. Adv._ 27, 153–176.
- Grabowski, H.G., Vernon, J.M., Thomas, L.G., 1978. Estimating the effects of regulation on innovation: an international comparative analysis of the pharmaceutical industry. _J. Law Econ._ 21, 133–163.
- Green, W.D., Perry, H.R., 2008. _Perry's Chemical Engineers Handbook._ The McGraw Hill.
- Hegewald, E., Wolleschensky, B., Guthke, R., Neubert, M., Knorre, W.A., 1981. Instabilities of product formation in a fed-batch culture of Penicillium chrysogenum. _Biotechnol. Bioeng._ 23, 1563–1572.
- Herschbach, G.J.M., Van der Beek, C.P., Van Dijck, P.W.M., 1984. _The Penicillins: Properties, Biosynthesis, and Fermentation._ Marcel Dekker AG.
- Hillenga, D.J., Versantvoort, H., Molen, S.V.D., Driessen, A., Konings, W.N., 1995. Penicillium chrysogenum takes up the penicillin G precursor phenylacetic acid by passive diffusion. _Appl. Environ. Microbiol._ 61, 2589–2595.
- Junker, B., 2007. Foam and its mitigation in fermentation systems. _Biotechnol. Prog._ 23, 767–784.
- Kawase, Y., Moo-Young, M., 1990. The effect of antifoam agents on mass transfer in bioreactors. _Bioprocess Eng._ 5, 169–173.
- Kheirolomoom, A., Kazemi-Vaysari, A., Ardjmand, M., Baradar-Khoshfetrat, A., 1999. The combined effects of pH and temperature on penicillin G decomposition and its stability modeling. _Process Biochem._ 35, 205–211.
- Lee, J.-M., Yoo, C.K., Lee, I.-B., 2004. Enhanced process monitoring of fed-batch penicillin cultivation using time-varying and multivariate statistical analysis. _J. Biotechnol._ 110, 119–136.
- Lin, J., Lee, S.-M., Lee, H.-J., Koo, Y.-M., 2000. Modeling of typical microbial cell growth in batch culture. _Biotechnol. Bioprocess Eng._ 5, 382–385.
- Lu, X., Xing, H., Su, B., Ren, Q., 2008. Effect of buffer solution and temperature on the stability of Penicillin G. _J. Chem. Eng. Data_ 53, 543–547.
- Luttmann, R., Bracewell, D.G., Cornelissen, G., Gernaey, K.V., Glassey, J., Hass, V.C., Kaiser, C., Preusse, C., Striedner, G., Mandenius, C.-F., 2012. Soft sensors in bioprocessing: a status report and recommendations. _Biotechnol. J._ 7, 1040–1048.
- McIntyre, M., Berry, D.R., McNeil, B., 1999. Response of Penicillium chrysogenum to oxygen starvation in glucose- and nitrogen-limited chemostat cultures. _Enzyme Microb. Technol._ 25, 447–454.
- Megee, R.D., Kinoshita, S., Fredrickson, a.G., Tsuchiya, H.M., 1970. Differentiation and product formation in molds. _Biotechnol. Bioeng._ 12, 771–801.
- Menezes, J.C., Alves, S.S., 1994. Mathematical modelling of industrial pilot-plant Penicillin-G fed-batch fermentations. _J. Chem. Technol. Biotechnol._ 61, 123–138.
- Metz, B., Kossen, N.W.F., 1977. The growth of molds in the form of pellets – a literature review. _Biotechnol. Bioeng._ XIX, 781–799.
- Montague, G.A., Morris, A.J., Wright, A.R., Aynsley, M., Ward, A., 1986. Modelling and adaptive control of fed-batch penicillin fermentation. _Can. J. Chem. Eng._ 64, 567–580.
- Nestaas, E., Wang, D.I.C., 1983. Computer control of the penicillin fermentation using the filtration probe in conjunction with a structured process model. _Biotechnol. Bioeng._ 25, 781–796.
- Nielsen, J., 1993. A simple morphologically structured model describing the growth of filamentous microorganisms. _Biotechnol. Bioeng._ 41, 715–727.
- Nielsen, J.H.i., Villadsen, J., Lidén, G., 2003. _Bioreaction Engineering Principles._ Kluwer Academic/Plenum Publishers.
- Olsvik, E., Kristiansen, B., 1994. Rheology of filamentous fermentations. _Biotechnol. Adv._ 12, 1–39.
- Patnaik, P.R., 2001. Penicillin fermentation: mechanisms and models for industrial-scale bioreactors. _Crit. Rev. Microbiol._ 27, 25–39.
- Paul, G., Syddall, M., Kent, C., Thomas, C., 1998. A structured model for penicillin production on mixed substrates. _Biochem. Eng. J._ 2, 11–21.
- Paul, G.C., Thomas, C.R., 1996. A structured model for hyphal differentiation and penicillin production using Penicillium chrysogenum. _Biotechnol. Bioeng._ 51, 558–572.
- Pirt, S., 1974. The theory of fed batch culture with reference to the penicillin fermentation. _J. Appl. Chem. Biotechnol._ 24, 415–424.
- Posch, A.E., Herwig, C., Spadiut, O., 2013. Science-based bioprocess design for filamentous fungi. _Trends Biotechnol._ 31, 37–44.
- Posch, A.E., Spadiut, O., Herwig, C., 2012. Switching industrial production processes from complex to defined media: method development and case study using the example of Penicillium chrysogenum. _Microb. Cell Fact._ 11, 88–102.
- Righelato, R.C., Trinci, a.P., Pirt, S.J., Peat, A., 1968. The influence of maintenance energy and growth rate on the metabolic activity, morphology and conidiation of Penicillium chrysogenum. _J. Gen. Microbiol._ 50, 399–412.
- Roels, J.A., Heijnen, J.J., 1980. Power dissipation and heat production in bubble columns: approach based on nonequilibrium thermodynamics. _Biotechnol. Bioeng._ 22, 2399–2404.
- Rolinson, N.G., 1952. Respiration of Penicillium chrysogenum in penicillin fermentations. _J. Gen. Microbiol._ 6, 336–343.
- Routledge, S.J., 2012. Beyond de-foaming: productivity the effects of antifoams on bioprocess productivity. _Comput. Struct. Biotechnol. J._ 3, 1–7.
- Royce, P.N., 1992. Effect of changes in the pH and carbon dioxide evolution rate on the measured respiratory quotient of fermentations. _Biotechnol. Bioeng._ 40, 1129–1138.
- Scragg, A.H., 1991. _Bioreactors in Biotechnology: A Practical Approach._ Ellis Horwood Limited.
- Seborg, D.E., Edgar, T.F., Mellichamp, D.A., 2004. _Process Dynamics & Control._ John Wiley & Sons.
- Shinskey, G.E., 1973. _pH and pION Control in Process and Waste Streams._ John Wiley & Sons.
- Shuler, M.L., Kargi, F., 2002. _Bioprocess Engineering: Basic concepts._ Prentice Hall PTR.
- Sin, G., Gernaey, K.V., Lantz, A.E., 2009. Good modeling practice for PAT applications: propagation of input uncertainty and sensitivity analysis. _Biotechnol. Prog._ 25, 1043–1053.
- Syndall, T.M., (Ph.D. thesis) 1998. _Improving the identification of a Penicillin fermentation model._ University of Birmingham.
- Tiller, V., Meyerhoff, J., Sziele, D., Schügerl, K., Bellgardt, K.H., 1994. Segregated mathematical model for the fed-batch cultivation of a high-producing strain of Penicillium chrysogenum. _J. Biotechnol._ 34, 119–131.
- Uhl, V.M., Gray, B.J., 1966. _Mixing – Theory and Practice._ Academic Press, New York.
- Ündey, C., Ertunç, S., Çinar, A., 2003. Online batch/fed-batch process performance monitoring, quality prediction, and variable-contribution analysis for diagnosis. _Ind. Eng. Chem. Res._ 42, 4645–4658.
- Vardar, F., Lilly, M.D., 1982. Effect of cycling dissolved oxygen concentrations on product formation in penicillin fermentations. _Eur. J. Appl. Microbiol. Biotechnol._ 14, 203–211.
- Vogel, H., Todaro, C., 1997. _Fermentation and Biochemical Engineering Handbook._ Noyes.
- Yu, X.L., 2008. Pharmaceutical quality by design: product and process development, understanding, and control. _Pharm. Res._ 25, 781–791.
- Zhang, H., Lennox, B., 2004. Integrated condition monitoring and control of fed-batch fermentation processes. _J. Process Control_ 14, 41–50.

---

_DOI: http://dx.doi.org/10.1016/j.jbiotec.2014.10.029_ _0168-1656/Crown Copyright © 2014 Published by Elsevier B.V. All rights reserved._



