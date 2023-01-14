# 보드게임컵 B - 할리갈리

## 문제 출처

[https://www.acmicpc.net/problem/27159](https://www.acmicpc.net/problem/27159)

## 문제 설명

총 4종류의 과일이 그려진 카드가 여러 장 주어지며, 입력은 과일 이름, 해당 카드의 개수의 쌍으로 주어진다.

이때 한 종류 이상의 과일이 정확히 5개 있으면 ‘YES’를 출력하고 아니면 ‘NO’를 출력하여야 한다.

## 문제 풀이

각각의 입력을 차례대로 받으면서 각 과일별 개수를 파이썬으로는 딕셔너리, c++로는 맵을 이용하여 누적해서 더해준다.

과일 중 개수가 5인 것이 하나라도 있으면 ‘YES’를 출력하고 아니면 ‘NO’를 출력하면 된다.

## 소스 코드

```python
from collections import defaultdict as dd
import sys
input = lambda: sys.stdin.readline().rstrip()

n = int(input())
ct = dd(int)

for _ in range(n):
    name, c = input().split()
    c = int(c)
    
    ct[name] += c
    
result = False
for v in ct.values():
    if v == 5:
        result = True
        break
        
if result:
    print('YES')
else:
    print('NO')
```