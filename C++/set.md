set은 이진 탐색 [[트리]]로 구현되어 있는 라이브러리이다.
데이터를 추가하면 각 요소는 자동으로 정렬되고 중복된 값을 허용하지 않는다. 
$O(logN)$의 탐색과 입력의 효율을 가진다. 

```cpp
#include <iostream>
#include <set>

using std::set;
using namespce std;

int main(){
// int 타입을 가지는 set을 생성
set<int> mySet;

//set에 데이터 추가
mySet.insert(5);
mySet.insert(3);
mySet.insert(8);
mySet.insert(2);

//set을 순회하며 값을 출력
for(const int& value : mySet)
{
	cout << value << endl;
}
// 5
// 3
// 8
// 2
//set에서 원하는 값을 찾기
int searchValue = 5;
//end는 값을 끝까지 찾아가면서 end까지 도달할때 값이 없는 것이다.
//end가 아니라는 것은 값이 있다는 것이다.
if(mySet.find(searchValue) != mySet.end())
{
	cout<< searchValue << "값을 찾았습니다." <<endl;
}
else
{
//end 일 경우가 되며 값이 없다는 것 이다.
	cout<< searchValue << "값을 못 찾았습니다.." <<endl;
}

//set에서 값 삭제
int removeValue = 5;
mySet.erase(removeValue);

//변경된 set 출력

for(const int& value : mySet)
{
	cout << value << endl;
}

//3
//8
//2
return 0;
}
```

set은 vector와 마찬가지로 객체를 생성하고 insert함수를 이용하여 값을 추가하고 for문을 이용하여 값을 출력한다. find함수는 값을 찾는 역할을 한다. 

