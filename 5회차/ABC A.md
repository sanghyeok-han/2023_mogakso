# ABC A

## 문제 출처

[https://atcoder.jp/contests/abc290/tasks/abc290_a](https://atcoder.jp/contests/abc290/tasks/abc290_a)

## 문제 설명

자연수 N이 주어지며, N개의 문제가 있는 대회가 있다.

각각의 문제를 풀 때 주어지는 점수와 몇 번째 문제들을 풀었는지에 대한 정보가 각각 주어질 때 얻는 점수의 총합을 출력하라.

1 ≤ N ≤ 100

1 ≤ 각 문제의 점수 ≤ 100

## 문제 풀이

각각의 푼 문제들의 점수를 모두 더해주면 된다.

## 소스 코드

```python
n, m = map(int, input().split())
A = list(map(int, input().split()))
B = list(map(int, input().split()))

total = 0
for v in B:
    total += A[v - 1]
    
print(total)
```