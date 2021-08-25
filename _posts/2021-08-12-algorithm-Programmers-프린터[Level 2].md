---
published: true
title: '[프로그래머스] Level2 - 프린터'
layout: post
subtitle: 'Programmers, Level2, Queue/Stack, Printer'
categories: algorithm
tags: programmers problems
comments: true
---

# **문제**
---
> [`문제: 프로그래머스 Level 2 - 프린터(큐/스택)`](https://programmers.co.kr/learn/courses/30/lessons/42587)

## **문제 설명 및 풀이**
---
1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.

이를 그대로 코드로 옮겨주면 된다. 인쇄 대기목록은 queue를 사용하고 중요도는 priority_queue를 이용하여 중요도가 높은 순서대로 유지해주면 된다. 큐를 돌면서 하나씩 pop해서 priority_queue의 front와 비교해주고 같다면 처리하고 다르다면 다시 q에 삽입하는 형태로 구현하면 된다.
아래 코드에서는 queue에 삽입할 때 흔히 사용하는 push가 아닌 emplace를 사용하였는데, 이는 임시 객체를 만들지 않고 바로 삽입되기 때문에 push보다 빠르고 또 불필요한 복사가 일어나지 않는다고 한다.
### **정답 코드**
---
```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(vector<int> priorities, int location)
{
    int answer = 0;
    priority_queue<int> pq;
    queue<pair<int, int>> q;

    int pSize = priorities.size();
    for (int i = 0; i < pSize; i++)
    {
        q.emplace(i, priorities[i]);
        pq.push(priorities[i]);
    }

    while (!q.empty())
    {
        int i = q.front().first;
        int p = q.front().second;
        q.pop();
        if (p == pq.top())
        {
            pq.pop();
            answer += 1;

            if (i == location)
                break;
        }
        else
            q.emplace(i,p);
    }
    return answer;
}
```
---
