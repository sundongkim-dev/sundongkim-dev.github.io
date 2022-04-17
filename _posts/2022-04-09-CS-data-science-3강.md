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

---

### Improving Apriori algorithm

**1. Multiple DB Scans**

**a. Partition: Scan Database only twice**

이전에 apriori의 단점으로 너무 많은 DB scan을 한다는 점이 있었다. 이를 개선하기 위해 DB를 k 개의 조각으로 나눈다. 이를 partition이라고 하고, 각 **partition은 메인 메모리에 올라갈 만큼의 크기**여야 한다.

각 파티션마다 **local frequent pattern**을 찾아야 한다.

단, local sup<sub>min</sub>은 **sup<sub>min</sub> / k**이다.

왜 그럴까?

예를 들어, minimum support가 100이고 4 개의 파티션으로 나눴다면 local minimum support가 25 이상인 것을 후보로 가져와야 한다. 이는 당연한 논리인 것이 minimum support를 만족하려면 어느 한 파티션에서라도 해당 패턴의 local support가 25 이상인 부분이 있을 것이다. 이 때의 패턴을 **local frequent pattern**이라고 한다. 하지만 local frequent pattern이라고 해서 global frequent pattern일까?

아니다!!!! 위의 예시를 이어서 설명해보면 하나의 파티션에서 25번 나왔다면 후보로 채택될텐데 다른 파티션에서 각각 24번씩 나왔다면 97(=25+24+24+24)번으로 minimum support인 100을 만족하지 않기 때문이다.

그렇기 때문에 DB scan을 하며 global한 frequent pattern을 만든다. 이렇게 총 2회만 스캔을 하면 된다. 위와 같은 방식을 적용하면, **frequent patteern을 놓칠 리는 만무하다.**

**b. Sampling for frequent patterns**

Simple sampling: DB에서 sampling해서 sampled DB(SDB)를 얻고 Apriori를 돌려서 local frequent patern을 찾는다. 이때, minSup은 sample만큼 나눠서 사용한다. 위에서 배운 파티션처럼 메모리의 올라올 수 있는 양이어야 한다. 그래야 부가적인 DB scan이 없을 것이기 때문이다.

하지만 위의 simple sampling은 **local frequent pattern이 실제로 frequent pattern이 아닐 수 있고 global frequent pattern을 놓쳤을 수 있는 문제**가 있다.
~~가짜를 진짜로 오인할 수 있고 진짜를 놓칠 수 있다!!~~

이를 해결하기 위해 검증을 위한 2번의 스캔을 더 시행한다.
샘플링해서 나온 결과를 frequent pattern이라고 생각하지 말고 candidate라고 생각하고 접근하자. 그 candidate 집합을 S라고 하자면, 그 S를 진짜 frequent한 지 아닌지를 확인해야 한다.

근데 이때, S에서 발견된 pattern뿐만 아니라 그들에 대한 negative borders를 마찬가지로 확인해주어야 한다. S의 Negative borders는 S에는 없지만 모든 부분집합이 S에 있는 것을 말한다.

결과적으로 첫 번째 Scan할 때, S(SDB)와 NB(S에는 없지만 모든 부분집합이 S에 있는 것)에서 frequent itemset을 찾는다. 두 번째 scan에선 missed frequent pattern을 찾아준다. NB에서 frequent itemset이 나와 S와 조합해서 frequent pattern을 이룰 가능성이 있기 때문에 그들을 찾아주는 것이다.

**c. DIC(Dynamic Item Counting)**

같은 스캔에서 길이가 다른 itemsets가 후보로 들어있다.
예를 들어, A와 D가 frequent하다는 것을 알게된 시점에서, 그 즉시 AD의 counting이 시작된다. 또는 BCD의 모든 길이 2짜리 subset이 frequent하다면 BCD의 counting이 시작된다.

결과적으로 알게 된 시점에서 scan이 시작되므로 다른 것을 scan하는 시점에 병렬적으로 새로운 패턴에 대해 scan이 이뤄지므로 scan의 overlap이 생겨서 그 횟수를 많이 줄일 수 있게 된다.

**2. Huge number of candidates**

**a. DHP: Reduce the Number of Candidates**

1만 개의 itemset이 있다면 1-itemset의 후보는 10000개이고 모두 frequent하다면 2-itemset의 후보는 10000*10000인 1억 개가 될 것이다. 하지만 아이템이 1만 개인 상황은 결코 아이템이 많은 상황이 아니다. 몇십만 개의 아이템이 일반적인 경우일 텐데 그러면 벌써 100억이 넘고 시작하는 것이다. 이러한 후보의 수를 어떻게 줄일 수 있을까?

> 해싱을 사용한다!! Itemset이 key인 해시 테이블 이용!!

DB 스캔 한 번 할 때, k-itemsets의 support를 계산하는 **동시**에 (k+1)-itemsets를 위한 **해시 테이블**을 만든다. 해시 테이블의 각 row는 hash bucket을 의미하며 해시값이 같은 itemset끼리 같은 hash bucket에 위치하도록해서 개수를 세어주었다. 이 때, 개수는 해당 hash bucket에 위치하는 itemset의 count의 합이다.

즉, 해당 hash bucket의 아이템셋의 count를 다 합쳤음에도 minSup보다 작다는 것은 결코 frequent pattern일 수 없기 때문에 제외한다.

결과적으로 hash bucket count가 minSup보다 작으면 frequent pattern에서 제외하므로 candidate를 줄이는데 매우 효과적이다. 특히 2개짜리 frequent itemset을 만드는데 매우 효과적이다.

cf) 보통 hash function bucket #는 h({x y}) = ((order of x)*10 + (order of y)) mod 7로 결정된다.

---

### Bottleneck of Frequent-pattern mining

- DB 스캔을 여러 번 하는 것은 시간적 비용이 많이 발생
- 긴 패턴을 마이닝하는 것은 그 길이만큼 많은 스캔과 많은 후보 생성(2<sup>n</sup>-1 개)이 필요하다
- 결국 Bottleneck은 후보 생성과 검증(수많은 스캔 요구)이다

후보 생성을 안 할수는 없을까? 그렇게 나온 것이 FP-Growth이다.

---

### FP-Growth: Mining frequent patterns without candidate generation

**FP tree**를 기반으로 **짧은 패턴에서 긴 패턴으로** 길이를 늘려간다.

만약 abc가 frequent pattern이고 abc를 갖는 모든 트랜잭션은 DB|abc라고 표현한다.
만약 d가 DB|abc에서 **local frequent item**이라면 abcd 또한 frequent item이다.
찾는 순서는 아래와 같다.

1. 먼저 DB를 스캔하고, frequent 1-itemset을 찾는다.(길이 1개짜리)
2. Frequent item의 frequency가 감소하는 순서대로 정렬한다. 이를 f-list라고 한다. 각 트랜잭션 DB를 frquency descending order로 frquent한 것만을 남긴다. 이렇게 불필요한 정보를 지우고 frequent한 것들만을 남기기 위해 sccan을 하게 된다.
3. 그 후 DB를 다시 스캔해서 FP-tree를 만든다. root는 {}로 비워두고, 각 트랜잭션마다 frequent item을 정렬해서 tree에 이어 붙인다. 이미 동일한 브랜치가 있으면 frequency를 증가시키고 없으면 브랜치를 새로 만들어준다.

cf) Header table을 만들어주어야 하는데, 앞서 구한 f-list를 통해서 만들어준다. 초기에는 frequency를 0으로 초기화해서 만들어준다. 그 후 frequent한 것들만을 남긴 트랜잭션 DB를 돌면서 트리를 성장시킨다. head 포인터도 링크드 리스트로 엮어준다.

결과적으로 FP tree라는 것은 트랜잭션 DB의 아주 compact한 representation이다. 필요한 정보를 다 담고 있으며, descending order를 이용하여 빈번할수록 많이 share하므로 메모리를 많이 아낄 수 있다.

Pattern을 나누어서 따져보자. F-list가 {f,c,a,b,m,p}라면 제일 밑에서부터 p를 포함하는 패턴, m을 포함하지만 p는 포함하지 않는 패턴, b를 포함하지만 m,p를 포함하지 않는 패턴, ..., 패턴 f까지!! 총 6 덩어리의 disjoint한 partition 획득!!

이후 각 아이템마다 conditional pattern base를 구한다. frequent item header table에서 p의 링크를 따라가고, p의 prefix path를 모두 이어서 p의 conditional pattern base 표를 만든다.

conditional pattern base 표로 conditional fp-tree를 만든다. p의 모든 conditional pattern base를 합쳐서 min sup이 넘는 item에 대해 p-conditional FP-tree를 만든다.

아래의 그림으로 이해해보자.

![FP tree](https://sundongkim-dev.github.io/assets/img/data_science/FP_tree.png)  

이러한 FP-tree 구조의 이점은 무엇일까?

**Completeness**와 **Compactness**이다.

Lossless하게 **frequent pattern mining의 완전한 정보**를 저장한다. 즉, 모든 frequent pattern을 포함한다. 또한 긴 패턴을 자르지 않고 fp-tree의 형태로 저장하기 때문에 complete하다.

불필요한 정보들을 지워주었고, 빈도가 더 높은 아이템일수록 더 잘 공유되기 때문에(frequency descending order이기 때문) 불필요한 정보들이 중복되지 않는다. 그렇기 때문에 original DB보다 항상 작고, Connect-4 DB같은 것은 1/100으로 압축된다고 한다. 이렇게 작게 압축하면 메인 메모리에 한번에 올릴 수 있다는 이점이 있고 이를 통해 disk i/o cost를 확 낮출 수 있게 되는 것이다.

---

### A Special Case: Single Prefix Path in FP-tree

FP-tree T가 single prefix-path p를 갖는다면, 두 부분으로 나누어서 계산하는 것이 빠르다. 그렇게 하지 않는다면 재귀적 호출로 인한 Stack operation이 더디기 때문이다. 결과적으로 single prefix path를 떼어서 하나의 노드로 만들어서(조합 연산으로 모든 frequent pattern 구해줌) 아래 분기 되는 지점의 노드와 concatenation을 해주면 된다.

### Summary of ideas with FP-Growth

새로운 frequent item을 더하면서 길이를 재귀적으로 늘려나간다. 각 frequent item마다 conditional pattern-base를 만들고 그의 conditional FP-tree를 만들어준다. 그 안에서 또 conditional pattern-base를 만드는 식으로 계속 반복한다.  
Conditional pattern base와 conditional FP-tree를 만들고 이를 반복하여 FP-tree가 empty이거나 single path만을 포함할 때까지 진행한다.

### FP-Growth vs. Apriori: Scalability with the support threshold

Minimum support가 작다면 그만큼 apriori가 생성할 후보의 수가 많기 때문에 fp-growth가 훨씬 빠르지만 크다면 생성할 후보의 수가 작아져서 결과적으로 속도가 비슷해진다.

### Why is FP-Growth the winner?

- Divide and conquer
- NO candidate generation and test
- NO repeated scans: just twice
- Compressed DB: FP-tree structure
- Basic operations: counting local frequent items and building a sub FP-tree, no pattern search and matching
