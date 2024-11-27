## 정렬 Sort - 버블, 선택, 삽입, 쉘

---

- **단순하지만 비효율적인 정렬**

1. 버블 정렬
2. 선택 정렬
3. 삽입 정렬
4. 쉘 정렬
---

### 버블 정렬 Bubble Sort

1. 배열의 첫번째 요소부터 마지막 요소까지 반복하면서 인접한 두 요소를 비교
2.  인접한 두 요소가 정렬되지 않은 경우 서로 교환

- 시간 복잡도 
  - 최악 - O(n²)  최선 - O(n)  평균 - O(n²)

- 간단하여 이해하기는 쉬우나 대량 데이터에 대한 성능이 매우 떨어짐

- 안정 정렬 - 동일한 값들이 입력 순서대로 유지

```c
#define SWAP(x,y,t)((t)=(x),(x)=(y),(y)=(t))
void bubbleSort(int list[], int n) {
	int temp;
	for (int i = n - 1; i > 0; i--) {
		for (int j = 0; j < i; j++)
			if (list[j] > list[j + 1]) // 앞 뒤 값을 비교하며 큰 값을 오른쪽 끝으로 이동시킴
				SWAP(list[j], list[j + 1], temp);
	}
}
```

---

### 선택 정렬 Selection Sort

1. 배열에서 가장 작은 요소를 찾아 첫번째 요소와 교환
2. 다음으로 작은 요소를 찾아 두번째 요소와 교환
3. 이 과정을 마지막 요소까지 반복

- 시간복잡도 : O(n²)
- 불안정 정렬 : 동일한 값들이 입력 순서를 유지하지 않음

```c
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        int min_idx = i; // 가장 작은 요소의 인덱스
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j; // 새로운 가장 작은 요소의 인덱스 업데이트
            }
        }
        // 가장 작은 요소를 현재 위치(i)와 교환
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}
```





---

### 삽입 정렬 Insertion Sort

1. 배열의 두번째 요소부터 시작, 현재 요소의 앞(왼쪽) 요소들과 비교
2. 현재 요소보다 큰 요소는 오른쪽으로 한칸씩 이동
3. 현재 요소보다 작은 요소를 발견 시 정지하고 그 앞칸(빈칸)에 현재 요소를 삽입
4. 이 과정을 마지막 요소까지 반복

- 시간 복잡도 : O(n²)

- 작은 데이터 세트, 어느정도 정렬있는 세트엔 효율적이고 구현이 간단하나, 반대인 경우엔 최악임

- 안정 정렬 - 동일한 값들이 원래 순서를 유지

```c
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        // 현재 요소를 올바른 위치에 삽입하기 위해 배열의 왼쪽 부분과 비교
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j]; // 현재 요소보다 큰 요소는 오른쪽으로 한칸 이동
            j--;
        }
        arr[j + 1] = key; // 현재 요소보다 작은 값의 앞 칸,빈 칸에 삽입
    }
}
```
### 쉘 정렬 Shell Sort

1. 배열을 큰 간격으로 나누어 간격을 기준으로 선택 정렬
2. 간격을 1/2씩 줄여가며 촘촘히 정렬

- 삽입정렬의 활용이라 간단하고 직관적인 편
- 자주 쓰는 정렬은 아닌데 중간 규모 배열에서 쓸만함

```c
// 간격을 두고 삽입 정렬을 수행하는 함수
void incInsertionSort(int list[], int first, int last, int gap) {
    int i, j, key;

    // 첫 번째 원소 이후부터 gap 간격으로 순회
    for (i = first + gap; i <= last; i = i + gap) {
        key = list[i]; // 현재 정렬하려는 값을 key에 저장
        // gap 간격으로 정렬된 부분 배열에서 key보다 큰 값을 뒤로 이동
        for (j = i - gap; j >= first && key < list[j]; j = j - gap) {
            list[j + gap] = list[j]; // 큰 값을 gap 간격 뒤로 이동
        }
        list[j + gap] = key; // key 값을 올바른 위치에 삽입
    }
}

// 쉘 정렬 함수
void shellSort(int list[], int n) {
    int i, gap;

    // 초기 gap을 n/2로 설정하고, 점진적으로 줄여가며 정렬
    for (gap = n / 2; gap > 0; gap = gap / 2) {
        // gap을 홀수로 하는게 더 좋음
        if ((gap % 2) == 0) gap++;

        // gap 간격으로 나눈 각 부분 배열에 대해 삽입 정렬 수행
        for (i = 0; i < gap; i++) {
            // i번째부터 시작하여 gap 간격으로 삽입 정렬
            incInsertionSort(list, i, n - 1, gap);
        }
    }
}

```

---

### 
