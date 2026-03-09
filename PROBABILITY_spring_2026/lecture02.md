2026-03-09 08:20
## 2강
### Learning Goals
확률에 대한 내용이 더 깊게 나옴
- 표본공간(sample space), 사건(event), 확률함수(probability function)의 정의를 안다.    
- 무작위성이 있는 상황을 실험(experiment)과 표본공간(sample space)으로 정리할 수 있다.    
- 확률함수를 사용하여 기본적인 계산을 할 수 있다.

### Probability Cast List
- Experiment(실험): 반복가능한 과정
- Sample space(샘플스페이스): 모든 가능성의 집합
- Event(이벤트): 샘플스페이스의 부분집합
	- 아웃컴과 미묘하게 다름
	- 아웃컴은 원소, 이벤트는 샘플스페이스의 부분집합
- Probability function(확률함수): 각각 아웃컴의 확률을 정의 해주는 함수
- Definition (Probability density)  
	- 확률밀도: 확률이 연속적으로 분포되어 있는 것
- Definition (Random variable)  
	- 확률변수: 무작위로 정해지는 수치적 결과

### Simple Examples
#### Toss a fair coin
- Experiment: 동전던지기
- Sample space: Ω = {H, T} (앞, 뒤 2가지)
- Probability function: P(H) = 0.5, P(T ) = 0.5

#### Fair coin 3번 던지기
- Experiment: 동전을 3회 던져서 그 결과를 기록
- Sample space: Ω = {HHH, HHT , HTH, HTT , THH, THT , TTH, TTT }
- Probability function: 각 결과는 모두 똑같이 일어날 가능성을 가지며, 그 확률은 1/8 이다.
	- 샘플스페이스가 작은 경우 probability table을 작성 할 수 있다.


#### 양성자의 질량을 재는 실험. 
- Experiment: 정해진 절차를 따라 질량을 측정하고 그 결과를 보고한다.
- Sample space: Ω = [0, ∞) 모든 양수
- Probability function: 가능한 결과가 연속체(continuum) 를 이루기 때문에 확률함수는 없다.  
	- 대신 확률밀도(probability density) 를 사용해야 하며, 이것은 강의의 뒷부분에서 배우게 된다.
- 특이 사항
	- 양성자가 양수라면 [0,무한대) 로 작성할 수 있음
	- 무한대면 각각의 아웃컴은 0이 되게 됨.
	- 이럴때는 프로바빌리티 펑션이 아니고 프로바빌리티 덴시티를 써야 함.
		- 연속구간에서는 신경써서 처리 해야 함.


#### 택시가 지나간 것을 카운팅
- 이런 문제는 푸아송 디스트리부션을 사용한다는 것을 알고 넘어 가면됨
- 람다 이런 식으로 확률 함수를 할당 할 수 있음
- 람다를 어떻게 하냐에 따라 확률을 조절 할 수 있음.

확률은 다 더하면 1이 나와야 함.
- 당연히 푸아송 디스트리부션도 합치면 1이 나와야 함.
- 이건 테일러 시리즈(Taylor series)를 이용하면 확인 할 수 있음.

#### 2dice_choice samlpe space
샘플스페이스를 1가지로 한정 할 필요는 없음
- 첫번째 주사위 값, 두번째 주사위 값을 (1,2) 이런식으로 세트로 적을수 있음
	- {(1, 1), (2, 1), (3, 1), . . . (6, 6)}
- 또는 두 주사위의 합을 적을 수도 있음
	- {2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}
	- 다만 이렇게 되면 모두가 같은 확률로 나오지는 않음
- 표본공간을 어떻게 정하는 것이 가장 좋은지는 상황에 따라 달라진다는 것을 보게 될 것이다.  
- 지금은 결과를 두 수의 순서쌍(pair of numbers)으로 나타내면, 합을 쉽게 구할 수 있다는 점만 알아두자.
	- 참고(Note): 실험(experiment), 표본공간(sample space), 확률함수(probability function)를 정리해서 적어 보는 것은 확률을 체계적으로 다루기 시작하는 좋은 방법이다.  이 방법은 이 주제에서 자주 생기는 몇 가지 흔한 실수를 피하는 데 도움이 될 수 있다.



### Event
- 아웃컴들의 집함.
- 또는 샘플 스페이스Ω의 부분 집합
- 이벤트의 확률은 아웃컴들의 확률의 합으로 구할 수 있음
#### Example
- 동전을 3회 던졌을때 압면이 2번 나올 이벤트
- E = ’exactly 2 heads’. ={HHT , HTH, THH}
- 각각의 outcome의 확률은 1/8이고, P(E)=3/8로 쓸 수 있다.

### Discrete sample space(이산 샘플 스페이스)
- 원소들을 하나씩 나열할 수 있는 표본공간
- 유한 할 수도 무한 할 수 도 있음
- ditcrete sample space는 구간으로 된 샘플스페이스(continuous sample space)와 성격이 다름.


### Probability function
#### 정의
이산 sample space S 에 대하여, 확률함수 P는 각 결과(outcome) ω 에 하나의 수 P(ω)를 대응시키며, 이 P(ω)를 ω 의 확률이라고 부른다.
#### Rules
결과 w가 나오는 확률 함수를 정하면 p(w)이고 2개의 규칙을 만족해야 함.
- 0<p(w)<1, 확률함수는 0~1사이
- 모든 P(w)의 합은 1
	-  if S = {ω1, ω2, . . . , ωn} then P (ω1) + P (ω2) + . . . + P (ωn) = 1.
	-  notation:  
   		$\displaystyle\sum_{j=1}^{n} P (ω_j ) = 1$
#### Event 확률
이벤트의 확률은 각각의 outcome의 합으로 구한다.  
	$P(E)=\displaystyle\sum_{\omega\in E} P (ω)$

### Example
첫번째로 앞면이 나오게 되는 동전의 던진 횟수
- Experiment: 동전의 앞면이 나올 때 까지 동전을 던지고 몇번 던졌는지를 기록
- Sample space: Ω = {1, 2, 3, . . .}
- Probability function: $P(n) = (1 − p)^{n−1}p$
- challenge
    - P(n) 확률식을 증명
		- n번째 동전이 앞면이 되려면 n-1번째 까지는 모두 뒷면이 나와야함.
		- 뒷면이 나올 확률은 1-p이고 n-1 번째 까지 반복되어야 하기 때문에 그 확률은 $(1 − p)^{n−1}$
		- 마지막으로 n번째 앞면이 나올 확률은 p 
		- 따라서 $P(n) = (1 − p)^{n−1}p$
    
	- 확률의 합이 1임을 확인
  		- 등비수열을 계산 하면 확률 함수 공식이 나옴.

$$
\begin{aligned}
S &= \sum_{n=1}^{\infty} P(n) \\
  &= p + (1-p)p + (1-p)^2p + (1-p)^3p + \cdots \\
(1-p)S &= (1-p)p + (1-p)^2p + (1-p)^3p + \cdots \\
S - (1-p)S &= p \\
pS &= p \\
S &= 1
\end{aligned}
$$
	

### Rules of Probability
For events A, L and R contained in a sample space Ω.
- $P (A^c ) = 1 − P(A)$
- If L and R are disjoint then $P(L ∪ R) = P(L) + P(R)$
	- disjoint: $P(L \cap R)=\emptyset$
- If L and R are not disjoint, we have the inclusion-exclusion 
	- $P(L ∪ R) = P(L) + P(R) − P(L ∩ R)$



### Example1
1부터 20 사이의 정수 하나를 무작위로 만들어 내는 실험이 있다고 가정하자.  
(이때 각 결과의 확률은 반드시 균등할 필요는 없다. 즉, 각 결과가 모두 같은 확률을 가질 필요는 없다.)
→ 1~20사이 랜덤하게 정수 1개가 나옴. 
- 짝수가 나올 확률이 0.6이면 홀수가 나올 확률은 0.4
#### Formal 하게 풀이
- 먼저, 나중에 이것을 가리켜 말할 수 있도록 무작위 정수를 **X** 라고 이름 붙이자.  
- 또한 **‘X가 짝수이다’** 라는 사건을 **A** 라고 하자.  
- 그러면 **‘X가 홀수이다’** 라는 사건은 **$A^c$** 이다.  
- 문제에서 **P(A)=0.6** 이라고 주어졌다.  
- 따라서
	$P(A^c)=1-0.6=0.4$


### Example2
Consider the 2 events:  
▶ A : ’X is a multiple of 2’.  
▶ B : ’X is odd and less than 10’.  
Suppose P(A) = 0.6 and P(B) = 0.25. 
- What is A ∩ B ?
	- 어떤 수가 동시에 짝수이면서 홀수일 수는 없으므로
	- $A \cap B = \emptyset$
	- 즉, 교집합이 공집합이므로 disjoint
- What is the probability of A ∪ B ?
	- $A \cap B = \emptyset$ 이기 때문에 $P(A ∪ B) = P(A) + P(B) = 0.85$ 



### Example3
A,B,C를 각각 X가 2의 배수인 사건, 3의 배수인 사건, 6의 배수인 사건이라고 하자.
If P(A) = 0.6, P(B) = 0.3 and P(C ) = 0.2 what is P(A or B)?
- A or B = A ∪ B
- A ∩ B = 6의 배수인 사건
- P(A ∪ B) = P(A) + P(B) − P(A ∩ B) = 0.6 + 0.3 − 0.2 = 0.7
