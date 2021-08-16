---
published: true
title: '[프로그래머스] Level1 - 숫자 문자열과 영단어'
layout: post
subtitle: 'Programmers, Level1, kakao internship 2021'
categories: algorithm
tags: programmers problems
comments: true
---

# **문제**
---
> [`[프로그래머스] level 1 - 숫자 문자열과 영단어, 2021 카카오 채용연계형 인턴십 기출`](https://programmers.co.kr/learn/courses/30/lessons/81301)

## **문제 설명 및 풀이**
---
사실 맨 처음에 실시간으로 저 문제를 풀 때에는 여러개의 if-else문으로 해결했었다. 더 깔끔하게 처리하는 방법을 알고 있었지만, 아무래도 이런 확장성이 필요없는 조건안에서의 문제는 단순하게 푸는 게 더 빨리 문제를 해결할 수 있기 때문에 아무 생각없이 우다다다 if-else문으로 해결했다. 지금은 끝나고 풀이를 하는 입장이기에 더 깔끔한 방법들을 소개하겠다. 첫 번째는 map을 사용해서 문자열을 치환해주는 풀이이다. 먼저 각 key(string s에 주어진 zero, one, ...)에 따른 value(0, 1, ...)를 지정해준다. 그 다음은 숫자 문자열이면 그냥 바로 추가해주고 그렇지 않으면 tmp 문자열에 모았다가 map에서 찾아주면 된다.

### **맵을 사용해서 푼 코드**
---
```cpp
#include <string>
#include <vector>
#include <map>

using namespace std;

int solution(string s) {
    map<string, string> MAP;
    MAP["zero"] = "0", MAP["one"] = "1", MAP["two"] = "2", MAP["three"] = "3", MAP["four"] = "4",
    MAP["five"] = "5", MAP["six"] = "6", MAP["seven"] = "7",
    MAP["eight"] = "8", MAP["nine"] = "9";
    string answer = "";
    string tmp = "";
    for(int i=0; i<s.length(); i++)
    {
        // 글자일 경우
        if(isdigit(s[i]) == 0)
        {
            tmp += s[i];
            if(MAP[tmp] != "")
            {
                answer += MAP[tmp];
                tmp = "";
            }
        }
        // 숫자일 경우
        else
            answer += s[i];
    }
    return stoi(answer);
}

```

### **regex_replace를 이용한 풀이**
---
두 번째 풀이는 다른 사람의 풀이인데, 너무 깔끔하고 이런 함수가 있구나 싶어서 같이 글에 쓴다. 좋은 코드인지는 모르겠으나 유용한 함수임은 분명하다. 바로 원하는 문자열을 원하는 문자열로 치환하는 함수이다. 헤더는 <regex>이며 사용한 함수는 regex_replace이다. regex는 regular expression을 의미하며 정규 표현식이라고 한다. 정규 표현식은 문자열에서 패턴을 찾는데 사용하며 이를 통해 원하는 패턴의 문자열을 검색하거나 치환할 수 있다.   
regex_replace의 경우 첫 번째 인자는 패턴이 있는 문자열, 두 번째 인자는 탐색하고자 하는 정규식, 세 번째 인자는 대체문자열이다. 그래서 두 번째 인자는 반드시 regex라는 함수로 정규식 변환을 한 뒤에 넘겨주어야 한다.

```cpp
#include <bits/stdc++.h>
using namespace std;

int solution(string s) {
    s = regex_replace(s, regex("zero"), "0");
    s = regex_replace(s, regex("one"), "1");
    s = regex_replace(s, regex("two"), "2");
    s = regex_replace(s, regex("three"), "3");
    s = regex_replace(s, regex("four"), "4");
    s = regex_replace(s, regex("five"), "5");
    s = regex_replace(s, regex("six"), "6");
    s = regex_replace(s, regex("seven"), "7");
    s = regex_replace(s, regex("eight"), "8");
    s = regex_replace(s, regex("nine"), "9");    
    return stoi(s);
}
```
---
