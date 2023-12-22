
# friend 함수 
일반함수는 private 멤버에 접근할 수 없으나 friend 멤버는 클래스 내의 멤버 함수들만 접근할 수 있도록 한다. 
- private 멤버에 접근 할 수 있도록 허용하는 것
- 프렌드 함수는 데이터 은닉에 위배되므로 예외적인 경우에만 사용함

## friend 함수 선언 형식
> friend 함수명 (매개변수 리스트);

## 조건
- 클래스 내부에 선언 : 접근할 private 멤버를 갖는 크래스 내부에 선언
- friend예약어 사용 : 함수명 앞에 예약어 friend를 붙여 함수를 선언함.

즉, friend는 일반함수가 클래스의 private 멤버변수에 접근이 가능하도록 해준다.
```cpp
class Complex {
private:
	int real;
	int image;

public:
	Complex(int x = 0, int y = 0);
	void ShowComplex() const;
	//클래스 내부에 friend로 해당 함수를 선언하면
	friend void prn(Complex* pCom);
};

//일반 함수가 클래스 private 멤버 변수에 직접 접근이 가능해진다.
void prn(Complex * pCom)
{
	for (int i = 0; i < 4; i++)
	{
		cout << "(" << pCom[i].real << " + " << pCom[i].image << ")" << endl;
	}
}



void main() {

	Complex arr[4] = {
		Complex(2,4),
		Complex(5,7),
		Complex(4,8),
		Complex(20,49)
	};
	Complex* pCom;
	pCom = arr;
	prn(pCom);
}

```


> A클래스의 멤버로 B클래스(포인터나 참조 제외)가 사용되었다면 두 클래스는 Composition관계이다. 반면 참조로만 접근하였다면 이는 Aggregation관계가 된다.