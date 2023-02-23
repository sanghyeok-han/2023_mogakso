# ABC B

## 문제 출처

[https://atcoder.jp/contests/abc290/tasks/abc290_b](https://atcoder.jp/contests/abc290/tasks/abc290_b)

## 문제 설명

자연수 N이 주어지며, 예선 대회에 참여하는 N명이 있다. 모든 참여자는 다른 등수를 얻었다.

이후 N 길이의 문자열 S가 주어진다. 만약 i등을 한 사람이 본선 진출을 원한다면 i번째는 o로 주어지고, 그렇지 않다면 x로 주어진다.

본선 진출을 원하는 사람들 중 K명만 본선에 참여 가능하다고 할 때 1~N등의 사람 각각 본선 진출 여부를 o, x로 구분해서 하나의 문자열로 붙여서 출력하여라.

 

1 ≤ K ≤ N ≤ 100

주어지는 문자열에는 최소한 K명의 참여를 희망하는 사람이 있다.

## 문제 풀이

주어진 문자열을 앞에서부터 (1등인 사람부터) 순회하면서 해당 사람이 본선 진출을 희망하며, 본선 티켓이 남아있다면 본선 티켓을 하나 사용하고 해당 사람을 본선으로 진출시키면 된다.

## 소스 코드

```python
n, k = map(int, input().split())
s = input()
 
result = ['x'] * n
 
for i in range(n):
    if k and s[i] == 'o':
        k -= 1
        result[i] = 'o'
        
result = ''.join(result)
 
print(result)
```