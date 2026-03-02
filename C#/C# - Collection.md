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

stringList.AddRange(anotherStringList); // 두 리스트가 합쳐짐
stringList.Insert(1,"z"); // 1번 인덱스 앞에 요소 추가
stringList.InsertRange(2,anoterStringList); //2번 인덱스 앞에 리스트 추가

stringList.Remove("b"); // "b" 삭제됨
stringList.RemoveAt(2); // 2번 인덱스 제거
stringList.RemoveAll((str) => {return str =="a"||str=="c";}); // 리스트를 돌면서 조건 만족하는 요소 모두 제거
stringList.Clear(); // 모두 제거

bool hasData = stringList.Contains("a"); //a가 있으면 true,아니면 false 반환
int index = stringList.IndexOf("b"); // 찾아서 인덱스 반환, 없으면 -1;
string? selectedString = stringList.Find(str=>{return str.StartsWith("a")}); // 조건에 맞는 첫 번째 요소 반환
List<string> selectedStrings = stringList.FindAll(str=>{return str.StartsWith("a")}); // 조건에 맞는 모든 요소 반환
