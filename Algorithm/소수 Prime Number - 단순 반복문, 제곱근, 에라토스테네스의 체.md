### 소수 Prime Number - 단순 반복문, 제곱근, 에라토스테네스의 체

---

- **소수** : 1과 자기자신을 제외하고 약수를 갖지 않는 1보다 큰 자연수

#### 알고리즘 1 - O(n)

- 2부터 해당 수 까지 나누어 보며 나누어 떨어지는 수가 있다면 합성수, 없다면 소수

```c++
bool isPrime(int n) {
    for (int i = 2; i < n; i++) { // 2부터 n까지 모든 자연수를 나누어 보며 판별
        if (n % i == 0)
            return false;
    }
    return true;
}
```



#### 알고리즘 2 - O(**√**N)

- 약수를 구할 때, 해당 수의 제곱근을 기준으로 좌측과 우측의 수가 짝을 이루게 되는 성질 이용
  - ex) 81의 약수:1,3,9,27,81,  제곱근 81 : 9 => 1-81 / 3-27 / 9
  - 즉 1~ 9(제곱근) 까지의 수 중 약수를 구하면 자동으로 짝을 이루는 약수도 구해짐

- 즉 2부터 모든 자연수를 나눌 필요 없이 제곱근 까지의 수만 나누어 보면 소수 판별이 가능

```c++
bool isPrime(int n) {
    for (int i = 2; i <= sqrt(n); i++) { // sqrt()로 n의 제곱근까지만 계산하며 판별
        if (n % i == 0)
            return false;
    }
    return true;
}
```



#### 알고리즘 3 - O(Nlog(logN)) : 에라토스테네스의 체 알고리즘

- 해당 수가 소수라면 해당 수의 배수들은 모두 소수가 아니라는 원리를 이용

1. 2부터 원하는 수 n까지 숫자들을 나열
2. 숫자들이 소수인지 나타내는 bool 배열 생성, 모두 true로 초기화
3. 배열의 첫번째 소수인 2부터 시작하여 그 숫자가 소수이면 그 숫자의 배수를 모두 false로 표시
4. 다음 숫자로 이동하며 배열 끝까지 표시 반복
5. 마지막 까지 true로 남은 숫자들은 모두 소수

- **큰 범위의 소수를 한번에 구하는 상황에 유용함**

```c++
void isPrime(int n) {
    bool* isprime = new bool[n+1]; // 인덱스를 n까지 사용해야하므로 n+1개 할당

    for (int i = 0; i <= n; i++)
        isprime[i] = true; //모든 요소를 true로 초기화

    isprime[0] = isprime[1] = false; // 0과 1은 제외

    for (int i = 2; i*i <= n; i++) { // 알고르즘 적용
        if (isprime[i]) {
            for (int j = i * i; j <= n; j += i)
                isprime[j] = false; // i의 배수를 false로 설정
        }
    }
   
    for (int i = 2; i <= n; i++) { // 소수 출력
        if (isprime[i])
            cout << i << endl;
    }
    
    delete[] isprime;
}
```

