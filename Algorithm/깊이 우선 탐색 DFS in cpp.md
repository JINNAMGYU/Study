## 깊이 우선 탐색 DFS in cpp

깊이 우선 탐색(DFS)은 그래프나 트리 구조에서 **모든 노드를 방문하기 위한 탐색 알고리즘** 중 하나. **한 노드에서 시작하여 가능한 깊이까지 탐색**한 후, 더 이상 갈 곳이 없으면 **직전에 방문했던 노드로 되돌아가(backtracking)** 다시 탐색을 이어가는 방식.

___

### **특징**

1. **탐색 방식**:
   - 한 방향으로 **최대한 깊이 들어간 후**, 갈 곳이 없으면 다시 되돌아오며 다른 경로를 탐색합니다.
   - 예를 들어, 트리 구조에서는 **왼쪽 자식 노드부터 끝까지 탐색한 뒤** 오른쪽 자식 노드로 넘어갑니다.
2. **구현 방식**:
   - **재귀**를 활용하거나, **스택**을 명시적으로 사용해 구현할 수 있습니다.
   - 노드 방문 여부를 기록하는 **visited 배열**을 사용하여 중복 방문을 방지합니다.

------

### **동작 원리**

1. 시작 노드에서 탐색을 시작.
2. **현재 노드에서 갈 수 있는 인접 노드를 하나 선택**하여 방문.
3. **인접 노드를 모두 방문했다면** 직전 노드로 돌아가 다른 경로를 탐색.
4. 모든 노드를 탐색할 때까지 반복.

------

### 구현 코드

```c++
#include <iostream>
#include <vector>
using namespace std;

vector<vector<int>> graph; // 그래프 인접 리스트
vector<bool> visited;      // 방문 여부

void dfs(int node) {
    visited[node] = true;
    cout << node << "방문 "; // 방문 노드 출력
    for (int neighbor : graph[node]) { // 인접 노드를 탐색
        if (!visited[neighbor])            // 아직 방문하지 않은 노드 발견
            dfs(neighbor);             // 그 노드에서 다시 dfs
    }
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

    // DFS 실행
    cout << "DFS Traversal (Recursive): ";
    dfs(0); // 시작 노드
    cout << endl;
}
```

---

### **장점**

- 구현이 간단하며, 탐색 경로가 적은 문제나 트리 구조의 탐색에 적합.
- 모든 경로를 탐색해야 하는 문제(예: 경로 찾기, 백트래킹 문제)에서 효율적.

------

### **단점**

- 그래프의 깊이가 매우 깊거나 무한 순환 구조가 있는 경우(사이클 그래프) **스택 오버플로**가 발생할 수 있음.
- 최단 경로를 보장하지 않음(최단 경로 탐색에는 BFS가 적합).

------

### **활용 사례**

1. 경로 탐색
   - 한 노드에서 시작해 특정 노드로 가는 모든 경로를 찾는 문제.
2. 연결 요소 찾기
   - 그래프가 여러 개의 독립된 연결 요소로 나뉘어 있을 때 각 연결 요소를 탐색.
3. 사이클 검출
   - 그래프에 사이클이 존재하는지 여부를 판별.
4. 백트래킹 문제
   - 퍼즐, 미로 찾기, N-Queen 문제 등에서 가능한 모든 경로를 탐색.

---

### 응용문제 풀이

백준 2606번 https://www.acmicpc.net/problem/2606

```c++
#include <iostream>
#include <vector>
using namespace std;

vector<vector<int>> graph; // 그래프 인접 리스트
vector<bool> visited;      // 방문 여부
int virus = 0;

void dfs(int node) {
    visited[node] = true;
    virus++;
    for (int neighbor : graph[node]) { // 인접 노드를 탐색
        if (!visited[neighbor])            // 아직 방문하지 않은 노드 발견
            dfs(neighbor);             // 그 노드에서 다시 dfs
    }
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	
    int V; // 노드 개수
    cin >> V;
    graph.resize(V); // 그래프 크기 설정
    visited.resize(V, false); // 방문 여부 초기화

    int n;
    cin >> n;
    int startNode, endNode;
    for (int i = 0; i < n; i++) {
        cin >> startNode >> endNode;
        graph[startNode - 1].push_back(endNode - 1);
        graph[endNode - 1].push_back(startNode - 1);
    }

    dfs(0); // 시작 노드
    cout << virus - 1; // 1번 컴퓨터를 제외한 수 출력
}
```

