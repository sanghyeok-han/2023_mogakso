# ABC D

## 문제 출처

[https://atcoder.jp/contests/abc290/tasks/abc290_d](https://atcoder.jp/contests/abc290/tasks/abc290_d)

## 문제 설명

자연수 N이 주어지며 N개의 정사각형이 좌표 0부터 N - 1까지 1차원으로 이어져 있다. 이제 각각의 좌표에 있는 정사각형을 다음의 방식을 통해 모두 색칠하려고 한다.

1. 0번 좌표의 정사각형을 칠한다.
2. 아래의 과정을 N - 1번 반복한다.
    1. 변수 x에 (A + D) mod N를 할당하며, A는 가장 최근에 칠해진 정사각형의 좌표이다.
    2. 만약 x의 정사각형이 칠해져 있다면, x를 (x + 1) mod N으로 대체하여라.
    3. x의 정사각형을 칠하여라.
    

 이러한 과정을 거칠 때 K번째에 색칠하게 되는 정사각형의 좌표를 출력하여라.

테스트케이스의 개수 ≤ 100000

1 ≤ K ≤ N ≤ 10 ^ 9

1 ≤ D ≤ 10 ^ 9

## 문제 풀이

같은 정사각형에 또 색칠하기 바로 전 과정을 거치기 위해 x번이 필요하다고 한다면, x + 1번째에 색칠하게 되는 것은 (처음 색칠한 곳 + 1) mod N의 좌표가 되게 된다.

이때 모든 정사각형을 색칠하기 위해 필요한 전체 횟수를 x번씩 그룹화시켜 생각한 다음, N와 D의 최소공배수를 이용하여 해결할 수 있다.

## 소스 코드

```python
from math import gcd
import io, os, sys
input = io.BytesIO(os.read(0, os.fstat(0).st_size)).readline

lcm = lambda a, b: a * b // gcd(a, b)

for _ in range(int(input())):
    n, d, k = map(int, input().split())
    k -= 1

    in_group_c = lcm(n, d) // d

    added = k // in_group_c

    nth_in_first_group = k % in_group_c

    nth_in_first_group

    temp = d * nth_in_first_group % n
    temp += added
    temp %= n

    print(temp)
```