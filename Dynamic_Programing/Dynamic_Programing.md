# Dynamic Programming (동적 계획법)

다이나믹 프로그래밍은 복잡한 문제를 더 작은 하위 문제로 나누어 해결하고, 그 결과를 저장하여 동일한 계산을 반복하지 않음으로써 효율성을 높이는 알고리즘 설계 기법입니다.

### 1. 핵심 조건
- **Overlapping Subproblems (중복되는 부분 문제):** 동일한 작은 문제들이 반복적으로 발생할 때.
- **Optimal Substructure (최적 부분 구조):** 부분 문제의 최적 해결 방법으로 전체 문제의 최적 해결 방법을 찾을 수 있을 때.

### 2. 구현 방식
- **Top-down (Memoization):** 재귀를 이용하며, 계산된 결과를 메모리에 저장(Memo)하여 중복 계산을 방지합니다.
- **Bottom-up (Tabulation):** 반복문을 이용하며, 작은 문제부터 차례대로 해결하여 테이블을 채워 나갑니다.

### 3. 예시: 피보나치 수열 (Python)
```python
# Bottom-up 방식
def fibonacci(n):
    if n <= 1: return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```
    