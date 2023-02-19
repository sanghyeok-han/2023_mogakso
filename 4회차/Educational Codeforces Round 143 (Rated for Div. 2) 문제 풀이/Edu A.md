# Edu A

## 문제 출처

[https://codeforces.com/contest/1795/problem/A](https://codeforces.com/contest/1795/problem/A)

## 문제 설명

빨간색과 파란색 블럭으로 이루어진 타워가 두 개 있으며, 빨간 블럭은 R, 파란 블럭은 B로 표시한다.

이때 블럭이 2개 이상 있는 타워의 경우 가장 위의 블럭을 다른쪽 타워의 가장 위쪽으로 옮기는 작업을 원하는만큼 할 수 있다.

이러한 과정을 통해 각 타워의 인접한 블럭들의 색깔을 모두 다르게 만들 수 있는지의 여부를 출력하여라.

최대 테스트케이스의 개수: 1000

1 ≤ 첫 번째 타워의 길이, 두 번째 타워의 길이 ≤ 20

## 문제 풀이

두 타워가 위쪽끼리 서로 이어진 하나의 문자열로 보자. 이때 인접한 색깔이 서로 다른 경우가 1번 이하 나타난다면 해당 인접한 부분을 각 타워의 꼭대기로 만들어 각 타워의 인접한 블럭들의 색깔을 모두 다르게 만들 수 있다는 것을 알 수 있다.

## 소스 코드

```python
import sys
input = lambda: sys.stdin.readline().rstrip()

for _ in range(int(input())):
    n, m = map(int, input().split())
    s = input()
    t = input()

    ns = s + t[::-1]
    nn = n + m
    same_c = 0
    for i in range(nn - 1):
        if ns[i] == ns[i + 1]:
            same_c += 1

    if same_c <= 1:
        print('YES')
    else:
        print('NO')
```

[문제 설명](https://www.notion.so/5aff98a417874b9aad73d27efc49768b)