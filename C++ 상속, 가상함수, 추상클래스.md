### C++ 상속, 가상함수, 추상클래스

#### 상속 

- 클래스 사이에 상속관계 선언 -> 기본클래스의 멤버를 파생클래스에 포함시킴

- 파생클래스에서 기본클래스의 private 멤버 이외에 모든 멤버 접근 가능 

- 계층적 분류, 관리 용이, 클래스 재사용과 확장으로 생산성 향상

  #### 가상함수

  - virtual로 선언, 자신의 호출바인딩을 실행시간으로 미룸
  - 가상함수를 파생클래스에 재작성 -> 오버라이딩
  - 함수를 호출 시 항상 오버라이딩 된 함수가 실행
  - 범위지정 연산자( :: )를 사용 시 기본클래스 함수 호출 가능

```c++
class Point{
protected:
    int x,y;
public:
    virtual void show(){ cout<<"("<<x<<","<<y<<")"<<endl;} //가상함수
}

class colorPoint:public Point{
    string color;
public:
	virtual void show(){ cout<<color<<":("<<x<<","<<y<<")"<<endl;} //오버라이딩
}
```

#### 추상클래스

- 클래스에 순수가상함수 선언 -> 추상클래스 -> 아직 객체를 생성할 수 없음
- 파생클래스에서 가상함수를 구현해야만 객체를 생성할 수 있게 됨
- 설계와 구현을 분리, 계층적 상속 관계를 만들기에 적합

```c++
class Point{ //추상클래스
protected:
    int x,y;
public:
    virtual void show() = 0; //순수가상함수
}

class colorPoint:public Point{
    string color;
public:
	virtual void show(){ cout<<color<<":("<<x<<","<<y<<")"<<endl;} 
}
```

