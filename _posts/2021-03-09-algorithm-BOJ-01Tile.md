---
published: false
title: '[백준] 1904번 - 01타일'
layout: post
subtitle: 'BOJ 1904, 01타일'
categories: algorithm
tags: BOJ
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/1904`](https://www.acmicpc.net/problem/1904)

## **문제 설명 및 풀이**
---









## **코드**
---

```c++
#include <iostream>

using namespace std;

int n;
int arr[1000001];

int main()
{
    arr[1] = 1, arr[2] = 2;
    for (int i = 3; i <= 1000000; i++)
        arr[i] = (arr[i - 2] + arr[i - 1])%15746;
    cin >> n;
    cout << arr[n]%15746;
    return 0;
}
```
