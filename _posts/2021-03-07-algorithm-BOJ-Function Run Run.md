---
published: true
layout: post
subtitle: >-
  BOJ 9184, Function Run Run from ICPC > Regionals > North America > Pacific
  Northwest Regional > 1999 Pacific Northwest Region Programming Contest C번
categories: algorithm
tags: BOJ
comments: true
title: '[백준] 9184번 - 신나는 함수 실행'
---
# **문제**
---
> [`https://www.acmicpc.net/problem/9184`](https://www.acmicpc.net/problem/9184)

## **문제 설명 및 풀이**
---
문제를 보자마자 떠오른 방법은 두 가지였다. 하나는 그냥 3중 for문을 돌려서 값을 다 저장해주는 것이었고 나머지는 재귀를 이용하여 갱신될때마다 값을 저장해주는 것이었다. Fibonacci 함수만 보면 재귀로 푸는 것이 익숙해 후자를 택해서 풀어보았다. 코드는 간단하다. 0보다 작거나 같거나, 20보다 큰지만 확인하고 해당 값이 결정되었는지를 묻고, 있다면 반환 없다면 그 수를 재귀로 찾아 저장해주면 된다. 당연하겠지만 3중 for문이 재귀보다는 더 빠르다. 변수를 대입함과 동시에 반환할 수 있음을 유의하자. 
## **코드**
---
```cpp:신나는_함수_실행.cpp
#include <bits/stdc++.h>

using namespace std;

int a, b, c;
int dp[21][21][21];

int w(int a, int b, int c)
{
  if(a<=0 || b<=0 || c<=0)
    return 1;
  if(a>20 || b>20 || c>20)
    return w(20,20,20);
  if(dp[a][b][c])
    return dp[a][b][c];
  if(a<b && b<c)
    return dp[a][b][c] = w(a,b,c-1) + w(a,b-1,c-1) - w(a,b-1,c);
  return dp[a][b][c] = w(a-1,b,c) + w(a-1,b-1,c) + w(a-1,b,c-1) - w(a-1,b-1,c-1);
}

int main(void)
{
  while(1)
  {
    cin >> a >> b >> c;
    if(a==-1 && b==-1 && c==-1)
      break;
    cout << "w(" << a << ", " << b << ", " << c << ") = " << w(a,b,c) << "\n";
  }
  return 0;
}
```
<https://gist.github.com/sundongkim-dev/3665e6abc16ff5de195963e3ef415d73.js>