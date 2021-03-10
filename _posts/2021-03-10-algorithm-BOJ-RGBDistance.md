---
published: true
title: '[백준] 1149번 - RGB거리'
layout: post
subtitle: 'BOJ 1149, RGB거리'
categories: algorithm
tags: BOJ
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/1149`](https://www.acmicpc.net/problem/1149)

## **문제 설명 및 풀이**
---
쉬운 DP 문제들은 보통 1차원 배열로 풀 수 있지만, 이 문제는 조금 다르다. 색을 고루 사용해야 하며, 각 색을 택할 때마다 경우가 달라지므로 색깔마다 DP 배열을 갖고 있어야 한다. 이 생각을 떠올리기 쉽지 않아서 그렇지, 떠올리고 나면 코드는 매우 간단하다. 구하고자 하는 값이 N 번째 값이라면 N-1 번째에서 이번에 선택할 색과 다른 각각 두 색깔의 DP 배열 중 최소를 골라 현재 고른 색깔의 비용을 더해주면 되기 때문이다.  

## **정답 코드**
---

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int n;
int rgb[1000][3];
int dp[1000][3];

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
        cin >> rgb[i][0] >> rgb[i][1] >> rgb[i][2];
    dp[0][0] = rgb[0][0], dp[0][1] = rgb[0][1], dp[0][2] = rgb[0][2];
    for (int i = 1; i < n; i++)
    {
        dp[i][0] = min(dp[i - 1][1], dp[i - 1][2]) + rgb[i][0];
        dp[i][1] = min(dp[i - 1][0], dp[i - 1][2]) + rgb[i][1];
        dp[i][2] = min(dp[i - 1][0], dp[i - 1][1]) + rgb[i][2];
    }
    cout << min(min(dp[n - 1][0], dp[n - 1][1]), dp[n - 1][2]);
    return 0;
}
```

---
cf) 굳이 2차원 배열로 저장하지 않고 바로바로 최신화해서 1차원 배열로 푸는 방법도 있다. 위와 같은 생각을 못 떠올렸다면 1차원 배열로도 풀 수 있음을 명심하자.
```c++
#include <iostream>
#include <algorithm>

using namespace std;

int n, r, g, b, dp[3] = { 0, };

int main()
{
    cin >> n;
    while (n--)
    {
        cin >> r >> g >> b;
        r += min(dp[1], dp[2]);
        g += min(dp[0], dp[2]);
        b += min(dp[0], dp[1]);
        dp[0] = r, dp[1] = g, dp[2] = b;
    }
    cout << min(min(r, g), b);
    return 0;
}
```
