# C# 문자열
---
텍스트 데이터를 표현하는 데이터타입, 문자열은 불변

### 선언, 초기화
```csharp
string hi = "hello";
string empty = ""; // 빈문자열
string nulls = null; // null
```

### 문자열 연결
```csharp
string s1 = "hi";
string s2 = "namgyu";
string s3 = s1 + " " + s2; // "hi namgyu"
```

### 문자열 보간
문자열 내에 변수 값을 포함
```csharp
string s1 = "hi";
string s2 = "namgyu";
string s3 = $"{s1} {s2}"; // "hi namgyu"
```

### 문자열 형식화
```csharp
string formatted = string.Format("name: {0}, age: {1}", name, age);
```

### 문자열 속성, 메서드
```csharp
int length = s1.Length; // 문자열 길이
```
```csharp
string part = s1.Substring(0,5); //0번에서 5번인덱스 까지만 추출
```
```csharp
bool check = s1.Contains("hi"); // 문자열 포함여부 확인
```
등등 많음...
