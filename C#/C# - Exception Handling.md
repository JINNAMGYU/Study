# C# - 예외 처리 #
---
프로그램 실행 중 발생할 수 있는 오류를 효과적으로 관리하는 기능

### try - catch
- try : 예외가 발생할 가능성이 있는 코드를 감싸는 블록
- catch : 예외 발생 시 실행되는 블록
```csharp
int[] ints = [1,2,3];

try
{
  int i= ints[5];
}
catch
{
  Console.WriteLine("예외!");
}
```

### 예외 객체
- Exception : 모든 예외의 부모 객체
- IndexOutOfRangeException : 배열이나 컬렉션의 범위를 벗어난 인덱스에 접근할 때 발생
- InvaildCastException : 잘못된 형 변환을 시도할 때 발생
- NullReferenceException: 할당되지 않은(null) 객체의 멤버를 참조할 때 발생
```csharp
int[] ints = [1,2,3];
object obj = "abc";

try
{
  int i= ints[5];
  double d = (double)obj;
}
catch(IndexOutOfRangeException ex) // 특정 예외 먼저
{
  Console.WriteLine("IndexOutOfRangeException 예외!");
}
catch(InvaildCastException ex)
{
  Console.WriteLine("InvaildCastException 예외!");
}
catch(Exception ex)   // 일반 예외 (default)
{
  Console.WriteLine("예외!");
}
```

### finally
- 예외 발생 여부와 관계없이 항상 실행되는 블록, 주로 자원 정리에 사용
```csharp
object obj = "abc";

string Error()
{
  try
  {
    double d = (double)obj;
  }
  catch(Exception ex)
  {
     return "Exception 예외 발생!";
  }
  finally // return 되기 전 반드시 실행
  {
    obj=null;
  }
  return "";
}

try
{
  int i= ints[5];
  double d = (double)obj;
}
catch(Exception ex)
{
  Console.WriteLine("예외!");
}
```

### 사용자 정의 예외 처리 ###
```csharp
class CustomException : Exception
{
  public CustomException(string message, int a, int b) : base(message)
  {
    A = a;
    B = b;
  }
  public int A {get;}
  public int B {get;}
}

try
{
  throw new CustumException("커스텀 에러",10,23);
}
catch(CustomException ex)
{
  Console.WriteLine($"{ex.Message} {ex.A} {ex.B}");
}
```
