# C# 배열 
---
### 배열 선언

```
int[] numbers1 = new int[5];  // {0,0,0,0,0}
int[] numbers2 = {0,1,2,3,4};  // {0,1,2,3,4}

string[] s1= new string[5]; // {null,null,null,null,null};
string[] s2= ["사과","바나나","포도"];
```

### 배열 접근

numbers[numbers.Length-1]) = numbers[^1]

### 다차원 배열

```
int[,] matrix = new int[2,3]; // 2행 3열

int[,] matrix = {{1,2,3},{4,5,6}}; // 초기화
```

### 가변 배열
- 다차원배열과 달리 각 행의 열 개수가 다를 수 있음
```
int[][] jaggedArray = [[1,2],[3,4,5],[6,7,8,9]];
```

### Array 클래스 매서드
* Array.Sort() : 오름차순 정렬
* Array.reverse() : 순서 뒤집기
* Array.IndexOf(array, value) : value의 인덱스를 찾음
* Array.Resize(ref array, size) : 배열의 크기를 size로 조정
