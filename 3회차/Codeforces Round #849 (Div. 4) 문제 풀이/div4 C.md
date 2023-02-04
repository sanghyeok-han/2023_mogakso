# div4 C

## 문제 출처

[https://codeforces.com/contest/1790/problem/C](https://codeforces.com/contest/1791/problem/C)

## 문제 설명

0 또는 1로 이루어진 문자열이 있다. 이때 이 문자열의 시작에 0, 끝에 1을 각각 추가하거나,

시작에 1, 끝에 0을 각각 추가하는 작업을 원하는만큼 할 수 있다. 

이러한 과정을 거친 문자열이 주어졌을 때 처음 문자열로 가능한 가장 작은 길이를 구해서 출력하여라.

## 문제 풀이

주어진 문자열을 덱 자료형으로 만든 다음에 양옆에서 0, 1 또는 1, 0을 뺄 수 있을 때까지 뺀 다음 남은 문자열의 길이를 출력하면 된다.

## 소스 코드

```python
from collections import deque
import sys
input = lambda: sys.stdin.readline().rstrip()

for _ in range(int(input())):
    n = int(input())

    deq = deque(input())
    while deq and deq[0] != deq[-1]:
        deq.popleft()
        deq.pop()

    r = len(deq)

    print(r)
```