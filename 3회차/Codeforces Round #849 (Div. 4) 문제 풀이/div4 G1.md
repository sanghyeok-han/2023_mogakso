# div4 G1

## 문제 출처

[https://codeforces.com/contest/1791/problem/G1](https://codeforces.com/contest/1791/problem/G1)

## 문제 설명

0번부터 n번까지의 번호가 일정한 구간마다 붙어 있는 수평선이 있다. 이때 1번부터 n번까지의 지점에는 순간이동장치가 있다.

또한 각 지점에서 순간이동장치를 사용할 때 필요한 금액이 각각 주어진다.

이때 당신은 1원을 사용해서 왼쪽 또는 오른쪽으로 한 칸 움직이거나, 해당 지점에서 순간이동장치를 사용할 때 필요한 금액을 지불하고 0번 지점으로 순간이동할 수 있다. 또한 각 순간이동장치는 최대 한 번씩만 이용할 수 있다.

당신이 현재 c원을 가지고 있을 때 최대 몇 개의 순간이동장치를 이용할 수 있는지를 구하여라.

1 ≤ 테스트 케이스의 수 ≤ 1000

1 ≤ n ≤ 200000

1 ≤ c ≤ 10^9

1 ≤ 순간이동장치를 이용할 때 필요한 각각의 금액 ≤ 10^9

모든 테스트 케이스에서의 n 값의 합 ≤ 200000

## 문제 풀이

어떤 지점으로 한 칸씩 이동한 다음 해당 지점의 순간이동장치를 이용해서 0번 지점으로 이동하는 것을 한 세트라고 하자.

이때 각각의 지점별로 위의 세트를 진행하기 위해 필요한 금액을 계산한 다음, 오름차순 정렬을 하고 가장 금액이 작은 세트부터 차례대로 가능한 만큼 이용하는 것이 정답이 된다.

## 소스 코드

```python
import sys
input = lambda: sys.stdin.readline().rstrip()

inf = float('inf')

for _ in range(int(input())):
    n, c = map(int, input().split())
    li = [inf] + list(map(int, input().split()))

    ws = [li[i] + i for i in range(n + 1)]
    ws.sort()

    r = 0
    for w in ws:
        if w <= c:
            c -= w
            r += 1
        else:
            break

    print(r)
```