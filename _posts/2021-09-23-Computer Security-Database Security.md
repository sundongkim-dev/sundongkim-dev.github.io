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
이 공격은 수신된 합법적인 응답으로부터 허가되지 않은 정보를 추론하고 쿼리를 수행하는 과정이다.

### Inference Countermeasures

### Statistical Databases(SDB) & Security

### Protecting Against Inference
1. Query set restriction
2. Data perturbation
3. Output perturbation

### Perturbation
1. data perturbation technique
  + Data swapping
2. output perturbation technique

### Database Encryption
### Cloud Security
### Cloud Computing Elements
### Cloud Security Risks
### Data Protection in the Cloud
