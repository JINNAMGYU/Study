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
Test(ref a);  // ref로 인해 메서드 내 a,원래 a 둘 다 "b"로 변경됨
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

//추가 로직 구현 예시
get{ return $"**{name}**";}
set{ name = $"##{value}##";}
```
- 자동 구현 프로퍼티
```csharp
public class Person
{
  public string Name { get; set;} // 자동 구현 버전, 컴파일러가 백업 필드를 자동으로 생성함
}
```
### 정적 타입
static으로 선언된 메서드, 필드, 프로퍼티 등은 클래스 자체에 속함 => 인스턴스 없이 호출 가능
```csharp
class MyClass{
  public static string name = "hi";
  public static void Print(){ Console.WriteLine(name);}
}

MyClass.print();
```
정적 메서드는 정적 멤버에만 접근 가능

- 정적 클래스 : 인스턴스를 생성할 수 없으며 모든 멤버가 static
```csharp
static class MyClass{
  public static string name = "hi";
  public static void Print(){ Console.WriteLine(name);}
}
```

### 확장 함수
```csharp
strint name = "john";
name.Print(); // 이런 함수는 원래 없음

static class MyClass{
  public static void Print(this string text){
    Console.WriteLine(text);
  }
} // 이를 통해 name.Print()가 활성화 됨. ( MyClass.Print(name)도 됨 )
```
확장함수는 담긴 클래스, 함수 자신 모두 static이여야만 함
### 상속
```csharp
class Animal{ //부모클래스
  public void Eat();
}
class Dog : Animal{ //자식클래스, Animal의 멤버들을 상속받아서 Dog가 다 사용할 수 있음
 public void Bark();
}
```
```csharp
// override,new

class Animal{
  public virtual void Eat(){...};
}
class Dog : Animal{ 
 public override void Eat(){ ... }; //override를 통해 부모의 메서드를 재정의해서 사용
}

class Cat : Animal{
 public new void Eat(){ ... }; //new를 통해 부모의 메서드를 숨기고 자식의 메서드를 사용
}

Animal dog = new Dog(); // override - 업캐스팅된 인스턴스에서 Eat() 호출 시 Dog의 Eat() 호출됨
Animal cat = new Cat(); // new - 업캐스팅된 인스턴스에서 Eat() 호출 시 Animal의 Eat() 호출됨
```

### 추상클래스
추상 클래스는 인스턴스화 불가능, 추상메서드를 가지고 있어 자식클래스에서 추상메서드가 구현되어야 함
```csharp
abstract class Shape{
 public abstract void Draw();
}
class Circle : Shape{
 public override void Draw(){ ...; }
}
```

### sealed
sealed 키워드로 선언한 클래스, 메서드는 더이상 상속, 재정의 불가능

