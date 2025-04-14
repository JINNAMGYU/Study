## 너비 우선 탐색 BFS in cpp

너비 우선 탐색(BFS)은 그래프나 트리 구조에서 **모든 노드를 방문하기 위한 탐색 알고리즘** 중 하나. **한 노드에서 시작하여 인접한 모든 노드를 방문한 후**, 더 깊은 레벨로 진행하며 탐색하는 방식.

---

### **특징**

1. **탐색 방식**:
   - 시작 노드에서 **가까운 레벨에 있는 모든 노드**를 방문한 후, 그다음 레벨로 이동.
   - FIFO(First In First Out) 방식의 **큐(Queue)**를 이용하여 탐색 진행.
2. **구현 방식**:
   - 큐를 사용해 탐색을 관리하며, 노드 방문 여부를 기록하는 **visited 배열**을 사용하여 중복 방문을 방지.

---

### **동작 원리**

1. 시작 노드를 큐에 추가하고 방문 처리.
2. 큐에서 노드를 하나 꺼내고, 해당 노드와 연결된 모든 인접 노드를 탐색.
3. 방문하지 않은 인접 노드를 큐에 추가하고 방문 처리.
4. 큐가 비워질 때까지 반복.

---

### 구현 코드

```c++
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

vector<vector<int>> graph; // 그래프 인접 리스트
vector<bool> visited;      // 방문 여부

void bfs(int startNode) {
    queue<int> q; // BFS를 위한 큐
    visited[startNode] = true;
    q.push(startNode);

    cout << "BFS 탐색 순서: ";
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";

        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
    cout << endl;
}

int main() {
    int V = 6; // 노드 개수
    graph.resize(V); // 그래프 크기 설정
    visited.resize(V, false); // 방문 여부 초기화

    // 간선 추가
    graph[0].push_back(1);
    graph[0].push_back(2);
    graph[1].push_back(3);
    graph[2].push_back(4);
    graph[3].push_back(5);

    // BFS 실행
    bfs(0); // 시작 노드
}
```

### **장점**

- 최단 경로를 보장(가중치가 없는 그래프에서).
- 그래프가 얕고 너비가 넓은 경우에 적합.
- 트리 구조에서 레벨 순서대로 데이터를 처리할 때 유용.

### **단점**

- 그래프가 매우 넓거나 깊을 경우, 큐의 크기가 커질 수 있어 메모리 사용량 증가.
- 모든 노드를 탐색해야 하는 경우 DFS보다 비효율적일 수 있음.

### **활용 사례**

1. 최단 경로 탐색
   - 가중치가 없는 그래프에서 한 노드에서 다른 노드로의 최단 경로를 찾는 문제.
2. 레벨 순서 탐색
   - 그래프나 트리의 레벨별 데이터를 처리.
3. 연결 요소 찾기
   - 그래프에서 연결된 모든 노드를 탐색하여 독립적인 연결 요소를 찾는 문제.
4. 네트워크 흐름 문제
   - 네트워크 내에서 데이터 패킷이 이동 가능한 경로를 탐색.

### 응용문제 풀이

#### 백준 1260번: DFS와 BFS

- 문제 링크: https://www.acmicpc.net/problem/1260

```c++
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

vector<vector<int>> graph;
vector<bool> visited;

void dfs(int node) {
    visited[node] = true;
    cout << node << " ";
    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor);
        }
    }
}

void bfs(int startNode) {
    queue<int> q;
    visited[startNode] = true;
    q.push(startNode);

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";

        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    int N, M, startNode;
    cin >> N >> M >> startNode;

    graph.resize(N + 1);
    visited.resize(N + 1, false);

    for (int i = 0; i < M; i++) {
        int u, v;
        cin >> u >> v;
        graph[u].push_back(v);
        graph[v].push_back(u);
    }

    for (int i = 1; i <= N; i++) {
        sort(graph[i].begin(), graph[i].end());
    }

    dfs(startNode);
    cout << endl;

    fill(visited.begin(), visited.end(), false);
    bfs(startNode);
    cout << endl;
}
```