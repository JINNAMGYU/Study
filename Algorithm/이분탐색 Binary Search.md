### 이분탐색 Binary Search

https://www.acmicpc.net/problem/1920

- 정렬된 리스트에서 탐색범위를 절반씩 좁혀가며 데이터를 탐색하는 방법
- 데이터는 정렬되어 있어야함
- start, end, mid를 이용해서 중간 지점에 있는 값과 데이터를 반복적 비교

```c++
while (start <= end) {
			int mid = (start + end) / 2;
			if (Array[mid] == data) {
				find=true;
				break;
			}
			else if (Array[mid] < data)
				start = mid + 1;
			else
				end = mid - 1;
		}
```

