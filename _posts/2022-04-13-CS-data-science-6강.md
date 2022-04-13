---
published: false
title: '[데이터 사이언스] Classification & Prediction (2)'
layout: post
subtitle: 'csReview DataScience Classification Prediction'
categories: csReview
tags: DataScience
comments: true
---

### Chapter 6. Classification and Prediction
- Lazy learners(or learning from your neighbors)
- Prediction
- Accuracy and error measures
- Ensemble methods
- Model selection
- Summary

---
### Lazy vs. Eager learning

**1. Eager learning**  

앞서 다뤄왔던 방법들이 전부 eager learning에 해당한다. 훈련 데이터셋이 주어지고, 새로운 테스트 튜플을 받기 전에 분류 모델을 만들고 테스트 셋이 오면 바로 모델에 넣어 분류를 하는 방식이다. 그렇기 때문에 테스트 샘플들은 분류가 이뤄질뿐 모델에 어떠한 영향을 주지 않는다.

결과적으로 eager method는 전체 데이터를 다 다룰 수 있는 하나의 모델(hypothesis)을 만들어야 한다.

**2. Lazy learning**  

다른 말로 instance-based learning, lazy evaluation이라고도 한다. 훈련 데이터셋을 그냥 저장해두고 테스트 튜플이 주어질 때까지 기다린다. 그렇기에 학습할 때는 시간이 적게 걸리지만 예측할 때 더 많이 걸린다.

Lazy method는 많은 eager method와 달리 단일 가설을 사용하지 않고 더 많은 local linear function들을 이용함으로써 풍부한 hypothesis space를 사용한다.

예시로는 K-nearest neighbobr approach가 있다. KNN 알고리즘으로도 익숙한 그것이다.

### K-Nearest Neighbor Algorithm

모든 instance들(n 개의 attribute 소유)은 n차원 공간에 대응된다. 거리는 그 공간에서 정의된다. 그래서 테스트 샘플이 주어지면 거리가 가장 가까운 k개의 샘플을 가져오고 그 중에서 다수의 class label를 따라간다.


[그림]

위 그림에서 k는 5이고 X<sub>q</sub>의 class label은 -가 될 것이다.

### What is Prediction?

Numerical prediction은 classification과 비슷하다. 모델을 만들고 그 모델로 input의 continuous value를 예측하는 점에서 말이다. 그러나 classification하고는 다르다.

Classification은 categorical class label을 예측하는 반면 prediction은 continuous-valued function 모델을 이용하여 continuous space의 값을 예측하기 때문이다.

Prediction의 주요 방법 중 하나는 **regression**이다. Regression은 한 개 이상의 predictor variables(예측 변수, 독립 변수 등)와 response variable(종속 변수) 사이의 관계를 모델링하는 것이다.

### Regression analysis

**1. Linear regression**
1개의 독립변수 x와 종속변수 y로 선형함수를 이루는 선형 회귀이다.

> y = w<sub>0</sub> + w<sub>1</sub>x

트레이닝 데이터로 가장 잘 맞는 직선을 찾는 것이다. 즉 x의 계수와 w<sub>0</sub>을 찾아야 한다. 찾는 방법으로는 least square method가 있다. 최소제곱법인데 말 그대로 실제값과 함수값의 차이의 제곱이 최소가 되도록 하는 w<sub>0</sub>와 w<sub>1</sub>을 찾으면 된다.

[수식 그림]
>
w1=sum((xi-avg(x))x(yi-avg(y)))/sum((xi-avg(x))^2)
w0=avg(y)-w1xavg(x)

**2. Multiple linear regression**

Linear regression은 독립변수가 하나였지만 이제는 두 개 이상인 경우이다.
> X = <x1, x2, x3, ..., xn> : Predictor variables

만약 2차원의 data라면 함수는 아래와 같다.
> y = w<sub>0</sub> + w<sub>1</sub>x<sub>1</sub> + w<sub>2</sub>x<sub>2</sub>

이 역시 parameter들을 구해야 하는데, least square method를 확장한 방법이나 SAS, S-Plus와 같은 툴로 구할 수 있다.

**3. Non-linear regression**

항상 linear하게 대처하는 것은 아니다. 대체로 더 잘 맞는 nonlinear하게 해결하는 모델들도 있다. 어떤 nonlinear 모델들은 다항 함수로 나타낼 수 있다. 다항함수 regression model은 linear regression model로 바꿀 수 있다. 예를 들면,

> y = w<sub>0</sub> + w<sub>1</sub>x<sub>1</sub> + w<sub>2</sub>x<sup>2</sup> + w<sub>3</sub>x<sup>3</sup>

위와 같은 nonlinear한 식의 경우 x제곱과 x세제곱을 각각 x<sub>2</sub>, x<sub>3</sub>으로 치환해서 풀 수 있다.

**4. 다른 regression 방법들**
- Generalized linear model
- Poisson regression
- Log-linear models
- Regression trees
