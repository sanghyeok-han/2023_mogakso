# div3 C

## 문제 출처

[https://codeforces.com/contest/1790/problem/C](https://codeforces.com/problemset/problem/1790/C)

## 문제 설명

1부터 n까지의 수가 하나씩 쓰인 순열이 하나 있다.

이때 이 순열의 첫번째에서 마지막까지 하나씩의 값이 없는 (n - 1) 길이의 수열 n개가 주어진다.

이때 주어진 수열들을 통해 원본 수열을 유추하여 출력하여라.

최대 테스트 케이스 개수: 10000

3 ≤ n ≤ 100

## 문제 풀이

일단 주어진 수열의 첫 번째 원소들만 본다면 첫 번째 원소가 빠진 하나를 제외한 나머지 수열들은 전부 첫 번째 원소가 첫 번째 위치에 있을 것임을 알 수 있다.

그러므로 이를 통해 원본 순열의 첫 번째 원소가 모든 주어진 수열의 첫 번째 값으로 여러 번 등장하는 수라는 것을 알 수 있다.

이제 첫 번째 값을 구하였으며, 이 값을 첫 번째 원소를 제외한 모든 원소가 있는 수열의 첫 번째로 만들면 정답이 된다.

## 소스 코드

```python
import io, os, sys
input = io.BytesIO(os.read(0, os.fstat(0).st_size)).readline

for _ in range(int(input())):
    n = int(input())
    li = [list(map(int, input().split())) for _ in range(n)]

    st = set()
    temp = []
    for i in range(n):
        st.add(li[i][0])
        temp.append(li[i][0])

    fs_i = -1
    for v in st:
        if temp.count(v) == 1:
            fs_i = temp.index(v)
            st.discard(v)

            break

    print(*([st.pop()] + li[fs_i]))
```