## 연결리스트 Linked List

---

- 각 노드가 데이터, 다음 노드에 대한 참조(포인터)를 포함하는 데이터 구조
- 배열과 달리 크기가 동적으로 변경될 수 있으며 삽입, 삭제가 용이함
  - 단순 연결 리스트
  - 이중 연결 리스트
  - 원형 연결 리스트

### 단순 연결 리스트 Singly Linked List

- 각 노드가 다음 노드에 대한 참조만 가지는 형태
- 처음 노드 부터 순차적으로 접근해야함
- 마지막 노드는 NULL을 가리킴

```c
typedef int element;
typedef struct Node { // 노드 정의
	element data;
	struct Node* link;
}Node;
```

```c
Node* createNode(int item) { // 노드 생성 함수
	Node* newNode = (Node*)malloc(sizeof(Node));
	newNode->data = item;
	newNode->link = NULL;
	return newNode;
}
```

```c
void appendNode(Node** head, int item) { // 리스트 끝에 노드를 추가하는 함수
	Node* n = createNode(item);
	if (*head == NULL) { // 헤드가 없으면 새로운 노드가 헤드
		*head = n;
		return;
	}
	
	Node* temp = *head;
	while (temp->link != NULL) // 리스트의 끝가지 이동
		temp = temp->link;
	temp->link = n;
}
```

```c
void deleteNode(Node** head, int item) { //삭제 함수
    if (*head == NULL) return;

    Node* temp = *head;

    // 삭제할 노드가 헤드 노드인 경우
    if (temp->data == item) {
        *head = temp->next;
        free(temp);
        return;
    }

    // 리스트에서 다른 노드를 찾는 경우
    Node* prev = NULL;
    while (temp != NULL && temp->data != item) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) {
        // 노드를 찾지 못한 경우
        printf("Node with data %d not found in the list.\n", item);
        return;
    }

    // 노드를 찾은 경우
    prev->next = temp->next;
    free(temp);
}
```

```c
void printList(Node* head) { // 리스트 출력
	Node* temp = head;
	while (temp != NULL) {
		printf("%d -> ", temp->data);
		temp = temp->link;
	}
	printf("NULL\n");
}

int main() { // 테스트
	Node *head = NULL;
	appendNode(&head, 1);
	appendNode(&head, 2);
	appendNode(&head, 3);
	appendNode(&head, 4);
	printList(head);
	return 0;
}
```



### 이중 연결 리스트 Doubly Linked List

- 각 노드가 데이터와 이전 노드. 다음 노드를 가리키는 포인터를 가지는 데이터 구조
- 메모리를 약간 더 사용하여 노드 간 양방향 이동, 탐색을 지원

```c
typedef int element;
typedef struct Node {  // 이중 연결리스트 노드 정의
    element data;
    struct Node* prev;
    struct Node* next;
} Node;
```

```c
void appendNode(Node** head, int item) { // 노드 추가 함수
    Node* n = createNode(item);
    if (*head == NULL) {
        *head = n;
        return;
    }

    Node* temp = *head;
    while (temp->next != NULL)
        temp = temp->next;

    temp->next = n;
    n->prev = temp;
}
```

```c
void deleteNode(Node** head, int item) { // 삭제 함수
    if (*head == NULL) return;

    Node* temp = *head;

    // 삭제할 노드가 헤드 노드인 경우
    if (temp->data == item) {
        if (temp->next == NULL) { // 노드가 하나만 있는 경우
            free(temp);
            *head = NULL;
            return;
        }

        // 여러 노드가 있는 경우
        *head = temp->next;
        (*head)->prev = NULL;
        free(temp);
        return;
    }

    // 리스트에서 다른 노드를 찾는 경우
    while (temp != NULL && temp->data != item) {
        temp = temp->next;
    }

    if (temp == NULL) {
        // 노드를 찾지 못한 경우
        printf("Node with data %d not found in the list.\n", item);
        return;
    }

    // 노드를 찾은 경우
    if (temp->prev != NULL)
        temp->prev->next = temp->next;
    if (temp->next != NULL)
        temp->next->prev = temp->prev;

    free(temp);
}
```

```c
void printList(Node* head) { // 정방향 출력
    Node* temp = head;
    while (temp != NULL) {
        printf("%d <-> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}
void printListReverse(Node* head) { // 역방향 출력
    if (head == NULL) return;

    Node* temp = head;
    while (temp->next != NULL)
        temp = temp->next;

    while (temp != NULL) {
        printf("%d <-> ", temp->data);
        temp = temp->prev;
    }
    printf("NULL\n");
}
```



### 원형 연결 리스트 Circular Linked List

- 마지막 노드가 첫 번째 노드를 가리키도록 연결된 데이터 구조
- 순환적인 탐색

```c
typedef int element;
typedef struct Node { // 원형 연결 리스트 정의
    element data;
    struct Node* next;
} Node;
```

```c
Node* createNode(int item) { // 노드 생성
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = item;
    newNode->next = newNode; // 원형 리스트는 처음엔 자기 자신을 가리킴
    return newNode;
}
```

```c
void appendNode(Node** head, int item) { // 노드 추가 함수
    Node* n = createNode(item);
    if (*head == NULL) {
        *head = n;
        return;
    }

    Node* temp = *head;
    while (temp->next != *head) // 다음 노드가 헤드일 때가 노드의 끝 
        temp = temp->next;

    temp->next = n;
    n->next = *head;
}
```

```c
void deleteNode(Node** head, int item) { // ** 삭제 함수 **
    if (*head == NULL) return;

    Node* temp = *head;
    Node* prev = NULL;

    // 만약 삭제할 노드가 헤드 노드인 경우
    if ((*head)->data == item) {
        // 리스트에 하나의 노드만 있는 경우
        if ((*head)->next == *head) {
            free(*head);
            *head = NULL;
            return;
        }

        // 리스트에 여러 노드가 있는 경우
        while (temp->next != *head)
            temp = temp->next;

        temp->next = (*head)->next;
        free(*head);
        *head = temp->next;
        return;
    }

    // 리스트에서 다른 노드를 찾는 경우
    prev = temp;
    temp = temp->next;
    while (temp != *head && temp->data != item) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == *head) {
        // 노드를 찾지 못한 경우
        printf("Node with data %d not found in the list.\n", item);
        return;
    }

    // 노드를 찾은 경우
    prev->next = temp->next;
    free(temp);
}
```

```c
void printList(Node* head) { // 출력
    if (head == NULL) return;

    Node* temp = head;
    do {
        printf("%d -> ", temp->data);
        temp = temp->next;
    } while (temp != head);
    printf("%d (head)\n", head->data); // 마지막 노드가 다시 head를 가리킴
}
```



- 위 함수들은 모두 간단한 삽입, 삭제, 출력 함수지만 필요에 따라 다양한 함수를 얼마든지 구현할 수 있음