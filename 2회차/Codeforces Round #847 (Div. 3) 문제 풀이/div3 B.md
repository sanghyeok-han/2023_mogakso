# div3 B

## 문제 출처

[https://codeforces.com/contest/1790/problem/B](https://codeforces.com/problemset/problem/1790/B)

## 문제 설명

1-6까지 쓰여있는 주사위 n개가 있다. n 개의 주사위를 모두 굴렸을 때 윗면에 쓰인 숫자의 합 s, s에서 윗면에 쓰인 숫자들의 최댓값 하나를 뺀 값을 r이라고 한다.

n, s, r이 주어졌을 때 가능한 n개의 주사위 윗면의 조합을 아무거나 출력하시오.

최대 테스트케이스: 1000개

2 ≤ n ≤ 50

1 ≤ r < s ≤ 300

## 문제 풀이

먼저 s - r의 값이 던져진 주사위 윗면들의 최댓값이라는 것을 알 수 있다.

그 후 n - 1개의 주사위의 윗면의 합이 r이라는 것을 이용해서 n - 1개의 주사위에 적절하게 배분해주어야 한다.

이때 각각의 주사위에 1씩을 배분하는 작업을 배분한 값의 합이 r이 될 때까지 반복해주면 된다.

## 소스 코드

```python
import io, os, sys
input = io.BytesIO(os.read(0, os.fstat(0).st_size)).readline
 
for _ in range(int(input())):
    n, s, r = map(int, input().split())
 
    result = [0] * n
    result[-1] = s - r
 
    i = 0
    while r:
        r -= 1
        result[i] += 1
 
        i += 1
        if i == n - 1:
            i = 0
 
    print(*result)
```