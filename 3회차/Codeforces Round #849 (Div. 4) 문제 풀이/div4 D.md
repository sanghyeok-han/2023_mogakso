# div4 D

## 문제 출처

[https://codeforces.com/contest/1790/problem/D](https://codeforces.com/contest/1791/problem/D)

## 문제 설명

f(x) 함수를 문자열 x에 속하는 서로 다른 문자의 개수라고 하자.

문자열 s가 주어졌을 때 s를 길이가 1 이상인 문자열 a,  b로 나누고 f(a) + f(b)를 구할 때 가능한 f(a) + f(b) 값의 최댓값을 구하여라.

1 ≤ 테스트 케이스의 개수 ≤ 10000

2 ≤ 문자열의 길이 ≤ 200000

문자열은 영문 소문자로만 이루어져 있다.

## 문제 풀이

먼저 왼쪽 배열, 오른쪽 배열에 속한 각 알파벳의 수를 저장할 배열을 각각 만들어주고 이를 각각 ct_l, ct_r이라고 하자.

그 후 먼저 전체 배열에서의 각 알파벳의 개수를 각각 구해준 후 이를 ct_r에 할당한다.

이제 첫 원소부터 n - 1번째 원소까지 차례로 ct_r에서 ct_l로 옮겨주면서 각각의 f(왼쪽 배열) + f(오른쪽 배열)을 구한 다음에 이 중 최댓값을 정답으로 하면 된다.

 

## 소스 코드

```python
import sys
input = lambda: sys.stdin.readline().rstrip()

get_value = lambda x: ord(x) - 97

for _ in range(int(input())):
    n = int(input())
    li = list(map(get_value, input()))

    ct_l = [0] * 26
    ct_r = [0] * 26
    for i in range(n):
        v = li[i]

        ct_r[v] += 1

    max_c = 0
    for i in range(n - 1):
        v = li[i]

        ct_r[v] -= 1
        ct_l[v] += 1

        c = 0
        for i in range(26):
            if ct_l[i] > 0:
                c += 1
            if ct_r[i] > 0:
                c += 1

        max_c = max(max_c, c)

    print(max_c)
```