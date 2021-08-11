---
published: true
title: '[프로그래머스] Level2 - 더 맵게'
layout: post
subtitle: 'Programmers, Level2, Heap, Scoville'
categories: algorithm
tags: programmers problems
comments: true
---

# **문제**
---
> [`https://programmers.co.kr/learn/courses/30/lessons/42626`](https://programmers.co.kr/learn/courses/30/lessons/42626)

## **문제 설명 및 풀이**
---
문제를 처음 보았을 때, 무지성으로 그저 주어진벡터에서 정렬과 push, pop을 번갈아가며 해주면 쉽게 해결되리라고 생각하고 바로 코드를 작성했다. 그러나 아래와 같이 정확성은 확보되지만 효율성에서 모조리 실패하는게 아닌가.
![그림1](https://sundongkim-dev.github.io/assets/img/algorithm/2021-08-21-algorithm-Programmers-더맵게_힙x.jpg)

아무래도 정렬을 매 반복마다 한번씩 하는것이 부담이 되었을 것이다. 이를 해결하기 위한 좋은 자료구조로는 우선순위 큐가 있다. 이는 매 원소의 삽입과 삭제마다 logN의 시간복잡도를 갖게 한다. 정렬 또한 마찬가지이다.
나의 경우 priority_queue를 사용할 때 마지막 인자로 greater<int>를 사용하지 않았지만 사용한다면 중간 중간 -를 안붙이고 깔끔하게 풀 수 있을 것이다.~~(필자는 디폴트가 내림차순인지 오름차순인지 헷갈려서 저렇게 코딩하는게 버릇되어서 편해졌다..)~~

### **힙 자료구조를 사용하지 않고 푼 코드**
---
```cpp
#include <algorithm>
#include <vector>
#include <queue>
using namespace std;

priority_queue<int> pq;

int solution(vector<int> scoville, int K)
{
    int answer = 0;
    // scoville 벡터 정렬안되어 있을 수 있기에 해주어야 함.
    sort(scoville.begin(), scoville.end());

    while(1)
    {
        if(scoville[0] >= K)
            break;
        if(scoville.size() == 1)
            return -1;
        int sco1 = scoville[0];
        int sco2 = scoville[1];
        scoville.push_back(sco1+sco2*2);
        answer++;
        scoville.erase(scoville.begin(), scoville.begin() + 2);
        sort(scoville.begin(), scoville.end());
    }
    return answer;
}
```

### **정답 코드**
---
```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

priority_queue<int> pq;

bool check(int pivot)
{
    if(-pq.top() >= pivot)
        return true;
    return false;
}

int solution(vector<int> scoville, int K) {
    int answer = 0;

    //배열 데이터 넣어줌
    for(int i=0; i<scoville.size(); i++)
        pq.push(-scoville[i]);

    //스코빌 지수 확인하고 아니면 음식 섞음
    while(!check(K))
    {
        //음식이 하나밖에 남아있지 않다면 실패
        if(pq.size() == 1)
            return -1;

        //음식 섞기
        int sco1 = -pq.top();
        pq.pop();
        int sco2 = -pq.top();
        pq.pop();
        int tmp = sco1 + sco2*2;
        pq.push(-tmp);
        answer++;
    }
    return answer;
}
```
---
