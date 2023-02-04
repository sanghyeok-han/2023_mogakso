# div4 E

## 문제 출처

[https://codeforces.com/contest/1791/problem/E](https://codeforces.com/contest/1791/problem/E)

## 문제 설명

길이가 n이며 각각의 원소가 -10^9 이상 10^9 이하인 배열 a가 있다.

이 배열에서 인접한 두 원소를 골라 각 원소의 부호를 바꿔주는 연산을 원하는 만큼 할 수 있다.

이때 배열의 합계로 가능한 최댓값을 구하여라.

1 ≤ 테스트 케이스의 수 ≤ 1000

2 ≤ n ≤ 200000

모든 테스트 케이스에서의 n의 합 ≤ 200000

## 문제 풀이

만약 0이 있는 경우는 - 부호를 전부 없애줄 수 있다.

0이 없을 때 - 부호의 개수가 짝수 개라면 연산을 충분히 진행하여 전부 양수로 바꿔줄 수있으며, - 부호의 개수가 홀수 개라면 전체의 원소 중 절댓값이 가장 작은 하나의 원소를 음수로 두고 나머지는 전부 양수로 둘 수 있다.

위와 같은 과정들을 통해 최댓값을 구할 수 있으며, 이것이 정답이 된다.

## 소스 코드

```python
import io, os, sys
input = io.BytesIO(os.read(0, os.fstat(0).st_size)).readline

for _ in range(int(input())):
    n = int(input())
    li = list(map(int, input().split()))

    ps = []
    ms = []
    c0 = 0
    for v in li:
        if v > 0:
            ps.append(v)
        elif v < 0:
            ms.append(v)
        else:
            c0 += 1

    if c0 >= 1 or len(ms) % 2 == 0:
        r = sum(ps) - sum(ms)
    else:
        li.sort(key=lambda x: -abs(x))
        to_minus = abs(li.pop())
        
        r = 0
        for v in li:
            r += abs(v)
            
        r -= to_minus

    print(r)
```