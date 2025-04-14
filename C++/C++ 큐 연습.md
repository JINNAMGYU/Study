### C++ 큐 연습

```c++
// 클래스로 간단 구현 연습
// 실제에선 std::queue, std::deque 사용
class Queue {
private:
	vector<int> data;
	int front;
public:
	Queue() { front = 0; }
	void push(int item) { data.push_back(item); }
	int pop() { 
		if (isEmpty())
			throw underflow_error("Queue underflow");
		return data[front++]; 
	}
	int getSize() const { return data.size() - front; }
	bool isEmpty() const { return getSize() <= 0; }
};
```

