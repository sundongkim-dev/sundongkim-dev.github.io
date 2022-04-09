---
published: true
title: '[데이터 사이언스] Classification & Prediction'
layout: post
subtitle: 'csReview DataScience Classification Prediction'
categories: csReview
tags: DataScience
comments: true
---

### Chapter 6. Classification and Prediction
- What is classification & Prediction?
- Issues regarding classification and prediction
- Classification by decision tree induction
- Bayesian classification
- Rule-based classification
- Associative classification
- Lazy learners(or learning from your neighbors)
- Prediction
- Accuracy and error measures
- Ensemble methods
- Model selection
- Summary

---
### Classification vs. Prediction

**1. Classification**  
categorical class labels(discrete or nominal)를 예측한다. class label을 갖고 있는 트레이닝셋을 학습시켜 모델을 구성하고 이를 이용하여 새로운 데이터를 분류한다.

Classification은 두 가지 step으로 이루어져 있다.

1. Model Construction
  + 모델을 사용하여 알려지지 않은 표본을 분류
  + 훈련 데이터로 튜플/샘플의 속성이 클래스를 결정하는 방법을 설명
  + Classification rules, decision trees, networks or mathematical formulae

2. Accuracy Evaluation
  + 테스트 셋(트레이닝 데이터와 유사하게 클래스 라벨을 가진다)을 이용해서 모델의 정확도를 평가
  + 훈련 데이터와는 독립적이어야 과적합이 발생하지 않는다
  + 모델을 통해 나온 결과와 실제 클래스 라벨을 비교하여 정확도를 계산


**2. Prediction**  
연속적인 값을 가진 함수의 모델을 구성하고 이를 이용하여 모르거나 잃어버린 값을 예측한다.

credit approval, target marketing, medical diagnosis, fraud detection 등에 활용된다.


### Supervised vs. Unsupervised Learning

- Supervised Learning(classification): 트레이닝셋은 class label을 포함하며 이를 학습시켜 새로운 데이터를 분류한다.
- Unsupervised Learning(clustering): 트레이닝셋의 class label이 주어지지않고 데이터의 클러스터를 형성한다.

2. Prediction


### Issues regarding classification and prediction
**1. Issues**

a. Data Preparation  
- Data cleaing: noise나 missing value 처리
- Relevance analysis: feature selection
- Data transformation: generalize, normalize data

b. Evaluating Classification Methods  
- Accuracy
  + classifier accuracy: 클래스 라벨을 얼마나 잘 분류하는가
  + predictor accuracy: attribute의 값을 얼마나 정확히 예측하는가
- Speed
  + 모델 생성 시간(training time)
  + 실제 이용할 때 걸리는 시간(classification, prediction time)
- Robustness: 노이즈나 비어있는 값을 다루는 능력
- Scalability: 디스크에 있는 많은 데이터에 대한 효율성
- Interpretability: 뉴럴 네트워크는 어떻게 그러한 분류 결과가 나왔는지 이유를 잘 말해주지 못하므로 이 특성이 낮다. <-> XAI
- Decision tree size, compactness of classification rules 등

### Classification by decision tree induction
**1. Algorithm**  
- greedy algorithm으로 top-down, recursive, divide-and-conquer 방식으로 decision tree를 구성한다.
- 처음에 모든 트레이닝 샘플이 루트 노드에 있다.
- Attribute는 categorical 하다고 가정한다. 연속적인 값이라면 범위 나누어서 분할해야 한다.
- 샘플들은 정해진 test attributes에 따라 재귀적으로 나누어진다.

재귀가 멈추는 경우는?
- 해당 노드에서 '모든 샘플이 같은 클래스 라벨에 속하거나'
- '샘플을 나눌 수 있는 Attribute가 더 이상 존재하지 않는 경우 (더 많은 수의 클래스 라벨로 분류: Majority voting)'
- '샘플이 없는 경우'

2. Test Attribute Selection - Attribute Selection Measure
그룹을 나눌 때, 좀 더 클래스 라벨이 비슷한 것끼리(more homogeneous) 잘 나누는 Attribute를 선택한다.

### Attribute Selection Measure

**1. Information Gain**
- 가장 높은 information gain을 얻는 test attribute를 선택!!
- 엔트로피(expected information)  

> Info(D)=-sum(pi * log2(pi))  

모든 클래스 라벨마다 전체 튜플 중 그 클래스 라벨의 확률(pi)을 대입하여 값을 구한다. 더 다양할수록 큰 엔트로피 값을 갖는다.
