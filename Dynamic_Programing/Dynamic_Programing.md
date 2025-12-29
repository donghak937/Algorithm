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

### 4. 2차원 동적 계획법 (2D Dynamic Programming)
상태가 두 개의 변수로 정의될 때 사용합니다. 주로 2차원 배열(Grid)에서의 경로 문제나, 두 개의 문자열 비교(LCS), 배낭 문제(Knapsack) 등이 있습니다.

#### 예시: 최소 경로 합 (Minimum Path Sum)
`m x n` 그리드에서 왼쪽 위(0,0)에서 오른쪽 아래(m-1, n-1)까지 이동할 때, 지나는 칸의 숫자의 합이 최소가 되도록 하는 문제입니다 (아래 또는 오른쪽으로만 이동 가능).

**점화식 (Recurrence Relation):**
`dp[i][j]` = `grid[i][j]` + `min(dp[i-1][j], dp[i][j-1])`
- `dp[i][j]`: (0,0)에서 (i,j)까지의 최소 합
- 현재 칸의 값(`grid[i][j]`)에 위쪽(`dp[i-1][j]`)이나 왼쪽(`dp[i][j-1]`) 중 더 작은 값을 더합니다.

```python
def min_path_sum(grid):
    rows = len(grid)
    cols = len(grid[0])
    
    # 2차원 DP 테이블 초기화
    dp = [[0] * cols for _ in range(rows)]
    
    dp[0][0] = grid[0][0]
    
    # 첫 번째 열 초기화 (위에서만 올 수 있음)
    for i in range(1, rows):
        dp[i][0] = dp[i-1][0] + grid[i][0]
        
    # 첫 번째 행 초기화 (왼쪽에서만 올 수 있음)
    for j in range(1, cols):
        dp[0][j] = dp[0][j-1] + grid[0][j]
        
    # 나머지 칸 채우기
    for i in range(1, rows):
        for j in range(1, cols):
            dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
            
    return dp[rows-1][cols-1]
```
    