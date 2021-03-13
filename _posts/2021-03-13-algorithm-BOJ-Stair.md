---
published: true
title: '[백준] 2579번 - 계단 오르기'
layout: post
subtitle: 'BOJ 2579, Olympiad > 한국정보올림피아드 > 한국정보올림피아드시․도지역본선 > 지역본선 2006 > 초등부 4번'
categories: algorithm
tags: BOJ
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/2579`](https://www.acmicpc.net/problem/2579)

## **문제 설명 및 풀이**
---
DP 문제는 항상 점화식을 구하는 문제이다. N 번째 값을 구할 때 그전에 구한 값들을 이용해서 식으로 표현하는 것과 마찬가지이다.
위 문제의 조건은 다음과 같다.
1. 계단은 한 번에 한 계단씩 또는 두 계단씩 오를 수 있다.
2. 연속된 세 개의 계단을 모두 밟아서는 안 된다. 단, 시작점은 계단에 포함되지 않는다.
3. **마지막 도착 계단은 반드시 밟아야 한다.**
I 번째 계단을 오르려면(항시 3번 조건 만족) 2칸 전에서 바로 오르거나, 3칸 전을 거쳐 바로 직전 칸을 거쳐 오는 방법 외에는 없다.
코드로 나타내면 아래와 같다.

## **정답 코드**
---

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int dp[301];
int stair[301];

int main()
{
  int n;
  cin >> n;
  for(int i=1; i<=n; i++)
    cin >> stair[i];
  dp[1] = stair[1], dp[2] = stair[1] + stair[2];
  for(int i=3; i<=n; i++)
    dp[i] = max(dp[i-3] + stair[i-1], dp[i-2]) + stair[i];
  cout << dp[n];
  return 0;
}
```
