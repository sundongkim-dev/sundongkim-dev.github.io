---
published: true
title: '[프로그래머스] Level 1 - 가운데 글자 가져오기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 가운데 글자 가져오기`](https://school.programmers.co.kr/learn/courses/30/lessons/12903)

---
## **문제 설명 및 풀이**

하나만 알고 둘은 모르나보다. 가운데 글자를 가져오는 것이라 당연히 홀수, 짝수 길이를 나누어서 출력해야겠다라고 생각했다.

어차피 몫 연산을 사용할거라면 미리 1을 빼주어서 전처리 해준다면 굳이 분기를 사용할 이유가 없다. 이미 아는 사실에도 그냥 후다닥 푸는 경향이 있어 또 놓친 것 같다.

---
### C++스러운 나의 코드
```python
def solution(s):
    answer = ''
    if len(s) % 2 == 0:
        answer = s[len(s)//2 -1 : len(s)//2+1]
    else:
        answer = s[len(s)//2]
    return answer
```

### Pythonic한 풀이
```python
def solution(str):
    return str[(len(str)-1)//2:len(str)//2+1]
```
