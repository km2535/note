스택(stack)
- 접시를 쌓듯이 자료를 차곡차곡 쌓아 올린 형태의 자료구조

스택에 저장된 원소는 top으로 정한 곳에서만 접근 가능

- top의 위치에서만 원소를 삽입하므로, 먼저 삽입한 원소는 밑에 쌓이고 나중에 삽입한 원소는 위에 쌓이는 구조
- 마지막에 삽입한 원소는 맨 위에 쌓여 있다가 먼저 삭제됨

이러한 구조를 LIFO(Last In First Out) 구조라고 한다.


다음 코드를 실행 시 스택의 결과는 아래와 같다.
```cpp
void x (){  }
void y (){  }
void z (){
	x();
	y();
}
void main(){ 
	z();
}
```

### 스택 순서 
| |empty| | |empty| | |empty| |top|empty| | |empty| 
|-|-|-|-|-|-|--|--|--|--|--| --|--|--|--|
||empty|| |empty||top |empty|||x|| top|empty|
||empty|| top|empty|||z|||z|||z|
|top|empty|||main|||main|||main|||main|


|top|empty| | |empty| | |empty| | |empty| 
|-|-|-|-|-|-|--|--|--|--|--|
||y|| top |empty|||empty|||empty|
||z|| |z||top|empty||  |empty|
||main|| |main|||main||top|empty|


1. main 함수 실행 
2. z 함수 실행
3. x 함수 실행
4. x 함수 종료
5. y함수 실행
6. y함수 종료
7. z함수 종료
8. main함수 종료


스택에서의 연산은 pop과 push를 사용한다.

## 스택의 push 알고리즘
```algorism
push(S, x)
	top <- top + 1;
	if(top > stack_SIZE) then overflow;
	S(top) <- x;
end push()
```

스택 S에서 top이 마지막 자료를 가리키고 있으므로 그 위에 자료를 삽입하려면 먼저 top의 위치를 하나 증가
이때 top의 위치가 스택사이즈보다 크면 memory overflow로 연산을 중지 

## 스택의 pop 알고리즘
```algorism
pop(S)
	if(isStackEmpty(S)) then underflow;
	else{
		return S(top);
		top <- top - 1;
	}
```

공백 스택이 아니면 top에 있는 원소를 삭제하고 반환
스택의 마지막 원소가 삭제되면 그 아래 원소, 즉 스택에 남아있는 원소 중에서 가장 위에 있는 원소가 top이 되어야 하므로 top 위치를 하나 감소


# stack 배열로 구현
```cpp
#pragma once
#define STACK_SIZE 100

typedef int element;// element 타입을 int형으로 정의
element stack[STACK_SIZE];

int isStackEmpty(); 
int isStackFull();
void push(element items);
element pop();
element peek();
void printStack();

```

```cpp

#include <iostream>
#include "stack.h"


using namespace std;
int top = -1;

int main() {

	element item;
	printStack();
	push(1);
	printStack();

	push(2);
	printStack();

	push(3);
	printStack();

	item = peek(); 
	printStack();
	std::cout << item << std::endl;

	item = pop();
	printStack();
	std::cout << item << std::endl;
	
	item = pop();
	printStack();
	std::cout << item << std::endl;

	item = pop();
	printStack();
	std::cout << item << std::endl;

	
	return 0;
}

//스택이 공백인지 확인하는 함수
int isStackEmpty()
{
	if (top == -1) return 1;
	return 0;
}
//스택이 포화인지 확인하는 함수
int isStackFull()
{
	if (top == STACK_SIZE - 1) return 1;
	return 0;
}

void push(element items)
{
	// stack 이 가득차면 경고 메시지
	if (isStackFull())
	{
		cout << "stack is full" << endl;
		return;
	}
	else
	{
		stack[++top] = items;
	}
}

element pop()
{
	if (isStackEmpty())
	{
		cout << "stack is empty" << endl;
		return 0;
	}
	else
	{
		return stack[--top];
	}
}

element peek()
{
	if (isStackEmpty())
	{
		cout << "Stack is empty" << endl;
		exit(1);
	}
	else
	{
		return stack[top];
	}
}

void printStack()
{
	cout << "Stack [  ";
	for (int i = 0; i <= top; i++)
	{
		cout << stack[i];
	}
	cout << " ] " << endl;
}

```

# stack 리스트로 구현
```cpp
#pragma once
#define STACK_SIZE 100

typedef int element;// element 타입을 int형으로 정의

struct stackNode
{
	element data;
	struct stackNode* link;
};

stackNode* top;

int isStackEmpty(); 
void push(element items);
element pop();
element peek();
void printStack();
```

```cpp

#include <iostream>
#include "stack.h"


using namespace std;

int main() {

	element item;
	printStack();
	push(1);
	printStack();

	push(2);
	printStack();

	push(3);
	printStack();

	item = peek(); 
	printStack();
	std::cout << item << std::endl;

	item = pop();
	printStack();
	std::cout << item << std::endl;
	
	item = pop();
	printStack();
	std::cout << item << std::endl;

	item = pop();
	printStack();
	std::cout << item << std::endl;

	
	return 0;
}

//스택이 공백인지 확인하는 함수
int isStackEmpty()
{
	if (top == nullptr) return 1;
	return 0;
}


void push(element items)
{
	stackNode* temp = new stackNode;
	temp->data = items;
	temp->link = top;
	top = temp;
}

element pop()
{
	element item;
	stackNode* temp = top;

	if (isStackEmpty()) {
		cout << "stack is empty" << endl;
		return 0;
	}
	else {
		item = temp->data;
		top = temp->link;
		delete temp;
		return item;
	}
}

element peek()
{
	if (isStackEmpty())
	{
		cout << "stack is empty" << endl;
		return 0;
	}
	else {
		return top->data;
	}
}

void printStack()
{
	stackNode* p = top;
	cout << "Stack [  ";
	while (p)
	{
		cout << p->data;
		p = p->link;
	}
	cout << " ] " << endl;
}

```

## 수식을 검사하는 함수 추가
```cpp

int testPair(const char* exp) {
	char symbol, open_pair;
	int length = strlen(exp);
	top = nullptr;
	for (int i = 0; i < length; i++)
	{
		symbol = exp[i];
		switch (symbol)
		{
		case '(':
		case '[':
		case '{':
			push(symbol); break;
		case ')':
		case ']':
		case '}':
			if (isStackEmpty()) return 0;
			else {
				open_pair = pop();
				if ((open_pair == '(' && symbol != ')') ||
					(open_pair == '[' && symbol != ']') ||
					(open_pair == '{' && symbol != '}'))
					return 0;
				else break;
			}
		default:
			break;
		}
	}
	if (top == nullptr) return 1;
	else return 0;
}
```

main
```cpp

	const char* express = "{(A+B) -3}*5 + [{cos(x+y)+7}-1]*4";
	std::cout << express << std::endl;
	if (testPair(express) == 1) {
		std::cout << "굳" << std::endl;
	}
	else {
		std::cout << "bed" << std::endl;
	}

```

