### 스택 (벡터) 응용 연습 - 괄호 검사 VPS

![image-20240707192643040](C:\Users\c\AppData\Roaming\Typora\typora-user-images\image-20240707192643040.png)

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

void VPS(string s) {

	vector<char> stack;
	for (int i = 0; i < s.length(); i++) {
		if(s[i]=='(')
			stack.push_back(s[i]);
		else if (s[i] == ')') {

			if (stack.size()==0) {
				cout << "NO\n";
				return;
			}

			char c = stack.back();
			stack.pop_back();
			if (c != '(') {
				cout << "NO\n";
				return;
			}
		}
	}

	if (stack.size() != 0) {
		cout << "NO\n";
	}
	else
		cout << "YES\n";
}

int main() {
	int t;
	cin >> t;
	cin.ignore(1);

	for (int i = 0; i < t; i++) {

		string s;
		getline(cin, s);
		VPS(s);
		
	}
}
```

