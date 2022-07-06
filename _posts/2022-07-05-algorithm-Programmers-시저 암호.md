---
published: true
title: '[프로그래머스] Level 1 - 시저 암호'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 시저 암호`](https://school.programmers.co.kr/learn/courses/30/lessons/12926)

---
## **문제 설명 및 풀이**

For문에서 index와 원소가 동시에 필요한 경우, enumerate를 활용하면 간단하게 코딩할 수 있다.

아스키 코드를 이용하여 풀 수도 있지만 미리 문자열을 만들어 놓고 인덱스를 통해 가져오는 식으로 풀었다.

ord는 아스키 코드로, chr은 해당 코드에 맞는 문자로 바꾸어주는 함수이다.

---
### C++스러운 나의 코드
```python
def solution(s, n):
    answer = ''
    low = 'abcdefghijklmnopqrstuvwxyz'
    upp = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

    for idx, i in enumerate(s):
        if i.isupper():
            pos = upp.index(i)
            answer += upp[(pos+n)%26]
        elif i.islower():
            pos = low.index(i)
            answer += low[(pos+n)%26]
        else:
            answer += i

    return answer
```

### 아스키 코드를 이용한 풀이
```python
def solution(s, n):
    s = list(s)
    for i in range(len(s)):
        if s[i].isupper():
            s[i]=chr((ord(s[i])-ord('A')+ n)%26+ord('A'))
        elif s[i].islower():
            s[i]=chr((ord(s[i])-ord('a')+ n)%26+ord('a'))

    return "".join(s)
```
