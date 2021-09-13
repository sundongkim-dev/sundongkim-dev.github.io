---
published: false
title: '[데이터베이스] Introduction to Database Design'
layout: post
subtitle: 'csReview Database'
categories: csReview
tags: DB
comments: true
---

## Steps in Database Design
DB를 디자인하는데 있어 크게 6가지 단계로 이루어져있다. 이번에 집중적으로 다룰 ER model은 처음 세 단계와 연관이 깊다.  

1. Requirements Analysis  
간단히 말해서 사용자가 무엇을 원하는지 또 무엇을 필요로 하는지 분석하는 단계이다.  
2. Conceptual Design  
1단계에서 얻은 정보들로 db구축에 있어서 보다 자세한 description을 만드는 단계이다. 대개 ER model을 사용하여 표현한다.
3. Logical Design  
2단계에서 만든 ER model을 DBMS data model로 변환한다. 이 과정에서 이를 구현할 DBMS를 반드시 골라야 한다.
4. Schema Refinement  
Consistency, Normalization
5. Physical Design  
Indexes, disk layout
6. Security Design  
DB 접근 권한, 방법

## Entity-Relationship model
요구사항으로부터 얻어낸 정보들을 Entity, Attribute, Relation으로 기술하는 그래프 기반의 데이터 모델이다.

## ER Model Basics: Entities
**Entity**: Attribute 값들로 설명하는 실제 세계의 **개체**이다.  
**Entity Set**
  + 개체들로 구성된 집합으로 이 집합.
  + 모든 Entity들은 같은 Attribute Set을 갖고 있다.
  + 각 개체들은 key를 가지고 있다. (밑줄을 그어 표시함)
  + 각 Attribute는 domain을 가지고 있다.

## ER Model Basics: Relationships
**Relationship**
+ 두 개 이상의 entity간의 관련성을 말한다.
+ Relationship 또한 Attribute를 지닐 수 있다.
+ **하나**의 Entitiy Set내에서의 Relationship을 **Unary Relationship**, **두 개**는 **Binary Relationship**, **세 개**는 **Ternary Relationship**이라 한다.

**Relationship Set**
+ 비슷한 관계들의 집합이다.
+ 개체와 그 개체가 속한 Entity Set으로 구성된 n개의 Tuple로 구성된다.
+ Descriptive Atrribute(관계에 관한 정보)를 가질 수 있다.

## Role Indicator
Unary Relationship에서 한 개체 집합이 여러 역할을 수행할 때, Role indicator는 Relation set의 Attribute와 해당 Entity Set의 Attribut를 결합하여 Entity Set의 Attribute를 유일한 상태로 유지시킨다.

## Additional Features of the ER model
1. Key Constraints
  + ER Diagram에서 Key Constraints는 화살표로 표시된다.
  + 1 to Many 관계를 나타내는 조건이다.
  + At most one이라고 생각하면 된다(0 or 1)
2. Participation Constraints
  + Total Participation: 굵은 실선으로 표시하며 해당 Entity Set에 속한 **모든 Entity**가 관계를 맺고 있음을 말한다. (=At least one)
  + Partial Participation: 얇은 실선으로 표시하며 해당 Entity Set에 속한 Entity 중 **일부만** 관계를 맺고 있음을 말한다.
3. Weak Entities
  + 굵은 실선으로 표시하며 다른 계체와 관계되어야 존재할 수 있는 개체이다.
  + Weak Entity의 Key는 단독적인 Key로 인정되지 않으며, Partial Key라 한다. (Weak Entity Key = Owner Entity Key + Weak Entity Partial key)
  + Partial Key는 끊어진 밑줄로 표시한다.
  + Owner 개체와 Weak Entity는 1-to-Many 관계이다.
  + Weak Entity는 반드시 Total Participation으로 Owner Entity와 관계된다.
  + Owner와 Weak Entity를 잇는 관계집합을 Identifying Relation Set이라 한다.

## Crow's Foot Notation
![Crow's Foot Notation](https://sundongkim-dev.github.io/assets/img/crowFootNotation.jpg)

## Math Terminology - Relations
![관계 수식에 따른 표현](https://sundongkim-dev.github.io/assets/img/mathTerminologyRelations.jpg)

---
## ISA("is a") Hierarchies
만약 A ISA B라면, 모든 A entity는 B의 Attribute도 직접적으로 갖고 있는 형태이다.

**Generalization(Upward)**: 여러 개체집합들 사이에서 공통되는 Attribute를 찾고, 공통되는 Attribute만으로 구성된 Entity Set(Superclass)을 생성하는 과정  
**Specialization(Down)**: 어떤 Superclass 개체 집합의 모든 Attribute를 Inherit받고 몇 개의 Attribute를 추가하는 과정

**Constraints in ISA Relation**
1. **Overlap Constraints(중첩 제약조건)**
한 개체가 두 개 이상의 SUbclass에 속할 수 있는가? ex) Joe가 Hourly_Emps인 동시에 Contract_Emps인가?
2. **Covering Constraints(포괄 제약조건)**
모든 Subclass가 Superclass 개체들을 전부 Cover하는가? ex)모든 Emps가 Hourly이거나 Contract인가?

---
## Aggregation
개체 집합과 관계 집합을 포함하는 Relationship를 모형화해야 할 때 사용한다.  
다른 관계에 참여할 수 있게 Relationship set을 Entity set처럼 여기게 한다.
