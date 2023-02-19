# Edu D

## 문제 출처

[https://codeforces.com/contest/1795/problem/D](https://codeforces.com/contest/1795/problem/D)

## 문제 설명

6의 배수인 자연수 n이 주어지며, n개의 정점과 n개의 간선을 가지고 있는 무방향 그래프가 있다.

이때 모든 정점이 정점 번호가 작은 순에서 큰 순으로 차례대로 3개씩 쌍을 이루게 된다. 예시로 1, 2, 3이 한 그룹에 속하고, 4, 5, 6은 또 다른 그룹에 속하게 된다. 각 그룹에 속한 모든 정점은 해당 그룹에 속한 모든 다른 정점과 간선으로 연결되어 있다.

이후 모든 정점을 빨간색 또는 파란색으로 색칠하려고 한다. 또한 빨간색을 가진 정점의 개수와 파란색을 가진 정점의 수는 동일하여야 한다.

서로 다른 색깔의 정점을 잇는 간선의 가중치의 합을 그래프의 종합 가중치라고 하자.

또한 각 정점들을 위의 규칙에 맞게 색칠하면서 얻을 수 있는 그래프의 종합 가중치의 최댓값을 W라고 하자.

이후 n개의 간선의 가중치 정보가 주어지며, 해당 정보는 차례대로 정점 1과 2, 1과 3, 2와 3, 4와 5, 4와 6, 5와 6을 잇는 방식으로 주어진다.

각 정점들을 위의 규칙에 맞게 색칠할 때 W를 얻을 수 있는 경우의 수를 998244353로 나눈 나머지를 구하여라.

6 ≤ n ≤ 300000, n은 6의 배수

1 ≤ 각 간선의 가중치 ≤ 1000

## 문제 풀이

각 정점을 색칠했을 때 그래프의 종합 가중치가 W가 되려면 각각의 그룹에서 최선의 방법으로 색칠해야 한다는 것을 알 수 있다. 이때 각 그룹별로 빨간색과 파란색을 1, 2 또는 2, 1번 칠해야 최적의 값이 나온다는 것을 알 수 있다.

이때 어떤 그룹은 빨간색으로 칠한 정점이 1개이며, 어떤 그룹은 2개가 될 수 있다는 것을 알 수 있으며, 또한 위의 두 경우의 수는 동일하다는 것을 알 수 있다.

각 그룹별로 위의 두 경우 중 하나로 분배해주는 경우의 수는 (n/3)C(n/6) 만큼 있다.

그 후, 그룹별로 모든 간선의 가중치가 같을 경우와 간선의 가중치 3개 중 작은 2개의 가중치가 서로 같은 경우에 해당하는지의 여부를 구해서 위의 두 경우의 총 개수들을 구해준 후 최종 경우의 수에 반영해주면 된다.

## 소스 코드

```python
mod = 998244353

max_num = 310000

factos = [0] * (max_num + 1)
factos[0] = 1
invs = [0] * (max_num + 1)
cur = 1
for i in range(1, max_num + 1):
    cur *= i
    cur %= mod
    factos[i] = cur
    
invs[max_num] = pow(factos[max_num], mod - 2, mod)
for i in range(max_num - 1, -1, -1):
    invs[i] = (i + 1) * invs[i + 1] % mod

def nCk(n, k):
    if n < k:
        return 0
    if k < 0:
        return 0
    return factos[n] * invs[k] * invs[n - k] % mod

n = int(input())
li = list(map(int, input().split()))

all_same_c = 0
small_two_same_c = 0
for i in range(0, n, 3):
    temp = [li[i], li[i + 1], li[i + 2]]
    temp.sort()
    
    if li[i] == li[i + 1] == li[i + 2]:
        all_same_c += 1
    elif temp[0] == temp[1]:
        small_two_same_c += 1
        
t1 = nCk(n // 3, n // 6) % mod
t2 = pow(3, all_same_c, mod)
t3 = pow(2, small_two_same_c, mod)

result = t1 * t2 * t3
result %= mod

print(result)
```