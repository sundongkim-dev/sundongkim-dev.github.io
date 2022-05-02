---
published: true
title: '[데이터 사이언스] Getting to know your data'
layout: post
subtitle: 'csReview DataScience Data'
categories: csReview
tags: DataScience
comments: true
---

### Chapter 2. Getting to know your data
- Data Objects and Attribute Types
- Basic Statistical Descriptions of Data
- Data visualization
- Measuring Data Similarity and Dissimilarity
- Summary

---

## Data Objects and Attribute Types  

### Types of Datasets.  
> 어떤 타입의 데이터셋이 있는지 알아야 전체 데이터를 잘 이해할 수 있다.  

- Record  
  - Attribute 값으로 이루어져 있는 row  
  - Relational records / Data matrix
    - Text documents: term-frequency vector
  - Transaction data  

- Graph and network   
  - Social or information networks  
  - World Wide Web  
  - Molecular Structures  

- Ordered  
  - Video data: sequence of images  
  - Temporal data: time-series  
  - Sequential data: transaction sequences  
  - Genetic sequence data  

- Spatial, Image and Multimedia  
  - Spatial data: maps  
  - Image data  
  - Video data  

### Important Characteristics of Data  

- Dimensionality  
  - Curse of dimensionality: dimension이 너무 커지면 발생하는 문제로, 차원이 작을 때는 잘 작동하다가 차원이 높아지면 잘 작동하지 않고 데이터도 많이 필요하게 된다(sparse matrix).  

- Sparsity  
  - 데이터가 많이 비어있는 상태(희소 행렬)
  - density가 낮으면(sparse하면) 데이터를 분석하기 어렵다.  

- Resolution  
  - Patterns depend on the scale

- Distribution  
  - centrality, dispersion  

### Data Objects  

- 데이터셋들은 데이터 오브젝트(실세계 객체)들로 이루어져 있다.  
  - Sales database: 고객, 아이템, 판매
  - Medical database: 환자, 치료
  - University database: 학생, 교수, 강의
- **Tuples**, **samples**, examples, instances, data points, objects라고도 한다.
- Data objects들은 Attribute들로 이루어져있다.    
- DB **rows** -> **data objects**
- DB **Columns** -> **attributes**


### Attributes & Attribute Types

특정 데이터 오브젝트를 설명하는 특성으로 dimensions, features, variables라고도 한다.

데이터 객체의 특성 또는 특징을 나타내는 data field이다. ex) customer _ID, name, address

- **Attribute Types**
  - **Nominal**: 카테고리, 상태, 어떤 것의 이름
    - 값이 유한하다.
      - ex) Hair_color={black, blond, brown, grey, red, white}  
    - 결혼 여부, 직업, 신분증 번호, 우편 번호 등이 nominal에 해당한다.

  - **Binary**: 2 가지 상태(0 또는 1)만 가지는 nominal attribute의 특별한 케이스  
    - Symmetric binary: 두 가지 값이 동등한 중요성을 갖는 경우 ex) gender  
    - Asymmetric binary: 동등하지 않은 경우 ex) medical test(양성 vs. 음성)
      - 중요한 결과에 1을 할당(HIV 양성이면 1, 음성이면 0)

  - **Ordinal**  
    - 값들이 중요한 순서를 갖고 있다. (Ranking)  
    - 연속된 값들이 얼마나 떨어져 있는 지 그 **Magnitude**를 알 수 없다.  
    - Size={small, medium, large}, Grades={A0, A+, B0, B+...}, Army rankings

  - **Numeric**  
    - Quantity(Integer or real-valued)
    - **Interval-scaled**   
      - 동등한 사이즈의 유닛들, 연속적인 두 값의 차이를 알 수 있음
      - Ordinal과 다르게 값에 순서가 있다. ex) 섭씨, 화씨 온도, 달력 날짜  
      - 진정한 의미의 zero-point가 존재하지 않는다. 0도는 온도가 없는 것이 아님을 예로 들 수 있다.   

    - **Ratio-scaled**
      - 진정한 zero-point가 존재한다.(없음을 의미하는 zero)
      - 임의의 값 사이에 규모가 얼마나 차이나는지 알 수 있다. ex) 6kg은 3kg의 두배
      - ex) 켈빈온도, 길이, 개수, 돈

    - Discrete vs Continuous Attributes  

      - **Discrete Attribute**  
        - 유한하고 셀 수 있는 값들, 가끔 정수 변수로 표현
          - 우편번호, 단어 수 등등  
        - Binary attribute는 discrete attributes의 특별한 케이스  

      - **Continuous Attribute**  
        - Attribute 값으로 실수값을 가진다. ex) 온도, 높이, 무게
        - 실제로, 실제 값은 한정된 자릿수를 사용해서만 측정되고 표현될 수 있다.
        - 연속형 속성은 일반적으로 부동 소수점 변수로 표현된다.

---
## Basic Statistical Descriptions of Data

데이터의 기본적인 통계에 대해 왜 알아야할까?

데이터를 잘 이해하기 위해, 즉 중심적인 경향을 알 수 있기 때문이다.  

데이터 분산의 특성으로는 median, max, min, quartiles, outliers, variance 등이 있다.

### Measuring the Central tendency  
- **Mean**(Algebraic measure)
  - Sample의 mean: (샘플인 x의 합) / (x의 개수)  
  - Population(전체)의 mean: (전체 x의 합)/(전체 x의 개수)
  - 전체 크기인 경우는 N, 샘플의 크기인 경우는 n으로 표기한다.  
    - **Weighted arithmetic mean**: 샘플마다 중요도를 반영한다.  
    - **Trimmed mean**: 너무 극단적인 값이 있다면 제외하고 계산한다. 적절한 기준을 설정하기 어려우므로 잘 사용하지 않는다.

Mean은 아웃라이어에 영향을 많이 받는다는 단점이 있어 Median이라는 척도가 생겼다.

- **Median**   
  - 홀수개의 데이터인 경우 가장 가운데 값, 짝수개의 데이터인 경우 가운데 두 값의 평균을 말한다.  
  - 새로운 값이 들어오면 정렬 후 구할 수 있기 때문에 data를 그룹화해서 interpolation으로 추정하는 방법 사용한다.
  - 처음에 구간을 나누고 도중에 새로운 데이터가 들어오면 그 데이터가 해당하는 구간의 frequency를 한 개 올려준다.
  - Median = L<sub>1</sub>(구간의 시작지점) + ((n/2-sum(이전 freq))/(median frequency))x width  

![Median](https://sundongkim-dev.github.io/assets/img/data_science/median.png)

위 식을 예로 적용해보자. 우선, 아래와 같이 데이터를 그룹화한다.
|age|frequency|
|:-:|:-------:|
|1-5|200|
|6-15|450|
|16-20|300|
|21-50|1500|
|51-80|700|
|81-110|44|

Median = 21 + ((1597-950)/(1500))x29 = 21 + 18763/1500  

- **Mode**  
  - 가장 데이터에서 많이 등장하는 값(최빈값)
  - 가장 빈도 높은 것 1(Unimodal), 2(Bimodal), 3(Trimodal)개 선택
  - Empirical formula  
    - 통계(경험)적으로 아래 식을 만족함  
    > mean-mode = 3 * (mean-median)  
      평균에서 최빈값 뺀 것은 평균에서 중앙값 뺀 것의 3배이다.  

- Symmetric vs. Skewed data  
위의 식에서 2개를 알고 있으면 나머지 하나를 예측할 수 있다.

![Symmetric vs. Skewed Data](https://sundongkim-dev.github.io/assets/img/data_science/Symmetric_Skewed_Data.png)

- Symmetric인 경우는 mean, median, mode 모두 같은 경우이다.
- Skewed인데 mean > median > mode인 경우, positively skewed이고 반대로 mode > median > mean인 경우, negatively skewed이다.  

### Measuring the Dispersion of Data  

- **Measurement**
  - **Quartiles**: Q<sub>1</sub>(25<sup>th</sup> percentile), Q<sub>3</sub>(75<sup>th</sup> percentile)를 의미하고 Q<sub>2</sub>(50<sup>th</sup> percentile = median) Q<sub>4</sub>(100<sup>th</sup> percentile = meaningless)
  - Inter-quartile range(IQR): IQR = Q<sub>3</sub>-Q<sub>1</sub>
  - Five number summary: min, Q<sub>1</sub>, median, Q<sub>3</sub>, max
  - Boxplot: graphical tool로, 사분위수, 중위수, 특이치 등 표시
  - Outlier: 주로 값이 1.5 x IQR보다 작거나 큰 값

  - **Variance and standard deviation**
    - Sample: s, Population: sigma
    - Sample(s)의 Variance(Algebraic, scalable computation): 편차 제곱의 평균인데 n이 아닌 n-1로 나눈다.
    - 전체 데이터(N)의 variance
    - Standard deviation: s또는 시그마는 variance의 루트

- **Boxplot Analysis**  
  - **Five-number summary**(minimum, Q1, median, Q3, Maximum)
  - **Boxplot**  
    - 데이터를 box로 표현한다.  
    - Box의 왼쪽 끝은 Q<sub>1</sub>, 오른쪽 끝은 Q<sub>3</sub>  
    - Median은 box안에 선으로 표기한다.  
    - Box 바깥은 선으로 연결하여 minimum, maximum까지 연결한다.  
    - Outliers: outlier threshold를 넘어간 곳에 점으로 표기한다.
  ![Boxplot Analysis](https://sundongkim-dev.github.io/assets/img/data_science/Boxplot.png)  

### Properties of Normal Distribution Curve  
- The normal (distribution) curve
  - 뮤: mean, 시그마: 표준편차
  - 뮤-시그마 to 뮤+시그마: 68%를 포함한다.  
  - 뮤-2시그마 to 뮤+2시그마: 95%를 포함한다.  
  - 뮤-3시그마 to 뮤+3시그마: 99.7%를 포함한다.  

---
## Data Visualization  

### Graphic Displays of Basic Statistical Descriptions

**1. Boxplot**  
5개의 숫자(min, Q<sub>1</sub>, median, Q<sub>3</sub>, max)를 시각적으로 보여줌.  

**2. Histogram**  
x축은 값, y축은 빈도를 나타내는 막대 형태의 그래프.  
- 막대는 서로 인접해있고 겹치지 않는다.  
- 각 범주에 속하는 사례의 비율을 보여준다.
- 카테고리는 일반적으로 일부 변수의 겹치지 않는 간격으로 지정된다.
- 카테고리(막대)는 인접해야 한다.
- 막대그래프와 차이  
  - 막대그래프는 높이가 그 값을 나타낸다.  
  - 히스토그램은 넓이가 그 값을 나타낸다.  
  - 각 막대가 서로 다른 너비를 가지면 중요한 차이를 보일 것!!  
- boxplots보다 더 많은 정보를 전달하기도 한다.  
  - min, Q<sub>1</sub>, median, Q<sub>3</sub>, max값이 모두 같아도 median쪽에 frequency가 더 많아도 되고 그 주변에 대칭으로 많아도 되기 때문에 boxplot 자체는 완전히 같지만 데이터 분포는 달라진다.  

**3. Quantile plot**
x값과 f를 한 쌍으로 표기하는 방식으로 이때 f는 100 f<sub>i</sub>%는 <= x<sub>i</sub>이라는 것을 의미한다.
**4. Quantile-quantile(q-q) plot**
한 분포의 quantiles와 이에 대응하는 다른 분포의 quantiles를 표기한다.
**5. Scatter plot**
각 값 쌍은 한 쌍의 좌표이며 평면에 점으로 표현된다.
