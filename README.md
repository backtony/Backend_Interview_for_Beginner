
<div align="center">
    <img src="./image/thumb.jpg" width="60%"></img>
</div>


----

<div align="center"> <h1> Backend Tech Interview </div>
  
  <div align="center"> 이곳은 신입 개발자로 취업을 준비하면서 공부했던 지식을 정리하는 공간입니다. <br> 지식의 확장을 넘어서 기술 면접을 준비함에 있어서 도움이 되기를 바랍니다.<br>
이 곳은 개인적인 공간이 아닌 여러분들과 함께 채워나갈 수 있기에,<br>issue와 Pull Request를 통해 이 레퍼지토리의 컨트리뷰터가 되어주세요. <br>
내용이 마음에 들거나 유용하다면 Star를 한번씩 눌러주시면 감사하겠습니다. 🙏  </div>

----




[**📌 2022 상반기 네이버 웹툰 신입 공채 합격 회고**](https://velog.io/@backtony/2022-%EC%83%81%EB%B0%98%EA%B8%B0-%EB%B0%B1%EC%97%94%EB%93%9C-%EA%B0%9C%EB%B0%9C-%EC%B7%A8%EC%97%85-%ED%9A%8C%EA%B3%A0)


<br>

## :memo: Table of Contents

+ [Java](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Java.md)
+ [Spring & JPA](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Spring%20%26%20JPA.md)
+ [Database](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Database.md)
+ [Network](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Network.md)
+ [Operating System](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/OS.md)
+ [Algorithm & SQL](https://github.com/backtony/Backend_Interview_for_Beginner/tree/master/algorithm#algorithm--sql)


<Br>


## :bulb: Java [Link](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Java.md)

+ Python vs Java vs Kotlin
+ Java 장단점
+ OOP(객체 지향 프로그래밍) 특징
+ SOLID 원칙
+ 객체 지향 프로그래밍 vs 절차 지향 프로그래밍
+ JVM 구조
+ 가비지 컬렉터
+ 접근 제한자
+ String vs Char
+ ==과 equals
+ 데이터 타입
+ Call By Value와 Call By Reference
+ hashcode
+ Wrapper class
+ 박싱, 언방식
+ non-static vs static
+ main이 static인 이유
+ final vs finally vs finalize
+ try with resources 
+ 제네릭
+ 직렬화와 역직렬화
+ 오버로딩, 오버라이딩
+ 추상 클래스와 인터페이스 차이
+ Error, Exception
+ Checked Exception, Unchecked Exception
+ Java Collections
+ String, StringBuilder, StringBuffer
+ Blocking vs Non-Blocking
+ Sync vs Async
+ 리플렉션
+ Stream
+ Fork Join Pool
+ 람다식
+ Optional
+ 자바8 추가된 내용
+ Java 8 -> Java 11
+ 함수형 프로그래밍
+ 멀티스레드 프로그래밍
+ Java 동기화 방식
+ Synchronized와 Lock & Condition 동기화
+ Atomic 동기화

<br>

## :bulb: Spring & JPA [Link](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Spring%20%26%20JPA.md)

+ 프레임워크란
+ Spring 정의 및 장점
+ DI (Dependency Injection)
    - 주입 방식
+ IoC
+ 스프링 컨테이너
+ Bean 정의 
    - 생명주기
    - 스코프
+ 싱글톤 vs 스프링 싱글톤
+ Annotation
+ Spring Annotation
+ 웹 서버와 웹 애플리케이션 서버
+ 서블릿
+ 서블릿 컨테이너
+ MVC 패턴
+ AOP(Aspect Oriented Programming)
+ POJO
+ DAO, DTO
+ Filter vs Interceptor
+ AOP vs Interceptor
+ 레이어드 아키텍처
+ OSIV
+ 커넥션 풀
+ DataSource
+ 트랜잭션을 추상화하는 이유
+ 트랜잭션 동기화 매니저
+ 선언적 트랜잭션 vs 프로그래밍 방식 트랜잭션
+ @Transactional
+ Propagation 전파단계
+ ORM
+ 영속성 컨텍스트
+ N+1 문제
+ fetch join 한계
    - OneToMany fetch join 페이징 쿼리 성능 이슈
    - MultipleBagFetchException
+ OneToOne 양방향 관계 Lazy 로딩 주의
+ 상속관계 매핑
+ QueryDsl을 사용하는 이유
+ Spring batch
+ MSA vs Monolithic(모놀리식)
+ DDD 구조

<br>

## :bulb: Database [Link](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Database.md)

+ DBMS
+ 스키마
+ 뷰
+ 키
+ 트랜잭션 ACID
+ 트랜잭션 격리수준
+ Commit
+ Rollback
+ Locking
+ 갱신 분실 문제
+ 조인
+ 트리거
+ 힌트
+ 인덱스
    - Cluster 인덱스
    - Non-Cluster 인덱스
    - 멀티 인덱스
    - B 트리
+ 정규화, 반정규화
+ 커넥션 풀
+ 관계형 DB vs NoSQL
+ Redis, MongoDB, Memcached
+ Elastic search
+ 클러스터링
+ 레플리케이션
+ 수직 파티셔닝
+ 샤딩(수평 파티셔닝)
+ SQL Injection
+ 행의 개수가 많은 테이블 설계
+ Statement, PreparedStatement
+ RabbitMQ와 Kafka

<br>

## :bulb: Network [Link](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/Network.md)

+ OSI 7계층
+ DNS
+ www.google.com에 접속할 때 일어나는 일
+ 4 way-hand shaking
+ 포트와 소켓
+ CIDR(사이더)
+ 서브넷
+ 캐스트
+ MTU
+ TCP, UDP
+ HTTP, HTTPS
+ HTTP 1.0 vs HTTP 1.1 vs HTTP 2.0
+ CORS
+ REST API
+ 쿠키, 세션
+ JWT
+ OAuth
+ URI, URL, URN
+ 중간자 공격
+ WebSocket과 Socket.io
+ gRPC

<br>

## :bulb: Operating System [Link](https://github.com/backtony/Backend_Interview_for_Beginner/blob/master/OS.md)

+ 커널
+ 메모리구조
+ 스택과 힙의 차이점
+ 힙영역을 크게 잡으면 안되는 이유
+ 프로세스와 스레드
+ 멀티 스레드 vs 멀티 프로세스
+ 크롬 탭은 프로세스인지 쓰레드인지
+ 스레드마다 스택을 독립적으로 할당하는 이유
+ 스레드마다 PC 레지스터를 독립적으로 할당하는 이유
+ 컨텍스트 스위칭
+ 프로세스 종류
+ Deadlock
+ Critical Section(임계영역)
+ 경쟁 상태(Race Condition)
+ 수준 스레드
+ 사용자 모드와 커널 모드
+ 프로세스 스케줄러 종류
+ CPU Scheduling
+ 인터럽트
+ 시스템 콜
+ 메모리 관리
+ 가상 메모리
+ Trashing
+ 캐시의 지역성

<br>

## :bulb: Algorithm & SQL [Link](https://github.com/backtony/Backend_Interview_for_Beginner/tree/master/algorithm#algorithm--sql)

+ 코딩 테스트에서 사용하는 파이썬 API
+ 코딩 테스트에서 사용하는 파이썬 정규식
+ 코딩 테스트에서 사용하는 자바 API
+ 프로그래머스 알고리즘
+ 리트코드 알고리즘
+ 프로그래머스 SQL
+ HackerRank SQL
