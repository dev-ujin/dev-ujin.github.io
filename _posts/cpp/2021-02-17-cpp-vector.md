---
layout: post
title: "[C++] STL :: Vector :: 01. 선언, 초기화, 멤버함수"
date: 2021-02-17 22:07:00 0800
categories: cpp
tags: cpp
comments: 1
changefreq: daily
priority: 1
---

> 🚧작성중🚧

# 🏁벡터란?
**동적인 배열**. 원소의 추가와 삭제가 일어나면 자동적으로 재배열해준다. 

# 🏁헤더파일
```cpp
#include <vector>
```

# 🏁생성과 초기화
- 벡터는 동적이기 때문에 생성시에 크기를 명시하지 않아도 된다.

```cpp
// 비어있는 벡터 vec 생성
vector <int> vec;

// 0으로 초기화 된 벡터 vec 생성
vector <int> vec(3); // {0, 0, 0}

// 1, 2, 3을 원소로 가지는 벡터 vec 생성
vector <int> vec = {1, 2, 3};
vector <int> vec{1, 2, 3};
```

# 🏁멤버함수
## [1] 반복자(Iterator) 관련 함수
- `begin()` : 첫 번째 원소를 가리키는 반복자
- `end()` : 마지막 원소를 가리키는 반복자
- `rbegin()` : 마지막 원소를 가리키는 반복자 (reverse beginning)
- `rend()` : 첫 번째 원소를 가리키는 반복자 (reverse end)
- `cbegin()` : 첫 번째 원소를 가리키는 상수 반복자 (constant begin)
- `cend()` : 마지막 원소를 가리키는 상수 반복자 (constant end)
- `crbegin()` : 마지막 원소를 가리키는 반복자 (contant reverse begin)
- `crend()` : 첫 번째 원소를 가리키는 반복자 (constant reverse end)
 
###### 🔽 r(reverse)는 역방향으로 벡터를 순회하고 싶을 때 사용한다.

```cpp
vecter <int> vec = {1, 2, 3, 4, 5};

// 정방향 반복문
for (auto itr = vec.begin() ; itr != vec.end() ; ++itr) {
    cout << *itr << " ";
}

===== console ===== 
1 2 3 4 5


// 역방향 반복문
for (auto itr = vec.rbegin() ; itr != vec.rend() ; ++itr) {
    cout << *itr << " ";
}

===== console =====
5 4 3 2 1
```

###### 🔽 c(constant)는 반복자가 가리키는 값을 변경할 수 없다.

```cpp
vector <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.begin() ; itr != vec.end() ; ++itr) {
    *itr = *itr + 10;
    cout << *itr << " ";
}

===== console =====
11 12 13 14 15
```
```cpp
// 에러
vector <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.cbegin() ; itr != vec.cend() ; ++itr) {
    *itr = *itr + 10;
    cout << *itr << " ";
}
```

### 🙋‍♀️ 질문 1 : **r(reverse)**이 왜 필요할까?
그냥 간단하게 순서만 바꿔서 end()을 먼저 쓰고 begin()을 나중에 쓰면 되는 거 아닌가? rbegin(), rend()는 왜 필요하지? 코드상 보기 예쁘라고 그런건가? 라는 생각을 했었다. 코드를 돌려본 결과 **반복문에서 반복자는 end()로 시작할 수 없다.**
```cpp
// 에러
for (auto itr = vec.end() ; itr != vec.begin() ; ++itr) {
    ...
}
```

## [2] 크기/용량(Size/Capacity) 관련 함수

- size() : 벡터 원소의 갯수
- capacity() : 메모리에 할당된 용량을 원소의 갯수로 표현
- max_size() : 벡터가 최대로 가질 수 있는 원소의 갯수
- resize(n) : 벡터의 크기를 n으로 재설정
- reserve(n) : 벡터가 n개의 요소를 담을 수 있도록 capacity를 조정
- empty() : 벡터가 비어있는지 검사
- shrink_to_fit() : capacity를 size에 맞추어 축소

> 주로 헷갈릴 수 있는 개념으로 size와 capacity를 같이 다루고, resize와 reserve를 함께 비교한다. 코드를 통해 용법과 특징을 비교해본다.

### size() / capacity()

###### 🔽 capacity는 size가 증가할 때 같이 증가하지만, size가 감소한다고 해서 같이 감소하지는 않는다.
- size와 capacity 모두 가변적인 요소이다.
- capacity가 size를 따라 같이 증가한다고 해서 같은 양으로 증가하는 것은 아니다. capacity는 항상 size와 같거나 크다.

```cpp
vector <int> vec;

cout << "[initial status] ";
cout << "size : " << vec.size() << ", ";
cout << "capacity : " << vec.capacity() << endl;

vec.push_back(1);
vec.push_back(2);
vec.push_back(3);
vec.push_back(4);
vec.push_back(5);

cout << "[after push_back] ";
cout << "size : " << vec.size() << ", ";
cout << "capacity : " << vec.capacity() << endl;

vec.pop_back();
vec.pop_back();

cout << "[after pop_back] ";
cout << "size : " << vec.size() << ", ";
cout << "capacity : " << vec.capacity() << endl;


===== console =====
[initial status] size : 0, capacity : 0
[after push_back] size: 5, capacity : 8
[after pop_back] size: 3, capacity : 8
```

### resize(n) / reserve(n)
###### 🔽 resize(n)는 벡터의 size를 항상 n으로 바꾸고, reserve(n)는 벡터의 capacity가 n보다 작은 경우에만 n으로 바꾼다.

```cpp

vector <int> vec = {1, 2, 3, 4, 5};

cout << "[initial status] ";
cout << "size : " << vec.size() << ", ";
cout << "capacity : " << vec.capacity() << endl;

vec.resize(7);

cout << "[after resize] ";
cout << "size : " << vec.size() << ", ";
cout << "capacity : " << vec.capacity() << endl;

vec.reserve(9);

cout << "[after first reserve] ";
cout << "size : " << vec.size() << ", ";
cout << "capacity : " << vec.capacity() << endl;

vec.reserve(13);
cout << "[after second reserve] ";
cout << "size : " << vec.size() << ", ";
cout << "capacity : " << vec.capacity() << endl;


===== console =====
[initial status] size : 5, capacity : 5
[after resize] size : 7, capacity : 10
[after first reserve] size : 7, capacity : 10
[after second reserve] size : 7, capacity : 13
```

###### 🔽 max_size는 벡터 원소의 자료형에 의존한다.
- 같은 크기의 자료형을 담는 벡터는 max_size()값이 같다.
- 크기가 작은 자료형을 담는 벡터일수록 더 많은 원소를 가질 수 있다.

```cpp
vector <char> vec1; // 1byte
vector <int> vec2; // 4bytes
vector <float> vec3; //4bytes
vector <double> vec4; // 8bytes

cout << vec1.max_size() << endl;
cout << vec2.max_size() << endl;
cout << vec3.max_size() << endl;
cout << vec4.max_size() << endl;

===== console =====
18446744073709551615
4611686018427387903
4611686018427387903
2305843009213693951
```


## 원소 접근(Element Access)
- reference_opertor [g] :
- at(g) :
- front() :
- back() :
- data() :

## 변경자(Modifier)
- assign() : 
- push_back() :
- pop_back() :
- insert() :
- erase() :
- swap () :
- clear() :
- emplace() :
- emplace_back() :

