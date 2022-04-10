---
published: true
title: '[데이터 사이언스] Introduction'
layout: post
subtitle: 'csReview DataScience'
categories: csReview
tags: DataScience
comments: true
---

## Chapter 1: Introduction
- Motivation: Why data mining?
- What is data mining?
- Data Mining: On what kind of data?
- Data mining functionality
- Classification of data mining systems
- Top-10 most popular data mining algorithms
- Major issues in data mining

---

### Why data mining?

왜 데이터 마이닝을 하는가?

이제는 데이터가 1초마다 폭발적으로 증가하고 있다. 당장 youtube만 봐도 기가바이트 단위의 영상이 1초에 몇 개나 올라올 지 감도 잡히질 않는다.

결국 데이터의 수집이나 가용성이 중요해졌고 그에 따라 자동화된 데이터 수집 도구나, 데이터베이스 시스템, 웹 등 다양한 도구들이 생겼다. 이러한 데이터의 주요 출처는 비즈니스(웹, 이커머스, 거래, 주식 등), 과학(원격 감지, 생체 정보학, 과학적 시뮬레이션 등), 사회와 사람들(뉴스, 카메라, 유튜브) 등이 있다.

> We are drowning in data, but starving for knowledge!

매우 익숙한 말이다. 데이터에 빠져살지만 정작 중요한 지식은 얻지 못한다는 말이다. 그래서 데이터 마이닝을 하기 시작한 것이다.

### What is data mining?

그렇다면 데이터 마이닝은 무엇인가?

데이터 마이닝은 쉽게 말하면 데이터로 부터 지식이나 흥미로운 패턴을 발굴하는 것이다. 사소하지 않고, 숨겨져 있고, 이전에 알려지지 않은 동시에 잠재적으로 유용한 것을 흥미로운 것으로 정의할 수 있겠다.

하지만 데이터 마이닝 용어 자체는 약간 이름을 잘못 지었다고도 할 수 있다. 예를 들어 gold mining은 광산에서 금을 캐는 것인데 데이터 마이닝을 여기에 빗대면 데이터에서 데이터를 캐는 이상한 말이 된다. 물론 그 데이터가 유용한 데이터라는 것이 생략되었겠지만 knowledge mining이라고 했으면 더 와닿지 않았을까?

그래서 이런 데이터 마이닝의 다른 이름으로는 knowledge discovery in databases(KDD), knowledge extraction, data/pattern analysis, data archeology, data dredging, information harvesting, business intelligence 등이 있다. ~~적고 보니 뭐이리 많은지..~~

참고로, 간단한 search나 query processing 혹은 deductive expert systems 같은 경우를 데이터 마이닝이라고 하지는 않는다.

아래는 KDD의 프로세스이다.
![KDD process](https://sundongkim-dev.github.io/assets/img/data_science/KDD.png)  

아래는 business intelligence의 프로세스이다.
![Business intelligence](https://sundongkim-dev.github.io/assets/img/data_science/business_intelligence.png)  

데이터 마이닝은 여러 분야가 융합된 것이다. Database 기술, 통계학, 알고리즘, 패턴 인식, 머신 러닝 등 아주 다양한 분야가 관여한다.

전통적인 data analysis가 안되는 이유는?
- 어마무시한 양의 데이터
- 매우 높은 차원의 데이터
- 매우 복잡한 데이터
- 새롭고 정교한 어플리케이션

### Data Mining: Classification Schemes

일반적인 분류로는 Descriptive data mining(현재의 데이터가 어떤 상태인지를 요약, 기술)과 predictive data mining(현재의 데이터로 예측)으로 나눌 수 있고, 관점이 다르면 분류 또한 달라진다.
- Data 관점: 마이닝할 데이터의 종류
ex) 관계형, 데이터 웨어하우스, 트랜잭션, 스트림, 객체 지향/
관계형, 능동형, 공간형, 시계열, 텍스트, 멀티미디어,
이기종, 레거시, WWW
- knowledge 관점: 검색할 지식의 종류
ex) 특성화, 식별, 연관성, 분류, 클러스터링,
추세/경향, 특이치 분석 등
- Method 관점: 활용할 기법의 종류
ex) 데이터베이스 지향, 데이터 웨어하우스(OLAP), 머신 러닝, 통계,
시각화 등
- Application 관점: 적용된 어플리케이션의 종류
ex) 소매, 통신, 은행, 사기 분석, 바이오 데이터 마이닝, 주식
시장 분석, 텍스트 마이닝, 웹 마이닝 등

### Functionalities for data mining
- Multidimensional concept description: characterization & discrimination
ex) 건조한 지역 vs 습한 지역
- Frequent patterns, association, correlation vs causality
ex) 기저귀 → 맥주[0.5% 75%]
- Classification and Prediction: 설명하고 구별하는 모델(함수)을 구성
ex) (기후)에 따라 국가 분류 또는 (연비 기준)에 따라 자동차 분류, 알 수 없거나 누락된 숫자 값 예측
- Cluster analysis: 클래스 레이블을 알 수 없기에 데이터를 그룹화하여 새 클래스를 만든다, 클래스 내 유사성 극대화 및 클래스 간 유사성 최소화
- Outlier analysis
Outlier: 일반적인 틀을 준수하지 않는 데이터 object, Noise인가 exception인가? 부정 행위 탐지, 희귀 사건 분석에 유용
- Trend and evolution analysis
ex) 추세 및 진화 분석

### Top-10 most popular data mining algorithms
1. C4.5
2. K-Means
3. SVM
4. Apriori
5. EM
6. PageRank
7. AdaBoost
7. KNN
7. Naive Bayes
10. CART

### Major issues in data mining
- Mining methodology
- User interaction
- Applications and social impacts
