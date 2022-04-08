---
published: true
title: '[데이터 사이언스] Frequent pattern mining'
layout: post
subtitle: 'csReview DataScience Apriori'
categories: csReview
tags: DataScience
comments: true
---

### 학습 목표

대규모 데이터베이스에서 데이터 마이닝의 테크닉 및 어플리케이션을 학습하자!!

- 데이터 마이닝의 컨셉 이야기(방대한 데이터에서 interesting한 패턴을 찾는 방법)
- 다양한 데이터 마이닝 테크닉 학습
- 데이터 마이닝 어플리케이션 이해하기
- 실세계 데이터를 데이터 마이닝을 사용해서 분석하기
- 데이터 마이닝 응용 프로그램을 개발하여 프로그래밍 능력 향상시키기

### 다룰 내용

1. Data preprocessing
2. Frequent pattern mining
3. Association mining
4. Data clustering
5. Classification and Prediction
6. Data generalization
7. Outlier analysis
8. Social network analysis
9. Recommendation
10. Other Big data issues

### 과제

1. Frequent pattern mining: Apriori
2. Classification: Decision tree
3. Clustering: DBSCAN
4. Recommender system

## Chapter 5: Mining Frequent Patterns, Association and Correlations
- Basic concepts and a road map
- Efficient and scalable frequent itemset mining methods
- Mining various kinds of association rules
- From association mining to correlation analysis
- Constraint-based association mining
- Summary

---
#### 1. Frequent pattern analysis란 무엇인가?  
Frequent pattern이란 데이터셋에서 빈번하게 발생하는 어떤 패턴(아이템들의 집합, 부분열 등)을 말한다.

데이터에서 내재된 특성, 규칙을 찾기 위해 생겨난 것이다. 예를 들어, "어떤 상품이 자주 같이 주문되는가?",
"컴퓨터를 사고난 다음에 살만한 물건은?", "신약에 민감한 DNA의 종류는?"과 같은 질문들에 답을 할 수 있게 되는 것이다.
~~맥주와 기저귀를 자주 구매,,아버지가 주로 쇼핑을 하셔서 그런가보다~~

이런 것들을 좀 더 그럴듯하게 표현해보면 Basket data analysis, cross-marketing, catalog design,
sale campaign analysis, web log(click stream) analysis, DNA sequence analysis 등을 해결할 수 있게 된다.

#### 2. 왜 Frequent pattern은 중요한가?  
앞서 말한 application들을 만들 수 있는 것만으로 직관적으로 frequent pattern이 중요함은 알 수 있지만 그래도 왜 중요할까?

다시 한번 말하지만, 데이터셋의 본질적 특성, 중요한 특성들을 알아낼 수 있기 때문이다. 이를 통해 데이터 마이닝 작업의
토대를 만들기도 하고, association(연관성), correlation(상관관계) 및 causality(인과관계) 등을 분석할 수 있게 된다.
또는 sub-graph처럼 순차적이고 구조적인 패턴을 얻을 수도 있다.

이뿐이랴? 시공간 멀티미디어 시간 패턴을 분석할수도 있고, 추후에 배울 classification, cluster analysis, Semantic Data
압축 등 광범위한 어플리케이션을 만들어낼 수도 있다.

---
### Basic concepts: Frequent patterns & Association rules
Frequent pattern에 대해서 직관적이지만 모호하게 표현하였는데 자세히 알아보자. 먼저 이를 학습하기 위해 몇 가지 기본이 되는 컨셉을 알아야 한다.

**1. 우선, Association rule을 알기 위해 아래 문장을 분석해보자.**

> minimum support & confidence를 만족하는 모든 Association rule(X->Y)들을 찾아라.

우선 support와 confidence부터 살펴보자.

support는 `아이템셋 X와 Y를 모두 포함하는 트랜잭션의 수 / 전체 트랜잭션의 수`라고 할 수 있겠다. 그렇기 때문에 X와 Y를 모두 갖고 있는(X U Y) 트랜잭션의 확률이라고 표현할 수 있다. 얼핏 보면 합집합이 아니라 교집합이 맞지 않나라고 생각할 수 있지만 합집합이 맞다. 아이템셋 관점이 아니라 트랜잭션 관점이기 때문이다. 즉, X와 Y가 트랜잭션이 아니라 아이템셋이기 때문이다.

confidence는 `아이템셋 X, Y를 포함하는 트랜잭션의 수 / 아이템셋 X를 포함하는 트랜잭션의 수`이다.

잘 이해가 안 갈 수 있다. 예시로 한 번 더 살펴보자. 아래와 같은 표가 주어지고,

| Transaction-id | Items bought |
| -------- | :------: |
| 10 | A,B,D |
| 20 | A,C,D |
| 30 | A,D,E |
| 40 | B,E,F |
| 50 | B,C,D,E,F |  

 sup<sub>min</sub>이 50%이고, conf<sub>min</sub>이 50%라면 모든 Association rule X->Y를 찾는 예시이다.

A와 D를 동시에 갖는 트랜잭션은 3개이고, A를 포함하는 셋은 마찬가지로 3개이기 때문에 confidence는 100%이고, A,D를 동시에 포함하는 트랜잭션의 수는 3개이고 전체 트랜잭션의 수는 5개이기에 3/5로 60%이다.

위와 같이 계산해보면 frequent pattern은 {A:3, B:3, D:4, E:3, AD:3}으로 구할 수 있고 ~~어떻게 구하는 지는 조금만 이따가!!,~~ association rule은 A->D(sup:60%, conf:100%), D->A(sup:60%, 75%)이다.

**2. 다음 알아야 할 것은 Closed-pattern과 Max-pattern이다.**  

Frequent pattern에 문제가 있다. 바로 sub-patterns를 모두 고려해야 하는데, 이는 cost가 매우 큰 원인이 된다. 만약 frequent pattern의 길이가 100이라면 100C1+...+100C100까지 모두 더한 값의 가짓수를 검토해야 하는데, 이는 2<sup>100</sup>-1 만큼이나 된다. 약 1.27*10<sup>30</sup>만큼이다.

그래서 frequent pattern 대신에 closed pattern과 max pattern을 구하게 된다.
아직은 잘 모르지만, 딱봐도 가짓수가 더 적은, 더 strict한 룰을 가지지 않겠는가!

아이템셋 X가 frequent하고 이와 같은 support를 갖는 super-pattern Y(X를 포함하는 Y)가 없다면 X를 closed pattern이라고 할 수 있다. 이러한 closed pattern은 lossless compression이다. 이는 곧 closed pattern만으로 frequent pattern을 만들어낼 수 있단 말이다.
ex) CLOSET

아이템셋 X가 frequent하고 super-pattern Y가 없다면 X는 max-pattern이다. 즉 더 늘릴게 없는 상황이다.
ex) MaxMiner

마찬가지로 예시를 들어보자. DB에 {<a1, ..., a100}, <a1, ..., a50>}과 같이 저장되어 있다고 하자. 편의를 위해 두 개의 트랜잭션만을 두었다. 이때 sup<sub>min</sub>이 1이라면, ~~support는 확률이지만 편의상 개수로 주어질 때도 있다~~

모든 frequent pattern의 가짓수는?
> 2<sup>100</sup>-1

closed itemset은?
> <a1, ... , a100> , <a1, ..., a50>

max pattern은?
> <a1, ... , a100>

---
### Efficient and scalable frequent itemset mining methods
Frequent pattern mining을 찾아내는 방법은 크게 세 가지가 있는데, 먼저 frequent pattern의 아주 중요한 특성을 소개하고자 한다. 바로 **downward closure**라고 부르는 property이다. 어떤 frequent한 아이템셋이 있다면, 그의 부분집합도 반드시 frequent하다는 것이다. 아주 당연한 말이다.

1. Apriori
2. Frequent pattern growth(FP-growth)
3. Vertical data format approach(Charm)

---
#### 1. Apriori: Frequent할 가능성이 있는 후보들을 생성하고 테스트하기
여기서 바로 앞서 배운 downward closure 명제의 대우를 사용하는데 그것이 바로 **Apriori pruning principle**이다. 만약 어떤 하나의 아이템셋이라도 infrequent하다면 그를 포함하는 superset은 볼 필요도 없다 것이다. 방법은 아래와 같다.

1. 최초로 DB를 한 번 스캔하며 1개짜리 frequent한 아이템셋을 얻는다.
2. 그 아이템 셋으로부터 길이가 1 늘어난 후보를 생성한다.
3. DB를 순회하면서 2번에서 생성한 후보들을 검증한다.
4. frequent set이 더이상 안나오거나, candidate set이 더이상 생성되지 않는다면 종료한다.

매우 간단한 로직이다. 이를 그림으로 살펴보면 아래와 같다. ![Apriori](https://sundongkim-dev.github.io/assets/img/data-science/apriori.png)  

후보를 생성하는 방법은 ~~앞선 그림을 통해 이해하면 더 빠르겠지만~~ 다음과 같다.
먼저 L<sub>k</sub>에서 self-joining을 해서 후보들을 만들어내고, pruning을 거친다. pruning은 만들어낸 후보의 subset이 frequent하지 않다면 걸러내면 된다.
예를 들어, L<sub>3</sub>={abc,abd,acd,ace,bcd}라면 self-joining을 통해 abcd와 acde를 얻을 수 있는데, acde의 subset인 ade가 L<sub>3</sub>에 존재하지 않기 때문에 frequent하지 않은 것이므로 걸러져서 C<sub>4</sub>이 된다. ~~이후 db를 돌면서 support를 만족하는지 따져주며 검증하면 된다~~

이러한 Apriori에는 몇 가지 문제점이 있다. 일단 길이마다 DB를 scan해야하기 때문에 max length만큼 반복하게 되고, 후보의 수도 어마어마하다는 사실을 앞서 배웠다. 또한 support counting하는 것조차 그 workload가 상당하다.

그에 따라, 이런 문제들을 개선하는 아이디어도 생겨났다.
Multiple scans -> scan 횟수 줄이기
Huge number of candidates -> 후보 줄이기
Support counting -> 똑똑하게 support 계산하기

다음장에서...
