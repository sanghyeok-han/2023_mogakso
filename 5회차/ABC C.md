# ABC C

## 문제 출처

[https://atcoder.jp/contests/abc290/tasks/abc290_c](https://atcoder.jp/contests/abc290/tasks/abc290_c)

## 문제 설명

자연수 N이 주어지며, 음수가 아닌 정수 N개가 주어진다.

그 후 자연수 K가 주어진다. 이때 N개의 수 중 K개를 뽑아서 mex 값을 최대화 할 때의 mex 값을 구하여라.

참고로 mex 값은 수열에서 0부터 차례대로 1씩 늘려가며 있는지 확인할 때 없는 첫 번째 값이 된다.

1 ≤ K ≤ N ≤ 300000

0 ≤ 각각의 수 ≤ 10^9

## 문제 풀이

주어진 수들을 정렬한 다음 차례대로 순회하면서 0부터 시작해서 0이 있으면 1이 있는지를 보고, 1이있으면 2가 있는지를 보는 방식을 반복하면 된다.

## 소스 코드

```python
n, k = map(int, input().split())
A = sorted(map(int, input().split()))

to_find = 0
for i in range(n):
    if k and A[i] == to_find:
        k -= 1
        to_find += 1
        
print(to_find)
```