---

layout: post

title: "소프트웨어검증 (Software Verification)"

categories:

  - Notes

commit: true

---


* 기말고사 부분부터 필기!

# III. Problems and Methods

## Chapter 9. Test Case Selection and Adequacy
	• Effectiveness of testing; 테스트의 효율성을 주로 중점으로 둠
	• Test adequacy undecidability 때문에!
	
	• Functional Testing
		○ 코드를 보는 것이 아니라 requirement같은 specification 등의 "기능"을 봄
		○ 필수적. 자동화가 되지 않음
		○ 100% 통과해야 함
	• Structural Testing
		○ 코드 자체의 "구조"를 봄
		○ Optional. 자동화 됨. Test case 자동으로 만들어줄 수 있음
		○ 도구 기능을 functional testing이랑 연동해서 많이 사용

	둘다 functionality를 판단하는 테스트이지만 그 resource가 뭐냐에 따라 갈리는 것

	• 용어
		○ Test case: input과 expected output의 조합 (조건을 포함하기도 함)
		○ Test case specification: test case를 만들 때 들어가는 정보. 이걸 보고 test case를 만듦
		○ Test obligation: ex. 10개의 test case의 공통적인 특징 (제약 조건? 조건?)
		○ Test suite: 특정 test obligation에 따라서 모인 test case의 set (동일한 것을 본다)
		○ Test (Test execution): 입력 넣고 출력 나오는지 확인 (그 후 pass/fail 넣는 건 test oracle?)
		○ Adequacy criterion
			§ <program, test suite> 하나라도 실패하면 false, 다 통과하면 true 나오는 수식왠만하면 false가 난다.
			§ test obligation(restrict)는 test suite 중 최소 하나의 test case에서는 만족되어야한다
			§ ex) statement coverage adequacy criteria
				□ Test case를 돌리면서 라인을 체크 - case 다 돌린 후 체크된 라인 수와 체크 안 된 수 비교100개 중 90개는 체크되었는데 10개는 안 됐음 -> 90%
			§ ex) dicision coverage adequacy criteria
				□ 소스를 CFG로 만들 때 if문 등으로 생기는 branch - true/false 모든 가지를 지나가는가

	• Satisfiability
		○ 우리는 보통 defensive programming 스타일 (문제가 생길 경우 어떻게 해라.. 등 코드를 만들어 둠)safety를 위해서. -> 이런 경우 statement coverage를 100% 달성할 수가 없음(문제가 생기지 않는 이상 테스트가 불가능)
		○ Adequacy criterion의 Unsatisfiability !!!! = 보장 못함!
		○ 그럼 계산은???
			§ A방법) Defensive를 위한 코드를 아예 계산에서 빼버리겠다.
			§ B방법) True 말고 percentage로 이야기하겠다.         Adequacy criterion 대신 coverage를 측정! => 이것이 우리가 알고 있는 coverage 개념!-> 보통 B방법을 씀!

*Branch에서 or문이 있으면 앞에 꺼만 확인하면 뒤에 꺼 안봐도 됨 -> test case에서 제외할 수 있음

	• Coverage
		○ Coverage는 별다른 노력 없이 올리는 것이 쉬움
		○ 절대적인 것은 아니다.
		○ 보통 structural coverage를 얘기함
		○ 
			§ 밑에꺼가 약한거(?)
			§ Subsume관계	
			§ 밑에꺼가 70%면 그 위에꺼는 70%이 나올 수 없다..???? 밑에꺼 퍼센티지 > 위에꺼 퍼센티지
			§ 이론적 - 거의 불가능
			§ 실용적 - 우리가 사용할 수 있는 최대치 MC/DC testing

	• Adequacy Criteria의 사용
		○ 1 test case 만들 때
		○ 2 사용하고 평가할 때
		○ => 보통 도구가 두가지 다 해준다. (code scroll이 이거 해준다..?)
			§ Test의 cardinality: 싼 도구는 test case 3천개 만들어 줌….비싼 도구는 30개 만들어 줌...


## Chapter 10. Functional Testing
	• Functional Testing
		○ Functional requirement coverage는 무조건 100퍼센트 여야 해!!
		○ Spec에 쓰여져 있는 "기능"보고 테스트"이렇게 들어가면 이렇게 output이 나와야 하는 구나."
		○ 코드를 보지 않기 때문에 black-box testing! (코드만 보면 white box, 기능과 코드 둘다 보면 gray box)spec에 잘 안 써주면 gray box testing을 해야 하는 거임...ㅎ
		○ Functional specification
			§ Formal
			§ Semiformal : UML(다이어그램 등등) 등을 보고 specification을..
			§ Informal

	• Random (uniform) testing
		○ ex) 들어가야 할 input의 범위(input space)가 있고 100개의 test case를 만들어야 한다고 할 때범위를 100칸으로 나눠서(균등하게!) 그 한 칸마다 random하게 input을 뽑음
		○ Random하게 뽑기 때문에 에러를 찾기가 어려움ex) divided by zero
	• Systematic (non-uniform) testing -> 우리가 할 것
		○ 범위에 value를 줘서(partition-based) 알아서 input을 뽑는다
		○ "category"를 가지고 partition을 나눈다!
		○ 기본적으로 CPT를 한다(?)

	• 특징
		○ 코드 구현이 되지 않아도 design된 것만 보고 test case를 만들 수 있다(timely)
		○ 여러 단계에서 활용 가능(effective? Widely applicable)
		○ Structural testing으로는 찾아낼 수 없는 것들을 찾아낼 수 있음(effective)(ex. 만들었다고 생각했는데 안 만든 부분이 있었다!)
도구 필요x 사람이 하면 됨~^^ (economical)

	- Functional spec을 본다 -> 독립적으로 테스트할 수 있는 피쳐(카테고리)를 찾는다 -> 카테고리 별로 대표값들을 찾아 -> 조합을 해서 test case specification(test case를 만들기 위한 requirement이고 이게 test case일 수도 아닐 수도 있다?)을 만들어 (combinational selection) (이게 제일 표준이야) -> test data 만들어서 테스팅~!
	- 카테고리 찾는다 -> 대표값을 찾는게 아니라 이게 잘 드러나는 모델을 찾는다 -> 여기서 test case 뽑아낸다


## Chapter 11. Combinational Testing
		○ Category-partition testing(CPT)
			§ Baseline testing 기법. 제일 기본 -> adaption해서 조절..해야 함
			§ Test 개수 엄청 많이 나와서 도구를 사용해 줄여야 한다
			§ Corner cases 코너 케이스들을 잘 포함하도록 category 나눠야 함
			1. 독립적으로 테스트해야하는 피쳐 - 기본적인 특징들을 찾음(category) = 수동
			2. category 당 value의 클래스 구분 = 수동(ex. Normal values / boundary values / special values / error values)- boundary value를 주의해서 testing!- erroneous condition도 여러 가지로 반영해서 testing
			3. test case를 위한 combinations을 생성 = 도구가 자동으로 할 수도 있음 (ex. TSL)
			§ Category = (ex. 전화를 하고 있을 때, 예약문자를 보낼 때, 통화 대기가 걸렸을 때 등)Test case = (ex. 위의 상황이 모두 합쳐져서 동시에 일어날 때)
			§ Parameter 3개 / Category 10개
			§ 
			§ 카테고리 개수를 모두 곱한 것이 test case 개수!
			§ Error Constraints = error가 나는 조건이 있으면 그 뒤에 굳이 test할 필요 X
			§ Property Constraints = flag 설정하듯이 제약 조건 설정. [property]를 만족하는 test case만 만든다
			§ Single Constraints = [single] property. 한 번만 testing하면 되는 것                           (따로 곱할 필요 없고 다른 거랑 조합만 하면 된다)=> 여기까지 다 하는게 CPT다!
			§ Test case(또는 spec)를 만든거지 test data를 만든 건 아니야

		○ Pairwise testing
			§ 2-way or 3-way
			§ 도구에 따라서 2개 or 3개씩 묶어서 줄여줌-> 도구가 알아서 해주니까 어떻게 묶는지 알려고 하지 마라,,
			§ 정당한지에 대한 validation 없음
			§ 잘 안 쓰긴 하는데 case가 너무 많이 나오면 어쩔 수 없이 씀
			§ http://www.pairwise.org/tools.asp
			
		○ Catalog-based testing
			§ Catalog 기준으로 category를 만든다? 잘 안 씀
			§ 어떤 업계에서는 이런 category와 n-way pairwise를 쓰더라 하는 catalog


## Chapter 12 Structural Testing
	• Structural Test
		○ Functionality를 보는 test라는 것은 동일 - 코드의 structure를 보고 case를 (input을) 만든다!
		○ 입력이 path, statement를 지나가는 test
		○ 소스코드 -> CFG, DFG -> structural testing 진행elements를 얼마나 지나가는 지를 본다
		
		○ Coverage가 100%가 안 될 수가 있다 (defensive code = safe)
		○ Structural test를 마쳤다고 error가 없다고 보장할 수 없다.
			§ Optimistic inaccuracy 때문 (완벽한 test case를 만드는 것은 이론적으로도 불가능)아무리 테스팅을 많이 해도 error를 완전히 다 찾을 수 없음
			§ Test case를 만드는 여러 가지 다양한 기법을 사용해 error를 최대한 찾도록 한다
			§ Functional Test에 비해서 실제로 구현이 안된 부분 등에서 error를 찾을 수 없다.
			
		○ 뭐를 잘 찾냐?>
			§ Functional Test는 지나가지 않는 코드가 많을 수 있음(주로 positive한 case)ex) A를 넣으면 B가 나와야 한다Structural Test는 모든 코드를 지나가도록 test (optimistic 유의) (negative한 case)ex) A가 아닌 값을 나오면 뭐가 나오나?

	• In practice
		○ Functional Test 후 추가적인 부분을 structural test 진행 (Functional이 메인!)
		○ 기본적으로 자동화가 됨(c의 경우) -> 근데 썩 좋진 않음 -> 그래서 잘 안써..
			§ Level이 높은 product는 모두 다 함 ex) Adapted lamp?(A레벨)
			§ Level이 낮은 product는 많이 생략함


		○ 이 그림은 도구가 그린다!^^ CFG로 바꿔~~~ 
		○ statements(base block) 11개 / branch 8개 (true, false 따로 카운트)(maximum excute block?)
	
	• Techniques
		○ Statement Testing = Coverage : 가장 약한 것
			§ Adequacy criterion (만족하면 true, 만족하지 않으면 false)가 기본이지만 모두 만족하는 것이 힘들어서Statement Coverage Adequacy Criteria를 사용
			§ CFG로 바꾼 상태에서 Test Suite
			§ ex) 100개 statement 중 80개는 최소 한 번씩 지나가졌는데 20개는 한 번도 안 지나갔다 = 80%
			§ Test의 size는 크게 관련이 없다. (한번에 긴 것보다 짜잘한게 많으면 디버깅할 때 편한 정도)

		○ Branch Testing = Dicision Coverage
			§ Statement coverage가 100%이어도 dicison coverage는 100%가 안 될 수도 있다 
			§ Branch coverage를 만족하면 statement coverage 만족
			§ 조건 내용을 보지는 않음 (true/false)
		○ Condition Testing = Condition Coverage
			§ If i == 0 || i != 0 일 때true false가 각각 다 나오면 4개하나는 true 밖에 안 나오고 나머지 하나는 true false 다 나오면 3개
			§ 각각의 Base condition들이 true와 false 하나씩 다 나와야 한다
			§ Number of truth values taken by all basic conditions / 2*number of basic condition(=> true/false)
			§ Dicision의 true/false 조합과는 다름 (Base condition에서 true/false가 다 나오는 지만 보기 때문에)조건 안에 base condition이 하나씩 밖에 없다면 dicison = condition
				□ Branch and condition coverage: 둘이 합쳐버림 (붙여놓은 것)
				□ Compound(or All) conditions coverage: 둘이 묶어놓은 것……? (제일 강력한 것이다)                                                    이론적으로만 있고 impractice
				□ MCDC(Modified Condition/Decision=MC/DC)
					® branch and condition coverage를 compound 와 비슷하게(가깝게) 만든 것
					® Important combinations of conditions 이용(value가 바뀌었을 때 result가 바뀌는 value가 하나라도 있는 combination만 모아둠)
					® Structural test에서 우리가 할 수 있는 것 중 최고봉이다..
					® 굳이 손으로 만들 필요 없다
		○ Path Testing = Path Coverage : 안 쓴다 (loop를 다 도는 것을 확인해봐야한다)
			§ 이론만 가능 실제로 불가능
			§ Excuted paths / pathts
			§ Cyclomatic complexity number (sonarqube에서 계산해 준다!)
				□ 5 미만이면 프로그램의 complexity가 낮다
				□ 8 이상이면 높다 => 짤라라ㅎ
				□ E - n + 2 (CFG 상에서 계산)
			§ Procedure Call Testing
				□ Inter-procedure (프로시저 사이의 call) = call graph를 봄
	
	• 
		○ 우리가 사용하는 Structural Testing
		○ MC/DC가 최고봉이다 ㅇㅅㅇ
		○ 보통 다 100%가 나올 수 없다 -> defensive code 때문에=> 목표를 100%보다 적게 잡음=> critical system에서는 이유를 다 적어줘야 함 ㄷㄷ


## Chapter 13. Data Flow Testing
	• Motivation
		○ DFG 사용
		○ CFG는 element가 중요하든지 안 중요하든지 다 지나가야 함=> 시간 너무 오래 걸리니까 중요한 것만 지나가자 (data 정의, 사용, 재정의 등의 important path만 확인해)
		○ 근데 잘 안 돼..ㅎㅎ 잘 하는 도구를 사용하면 꽤 좋아….

	• Def-Use Pairs
		○ 소스코드를 CFG로 바꾼 후 적절한 DFG로 바꿔 준다
		○ DU pair: x를 1번에서 정의, 4번에서 재정의, 6번에서 사용 => (1,6) (4,6)
		○ DU path
			§ DU pair가 되려면 DU path가 있어야 함
			§ Definition-clear path(중간에 kick이 안 되는 path)가 하나라도 있어야 한다
				□ 1,2,3,5,6은 중간에 kick 안됨 => (1,6)은 DU pair가 될 수 있다
				□ 1,2,4,5,6은 중간에 4에서 kick
				□ 4,5,6은 중간에 kick 없음 => (4,6)은 DU pair 될 수 있다
				
	• Adequacy Criteria
		○ All DU pairs: 모든 DU pair는 최소 하나의 test case를 지나야 한다
		○ All DU paths: 모든 simple DU path(non-loop)는 최소 하나의 test case를 지나야 한다
		○ All definitions: 모든 definition은 적어도 한번의 test case가 지나가야 한다
		
	• Data Flow Coverage in Practice
		○ 되게… 어렵다… 거의 안 돼.. Difficult Cases (i와 j가 계산하면서 계속 바뀌어서 넘 찾기 어려워)
		○ 복잡한 구조를 가지고 있다면 사용 못해
		○ 그래서 DFG based 거의 안 써..


## Chapter 14. Model-Based Testing
(이건 Functional Testing이야)
	• MBT
		○ Specification을 보고 그냥 바로 뽑아내는 것은 MBT가 아님!
		○ Indefendently testable feature(category)를 뽑아야 함Category를 찾은 다음에 그게 잘 드러나는 Model을 만든다…특정 adequacy criterion 어쩌고 적용해서 만드는거 => 수단과 방법을 가리지 않고 만든다^^ (informal or semi-formal 거의 semi) 이 기법의 핵심..?ㄷ

	• Finite State Machine
		○ Informal spec을 보고 finite state machine 그림을 만들어 냄state 기반으로 움직이는 시스템이어야 함
		○ Transition Coverage Criteria
			§ All State coverage: 모든 state는 적어도 하나의 test case를 거쳐야 함
			§ All Transition coverage: 각 transition를 적어도 하나의 test case가 지나가야 함

	• Test Case
		○ Decision table -> basic condition coverage, compound… , MC/DC
		○ Informal Specification -> CFG, DFG -> Test Case
		○ => 이렇게 뽑은 Test case로 소스코드를 실행시켜서 테스트 한다~!


## Chapter 15. Testing Object-Oriented Software
	• 이러인어린얼이리런 어려움이 있어서 안된다.
	• Object들이 자꾸 바뀌기 때문에….


## Chapter 16.  Fault-Based Testing
	• FBT
		○ Hardware system testing에서 주로 사용
		
		○ Mutation Testing
			§ Error를 찾는 testing이 아니라 Test Suite의 Quality가 얼마나 좋은가를 평가하는 testing
			§ Original program에 error를 심는다! (x랑 y를 바꾼다던지… 간단한 수정)이걸 찾는 지 아닌지 확인!100개 중 99개는 찾았는데 1개는 못 찾았다 -> 실제로 99%의 정확성이 있구나~
			§ 가정
				□ 간단한 fault도 찾았기 때문에 조금 더 복잡한 fault도 찾을 것이다
				□ 실제 fault가 거의 correct한 프로그램의 아주 작은 variation일 것이다.
			§ Mutant operators: 도구를 써야 함

		○ Fault-Based Adequacy Criteria
			§ 3 steps
				1. 도구를 선택해요
				2. 프로그램 하나 당 error 하나 심어요
				3. Distinguish mutants: 심은 error를 구분
	
		○ Variations
			§ Problem: 많은 mutant가 있으면 각각 test case를 돌리는 게 비싸다(시간적으로)
			§ => weak mutation / statistical mutation(추정해서 하는 거)
	
	
## Chapter 17. Test Execution
	• Execution
		○ Test case는 훨씬 전에 만들고 마지막에 실행한다
		○ 지금까지 한 이전 단계는 모두 전에 만드는 거… 실행만 마지막
		○ Automation이 안 됨~!

	• From Test case Specifications to Test Cases
		○ TSL에서 나오는 건 test case specifications
		○ Test data를 넣은게 Test case-> 이거 자동으로 해주는 DDsteps이 있는데 안 씀 ㅇㅅㅇ

	• Scaffolding (테스트 끝나면 없애는 거)
		○ Test harnesses (테스트 환경과 관련된….커다란 것…...emulator….)
		○ Drivers (메인 함수)
		○ Stubs (아직 구현 안 된거 emulation)
		○ Ex) 테스팅할 때 printf 쓰는거 - 이게 scaffolding이다~!끝나고 지워줘야 된다~!

	• Controllability & Observability
		○ 누르고 send하는 거랑 똑같은 bypass하는 driver를 하나 만들어…API를 통해서..
		○ GUI 작동 내용을 text로 log로 저장해..
		○ 블루스크린이…..log file을 끄집어 내는 거다….

	• Test Oracles
		○ Expected output이랑 real output을 비교해서 true/false를 계산하는 프로시저
		○ 엄청나게 어려워요……..
		
		○ Comparison-based Oracle
			§ 일반적으로 전부 수작업...System일 때는 자동으로 안 돼요….Unit testing일 때는 돼요….
			
		○ Self-Checks as Oracle
			§ 만족해야 하는 특정 룰이 정해져 있다


## Chapter 18. Inspection
	• 사람이 보는 거 = Review
	• 모든 target 다 가능 (소스코드, 모델 등)
	• Brainstorm… 체계적으로 본다…… 핵심 point는 미리...check list


이걸 다 써서 효과적으로 적재적소에 써서 퀄리티를 높이는게 퀄리티 엔지니어의 임무다~~!~!~!~!!



<br><br>