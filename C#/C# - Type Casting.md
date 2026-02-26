# C# - 타입 캐스팅 #
---
### 명시적변환, 암시적변환
```csharp
int intNum=100;
double doubleNum = intNum; // 암시적 변환, 데이터 손실x

intNum=(int)doubleNum; // 명시적 변환, 데이터 손실O
```

### object 타입
- object : 모든 타입의 최상위격 타입
```csharp
object stringObject ="C#"; //boxing
object intObject = 123;
...

string s = (string)stringObject; //unboxing
```
- 성능 상 이유로 object 타입은 사용 지향

### Type 변환 (as) ###
```csharp
object obj = "C#";
string? str = obj as string; //타입 변환 실패 시 null
```

### Type 변환 (Convert Class) ###
```csharp
string strNum = "123";
int convertInt = Convert.ToInt32(strNum);
// int convertInt = (int)strNum; 오류!
```

### Type 변환 (is) ###
```csharp
object obj = "C#"
if(obj is string) // bool 타입 반환
  Console.WriteLine("성공!");
```
```csharp
object obj = "C#"
if(obj is string str) // 변환 가능하면 str로 변환해서 할당해줌
  Console.WriteLine(str);
```
