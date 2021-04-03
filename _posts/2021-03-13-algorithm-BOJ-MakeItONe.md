---
published: true
title: '[백준] 1463번 - 1로 만들기'
layout: post
subtitle: 'BOJ 1463, 1로 만들기'
categories: algorithm
tags: boj problems
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/1463`](https://www.acmicpc.net/problem/1463)

## **문제 설명 및 풀이**
---
DP 문제 중 이런 문제가 제일 편하다고 생각된다. 문제에서 IF 조건을 친절하게 번호까지 붙여가며 알려주기 때문이다. I-1 번째 수에 1을 더한 것이 I 번째 수이므로, 기본적으로 I-1 번째 값에 1을 더한 값이 I 번째 값이다. 그러나, 2와 3으로 나누어떨어진다면 그 수가 더 작아질 경우가 있음으로 확인해주면 된다. 나누어떨어진다면 그 값에 1을 더한 값이 I 번째 값이다. 이것이 맨 처음 내가 떠올린 풀이이다. 근데 막상 제출해보니 메모리와 시간이 다른 사람들의 답보다 한참 높게 나와서 다른 사람들의 코드도 살펴보았다.  
바로 재귀를 이용한 풀이다. 현재 위치에 도달하는 최솟값을 리턴하는 함수를 만드는데, 이는 2 또는 3으로 나누어떨어지는 거리(x/2, x/3)와 나머지 거리(x%2, x%3)에 1(무조건 드는 연산 횟수)을 더한 값이다. 둘 중 최솟값이 곧 정답이 된다.

## **정답 코드**
---

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int n;
int dp[1000001] = { 0, };

int main()
{
    cin >> n;
    for (int i = 2; i <= n; i++)
    {
        dp[i] = dp[i - 1] + 1;
        if (i % 2 == 0)
            dp[i] = min(dp[i], dp[i / 2] + 1);
        if (i % 3 == 0)
            dp[i] = min(dp[i], dp[i / 3] + 1);
    }
    cout << dp[n] << "\n";
    return 0;
}
```
## 재귀를 이용한 코드
---

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int n;

int recur(int x)
{
  if(x <= 1)
    return 0;
  return min(recur(x/3) + 1 + x%3, recur(x/2) + 1 + x%2);
}

int main()
{
  cin >> n;
  cout << recur(n);
  return 0;
}
```
