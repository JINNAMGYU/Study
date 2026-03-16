# C# Collection

## 1. List<T> (동적 배열)

자동으로 크기가 조절되며, 인덱스로 접근 가능한 가장 범용적인 컬렉션입니다.

### **선언 및 초기화**

```csharp
var stringList = new List<string>();
var optimizedList = new List<string>(1000); // 메모리 미리 할당 (최적화)

// 초기화 스타일
var list1 = new List<string> { "a", "b", "c" };
List<string> list2 = ["A", "B", "C"]; // 최신 C# 컬렉션 식

```

### **요소 조작 (추가/삽입/삭제)**

| 기능 | 메서드 | 설명 |
| --- | --- | --- |
| **추가** | `Add(item)` | 끝에 요소 추가 |
| **병합** | `AddRange(list)` | 다른 리스트의 모든 요소 추가 |
| **삽입** | `Insert(index, item)` | 특정 인덱스에 요소 삽입 |
| **삭제** | `Remove(item)` | 첫 번째로 일치하는 요소 삭제 |
| **인덱스 삭제** | `RemoveAt(index)` | 해당 위치의 요소 삭제 |
| **조건 삭제** | `RemoveAll(predicate)` | 조건에 맞는 모든 요소 삭제 |
| **전체 삭제** | `Clear()` | 모든 요소 제거 |

### **검색 및 정렬**

```csharp
// 검색
bool hasData = stringList.Contains("a"); 
int index = stringList.IndexOf("b"); 
string? item = stringList.Find(str => str.StartsWith("a"));
List<string> items = stringList.FindAll(str => str.StartsWith("a"));

// 정렬
intList.Reverse();                        // 역순 정렬
intList.Sort();                           // 오름차순 (기본)
intList.Sort((a, b) => a.CompareTo(b));   // 오름차순 (커스텀)
intList.Sort((a, b) => b.CompareTo(a));   // 내림차순 (커스텀)

```

---

## 2. Dictionary<K, V>

Key와 Value의 쌍으로 데이터를 관리하며 검색 속도가 매우 빠릅니다.

### **데이터 추가 및 읽기**

```csharp
var fruitDict = new Dictionary<string, string>();

fruitDict.Add("apple", "사과");    // 중복 키가 있으면 예외 발생
fruitDict["apple"] = "애플";     // 중복 키가 있으면 덮어쓰기

// 안전하게 값 가져오기
if (fruitDict.TryGetValue("apple", out string? fruit)) {
    Console.WriteLine(fruit);
}

```

### **순회 및 삭제**

```csharp
foreach (var key in fruitDict.Keys) { /* Key 순회 */ }
foreach (var value in fruitDict.Values) { /* Value 순회 */ }

fruitDict.Remove("banana"); // 특정 키 삭제
fruitDict.Clear();          // 전체 삭제

```

---

## 3. Queue & Stack

특수한 데이터 입출력 구조를 가진 컬렉션입니다.

### **Queue<T> (FIFO: 선입선출)**

* `Enqueue(item)` : 데이터 넣기
* `Dequeue()` : 데이터 꺼내기 (가장 먼저 들어온 것)
* `Peek()` : 데이터 확인만 하기
* `TryDequeue(out item)` : 안전하게 꺼내기

### **Stack<T> (LIFO: 후입선출)**

* `Push(item)` : 데이터 쌓기
* `Pop()` : 데이터 꺼내기 (가장 마지막에 들어온 것)
* `Peek()` : 데이터 확인만 하기
* `TryPop(out item)` : 안전하게 꺼내기
