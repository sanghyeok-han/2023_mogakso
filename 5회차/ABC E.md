# ABC E

## 문제 출처

[https://atcoder.jp/contests/abc290/tasks/abc290_e](https://atcoder.jp/contests/abc290/tasks/abc290_e)

## 문제 설명

수열 X가 있을 때 f(X)를 X를 팰린드롬으로 만들기 위해 필요한 최소의 원소 수정 횟수라고 하자.

수열 A와 A의 길이 N이 주어질 때 A의 모든 연속된 부분 수열의 f(X) 값의 합을 구하여라.

## 문제 풀이

먼저, 위의 정답을 바로 구하는 것보다는 수열의 값이 모두 다를 때의 답에 바꿀 필요가 없는 횟수를 빼는 방법을 사용하는 것이 더욱 간단하다는 것을 파악하여야 한다.

그 후 주어진 각 수의 범위가 N (200000) 이하라는 것을 이용하여 각 수별로 따로 처리할 수 있음을 파악할 수 있다.

또한 만약 전체 길이가 100인 수열에서 왼쪽에서 2번째 원소와 오른쪽에서 5번째 원소가 같다면,

두 원소를 모두 포함하는 총 2개의 연속 부분 수열에서의 연산량이 하나씩 줄어듦을 알 수 있다.

이를 이용하여, 주어진 원소들을 차례대로 순회하면서 각 수별로 [아직 오른쪽이 더 많이 남은 인덱스들의 합, 아직 오른쪽이 더 많이 남은 인덱스들의 최대힙, 왼쪽이 더 많이 남아서 사실상 오른쪽의 길이에 따라갈 수밖에 없는 개수]를 만들어 관리하여 해결할 수 있다.

1 ≤ N ≤ 200000

1 ≤ 각각의 수 ≤ N

## 소스 코드

```python
from heapq import heappush, heappop

n = int(input())
A = list(map(int, input().split()))

total = 0
for cur_len in range(1, n + 1):
    temp_c = cur_len // 2
    total += (n - cur_len + 1) * temp_c
    
info = [[0, [], 0] for _ in range(n + 1)] # inde_sum, indes heap, followed_c
for i in range(n):
    av = A[i]

    left_c = i + 1
    right_c = n - i
    followed_c = info[av][2]
    
    while info[av][1] and -info[av][1][0] >= right_c:
        fav = -heappop(info[av][1])
    
        info[av][0] -= fav
        followed_c += 1
        
    to_minus = info[av][0] + followed_c * right_c
    total -= to_minus
    
    if left_c < right_c:
        info[av][0] += left_c
        heappush(info[av][1], -left_c)
    else:
        followed_c += 1
        
    info[av][2] = followed_c
    
print(total)
```