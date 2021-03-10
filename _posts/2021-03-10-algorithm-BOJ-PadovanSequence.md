---
published: true
title: '[백준] 9461번 - 파도반 수열'
layout: post
subtitle: >-
  BOJ 9461, ICPC > Regionals > Asia Pacific > Korea > Asia Regional - Daejeon
  2013 G번
categories: algorithm
tags: BOJ
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/9461`](https://www.acmicpc.net/problem/9461)

## **문제 설명 및 풀이**
---
이 문제 또한 매우 전형적인 DP 문제이다. DP 문제를 가만히 놓고 보면 꼭 어릴 적에 한 번쯤 풀어보았던 IQ 테스트의 수열 주어지고 빈칸에 들어갈 수를 맞히는 것이 떠오른다. 혹시나 이런 사람이 있을까 싶어서 그냥 수만 보고 예측해서 코드를 짜보았다.  1, 1, 1, 2, 2, 3, 4, 5, 7, 9…. 흠 대충 살펴보니, **N 번째 수**는 `N-2 번째 수와 N-3 번째 수의 합`이다.  
**수열만 보고 짠 코드**
---
```c++
#include <iostream>

using namespace std;

int n;
long long arr[101];

int main()
{
    arr[1] = 1, arr[2] = 1, arr[3] = 1, arr[4] = 2;
    for (int i = 5; i <= 100; i++)
    {
        arr[i] = arr[i - 2] + arr[i - 3];
    }
    cin >> n;
    while (n--)
    {
        int p;
        cin >> p;
        cout << arr[p] << "\n";
    }
    return 0;
}
```
나는 당연히 틀릴 줄 알고 제출했더니 맞아버렸다…. 당황해서 왜 맞았는지를 생각해보았다.  
이에 앞서, 답을 유출하는 정석적인 방법을 먼저 설명하겠다. 친절하게도 백준에서 그림을 줘서 그림만 보아도 규칙을 알 수 있다. N 번째 삼각형은 N-1 번째 삼각형의 변과 N-5 번째 삼각형의 변의 합과 같음을 알 수 있다. 이를 토대로 코드를 짜면 아래와 같다.  
자, 이제 생각도 안 하고 나열된 수만 보고 점화식을 유도한 경우를 다시 살펴보자. 왜 맞았을까..?  
이것도 조금만 살펴보면 알아낼 수 있다. N-2 번째는 N-1 번째와 변을 공유하고, N-3 번째는 N-5 번째와 같은 변을 공유하기 때문이다. 굳이 이렇게 풀 이유는 없을 것 같다. 그냥 딱 봤을 때 N 번째 삼각형은 N-1 번째 삼각형의 변에 N-5 번째 삼각형의 변을 더한 값이기 때문이다.  
## **정답 코드**
---
```c++
#include <iostream>

using namespace std;

long long tri[1000];

int main() 
{
  long long T, N, ans;
  cin >> T;

  tri[1] = 1, tri[2] = 1, tri[3] = 1, tri[4] = 2, tri[5] = 2;
  for(int i=6; i<=100; i++)
    tri[i] = tri[i-5] + tri[i-1];
  
  for(int i=0; i<T; i++)
  {
    cin >> N;
    cout << tri[N] << "\n";
  }
  return 0;
}
```
