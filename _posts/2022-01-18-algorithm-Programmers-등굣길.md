---
published: true
title: '[프로그래머스] Level 3 - 등굣길'
layout: post
subtitle: 'Programmers, Level 3, Dynamic Programming'
categories: algorithm
tags: programmers problems
comments: true
---

# **문제**
---
> [`[프로그래머스] level 3 - 등굣길, DP`](https://programmers.co.kr/learn/courses/30/lessons/42898)

## **문제 설명 및 풀이**
---
~~등교길이 맞는 지 등굣길이 맞는 지 쳐보게 되었..~~  
중학교 때 경우의 수에서 배웠던 것이 바로 생각났다.. ~~왜 이렇게 웅덩이를 만들고 난리야했던 기억이~~ 문제를 풀면서 주의할 점은 바로 m과 n이 상식에 맞지 않게 반대되어서 제공되었단 점이다. 다시 한번 문제를 잘 읽어봐야 함을 깨달았다. M과 N이 일반적인 것과 반대로 즉, m이 열, n이 행으로 주어졌으므로, 웅덩이 또한 반대로 저장해야 함을 잊지 말자. 당신이 필자처럼 하나빼고 올 fail이 뜬다면 m과 n을 다시 살펴보자..  
중딩 때 풀던 경우의 수 문제인데, 돌이켜보니 dp와 매우 유사하다. 어느 지점까지의 거리를 계산하고 다음 지점을 계산할 때 그대로 값을 쓰는 것이다.  

~~왜 level 3일까..왜 사람들은 대부분 dfs로 푼 것일까..~~

### **Map과 Set을 사용해서 푼 코드**
---
```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

#define DIVIDE 1000000007

using namespace std;

int solution(int m, int n, vector<vector<int>> puddles) {
    int answer = 0;
    int map[100][100] = {0,};

    for(auto x : puddles)
        map[x[1]-1][x[0]-1] = -1; // 웅덩이는 -1로 저장

    for(int i=0; i<n; i++)
    {
        if(map[i][0] == -1) // -1은 웅덩이이므로 더이상 계산 불가
            break;
        else
            map[i][0] = 1;  // 해당 칸까지 가는 최소 경우의 수는 1이라는 뜻
    }
    for(int i=0; i<m; i++)
    {
        if(map[0][i] == -1)
            break;
        else
            map[0][i] = 1;
    }
    for(int i=1; i<n; i++)
    {
        for(int j=1; j<m; j++)
        {
            if(map[i][j] == -1) // -1은 웅덩이이므로 패스
                continue;
            // 위와 왼쪽 둘다 웅덩이가 아니라면 그 둘의 합이 해당 지점까지의 경우의 수
            if(map[i-1][j] != -1 && map[i][j-1] != -1)
                map[i][j] = map[i-1][j] + map[i][j-1];
            // 왼쪽은 웅덩이이고 위는 아니라면 위의 값 그대로 가져온다.
            else if(map[i-1][j] == -1 && map[i][j-1] != -1)
                map[i][j] = map[i][j-1];
            // 위는 웅덩이이고 왼쪽은 아니라면 왼쪽 값 그대로 가져온다.
            else if(map[i-1][j] != -1 && map[i][j-1] == -1)
                map[i][j] = map[i-1][j];
            // 문제 조건에 따라 나머지 구하기
            map[i][j] %= DIVIDE;
        }
    }
    answer = map[n-1][m-1] % DIVIDE;
    return answer;
}
