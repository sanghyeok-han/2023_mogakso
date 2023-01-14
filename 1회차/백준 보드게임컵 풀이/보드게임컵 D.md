# 보드게임컵 D - Yacht Dice

## 문제 출처

[https://www.acmicpc.net/problem/27159](https://www.acmicpc.net/problem/27162)

## 문제 설명

주사위를 총 세 번 굴린 결과가 주어지고 나머지 두 번을 굴려야 할 때 다음과 같은 주사위 게임 족보를 통해 얻을 수 있는 최대 점수는 무엇인가? 이때 과거에 이용했던 족보는 이용할 수 없는데 이러한 족보 또한 입력을 통해 주어진다.

주사위 게임 족보는 다음과 같다.

- **Ones**: 1이 나온 주사위의 눈 수의 총합.
- **Twos**: 2가 나온 주사위의 눈 수의 총합.
- **Threes**: 3이 나온 주사위의 눈 수의 총합.
- **Fours**: 4가 나온 주사위의 눈 수의 총합.
- **Fives**: 5가 나온 주사위의 눈 수의 총합.
- **Sixes**: 6이 나온 주사위의 눈 수의 총합.
- **Four of a Kind**: 동일한 주사위 눈이 **4개 이상**이라면, 동일한 주사위 눈 **개**의 총합. 아니라면 0점.
- **Full House**: 주사위 눈이 **정확히 두 종류**로 이루어져 있고 한 종류는 3개, 다른 종류는 2개일 때, 주사위 눈 5개의 총합. 아니라면 0점.
- **Little Straight**: 주사위 눈이 1, 2, 3, 4, 5의 조합이라면, 즉 1에서 5까지의 눈이 한 번씩 등장했다면 30점, 아니라면 0점.
- **Big Straight**: 주사위 눈이 2, 3, 4, 5, 6의 조합이라면, 즉 2에서 6까지의 눈이 한 번씩 등장했다면 30점, 아니라면 0점.
- **Yacht**: 동일한 주사위 눈이 5개라면 50점, 아니라면 0점.
- **Choice**: 모든 주사위 눈의 총합.

## 문제 풀이

완전탐색을 이용해 남은 두 차례에 나올 수 있는 경우를 모두 만들어 준 뒤 각각을 미리 주어진 3개의 결과와 병합하여 점수를 계산하며, 그 중 최댓값을 출력하면 된다.

각각의 경우에 대해 점수를 계산할 때는 현재 사용할 수 있는 모든 족보를 통해 점수를 독립적으로 산출해보아야 한다.

## 소스 코드

```python
from collections import Counter

def get_v(li, tp):
    if tp <= 5:
        return li.count(tp + 1) * (tp + 1)
    
    sli = sorted(li)
    ct = Counter(li)
    mc = ct.most_common()
    if tp == 6:
        if mc[0][1] >= 4:
            return mc[0][0] * 4
        else:
            return 0
    elif tp == 7:
        if len(mc) == 2 and mc[0][1] == 3 and mc[1][1] == 2:
            return sum(li)
        else:
            return 0
    elif tp == 8:
        if sli == [1, 2, 3, 4, 5]:
            return 30
        else:
            return 0
    elif tp == 9:
        if sli == [2, 3, 4, 5, 6]:
            return 30
        else:
            return 0
    elif tp == 10:
        if mc[0][1] == 5:
            return 50
        else:
            return 0
    elif tp == 11:
        return sum(li)
    
    
s = input()
li = list(map(int, input().split()))

max_sc = 0
for a in range(1, 7):
    for b in range(1, 7):
        nli = li + [a, b]
        
        for i in range(12):
            if s[i] == 'Y':
                sc = get_v(nli, i)
                
                max_sc = max(max_sc, sc)
                
print(max_sc)
```