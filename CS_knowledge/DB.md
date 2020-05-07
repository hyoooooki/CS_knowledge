DB(데이터베이스) -data base

##### [1.DBMS(DataBase Management System)](#DBMS)

##### [2. 데이터베이스 풀](#DatabasePool)

##### [3. 정규화(1NF, 2NF, 3NF, BCNF)](#NormalForm)

##### [4. 트랜잭션(Transaction)](#Transaction)

##### [5. JOIN](#JOIN)

##### [6. SQL INJECTION](#SQL-INJECTION)

##### [7. INDEX 란?](#INDEX)

##### [8. Statement와PrepareStatement](#Statement와PrepareStatement)

##### [9. RDBMS & NOSQL](#RDBMS-vs-NOSQL)

##### [10. JDBC & ORM](#JDBC-and-ORM)

##### [11. replication(복제)](#replication)

##### [12. optimizer](#optimizer)

##### [13. Partitioning](#Partitioning)

##### [14. Sharding](#Sharding)

---

## DBMS

<img src="/assets/DBMS_structure.png">

#### 용어정리

* **데이터 (data)** : 의미를 가지며 기록될 수 있는 사실
* **데이터베이스 (database)** : 서로 연관이 있는 데이터의 모임
* **작은 세계(mini-world)** : 전체 세계의 일부분으로 데이터베이스 구축의 대상
* **데이터베이스 관리 시스템(DBMS)** : 데이터베이스를 생성하고, 데이터를 저장 및 관리할 수 있도록 하는 기능을 제공하는 전문 프로그램
* **데이터베이스 시스템 (database system)** : DBMS + DB
* **개체(object)** : 어떠한 사물들을 대표하는 것 (**학생** - 짱구, 철수 등등 /**수업** - DB, OS 등등 )
* **메타데이터(meta - data)** : 기본 데이터베이스의 구성, 데이터 항목 타입, 저장 구조, 제약조건을 명시하는 데이터
* **시스템 카탈로그 (system catalog)** : 메타 데이터를 저장 및 관리하는 장소
* **뷰(view)** : 전체 DB로부터 추출된 가상의 데이터 베이스



#### DB의 특징

* **데이터베이스 시스템의 자기 기술성** : DB내에서 데이터 자체 뿐만 아니라 DB 특성에 관한 데이터를 시스템에서 관리
* **프로그램과 데이터의 격리** : 데이터와 프로그램이 각각 따로 존재하여 데이터가 변경되어도 프로그램에 영향을 주지 않음
* **데이터 추상화** : 구조에 관한 상세 정보를 감춤(사용자에게 view만 제공함)
* **데이터에 대한 다중 뷰 제공** : 사용자의 관점에 따라서 다른 형태의 뷰를 제공
* **데이터 공유** : 다수의 사용자가 동시 접근 가능, 동시성 제어(concurrency control) 기능



#### DB사용자 분류

* **시스템 분석가** : 사용자의 요구사항 분석, 이에 만족하는 트랜잭션 명세 설계
* **DB 설계자** : DB에 저장된 데이터를 선정, DB의 구조 및 특성을 정의
* **응용 프로그래머** : 트랜잭션 명세를 참고하여 응용 프로그램 작성
* **DB관리자 (DBA)** : DB 시스템과 관련된 자원 관리
* **최종 사용자** : DB에 대하여 질의, 변경, 보고서 등을 작성하는 사람
* **DBMS 설계 및 구현자** : DBMS 모듈들과 인터 페이스들을 소프트웨어 패키지로 설계하고 구현
* **도구 개발자** : 데이터베이스 설꼐, 사용, 성능 개선등에 필요한 소프트웨어 설계 및 구현
* **운영 및 유지 보수자** : DB시스템을 위한 하드웨어 및 소프트웨어 환경의 운영 및 유지 보수



#### DBMS의 기능

* 데이터 중복의 제어
  * 데이터 중복 : 동일한 데이터가 여러 곳에서 저장 및 관리
    * 문제점 : 디스크의 낭비, 데이터 일관성(consistency)의 결여 유발
  * 여러 사용자가 하나의 DB를 공유하도록 하여 이러한 중복의 문제 해결
* 권한없는 접근의 통제
  * 접근이 허용된 사용자만 데이터에 접근 가능, 권한 관리 가능
* 프로그램 데이터의 지속성 제공
  * 프로그램과 데이터는 독립적이므로 프로그램에 상관없이 데이터 보존
* 다양한 사용자 인터페이스 제공
  * 사용자에 따라 적합한 형테의 DB접근 방법 제공 (질의어, 프로그래밍 인터페이스 등)
* 관계 표현 기능
  * 서로 다른 데이터간에 다양한 형태의 연관성을 표현할 수 있는 기능 제공
* **무결성 제약 조건의 시행**
  * 무결성 : 응용 데이터가 지정된 제약 조건을 만족해야 하는 성질
  * 무결성에 관한 제약 조건을 정의, 정의된 무결성 제약 조건을 검사
* 백업 및 회복
  * 하드웨어 및 소프트웨어이 고장으로부터 복구 가능
  * 백업 : DB내의 데이터를 중복 저장하는 기능
  * 회복 : 고장시 백업된 데이터로부터 최신 데이터 복구하는 기능



#### DB사용 효과

* **표준화에 공헌** : 조직 내 모든 부서가 표준화 하여 데이터 관리
* **응용 프로그램 개발 시간 단축** : DBMS를 이용해서 처리가 가능하므로 개발 부담 줄음.
* **데이터베이스 구조 수정에 융통성제공** : DB내 자료 구조가 변경되어도 사용자에 영향 X
* **항상 최신의 정보 제공** : 다른 사람의 변경사항을 즉시 참조
* **규모의 경제성** : 조직내 데이터 통합관리로 업무의 중복성이 줄음.



##### DBMS를 사용시 단점

1. 초기 투자비용이 높음.
2. 보안, 동시성 제어, 회복, 무결성 조건 등의 오버헤드가 큼.
3. 단순 작업 시에는 굳이 필요 X.
4. 실시간 데이터 처리 요구 사항이 엄격한 경우 적절하지 않음.
5. 단일 사용자 사용 시 적절하지 않음.



#### 데이터 모델의 개념

* 데이터 추상화를 제공하기 위한 도구
* DB의 구조를 명시하는데 사용되는 개념들의 집합
* 제공하는 개념들의 유형에 따라 모델 분류 가능



#### 데이터 모델의 분류

* 물리적 데이터 모델
  * 데이터가 컴퓨터 내에서 물리적으로 어떻게 저장되는가에 관한 세부 사항을 명시
  * 실질적 데이터 저장 방식과 low-level의 데이터 모델
  * 레코드 형식, 순서, 접근 경로 등의 정보 제공
* 개념적 데이터 모델
  * 데이터를 개념적으로 표현하는 방식
  * 일반 사용자들이 인식하는 방식과 밀접한 상위 수준의 데이터 모델
  * 대표적인 예시 ER모델
* 표현 데이터 모델
  * 물리적 데이터 모델과 개념적 데이터 모델의 중간 수준
  * 일반 사용자들이 이해할 수 있는 방식으로 데이터를 표현하면서도 실질적 데이터 저장방식과도 잘 대응되는 방식 제공
  * 대부분의 DBMS에서 채택
  * 예시 : 관계 모델, 네트워크 모델, 계층 모델



#### 스키마와 인스턴스

* 스키마

  * 데이터 베이스 구조에 대한 명세
  * 설계과정에서 정의
  * 자주 변경 X
  * 구성
    * 내부단계 : 물리적 저장 구조를 기술하는 내부 스키마
    * 개념단계 : 전체 DB의 논리적 구조를 기술하는 개념 스키마
    * 외부단계 (view단계) : 사용자에 따라서 특정 부분만 기술하는 외부 스키마(뷰)

  <br>

* 인스턴스

  * 특정 시점의 DB 내용. 데이터 그 자체로 이해하면 편함.
  * 새로운 데이터의 삽입, 갱신, 삭제에 따라 지속적 변경.



#### 데이터 독립성

* 하위 단계의 스키마를 변경하여도 상위 단계의 스키마에 영향 X
* 논리적 데이터 독립성 : 개념 스키마가 변경되어도 외부 스키마가 영향 X
* 물리적 데이터 독립성 : 내부 스키마가 변경되어도 개념 스키마가 영향 X



#### DBMS 분류

* 데이터 모델에 의한 분류
  * 관계모델 : 레코드들의 집합을 포함하는 다수의 테이블로 표현
  * 네트워크 모델 : 레코드 타입과 1:N 관계의 집합 타입
  * 계층 모델 : 계층적 트리 구조를 이용하여 표현
  * 객체지향 모델 : 객체들의 집합을 포함하는 다수의 클래스로 표현
* 사용자 수에 의한 분류
  * 단일 사용자용
  * 다수 사용자용
* 분산 사이트 수에 의한 분류
  * 중앙 집중형 DBMS
  * 분산 DBMS
* 용도에 의한 분류
  * 범용 DBMS
  * 특수 목적용 DBMS

---



## DatabasePool

#### Connection Pool

DB와 미리 connection( 연결 )을 해놓은 객체들을 pool( 웅덩이 )에 저장해두었다가,

클라이언트 요청이 오면 커넥션을 빌려주고, 볼일이 끝나면 다시 커넥션을 반납받아 pool에 저장하는 방식

<img src="/assets/connectionpool.png">

클라이언트가 DB와 연결이 필요할 때, connection pool에서 connection을 빌려와 DB에 접근해서 쿼리를 막 날린 후, 볼 일이 끝나면 사용했던 connection을 다시 pool에 반납을 하는 과정

<br>

#### Connction이 부족하면?

- 모든 요청이 DB에 접근하고 있고 남은 Conncetion이 없다면, 해당 클라이언트는 대기 상태로 전환시키고 Pool에 Connection이 반환되면 대기 상태에 있는 클라이언트에게 순차적으로 제공된다.

#### 왜 사용할까?

- 매 연결마다 Connection 객체를 생성하고 소멸시키는 비용을 줄일 수 있다.
- 미리 생성된 Connection 객체를 사용하기 때문에, DB 접근 시간이 단축된다.

<br>

​	=> 미리 연결을 맺고 있는 커넥션들이 있기 때문에 커넥션을 맺고 끊는 과정이 불필요.

​		 즉, DB 접근 시 **불필요한 작업( 커넥션 생성, 끊기 )이 사라지므로 성능향상을 기대**

<br>

- DB에 접근하는 Connection의 수를 제한하여, 메모리와 DB에 걸리는 부하를 조정할 수 있다.

  => 커넥션 또한 객체이므로 **메모리를 차지**

  ​	 따라서 무작정 많이 늘리는 것은 메모리를 많이 차지하게 되므로 오히려 성능이 떨어지는 결과 초래

<br>

#### Thread Pool

- 비슷한 맥락으로 Thread pool이라는 개념도 있다.
- 이 역시 매 요청마다 요청을 처리할 Thread를 만드는것이 아닌, 미리 생성한 pool 내의 Thread를 소멸시키지 않고 재사용하여 효율적으로 자원을 활용하는 기법.

#### Thread Pool과 Connection pool

- WAS(Web Application Server)에서 Thread pool과 Connection pool내의 Thread와 Connection의 수는 직접적으로 메모리와 관련이 있기 때문에, 많이 사용하면 할 수록 메모리를 많이 점유하게 된다. 그렇다고 반대로 메모리를 위해 적게 지정한다면, 서버에서는 많은 요청을 처리하지 못하고 대기 할 수 밖에 없다.
- 보통 WAS의 Thread의 수가 Conncetion의 수보다 많은 것이 좋은데, 그 이유는 모든 요청이 DB에 접근하는 작업이 아니기 때문이다.

<br>

## NormalForm

#### 정규화

*관계형 데이터베이스의 설계에서 중복을 최소화하게 데이터를 구조화하는 프로세스를* *정규화라고 한다.*



함수적 종속성을 이용해서 연관성 있는 속성들을 분류하고, 각 릴레이션들에서 이상현상이 생기지 않도록 하는 과정을 말한다.

**데이터베이스 정규화의 목적은 주로 두 가지이다.**

> 1. 불필요한 데이터(data redundancy)를 제거한다.
>
> 2. 데이터 저장을 "논리적으로" 한다.(테이블의 구성이 논리적이고 직관적)

우선 정규화를 안 했을 때의 문제점에 대해서 알아보면

| **STUDENT_ID** | **STUDENT_NM** | S_Address | Subject_opted |
| -------------- | -------------- | --------- | ------------- |
| 401            | Adam           | Nodia     | Bio           |
| 402            | Alex           | Panipat   | Maths         |
| 403            | Stuart         | Jammu     | Maths         |
| 404            | Adam           | Noida     | Physics       |

  위와 같이 정규화가 되지 않은 구조의 테이블의 경우, 데이터 핸들링시 다양한 이상현상이 발생하게 된다.

1. **Update** : Adam의 Address가 변경되었을 때, 여러줄의 데이터를 갱신해야한다. 이로인해 데이터의 불일치(inconsistency)가 발생할 수 있다.

2. **Insert** : 만약 학생이 아무 과목도 수강하지 않는다고 하면, Subject_opted 컬럼에는 NULL이 들어갈 것이다.

3. **Deletion** : 만약 Alex 학생이 과목 수강을 취소한다면 Alex의 레코드가 아예 테이블에서 지워져버린다.

<br>

위와 같이 정규화가 제대로 되지 않은 테이블의 경우 갱신/삽입/삭제 시 다양한 문제점이 발생할 수 있다. 이를 테이블의 구성을 논리적으로 변경하여 해결하고자 하는 것이 바로 정규화이다.

<br>

#### 제 1 정규형 (1NF; First Normal Form)

*릴레이션에 속한 모든 속성의 도메인이 원자 값으로만 구성되어 있으면 **제1정규형**에 속한다.*

<br>

| **STUDENT_ID** |          **COURSE_ID**          |   GRADE   | STUDENT_NM |
| :------------: | :-----------------------------: | :-------: | :--------: |
|    20800399    | CSE011101, CSE022202, CSE033303 | A+, A, B+ |    야붕    |

위와같은 형태의 릴레이션은 제1정규형을 만족하지 않는다. 최소한 아래와 같은 형태가 되어야 제1정규형을 만족한다고 할 수 있다.

<br>

관계형 데이터베이스의 릴레이션은 모든 속성이 원자 값을 가지는 특성이 있기 때문에, 최소한 제1정규형을 만족해야 릴레이션이 될 자격이 있다.

| **STUDENT_ID** | **COURSE_ID** | GRADE | STUDENT_NM |
| :------------: | :-----------: | :---: | :--------: |
|    20800399    |   CSE011101   |  A+   |    야붕    |
|    20800399    |   CSE022202   |   A   |    야붕    |
|    20800399    |   CSE033303   |  B+   |    야붕    |

<br>

#### 제 2 정규형 (2NF; Second Normal Form)

제1정규형만 만족시키는 릴레이션에서 부분 함수 종속성을 가지게 되는 경우 삽입이상, 갱신이상, 삭제이상 세가지 이상현상이 모두 나타나게 된다.

*제1정규형에 속하면서, 기본키가 아닌 모든 속성이 기본키에 완전 함수 종속(기본키 중에 특정 컬럼에만 종속된 컬럼이 없어야 함)되면 **제2정규형**이다.*

<br>

| **학번**(P) | **과목코드**(P) | 성적 | 학부         | 등록금 |
| ----------- | --------------- | ---- | ------------ | ------ |
| 20800399    | CSE011101       | A+   | 컴퓨터공학부 | 350    |
| 20800399    | CSE022202       | A    | 컴퓨터공학부 | 350    |
| 20800399    | CSE033303       | B+   | 컴퓨터공학부 | 350    |
| 21300758    | MEC011101       | F    | 경영학부     | 300    |
| 21400001    | POD032939       | C+   | 기계공학부   | 400    |
| 21500399    | CSE011101       | D    | 컴퓨터공학부 | 350    |

위 릴레이션의 함수적 종속성을 살펴보면 아래와 같다.

> {학번, 과목코드} => 성적
> {학번, 과목코드} => 학부
> {학번, 과목코드} => 등록금
> 학번 => 학부
> 학번 => 등록금
> 학부 => 등록금

현재 학번 => 학부, 학번 => 등록금 두개의 부분 함수 종속성을 가지고 있다. 이를 제거해 주는 것을 제2정규화라고 한다.

<br>

학번->학부, 학번->등록금 두개의 부분 함수 종속성을 제거하여 분리한 두개의 릴레이션은 아래와 같다.

**학생 릴레이션**

| **학번**(P) | 학부         | 등록금 |
| ----------- | ------------ | ------ |
| 20800399    | 컴퓨터공학부 | 350    |
| 21300758    | 경영학부     | 300    |
| 21400001    | 기계공학부   | 400    |
| 21500399    | 컴퓨터공학부 | 350    |

**성적 릴레이션**

| **학번**(P) | **과목코드**(P) | 성적 |
| ----------- | --------------- | ---- |
| 20800399    | CSE011101       | A+   |
| 20800399    | CSE022202       | A    |
| 20800399    | CSE033303       | B+   |
| 21300758    | MEC011101       | F    |
| 21400001    | POD032939       | C+   |
| 21500399    | CSE011101       | D    |

릴레이션이 둘로 분해되면서 학부와 등록금에 대한 중복항목이 제거되었다. 정규화 과정에서 주의할 점은 정규화를 통해 분해된 릴레이션들이 조인을 통해 원래의 구조로 복원될 수 있어야 한다는 것이다.

두 릴레이션 모두 제1정규형에 속하고, 기본키가 아닌 모든 속성이 기본키에 완전 함수 종속되므로 제2정규형을 만족한다.

<br>

> 제 2 정규형을 만족하면 이상현상이 없어질까?  **그렇지 않다.**

**삽입이상**
새로운 학부가 생기는 경우 등록된 학생(학번)이 없다면 학번속성이 NULL이 되므로 삽입할 수 없다.

**갱신이상**
컴퓨터공학부 등록금이 400으로 오르는 경우 20800399, 21500399 둘 모두 바꾸어 주지 않으면 데이터 불일치 문제가 발생한다.

**삭제이상**
21400001 학번을 가진 학생이 자퇴하는 경우, 기계공학부에 대한 정보가 함께 사라진다.

제2정규형에서도 이상현상이 발생하는 이유는 **이행적 함수 종속**이 존재하기 때문이다. 이행적 함수 종속을 없애주는 과정이 **제 3 정규화**이다.

<br>

#### 제 3정규형(3NF; Third Normal Form)

*제 2 정규형에 속하면서, 기본키가 아닌 모든 속성이 기본키에 이행적 함수 종속이 되지 않으면 **제 3 정규형**이다.*

<br>
**이행(移行)적 함수 종속 (Transitive Functional Dependency)**

이행적 함수 종속이라는 게 뭐냐하면 삼단논법 같은 관계를 가진 함수종속이다. X, Y, Z 에 대해 X->Y 이고 Y->Z 이면 X->Z 가 성립한다. 이를 Z 가 X 에 이행적으로 함수 종속되었다고 한다.

학생 릴레이션에서 함수적 종속성은 아래와 같다.

> 학번(X) -> 학부(Y)
> 학부(Y) -> 등록금(Z)
> 학번(X) -> 등록금(Z)

학부에 따라 등록금이 결정되는 것이지 학번에 따라 결정되는 것은 아니므로 두 개의 릴레이션으로 분리

(X->Y, Y->Z 함수적 종속관계로 인해 X->Z 의 이행적 함수 종속 관계가 나타나면 [X, Y], [Y, Z] 두 릴레이션으로 분해)

**이행적 종속 관계를 제거 한 학생 릴레이션과 학부 릴레이션은 아래와 같다.**

| **학번** | 학부         |
| -------- | ------------ |
| 20800399 | 컴퓨터공학부 |
| 21300758 | 경영학부     |
| 21400001 | 기계공학부   |
| 21500399 | 컴퓨터공학부 |

| 학부         | 등록금 |
| ------------ | ------ |
| 컴퓨터공학부 | 350    |
| 경영학부     | 300    |
| 21500399     | 400    |

> 제 3 정규형을 만족하면 이상현상이 없어질까? **그렇지 않다.**

지금까지 살펴본 세가지 릴레이션에서는 기본키가 될 수 있는 후보키가 하나 밖에 없었다. 하지만 **후보키를 여러개 가지고 있는 릴레이션**에서는 제3정규형을 만족하더라도 이상현상이 생길 수 있다.

이를 해결하기 위한 정규형이 보이스-코드 정규형 (BCNF; Boyce-Codd Normal Form)이다. 제3정규형보다 조금 더 엄격한 제약조건을 가지기 때문에 Strong 3NF 라고도 한다.

<br>

#### BCNF (Boyce-Codd Normal Form)

모든 결정자가 Candidate KEY 인 경우 **BCNF** 이다

BCNF 를 위반하는 릴레이션은 이론적으로는 아래와 같은 구조를 가지게 된다.

<img src="/assets/bcnf-violate.png">

위 릴레이션은 1NF 는 만족한다는 가정하에,

- 기본키가 아닌 모든 속성이 기본키에 완전 함수 종속이므로 2NF 를 만족한다.
- 기본키가 아닌 모든 속성이 기본키에 이행적 함수 종속이 되지 않으므로 3NF 를 만족한다.

하지만, 결정자인 C 가 슈퍼키가 아니다. 그러므로 BCNF 를 위반한다. A, B, C 속성만 사용해서 예제를 만들어보자.

##### BCNF를 위반 하는 예제

<img src="/assets/bcnf-violation-ex.png">

키로 사용될 수 있는 속성은 {Student, Course} 혹은 {Course, Instructor} 가 될 수 있다. 이 중에서 {Student, Course} 를 기본키로 선정했다.

3NF 까지 만족하지만 BCNF 를 만족하지 않는 경우에도 삽입이상, 갱신이상, 삭제이상이 생길 수 있다.

**삽입이상**
Algorithms 라는 수업이 Dijkstra 에 의해 열렸다고 하자. 하지만 수강생이 아무도 없는 경우 삽입할 수 없다.

**갱신이상**
James Gosling 이 담당하는 강의가 바뀌게 될 경우 수강생의 수만큼 갱신해줘야 하므로 하나라도 빠뜨리면 데이터 불일치 문제가 발생할 여지가 있다.

**삭제이상**
모찌가 자퇴해서 Computer Architecture 수업의 수강생이 없어지면 Alan Turing 이라는 강사도 사라진다.

<BR>

분해한 두 개의 릴레이션에서 기존 릴레이션에서 결정자역할을 했던 속성을 키로 해준다. 그러면 BCNF 까지 만족시키는 릴레이션 두 개가 생기게 된다.

<img src="/assets/bcnf-violation-resolved.png">

#### 제 4정규형(4NF)

다치 종속(MVD, 다중 값 종속)이 존재할 경우 이를 분해하는 과정

#### 제 5정규형(5NF)

조인 종속이 후보키를 통해서만 성립이 되도록 하는 과정

## Transaction
### 트랜잭션이란
* 트랜잭션(Transaction) 이란
    * 데이터베이스의 상태를 변환시키는 하나의 논리적인 작업 단위를 구성하는 연산들의 집합이다.
        * 예를들어, A계좌에서 B계좌로 일정 금액을 이체한다고 가정하자.
          1. A계좌의 잔액을 확인한다.
          2. A계좌의 금액에서 이체할 금액을 빼고 다시 저장한다.
          3. B계좌의 잔액을 확인한다.
          4. B계좌의 금액에서 이체할 금액을 더하고 다시 저장한다.
        * 이러한 과정들이 모두 합쳐져 계좌이체라는 하나의 작업단위를 구성한다.
    * 하나의 트랜잭션은 Commit 되거나 Rollback 된다.
        * Commit 연산
            * 한개의 논리적 단위(트랜잭션)에 대한 작업이 성공적으로 끝나 데이터베이스가 다시 일관된 상태에 있을 때, 이 트랜잭션이 행한 갱신 연산이 완료된 것을 트랜잭션 관리자에게 알려주는 연산이다.
        * Rollback 연산
            * 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 정상적으로 처리되었더라도 트랜잭션의 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산이다.
            * Rollback 시에는 해당 트랜잭션을 폐기하고, 선택적으로 재시작한다.
    * 데이터베이스 응용 프로그램은 트랜잭션들의 집합으로 정의 할 수 있다.
* 트랜잭션의 성질(ACID)
    * 원자성(Atomicity), All or nothing
        * 트랜잭션의 모든 연산들은 정상적으로 수행 완료되거나 아니면 전혀 어떠한 연산도 수행되지 않은 상태를 보장해야 한다.
    * 일관성(Consistency)
        * 트랜잭션 완료 후에도 데이터베이스가 일관된 상태로 유지되어야 한다. 모순성이 없어야한다.
    * 격리성(Isolation)
        * 하나의 트랜잭션이 실행하는 도중에 변경한 데이터는 이 트랜잭션이 완료될 때까지 다른 트랜잭션이 참조하지 못한다.
        * 어느 강도로 참조하지 못하게 막을 것인지는 트랜잭션 격리 수준 설정 레벨에 달라짐
    * 영속성(Durability)
        * 성공적으로 수행된 트랜잭션은 영원히 반영되어야 한다.
* 트랜잭션의 필요성
    * 현금 인출기를 작동하는 도중에 기계오류나 정전 등과 같은 예기치 않은 상황이 발생하여 카드가 나오지 않거나 기계가 멈추는 경우
    * 각각 다른 지점의 은행에서 동시에 인출할 때, 하나의 지점이 다른 지점에서 저장한 잔액을 덮어 쓰는 경우
    * 위와 같은 상황이 발생되지 않도록 방지하기 위해, 즉, 트랜잭션의 성질인 ACID를 제공받기위해 트랜잭션을 사용한다.
* 트랜잭션의 상태  
    <img src="./assets/transaction-status.png" width="70%" height="70%">
    * 활동(Active)
        * 트랜잭션이 실행 중에 있는 상태, 연산들이 정상적으로 실행 중인 상태
    * 장애(Failed)
        * 트랜잭션이 실행에 오류가 발생하여 중단된 상태
    * 철회(Aborted)
        * 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
    * 부분 완료(Partially Committed)
        * 트랜잭션이 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태
    * 완료(Committed)
        * 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태

### 트랜잭션 격리 수준
* Isolation Level 이란?
  
    * 트랜잭션에서 일관성이 없는 데이터를 허용하도록 하는 수준
* Isolation Level 의 필요성
    * 데이터베이스는 ACID 같이 트랜잭션이 원자적이면서도 독립적인 수행을 하도록 한다.
    * 그래서 Locking 이라는 개념이 등장한다.
        * 트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여하지 못하게 막는 것
    * 하지만 무조건적인 Locking으로 동시에 수행되는 많은 트랜잭션들을 순서대로 처리하는 방식으로 구현되면 DB의 성능은 떨어지게 된다.
    * 반대로 응답성을 높이기 위해 Locking 범위를 줄인다면 잘못된 값이 처리 될 여지가 있다.
    * 그래서 최대한 효율적인 Locking 방법이 필요하다.
* Isolation Level 의 종류
    1. Read Uncommitted (레벨 0)
        * SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리지 않는 Level
        * 트랜잭션에 처리중인 혹은 아직 커밋되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용한다.
        * 따라서, 어떤 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 아직 완료되지 않은(Uncommitted 혹은 Dirty) 트랜잭션이지만 변경된 데이터인 B를 읽을 수 있다.
        * 데이터베이스의 일관성을 유지할 수 없다.
    2. Read Committed (레벨 1)
        * SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리는 Level
        * 트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기하게 된다.
        * Commit이 이루어진 트랜잭션만 조회할 수 있다.
        * 따라서, 어떤 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 해당 데이터에 접근할 수 없다.
        * SQL Server가 Default로 사용하는 Isolation Level
    3. Repeatable Read (레벨 2)
        * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 Level
        * 트랜잭션이 범위 내에서 조회한 데이터의 내용이 항상 동일함을 보장한다.
        * 따라서, 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정이 불가능하다.
    4. Serializable (레벨 3)
        * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 Level
        * 완벽한 읽기 일관성 모드를 제공한다.
        * 따라서, 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정 및 입력이 불가능하다.
    * Isolation level 조정은 동시성이 증가되는데 반해 데이터 무결성에 문제가 발생할 수 있고, 데이터의 무결성을 유지하는 데 반해 동시성이 떨어질 수 있다.
    * 레벨이 높아질수록 비용이 높아진다.
* 낮은 단계의 Isolation Level 이용시 발생하는 현상  
    <img src="./assets/isolation-level.png" width="70%" height="70%">
    * Dirty Read
        * 커밋되지 않은 수정 중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 발생하는 현상
        * 어떤 트랜잭션에서 아직 실행이 끝난지 않은 다른 트랜잭션에 의한 변경 사항을 보게 되는 되는 경우
    * Non-Repeatable Read
        * 한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션이 값을 수정 또는 삭제함으로써 두 쿼리의 결과가 상이하게 나타나는 비 일관성 현상
    * Phantom Read
        * 한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽을 때, 첫 번째 쿼리에서 없던 레코드가 두 번째 쿼리에서 나타나는 현상
        * 이는 트랜잭션 도중 새로운 레코드가 삽입되는 것을 허용하기 때문에 나타난다.
        

# JOIN

> ### JOIN 이란?
> join(조인) 또는 결합 구문은 한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 하나의 열로 표현한 것이다. 따라서 조인은 테이블로서 저장되거나, 그 자체로 이용할 수 있는 결과 셋을 만들어 낸다. JOIN은 2개의 테이블에서 각각의 공통값을 이용함으로써 필드를 조합하는 수단이 된다.
>

자신이 검색하고 싶은 컬럼이 다른 테이블에 있을 경우 주로 사용하며 여러개의 테이블을 마치 하나의 테이블인것처럼 활용하는 방법.
보통 primary key 혹은 foreign key로 두 테이블을 연결. 테이블을 연결하려면 적어도 하나의 컬럼은 서로 공유되고 있어야 한다.


<sub>※ Foreign Key(외래 키)란 한 테이블의 필드(attribute) 중 다른 테이블의 행(row)을 식별할 수 있는 키를 말한다.</sub>

### JOIN의 종류

#### 1. INNER JOIN
- 기준 테이블과 JOIN한 테이블의 중복된 값을 보여준다. A의 테이블과 B의 테이블을 JOIN했다고 하면 결과는 A의 테이블과 B테이블이 모두 가지고 있는 데이터만 검색 된다.
- 표현 형태
  
    1. 명시적 표현(explicit)
    ```sql
		SELECT *
		FROM employee INNER JOIN department
		ON employee.DepartmentID = department.DepartmentID;
    ```
    2. 암시적 표현(implicit)
    ```sql
		SELECT *
		FROM employee, department
		WHERE employee.DepartmentID = department.DepartmentID
    ```
- 종류
  
    1. 동등 JOIN (EQUI JOIN)
       
        JOIN의 대표적 형태. 둘 이상의 테이블에 존재하는 공통 컬럼(속성)의 동등 비교만을 사용하며, 부등호 조인은 동등 조인에 포함하지 않는다.
        ```sql
         SELECT * FROM emp INNER JOIN dept ON emp.deptno = dept.deptno
        ```

    2. 자연 JOIN (NATURAL JOIN)

        조인 대상 테이블의 모든 컬럼을 비교하여, 같은 컬럼명을 가진 컬럼으로 조인을 수행.
        ```sql
        SELECT * FROM emp NATURAL JOIN dept
        ```

    3. 교차 JOIN (CROSS JOIN)

        카티션 곱 (Cartesian Product)이라고도 한다. 한 쪽 테이블의 모든 행들과 다른 테이블의 모든 행을 조인시키는 기능을 한다. 가능한 모든 경우의 수를 출력.

    4. 셀프 JOIN (SELF JOIN)

        같은 두 테이블을 활용하여 데이터를 추출하는 조인 기법.
        ```sql
        SELECT e.empno, e.ename, e.job, e.hiredate, e.sal, m.empno, m.ename, m.job
        FROM emp E
        INNER JOIN emp M ON E.mgr = M.empno
        ```

#### 2. OUTER JOIN
- 조인 대상 테이블에서 특정 테이블의 데이터가 모두 필요한 상황에서 사용.
- 조건에 맞지 않는 데이터도 표시하고 싶을때 사용.

    1. LEFT OUTER JOIN
    
	<img src="/assets/sql-left-join.png">

        수행시 먼저 표기된 좌측 테이블에 해당하는 데이터를 먼저 읽은 후, 나중 표기된 우측 테이블에서 JOIN대상 데이터를 읽어 온다. 테이블 A, B가 있을때 B의 JOIN 컬럼에서 값이 있으면 데이터를 가져오고 없으면 NULL으로 채운다.
        ```sql
        SELECT STADIUM.STADIUM_NAME, STADIUM.STADIUM_ID, STADIUM.SEAT_COUNT, STADIUM.HOMETEAM_ID, TEAM.TEAM_NAME
        FROM STADIUM LEFT OUTER JOIN TEAM
        ON STADIUM.HOMETEAM_ID = TEAM.TEAM_ID
        ORDER BY STADIUM.HOMETEAM_ID;
        ```
    
    2. RIGHT OUTER JOIN
    
	<img src="/assets/sql-right-join.png">

        LEFT JOIN과는 반대로 우측 테이블이 기준이 되어 결과를 생산. 즉 테이블 A,B가 있을 때 컬럼에 같은 값이 있을 때 해당 데이터를 가져오고 A의 JOIN 컬럼에서 같은 값이 없는 경우에는 A 테이블에서 가져오는 컬럼들은 NULL 값으로 채운다.
        
        ```sql
        SELECT E.ENAME, D.DEPTNO, D.DNAME, D.LOC
        FROM EMP E RIGHT OUTER JOIN DEPT D
        ON E.DEPTNO = D.DEPTNO;
        ```


    3. FULL OUTER JOIN 


​	
​	<img src="/assets/sql-full-join.png">
​	
	     LEFT OUTER JOIN 과 RIGHT OUTER JOIN을 합친 결과가 나온다.


# SQL INJECTION

> ### SQL INJECTION이란?
> SQL Injection 이란 악의적인 사용자가 보안상의 취약점을 이용하여, 임의의 SQL 문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위 입니다. 인젝션 공격은 OWASP Top10 중 첫 번째에 속해 있으며, 공격이 비교적 쉬운 편이고 공격에 성공할 경우 큰 피해를 입힐 수 있는 공격입니다.

#### 종류 및 방법
1.  Error Based SQL Injection - 논리적 에러를 이용한 SQL Injection


    가장 대중적인 공격 기법
    
    ex) 
    
    <img src="/assets/error-based-injection.png">
    
    일반적으로 로그인시 많이 사용하는 쿼리문이다. 해당 구문에서 입력값에 대한 검증이 없다는 사실을 확인한다면, 악의적인 사용자가 임의의 SQL 구문을 주입할 수 있다. 주입된 내용은 ‘ OR 1=1 -- 로  WHERE 절에 있는 싱글쿼터를 닫아주기 위한 싱글쿼터와 OR 1=1 라는 구문을 이용해 WHERE 절을 모두 참으로 만들고, -- 를 넣어줌으로 뒤의 구문을 모두 주석 처리 해준다.
    
    매우 간단한 구문이지만, 결론적으로 Users 테이블에 있는 모든 정보를 조회하게 됨으로 써 가장 먼저 만들어진 계정으로 로그인에 성공하게 된다. 보통은 관리자 계정을 맨 처음 만들기 때문에 관리자 계정에 로그인 할 수 있게 된다. 관리자 계정을 탈취한 악의적인 사용자는 관리자의 권한을 이용해 또 다른 2차피해를 발생 시킬 수 있게 된다.

<br>

2. Union based SQL Injection
  
     SQL 에서 Union 키워드는 두 개의 쿼리문에 대한 결과를 통합해서 하나의 테이블로 보여주게 하는 키워드. 이를 악용하여 Injection 을 수행한다.


     ex)
    
    <img src="/assets/union-based-injection.png">
    
    Board 라는 테이블에서 게시글을 검색하는 쿼리문이다. 입력값을 title 과 contents 컬럼의 데이터랑 비교한 뒤 비슷한 글자가 있는 게시글을 출력한다.  여기서 입력값으로 Union 키워드와 함께 컬럼 수를 맞춰서 SELECT 구문을 넣어주게 되면 두 쿼리문이 합쳐서서 하나의 테이블로 보여지게 되기에 사용자의 id와 passwd를 요청하는 쿼리문을 injection 함으로써 인젝션이 성공하게 되면, 사용자의 개인정보가 게시글과 함께 화면에 보여지게 된다.


<br>

3. Blind SQL Injection - Boolean based SQL

      데이터베이스로부터 특정한 값이나 데이터를 전달받지 않고, 단순히 참과 거짓의 정보만 알 수 있을 때 사용 가능하다. 로그인 폼에 SQL Injection이 가능하다고 가정 했을 때, 서버가 응답하는 로그인 성공과 로그인 실패 메시지를 이용하여, DB의 테이블 정보 등을 추출해 낼 수 있다.

      ex)
      
	<img src="/assets/blind-sql-injection.png">

      injection이 가능한 로그인 폼을 통하여 악의적인 사용자는 임의로 가입한 abc123 이라는 아이디와 함께 abc123’ and ASCII(SUBSTR(SELECT name From information_schema.tables WHERE table_type=’base table’ limit 0,1)1,1)) > 100 -- 이라는 구문을 주입한다.

      해당구문은 MySQL 에서 테이블 명을 조회하는 구문으로 limit 키워드를 통해 하나의 테이블만 조회하고, SUBSTR 함수로 첫 글자만, 그리고 마지막으로 ASCII 를 통해서 ascii 값으로 변환해준다. 만약에 조회되는 테이블 명이 Users 라면 ‘U’ 자가 ascii 값으로 조회가 될 것이고, 뒤의 100 이라는 숫자 값과 비교를 하게 된다.  거짓이면 로그인 실패가 될 것이고, 참이 될 때까지 뒤의 100이라는 숫자를 변경해 가면서 비교를 하면 된다.  공격자는 이 프로세스를 자동화 스크립트를 통하여 단기간 내에 테이블 명을 알아 낼 수 있다.


<br>

4. Blind SQL Injection - Time based SQL

      서버로부터 특정한 응답 대신에 참 혹은 거짓의 응답을 통해서 데이터베이스의 정보를 유추하는 기법. MySQL 기준으로 SLEEP 과 BENCHMARK를 사용.


      ex)
    
    <img src="/assets/time-based-injection.png">
    
      Time based SQL Injection을 사용하여 현재 사용하고 있는 데이터베이스의 길이를 알아내는 방법이다. 악의적인 사용자가 abc123’ OR (LENGTH(DATABASE())=1 AND SLEEP(2)) – 이라는 구문을 주입한다. 여기서 LENGTH 함수는 문자열의 길이를 반환하고, DATABASE 함수는 데이터베이스의 이름을 반환 한다.
    
      주입된 구문에서, LENGTH(DATABASE()) = 1 가 참이면 SLEEP(2) 가 동작하고, 거짓이면 동작하지 않는다. 이를 통해서 숫자 1 부분을 조작하여 데이터베이스의 길이를 알아 낼 수 있다. 만약에 SLEEP 이라는 단어가 치환처리 되어있다면, 또 다른 방법으로 BENCHMARK 나 WAIT 함수를 사용 할 수 있다. BENCHMARK 는 BENCHMARK(1000000,AES_ENCRYPT('hello','goodbye')); 이런 식으로 사용이 가능하다.


<br>

5. Stored Procedure SQL Injection
   
    저장 프로시저(Stored Procedure) 은 일련의 쿼리들을 모아 하나의 함수처럼 사용하기 위한 것이다. 공격에 사용되는 대표적인 저장 프로시저는 MS-SQL 에 있는 xp_cmdshell로 윈도우 명령어를 사용할 수 있게 된다. 단, 공격자가 시스템 권한을 획득 해야 하므로 공격난이도가 높으나 공격에 성공한다면, 서버에 직접적인 피해를 입힐 수 있는 공격이다.

<br>
      

6. Mass SQL Injection

    보통 MS-SQL을 사용하는 ASP 기반 웹 애플리케이션에서 많이 사용되며, 쿼리문은 HEX 인코딩 방식으로 인코딩 하여 공격한다. 보통 데이터베이스 값을 변조하여/ 데이터베이스에 악성스크립트를 삽입하고, 사용자들이 변조된 사이트에 접속 시 좀비PC로 감염되게 한다. 이렇게 감염된 좀비 PC들은 DDoS 공격에 사용된다.

<br>

#### 대응방안

1. 입력 값에 대한 검증

    SQL Injection 에서 사용되는 기법과 키워드는 굉장히 많다. 이를 해결하기 위해서는 사용자의 입력 값에 대한 화이트리스트 기반으로 검증해야 한다. 블랙리스트 기반으로 검증하게 되면 수많은 차단 리스트를 등록해야 하고, 하나라도 빠지면 공격에 성공하게 되기 때문이다. 
    
    <br>
2. Prepared Statement 구문사용

    Prepared Statement 구문을 사용하게 되면, 사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전에DBMS가 미리 컴파일 하여 실행하지 않고 대기한다. 그 후 사용자의 입력 값을 문자열로 인식하게 하여 공격쿼리가 들어간다고 하더라도, 사용자의 입력은 이미 의미 없는 단순 문자열 이기 때문에 전체 쿼리문도 공격자의 의도대로 작동하지 않는다.

    <br>
3. Error Message 노출 금지

    공격자가 SQL Injection을 수행하기 위해서는 데이터베이스의 정보(테이블명, 컬럼명 등)가 필요하다. 데이터베이스 에러 발생 시 따로 처리를 해주지 않았다면, 에러가 발생한 쿼리문과 함께 에러에 관한 내용을 반환한다. 여기서 테이블명 및 컬럼명 그리고 쿼리문이 노출이 될 수 있기 때문에, 데이터 베이스에 대한 오류 발생시 사용자에게 보여줄 수 있는 페이지를 제작 혹은 메시지 박스를 띄우도록 해야한다.

    <br>
4. 웹 방화벽 사용

    웹 공격 방어에 특화되어있는 웹 방화벽을 사용하는 것도 하나의 방법이다. 웹 방화벽은 소프트웨어 형, 하드웨어 형, 프록시 형 이렇게 세가지 종류로 나눌 수 있는데 소프트웨어 형은 서버 내에 직접 설치하는 방법이고, 하드웨어 형은 네트워크 상에서 서버 앞 단에 직접 하드웨어 장비로 구성하는 것이며 마지막으로 프록시 형은 DNS 서버 주소를 웹 방화벽으로 바꾸고 서버로 가는 트래픽이 웹 방화벽을 먼저 거치도록 하는 방법이다.





## INDEX



### INDEX 란?

- INDEX란 테이블에 저장된 데이터를 빠르게 조회할 수 있는, 즉 테이블에 대한 동작의 속도를 높여주는 자료구조를 일컫는다.  
  
- DBMS에서 INDEX는 데이터의 저장 성능을 희생하고, 데이터의 읽기 속도를 높이는 기능이다. 왜냐하면 인덱스는 항상 정렬된 상태를 유지하기 때문에 검색은 빠르지만, 추가/삭제/수정의 경우는 속도가 느려질 수 있다.

<br/>

### INDEX를 사용해야 하는 경우

- 데이터의 양이 방대하고 검색이 변경보다 빈번한 경우  

- 인덱스를 걸고자 하는 필드의 값이 다양한 값을 가지는 경우

<br/>

### INDEX를 위한 자료구조

1. B+-Tree Index

   - 데이터베이스의 인덱스 자료구조 중 가장 일반적이고, 범용적인 목적으로 사용되는 자료구조이다.
   
   - 칼럼의 원래 값을 변형시키지 않고, 인덱스 내에서는 항상 정렬된 상태로 유지  
   
2. Hash Index

   - 칼럼의 값으로 해시 값을 계산해서 인덱싱 하는 자료구조, 매우 빠른 검색을 지원하다.
   
   - 값을 변형해서 인덱싱하므로, 전방(Prefix) 일치와 같이 일부 값만 검색하고자 할 때는 사용할 수 없다.
   
   - 주로 메모리 기반 데이터베이스에서 사용

##### 일반적으로 B+-Tree를 사용하는 이유는?

Hash Index의 경우 데이터 접근 시간복잡도가 O(1)로 매우 빠르지만,  Select 조건에는 부등호 연산도 포함이 된다. 즉, Hash Index는 등호(=) 연산에 특화된 자료구조이기 때문에 데이터베이스의 자료구조로 적합하지 않다.

<br/>

### 인덱스의 종류

#### 1. 키에 따른 인덱스 분류 (Primary Index VS Secondary Index)

- 기본 인덱스(Primary Index) 

  - 일반적으로 기본 키(primary key)를 포함하는 인덱스(키의 순서가 레코드의 순서를 결정지음)
  
  - 데이터 블록들 안의 행들의 정렬을 강요한다.
  
  - 키의 중복이 있으면 안된다.
  
  - 하나의 테이블에 오직 하나의 기본 인덱스만 가질 수 있다.
  
  <img src="./assets/primaryindex.png" width="70%" height="70%">

- 보조 인덱스(Secondary Index) 

  - 기본 인덱스 이외의 인덱스( 키의 순서가 레코드의 순서를 의미하지는 않음)
  
  <img src="./assets/secondary.png" width="70%" height="70%">

#### 2. 파일 조직에 따른 인덱스 (Clustered Index VS Unclustered Index)

- 집중 인덱스(Clustered Index) 

  - 레코드의 물리적 순서가 그 파일에 대한 인덱스 엔트리 순서와 동일하게(유사하게) 유지되도록 구성된 인덱스
  
- 비집중 인덱스(Unclustered Index) 

  - 집중 형태가 아닌 인덱스
  <br/>
  <img src="./assets/cluster.png" width="70%" height="70%">

#### 3. 데이터 범위에 따른 인덱스 분류 (Dense Index VS Sparse Index)

- 밀집 인덱스(Dense Index) 

  - 데이터 레코드 각각에 대해 하나의 인덱스 엔트리가 만들어진 인덱스

- 희소 인덱스(Sparse Index) 

  - 레코드 그룹 또는 데이터 블록에 대해 하나의 엔트리가 만들어지는 인덱스 
  <br/>
  <img src="./assets/sparse.png" width="50%" height="50%">

#### 4. 그 외

- 결합 인덱스(Composite Index)

  - 복수 개(2개 이상)의 칼럼으로 구성된 인덱스
  
  - 하나의 칼럼으로는 분포도가 넓어서 인덱스로 만들기에는 부적합하지만 결합을 할 경우 분포도가 양호해 지는경우 생성
  
- 다단계 인덱스(Multilevel Index)

  - 인덱스를 위한 인덱스, 인덱스를 좀 더 효율적으로 사용할 수 있다.
  
  - single-level을 사용 할 경우,  큰 사이즈의 인덱스를 메모리에 유지할 수 없기 때문에 사용한다.
  <br/>   
    
     
  
  <img src="./assets/multi.png" width="30%" height="30%">



#### 참고 - Cost of Operations

<img src="./assets/cost1.png" width="50%" height="50%">
<br/>
<img src="./assets/cost2.png" width="50%" height="50%">

- Heap File : 가장 간단한 파일 구조인 순서가 없는 파일구조
- Sorted FIle : 페이지 내의 데이터가 정렬되어 있는 파일구조
- F : Fanout(한 노드의 자식 노드의 수)
- B : data block의 수
- D : Average time to read/write disk block

<br/>

## Statement와PrepareStatement




### Statement / PreparedStatement 란? 

:  SQL구문을 실행시키는 기능을 갖는 객체
<br/>

### 비교 (Statement vs PreparedStatement)

**Statement**

1. 단일로 사용될 때 빠른 속도를 지닌다.

2. 매번 컴파일을 수행해야 한다.

3. 객체 재사용이 가능하다.
<br/>

**PreparedStatement**

1. 여러번 수행될 때 빠른 속도를 지닌다.

2. 처음 프리컴파일 된 후, 이후에는 컴파일을 수행하지 않는다.

3. 객체 생성시 지정된 sql 실행 -> 객체 재사용 불가능

<br/>

**이 중 가장 큰 차이점은 캐시(cache) 사용여부이다.**

1단계 쿼리 문장 분석

2단계 컴파일

3단계 실행 

Statement의 경우 매번 1~3 단계 수행

PreparedStatement의 경우 처음 1~3단계 수행 후 캐시에 담아 재사용

즉, 동일 쿼리를 반복 수행할 경우 PreparedStatement의 성능이 우월하다.

<br/>

ex) Statement

<img src="./assets/statement.png" width="50%" height="50%">

- 생성 시, 인자가 들어가지 않는다.

- 실행 시, 인자가 들어간다.

- 매번 컴파일 수행

<br/>

ex) PreparedStatement

<img src="./assets/preparedstatement.png" width="50%" height="50%">

- 생성 시, 인자가 들어간다.

- 실행 시, 인자가 들어가지 않는다.

- 첫 실행 시에만 컴파일 수행

- 위치홀더 (?) 사용



=======
## RDBMS vs NOSQL

RDBMS - Relational Database Management System

NOSQL - Not Only SQL (Not relational Database)



#### RDBMS

관계형 데이터베이스 관리 시스템.

정해져있는 데이터 스키마에 따라 DB테이블에 저장되며 관계를 통한 테이블 연결.

데이터의 효율적 관리를 위해 구조화가 굉장히 중요.



**장점**

- 정해진 스키마에 따라 데이터 저장, 명확한 데이터 구조를 보장 (데이터 품질 향상)
- 각 데이터에 맞게 테이블을 나누어 데이터 중복을 피해 데이터 공간 절약
- ACID트랜잭션을 이용한 쉬운 개발 방식
- 뷰를 사용한 보안 설정으로 사용자들로부터의 무분별한 조회나 변경을 막음.



**단점**

- Oracle 같은 시스템을 사용하면 비용적으로 부담 발생
- 시스템 복잡도를 고려하여 구조화 해야함.
- 시스템이 복잡해질수록 query문이 복잡해지고 성능 저하
- 수평적 확장 (서버증설) 이 어려움.대부분 수직적 확장(하드웨어 변경이나 서버 변경)을 함.
- 전체 문서에 대한 검색은 별도의 도구 필요
- 가변성 있는 데이터 저장이 어려움





#### NOSQL

**데이터간의 관계를 정의하지 않음**

관계형 데이터베이스에 반대되는 방식을 사용하여 스키마와 관계라는 개념이 없음.

스키마가 없어 자유롭게 데이터 관리 가능

테이블과 같은 개념으로 **컬렉션**이라는 형태로 데이터 관리



**장점**

- 자유롭게 데이터를 추가 가능. 
- 복잡도의 한계를 극복하여 대용량 데이터를 저장 가능
- 복잡한 테이블간의 관계를 형성하는 형태의 구조를 신경쓰지 않아도 됨.
- 수평적 확장(Scale out)이 쉬움. (수직적 확장 - Scale up)
- 분산처리를 목적으로 나왔기에 프레임 워크에서 분산처리 긴으 포함.
- 필요한 데이터가 보통 하나의 컬렉션에 있음. 자주 변경되지 않음.
- 컴포넌트 형태로 서로 교환될 수 있는 모듈화된 아키텍처 제공
- 자동 샤딩 기술에 대해 적은 운영 비용 발생



**단점**

- 자유롭게 데이터가 추가 가능하므로 컬렉션에 중복된 데이터 저장 가능.
- 만약 중복데이터가 있을 시 업데이트 하려면 데이터를 똑같이 관리해주어야함.
- 세밀한 보안이 제공되지 않음.
- 문서 저장은 NOSQL마다 자체 쿼리언어를 사용해 이식성을 방해함.(표준화X)
- 개발자들에게 새로우며 추가적인 조치를 교육해야함.



**NOSQL 분류**

1. **key/value model**
   - 가장 기본적인 형태
   - **단일 키 - 단일 데이터** 저장 및 조회
   - 단순 저장 구조이며 복잡한 조회 연산은 지원하지 않음
   - 고속 읽기와 쓰기에 최적화
   - 하나의 서비스에 다수의 데이터 조회 및 연산이 발생하면 트랜잭션 처리가 불가능하여 데이터 정합성을 보장할 수 없음. (데이터들의 값이 서로 일치하지 않음.)
2. **document model**
   - key/value 모델의 개념적 확장한 구조
   - **단일 키 - 하나의 구조화된 문서** 저장 및 조회
   - 키는 문서에 대한 ID로 표현 - 이를 이용해 인덱스 생성
   - 문서는 컬렉션 형태로 저장
3. **column model**
   - **단일 키 - 여러 개의 컬럼 이름,값의 쌍(pair)** 형태로 저장 및 조회
   - 모든 컬럼은 항상 타임스탬프 값과 함께 저장
   - 컬럼의 집합 - 로우(row), 로우를 유일하게 식별하는 값 - 로우키(row key), 로우키의 집합 - 키 스페이스(key space)
   - 대부분의 컬럼 모델은 쓰기와 읽기중 쓰기에 특화
   - 데이터를 먼저 커밋로그와 메모리에 저장 후 응답하기에 응답속도 빠름.
   
-----
## JDBC and ORM
#### JDBC(java database connectivity)

자바 프로그램 내에서 DB와 관련된 작업을 처리할 수 있도록 도와주는 일을 함.

- JDBC는 관계형 데이터베이스에 사용되는 SQL문을 실행하기 위해 자바로 작성된 클래스와 인터페이스로 구성되어 있다.

- 특정 데이터베이스나 특정 데이터베이스 메커니즘에 구애 받지않는 독립적인 인터페이스를 통해 다양한 데이터베이스에 접근하는 코드를 구현할 수 있도록 제공하는 자바 클래스의 표준 집합이다.

- JDBC 클래스는 자바 패키지 `java.sql`과 `javax.sql`에 포함되어 있다.

  

  <img src="./assets/JDBC1.png" width="70%" height="70%">



**장점**

- 자바는 DBMS종류에 상관없이 하나의 JDBC를 사용하여 DB작업을 처리할 수 있기 때문에 알아두면 어떤 DBMS든 작업을 처리 할 수 있게 됨 



**실행순서**

1. JDBC 드라이버를 로딩시킨다.

2. DriverManager.getConnection을 통해 데이터베이스 Connection을 구한다.

3. Query 실행을 하기 위하여 Statement 객체 생성한다.

4. Query를 실행한다.

5. Query 실행 결과 사용

6. Statement 종료

7. 데이터베이스 커넥션 종료

<img src="./assets/JDBC2.png" width="70%" height="70%">

**문제점**

- 쿼리를 실행하기 전과 후에 많은 코드를 작성해야한다. EX) 연결 생성, 명령문, ResultSet 닫기, 연결 등
- 데이터베이스 로직에서 예외 처리 코드를 수행해야 한다.
- 트랜잭션을 처리해야 한다.
- 이러한 모든 코드를 반복하는 것으로, 시간이 낭비된다.



reference

-  https://hzoou.tistory.com/64?category=781564 

---

#### ORM(object relational mapping)
<img src="./assets/ORM.png" width="70%" height="70%">

**객체-관계 매핑**

- 사물을 추상화 시켜 이해하는 OOP와 데이터모델을 정형화하여 관리하는 RDB 사이를 연결할 계층의 역할로 제시된 패러다임

- 객체와 관계형 DB의 데이터를 자동으로 매핑해주는 것
  - OOP는 클래스를 사용하고 RDB는 테이블을 사용
  - 객체 모델과 관계형 모델 간에 불일치 존재
  - ORM을 통해 객체 간의 관계를 바탕으로 SQL을 자동 생성하여 불일치를 해결
- **DB테이블 데이터를 Java객체로 전달받을 수 있는 것**



**장점**

- 객체 지향적 코드로 인해 더욱 직관적이고 비즈니스 로직에 집중 가능
  - 개발비용 절감
  - 선언문, 할당, 종료와 같은 부수적인 코드가 없거나 급격히 줄어들음.
  - 각종 객체에 대한 코드를 별도로 작성, 가독성 증가
  - SQL의 절차적이고 순차적인 접근이 아닌 객체 지향적 접근으로 생산성 증가
- 재사용 및 유지보수 편리
  - ORM은 독립적으로 작성, 해당 객체들을 재활용 가능
  - 매핑정보가 명확하여, ERD를 보는 것에 대한 의존도를 낮춤.
- DBMS에 대한 종속성이 줄어든다.
  -  프로그래머가 객체에 집중함으로 DBMS교체와 같은 거대한 작업에도 비교적 적은 리스크와 시간 소요.



**단점**

- 완벽한 ORM으로만 서비스 구현하기 힘듦.
  - 사용하기 편리하지만 설계 단계를 매우 신중하고 정밀하게 구성해야함.
  - 복잡도가 커질수록 난이도가 빠르게 올라감.
  - 잘못된 구현으로 인해 일관성이 깨지는 등의 치명적 오류 발생 가능.
- 자주 사용되는 쿼리의 경우 속도 향상을 위해 Stored procedure를 써야함.
  - stored procedure가 많으면 ORM의 객체 지향적 장점을 활용하기 어려움.
  
  ---
  **영속성**

- 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성.
- 영속성을 갖지 않는 데이터는 단지 메모리에서만 존재하기 때문에 프로그램을 종료하면 모두 잃어버리게 된다. 때문에 파일 시스템, 관계형 테이터베이스 혹은 객체 데이터베이스 등을 활용하여 데이터를 영구하게 저장하여 영속성 부여한다.



 **Persistence layer**

프로그램의 아키텍처에서, 데이터에 영속성을 부여해주는 계층. JDBC를 이용하여 직접 구현할 수 있지만 Persistence framework를 이용한 개발이 많이 이루어진다.

**Persistence framework**

JDBC 프로그래밍의 복잡함이나 번거로움 없이 간단한 작업만으로 데이터베이스와 연동되는 시스템을 빠르게 개발할 수 있으며 안정적인 구동을 보장한다.



<img src="./assets/ORM2.png" width="50%" height="50%">

## replication

#### DBMS 리플리케이션(replication)이란?
* 메인 DBMS 서버의 데이터를 여러개의 slave DBMS 서버에 백업함

#### 목적
* 실시간 데이터 백업
* 엄격한 동기화까진 필요없는 SELECT query 분산 처리 (web page 등)

#### 기법
* 표준 비동기 복제
	* Master DB에 write를 수행하면 해당 변경 내용을 binary log로 남김
	* Binary log를 남기면 데이터 변경 event 발생
	* Slave DBMS가 해당 이벤트 받고 binary log를 slave의 relay log로 가져옴
	* Slave relay log를 기반으로 DB 데이터 업데이트
* 준 동기 복제(semisynchronous)
	* 표준 비동기 복제의 바리에이션
	* Master에서 어떤 write를 하면 binary log를 남기고 나서 데이터 변경 event 발생 후 적어도 하나의 slave로부터 event를 받았단 ACK를 받기 전까지 wait를 함. (혹은 timeout)
	* Wait하면서 master가 block됨으로 성능 저하 발생

#### 쉽게 오해할 수 있는 부분
* Db replication은 동기화 백업 기법이다.
	* Master와 slave가 실시간으로 동기화되는 것은 보장되지 않는다
* Master 서버의 장애발생시 복구수단으로 사용할 수 있다.
	* 완벽한 데이터 복원은 불가능함. 동기화가 보장되지 않기 때문
* 트랜잭션 부하도 분산될 것이다.
	* 선택적인 SELECT만 분산됨.
	* 완벽한 동기화가 필요한 SELECT 문도 분산시킬 순 없음
	* WRITE, select, 테이블 별로 기능 구분을 하여 master, slave를 구분해주는 오버헤드도 고려해야함 Proxy로 구현하거나 application 단에서 구현

#### 로그 기반 복제 (binary log) 
##### 문장(명령) 기반 복제
* 문장 기반 복제에서는 SQL 쿼리문이 binlog에 저장된다. 즉 동일한 INSERT/UPDATE/DELETE 문이 슬레이브에서 그대로 수행된다.
* 이 시스템에서는 아래와 같은 장단점이 있다.
	* 실제의 문장이 바이너리 로그에 저장되므로 데이터베이스를 감사하기 쉽다.
	* 네트워크상에 전송되는 데이터의 양이 적다.
	* 비 결정적 쿼리들은 슬레이브 환경에서 혼란을 야기할 수 있다. (timestamp 등)
	* 쿼리(INSERT based on SELECT 등)에 따라 성능에 영향을 줄 수 있다.
	* SQL의 최적화 및 실행으로 인해 복제가 느려질 수 있다.

##### 행(데이터) 기반 복제
행 기반 복제는 MySQL 5.7.7 부터 기본값으로 많은 장점을 가지고 있다. 행의 변화가 바이너리 로그에 저장되며 문맥정보를 필요로 하지 않는다. 이로 인해 비 결정적 쿼리에 영향을 받지 않는다.
* 추가적인 이점으로는 :
	* 대용량이 아닌 잔챙이 row update에 대해서는 병렬 처리가 가능함
* 단점
	* 많은 수의 행을 변경하는 쿼리를 실행한 경우 네트워크의 트래픽이 현저하게 높아질 수 있다.
	* 데이터베이스상의 변경을 감사하기에 어렵다.
	* 몇 몇의 경우에는 문장기반 복제보다 느려질 수 있다.

## optimizer
#### 옵티마이저란?
* 옵티마이저(Optimizer)는 SQL을 가장 빠르고 효율적으로 수행할 최적(최저비용)의 처리경로를 생성해 주는 DBMS 내부의 핵심엔진이다.
<image src="./assets/optimizer.jpg">
#### 옵티마이저의 종류
##### 규칙 기반 옵티마이저
* 미리 정해놓은 규칙대로 실행 경로가 결정됨
* 휴리스틱 옵티마이저라고도 부름
<image src="./assets/ruleBasedOptimizer.png">
* 규칙 요약
	* Single row > multiple rows
	* Rowid > hashed index
	* Hashed Index > non-index
	* = > between or like
	* Between > 한쪽
	* 한쪽 > full scan
* 예시
	* 아래에서 	Job = 'SALESMAN' 이 sal between 3000 and 6000보다 먼저 수행됨
<code>
select  ename
  from EMP
 where job='SALESMAN'
  and sal between 3000 and 6000
</code>

* 단점
	* 항상 인덱싱을 신뢰하며, full table scan과 손익을 따지지 않음.
##### 비용 기반 옵티마이저
* 비용을 기반으로 최적화를 수행
* "비용"은 예상된 수치이며, 이 통계 지표를 dictionary에 관리함
* 인덱싱을 전적으로 신뢰하며 발생하는 단점을 보완하기 위해 나옴
* 비용을 계산하는 통계 정보가 신뢰성이 좋아야 성능이 좋게 나옴

##### 스스로 학습하는 옵티마이저
* 보다 좋은 성능의 통계 정보를 만들기 위해 자가 학습으로 실시간 개선
##### 옵티마이저의 한계
* 절대 완벽할 순 없음.
* 옵티마이징 펙터를 제공하는 것은 사람의 몫(애초에 DB를 효율적으로 짜놔야함)
* 100% 정확한 통계 유지 어려움
* 통계 지표로 쓰이는 히스토그램 버킷 개수가 254개까지만 허용
* 상관성이 있는 colmumn인 경우 통계 지표가 불리하게 작용될 수도 있음

<br>

## Partitioning

#### Partitioning이란?

큰 Table이나 인덱스를 관리하기 쉬운 단위로 분리하는 방법을 의미.

<br>

#### 목적

##### 1. 성능(Performance)

- 특정 DML과 Query의 성능을 향상시킴, 주로 `대용량 Data Write` 환경에서 효율적이다.
- 많은 Insert가 있는 OLTP 시스템에서 Insert 작업들을 분리된 파티션들로 분산시켜 경합을 줄인다.

##### 2. 가용성(Available)

- 물리적인 파티셔닝으로 인해 전체 데이터의 훼손 가능성이 줄어들고 데이터 가용성이 향상된다.
- 각 분할 영역(partition별로)을 독립적으로 백업하고 복구할 수 있다.
- table의 partition 단위로 Disk I/O을 분산하여 경합을 줄이기 때문에 UPDATE 성능을 향상시킨다.

##### 3. 관리용이성(Manageability)

- 큰 table들을 제거하여 관리를 쉽게 해준다.

<br>

#### DB파티셔닝의 장단점

##### 장점

- 관리적 측면 : partition 단위 백업, 추가, 삭제, 변경
  - 전체 데이터를 손실할 가능성이 줄어들어 데이터 가용성이 향상된다.
  - partition별로 백업 및 복구가 가능하다.
  - partition 단위로 I/O 분산이 가능하여 UPDATE 성능을 향상시킨다.
- 성능적 측면 : partition 단위 조회 및 DML수행
  - 데이터 전체 검색 시 필요한 부분만 탐색해 성능이 증가한다. 즉, Full Scan에서 데이터 Access의 범위를 줄여 성능 향상을 가져온다.
  - 필요한 데이터만 빠르게 조회할 수 있기 때문에 쿼리 자체가 가볍다.

##### 단점

- table간 JOIN에 대한 비용이 증가한다.
- table과 index를 별도로 파티셔닝할 수 없다.
  - table과 index를 같이 파티셔닝해야 한다.

<BR>

#### DB 파티셔닝의 종류

##### 1. 수평 파티셔닝

<img src="./assets/horizontal-partitioning.png">

하나의 테이블의 각 행을 다른 테이블에 분산시키는 것이다.

- 개념
  - 샤딩(Sharding) 과 동일한 개념
  - 스키마(schema)를 복제한 후 샤드키를 기준으로 데이터를 나누는 것을 말한다.
  - 즉, 스키마(schema)가 같은 데이터를 두 개 이상의 테이블에 나누어 저장하는 것을 말한다.
- 특징
  - 퍼포먼스, 가용성을 위해 KEY 기반으로 여러 곳에 분산 저장한다.
  - 일반적으로 분산 저장 기술에서 파티셔닝은 수평 분할을 의미한다.
  - 보통 수평 분할을 한다고 했을 때는 하나의 데이터베이스 안에서 이루어지는 경우를 지칭한다.
- 장점
  - 데이터의 개수를 기준으로 나누어 파티셔닝한다.
  - 데이터의 개수가 작아지고 따라서 index의 개수도 작아지게 된다. 자연스럽게 성능은 향상된다.
- 단점
  - 서버간의 연결과정이 많아진다.
  - 데이터를 찾는 과정이 기존보다 복잡하기 때문에 latency가 증가하게 된다.
  - 하나의 서버가 고장나게 되면 데이터의 무결성이 깨질 수 있다.

<br>

##### 2. 수직 파티셔닝

<img src="./assets/vertical-partitioning.png">

테이블의 일부 열을 빼내는 형태로 분할한다.

- 개념
  - 모든 컬럼들 중 특정 컬럼들을 쪼개서 따로 저장하는 형태를 의미한다.
  - 스키마(schema)를 나누고 데이터가 따라 옮겨가는 것을 말한다.
  - 하나의 엔티티를 2개 이상으로 분리하는 작업이다.
- 특징
  - 관계형 DB에서 3정규화와 같은 개념으로 접근하면 이해하기 쉽다.
  - 하지만 수직 파티셔닝은 이미 정규화된 데이터를 분리하는 과정이다.
- 장점
  - 자주 사용하는 컬럼 등을 분리시켜 성능을 향상시킬 수 있다.
  - 한 테이블을 SELECT하면 결국 모든 컬럼을 메모리에 올리게 되므로 필요없는 컬럼까지 올라가서 한 번에 읽을 수 있는 ROW가 줄어든다. 이는 I/O 측면에서 봤을 때 필요한 컬럼만 올리면 훨씬 많은 수의 ROW를 메모리에 올릴 수 있으니 성능상의 이점이 있다.
  - 같은 타입의 데이터가 저장되기 때문에 저장 시 데이터 압축률을 높일 수 있다.

<BR>

#### DB 파티셔닝의 분할 기준

데이터베이스 관리 시스템은 분할에 대해 각종 기준(분할 기법)을 제공하고 있다. 분할은 ‘분할 키(partitioning key)’를 사용한다.

<img src="./assets/partitioning.png">

##### 1. 범위 분할(Range Partitioning)

- 연속적인 숫자나 날짜 기준으로 Partitioning 한다.
- 손쉬운 관리 기법 제공 에 따른 관리 시간의 단축할 수 있다.

<img src="./assets/range-partitioning.png">

##### 2. 목록 분할(List Partitioning)

- 특정 Partition에 저장 될 Data에 대한 명시적 제어 가능하다.
- 분포도가 비슷 하며, 많은 SQL에서 해당 Column의 조건이 많이 들어오는 경우 유용하다.

<img src="./assets/list-partitioning.png">

##### 3. 해시 분할(Hash Partitioning)

- Partition Key의 Hash값에 의한 Partitioning (균등한 데이터 분할 가능)
- Select시 조건과 무관하게 병렬 Degree 제공 (질의 성능 향상)
- 특정 Data가 어느 Hash Partition에 있는지 판단 불가
- Hash Partition은 파티션을 위한 범위가 없는 데이터에 적합

<img src="./assets/hash-partitioning.png">

##### 4. 합성 분할(Composite Partitioing)

- Composite Partition은 Partition의 Sub-Partitioning 을 말한다.
- 큰 파티션에 대한 I/O 요청을 여러 partition으로 분산할 수 있다.
- Range Partitioning 할 수 있는 Column이 있지만, Partitioning 결과 생성된 Partition이 너무 커서 효과적으로 관리할 수 없을 때 유용하다.

<br>

## Sharding

#### Sharding이란?

<img src="./assets/horizontal-partitioning.png">

- 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법을 의미.

- 'Horizontal Partitioning'이라고 볼 수 있다.

<BR>

#### 샤딩(Sharding)을 적용하기에 앞서.

샤딩(Sharding)을 적용한다는것은?

- 프로그래밍, 운영적인 복잡도는 더 높아지는 단점이 존재.

**가능하면 Sharding을 피하거나 지연시킬 수 있는 방법을 찾는 것이 우선시 되어야 한다.**

- Scale-in
  - Hardware Spec이 더 좋은 컴퓨터를 사용
- Read 부하가 크다면?
  - `Cache`나 [Database의 Replication](https://nesoy.github.io/articles/2018-02/Database-Replication)을 적용하는 것도 하나의 방법
- Table의 일부 컬럼만 자주 사용한다면?
  - `Vertically Partition`도 하나의 방법
  - Data를 Hot, Warm, Cold Data로 분리 [Link](https://d2.naver.com/helloworld/526125)

<BR>

#### 샤딩(Sharding)에 필요한 원리

1. 분산된 Database에서 Data를 어떻게 Read할 것인가?
2. 분산된 Database에 Data를 어떻게 잘 분산시켜서 저장할 것인가?
   - 분산이 잘 되지 않고, **한 쪽으로 Data가 몰리게 되면 자연스럽게 Hotspot**이 되어 성능이 느려지게 된다.
   - 그렇기 때문에 균일하게 분산하는 것이 중요한 목표

<BR>

#### 샤딩(Sharding)의 방법

Shard Key를 어떻게 정의하느냐에 따라 데이터를 효율적으로 분산시키는 것이 결정

##### Hash Shading

<img src="./assets/hash-sharding.png">

Shard Key : Database id를 Hashing 하여 결정

- Hash크기는 Cluster안에 있는 Node개수로 정하게 된다.

**단점**

- Cluster가 포함하는 Node의 개수를 변경하게 되면, Hash 크기가 변하게 되고, Hask Key 또한 변하게 된다. 그려면 기존의 분배된 Data 분산 Rule이 모두 어긋 나게 되고, 결국엔 Resharing이 필요하게 된다.
- Hash Key로 분산되기 때문에 공간의 효율에 대해서는 고려하지 않는다.

<br>

##### Dynamic Sharding

<img src="./assets/dynamic-sharding.png">

- Locator Service를 통해 Shard Key를 얻는다.
- Cluster가 포함하는 Node 개수를 늘려본다면?
  - Locator Service에 Shard Key를 추가만 하면된다.
  - 기존의 Data의 Shard Key는 변경이 없다.
  - 확장에 유연한 구조

**단점**

- Data Relocation을 하게 된다면?
  - Locator Service의 Shard Key Table도 일치시켜줘야 한다.
- Locator가 성능을 위해 Cache하거나 Replication을 한다면?
  - 잘못된 Routing을 통해 Data를 찾지 못하고 Error가 발생한다.
  - Locator에 의존할 수 밖에 없는 단점이 있다.

##### Entity Group

<img src="./assets/EntityGroup.png">

**Key-Value가 아닌 다양한 객체들로 구성된다면 어떨까?**

- 우리는 RDBMS의 join, index, transaction을 사용함으로써 Application의 복잡도를 줄이는 효과를 얻었다.
- 이와 유사한 방법으로 Sharding하는 방법이 Entity Group입니다.

**장점**

- 하나의 물리적인 Shard에 쿼리를 진행한다면 효율적.
- 하나의 Shard에서 강한 응집도를 가질 수 있다.
- 데이터는 자연스럽게 사용자별로 분리되어 저장된다.
- 사용자가 늘어남에 따라 확장성이 좋은 Partitioning이다.

**단점**

- cross-partition 쿼리는 single partition 쿼리보다 consistency의 보장과 성능을 잃는다.
  - 그렇기 때문에 이런 쿼리들이 자주 실행하지 않도록 만들어야 한다.

<br>

<br>

https://medium.com/@jeeyoungk/how-sharding-works-b4dec46b3f6

http://mongodb.citsoft.net/?page_id=225#comment-91922

https://d2.naver.com/helloworld/14822

http://tech.kakao.com/2016/07/01/adt-mysql-shard-rebalancing/