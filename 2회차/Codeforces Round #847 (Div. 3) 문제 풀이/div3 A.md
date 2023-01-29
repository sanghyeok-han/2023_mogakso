# div3 A

## 문제 출처

[https://codeforces.com/contest/1790/problem/A](https://codeforces.com/contest/1790/problem/A)

## 문제 설명

길이가 30 이하인 0-9까지의 숫자들로 이루어진 문자열이 주어질 때 앞부분부터 몇 개의 숫자가 원주율 π 값의 앞부분부터의 값하고 같은지 그 개수를 구하시오. 

이때  π의 소숫점은 때고 계산하여야 한다.

## 문제 풀이

예제의 테스트 케이스 중에 π의 30번째 값까지 주어진 것이 있으므로 이를 참고하여 주어진 문자열의 앞부분부터 순회하면서 일치할 때마다 정답을 1 추가해주고 문자열이 끝나거나 일치하지 않으면 반복문을 종료해주면 된다.

## 소스 코드

```python
import sys
input = lambda: sys.stdin.readline().rstrip()

pi = '314159265358979323846264338327'

for _ in range(int(input())):
    s = input()
    n = len(s)
    
    r = 0
    for i in range(n):
        if pi[i] == s[i]:
            r += 1
        else:
            break
            
    print(r)
```

[문제 설명](https://www.notion.so/95f6707ae968431eb8eace98ad12b7fc)