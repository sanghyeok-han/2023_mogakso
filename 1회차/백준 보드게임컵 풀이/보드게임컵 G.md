# 보드게임컵 G - 모든 곳을 안전하게

## 문제 출처

[https://www.acmicpc.net/problem/27165](https://www.acmicpc.net/problem/27165)

## 문제 설명

0번부터 n번까지 왼쪽부터 순서대로 번호가 매겨진 n + 1 칸이 있으며, 주사위의 눈이 1부터 n까지 있는 게임판이 있다.  각 칸에는 말이 있을 수 있으며, 동일한 칸에 말이 여러 개 있을 수도 있다.

말 하나를 x만큼 이동하여 모든 칸의 말의 개수가 0개 혹은 2개 이상이 되게 할 수 있는지를 구하여라.

현재 각 칸에 있는 말의 수는 입력으로 주어진다.

## 문제 풀이

각 칸의 말의 개수를 세서 1개인 칸이 세 칸이면 무조건 불가능해진다.

한 칸이라면 해당 칸의 말을 이동시킬지, 해당 칸으로 말을 이동시킬지의 경우를 나눠서 확인해볼 수 있으며,

두 칸이라면 왼쪽 칸에서 오른쪽 칸으로 말을 하나 이동시키는 경우를 확인해보면 된다.

그러한 칸이 하나도 없다면 모든 칸의 말을 독립적으로 이동시켜보면서 시작점의 말 개수와 도착점의 말 개수 중 어느 것도 1개가 되지 않게 할 수 있는 지를 보면 된다. 

## 소스 코드

```python
n = int(input())
li = list(map(int, input().split()))
x = int(input())

st = set()
for i in range(n + 1):
    if li[i] == 1:
        st.add(i)
        
st_len = len(st)
        
if st_len >= 3:
    print('NO')
elif st_len == 2:
    left, right = sorted(st)
    
    if left + x == right:
        print('YES')
        print(left, right)
    else:
        print('NO')
elif st_len == 1:
    v = st.pop()
    
    if v - x >= 0 and li[v - x] >= 3:
        print('YES')
        print(v - x, v)
    elif v + x < n and li[v + x] != 0:
        print('YES')
        print(v, v + x)
    else:
        print('NO')
elif st_len == 0:
    ip = False
    for i in range(n + 1 - x):
        if li[i] >= 3 and li[i + x] != 0:
            ip = True
            
            print('YES')
            print(i, i + x)
            break
    
    if not ip:
        print('NO')
```