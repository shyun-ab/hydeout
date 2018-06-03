---
layout: post
title: "Software Verification - Jackpot ATM"
categories:
  - Projects
commit: true
excerpt_separator:  <!--more-->
---

- 개요: 소프트웨어 검증 수업에서 진행한 팀 프로젝트
- 목적: CTIP 환경 구축 및 정적 분석, 시스템 테스팅
- 진행 기간: 2018.03.12 ~ 2018.06.11 (3개월)
<br><br>

- - -

<br>
###CTIP 환경
- 사용 언어 : **Java** (jdk 9)
- 개발 도구 : **Eclipse Oxygen**
- 유닛 테스트 : **JUnit 4**
- CI 서버 : **Jenkins**
- 빌드 : **Gradle**
- 형상 관리 : **Github**
- 요구사항 관리 : **ReqView**, **Trello**
- 이슈/프로젝트 관리 : **Redmine**
- 시스템 테스트 : **TestLink**
- 정적 분석 : **Code Inspector**, **SonarQube**, **FindBugs**, **Pmd**
- Cloud Server : **AWS EC2**, Azure, **Naver Cloud Platform**
<br><br>
Jenkins<br>
![Jenkins](https://github.com/shyun-ab/shyun-ab.github.io/blob/master/_screenshots/Jenkins.JPG?raw=true)
Trello<br>
![Trello](https://github.com/shyun-ab/shyun-ab.github.io/blob/master/_screenshots/Trello.JPG?raw=true)
Redmine<br>
![Redmine](https://github.com/shyun-ab/shyun-ab.github.io/blob/master/_screenshots/Redmine-issue.JPG?raw=true)
TestLink<br>
![TestLink](https://github.com/shyun-ab/shyun-ab.github.io/blob/master/_screenshots/TestLink-bugs.JPG?raw=true)
SonarQube<br>
![SonarQube](https://github.com/shyun-ab/shyun-ab.github.io/blob/master/_screenshots/SonarQube.JPG?raw=true)
<br>
<br>
CTIP 환경 구축이 거의 프로젝트의 반..이었다고 볼 수 있는데...<br><br>
자동화 환경이라는 건 한 번 만들면 정말 편하지만 만드는 과정이 꽤 복잡한 것 같다. 사실상 실습 수업에서는 정말 'CTIP' 자체가 무엇인지만 알려주고, ~~대충 소프트웨어 도구 모음 사이트만 던져준 후, 알아서 조사해서~~ 환경을 만들라고 했다. (....)<br>
<br>
그래서 만들었다! TestLink, Redmine 설치 빼고 나머지 환경구축은 내가 다 한 것 같다. 팀원들이 안 해서는 아니고 빨리 조사하고 해결하지 않으면 내 마음이 편치 못해서 새벽까지 구글링했다.<br><br>
처음에 힘들었던 점은, 나 혼자 사용하는 서버가 아니라 정말 실시간으로 사용할 수 있는 환경을 만들어야 해서 클라우드 서버 서비스를 이용해야 했는데 이에 대해 아는 것이 정말 하나도 없었다는 점이다..ㅜ
<br>
프리 티어를 사용하기 위해 AWS 영어 문서를 어찌어찌 해석해가며 세팅하고, Jenkins와 SonarQube를 AWS EC2에 설치했는데 SonarQube가 running을 시키자마자 바로 다운됐다. 로그를 보니 메모리 부족인데 프리 티어는 메모리가 한정되어 있어서 그 메모리 안에서 쓸 수 있는 방법을 찾으려고 며칠 밤 동안 새벽까지 검색했는데 유일하게 보이는 해결법인 JVM 설정은 효과가 없었다. <br>
그래서 그냥 Jenkins와 SonarQube를 각각 Azure와 Naver Cloud Platform으로 옮겼다. (Jenkins와 SonarQube를 연결하려면 SonarScanner라는 플러그인을 깔아야 하는데 이것도 메모리를 만만치 않게 잡아먹어서 AWS 프리 티어로는 역부족이었다.)<br>
<br>
그 다음으로 힘들었던 점은 gradle 빌드에 대해서도 아는 것이 거의 없었던 것... plugin을 사용할 때 Jenkins에서 열심히 설정했음에도 불구하고 build.gradle 파일을 제대로 수정하지 않아 왜 report들이 안 뜨는지 이해를 못해서 조금 헤맸다. <br>
그치만 gradle은 공식 사이트에 문서가 많고 이해하기 쉽게 잘 되어 있기 때문에, 사실상 공식 사이트만 제대로 쭉 읽어도 헤맬 일이 없다!^^ 구글링하면 maven같은 것만 나와서 왜 gradle은 정보가 별로 없나 생각했는데... 그게 아니라 공식 문서에 예시 코드까지 다 있었던 것이다. (....)<br>
maven 보다 빌드 설정하기도 쉽고, gradle에서 쓰는 언어인 groovy도 딱히 따로 공부할 필요가 없는 것이어서 앞으로 다른 프로젝트에서도 계속 쓸 것 같다. <br>
<br>
내가 지식이 거의 없는 상태에서 시작해서 좀 헤매긴 했지만, 그렇기 때문에 얻어가는 것이 매우 많은 수업이었던 것 같다. 빌드 자동화라던지 프로젝트를 위한 여러 도구들을 써볼 기회가 없었는데 이 수업을 통해서 경험해봐서 좋았다. 지식이 없어서 어렵긴 했어도, 그 모르는 것들을 열심히 찾아서 혼자 해결하는 과정도 굉장히 뿌듯했다! 맨 마지막에 모든 세팅이 끝나고, 자동화가 완벽하게 돌아가면서 의도한 report들도 다 나올 때 새벽에 혼자 박수치기도 했다.
<br><br>

- - -

<br>
###System Testing & Static Analysis
- [1st System Test Report](http://dslab.konkuk.ac.kr/Class/2018/18SV/Team%20Project/4/T5_System_Test_Report.pdf)
- [2nd System Test Report](http://dslab.konkuk.ac.kr/Class/2018/18SV/Team%20Project/5/T5_System_Test_Report.pdf)
- [Static Analysis Report](http://dslab.konkuk.ac.kr/Class/2018/18SV/Team%20Project/5/T5_Static_Analysis_Report.pdf)
<br><br>
아 졸리당 여기까지 쓰고 이어서 써야지~