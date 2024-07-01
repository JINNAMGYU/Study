## 스택 Stack

---

- 후입선출(LIFO) 원칙에 따라 데이터를 저장하는 추상 데이터 구조
  - push : 스택에 최상위에 요소를 추가
  - pop : 스택의 최상위 요소를 제거하고 반환

### 배열 기반 스택 구현

- 배열로 구현하는 것은 메모리 관리가 간단하지만 공간 낭비가 발생함

```c
typedef int element;
typedef struct { // 스택 구조체 정의
    int top;          // 스택의 상단을 나타내는 인덱스
    element data[MAXSIZE]; // 스택을 저장하는 배열
} Stack;
```

```c
void initStack(Stack* s) { // 스택 초기화
    s->top = -1; // 스택이 비어 있는 상태
}
int isEmpty(Stack* s) {  // 스택이 비어 있는지 검사
    return s->top == -1;
}
int isFull(Stack* s) { // 스택이 포화 상태인지 검사
    return s->top == MAXSIZE - 1;
}
```

```c
// 스택에 요소 추가 (push)
void push(Stack* s, element item) {
    if (isFull(s)) {
        printf("스택 포화 에러\n");
        return;
    }
    s->data[++(s->top)] = item;
}

// 스택에서 요소 제거 (pop)
element pop(Stack* s) {
    if (isEmpty(s)) {
        printf("스택 공백 에러\n");
        return -1; // 오류 값을 반환
    }
    return s->data[(s->top)--];
}
```



### 연결리스트를 이용한 동적 스택

```c
typedef int element;

typedef struct Node { // 연결 리스트의 노드 정의
    element data;
    struct Node* next;
} Node;
typedef struct { // 스택 구조체 정의
    Node* top; // 스택의 상단을 나타내는 포인터
} Stack;
```

```c
void initStack(Stack* s) { // 스택 초기화
    s->top = NULL; // 스택이 비어 있는 상태
}

int isEmpty(Stack* s) { // 스택이 비어 있는지 검사
    return s->top == NULL;
}
```

```c
void push(Stack* s, element item) { // 스택에 요소 추가 (push)
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL) {
        printf("메모리 할당 오류\n");
        return;
    }
    newNode->data = item;
    newNode->next = s->top;
    s->top = newNode;
}

element pop(Stack* s) { // 스택에서 요소 제거 (pop)
    if (isEmpty(s)) {
        printf("스택 공백 에러\n");
        return -1; // 오류 값을 반환
    }
    Node* temp = s->top;
    element item = temp->data;
    s->top = s->top->next;
    free(temp);
    return item;
}
```



### Cpp로 구현 연습

- Cpp 클래스와 배열을 이용한 정적 스택 구현

```c++
class Stack {
    int stack[MAXN];  // 스택을 저장할 정수 배열
    int tos;          // 스택의 최상위 요소를 가리키는 인덱스
public:
    Stack():tos(-1){}
    // 스택에 요소를 추가하는 메서드
    void push(int data) {
        if (tos >= MAXN - 1) {
             throw std::out_of_range("Stack FULL"); // 스택이 가득 차면 예외를 던짐
        }
        stack[++tos]=data; // 배열에 요소를 추가
    }
    // 스택에서 요소를 제거하고 반환하는 메서드
    int pop() {
        if (tos<0) {
             throw std::out_of_range("Stack Empty"); // 스택이 비어있으면 예외를 던짐
        }
        return stack[tos--]; // 최상위 요소를 반환하고 인덱스 감소
    }
};
```



- Cpp 클래스와 vector 컨테이너를 이용한 동적 스택 구현
  - vector의 동적메모리 관리와 자동 크기 조절로 매우 유연함

```c++
template <class T>
class Stack {
    vector<T> stack;  // 스택을 저장할 벡터
public:
    // 스택에 요소를 추가하는 메서드
    void push(T data) {
        stack.push_back(data); // 벡터에 요소를 추가
    }
    // 스택에서 요소를 제거하고 반환하는 메서드
    T pop() {
        if (stack.empty()) {
             throw std::out_of_range("Stack Empty"); // 스택이 비어있으면 예외를 던짐
        }
        T popdata = stack.back();
        stack.pop_back();
        return popdata; // 최상위 요소를 반환하고 벡터에서 제거
    }
};
```

