map을 사용하면 키 - 값 쌍을 이용해 자료구조를 저장할 수 있다. 
각각의 요소는 유일한 키를 가지며 해당 키에 대응하는 값을 저장한다. 
이러한 특성으로 인해 map은 맵핑 또는 딕셔너리 구조로 사용 될 수 있다. 
만약 동일한 키가 존재한다면 요소는 추가되지 않고 기존 값에 업데이트한다. 

```cpp
#include <iostream>
#include <map>
#include <string>


// 사용자 정의 구조체
struct FruitInfo{
	std::wstring name;
	int quantity;

	//생성자 함수
	FruitInfo(const std::wstring& _name, int _qauntity)
		: name(_name)
		, quantity(_qauntity)
	{
	}
}

int main(){
	//whcar_t 타입의 키와 구조체를 값으로 하는 map생성
	std::map<const wchar_t*, FruitInfo> fruitMap;
	//insert를 이용해서 값을 추가
	// insert를 이용할 때는 make_pair함수를 이용해야한다. 
	// 생성자 함수를 재정의하여 값을 넣으면서 초기화하였다.
	fruitMap.insert(std::make_pair(L"Apple", FruitInfo(L"Red Apple", 5)));
	fruitMap.insert(std::make_pair(L"Banana", FruitInfo(L"Yellow Banana", 3)));

	//map에 값을 넣으면 다음과 같이 for문을 이용하여 출력할 수 있다.
	for(auto it  = fruitMap.begin(); it != fruitMap.end(); ++i)
	{
		//키 값을 출력
		const wchar_t* key = it -> first;
		const FruitInfo& info = it->second;

		
       std::wcout << L"Key: " << key << L", Name: " << info.name << L", Quantity: " << info.quantity << std::endl;
    }
	
}

//Key: Apple, Name: Red Apple, Quantity: 5
//Key: Banana, Name: Yellow Banana, Quantity: 3
