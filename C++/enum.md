열거형 데이터 형식을 정의하는 데 사용한다.
enum은 상수들의 집합을 정의하고 이를 하나의 타입으로 취급할 수 있도록 해준다. 

```cpp
#include <iostream>
#include "CBST.h"

//열거형
enum MY_TYPE
{
	TYPE_1,	//	0
	TYPE_2,	//	1
	TYPE_3,	//	2
	TYPE_4,	//3
	TYPE_5 = 100,	// 100
	TYPE_6	,	//101
};
enum class OTHER_TYPE
{
	//enum class는 열거되는 변수들의 타입이 헷갈리지 않도록 도와준다.
	TYPE_10,	
};


int main() {
	
	//enum과 define의 차이 define 전처리기는 컴파일 이전단계에서 진행된다.
	int a = TYPE_1;
	//클래스형의 enum은 class 명을 명시적으로 작성함으로써 중복문제를 회피한다.
	int b =(int)OTHER_TYPE::TYPE_10;


	return 0;
}
```


>enum class
	enum class를 사용하지 않으면 열거되는 변수들의 중복문제가 발생할 수 있다.
	따라서 enum class로 사용하여 클래스명을 명시적으로 작성하도록 유도하여 고유의 변수를 사용하면서 예기치 못한 에러를 방지한다.

다음과 같이 반복되고 코드가 대칭적인 구조일 경우 enum class를 정의하여 코드를 좀더 간결하고 가독성을 높일 수 있다.

## 개선 전
```cpp
#pragma once
//노드안의 data 타입 구조체
template <typename T1, typename T2>
struct tPair
{
	T1 first;
	T2 second;

};

//실제 저장되는 노드타입 구조체
template <typename T1, typename T2>
struct tBSTNode
{
	//실제 data 파트
	tPair<T1, T2> pair;
	// 부모노드
	tBSTNode* pParent;
	// 자식노드
	tBSTNode* pLeftChild;
	tBSTNode* pRightChild;
	
};

//T1 키값으로 사용
//T2 데이터로 사용
template <typename T1, typename T2>
class CBST 
{
private :
	tBSTNode<T1,T2>* m_pRoot;		// 루트 노드 주소
	int m_iCound;					//	데이터 갯수

public :
	 bool insert(const tPair<T1, T2>& _pair);

public :
	CBST()
		: m_pRoot(nullptr)
		, m_iCound(0)
	{

	}
};

template<typename T1, typename T2>
inline bool CBST<T1, T2>::insert(const tPair<T1, T2>& _pair)
{
	//노드의 동적 생성
	tBSTNode<T1, T2>* pNewNode = new tBSTNode<T1, T2>();

	pNewNode->pair = _pair;
	pNewNode->pParent = nullptr;
	pNewNode->pLeftChild = nullptr;
	pNewNode->pRightChild = nullptr;

	//첫 번째 데이터 라면
	if (nullptr == m_pRoot)
	{
		m_pRoot = pNewNode;
	}
	else
	{
		//루트 노드가 존재한다면
		// 단말노드에 도달할때까지 비교 한다.
		//루트 노드 복사
		tBSTNode<T1, T2>* pNode = m_pRoot;
		while (true)
		{
			
			if (pNode->pair.first < pNewNode->pair.first)
			{
				if (nullptr == pNode->pRightChild)
				{
					pNode->pRightChild = pNewNode;
					pNewNode->pParent = pNode;
					break;
				}
				else
				{
					// 루트보다 크면 오른쪽으로 갱신
					pNode = pNode->pRightChild;
				}
			}
			else if (pNode->pair.first > pNewNode->pair.first)
			{
				if (nullptr == pNode->pLeftChild)
				{
					pNode->pLeftChild = pNewNode;
					pNewNode->pParent = pNode;
					break;
				}
				else 
				{
					//루트보다 작으면 왼쪽으로 갱신
					pNode = pNode->pLeftChild;
				}
			}
			else
			{
				//루트와 같은 값이면 
				return false;
			}
		}
	}
}


```


## 개선 후
```cpp
#pragma once
enum class NODE_TYPE
{
	PARENT,		// 0
	LCHILD,		// 1 
	RCHILD,		// 2
	END,				// 3
};	
//노드안의 data 타입 구조체
template <typename T1, typename T2>
struct tPair
{
	T1 first;
	T2 second;
};

//실제 저장되는 노드타입 구조체
template <typename T1, typename T2>
struct tBSTNode
{
	tPair<T1, T2> pair;
	tBSTNode* arrNode[(int)NODE_TYPE::END];
	tBSTNode()
		:pair()
		,arrNode{}
	{}
	tBSTNode(const tPair<T1,T2>& _pair, tBSTNode* _pParent, tBSTNode* _pLChild, tBSTNode* _pRChild)
		:pair(_pair)
		, arrNode{ _pParent , _pLChild ,_pRChild }
	{
	}
};

//T1 키값으로 사용
//T2 데이터로 사용
template <typename T1, typename T2>
class CBST 
{
private :
	tBSTNode<T1,T2>* m_pRoot;		// 루트 노드 주소
	int m_iCound;					//	데이터 갯수

public :
	 bool insert(const tPair<T1, T2>& _pair);

public :
	CBST()
		: m_pRoot(nullptr)
		, m_iCound(0)
	{

	}
};

template<typename T1, typename T2>
inline bool CBST<T1, T2>::insert(const tPair<T1, T2>& _pair)
{
	//노드의 동적 생성
	tBSTNode<T1, T2>* pNewNode = new tBSTNode<T1, T2>(_pair, nullptr, nullptr, nullptr);

	//첫 번째 데이터 라면
	if (nullptr == m_pRoot)
	{
		m_pRoot = pNewNode;
	}
	else
	{
		//루트 노드가 존재한다면
		// 단말노드에 도달할때까지 비교 한다.
		//루트 노드 복사
		tBSTNode<T1, T2>* pNode = m_pRoot;
		NODE_TYPE node_type = NODE_TYPE::END;

		while (true)
		{
			if (pNode->pair.first < pNewNode->pair.first)
				node_type = NODE_TYPE::RCHILD;
			else if (pNode->pair.first > pNewNode->pair.first)
				node_type = NODE_TYPE::LCHILD;
			else
				return false;
			//방향을 정하였기때문에 해당 방향의 노드로 값을 할당한다.
			if (nullptr == pNode->arrNode[(int)node_type])
			{
				pNode->arrNode[(int)node_type] = pNewNode;
				pNewNode->arrNode[(int)NODE_TYPE::PARENT] = pNode;
				break;
			}
			else
			{
				pNode = pNode->arrNode[(int)node_type];
			}
		}
	}
}

```