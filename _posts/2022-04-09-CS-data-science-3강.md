---
published: true
title: '[데이터 사이언스] FP-growth vs Apriori'
layout: post
subtitle: 'csReview DataScience FPgrowth'
categories: csReview
tags: DataScience
comments: true
---

이전에 Apriori에 대해 살펴보았는데 Apriori의 문제점을 개선하는 것들을 소개하고 특정 상황에서는 더 좋은 알고리즘인 FP Growth에 대해 알아보자.

### Improving Apriori algorithm

**1. Multiple DB Scans**

a. Partition

이전에 apriori의 단점으로 너무 많은 DB scan을 한다는 점이 있었다. 이를 개선하기 위해 DB를 k 개의 조각으로 나눈다. 이를 partition이라고 하고, 각 partition은 메인 메모리에 올라갈 만큼의 크기여야 한다.

각 파티션마다 local frequent pattern을 찾아야 한다. 단, local  sup<sub>min</sub>은 sup<sub>min</sub> / k이다. 각 파티션의 frequent pattern 즉, local frequent pattern은 local sup<sub>min</sub>보다 항상 같거나 크다. 이후에, DB scan을 하며 global한 frequent pattern을 만든다. local frequent pattern이더라도 global frequent pattern은 아닐 수 있기 때문이다. 이렇게 총 2회만 스캔을 하면 된다.

직관적으로 각 파티션에서 local supmin을 만족하지 못하면 frequent pattern이 될 수 없다는 것을 알 수 있다.

b. Sampling for frequent patterns

Simple sampling: DB에서 sampling해서 sampled DB(SDB)를 얻고 Apriori를 돌려서 local frequent patern을 찾는다. 이때, minSup은 sample만큼 나눠서 사용한다.

하지만 위의 simple sampling은 local frequent pattern이 실제로 frequent pattern이 아닐 수 있고 global frequent pattern을 놓쳤을 수 있는 문제가 있다.

이를 해결하기 위해 검증을 위한 2번의 스캔을 더 시행한다.
첫 번째 Scan할 때, S(SDB)와 NB(S에는 없지만 모든 부분집합이 S에 있는 것)에서 frequent itemset을 찾는다. 두 번째 scan에선 missed frequent pattern을 찾아준다.

c. DIC
같은 스캔에서 길이가 다른 itemsets가 후보로 들어있다.
예를 들어, A와 D가 frequent하다면, AD의 counting이 시작된다. BCD의 모든 길이 2짜리 subset이 frequent하다면 BCD의 counting이 시작된다.

**2. Huge number of candidates**

a. DHP

DB 스캔 한 번 할 때, k-itemsets의 support를 계산하는 동시에 (k+1)-itemsets를 위한 해시 테이블을 만든다. 해시 테이블의 각 row는 hash bucket을 의미하며 해시값이 같은 itemset끼리 같은 hash bucket에 위치하도록해서 개수를 세어주었다. 이때, hash bucket count가 minSup보다 작으면 frequent pattern에서 제외하므로 candidate를 줄이는데 매우 효과적이다.

### Bottleneck of Frequent-pattern mining
- DB 스캔을 여러 번 하는 것은 시간적 비용이 많이 발생
- 긴 패턴을 마이닝하는 것은 많은 스캔과 많은 후보 생성이 필요하다
- 결국 Bottleneck은 후보 생성과 검증이다

후보 생성을 안 할수는 없을까? 그렇게 나온 것이 FP-Growth이다.

### FP-Growth: Mining frequent patterns without candidate generation

FP tree를 기반으로 짧은 패턴에서 긴 패턴으로 길이를 늘려간다.
ex) abc가 frequent pattern이고 abc를 갖는 모든 트랜잭션은 DB|abc라고 표현한다. 만약 d가 DB|abc에서 local frequent item이라면 abcd 또한 frequent item이다.

먼저 DB를 스캔하고, frequent 1-itemset을 찾는다.(길이 1개짜리)

Frequent item의 frequency가 감소하는 순서대로 정렬한다. 이를 f-list라고 한다.

그 후 DB를 다시 스캔해서 FP-tree를 만든다. root는 {}로 비워두고, 각 트랜잭션마다 frequent item을 정렬해서 tree에 이어 붙인다. 이미 동일한 브랜치가 있으면 frequency를 증가시키고 없으면 브랜치를 새로 만들어준다.

Pattern을 나누어서 따져보자. F-list가 {f,c,a,b,m,p}라면 p를 포함하는 패턴, m을 포함하지만 p는 포함하지 않는 패턴, b를 포함하지만 m,p를 포함하지 않는 패턴, ..., 패턴 f까지!!

이후 각 아이템마다 conditional pattern base를 구한다. frequent item header table에서 p의 링크를 따라가고, p의 prefix path를 모두 이어서 p의 conditional pattern base 표를 만든다.

conditional pattern base 표로 conditional fp-tree를 만든다. p의 모든 conditional pattern base를 합쳐서 min sup이 넘는 item에 대해 p-conditional FP-tree를 만든다.

아래의 그림으로 이해해보자.

![FP tree](https://sundongkim-dev.github.io/assets/img/data_science/FP_tree.png)  

이러한 FP-tree 구조의 이점은 무엇일까?

Completeness와 Compactness이다.

Lossless하게 frequent pattern mining의 완전한 정보를 저장한다. 즉, 모든 frequent pattern을 포함한다.

빈도가 더 높은 아이템일수록 더 잘 공유되기 때문에(frequency descending order이기 때문) 불필요한 정보들이 중복되지 않는다. 그렇기 때문에 original DB보다 항상 작고, 일반적으로 1/10으로 압축된다고 한다.

### Summary of ideas with FP-Growth

새로운 frequent item을 더하면서 길이를 재귀적으로 늘려나간다.
Conditional pattern base와 conditional FP-tree를 만들고 이를 반복하여 FP-tree가 empty이거나 single path만을 포함할 때까지 진행한다.

### Why is FP-Growth the winner?

- Divide and conquer
- NO candidate generation and test
- NO repeated scans: just twice
- Basic operations: counting local frequent items and building a sub FP-tree, no pattern search and matching
