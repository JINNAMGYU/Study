### C++ 스택 활용

- 백준 4949 https://www.acmicpc.net/problem/4949

![image-20241225204621653](C:\Users\jdc15\AppData\Roaming\Typora\typora-user-images\image-20241225204621653.png)

![image-20241225204646237](C:\Users\jdc15\AppData\Roaming\Typora\typora-user-images\image-20241225204646237.png)

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	
	while (true) {
		string s;
		vector<char> stack;
		getline(cin, s);
		if (s == ".")
			break;
		bool cheak = true;

		for (int i = 0; i < s.length(); i++) {
			if (s[i] == '(' || s[i] == '[')
				stack.push_back(s[i]);
			else if (s[i] == ')') {
				if (stack.empty() || stack.back() != '(') {
					cheak = false;
					break;
				}
				else
					stack.pop_back();
			}
			else if (s[i] == ']') {
				if (stack.empty() || stack.back() != '[') {
					cheak = false;
					break;
				}
				else
					stack.pop_back();
			}
		}
		if (stack.empty()==false)
			cheak = false;

		if (cheak == true)
			cout << "yes" << endl;
		else
			cout << "no" << endl;
	}
}
```

