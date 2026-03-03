# C# - Collection #
---
### List<T> - 동적배열 ###
- 자동으로 크기를 조정하는 배열
```csharp
var stringList = new List<string>();
stringList.Add("a");
stringList.Add("b");
stringList.Add("c"); // 요소 추가
// var stringList = new List<string> { "a","b","c"};
// List<string> stringList = ["A","B","C"];

// 요소 삽입
stringList.AddRange(anotherStringList); // 두 리스트가 합쳐짐
stringList.Insert(1,"z"); // 1번 인덱스 앞에 요소 추가
stringList.InsertRange(2,anoterStringList); //2번 인덱스 앞에 리스트 추가

// 요소 삭제
stringList.Remove("b"); // "b" 삭제됨
stringList.RemoveAt(2); // 2번 인덱스 제거
stringList.RemoveAll((str) => {return str =="a"||str=="c";}); // 리스트를 돌면서 조건 만족하는 요소 모두 제거
stringList.Clear(); // 모두 제거

// 요소 검색
bool hasData = stringList.Contains("a"); //a가 있으면 true,아니면 false 반환
int index = stringList.IndexOf("b"); // 찾아서 인덱스 반환, 없으면 -1;
string? selectedString = stringList.Find(str=>{return str.StartsWith("a")}); // 조건에 맞는 첫 번째 요소 반환
List<string> selectedStrings = stringList.FindAll(str=>{return str.StartsWith("a")}); // 조건에 맞는 모든 요소 반환

// 정렬
var intList = new List<int> { 3, 100 , 5, -1, 20};
intList.Reverse(); // 역순으로 -> 20,-1,5,100,3
intList.Sort(); // 기본정렬(오름차순)
intList.Sort((a,b)=>a.CompareTo(b)); // 커스텀 정렬

int count = intList.Count; // 요소의 개수
int[] ints = intList.ToArray();
```

### Dictionary ###
key와 value를 데이터쌍으로 저장하는 제네릭 컬렉션
```csharp
var fruitDict = new Dictionary<string,string>(); // 생성
fruitDict.Add("apple", "사과"); // 요소 추가(이미 같은 key가 있으면 오류)
fruitDict["apple"] = "애플"; // 요소 추가(이미 같은 key가 있으면 덮어씀)

// 초기화
var fruitDict = new Dictionary<string,string>{
  {"apple","사과"},
  {"banana","바나나"}
};

string fruit = fruitDict["apple"]; //value 꺼내오기 (없을 시 오류)
bool hasKey = fruitDict.TryGetValue("apple", out string? fruit); //안전한 버전
if(hasKey)
  Console.WriteLine(fruit);
else
  Console.WriteLine("없음");

foreach(var key in fruitDict.Keys){
  //dictionary의 key들을 순회
}

foreach(var value in fruitDict.Values){
  //dictionary의 value들을 순회
}

fruitDict.Remove("banana"); // 데이터 삭제
fruitDict.Clear(); // 모두 삭제
```
### Queue ###
```csharp
var queue = new Queue<int>();
queue.Enqueue(1);
queue.Enqueue(2);
int q = queue.Dequeue();
int q = queue.Peek(); //그냥 보여주기만함
queue.TryDequeue(out int? i); //안전한 dequeue
```
### Stack ###
```csharp
var stack = new Stack<int>();
stack.Push(1);
stack.Push(2);
int s = stack.Pop();
int s = stack.Peek(); //그냥 보여주기만함
stack.TryPop(out int? i); //안전한 pop
```



