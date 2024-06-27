### Algorithm - 최대공약수(GCD) 최소공배수(LCM) 

- 최대공약수 - Brute force
  - 두 수 중 작은 수를 선택, 그 수 부터 1까지 모든 자연수를 나누면서 동시에 나누어 떨어지는 수를 찾는 방법 - O(n)

```c++
int min = a < b ? a : b;
for (int i = min; i > 0; i--) {
	if (a % i == 0 && b % i == 0) {
		cout << i<<'\n'; 
		break;
	}
}
```

- 최대공약수 - 유클리드 호제법
  - x % y = r 일 때, x와 y의 최대공약수는 y와 r의 최대공약수와 같다는 원리를 이용

```c++
int x = 12, y = 18, r = 1;
while(x % y != 0) {
	r = x % y;
    x = y;
    y = r;
}
cout << y; // 계속 대입하고 나누다가 r이 0이 되면 y가 최대공약수
return 0;
```

- 최소공배수
  - 두 수의 곱 / 최대공약수 = 최소공배수

```c++
lcm = a * b / gcd;
cout << lcm << '\n';
```

