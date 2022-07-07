---
published: true
title: '[프로그래머스] Level 1 - k번째수'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - k번째수`](https://school.programmers.co.kr/learn/courses/30/lessons/42748)

---
## **문제 설명 및 풀이**

인덱스 슬라이싱을 이용해서 문제 그대로 구현해주었다.

이를 한 줄만으로도 구현할 수 있다. lambda와 map을 사용해서 원하는 처리를 해주면 된다. 앞으로 이렇게 최대한 압축하려고 노력해보아야겠다.

만약, map을 사용하지 않으면 나처럼 for문을 일일이 리스트 원소에 접근하고 append하는 식의 번거로운 과정을 거쳐야 하지만, 모든 원소에 같은 함수를 적용한다면 아래와 같이 lambda와 map으로 쉽게 구해줄 수 있다.

map 객체는 보통 list로 형 변환해서 사용한다. ~~하나의 묶음으로 처리하고 받고 싶기 때문에 list를 주로 사용~~

---
### C++스러운 나의 코드
```python
def solution(array, commands):
    answer = []
    for i in commands:
        tmp = array
        new_arr = tmp[i[0]-1:i[1]]
        new_arr.sort()
        answer.append(new_arr[i[2]-1])

    return answer
```

### Pythonic한 풀이
```python
def solution(array, commands):
    return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```
