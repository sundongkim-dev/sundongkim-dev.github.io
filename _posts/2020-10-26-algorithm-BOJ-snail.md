---
published: true
layout: post
subtitle: 'BOJ 2869, PUŽ  from  COCI 2010/2011 > Contest #2 1번'
categories: algorithm
tags: boj problems
comments: true
title: '[백준] 2869번 - 달팽이는 올라가고 싶다'
---
# 문제
> [`https://www.acmicpc.net/problem/2869`](https://www.acmicpc.net/problem/2869)

처음 이 문제를 보고 접근한 방식은 그냥 간단하게 낮에 도달하면 끝이므로, sum에 a를 더하고 v와 비교한 후 크거나 같다면 day를 출력해주고 그렇지 않다면 b를 빼주고 day를 1 늘려주며 sum이 v보다 크거나 같아질때까지 이를 반복하여 답을 구하였다. 그러나 위 문제의 시간 제한은 0.15초로 보다 빠른 방법을 생각했어야 했다. 나는 평소 문제를 꼼꼼히 보는 편인데 너무 쉬운 문제를 만나 그냥 아무 생각 없이 지나갔던거 같다. (꼼꼼히 보지 않는다는 반증인듯,,,)
<script src="https://gist.github.com/sundongkim-dev/5c72573c668099c230667874ff1a4de7.js"></script>

조금 더 생각해보니, 결국 (V-B)만큼을 도달하면 되는 것이다. (V-B)를 하루에 오를 수 있는 양인 (A-B)로 나눴을 때 나머지가 0이라면 그 몫이 곧 답이며, 그렇지 않다면 하루가 부족하다는 것이므로 몫에 1을 더해준 값이 답이 된다.

이후에 정답자들의 코드를 살펴보니, 그냥 (V-B-1)/(A-B)+1을 출력하면 항상 답을 출력했다.
몇 개의 수를 넣어보니 직관적으로 이게 답이라는 것을 알았지만 수학적으로는 이해가 가지 않았었다.

(V-B)를 p라 하고, (A-B)를 q라 하자.
p/q가 나눠떨어진다면 그 값을 임의의 정수 n이라 하자. (p-1)/q는 반드시 n보다 작은데 int형은 소수점을 버리므로, (p-1)/q는 n-1이며 여기다 1을 더하면 원래의 값인 n이 된다.
p/q가 나눠떨어지지 않는다면 n + f(0<f<1)이라 하자. 이 때, 양변에 q를 곱해주면 p = q(n+f)이다. 여기서 양변에 1을 뺴주면 p-1 = q(n+f)-1이다. 다시 q로 나눠주면 (p-1)/q = (n+f) - 1/q이며 1/q는 int 연산이므로 0이 되고 f또한 버려지므로 위의 나눠떨어지는 경우와 결과값이 같아진다.

아휴~ 그냥 if문 나눠 쓰고말지,,,라는 생각을 하지만 이런 고찰이 고수와 나를 구분하는 점이 아닌가 싶다.

<script src="https://gist.github.com/sundongkim-dev/fefde2ad76f15fd952151ea2087322e7.js"></script>
