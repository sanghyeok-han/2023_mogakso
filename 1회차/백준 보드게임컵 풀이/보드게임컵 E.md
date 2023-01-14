# 보드게임컵 E - 벚꽃 내리는 시대에 결투를

## 문제 출처

[https://www.acmicpc.net/problem/27159](https://www.acmicpc.net/problem/27163)

## 문제 설명

방어력을 의미하는 ’오라’와 생명력을 의미하는 ’라이프’가 주어지며 라이프가 0 이하가 되면 즉시 패배하게 된다.

플레이어는 현재 A만큼의 오라, L만큼의 라이프를 가지고 있으며 상대의 N번의 공격을 버텨내어야 한다.

상대의 공격이 가진 공격력은 두 가지의 값 X, Y로 이루어져 있는데, X는 오라 공격력, Y는 라이프 공격력을 의미한다. X, Y는 0 이상의 정수 혹은 -1이며, 둘 다 -1인 경우는 없다.

플레이어는 오라에 X 데미지를 받거나 라이프에 Y 데미지를 받는 것 중 하나를 선택할 수 있으며, 다음과 같은 추가 규칙 또한 적용된다.

- X, Y가 모두 -1가 아닐 때 현재 오라가 X보다 작다면 무조건 라이프에 Y 데미지를 받는다.
- Y가 -1이라면 무조건 오라에 X 데미지를 받는다. 만약 오라가 0 미만이 된다면 다시 0으로 회복된다.
- X가 0이라면 무조건 라이프에 Y 데미지를 받게 된다.

상대의 N번의 공격이 차례대로 주어질 때 과연 플레이어가 각각의 공격에 적절히 대처하여 살아남을 수 있는 지의 여부를 출력해야 하며, 만약 살아남을 수 있다면, 각각의 상대 공격에 대해 어떤 쪽으로 데미지를 받는 것이 올바른 선택인지를 같이 출력하여야 한다.

1 ≤ N ≤ 5000

0 ≤ A ≤ 1e9

1 ≤ L ≤ 5000

모든 X는 -1 ≤ X ≤ 1e9

모든 Y는 -1 ≤ Y ≤ 5000

## 문제 풀이

L이 5000으로 A보다 훨씬 적으며, N이 5000이어서 5000 * 5000 = 25000000으로 1초 이내에 충분히 동작할 수 있다는 것을 활용하여, 현재 턴별 현재 플레이어의 라이프별 가능한 최대 오라를 담을 배열을 만들어서 다이나믹 프로그래밍 알고리즘으로 해결할 수 있다.

또한 생존이 가능할 때는 각 턴별 어떠한 선택을 해야 하는지 출력이 필요하므로 역추적을 위해 dp 테이블의 각 오라별로 해당 값이 이전 턴의 어떤 라이프에서 넘어왔고 어떤 선택을 하였는지도 같이 저장해 주어야 한다.

## 소스 코드

```python
import io, os, sys
input = io.BytesIO(os.read(0,os.fstat(0).st_size)).readline

n, a, l = map(int, input().split())
li = [list(map(int, input().split())) for _ in range(n)]

dp = [[-1] * 5001 for _ in range(n + 1)]
dp[0][l] = a

from_ = [[()] * 5001 for _ in range(n + 1)] # 1: 이전에 A 선택, 2: 이전에 L 선택
for i in range(n):
    x, y = li[i]
    
    for cur_l in range(1, 5001):
        cur_a = dp[i][cur_l]

        if cur_a == -1:
            continue
        
        if x != -1 and y != -1:
            if cur_a >= x:
                n_a = cur_a - x
                n_l = cur_l
                
                if n_a > dp[i + 1][n_l]:
                    dp[i + 1][n_l] = n_a
                    from_[i + 1][n_l] = (cur_l, 'A')

            if cur_l - y > 0:
                n_a = cur_a
                n_l = cur_l - y

                if n_a > dp[i + 1][n_l]:
                    dp[i + 1][n_l] = n_a
                    from_[i + 1][n_l] = (cur_l, 'L')
        elif y == -1:
            n_a = cur_a - x
            n_a = max(0, n_a)
            n_l = cur_l
            
            if n_a > dp[i + 1][n_l]:
                dp[i + 1][n_l] = n_a
                from_[i + 1][n_l] = (cur_l, 'A')
        elif x == -1:
            if cur_l - y > 0:
                n_a = cur_a
                n_l = cur_l - y
                
            if n_a > dp[i + 1][n_l]:
                dp[i + 1][n_l] = n_a
                from_[i + 1][n_l] = (cur_l, 'L')
                
i = n
ip = False
seq = []
for cur_l in range(1, 5001):
    if dp[i][cur_l] >= 0:
        ip = True
        
        for cur_seq in range(n, 0, -1):
            f_l, used = from_[cur_seq][cur_l]
                
            seq.append(used)
            cur_l = f_l
            
        break

if not seq:
    print('NO')
else:        
    print('YES')
    
    seq = ''.join(reversed(seq))
    print(seq)
```