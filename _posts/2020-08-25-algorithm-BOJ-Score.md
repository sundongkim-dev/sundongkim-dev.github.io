---
published: true
layout: post
title: '[백준] 8958번 - OX퀴즈'
subtitle: 'BOJ 8958, Score from ICPC-Korea-Seoul 2005 #A'
categories: algorithm
tags: BOJ
comments: true
---
# 문제
> [`https://www.acmicpc.net/problem/8958`](https://www.acmicpc.net/problem/8958)

'O'이 연속하면 점수가 연속한만큼 증가하고, 'X'가 나오면 다시 문제의 점수가 0점이 되므로 전 문제가 'O'였는지 'X'였는지 보고 점수를 매기면 되는 문제이다. 
처음에는 간단하게, 연속하는 두 문제가 각각 'O'인지 'X'인지, 즉 4가지 경우로 나뉘어서 점수를 합산했다. 연속하는 두 문제 모두 맞추었다면 가중치가 1씩 올라가게 저장하고, 틀렸다면 가중치를 초기화하는 것이다.   
<script src="https://gist.github.com/sundongkim-dev/37071a00f6db32c625cd01ecd00b3832.js"></script>

조금만 더 생각해보았더니, **전위 연산자**를 사용하면 굳이 변수를 새로 선언할 필요도, if문도 2개면 된다. 코드는 아래와 같다.  
<script src="https://gist.github.com/sundongkim-dev/f9c445d9d21bd41fa5e3d21263cd97fe.js"></script>
