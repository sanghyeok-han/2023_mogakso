# Edu C

## 문제 출처

[https://codeforces.com/contest/1795/problem/C](https://codeforces.com/contest/1795/problem/C)

## 문제 설명

자연수 n이 주어지며, n개의 마시는 차와 n명의 사람이 있다.

이후 각 차의 현재 양이 주어진다. 또한 각 사람이 한번에 최대 얼마를 마실 수 있는지가 주어진다.

각 사람들이 차를 시음하는 과정은 다음과 같이 이루어진다.

먼저 i번째 사람은 i번째 차를 마실 수 있는만큼 마신다.

그 후 i번째 사람은 i - 1번째의 차를 마시며, 이때 첫 번째 사람은 더 이상 차를 마시지 않게 된다.

그 후 i번째 사람은 i - 2번째의 차를 마시며, 이때 두 번째 사람은 더 이상 차를 마시지 않게 된다.

이러한 과정을 마지막 사람이 차를 마시지 못할 때까지 진행했을 때 각 사람들이 마신 차의 양을 출력하여라.

최대 테스트 케이스 개수: 10000

1 ≤ n ≤ 200000

1 ≤ 각 차의 양, 각 사람이 한번에 마실 수 있는 최대 양 ≤ 1000000000

모든 테스트 케이스에서의 n의 합 ≤ 200000 

## 문제 풀이

각 인덱스를 차례대로 순회하면서 현재 인덱스에 해당하는 차의 양 + 이전 사람들이 마신 누적량 (이하 pre_used)를 멀티셋에 추가하며 멀티셋에 있는 값 중에서 현재 인덱스에 해당하는 사람이 최대로 마실 수 있는 양 (이하 can_use)과 pre_used를 더한 값보다 작은 값들은 현재 사람까지만 마실 수 있으므로 현재 사람이 마신 양에 더해주고 멀티셋에서 제거해준다.

이제 멀티셋에 남은 값들은 전부 해당 사람이 최대로 마셔도 남는 것들밖에는 없게 된다.

그러므로 멀티셋 길이 * 해당 사람이 한번에 최대 마실 수 있는 양을 현재 사람이 마신 양에 더해준다.

이러한 과정을 통해 각 사람이 최종적으로 마신 차의 양을 구할 수 있다.

## 소스 코드

```python
import io, os, sys
input = io.BytesIO(os.read(0, os.fstat(0).st_size)).readline

# https://github.com/tatyam-prime/SortedSet/blob/main/SortedMultiset.py
import math
from bisect import bisect_left, bisect_right, insort
from typing import Generic, Iterable, Iterator, TypeVar, Union, List
T = TypeVar('T')

class SortedMultiset(Generic[T]):
    BUCKET_RATIO = 50
    REBUILD_RATIO = 170

    def _build(self, a=None) -> None:
        "Evenly divide `a` into buckets."
        if a is None: a = list(self)
        size = self.size = len(a)
        bucket_size = int(math.ceil(math.sqrt(size / self.BUCKET_RATIO)))
        self.a = [a[size * i // bucket_size : size * (i + 1) // bucket_size] for i in range(bucket_size)]
    
    def __init__(self, a: Iterable[T] = []) -> None:
        "Make a new SortedMultiset from iterable. / O(N) if sorted / O(N log N)"
        a = list(a)
        if not all(a[i] <= a[i + 1] for i in range(len(a) - 1)):
            a = sorted(a)
        self._build(a)

    def __iter__(self) -> Iterator[T]:
        for i in self.a:
            for j in i: yield j

    def __reversed__(self) -> Iterator[T]:
        for i in reversed(self.a):
            for j in reversed(i): yield j
    
    def __len__(self) -> int:
        return self.size
    
    def __repr__(self) -> str:
        return "SortedMultiset" + str(self.a)
    
    def __str__(self) -> str:
        s = str(list(self))
        return "{" + s[1 : len(s) - 1] + "}"

    def _find_bucket(self, x: T) -> List[T]:
        "Find the bucket which should contain x. self must not be empty."
        for a in self.a:
            if x <= a[-1]: return a
        return a

    def __contains__(self, x: T) -> bool:
        if self.size == 0: return False
        a = self._find_bucket(x)
        i = bisect_left(a, x)
        return i != len(a) and a[i] == x

    def count(self, x: T) -> int:
        "Count the number of x."
        return self.index_right(x) - self.index(x)

    def add(self, x: T) -> None:
        "Add an element. / O(√N)"
        if self.size == 0:
            self.a = [[x]]
            self.size = 1
            return
        a = self._find_bucket(x)
        insort(a, x)
        self.size += 1
        if len(a) > len(self.a) * self.REBUILD_RATIO:
            self._build()

    def discard(self, x: T) -> bool:
        "Remove an element and return True if removed. / O(√N)"
        if self.size == 0: return False
        a = self._find_bucket(x)
        i = bisect_left(a, x)
        if i == len(a) or a[i] != x: return False
        a.pop(i)
        self.size -= 1
        if len(a) == 0: self._build()
        return True

    def lt(self, x: T) -> Union[T, None]:
        "Find the largest element < x, or None if it doesn't exist."
        for a in reversed(self.a):
            if a[0] < x:
                return a[bisect_left(a, x) - 1]

    def le(self, x: T) -> Union[T, None]:
        "Find the largest element <= x, or None if it doesn't exist."
        for a in reversed(self.a):
            if a[0] <= x:
                return a[bisect_right(a, x) - 1]

    def gt(self, x: T) -> Union[T, None]:
        "Find the smallest element > x, or None if it doesn't exist."
        for a in self.a:
            if a[-1] > x:
                return a[bisect_right(a, x)]

    def ge(self, x: T) -> Union[T, None]:
        "Find the smallest element >= x, or None if it doesn't exist."
        for a in self.a:
            if a[-1] >= x:
                return a[bisect_left(a, x)]
    
    def __getitem__(self, x: int) -> T:
        "Return the x-th element, or IndexError if it doesn't exist."
        if x < 0: x += self.size
        if x < 0: raise IndexError
        for a in self.a:
            if x < len(a): return a[x]
            x -= len(a)
        raise IndexError

    def index(self, x: T) -> int:
        "Count the number of elements < x."
        ans = 0
        for a in self.a:
            if a[-1] >= x:
                return ans + bisect_left(a, x)
            ans += len(a)
        return ans

    def index_right(self, x: T) -> int:
        "Count the number of elements <= x."
        ans = 0
        for a in self.a:
            if a[-1] > x:
                return ans + bisect_right(a, x)
            ans += len(a)
        return ans

for _ in range(int(input())):
    n = int(input())
    A = list(map(int, input().split()))
    B = list(map(int, input().split()))

    totals = [0] * n
    pre_used = 0
    ms = SortedMultiset()
    for bi in range(n):
        ms.add(A[bi] + pre_used)
        can_use = B[bi]

        while ms and ms[0] <= pre_used + can_use:
            to_use = ms[0] - pre_used
            totals[bi] += to_use
            ms.discard(ms[0])

        totals[bi] += len(ms) * can_use
        pre_used += can_use

    print(*totals)
```