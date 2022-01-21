---
published: true
title: '[백준] 10815번 - 숫자 카드'
layout: post
subtitle: 'BOJ 10815, 정렬, 이분 탐색'
categories: algorithm
tags: boj problems
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/10815`](https://www.acmicpc.net/problem/10815)

## **문제 설명 및 풀이**
---
정렬하고 배열을 돌면서 해당 원소가 있는 지 확인해주면 된다. 확인하는 방법으론 여러 방법이 있지만, 카테고리가 이분 탐색이길래 이분 탐색으로 구현해보았다.   
이보다 메모리를 더 아끼면서도 훨씬 더 빠르게 문제를 풀 수 있는 경악스런 방법이 있다. 총 범위의 두배만큼의 메모리를 쓰고 bool자료형을 써서 int를 썻을 때 대비 1/4로 아끼고, 한 번 접근으로 매번 답을 구할 수 있다.

## **정렬 및 이분 탐색을 이용한 코드**
---

```c++
#include <string>
#include <iostream>
#include <algorithm>

using namespace std;

int N, M, answer;
int deck[500000] = { 0, };
int aDeck[500000] = { 0, };

int findNum(int A)
{
    int low = 0;
    int high = N-1;
    while (low <= high)
    {
        int mid = (low + high) / 2;
        if (A == deck[mid])
            return 1;
        else if (A < deck[mid])
            high = mid - 1;
        else
            low = mid + 1;
    }
    return 0;
}

int main()
{
    cin >> N;
    for (int i = 0; i < N; i++)
        cin >> deck[i];

    cin >> M;
    for (int i = 0; i < M; i++)
        cin >> aDeck[i];

    sort(deck, deck + N);

    for (int i = 0; i < M; i++)
    {
        answer = findNum(aDeck[i]);
        cout << answer << " ";
    }

    return 0;
}
```

## **다른 정답 코드**
---
```c++
#include <iostream>
#include <vector>
using namespace std;

int l, n;
void init() // 요 함수가 없으면 시간 초과가 나기 때문에 좋은 코드라고는 말 못하겠지만 이런 방법도 있다..
{
  ios_base::sync_with_stdio(false);
  cin.tie(0);
  cout.tie(0);
}

int main()
{
    init();
    vector<bool> v(20000001, false);
    cin >> l;
    while(l--){
        cin >> n;
        v[n + 10000000] = true;
    }
    cin >> l;
    while(l--){
        cin>> n;
        if(v[n + 10000000])
          cout << "1 ";
        else
          cout << "0 ";
    }
}
```
