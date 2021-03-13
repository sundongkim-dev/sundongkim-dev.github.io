---
published: true
title: '[백준] 1932번 - 정수 삼각형'
layout: post
subtitle: 'BOJ 1932, Olympiad > International Olympiad in Informatics > IOI 1994 1번'
categories: algorithm
tags: BOJ
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/1932`](https://www.acmicpc.net/problem/1932)

## **문제 설명 및 풀이**
---
[RGB거리와 매우 유사하다](https://sundongkim-dev.github.io/algorithm/2021/03/10/algorithm-BOJ-RGBDistance/). 그저 계속 갱신해주면 된다. 그나마 주의할 점은 MAX값을 구하는 것이라는 것과 예제 상으로 아래 또는 대각선 오른쪽으로만 진행한다는 것을 빼먹지 않으면 된다. 코드는 아래와 같다.  

## **정답 코드**
---

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int n, ans = 0;
int dp[500][500];

int main()
{
    cin >> n;
    cin >> dp[0][0];
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j <= i; j++)
        {
            int x;
            cin >> x;
            if (j == 0)
                dp[i][j] = dp[i - 1][j] + x;
            else
                dp[i][j] = max(dp[i - 1][j - 1], dp[i - 1][j]) + x;
        }
    }
    for (int i = 0; i < n; i++)
        ans = max(ans, dp[n - 1][i]);
    cout << ans << "\n";
    return 0;
}
```
