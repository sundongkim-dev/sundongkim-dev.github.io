---
published: true
title: '[데이터 사이언스] Mining max patterns & closed patterns'
layout: post
subtitle: 'csReview DataScience FPgrowth'
categories: csReview
tags: DataScience
comments: true
---

Frequent pattern이 너무 많아서 그 대신 max pattern이나 closed pattern과 같은 좀 더 엄격한 룰을 적용한 패턴을 마이닝하는 것이 보완책으로 제안되었다.

### MaxMiner: Mining Max-patterns

Max pattern은 더 늘릴 게 없는 frequent pattern이다. 즉 frequent super pattern이 없는 상태를 말한다.

Apriroi 알고리즘을 기반으로, max pattern만을 효과적으로 구하기 위한 방법으로 MaxMiner가 제시되었다.

첫 번째 scan에서 frequent item들을 찾고 오름차순(frequency 기준)으로 정렬한다. ex) A, B, C, D, E -> E가 제일 빈번함

두 번째 scan에서 2-itemsets와 potential max-patterns의 support를 구한다.

ex) {BC, BD, BE}라면 potential max-patterns는 BCDE 이런식으로 구해서 만약 ABCDE가 frequent하다면, 그의 부분집합도 모두 freqeunt하다. 즉, BCD, BDE, CDE를 검증할 필요가 없어진다.

만약, AC가 frequent하지 않다면, ABC는 검증할 필요가 없어진다.

Set-enumeration tree를 이용하고 pruning하면서 진행한다.

### CLOSET: Mining Closed-patterns

Closed pattern은 frequent pattern인 동시에 그와 같은 support를 갖는 super pattern이 없는 것이다. CLOSET은 FP-tree를 사용해서 frequent pattern을 찾는다.

### CHARM: Mining by Exploring Vertical Data Format

Vertical Format이란 트랜잭션 관점(horizontal view)에서 보는 것이 아닌 아이템 관점으로 보는 것이다. 해당 아이템을 갖고 있는 트랜잭션을 list(tid-list)로 갖는다고 생각하면 된다.

Horizontal한 format을 vertical로 바꾸기 위해 한 번 scan한다. Item 수가 transaction 수보다 훨~~~씬 적기 때문에 쉽다. 그 다음, K=1부터 K+1 itemset의 후보를 만든다. Tid-sets interaction(Minsup 넘어야 함)과 Apriori property를 이용한다. 그래서 frequent itemset이 더이상 나오지 않을때까지 반복한다.

장점으로는 (k+1)-itemsets의 support를 계산하기 위해 database를 스캔하지 않아도 된다. TID-set이 자체로 support value를 지니고 있기 때문이다. 하지만 intersection에 많은 시간과 공간이 필요하다. 이를 해결하기 위해 diffset technique를 이용한다. 두 아이템셋이 등장하는 transaction id를 비교하여 차집합만 저장한다.

### Mining various kinds of association rules
**a. Mining multilevel association**
아이템들은 주로 계층을 형성한다!! 계층이 낮을 수록 낮은 support value를 사용하는 것이 좋다. 예를 들어, Milk라는 아이템이 있고 2% milk, skim milk라는 하위 계층의 milk가 있다면 당연히 하위 계층에 낮은 support value를 적용하는 것이 당연해보인다. 그게 reduced support라고 하고 그렇지 않고 똑같이 적용하는 것이 uniform support이다. uniform support는 계층이 낮을수록 association rule에 포함되기 힘들고, 높을수록 포함되기 쉬워진다.

**Redundancy Filtering**  
어떤 rule들은 ancestor가 있기 때문에 중복되는 경우가 있다.

> milk => wheat bread (support=8%, confidence=70%)  
2% milk => wheat bread (support=2%, confidence=72%)

위와 같을 때 첫 번째 rule이 두 번째 rule의 ancestor라고 한다.
Descendent rule은 descendent의 support가 ancestor의 support값과 비교하여 기대하는 값과 비슷하고, descendent의 confidence값이 ancestor의 confidence 와 비슷할 때, 'redundant' 하다고 한다.

**b. Mining multidimensional association**
- Single-dimensional rules: 하나의 dimension이나 predicate를 갖는다.  
ex) buys(X, "milk") => buys(X, "bread"): milk->bread
처럼 buys 하나의 predicate만 사용!!

- Multi-dimensional rules: 2개 이상의 dimensions나 predicates를 갖는다.  
  + Inter-dimension association rules(no repeated predicates)  
  ex) age(X, "19-25") ^ occupation(X, "student") => buys(X, "coke")
  + Hybrid-dimension association rules(repeated predicates)  
  ex) age(X, "19-25") ^ buys(X, "popcorn") => buys(X, "coke")

> age(X, "19-25") ^ occupation(X, "student") => buys(X, "coke")

**Attribute Types**  
위의 "19-25", "student", "coke"들이 attribute에 해당된다.
- Categorical Attributes: value가 유한한 양수이고 value 사이에 순서가 없다.
- Quantitative Attributes: 수치이며 value 사이에 암시된 순서가 있으며, 이산화하거나 클러스터링 작업이 필요


**c. Mining quantitative association**
1. Static discretization based on predefined concept hierarchies(data cube methods): numeric values는 range(categorical value 처럼)로 바꾸고, k-predicate sets는 k 또는 k+1의 table scan이 필요하다.
ex) 3개의 predicate라면, 3 또는 4번의 스캔

2. Dynamic discretization based on data distribution:  
2D quantitative association rules: A<sub>quan1</sub> ^ A<sub>quan2</sub> => A<sub>cat</sub>  
confidence, support가 threshold보다 높아야 한다.
3. Clustering: distance-based association

**d. Mining interesting correlation patterns**
기존의 support나 confidence는 corrleation을 나타내기 좋은 도구가 아니다. 예를 들어, 전체 학생의 75%가 시리얼을 먹는데 농구를 하면 시리얼을 먹는다[40%, 66.7%]라는 rule은 잘못된 rule이다. confidence가 75%보다 작은 66.7%이기 때문이다. 농구를 하지 않으면 시리얼을 먹지 않는다[20%, 33.3%]가 훨씬 의미 있는 룰이다.

그렇기 때문에 corrleation을 잘 나타내기 좋은 도구로 lift, cosine, all_conf라는 것들이 있다. 그러나 강의 중엔 Lift만 다루었다.

**Lift**  
> lift = P(AUB) / P(A)*P(B)

1을 기준으로 1보다 크면 양의 상관관계이고 낮으면 음의 상관관계를 갖는다.

### Constraint-based(Query-Directed) association mining

Database에 있는 모든 pattern을 찾는 것은 비현실적이다. 패턴은 너무 많기 때문에 사용자가 원하는 방향으로 mining을 진행할 수 있어야 한다.

User flexibility : 무엇을 mining 할지 constraints를 준다.
System optimization : 효과적으로 mining 하기 위해서 constraints를 파악한다.

### Constraints in Data Mining
- Knowledge type constraint: classification, association, clustering etc.

- Data constraint: : SQL-like 쿼리 사용
ex) 상점에서 함께 팔린 물건의 쌍을 찾아라!

- Dimension/level constraint: 모든 attribute를 고려하는 것이 아닌 몇 개만 고려

- Interestingness constraint: min support, min confidence에 대한 constraint 제시

### Constrained Mining vs Other Operations
- Constrained Mining vs Constrained-based search

두 방법의 목표는 search space를 줄이는 것이다. 다만, constrained mining은 constraints를 만족하는 모든 패턴을 찾고, constrained-based search는 constraints를 만족하는 답을 찾기만 하면 된다.

- Constrained Mining vs query processing in DBMS

두 방법은 해당 조건에 맞는 모든 답을 찾는 것이지만 전자는 patterns를 찾는 것이고, 후자는 tuples을 찾는 것이다.

Constrained mining은 query processing에서 pushing selections와 유사한 철학을 공유한다.

### Anti-Monotonicity in Constraint Pushing

- Anti-monotonicity: 만족하지 못하면 앞으로도 만족하지 못한다.

itemset S가 constraint에 성립하지 않으면 S의 superset도 constraint에 성립하지 않는다.

> sum(S.Price) <= v 는 anti-monotone
sum(S.Price) >= v 는 not anti-monotone
range(S.profit)<=15 is anti-monotone

- Monotonicity: 만족하면 앞으로도 만족한다.

itemset S가 constraint에 성립하면 S의 superset도 constraint에 성립한다.

> sum(S.Price)>=v is monotone
min(S.Price)<=v is monotone
range(S.profit)>=15 is monotone

**Succinctness**  
Itemset A1이 constraint C를 만족하면, C를 만족하는 어떤 집합 S는 A1에 기반해서 간단히 구해질 수 있다.

> min(S.Price)<=v is succinct
sum(S.Price)>=v is not succinct

Succinctness의 장점은 transaction database를 보지 않아도 itemset S가 어떤 item들을 선택했는지에 따라 constraint C를 만족하는지를 결정할 수 있다.

최적화: 만약 C가 succinct하면 C는 pre-counting pushable 하다.
candidate-generation time에 basic elements가 포함되어있는지만 확인하면 해당 constraint를 만족하는지 확인할 수 있기 때문이다.

### Converting "Tough" Constraints
tough constraints를 anti-monotone이나 monotone으로 바꾼다.

예시로, avg(S.profit)>=25와 같은 tough constraint를 item을 정렬함으로써 anti-monotone하게 바꾼다. <a,f,g,d,b,h,c,e>로 정렬했고, afb가 C를 위반하면 afbh도 위반할 것이다.

### Frequent-pattern mining: Summary
- Frequent pattern mining - an important task in data mining
- Scalable frequent pattern mining methods
  + Apriori(Candidate generation & test)
  + Projection-based(FPgrowth, CLOSET+, ...)
  + Vertical format approach(CHARM, ...)
- Mining a variety of rules and interesting patterns
- Constraint-based mining
- Extensions and applications
