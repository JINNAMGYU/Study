## 정렬 Sort - 합병, 퀵, 히프, 기수

---

- **복잡하지만 효율적인 정렬**

1. 합병 정렬
2. 퀵 정렬
3. 히프 정렬 (생략)
4. 기수 정렬
---

### 합병 정렬 Merge Sort

1. 분할 : 입력 배열을 같은 크기의 2개의 부분 배열로 분할
1. 정복 : 부분 배열을 정렬, 부분 배열의 크기가 충분히 작지 않으면 순환호출로 다시 분할 정복
1. 합병 : 정렬된 부분 배열을 하나의 배열에 통합

- 실제 정렬은 분할된 배열을 합병시키는 과정에서 이루어짐
  
- 시간 복잡도 : nlog₂n
  
- 레코드 크기가 큰 경우 시간 낭비 -> 연결 리스트 사용 시 감소

- 안정 정렬 - 동일한 값들이 입력 순서대로 유지

```c
int sorted[MAX_SIZE]; // 정렬을 위한 추가공간

/* i=정렬된 왼쪽 리스트에 대한 인덱스
   j는 정렬된 오른쪽 리스트에 대한 인덱스
    k는 정렬될 리스트에 대한 인덱스*/
void merge(int list[], int left, int mid, int right) {  //결합 함수
    int i, j, k, l;
    i = left; j = mid + 1; k = left;

    while (i <= mid && j <= right) { // 분할되있는 두 배열을 비교해가며 오름차순으로 결합
        if (list[i] <= list[j])
            sorted[k++] = list[i++];
        else
            sorted[k++] = list[j++];
    }

    if (i > mid)    // 남아있는 요소들 처리
        for (l = j; l <= right; l++)
            sorted[k++] = list[l];
    else
        for (l = i; l <= mid; l++)
            sorted[k++] = list[l];

    for (l = left; l <= right; l++) // 원래 리스트로 정렬된 배열 저장
        list[l] = sorted[l];
}

void mergeSort(int list[], int left, int right) {
    int mid;
    if (left < right) {
        mid = (left + right) / 2;
        mergeSort(list, left, mid);     // 재귀적으로 부분리스트로 분할 -> 합병
        mergeSort(list, mid + 1, right); 
        merge(list, left, mid, right); //합병
    }
}
```

---

### 퀵 정렬 Quick Sort

1. 리스트의 한 요소를 피벗(pivot)으로 선택
2. 피벗보다 작은 요소를 왼쪽, 큰 요소를 오른쪽으로 옮김
3. 좌우로 분할된 배열에 대해서 피벗 설정 후 정렬 반복

- 시간복잡도 : nlog₂n
- 불안정 정렬 - 동일한 값들이 입력 순서대로 유지하지 않음
- 매우 빠른 수행 속도를 자랑함

```c
#define SWAP(x,y,t)((t)=(x),(x)=(y),(y)=(t))

int partition(int list[], int left, int right) {
	int pivot, temp;
	int low, high;

	low = left;
	high = right + 1;
	pivot = list[left]; // 부분배열의 첫 요소를 피벗으로 지정

	do {
		do
			low++;
		while (list[low] < pivot); //왼쪽부터 피벗보다 큰 값 탐색
		do
			high--;
		while (list[high] > pivot); //오른쪽부터 피벗보다 작은 값 탐색
		// 탐색된 값 교환 -> 왼쪽엔 피벗보다 작은값, 오른쪽엔 피벗보다 큰 값으로 정렬됨
		if (low < high) SWAP(list[low], list[high], temp); 
	} while (low < high);
	
	SWAP(list[left], list[high], temp); //피벗을 중앙으로 이동
	return high; //피벗 위치 반환
}
void quickSort(int list[], int left, int right) {
	if (left < right) {
		int q = partition(list, left, right); //피벗 설정 후 정렬
		quickSort(list, left, q - 1);	//피벗을 기준으로 나눠진 두 배열을 다시 퀵정렬
		quickSort(list, q + 1, right);
	}
}
```





---

### 기수 정렬 Radix Sort

1. 1의 자릿수부터 시작해서 데이터들의 각 자릿수의 값에 해당하는 버킷(queue[0-9])에 저장
1. 자릿수가 같은 데이터를 큐에 넣어놓고 queue[0]부터 차례대로 큐에서 꺼내서 list에 저장
1. 자릿수를 올리고 반복 -> 낮은 자릿수부터 높은 자릿수까지 순차적으로 정렬됨

- 시간 복잡도 : dn

- 비교없이 정렬하는 알고리즘

- 안정 정렬 - 동일한 값들이 원래 순서를 유지

```c
#define BUCKETS 10
#define DIGITS 4
void radixSort(int list[], int n) {
	int i, b, d, factor = 1;
	Queue queue[BUCKETS]; //각 자릿수를 기준으로 저장할 버킷

	for (b = 0; b < BUCKETS; b++) initQueue(&queue[b]); // 큐 초기화

	for (d = 0; d < DIGITS; d++) { 
		for (i = 0; i < n; i++)	// 데이터를 각 자릿수에 따라 큐에 삽입(1의 자리부터 시작)
			enqueue(&queue[(list[i] / factor) % 10], list[i]);

		for (b = i = 0; b < BUCKETS; b++) {
			while (!isEmpty(&queue[b]))
				list[i++] = dequeue(&queue[b]); //현재 자릿수(factor)를 기준으로 정렬된 리스트
		}
		factor *= 10; //그 다음 자리수로 올린 뒤 반복
	}
}
```
