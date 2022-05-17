---
published: true
title: '[데이터 사이언스] Cluster Analysis'
layout: post
subtitle: 'csReview DataScience Data'
categories: csReview
tags: DataScience
comments: true
---

### Chapter 2. Getting to know your data
- What is Cluster Analysis?
- Types of Data in Cluster Analysis
- A categorization of Major Clustering
- Partitioning Methods
- Hierarchical Methods
- Density-Based Methods
- Outlier Analysis

---

## What is Cluster Analysis?

Cluster Analysis는 무엇일까? 먼저 cluster가 뭔지 살펴보자. Cluster란 군집이라고도 하는데, 결국 data object들의 모임을 말한다. 같은 cluster 안에 있으면 서로 비슷한 것을 뜻하며 반대로 서로 다른 cluster라면 비슷하지 않은 것이다.

이러한 cluster를 분석한다는 것은 즉, 데이터의 특성을 바탕으로 데이터 간의 유사도를 구하는 것이다. 유사도를 구해서 비슷한 data object들끼리 묶어주기 위함이다.

Cluster analysis는 unsupervised learning의 한 종류로 학습 시 데이터에 정의된 클래스가 없다. 이는 데이터 분포에 대한 insight를 얻을 수 있는 stand-alone tool이며 다른 알고리즘을 위한 전처리 과정에 해당된다.

사용 예시로는 Spatial Data analysis, Economic Science(like market research), WWW(Cluster documents, weblog data), Image processing & pattern recognition 등이 있다. 이외에도 marketing, land use, insurance, city-planning이 있다.

---
## Quality and Requirements of Clustering

"Good" clustering method로는 높은 quality의 cluster를 제공하는데, 서로 다른 클래스 간에 낮은 유사도 혹은 하나의 클래스 안에서 높은 유사도를 보이는 것을 말한다.

결국 clustering의 결과의 quality는 **similarity measure**와 **method**로 결정된다. Clustering method의 quality는 숨겨진 패턴을 발견하는 능력에 의해 결정된다.

Similarity measure는 similarity와 Dissimilarity metric을 알아야 한다. Similarity는 distance function으로 d(i,j)로 표현하곤 한다. 변수 타입(interval-scaled, boolean, categorical, ordinal ratio, vector variables)에 다라 다르고 충분히 유사하다 혹은 충분히 좋다를 정의하기란 매우 주관적이다. 가중치는 attribute마다 다른 가중치를 가져야 한다.

Data mining에서 clustering의 **Requirements**는 아래와 같은 것들이 있다.
- 서로 다른 타입의 attribute들을 처리할 수 있어야 한다.
- 새로운 데이터가 추가될 때마다 잘 처리할 수 있어야 한다.
- 임의의 모양의 cluster를 발견한다.
- 파라미터를 정하는 것은 힘들기 때문에 최소의 파라미터 개수를 필요로 해야 한다.(???)
- Noise와 outlier를 처리할 수 있어야 한다.
- 입력 순서와 상관없이 동일한 결과를 출력해야 한다.
- 높은 차원을 갖는 attribute를 처리할 수 있어야 한다.(???)
- Scalability
- Incorporation of user-specified constraints

## A Categorization of Major Clustering Methods  

### 1. Major Clustering Approaches  

- Paritioning approach  
  - 다양한 파티션을 구성하고 몇 가지 기준에 따라 평가한다.   
  - Typical methods: k-means, k-medoids, CLARANS  

- Hierarchical approach  
  - 어떤 기준으로 계층적으로 데이터를 분리한다.   
  - Typical methods: Diana, Agnes, BIRCH, ROCK, CHAMELEON    

- Density-based approach  
  - 밀도함수를 기반으로 클러스터를 형성한다.   
  - Typical methods: DBSCAN, OPTICS    

### 2. Centroid, Radius, and Diameter of a cluster  

클러스터 내에서 centroid, radius, diameter의 정의!!

- Centroid: 클러스터의 중간 지점
  - 각 애트리뷰트 값 끼리 더해서 평균을 구한다.  
  - i: i th object, p: p th attribute라면, 아래와 같다.  
  ![Centroid](https://sundongkim-dev.github.io/assets/img/data_science/centroid.png)

- Radius: cluster의 모든 object에서 centroid까지 거리 제곱의 평균의 루트값  
  ![Radius](https://sundongkim-dev.github.io/assets/img/data_science/radius.png)

- Diameter: 모든 오브젝트 페어들의 거리 제곱의 평균의 루트값  
  ![Diameter](https://sundongkim-dev.github.io/assets/img/data_science/diameter.png)

클러스타 간의 거리를 계산하는 일반적인 대안으로 여러 가지 방식이 있다.
1. Single link: 한 클러스터의 원소와 다른 클러스터의 원소 사이의 최소 거리  
    - dis(K<sub>i</sub>, K<sub>j</sub>) = min(t<sub>ip</sub>, t<sub>jq</sub>)  

2. Complete link: 한 클러스터의 원소와 다른 클러스터의 원소 사이의 최대 거리  
    - dis(K<sub>i</sub>, K<sub>j</sub>) = max(t<sub>ip</sub>, t<sub>jq</sub>)

3. Average: 한 클러스터와 다른 클러스터 각각에서 원소를 하나씩 뽑은 모든 페어에 대해서 거리를 구한 후 평균을 구한 것  
  - dis(K<sub>i</sub>, K<sub>j</sub>) = avg(t<sub>ip</sub>, t<sub>jq</sub>)

4. Centroid: 두 클러스터의 centroid 사이의 거리!  
  - centroid는 실제 object가 아니라 위치를 나타낸다.
  - dis(K<sub>i</sub>, K<sub>j</sub>) = dis(C<sub>i</sub>, C<sub>j</sub>)

5. Medoid: 두 클러스터의 medoid 사이의 거리!  
  - dis(K<sub>i</sub>, K<sub>j</sub>)=dis(M<sub>i</sub>, M<sub>j</sub>)  
  - Medoid: 클러스터에서 가장 가운데에 위치한 실제 object   

## Partitioning Methods  

### 1. Basic Concept  

- Database D에서 n개의 objects를 k개의 클러스터로 나누는 것으로 클러스터를 대표하는 값과 그 클러스터의 모든 objects 까지 거리의 제곱의 합이 최소가 되도록 한다.   
![Partitioning method](https://sundongkim-dev.github.io/assets/img/data_science/partitioning_method.png)
- 모든 파티션을 다 살펴보면 global optimal을 찾을 수 있겠지만 heuristic methods를 사용한다.   
  - K-means: 각 cluster는 cluster의 centroid로 표현된다.
  - K-medoids or PAM(Partition around medoids): 각 cluster는 cluster의 object 중 하나로 표현된다.  


### 2. The K-Means Clustering Method  

K값이 주어졌을 때 다음과 같이 진행된다.
- objects를 임의로 k 부분으로 나눈다.  
- k 부분으로 나눠진 각 클러스터에 대해서 centroid(center로 cluster의 mean point) 값을 계산한다.                                                   
- 각 objects를 가장 가까운 seed point(centroid)의 클러스터로 다시 포함시킨다.  
- 다시 centroid값을 계산으로 돌아가는 과정을 반복하여 클러스터가 바뀌지 않을 때까지 진행한다.  

K-means는 상대적으로 효율적이다. 시간복잡도가 O(n*k*t)이다. n은 object의 수이며 k는 cluster의 수이고 t는 반복 횟수이다. 일반적으로 n이 다른 두 수보다 매우 크다. PAM(=O(k*(n-k)<sup>2</sup>)), CLARA(O(ks<sup>2</sup>+k(n-k)))와 비교해보면 상대적으로 효율적임을 알 수 있다.

하지만 종종 local optimum으로 빠진다는 문제가 있다. 또한 categorical data인 경우는 적용할 수 없다. Mean을 define할 수 있어야하기 때문이다. 결과적으로 numerical attribute와 같은 타입에 적용 가능하다. 또한 사전에 k 값을 정해주어야 하는데 까다로울 수 있으며 noise와 outlier를 잘 처리하지 못한다는 단점이 있다. Non-convex shape일 때 cluster를 발견하는 것은 적절하지 않다.

이러한 K-Means method의 변형으로 2 가지가 있다. 앞서 categorical data를 처리하지 못하니까 이를 해결하고자 k-modes가 나왔다. Centroid 대신에 modes(최빈값)을 사용한다.
- X, Y: m 개의 categorical attribute를 갖는 object들
- Dissimilarity d(X, Y): # of total mismatches
- Mode는 해당 object와의 mismatch 수의 합이 가장 작은 벡터이다.
- Attribute마다 가장 자주 발생하는 object가 차지하는 값을 가져온다.
- frequency-based method을 사용하여 cluster의 mode를 갱신한다.

일반적으로 데이터는 categorical과 numerical data가 섞여있으므로 k-prototype method를 사용한다.

K-Means method의 문제점으로 outlier에 너무 민감한 점을 꼽을 수 있다. Outlier 때문에 클러스터가 잘못 분리하여 왜곡할 수 있다.

이 때문에 K-Medoids라는 방식이 나왔는데, cluster 내 object의 평균값(centroid)을 기준점으로 삼는 대신에 cluster 내 가장 중앙에 위치한 object(medoid)를 사용할 수 있다.


---
## Hierarchical Methods

---
## Density-Based Methods

---
## Outlier Analysis
