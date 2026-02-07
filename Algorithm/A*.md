---

## 1. 개요 (Concept)

A* 알고리즘은 **시작점에서 현재까지 온 거리(G)**와 **목적지까지 예상되는 거리(H)**를 더한 **최종 비용(F)**이 최소가 되는 경로를 우선적으로 탐색하는 그래프 알고리즘입니다.

* **G (Cost):** 시작 지점에서 현재 노드까지 도달하는 데 걸린 실제 비용.
* **H (Heuristic):** 현재 노드에서 목적지까지 도달할 것으로 예상되는 추정 비용.
* **F (Total):** 해당 노드를 거쳐갈 경우의 총 예상 비용.

---

## 2. 주요 데이터 구조

### 1) Node 구조체

각 타일의 상태와 경로 역추적을 위한 정보를 저장합니다.

* `pos`: 현재 좌표 (x, y)
* `g, h`: 비용 값
* `parent`: 최단 경로를 기록하기 위해 직전 노드를 가리키는 포인터

### 2) Open List (우선순위 큐)

* **역할:** 탐색 후보지 관리.
* **특징:** F값이 가장 낮은 노드를 먼저 꺼내기 위해 `std::priority_queue` (Min-Heap)를 사용합니다.

### 3) Closed List (방문 기록)

* **역할:** 이미 최단 거리가 확정된 노드를 재방문하지 않도록 관리.
* **특징:** 2차원 배열이나 해시맵으로 구현하여 $O(1)$로 조회합니다.

---

## 3. 알고리즘 로직 (Step-by-Step)

1. **초기화:** 시작 노드를 Open List에 넣습니다.
2. **반복 (While):** Open List가 빌 때까지 다음을 수행합니다.
* **추출:** Open List에서 F값이 가장 작은 노드(`curr`)를 꺼냅니다.
* **방문 처리:** `curr`을 Closed List에 추가합니다.
* **도착 확인:** `curr`이 목적지라면 반복을 종료하고 경로를 역추적합니다.
* **이웃 탐색:** `curr` 주변의 인접 노드들을 검사합니다.
* 벽이거나 이미 Closed List에 있다면 무시합니다.
* 새로운 G값이 기존보다 작거나 처음 방문한다면, 비용을 갱신하고 Open List에 넣습니다.





---

## 4. 구현 코드 요약 (C++)

```cpp
// 우선순위 큐를 위한 비교 연산자 (F값 기준 오름차순)
struct Node {
    Point pos;
    int g, h;
    Node* parent;
    int f() const { return g + h; }
    bool operator>(const Node& other) const { return f() > other.f(); }
};

// 핵심 루프
while (!openList.empty()) {
    Node* curr = openList.top();
    openList.pop();

    if (closedList[curr->y][curr->x]) continue;
    closedList[curr->y][curr->x] = true;

    // 목적지 도달 시 parent를 따라가며 경로 생성
    if (curr->pos == end) {
        ReconstructPath(curr);
        break;
    }

    // 상하좌우 탐색 로직...
}

```

---

## 5. 실무 적용 팁 💡

* **Heuristic (H):** * 격자형 맵(상하좌우)에서는 **맨해튼 거리**()가 가장 효율적입니다.
* **최적화:**
* 매 탐색마다 `new/delete`를 하면 성능이 저하됩니다. **Object Pool**을 사용하여 노드 객체를 재사용하세요.
* 맵이 너무 크다면 **Hierarchical A***(맵을 구역으로 나눔)나 **JPS**(Jump Point Search)를 고려할 수 있습니다.



---

