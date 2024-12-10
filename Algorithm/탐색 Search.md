## 탐색 Search

---

### 순차 탐색 

- 처음부터 마지막까지 다 검사하여 항목을 찾음
- 정렬되지 않은 배열에서 사용

```c
int seqSearch(int key, int low, int high) {
	int i;

	list[high + 1] = key;
	for (i = low; list[i] != key; i++)
		;
	if (i == high + 1) return -1;
	else return i;
}
```

---

### 이진탐색 Binary Search

1. 리스트의 중앙값과 비교
2. 중앙값보다 크면 중앙값의 오른쪽 리스트에서 반복, 중앙값보다 작으면 반대로

- 시간복잡도 : log₂n
- 정렬된 배열에서 사용

```c
int BinarySearch(int key, int low, int high) {
	int middle;
	if (low <= high) {
		middle = (low + high) / 2;
		if (key == list[middle]) // 탐색 성공
			return middle;
		else if (key < middle)	// 왼쪽 리스트 탐색
			return BinarySearch(key, low, middle - 1);
		else                   // 오른쪽 리스트 탐색
			return BinarySearch(key, middle + 1, high);
	}
	return -1; //탐색 실패
}
```





---

### 색인 순차 탐색 Index Sequential Search

1. 주 자료 리스트의 일부를 발췌해서 key, index를 인덱스 테이블에 저장해둠
1. key값을 기준으로 인덱스 테이블을 정렬해두고 찾고자 하는 값과 비교하여 index 범위를 정한다
1. 정해진 index 범위 내에서 순차탐색

```c
typedef struct {
	int key;
	int index;
}itable;
itable list[100]; //인텍스 테이블, 주 자료 리스트에서 일정 간격으로 발췌한 자료를 저장해둠

int IndexSearch(int key, int n) {
	int i, low, high;

	//키 값이 리스트 범위 내 값이 아니면 종료
	if (key<list[0].key || key>list[n - 1].key)
		return -1;

	//인텍스 테이블을 조사하여 찾는 키의 구간을 결정
	for (i = 0; i < 100; i++)
		if (list[i].key <= key && list[i + 1].key > key)
			break;
	if (i == 100) {
		low = list[i - 1].index;
		high = n;
	}
	else {
		low = list[i].index;
		high = list[i+1].index;
	}
	return seqSearch(key, low, high); //결정된 범위 내에서만 순차탐색
}
```



---

### 보간 탐색 Interpol Search

1. 이진탐색과 같은 방식
2. 중앙값이 아닌 특수한 계산식 사용
3. 균등히 분포된 리스트에선 이진탐색보다 빠른 탐색

```c
int InterpolSearch(int key, int n) {
	int low, high, j;
	low = 0;
	high = n - 1;
	while ((list[high] >= key) && (key > list[low])) {
		j = ((float)(key = list[low]) / (list[high] - list[low]) * (high - low)) + low;
		if (key > list[j])low = j + 1;
		else if (key < list[j])high = j - 1;
		else low = j;
	}
	if (list[low] == key) return(low);
	else return -1;
} 
```

