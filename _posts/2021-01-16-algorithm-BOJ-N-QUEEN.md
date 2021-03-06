---
published: true
layout: post
title: '[백준] 9663번 - N-Queen'
subtitle: 'BOJ 9663, N-Queen'
categories: algorithm
tags: boj problems
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/9663`](https://www.acmicpc.net/problem/9663)

## **문제 설명 및 풀이**
---
퀸은 자신의 위치에서 상하좌우, 대각선 방향으로 움직일 수 있는 기물이다. 그래서 같은 열과 같은 대각선에 위치하지 않게 퀸을 배치하는 경우를 찾는 문제이다. 이 문제 역시 백트래킹 알고리즘을 통해 풀 수 있다. 첫 번째 행의 첫 번째 열부터 배치하면서 그 다음 칸에 배치해도 되는지를 파악해가며, 배치할 수 없다면 다시 한 칸 위로 올라와서 다음 수를 고려하면 된다.  
결국 이 문제의 포인트는, 퀸을 배치할 공간의 상하, 좌우, 우상향 대각선, 우하향 대각선들을 어떻게 체크하면서 재귀할 것인가를 알면 된다. 좌우는 for문을 돌면서 자동으로 고려가 되어서 상하, 우상향 대각선, 우하향 대각선만을 고려하면 된다. 이 3가지를 체크하기 위해 boolean 자료형의 배열 visited1, visited2, visited3를 만들어주었다.  
첫 번째로, 상하는 그냥 for문을 통해서 i번째 index를 1로 바꿔주면 된다. 매우 간단하다.  
두 번째로, 우상향 대각선은 좌표가 x,y라면 x+y가 일정한 값으로 유지되는 것을 알 수 있다. 기울기를 생각해보면 이해하기가 쉽다. 우상향 직선을 만들기 위해서는 x와 y가 각각 한칸씩 늘어나거나 줄어들어야 하기 때문이다. n * n 배열에서 대각선의 갯수는 2 * n - 1개가 존재한다.   
세 번째로, 우하향 대각선은 y - x + (n - 1) 값이 일정한 값으로 유지되는 것을 알 수 있다. 이것도 마찬가지로 기울기를 생각해보면 이해하기가 쉽다. 다만 배열을 쉽게 인덱스로 접근하기 위해 n-1을 더해준다.  
종합적으로, 위 세가지를 따져가면서 깊이 탐색을 하고, 마지막 줄까지 이상이 없다면 cnt를 늘려주어 경우의 수를 찾으면 된다.
## **코드**
---
<script src="https://gist.github.com/sundongkim-dev/37da078d835bf79becc39afa26910f0a.js"></script>
