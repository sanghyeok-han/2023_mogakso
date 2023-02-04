# div4 B

## 문제 출처

[https://codeforces.com/contest/1790/problem/B](https://codeforces.com/contest/1791/problem/B)

## 문제 설명

현재 (0, 0) 좌표에 위치해 있으며, 이동할 방향들을 의미하는 문자열이 주어진다.

이때 각 문자는 ‘U’, ‘D’, ‘L’, ‘R’ 중의 하나이며, 이는 각각 상하좌우로 한 칸씩 이동함을 의미한다. 

이때 이동 중에 (1, 1) 좌표에 위치에 있는 경우가 있으면 ‘YES’를, 아니면 ‘NO’를 출력하시오.

## 문제 풀이

(0, 0)에서 시작하여 주어진 문자열의 방향대로 차례대로 이동해보면서 (1, 1)를 지나는 경우가 있는지를 확인하면 된다.

## 소스 코드

```python
import sys
input = lambda: sys.stdin.readline().rstrip()

# L R D U
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]
alphas = 'LRDU'

for _ in range(int(input())):
    n = int(input())
    s = input()

    x = y = 0
    ip = False
    for v in s:
        d = alphas.index(v)

        x += dx[d]
        y += dy[d]

        if x == y == 1:
            ip = True
            break

    if ip:
        print('YES')
    else:
        print('NO')
```