# div4 A

## 문제 출처

[https://codeforces.com/contest/1790/problem/A](https://codeforces.com/contest/1791/problem/A)

## 문제 설명

알파벳이 하나 주어질 때 해당 알파벳이 ‘codeforces’에 속한 알파벳이면 ‘YES’, 아니면 ‘NO’를 출력하시오.

## 문제 풀이

파이썬 문법 in을 이용해서 알파벳의 포함 관계를 확인하면 된다.

## 소스 코드

```python
import sys
input = lambda: sys.stdin.readline().rstrip()
 
for _ in range(int(input())):
    c = input()
 
    if c in 'codeforces':
        print('yes')
    else:
        print('no')
```