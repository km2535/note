- 별칭(다른 이름)을 의미함.
- 따로 기억공간이 할당되지 않음.
- 메모리 상에 오로지 하나만 존재하는 변수를 여러 이름으로 접근해서 사용할 수 있게 함.

## 참조변수의 선언
```cpp
자료형 &별칭으로 사용할 변수명 = 앞서 선언된 변수명

int a = 10;
int &referenceA = a;
```

a와 referenceA는 주소 값, value도 동일하다.
- 선언 시 들어가는 &기호는 참조 연산자이다.
- 선언과 동시에 초기값을 할당해야 한다.
```cpp
#include <iostream>
using std::cout;
using std::endl;


int main() {
	int a = 10; 
	int& Ra = a;
	cout << "a의 주소 : " << &a << endl; // 000000A2485DFC74
	cout << "&Ra의 주소 : " << &Ra << endl; // 000000A2485DFC74

	cout << "a의 값 : " << a << endl; // 10
	cout << "Ra의 값 : " << Ra<< endl; // 10
	return 0;
}


```

Ra의 값을 변경하면 a의 값도 변경된다.
```cpp

int main() {
	int a = 10; 
	int& Ra = a;
	b += 300; 
	cout << "a의 값 : " << a << endl; // 310
	cout << "Ra의 값 : " << Ra<< endl; // 310

	return 0;
}

```

함수를 만들어 참조에 의한 전달을 해보자'
```CPP
#include <iostream>
using std::cout;
using std::endl;

void swap(int& a, int& b);

int main() {
	int a = 10; 
	int b = 20;
	swap(a, b);
	cout << a << "  " <<  b <<endl;

	return 0;
}

void swap(int& Ra, int& Rb)
{
	// 참조를 받으면 Ra와 Rb는 a와 b의 동일한 주소, 값을 가진다.
	int t; // 임시 저장공간.
	t = Ra; // Ra의 값을 할당
	Ra = Rb; //Ra에 Rb를 할당, a의 주소가 동일하므로 a의 값이 변경된다.
	Rb = t; // Rb에 t의 값을 할당, b의 주소가 동일하므로 b의 값이 변경된다.
}
```