포인터형으로 선언하여 실 매개변수의 주소를 넘겨 받음.
형식 매개변수의 값을 변경하면 실 매개변에 그대로 반영됨.

```cpp
#include <iostream>
using std::cout;
using std::endl;

void swap(int* a, int* b); //실 매개변수의 주소를 받을 포인터 변수 선언

int main() {

	int a = 10;
	int b = 20;
	swap(&a, &b); // 변수의 주소를 넘겨줌.
	cout << a << "  "  << b << endl;

	return 0;
}

void swap(int* a, int* b)
{
	int t; // 임시 저장공간.
	t = *a; // a의 주소가 가르키는 값을 t에 저장. 
	*a = *b; // a 포인터 변수의 값을 b포인터 변수의 값으로 변경. /
	// 위 에서 변수 a의 값이 변경된다.
	*b = t; // b 포인터 변수의 값을 t로 변경.
	// 위에서 변수 b의 값이 변경된다.
}

```

swap함수에서 받아온 포인터 변수는 실제 a, b의 값을 가르키고 있기 때문에 메모리 상에서의 a, b의 값을 변경할 수 있다. 