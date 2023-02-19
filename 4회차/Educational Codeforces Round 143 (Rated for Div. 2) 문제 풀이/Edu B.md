# Edu B

## 문제 출처

[https://codeforces.com/contest/1795/problem/B](https://codeforces.com/contest/1795/problem/B)

## 문제 설명

자연수 n이 주어지며 n개의 서로 다른 1차원 구간 범위의 시작점과 끝점이 주어진다.

f(x)를 좌표 x를 포함하는 구간의 개수라고 하자. 이때 좌표 x가 다른 모든 각각의 좌표 y와 비교했을 때 f(x) > f(y)를 만족한다면 해당 좌표 x를 이상적이라고 하자.

좌표 k가 주어질 때 주어진 구간들 중 원하는 만큼을 제거하거나 그대로 두어  k 좌표를 이상적으로 만들 수 있는지의 여부를 출력하여라.

최대 테스트케이스: 1000개

2 ≤ n, k ≤ 50

1 ≤ 각 구간의 시작점, 각 구간의 끝점 ≤ 50

각 구간의 시작점 ≤ 각 구간의 끝점

## 문제 풀이

좌표 k를 포함하지 않는 구간은 모두 없애는 것이 좋다는 것을 쉽게 알 수 있다. 그렇다면 좌표 k를 포함하는 경우는 어떨까?

만약 좌표 k를 포함하는 구간을 없앨 경우 해당 구간이 포함하고 있을 수 있는 k가 아닌 다른 좌표 x 에서의 f(x) 값이 1 줄어들 수 있겠지만 일단 f(k) 값이 1 줄어드는 것은 확정이므로 해당 구간을 없애는 것이 이득이 되지 않는다는 것을 알 수 있다.

위와 같은 과정을 거친 후 f(k)가 모든 좌표에서 유일한 최댓값인지를 확인하면 된다.

## 소스 코드

```python
import io, os, sys
input = io.BytesIO(os.read(0, os.fstat(0).st_size)).readline

for _ in range(int(input())):
    n, k = map(int, input().split())

    deltas = [0] * 52
    for _ in range(n):
        l, r = map(int, input().split())

        if l <= k <= r:
            deltas[l] += 1
            deltas[r + 1] -= 1

    cur = 0
    curs = [0] * 52
    for i in range(51):
        cur += deltas[i]
        curs[i] = cur

    max_c = -1
    max_c_is = []
    for i in range(51):
        if curs[i] == max_c:
            max_c_is.append(i)
        elif curs[i] > max_c:
            max_c = curs[i]
            max_c_is = [i]

    if len(max_c_is) == 1 and max_c_is[0] == k:
        print('YES')
    else:
        print('NO')
```