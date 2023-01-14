# 보드게임컵 N - 수 나누기 게임

## 문제 출처

[https://www.acmicpc.net/problem/27165](https://www.acmicpc.net/problem/27172)

## 문제 설명

각각의 플레이어는 1부터 1000000까지의 서로 다른 수가 적힌 카드를 가지고 있다.

모든 플레이어는 자신을 제외한 다른 모든 플레어의 카드와 한 번씩 비교해보며 다음과 같이 점수를 산출하게 된다.

만약 현재 카드의 수가 a이고 비교할 다른 카드의 수가 b일 때 a가 b의 약수이면 a 카드를 가진 플레이어는 1점을 획득하고 상대는 1점을 잃는다.

각 플레이어가 가진 카드에 적힌 수들이 주어졌을 때 모든 비교가 끝난 후 각 플레이어별 점수를 구하여라.

## 문제 풀이

각 원소별로 순회하면서 백만 이하의 모든 배수를 확인하며 있는지의 여부를 검사해주며 현재 원소의 인덱스가 ai, 현재 원소의 배수인 인덱스가 bi일 때 각각의 점수에서 1을 더하고 빼주면 된다.

이때 각 수의 배수가 아닌 약수를 모두 구하게 되면 연산량이 훨씬 늘어나게 되며, 현재 원소의 배수가 있는지의 여부는 주어진 배열을 set으로 변경하여 확인하는 식으로 시간 복잡도를 줄일 수 있다.

## 소스 코드

```python
n = int(input())
li = list(map(int, input().split()))

v_to_i = [-1] * 1000001
for i in range(n):
    v = li[i]
    
    v_to_i[v] = i
    
scs = [0] * n
    
st = set(li)

for cur in li:
    oppo = cur
    while True:
        oppo += cur
        if oppo > 1000000:
            break
        
        if oppo in st:
            cur_i = v_to_i[cur]
            oppo_i = v_to_i[oppo]
            
            scs[cur_i] += 1
            scs[oppo_i] -= 1
        
print(*scs)
```