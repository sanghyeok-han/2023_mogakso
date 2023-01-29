# div3 E

## 문제 출처

[https://codeforces.com/contest/1790/problem/E](https://codeforces.com/contest/1790/problem/E)

## 문제 설명

1 ≤ x ≤ 2 ^ 29인 x가 주어질 때 x = a xor b = (a + b) / 2이며, (0 < a, b ≤ 2 ** 32)인 a와 b의 값을 아무거나 하나 찾아서 출력하여라.

만약 주어진 x에서의 a, b가 존재하지 않는다면 -1를 출력하면 된다.

## 문제 풀이

이 문제를 풀기 위해서는 먼저 a + b = a xor b + 2 * (a and b) 라는 공식을 알고 있어야 풀기 수월해진다.

주어진 수식 x = a xor b = (a + b) / 2와 a + b = a xor b + 2 * (a and b)를 이용하여 식 정리를 하게 되면 a xor b = 2 * (a and b)라는 식을 얻을 수 있다.

이때 a xor b과 a and b를 직접 0과 1의 비트 표현으로 적어본다면, 각각 1010, 10100 같이 a and b의 비트 표현 뒤에 0이 하나 붙은 것이 a xor b가 된다는 것을 알 수 있다.

이를 통해 a xor b의 비트 표현의 가장 오른쪽 값은 무조건 0이어야 한다는 것을 알 수 있다. 그러므로 주어진 식에서 x = a xor b이므로 x가 홀수이면 비트 표현 가장 오른쪽 값이 1이 되므로 x가 홀수일 경우에는 무조건 -1를 출력하여야 한다는 것을 알 수 있다.

그 다음 확인해 볼 것으로는, a xor b와 a and b의 각각의 비트 자리를 확인해보면서 a, b의 해당 자리 비트가 무슨 값을 가져야 a xor b와 a and b에서의 해당 자리 비트 값이 성립하는 지를 보는 것이다.

a를 b보다 크거나 같은 수로 만들고 위의 과정을 통해서 확인해보면서 a, b의 각각의 비트값을 차례대로 결정해 나갈 수 있다. 이때 불가능한 경우가 나오면 답이 -1임을 알 수 있다.

## 소스 코드

```python
import io, os, sys
input = io.BytesIO(os.read(0, os.fstat(0).st_size)).readline

for _ in range(int(input())):
    n, s, r = map(int, input().split())

    result = [0] * n
    result[-1] = s - r

    i = 0
    while r:
        r -= 1
        result[i] += 1

        i += 1
        if i == n - 1:
            i = 0

    print(*result)
```