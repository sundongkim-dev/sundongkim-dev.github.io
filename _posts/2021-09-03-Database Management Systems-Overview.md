---
published: true
title: '[데이터베이스] Database Management Systems - Overview'
layout: post
subtitle: 'csReview Database'
categories: csReview
tags: DB
comments: true
---

# DB 복습
DB는 원래 2학년 2학기에 수강해야하는 과목이지만 과제가 너무 어렵다고 하여 미뤄두었던 과목이다. 이번 학기에 수강을 시작하였는데 미리 미리 정리하여 복습해야겠다. 본문은  Ramakrishnan & Gehrke, Database Management Systems, 3rd Ed., 2002를 참고하였다.

---
### What is a DBMS?
DB는 매우 크고 통합된 데이터 모음으로 실제 세상을 모델로 하며 DBMS(DB Management System)는 DB를 저장하고 관리하도록 설계된 소프트웨어 패키지이다. 다음과 같은 크게 5가지 이유 때문에 사람들이 DBMS를 사용한다.

1. Data Independence(데이터 독립성)와 효율적인 Access
2. 애플리케이션 개발 시간 단축
3. 데이터 무결성 및 보안
4. 데이터의 용이한 관리
5. 동시 Access 및 충돌 복구

### Data models
**Data model**: 데이터를 기술하는 개념의 모음이다  
**Schema**: 스키마는 지정된 데이터 모델을 사용하는 특정 데이터 집합에 대한 설명이다  
**Relational model of data**: 데이터 관계형 모델로, 오늘날 가장 널리 사용되며 관계와 행과 열이 있는 표로 나타낸다. 모든 관게에는 열 또는 필드를 설명하는 스키마가 있다

### Levels of Abstraction
다음과 같은 3단계 스키마 구조에서는 DB를 관점에 따라 외부 스키마(View 1,2,3...), 개념 스키마(Conceptual Schema), 내부 스키마(Physical Schema) 3단계로 나뉜다.  
![Levels of Abstraction(3-Level Schema)](https://sundongkim-dev.github.io/assets/img/3LevelAbstraction.JPG)
1. 외부 스키마: 각 사용자의 데이터에 대한 관점
2. 개념 스키마: 모든 사용자의 관점(논리적 관점), 하나의 데이터베이스 시스템에는 하나의 개념 스키마만 존재함
3. 내부 스키마: 물리적으로 DB에 접근하는 관점(물리적 관점)
위와 같이 3단계로 나눔으로써 논리적/물리적 독립성을 얻게 된다.

**Data Independence(데이터 독립성)**: 하위 단계의 데이터 구조가 변경되더라도 상위 단계에 영향을 미치지 않는 속성으로 구조의 변화로 인한 영향을 프로그램에 미치지 않도록 한다
1. Logical data Independence: 가운데 단계인 개념 스키마를 바꿔도 상위 단계인 View(외부 스키마)에 영향을 주지 않는 것
2. Physical data Independence: 데이터의 물리적인 구조가 변화더라도 상위 단계인 개념 스키마에 영향을 주지 않는 것




---  
아래 주제들은 이후에 자세히 다루도록 하겠다.
### Concurrency control
### Transaction
### Scheduling Concurrent Transactions
### Ensuring Atomicity
### The Log
### Structure of a DBMS
![Structure of a DBMS](https://sundongkim-dev.github.io/assets/img/DBMSstructure.jpg)
