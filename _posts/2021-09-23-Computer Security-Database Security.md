---
published: true
title: '[컴퓨터 보안] Database Security'
layout: post
subtitle: 'csReview Computer Security'
categories: csReview
tags: ComputerSecurity
comments: true
---


# Database security

![DBMS Architecture](https://sundongkim-dev.github.io/assets/img/DMBS_Architecture.jpg)  
DBMS에 대한 보다 자세한 설명은 다른 탭에 있는 DB글을 참고하길 바란다.

### Relational Databases
행과 열로 구성된 데이터 테이블들로, 각 열에는 특정 유형의 데이터가 들어가 있으며, 각 행은 각 열에 대한 특정 값을 갖는다. 이상적으로는, 모든 값이 고유한 하나의 열이 있어 해당 행에 대한 식별자(키)를 형성한다.

**Relational Database Elements**
+ Relation / Table / File
+ Tuple / Row(Record)
+ Attribute / Column(Field)

1. Primary Key(기본 키, PK)
  열을 고유하게 식별하며, 하나 이상의 열 이름으로 구성됨
2. Foreign key(외래 키, FK)
  한 표를 다른 표의 속성과 연결하는 키
3. View / Virtual table
  하나 이상의 테이블에서 선택한 행과 열을 반환하는 쿼리의 결과

### Structured Query Language(SQL)
1970년대 중반에 IBM에 의해 개발되었으며, 관계형 데이터베이스(RDBMS)에서 데이터를 정의, 조작 및 쿼리하는 표준화된 언어이다. 표를 만들고, 데이터를 삽입, 삭제할 수 있으며, View를 만들고, 쿼리를 통해 저장된 데이터를 불러올 수 있다.

### OWASP TOP 10
OWASP TOP 10은 악용가능성, 탐지가능성 및 영향에 대해 빈도수가 높고 보안상 영향을 크게 줄 수 있는 10가지 웹 애플리케이션 보안 취약점 목록이다. 수업시간에 배운자료는 다음과 같이 2010과 2013이였지만 최근 기록을 찾아보니 꽤나 바뀌었음을 확인할 수 있었다.
![OWASP TOP 10_2010 & 2013](https://sundongkim-dev.github.io/assets/img/OWASP2013.jpg)  
![OWASP TOP 10_2017 & 2021 ](https://sundongkim-dev.github.io/assets/img/OWASP2021.jpg)  
### SQL Injection Attack
수업시간에 참고한 OWASP 자료가 2010년과 2013년 기준이어서 그런지, Injection에 대해 강조하셨다. 임의의 SQL문을 주입하여 실행하고 db가 비정상적인 동작을 하도록 조작하는 공격이다. 예시를 들자면 아래 그림과 같다. 대다수의 Web application이 form을 통해 사용자 입력을 가져오는 데, 이 때, ID부분에 저런식으로 입력해보는 것이다.
![SQL Injection Userid](https://sundongkim-dev.github.io/assets/img/sqlInjectionAttack.jpg)
만약 이것이 실행된다면, SELECT user FROM table WHERE name = 'user_input'; 이런 SQL 문이 실행되는 것과 유사하다. 이렇게 되면, 비밀번호 없이 접근이 가능해진다.
ex) select * from users where user = 'M' OR '1=1 --' AND pwd='M' OR '1=1'  
위와 같은 쿼리문을 실행하면, 1과 1은 같기에 무조건 참이 되어 로그인에 성공하게 된다.

위의 쿼리를 한 단계 더 발전시켜보자.  
1. Select user, pwd from users where user = '$usern'
$usern = 'M' OR '1=1'  
결과적으로, 해당 table의 모든 내용을 얻게 된다.  
2. $usern="M'; drop table user;"  
해당 테이블을 삭제하는 것도 가능하다.

### Correct Solution for SQL Injection Attack
Escape method로 해결할 수 있다. Escape("t ' c") = "t \\' c"
select user, pwd from users where user='$usern'
$usern=escape("M'; drop table user;")
-> select user, pwd from users
      where user = 'M\\' drop table user;\\''
보통의 경우 홀따옴표를 쌍따옴표로 바꿔주어 쿼리를 생성한다.

### SQL Access Controls
접근 권한을 관리하는 데 있어 다음 두 가지 command가 있다.
1. Grant: 하나 이상의 접근 권한을 부여하거나 역할에 사용자를 할당하는 데 사용할 수 있음
2. Revoke: 액세스 권한 취소
ex) select, insert, update, delete, references

만약 Revoke된다면 다음과 같이 시점에 따라 cascading된다. David에서 Frank가 지워지지 않은 이유는 시점 상 chris가 준 권한으로 이루어졌을 수 있기 때문이다.
![Cascading Authorizations](https://sundongkim-dev.github.io/assets/img/cascadingAuthorization.jpg)

### RBAC(Role-Based Access Control)
Role-Based Access Control는 관리 부담을 완화하고 보안을 개선한다. DB 사용자의 유형은 다음과 같다.
+ Application Owner: 애플리케이션의 일부로 데이터베이스 개체를 소유한 최종 사용자
+ End User: 특정 응용 프로그램을 통해 데이터베이스 개체에서 작동하지만 데이터베이스 개체를 소유하지 않는 최종 사용자
+ Administrator: 데이터베이스의 일부 또는 전체에 대한 관리 책임이 있는 사용자
DB RBAC은 역할 생성 및 삭제, 역할 할당에 대한 권한 정의, 역할에 대한 사용자 할당 취소 등의 기능을 제공해야 한다.

### Inference Attack
이 공격은 수신된 합법적인 응답으로부터 허가되지 않은 정보를 추론하고 쿼리를 수행하는 과정이다. Inference channel은 허가되지 않은 데이터가 얻어지는 정보 전송 경로이다.  
![Indirect Information Access Via Inference Channel](https://sundongkim-dev.github.io/assets/img/InferenceAttack.jpg)
예를 들어, 누가 얼마의 연봉(Sensitive data)을 받는지를 알고 싶은 상황이 있다. Position과 Salary의 테이블과 Name과 Department의 테이블을 가져와서 추론하는 것이다.
![Inference Example](https://sundongkim-dev.github.io/assets/img/inferenceExample.jpg)

### Inference Countermeasures
+ 데이터베이스 설계 시 탐지 가능: 데이터베이스 구조 변경 또는 접근 제어 시스템 변경
+ Query time에 추론 탐지: 쿼리를 모니터링하거나 변경 또는 거부


### Statistical Databases(SDB) & Security
개수 및 평균과 같은 통계적 특성에 대한 데이터를 제공하는 DB로 두 가지 유형이 있다.
1. Pure Statistical DB: 통계 데이터만을 저장
2. Ordinary DB with Statistical Accesss: 개별 항목을 포함하며 DAC, MAC, RBAC을 사용한다.
접근 제어  목표는 데이터베이스의 기밀성을 훼손하지 않고 사용자에게 필요한 정보를 제공하는 것이다.
Statistical query는 쿼리 집합에 대해 계산된 값을 생성하는 쿼리이다.

### Protecting Against Inference
1. Query set restriction
  + Query set overlap control: 새 쿼리와 이전 쿼리 간의 중복을 제한함
  + Partitioning: 레코드를 서로 상호 배타적인 그룹으로 클러스터링함 / 각 그룹의 통계 속성을 전체적으로 조회함
  + Query denial and Information leakage: 쿼리 거부는 정보를 누설할 수 있으며, counter하려면 사용자로부터 쿼리를 추적해야 함
2. Data perturbation
3. Output perturbation

### Perturbation
원본 데이터에서 생성된 통계에 노이즈를 추가하는 것이다. 목표는 원래 결과와 교란된 결과 간의 차이를 최소화하는 것이다. 주요한 도전과제는 사용할 오차의 평균 크기를 결정하는 것이다.
1. data perturbation technique: 데이터를 수정하여 다음 값을 추론하는 데 사용할 수 없는 통계를 생성할 수 있음
  + Data swapping
2. output perturbation technique: 시스템은 원래 데이터베이스가 제공하는 통계에서 수정된 통계를 생성함
  + Random-sample query

### Database Encryption
DB는 여러 계층의 보안에 의해 보호되는데, 다음과 같은 것들이 지원해준다.
+ Firewall
+ Authentication
+ OS Access control system
+ DB access control system
+ database encryption
암호화는 특히 중요한 데이터를 위해 사용되는 경우가 많으며 레코드 수준, 어트리뷰트 수준 또는 개별 필드의 수준에서 전체 데이터베이스에 적용할 수 있다. 암호화로 인한 단점이 몇 가지 있는데, 키 관리가 어렵고, 쿼리를 처리할 때 inflexible하다.

다음 4개의 주체가 상호작용을 한다.
1. Data Owner: 통제된 release에 사용 가능한 데이터를 만드는 조직
2. User: 시스템에 쿼리를 표시하는 사용자
3. Client: 사용자의 쿼리를 서버에 저장된 암호화된 데이터에 대한 쿼리로 변환하는 프론트엔드
4. Server: data owner로부터 암호화된 데이터를 받고 다른 client들을 위해 사용 가능(분배)하게 함

### Cloud Security & Cloud Computing Elements
![Cloud Computing Elements](https://sundongkim-dev.github.io/assets/img/cloudComputingElements.jpg)

### Cloud Security Risks
1. **Abuse and nefarious use of cloud Computing**
2. Insecure interfaces and APIs
3. **Malicious insiders**
4. Shared technology issues
5. **Data loss or leakage**
6. Account or service hijacking
7. Unknown risk profile
### Data Protection in the Cloud
+ Cloud에서 데이터 손상 위협은 증가하고 있다.
  + 클라우드 고유의 리스크 및 과제
  + 클라우드 환경의 아키텍쳐 또는 운영 특성
+ Multi-Instance Model
  + 각 클라우드 가입자에 대해 가상 시스템 인스턴스에서 실행되는 고유한 DBMS 제공
  + 가입자가 보안과 관련된 관리 작업을 완전히 제어할 수 있도록 함
+ Multi-Tenant Model
  + 일반적으로 가입자 식별자가 있는 데이터 태그를 통해 다른 tenant와 공유되는 클라우드 가입자를 위한 미리 정의된 환경을 제공
  + 인스턴스를 독점적으로 사용하는 것처럼 보이지만 안전한 데이터베이스 환경을 구축하고 유지하기 위해 클라우드 공급자에 의존
