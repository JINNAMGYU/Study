# C#- class
---
### 클래스 구성요소
- 필드(field) : 클래스의 데이터, 상태를 나타내는 변수
- 프로퍼티(Property) : 필드에 대한 접근을 제어하는 멤버 (속성)
- 메서드(Method) : 클래스가 수행할 수 있는 동작 정의
- 생성자(Constructor) : 객체가 생성될 때 호출, 초기화 작업을 수행
- 소멸자(Destructor) : 객체가 소멸될 때 호출되는 메서드, 자원 정리를 수행
- 이벤트(Event) : 클래스 외부에서 발생하는 이벤트를 처리하는 메커니즘
- 인덱서(Indexer) : 클래스의 인스턴스를 배열처럼 사용할 수 있게 해주는 멤버



### 접근 제한자
- public : 모든 곳에서 접근 가능
- private : 동일 클래스 내에서 접근 가능
- protected : 동일 클래스 및 파생 클래스에서 접근 가능
- internal : 같은 어셈블리 내에서 접근 가능

### 가변 매개변수
```csharp
void Test(params string[] options){
  foreach(string option in options){
      // 처리---
    }
  }
Test("hi", "hello");
// ---> options = ["hi","hello"] 
```

### ref
매개변수로 참조를 넘김
```csharp
void Test(ref string a){
  a="b";
}
string a="a";
Test(ref a);  // ref로 인해 메서드 내 a,원래 a 둘 다 "b"로 할당
```
### out
ref와 비슷하나, out으로 받은 변수는 초기값이 필요없고 메서드 내에서 반드시 할당되어야 함

```csharp
void Test(out string a){
  a="b";  // 반드시 할당 필요
}

string result;
Test(out result);  // result = "b"

// C# 7.0 이상 (인라인 선언)
Test(out string result2);
```
 ### 프로퍼티
 필드 값을 안전하게 읽고 수정할 수 있음. 필요에 따라 추가 로직 포함 가능
```csharp
public class Person
{
  private string name; // 필드
  public string Name
  {
    get {return name;}  // 속성 값을 반환
    set {name = value;} // 속성 값을 설정
  }
}
```
```csharp
public class Person
{
  public string Name { get; set;} // 자동 구현 버전, 컴파일러가 백업 필드를 자동으로 생성함
}
```  







