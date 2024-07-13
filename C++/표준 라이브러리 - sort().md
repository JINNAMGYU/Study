## 표준 라이브러리 - sort()



### 기본형태

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};
    std::sort(v.begin(), v.end());
    return 0;
}
```

- sort() - v의 요소들을 **오름차순**으로 정렬

#### 사용자 정의 비교 함수 사용

```c++
#include <algorithm>
#include <vector>

bool compare(int a, int b) {
    return a > b; // 내림차순 정렬
}

int main() {
    std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};
    std::sort(v.begin(), v.end(), compare);
    return 0;
}
```

- compare 함수가 두 요소를 비교하여 원하는 기준(내림차순)으로 정렬함

### 기타 유사함수

- stable_sort() - 안정 정렬 보장

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};
    std::stable_sort(v.begin(), v.end());
    return 0;
}
```

- partial_sort() - n개의 요소 까지만 정렬하다가 멈춤

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};
    std::partial_sort(v.begin(), v.begin() + 5, v.end());
    return 0;
}
```



등등

