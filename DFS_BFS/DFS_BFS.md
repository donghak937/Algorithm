# DFS & BFS (Graph Traversal)

그래프 탐색 알고리즘인 DFS(깊이 우선 탐색)와 BFS(너비 우선 탐색)입니다. 많은 알고리즘 문제의 기초가 되는 중요한 개념입니다.

## 1. DFS (Depth-First Search, 깊이 우선 탐색)
루트 노드(혹은 다른 임의의 노드)에서 시작해서 **다음 분기(Branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색**하는 방법입니다.
- **특징:** 깊게(Deep) 들어가는 것을 우선합니다.
- **구현:** **스택(Stack)** 자료구조 혹은 **재귀 함수(Recursion)**를 사용합니다.
- **용도:** 모든 노드를 방문하고자 할 때, 미로 찾기 등.

### DFS 예제 (C++ - 재귀)
```cpp
#include <iostream>
#include <vector>
using namespace std;

bool visited[9]; // 방문 처리를 위한 배열
vector<int> graph[9]; // 그래프 데이터를 담을 인접 리스트

void dfs(int x) {
    // 현재 노드를 방문 처리
    visited[x] = true;
    cout << x << " ";
    
    // 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for (int i = 0; i < graph[x].size(); i++) {
        int y = graph[x][i];
        if (!visited[y]) {
            dfs(y);
        }
    }
}

int main() {
    // 그래프 연결 (예시)
    // 노드 1에 연결된 노드 정보 저장 
    graph[1].push_back(2);
    graph[1].push_back(3);
    graph[1].push_back(8);
    
    // ... 나머지 노드 연결 정보 생략 (python 예시와 동일한 구조) ...
    // 실제 문제에서는 입력을 받아 graph[u].push_back(v) 형태로 구성
    
    dfs(1);
    return 0;
}
```

---

## 2. BFS (Breadth-First Search, 너비 우선 탐색)
시작 노드에서 **가까운 노드부터 우선적으로 턈색**하는 방법입니다.
- **특징:** 넓게(Broad) 퍼져나가는 것을 우선합니다. 주로 두 노드 사이의 **최단 경로**를 찾고 싶을 때 사용합니다.
- **구현:** **큐(Queue)** 자료구조를 사용합니다 (Python에서는 `collections.deque` 사용 권장).

### BFS 예제 (C++ - 큐)
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

bool visited[9];
vector<int> graph[9];

void bfs(int start) {
    queue<int> q;
    q.push(start);
    
    // 현재 노드를 방문 처리
    visited[start] = true;
    
    // 큐가 빌 때까지 반복
    while(!q.empty()) {
        // 큐에서 하나의 원소를 뽑아 출력
        int x = q.front();
        q.pop();
        cout << x << " ";
        
        // 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
        for(int i = 0; i < graph[x].size(); i++) {
            int y = graph[x][i];
            if(!visited[y]) {
                q.push(y);
                visited[y] = true;
            }
        }
    }
}

int main() {
    // ... 그래프 초기화 (DFS 예제와 동일) ...
    bfs(1);
    return 0;
}
```

## 3. 요약 비교

| 특징 | DFS (깊이 우선) | BFS (너비 우선) |
|---|---|---|
| **탐색 방식** | 한 놈만 팬다 (깊게) | 주위부터 훑는다 (넓게) |
| **구현 방법** | 스택 / 재귀함수 | 큐 (Queue) |
| **주요 활용** | 경로의 특징 저장 필요시, 미로 탐색 | **최단 거리** 구하기 |
