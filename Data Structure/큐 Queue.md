## 큐 Queue

___

- 선입선출(FIFO) 구조
- 후단(rear)에서 삽입 (enqueue), 전단(front)에서 삭제 (dequeue)
  - 배열을 이용한 선형 큐
  - 배열을 이용한 원형 큐
  - 연결리스트를 이용한 큐

### 선형 큐 Linear Queue

- 배열로 구현하여 이해하기 쉽고 구현하기도 쉬움
- 문제점 : 삭제된 공간을 재사용할 수 없음

```c
typedef int element;
typedef struct {
	int front; // 전단
	int rear;  // 후단
	element data[MAXSIZE];
}Queue;

void initQueue(Queue* q) { // 큐 초기화
	q->rear = -1;
	q->front = -1;
}
```

```c
int isFull(Queue* q) { // 큐 포화 검사
	return q->rear + 1 == MAXSIZE;
}
int isEmpty(Queue* q) { // 큐 공백 검사
	return q->front == q->rear;
}
```

```c
void enqueue(Queue* q, element item) { // 큐 데이터 삽입
	if (isFull(q)) {
		printf("포화 에러\n");
		return;
	}
	q->data[++(q->rear)] = item;
}
element dequeue(Queue* q) { 		  // 큐 데이터 삭제
	if (isEmpty(q)) {
		printf("공백 에러\n");
		return -1;                   // 예외 처리를 위한 코드 추가 하는 것이 좋음
	}
	return q->data[++(q->front)];
}
```

### 원형큐 Circular Queue

- 배열의 끝과 시작을 연결하여 순환구조를 형성 -> 효율적인 공간 활용
- front와 rear의 초기화와 증가시키는 계산이 바뀜

```c
typedef int element;
typedef struct {
	int front; // 전단
	int rear;  // 후단
	element data[MAXSIZE];
}Queue;

void initQueue(Queue* q) { // 큐 초기화
	q->rear = 0; // 0으로 초기화
	q->front = 0;
}
```

```c
int isFull(Queue* q) { // 큐 포화 검사
	return (q->rear + 1) % MAXSIZE == q->front;
}
int isEmpty(Queue* q) { // 큐 공백 검사
	return q->front == q->rear;
}
```

```c
void enqueue(Queue* q, element item) { // 큐 데이터 삽입
	if (isFull(q)) {
		printf("포화 에러\n");
		return;
	}
	q->rear = (q->rear + 1) % MAXSIZE;
	q->data[q->rear] = item;
}
 element dequeue(Queue* q) {		  // 큐 데이터 삭제
	if (isEmpty(q)) {
		printf("공백 에러\n");
		return -1;
	}
	q->front = (q->front + 1) % MAXSIZE;
	return q->data[q->front];
}
```

### 연결리스트로 구현한 큐 Linked List Queue

- 동적 크기 조정과 효율적인 삽입, 삭제 연산 가능

```c
typedef int element;
typedef struct Node { // 연결리스트 노드 정의
	element data;
	struct Node* next;
}Node;

typedef struct { // 큐 구조체 정의
	Node* front; // 전단
	Node* rear;  // 후단
}Queue;
```

```c
void initQueue(Queue* q) { // 큐 초기화
	q->rear = NULL;
	q->front = NULL;
}
int isEmpty(Queue* q) { // 큐 공백 검사
	return q->front == NULL;
}
```

```c
void enqueue(Queue* q, element item) { // 큐 데이터 삽입
	Node* newNode = (Node*)malloc(sizeof(Node));
	if (newNode == NULL) {
		printf("메모리할당 오류\n");
		return;
	}
	newNode->data = item;
	newNode->next = NULL;
	if (isEmpty(q))
		q->front = newNode;
	else
		q->rear->next = newNode;
	q->rear = newNode;
}
 element dequeue(Queue* q) {		  // 큐 데이터 삭제
	if (isEmpty(q)) {
		printf("공백 에러\n");
		return -1;
	}
	Node* temp = q->front;
	element item = temp->data;
	q->front = q->front->next;
	if (q->front == NULL) {
		q->rear = NULL;
	}
	free(temp);
	return item;
}
```

