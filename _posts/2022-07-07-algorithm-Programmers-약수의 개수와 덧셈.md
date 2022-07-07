---
published: true
title: '[프로그래머스] Level 1 - 약수의 개수와 덧셈'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 약수의 개수와 덧셈`](https://school.programmers.co.kr/learn/courses/30/lessons/77884)

---
## **문제 설명 및 풀이**

바보같이 약수의 개수를 구해주는 함수로 구해주었다.

사실 해당 약수의 개수가 무엇인지가 중요한 게 아니라 홀수인지 짝수인지만 알면 되기 때문에 더 쉽게 풀 수 있다.

약수의 개수가 홀수이면 제곱꼴을 갖는 수로 1, 4, 9, 16...의 꼴을 갖는다. 결과적으로, 아래와 같이 풀 수 있다.

---
### 나의 코드
```python
def countNum(num):
    res = 0
    for i in range(1, int(num**0.5)+1):
        if num%i == 0:
            res += 1
    if int(num**0.5) == num**0.5:
        res = (res-1)*2 + 1
    else:
        res = res * 2
    return res

def solution(left, right):
    answer = 0
    for i in range(left, right+1):
        if countNum(i) % 2 == 0:
            answer += i
        else:
            answer -= i
    return answer
```

### Pythonic한 풀이
```python
def solution(left, right):
    answer = 0
    for i in range(left,right+1):
        if int(i**0.5)==i**0.5:
            answer -= i
        else:
            answer += i
    return answer
```
