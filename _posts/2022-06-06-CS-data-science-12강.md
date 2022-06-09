---
published: true
title: '[데이터 사이언스] Social Network Analysis'
layout: post
subtitle: 'csReview DataScience Data'
categories: csReview
tags: DataScience
comments: true
---

### Chapter 9. Social Network Analysis
- Social Network Introduction
- Social Network Generation
- Mining on Social Network

---

Individual을 node로, social relationship을 link로 표현할 수 있다. Social network란 많은 개인들이 서로 다양한 사회적 상호작용을 하는 것을 말한다.

Social network의 예로, communication network를 말할 수 있는데 이는 많은 non-identical한 components(컴퓨터, 라우터, 위성 등)들이 다양한 연결(전화선, tv선, 통신선 등)을 서로 하고 있는 것을 말한다.

### Some Interesting Quantities
- Connected components: 얼마나 많고, 얼마나 큰가?
- Network diameter: 가장 먼 두 노드의 shortest path는? 그 edge의 수는?
- Clustering: 어느 정도로 cluster가 local하게 연결되어 있는가? long-distance connection은 얼마나 있는가?
- Degree distribution: 노드가 평균적으로 갖고 있는 edge의 수는?

일반적인 network는

- A few connected components(어떤 path로 웬만하면 노드끼리 도달 가능하다)
- Small diameter(약 6단계 정도로 매우 작고 logarithmical하게 증가한다)
- High degree of clustering(local하게 잘 묶인다)
- Heavy-tailed degree distribution(Edge가 많은 노드가 꽤 존재한다)

의 모습을 보인다.

### Models of Social Network Generation

**1. Random Graphs**: 전체 노드들 중에서 랜덤하게 edge가 생성되어 모델이 만들어진다는 말이다.  
**2. Scale-free Networks**: Power law 분포를 따르는 모델

WWW 문서들을 노드라고 하고 하이퍼링크를 링크라고 했을 때 8억 개의 documents를 조사하였더니 그 결과는 power law 분포를 따랐다. ~~예상은 normal distribution이었지만..~~
결과적으로 WWW는 scale-free network이다.

Scale-free network 모델에서는 노드의 수가 고정되어 있다고 가정하지 않고 지속적으로 확장된다고 가정한다. 또 attachment가 uniform하지 않다고 가정한다. in-link에 비례해서 link가 생긴다고 생각하기 때문이다. 이러한 두 가지 특성이 scale free network를 만든다고 한다.

- Hyperlinks on the web
- Internet backbone
- Actor connectivity
- Science Citation Index

### Robustness of Random vs. Scale-Free Networks

Random network를 랜덤하게 공격할 경우 혹은 failure가 발생할 경우 전체 네트워크가 끊어질 가능성이 높지만 scale-free network는 그렇지 않다. 반면, 랜덤하게 공격하지 않고 hub를 집중적으로 공격하거나, hub에서 failure가 발생할 경우 scale-free network 또한 네트워크가 끊어질 가능성이 높다. 결과적으로 hub를 잘 지켜야 네트워크를 잘 지킬 수 있다.

### Information on the Social Network

서로 다르고, 다양한 관계를 갖는 데이터가 그래프 또는 네트워크로 표현된다.

노드는 object이고 각기 다른 종류의 object를 가질 수 있으며, object들은 attribute들을 가지며, label 또는 class가 있을 수 있다.

Edge들은 link이며 다른 종류의 link를 가질 수 있으며, 역시 attribute들을 갖는다. 또한, link들은 방향이 지정될 수 있으며 binary일 필요(weight이 있을 수 있음)는 없다.

Link들은 object간의 관계나 상호작용을 표현한다. 이러한 것들은 mining을 더욱 풍부하게 만든다.

### What is New for Link Mining Here

기존의 머신러닝 및 데이터 마이닝은 하나의 관계에서 얻은 같은 종류의 객체들을 대상으로 했었다. 그러나, 실제 세계의 데이터셋은 다중 관계, 서로 다른 종류, semi-structured(like webpage, 형태가 딱히 정해져 있지 않음) 등으로 구성되어 있다. 이 때문에, Link mining과 social network analysis는 새롭게 부상하는 연구 분야가 되었다.

### A Taxonomy of Common Link Mining Tasks

- Object-Related Tasks
  + Link-based object ranking
  + Link-based object classification
  + Object clustering (group detection)
- Link-Related Tasks
  + Link prediction
- Graph-Related Tasks
  + Subgraph discovery
  + Graph classification
  + Generative model for graphs

### What is a link in link mining?

링크란 데이터 간의 관계로 link를 가지는 network에는 두 가지 종류가 있다. Homogeneous와 heterogeneous로 나눌 수 있는데, Homogeneous는 단일 object type과 단일 link type을 갖으며, 단일 모델이다. 예로 친구 네트워크(사람과 친구관계만 있음)나 linked Web page들의 집합인 WWW를 들 수 있다.

Heterogeneous는 다중 object type과 link type을 갖으며, 예로 medical network(환자, 의사, 질병, 치료)나 bibliographic network(출판물, 저자, 발표 장소)을 들 수 있다.

### Link-Based Object Ranking(LBR)

LBR은 그래프의 링크 구조를 잘 분석하여 그래프 내의 object 집합의 순서를 중요도에 따라 지정하거나 우선순위를 지정하는 것이다. 이를 통해 단일 object type과 단일 link type을 갖는 그래프에 집중하는 것이다. 예로, web Information analysis를 들 수 있는데, HITS나 PageRank가 전형적인 LBR 접근 방식이다.

### HITS: Capturing Authorities & Hubs

하이퍼링크는 일종의 참조를 말하는데, 많은 페이지들에 의해 참조되는 페이지를 "good Authorities"라고 하며, 많은 페이지들을 가리키는 페이지를 "good hubs"라고 한다.

HITS의 key idea는 "good Authorities"는 "good hubs"들이 가리킬 것이고, "good hubs"는 "good Authorities"들을 가리킬 것이라는 것이다. 즉 서로 어떤 게 더 좋은 hub이고 authority인지를 비교하여 알 수 있다.

각 페이지(d<sub>i</sub>)는 두 가지 score를 갖는다. Hub score(=h(d<sub>i</sub>))와 Authority score(=a(d<sub>i</sub>))이다.

Hub score는 해당 페이지의 out-link neighbor들의 authority score들의 합이고, authority score는 반대로 해당 페이지의 in-link neighbor들의 hub score들의 합이다.

### PageRank: Capturing Page Popularity

자주 인용되는 페이지는 일반적으로 더 중요하다고 볼 수 있다. PageRank는 기본적으로 citation counting이지만 그저 counting하는 것 이상의 효과를 보인다. "Indirect citations"를 고려하는데 이는 많이 인용된 paper가 인용하는 것은 더 큰 의미가 있다는 것을 뜻한다. 또한, 모든 page의 인용 횟수가 0이 아닌 것으로 가정한다.

결과적으로, pageRank는 "random surfing"으로 해석될 수 있다.







###
