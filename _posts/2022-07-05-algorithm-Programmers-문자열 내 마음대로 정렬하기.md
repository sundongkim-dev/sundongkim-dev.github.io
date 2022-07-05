---
published: true
title: '[프로그래머스] Level 1 - 문자열 내 마음대로 정렬하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 문자열 내 마음대로 정렬하기`](https://school.programmers.co.kr/learn/courses/30/lessons/12915)

---
## **문제 설명 및 풀이**

n번 째 글자를 기준으로 정렬하는 문제이다. c++스럽게 index를 따로 세어주다가 enumerate를 알게된 문제이다. enumerate는 원소와 index를 같이 가져와주는 고마운 존재이다.

혹은 lambda와 sorted를 통해 풀 수도 있다. sorted는 key를 정해주어서 그 값으로 정렬 기준을 정할 수 있다. key에 넣어주는 형태는 function으로 이 때, lambda를 활용해줄 수 있다.

key가 같다면 사전순으로 정렬해주어야하므로 정렬을 두 번해주면 된다.

---
### C++스러운 나의 코드
```python
def solution(strings, n):
    answer = []
    li = []
    strings.sort()
    for idx, i in enumerate(strings):
        li.append([i[n], idx])
    li.sort()
    for item in li:
        answer.append(strings[item[1]])

    return answer
```

### Pythonic한 풀이
```python
def solution(strings, n):
    return sorted(strings,  key=lambda x:(x[n],x))
```

```python
def solution(strings, n):
    return sorted(sorted(strings),  key=lambda x: x[n])
```
