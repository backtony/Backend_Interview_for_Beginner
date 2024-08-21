# graphQL

<br>

-----------------------

### graphQL 이란

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

> API용 쿼리 언어

REST는 클라이언트의 빠르게 변화하는 요구 사항에 대처하기에 그렇게 유연하지 않다. 그런 경우 데이터가 더 복잡해지면 경로가 더 길어진다. 때로는 단일 요청으로 데이터를 가져오는 것이 어려울 수도 있고(언더 페칭), 불필요한 데이터 필드까지 조회해야만 하는 경우(오버페칭)가 있다. 

* 장점
  * 하나의 엔드포인트로 요청을 처리
  * 불필요한 데이터가 오는 오버 페칭 문제 해결
  * 한 번의 요청으로 원하는 데이터를 다 가져오지 못하는 언더 페칭 문제 해결
* 단점
  * multipart/form-data 형식 미지원 => 파일 업,다운로드 구현이 어려움
  * 단일 엔드포인트로 인해 http 캐싱이 어렵다
  * 서버단에서 rest api에 비해 구현하기 어렵다.(러닝 커브) 

</details>

-----------------------

<br>

### Schema 

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

스키마는 GraphQL 서버를 통해 페치할 수 있는 데이터의 모델이다.  
클라이언트가 어떤 쿼리를 할 수 있는지, 서버에서 어떤 유형의 데이터를 페치할 수 있는지, 그리고 이러한 유형 간의 관계가 무엇인지 정의한다.

</details>

-----------------------

<br>

### union, interface, enum, fragment, directive, Instrumentation

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

* union : 여러 타입 중 하나임을 의미하는 집합 형태로 공통된 필드를 가지지 않아도 된다.
* interface : 여러 타입이 공통적으로 가져야하는 필드를 정의할 때 사용
* enum : 자바와 같은 열거형 타입
* fragment : 재사용 가능한 필드 집합 정의, 특정 타입의 일부 필드만 별도로 구성하여 재사용하고 싶은 경우에 사용
* directive : 스키마에 동적 동작을 추가하기 위해 사용하는 도구(annotation을 달아서 처리하는데 spring aop와 유사)
* Instrumentation : 쿼리의 실행을 관찰하고 런타임 동작을 변경할 수 있는 코드를 주입하는 기능(인터셉터와 유사) 

</details>

-----------------------


<br>

### resolver

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

* resolver : 특정 필드에 대한 요청을 처리하는 함수
  * 종류
    * query : 조회(read)
    * mutation : 쓰기(write)
    * field : 특정 필드에 대한 데이터를 처리
    * batch(= dataLoader) : N+1 문제를 해결하기 위한
    * subscription : 지속적인 읽기(websocket)
      * 클라이언트는 서버를 반복적으로 폴링하는 대신 특정 이벤트를 구독하고 서버는 관련 이벤트가 발생하면 구독된 클라이언트에 업데이트를 푸시
  
query같은 경우 조회에 해당하므로 병렬 처리가 되나 mutation의 경우 순차처리가 default


</details>

-----------------------

<br>

### 동작 순서

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

1. 요청 수신
2. 쿼리 파싱 & 검증(쿼리 구문 오류, 유효한 스키마, ..)
3. 리졸버 선택 & 실행
4. 필요시 배치 처리, 필드 리졸버 호출
5. 응답 객체 생성 후 응답

</details>

-----------------------

<br>

### 에러 핸들링

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

기본적으로 에러가 발생해도 http status는 200으로 내려가며 응답 필드로 errors 필드가 추가되어 나간다. 
spring graphql은 에러 타입을 다음과 같이 제공한다.

* BAD_REQUEST
* UNAUTHORIZED
* FORBIDDEN
* NOT_FOUND
* INTERNAL_ERROR

</details>

-----------------------

<br>

### 권한과 인증

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

자체적으로 제공하는 기능은 없고 spring을 사용한다면 resolver 단에 security를 붙일 수 있다.

</details>

-----------------------

<br>

### context

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

리졸버는 마지막 인자로 context 객체를 받을 수 있다. context에는 특정 쿼리 실행에서 모든 리졸버 간에 공유 환경을 제공한다. 가령 인증 정보 등을 담아서 사용한다. 

</details>

-----------------------

<br>

### Versioning

<details>
   <summary> 예비 답안 보기 (👈 Click)</summary>
<br />

-----------------------

> https://graphql.org/learn/best-practices/#versioning


graphql은 버저닝을 권고하지 않는다. 
애초에 새로운 필드와 타입을 추가할 수 있고 client는 원하는 필드만 가져가서 사용하면 되기 때문이다.

</details>

-----------------------

<br>
