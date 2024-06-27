### C++ 제네릭 기법

- 제네릭 프로그래밍 : **하나의 값이 여러 다른 데이터 타입들을 가질 수 있는 기술에 중점을 두어 재사용성을 높일 수 있는 프로그래밍 방식**

- 템플릿 : 제네릭 함수를 선언하고 컴파일 시간에 구체화 하기 위한 틀

```c++
template <class T> //템플릿
void myswap(T &a,T &b){ // 제네릭 함수
    T tmp;
    tmp=a;
    a=b;
    b=temp;
}

int a=4,b=5;
myswap(a,b); // myswap(int &a,int &b) 함수 구체화, 호출
double c=1.5,d=0.5;
myswap(c,d); // myswap(double &a,double &b) 함수 구체화, 호출
```

