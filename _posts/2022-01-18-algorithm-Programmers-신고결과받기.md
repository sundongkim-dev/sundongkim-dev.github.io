---
published: true
title: '[프로그래머스] Level 1 - 신고 결과 받기'
layout: post
subtitle: 'Programmers, Level 1, 2022 KAKAO BLIND RECRUITMENT'
categories: algorithm
tags: programmers problems
comments: true
---

# **문제**
---
> [`[프로그래머스] level 1 - 신고 결과 받기, 2022 KAKAO BLIND RECRUITMENT`](https://programmers.co.kr/learn/courses/30/lessons/92334)

## **문제 설명 및 풀이**
---
문제를 보자마자 굉장히 실생활에서 쓰일 것만 같아서 미소가 지어졌었다 ㅎㅎ,,,  
유의할 점은 자기 자신을 신고하는 경우는 없으며 한 사람이 어떤 사용자를 여러 번 신고했다 하더라도 동일한 유저에 대한 신고 횟수는 1번으로 처리된다는 점이다. 이용자 id와 신고한 id는 공백 하나로 구분되어 있는데 즉, 신고한 사람과 신고를 당한 사람을 엮어서 표현해야하므로 자료구조는 map이 바로 떠올랐다. 이에 더해, 동일한 유저에 대한 다수의 신고는 무의미하기 때문에 set을 사용하여 중복을 제거하면 되겠다라는 생각을 하였다.

### **Map과 Set을 사용해서 푼 코드**
---

```cpp  
#include <string>
#include <vector>
#include <iostream>
#include <map>
#include <set>

using namespace std;

vector<int> solution(vector<string> id_list, vector<string> report, int k) {
    vector<int> answer(id_list.size());
    map<string, set<string>> reportedMap;
    map<string, int> reportCnt;
    set<string> victim;

    for(string s : report)
    {
        int idx = s.find(" ");
        string reportedMan = s.substr(idx+1); // 신고당한 사람
        string reporter = s.substr(0, idx);; // 신고한 사람
        // 이미 신고한 사람이라면 넘어감
        if(reportedMap[reporter].count(reportedMan))
            continue;
        reportedMap[reporter].insert(reportedMan);
        reportCnt[reportedMan]++; // 해당 사람 신고 횟수 늘리기
    }
    // 신고 횟수 기준 초과한 사람 저장
    for(string x : id_list)
    {
        if (reportCnt[x] < k)
            continue;
        victim.insert(x);
    }

    for(int i=0; i<id_list.size(); i++)
    {
        int cnt = 0;
        // 처리 메일 횟수 저장
        for(auto x : reportedMap[id_list[i]])
            if(victim.find(x) != victim.end())
                cnt ++;
        answer[i] = cnt;
    }
    return answer;
}

'''
