# C# - interface
---
클래스나 구조체가 구현해야 하는 멤버의 집합을 정의, 인터페이스는 클래스 간의 계약(contract)
- 인터페이스는 특정 기능을 수행하기 위한 메서드, 속성, 이벤트 도안을 정의, 실제 구현은 클래스나 구조체에서
- 인터페이스 타입으로 객체를 다루면 세부 구현을 몰라도 필요한 기능호출이 가능함 => 추상성

```csharp
public interface IAnimal{
  void MakeSound();
  string Name { get; set;}
}

public class Dog : IAnimal{ // 클래스나 구조체가 인터페이스를 상속받도록 하여 사용
  public string Name {get; set;}
  public void MakeSound(){
    ...
  }
  // 구현 시 인터페이스의 멤버를 모두 구현해야만 함
}
```
- 메서드, 속성, 이벤트를 정의가능, 구현 세부사항은 X
- 인터페이스 내에선 필드를 정의할 수 없음

### 다중 구현
- 하나의 클래스가 여러 인터페이스를 구현할 수 있음
```csharp
public class Duck : IAnimal, IFlyable, ISwimable {
  public ...
  ... // 모두 구현
}
```

### 명시적 인터페이스 구현
- 인터페이스 멤버를 클래스의 다른 멤버와 구분하기 위해 명시적 구현 가능->인터페이스로만 접근 가능
- 이름 충돌 시 사용
```csharp
public class Cat : IAnimal{
  public string Name {get; set;}
  void IAnimal.MakeSound(){ //명시적 구현
    Console.WriteLine("야옹!");
  }
}
IAnimal animal = new Cat();
animal.MakeSound(); // "야옹!" 

Cat cat = new Cat();
cat.MakeSound(); // 컴파일 오류
```
### 디폴트 구현
C# 8.0 이후론 인터페이스에 디폴트 구현을 제공, 인터페이스에 메서드 기본 구현을 포함 가능, 클래스는 필요에 따라 오버라이드 가능
```csharp
public interface IAnimal{
  public string Name {get; set;}
  void MakeSound(){ // 디폴트 구현
    Console.WriteLine("야옹!");
  }
}

public class Dog : IAnimal{
  public string Name {get; set;}
  ... //필요에 따라 디폴트 구현을 그냥 사용하거나 오버라이드
}

Dog myDog = new Dog();
// myDog.MakeSound(); // 만약 Dog에서 구현하지 않았다면 컴파일 에러!

IAnimal animal = myDog;
animal.MakeSound(); // 인터페이스 타입을 통해서만 디폴트 구현 호출 가능
```

### 인터페이스 vs 추상 클래스 (Abstract Class)

| 구분 | 인터페이스 (Interface) | 추상 클래스 (Abstract Class) |
| --- | --- | --- |
| **핵심 목적** | 클래스의 **행위(Can-do)**를 정의 | 클래스의 **정체성(Is-a)**을 정의 |
| **상속** | 다중 구현 가능 | 단일 상속만 가능 |
| **필드(변수)** | 가질 수 없음 | 가질 수 있음 |
| **접근 제한자** | 기본적으로 `public` | 다양한 제한자 사용 가능 (`protected` 등) |

- 추상 클래스 : "뿌리가 같은 혈연관계". 공통된 **성질(데이터)**과 기능을 물려줄 때 씁니다. (예: 사과, 바나나 → 과일)
= 인터페이스 : "할 줄 아는 기능". 뿌리가 달라도 공통된 행위가 가능하다면 묶어줍니다. (예: 사람, 비행기 → 이동할 수 있는)
