---
published: true
title: '[백준] 1764 - 듣보잡'
layout: post
subtitle: 'BOJ 10815, 정렬'
categories: algorithm
tags: boj problems
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/1764`](https://www.acmicpc.net/problem/1764)

## **문제 설명 및 풀이**
---
이렇게 문자열로 무언가 검색을 한다거나 관련 정보를 저장하고 싶다면 map이 제일 먼저 떠오른다. map과 vector를 사용하여 간단하게 구현해보았다. 결과적으로, map도 탐색할 때 O(logn)의 시간 복잡도를 가지므로 큰 차이가 없기에 이분탐색으로 굳이 구현할 필욘 없다고 생각했다.
허나 vector를 사용한 이분탐색을 하게 되면 실제로는 백준 로그 상 절반 정도의 시간만이 걸렸다. map은 삽입할 때마다 정렬을 하고 vetor는 모두 입력받은 후에 정렬을 해주기 때문에 더 빠른 걸까..?  
정답을 안다면 댓글을 달아주시면,,,감사하겠습니다..  

## **map과 vector를 이용한 코드**
---

```c++
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;

int main()
{
    int N, M;
    map<string, int> m;
    vector<string> v;
    string tmp;

    cin >> N >> M;

    for (int i = 0; i < N; i++)
    {
        cin >> tmp;
        m[tmp] = 1;
    }
    for (int i = 0; i < M; i++)
    {
        cin >> tmp;
        if (m[tmp])
            v.push_back(tmp);
    }
    sort(v.begin(), v.end());
    cout << v.size() << endl;
    for (int i = 0; i < v.size(); i++)
        cout << v[i] << endl;
    return 0;
}
```

## **다른 정답 코드**
---
```c++
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;

int main()
{
    string tmp;
    int N, M;
    vector<string> v, ans;

    cin >> N >> M;
    v.resize(N);

    for (int i = 0; i < N; i++)
        cin >> v[i];

    sort(v.begin(), v.end());

    for (int i = 0; i < M; i++)
    {
        cin >> tmp;
        if (binary_search(v.begin(), v.end(), tmp))
            ans.push_back(tmp);
    }
    sort(ans.begin(), ans.end());
    cout << ans.size() << endl;
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << endl;
    return 0;
}
```
