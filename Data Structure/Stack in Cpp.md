### Stack in Cpp

---

- Stack : 후입선출(LIFO) 원칙에 따라 데이터를 저장하는 추상 데이터 구조
  - push : 스택에 최상위에 요소를 추가
  - pop : 스택의 최상위 요소를 제거하고 반환



- Cpp 배열을 이용한 정적 스택 구현

```c++
#include <iostream>   // 표준 입출력 스트림을 사용하기 위한 헤더 파일
#include <stdexcept>  // 표준 예외 클래스를 사용하기 위한 헤더 파일
using namespace std; // 표준 네임스페이스를 사용
#define MAXN 100 // 최대 크기 정의

class Stack {
    int stack[MAXN];  // 스택을 저장할 정수 배열
    int tos;          // 스택의 최상위 요소를 가리키는 인덱스
public:
    Stack():tos(-1){}
    // 스택에 요소를 추가하는 메서드
    void push(int data) {
        if (tos >= MAXN - 1) {
            throw runtime_error("Stack Overflow"); // 스택이 가득 차면 예외를 던짐
        }
        stack[++tos]=data; // 배열에 요소를 추가
    }
    // 스택에서 요소를 제거하고 반환하는 메서드
    int pop() {
        if (tos<0) {
            throw runtime_error("Stack is Empty"); // 스택이 비어있으면 예외를 던짐
        }
        return stack[tos--]; // 최상위 요소를 반환하고 인덱스 감소
    }
};

int main() {
    Stack s; // 정수 타입의 스택 생성
    try {
        s.push(1); // 스택에 1 추가
        s.push(2); // 스택에 2 추가
        s.push(3); // 스택에 3 추가
        cout << s.pop() << endl; // 스택에서 요소 제거 및 출력 (3)
        cout << s.pop() << endl; // 스택에서 요소 제거 및 출력 (2)
        cout << s.pop() << endl; // 스택에서 요소 제거 및 출력 (1)
        cout << s.pop() << endl; // 스택에서 요소 제거 시 예외 발생
    }
    catch (const runtime_error& e) { // runtime_error 예외를 처리
        cout << e.what() << endl; // 예외 메시지 출력 ("Stack Empty")
    }
}

```



- Cpp vector 컨테이너를 이용한 동적 스택 구현

```c++
#include <iostream>   // 표준 입출력 스트림을 사용하기 위한 헤더 파일
#include <vector>     // 벡터 컨테이너를 사용하기 위한 헤더 파일
#include <stdexcept>  // 표준 예외 클래스를 사용하기 위한 헤더 파일
using namespace std; // 표준 네임스페이스를 사용

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
            throw runtime_error("Stack Empty"); // 스택이 비어있으면 예외를 던짐
        }
        T popdata = stack.back();
        stack.pop_back();
        return popdata; // 최상위 요소를 반환하고 벡터에서 제거
    }
};

int main() {
    Stack<int> s; // 정수 타입의 스택 생성
    try {
        s.push(1); // 스택에 1 추가
        s.push(2); // 스택에 2 추가
        s.push(3); // 스택에 3 추가
        cout << s.pop() << endl; // 스택에서 요소 제거 및 출력 (3)
        cout << s.pop() << endl; // 스택에서 요소 제거 및 출력 (2)
        cout << s.pop() << endl; // 스택에서 요소 제거 및 출력 (1)
        cout << s.pop() << endl; // 스택에서 요소 제거 시 예외 발생
    }
    catch (const runtime_error& e) { // runtime_error 예외를 처리
        cout << e.what() << endl; // 예외 메시지 출력 ("Stack Empty")
    }
}
```

