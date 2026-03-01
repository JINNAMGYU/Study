# C# - delegate #
대리자는 특정 메소드의 참조를 캡슐화하는 객체 -> 메소드를 변수처럼 사용

```csharp
void MyMethod(){
  ...
}

delegate void MyDelegate(); // 대리자 정의

MyDelegate myDelegate = MyMethod; // 정의한 대리자 선언 후 참조할 메서드 지정

myDelegate(); // myDelegate가 참조하고 있는 MyMethod 호출
```

```csharp
int MyMethod(int a, int b){
  ...
}

delegate int MyDelegate(int a, int b); // 반환 형식, 매개변수 목록이 일치해야 함

MyDelegate myDelegate = MyMethod;
int result = myDelegate(1,2);
```

### 멀티 캐스팅
```csharp
int Plus(int a, int b){
  Console.WriteLine("Plus");
  return a+b;
}
int Minus(int a, int b){
  Console.WriteLine("Minus");
  return a-b;
}

delegate int MyDelegate(int a, int b);

MyDelegate myDelegate = Plus;
myDelegate += Minus; // 두 메소드를 동시에 참조
//myDelegate -= Plus; 로 참조된 메서드를 제거 가능
int result = myDelegate(1,2); // 결과값은 마지막에 참조된 메서드값만 받음

// PlusMinus 출력, result = -1;
```

### 이벤트 ###
```csharp
delegate void ValueChangedHandler(int result, string message); // 대리자 정의

class Calcuate{
  public event ValueChangedHandler? OnValueChanged; // 대리자를 이벤트로 선언 (? : null일수도 있음)
  private int _value;

  public void Plus(int value){
    _value+=value;
    OnValueChanged(_value,$"{value}을 더했습니다."}; // value가 변화할 때 이벤트 발생시킴;
    //OnValueChanged?.Invoke(...) 를 쓰면 OnValueChanged가 null일 때 무시되어 안전함
  }
}

Calcuate calcuate = new Calcuate();
calcuate.OnValueChanged += Calcuate_OnValueChanged; // 이벤트 구독

void Calcuate_OnValueChanged(int result, string message){
  Console.WriteLine($"{message} , 현재 값 : {resulte}");
}

calcuate.Plus(2); // 이벤트에 참조된 메서드 호출됨
calcuate.Plus(4);
```
- 이벤트 특징
외부에서는 +=, -= 만 가능, 직접 호출 불가, 클래스 내부에서만 invoke -> 캡슐화, 안정성
### 매개변수 ###
대리자를 매개변수로 활용 가능함
```csharp
delegate int Operation(int a, int b);

void ApplyOperation(int a, int b, Operation operaion){
  int result = operation(a,b);
  Console.WriteLine(result);
}

int Plus(int a, int b) => a + b;
int Minus(int a, int b) => a - b;

ApplyOperation(2,3,Plus); // 5 출력
ApplyOperation(2,3,Minus); // -1 출력
```

- 사전 정의된 대리자

1. Func : 반환값이 있는 메서드 캡슐화
```csharp
void ApplyOperation(int a, int b, Func<int,int,int> operaion){ // 제네릭 맨 마지막은 반환값의 타입
  int result = operation(a,b);
  Console.WriteLine(result);
}

int Plus(int a, int b) => a + b;
int Minus(int a, int b) => a - b;

ApplyOperation(2,3,Plus); // 5 출력
ApplyOperation(2,3,Minus); // -1 출력
```
2. Action : 반환값이 없는 메서드 캡슐화
```csharp
void ActionMethod(string s, int i){..;}

Action<string,int> action = ActionMethod;
```
3. Predicate : bool값을 반환하는 메서드 캡슐화
```csharp
bool IsGreaterThanZero(int value){ return value > 0; }
Predicate<int> predicate = IsGreaterThanZero; 
```
4. Comparison : 두 값을 비교하고 정렬 순서를 나타내는 int 반환
```csharp
int Compare(int x, int y){
  return x.CompareTo(y);
}
Comparison<int> comparison = Compare;
```
### 람다 표현식 ###
매개변수를 받아 특정 작업을 수행하는 익명함수를 정의
-> 간단하게 함수를 작성하여 가독성, 간결성 굳

(매개변수) => {표현식}
```csharp
Func<int,int,int> operation = (a, b) => {return a+b;};
// Func<int,int,int> operation = (a, b) => a+b;
Action<int,int> operation = (a,b) => {Console.WriteLine(a+b);};
// Action<int,int> operation = (a,b) => Console.WriteLine(a+b);

- 사전 정의 대리자 + 람다가 많이 사용됨









