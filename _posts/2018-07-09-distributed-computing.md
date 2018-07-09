---

layout: post

title: "분산시스템및컴퓨팅 (Distributed Computing)"

categories:

  - Notes

commit: true

---


* 중간고사까지의 필기입니다!
<br>

* 분산 파일 시스템 개념
	-  각 single coherent system을 가진 autonomous한(자주적인) 컴퓨팅 시스템의 집합
	-  Autonomous computing elements = nodes, 하드웨어 디바이스 나 소프트웨어 프로세스
	-  Single coherent system: 사용자나 응용은 하나의 시스템으로 여김
	-> 모든 노드는 하나의 operation을 함께 수행해야 함

	- "Distribution Transparency"
		- Access: data representation의 차이점과 객체에 어떻게 접근하는 지 숨김
		- Location: 객체가 어디있는지 숨김
		- Relocation: 객체가 사용 중에 다른 위치로 옮겨졌다는 것을 숨김
		- Migration: 객체가 다른 위치로 옮겨졌다는 것을 숨김
		- Replication: 객체가 복제되었다는 것을 숨김
		- Concurrency: 객체가 여러 독립적인 사용자들로부터 공유되고 있다는 것을 숨김
		- Failure: 객체의 failure와 recovery를 숨김

	- Partial failure는 불가피
		- Communication latency 숨길 수 없음
		- 네트워크와 노드의 failure 숨길 수 없음
		- Full transparency는 성능 저하를 일으킴
	- '분산되어 있다'는 사실을 어떻게 숨길 것인가?? -> 완전히 숨기는 것 보다 드러내는 것이 나음
	- 분산에서의 OS(=framework, platform) : middleware로 분산 시스템을 연결 (ex. Hadoop) local OS와는 별개

* Scalability
	- "Scalable"
		- Size scalability: 유저나 프로세스의 개수가 많을수록
		- Geographical scalability: 노드들 간의 거리가 떨어져 있을수록
			- 문제점
				- LAN 상에서는 괜찮았으나 WAN 상으로 가면 latency가 길어져 시스템에 문제가 생길 수 있음
				- WAN 상에서 unreliable해질 수 있음
				- WAN 상에서 multicasting이 이루어지지 않음
		- Administrative scalability: (ex. 많은 관리 업체가 하나의 제품(시스템)을 만들 경우 - 하나의 시스템처럼 파악할 수 있도록 했을 때)
			- Computational grids: 다른 관리 domain들이 비싼 resource를 공유함
			- Shared equipment: 어떻게 다른 domain들이 shared equipment를 control, 관리, share하게 할 것인가

* 3 types of 분산 시스템 차이점? & 분산 시스템 예
	- a. High performance distributed compution systems
		- 개미 군단이 코끼리보다 쎄다..^^
		- Started with parallel computing
	- b. Distributed information systems
	- c. Distributed systems for pervasive computing

* 분산 시스템 예) Hadoop, Big data computing, High performance cluster computing

* parallel computing (multi 어쩌구 shared 어쩌구 차이점)
	- Multiprocessor는 multicomputer보다 프로그래밍이 상대적으로 쉬움
	- Performance 면에서 multiprocessor가 훨씬 뛰어나다.
	- Multiprocessor는 프로세서들이 interconnect되어 메모리를 공유
	- Multicomputer는 프로세서들이 각각의 메모리를 가지고 interconnect되어 있다 (서로 접근x)
	- Multiprocessor 프로세서 맥시멈 32개, Multicomputer는 훨씬 적다

* Architecture
	- Layered Architecture : 음 OSI 계층 얘기… 
		- 장점 / 단점: layer 여러개를 거쳐야 해서 low runtime performance
		- 많은 어플리케이션이 이 architecture에 맞지 않다.
			        3) Mapreduce framework
			        2) Yarn framework
			        1) HDFS
	- P2P (Peer to Peer)
		- 프로세스들이 모두 동등하다.
		- 각 프로세스들은 동시에 클라이언트와 서버 둘 다로서 작동한다.
		- (key, value) 페어를 가지고 있다. 둘 사이에 연결 생성
	- Middleware organization
		- 컴포넌트에서 제공하는 인터페이스가 모든 어플리케이션에 맞지는 않으므로 대부분의 클라이언트 어플리케이션에 맞는 인터페이스를 제공하는 wrapper 혹은 adapter를 사용한다.
		- 단점: "대부분"의 어플리케이션에 맞는 인터페이스 제공이므로 다른 특정 어플리케이션을 사용할 때 맞출 수 없을 수 있다..
	- Multi-tiered centralized system architecture
		- 분리된 머신에 각각의 layer가 존재
	- Master-Slave architecture
		- Fault tolerance와 시스템 신뢰성을 위한 main-subroutine architecture. 
		- Slave는 Master에게 복제된 서비스를 제공, 마스터는 서비스의 요청을 설정하고 slave로부터 결과를 받은 후 특정 선택 계획(?)에 따라 특정 결과를 선택한다. 
		- 신뢰성이 아주 중요한 시스템에서 사용됨
		- slave들은 각자 아예 다른 알고리즘과 방법으로 같은 일을 수행할 수 있다. 병렬 처리로 수행.

* Hadoop : 큰 클러스터들의 큰 dataset의 분산 프로세싱을 위한 소프트웨어 프레임워크, 구글 MapReduce의 오픈 소스 도구
	- 두 main layers
		- HDFS: 분산 파일 시스템 - 전체 클러스터를 위한 하나의 namespace. Fault-tolerance를 위해 3x 복제
		- MapReduce: 실행 엔진 - 분산 & fault-tolerance를 관리. Map과 reduce로 job 실행 -> MapReduce랑 Yarn 설명
	- 어디에 쓰는지?
		- 특히 big data를 만드는 applications에서 쓴다! (ex. 웹, 소셜 네트워크, 과학적 어플리케이션)
	- 왜 쓰는지? (Design Principles of Hadoop)
		- Scalability : petabytes of data, 수천개의 머신 - 빅데이터를 프로세스해야 함
		- Flexibility : 모든 데이터 포멧을 받아들임
		- Fault-tolerance, automatic recovery
		- 간단한 메커니즘 & programming : "map" "reduce" 두 function만 제공
		- Cost-efficiency : 비싸지 않은 하드웨어 (cheap, but unreliable) - 병렬로 동작하는 싼 머신들을 아주 많게 (Parallel DBs와 반대된다.)
		- 자동적인 병렬 & 분산 : end-user들에게 숨김
	- Master-Slave shared-nothing Architecture로 디자인 되었다.
		- Master node - Job Tracker. Runs with the namenode
			- 데이터에 대한 하나의 처리인 'job'을 job tracker에서 'task' 단위로 분할
		- Slave node - Task Tracher. Runs on each datanode

* MapReduce: 분산처리 프레임워크 - 하둡의 주요 프로젝트 중 하나.
	- Split = Map 단계로 들어오는 입력 데이터. JobClient에서 크기를 정함
		- Data type: key-value records -> 이게 한 개씩 Map 단계로 넘어감

	- Map function: 입력되는 데이터 필터링. Key-Value 쌍을 Map 처리

	- Shuffle and sort : Map 결과가 Reduce까지 전달되는 과정
		- Shuffle = 메모리에 저장되어있는 mapper의 출력 데이터를 partition, sort and spill한 후 로컬 디스크에 저장 -> 네트워크를 통해 Reducer의 입력 데이터로 전달되는 과정
		- Sort = reduce task로 들어온 데이터를 merge하는 과정

	- Reduce funtion: Map에서 출력된 결과를 모두 받으면 정렬된 조각조각들을 하나로 모으는 처리
		- 같은 Key로 모인 데이터(Value 집합)에 대해 정의내린 Reduce 실행 -> 새로운 쌍 생성 및 출력

	- Yarn : 자원 관리, 자원 스케쥴링
		- ResourceManager = Yarn 클러스터의 마스터 서버. 클러스터 전체 리소스 관리
			- 리소스를 사용하고자 하는 플랫폼으로부터 요청을 받아 리소스 할당(스케쥴링)
		- NodeManager = Yarn 클러스터의 slave 서버.
        	- 사용자가 요청한 프로그램을 실행하는 컨테이너를 fork시키고 모니터링
        	- 컨테이너 문제 상황 또는 오버된 사용 감시 (오버하면 kill)

<br><br>