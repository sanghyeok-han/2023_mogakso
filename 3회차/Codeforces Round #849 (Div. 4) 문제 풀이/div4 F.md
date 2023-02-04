# div4 F

## 문제 출처

[https://codeforces.com/contest/1791/problem/F](https://codeforces.com/contest/1791/problem/F)

## 문제 설명

길이가 n인 배열 a가 주어지며, 각각의 원소의 값의 범위는 1 이상 1^9 이하이다.

또한 처리해야할 q개의 쿼리가 주어지며 쿼리의 종류는 다음과 같다.

- 1 l r: l ≤ 인덱스 ≤ r에 속하는 각각의 인덱스에 해당하는 값을 해당 값을 구성하는 각각의 숫자들의 합으로 바꾼다.
- 2 x: a 배열의 x 인덱스의 값을 출력한다.

2번 쿼리가 들어올 때마다 그때의 정답을 출력하여라.

1 ≤ 테스트 케이스의 수 ≤ 1000

1 ≤ n, q ≤ 200000

모든 테스트 케이스에서의 n 값의 합 ≤ 200000

모든 테스트 케이스에서의 q 값의 합 ≤ 200000

## 문제 풀이

모든 원소가 0인 세그먼트 트리를 먼저 구축한 후에 1번 쿼리가 주어질 때마다 l에 해당하는 원소를 +1 해주며, r + 1에 해당하는 원소를 -1 해주는 방식을 사용하며, 2번 쿼리가 주어질 때 0~x 범위의 합을 구하면 이 값이 해당 값에 적용될 위의 과정을 진행할 횟수가 된다.

이때 먼저 특정 수를 해당 수의 각각의 숫자값의 합으로 다시 할당하는 과정을 진행하면서 해당 수가 0~9가 되면 더 이상 과정을 진행할 필요가 없어진다는 것을 알 수 있다.

그러므로 2번 쿼리가 주어진다면 해당 수가 0~9가 된다면 더 이상 과정을 진행하지 않고 종료하는 식으로 해당 수의 최종 값을 구하여 출력하면 된다.

## 소스 코드

```python
import sys
input = lambda: sys.stdin.readline().rstrip()

class SegmentTree:
    def __init__(self, data, default=10**15, func=lambda a, b: max(a,b)):
        """initialize the segment tree with data"""
        self._default = default
        self._func = func
        self._len = len(data)
        self._size = _size = 1 << (self._len - 1).bit_length()
 
        self.data = [default] * (2 * _size)
        self.data[_size:_size + self._len] = data
        for i in reversed(range(_size)):
            self.data[i] = func(self.data[i + i], self.data[i + i + 1])
 
    def __delitem__(self, idx):
        self[idx] = self._default
 
    def __getitem__(self, idx):
        return self.data[idx + self._size]
 
    def __setitem__(self, idx, value):
        idx += self._size
        self.data[idx] = value
        idx >>= 1
        while idx:
            self.data[idx] = self._func(self.data[2 * idx], self.data[2 * idx + 1])
            idx >>= 1
 
    def __len__(self):
        return self._len
 
    def query(self, start, stop):
        if start == stop:
            return self.__getitem__(start)
        stop += 1
        start += self._size
        stop += self._size
 
        res = self._default
        while start < stop:
            if start & 1:
                res = self._func(res, self.data[start])
                start += 1
            if stop & 1:
                stop -= 1
                res = self._func(res, self.data[stop])
            start >>= 1
            stop >>= 1
        return res
 
    def __repr__(self):
        return "SegmentTree({0})".format(self.data)
    
func = lambda a, b: a + b

for _ in range(int(input())):
    n, q = map(int, input().split())
    li = input().split()

    seg = SegmentTree([0] * (n + 1), 0, func=func)

    for i in range(q):
        tp, *qu = map(int, input().split())

        if tp == 1:
            l, r = qu[0], qu[1]
            l -= 1
            r -= 1

            seg[l] += 1
            seg[r + 1] -= 1
        else:
            x = qu[0]
            x -= 1

            sv = seg.query(0, x)

            cur = li[x]
            for _ in range(sv):
                if len(cur) == 1:
                    break

                ncur = 0
                for v in cur:
                    ncur += int(v)
                cur = str(ncur)

            print(cur)
```