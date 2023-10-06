형식 매개변수가 실 매개변수와 별개의 기억공간을 할당 받아 값을 복사함.
함수를 정의한 곳에서 형식 매개변수의 값을 변경해도 실 매개변수의 값은 변경되지 않음.

```cpp
#include <iostream>
using std::cout;
using std::endl;

int add(int x, int y)
{
	x = x + y;
	return x;
}

int main() {
	int a = 10;
	int b = 20; 
	
	int sum = add(a, b);

	cout << sum << endl; // 30;
	return 0;
}
```

실 매개변수에서 값을 직접 전달하는 방식으로 형식 매개변수는 별도의 기억공간을 할당 받는다.
즉, a, b, sum, x, y 모두 다른 주소 값을 가진다. 

또한 x는 별도의 기억 공간을 할당하였기 때문에 x의 값은 변경되어도 a의 값은 그대로 이다.

