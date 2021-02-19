---
layout: post
title: "[C++] STL::Vector"
date: 2021-02-17 22:07:00 0800
categories: cpp
tags: cpp
comments: 1
changefreq: daily
priority: 1
---

> 🚧작성중🚧

# 🏁벡터란?
- **동적인 배열** : 원소의 추가와 삭제가 일어나면 자동적으로 재배열해준다. 
- **순차 컨테이너(sequence contatiner)** : 자료를 순서대로 저장하는 구조이다.

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
- `end()` : 이론적으로 마지막 원소의 다음을 가리키는 반복자
- `rbegin()` : 이론적으로 마지막 원소의 다음을 가리키는 반복자 (reverse beginning)
- `rend()` : 첫 번째 원소를 가리키는 반복자 (reverse end)
- `cbegin()` : 첫 번째 원소를 가리키는 상수 반복자 (constant begin)
- `cend()` : 이론적으로 마지막 원소의 다음을 가리키는 상수 반복자 (constant end)
- `crbegin()` : 이론적으로 마지막 원소의 다음을 가리키는 반복자 (contant reverse begin)
- `crend()` : 첫 번째 원소를 가리키는 반복자 (constant reverse end)
 
###### 🔽 begin()과 end()는 벡터를 정방향으로 순회할 때 사용한다.
```cpp
vecter <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.begin() ; itr != vec.end() ; ++itr) {
    cout << *itr << " ";
}

===== console ===== 
1 2 3 4 5
```

###### 🔽 r(reverse)은 벡터를 역방향으로 순회할 때 사용한다.
```cpp
vecter <int> vec = {1, 2, 3, 4, 5};

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

- `size()` : 벡터 원소의 갯수
- `capacity()` : 메모리에 할당된 용량을 원소의 갯수로 표현
- `max_size()` : 벡터가 최대로 가질 수 있는 원소의 갯수
- `resize(n)` : 벡터의 크기를 n으로 재설정
- `reserve(n)` : 벡터가 n개의 요소를 담을 수 있도록 capacity를 조정
- `empty()` : 벡터가 비어있는지 검사
- `shrink_to_fit()` : capacity를 size에 맞추어 축소

### size()와 capacity()
- size와 capacity 모두 가변적인 요소이다.
- capacity는 항상 size와 같거나 크다.
- capacity는 size가 증가할 때 같이 증가하지만, size가 감소한다고 해서 같이 감소하지는 않는다.

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

### max_size()
- max_size는 벡터 원소의 자료형의 크기에 반비례한다.
- 같은 크기의 자료형을 담는 벡터는 max_size값이 같다.

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

### resize(n)와 reserve(n)
- resize는 벡터의 size를 항상 n으로 바꾼다.
- reserve는 벡터의 capacity가 n보다 작은 경우에만 n으로 바꿔 n만큼의 크기를 확보한다.
- resize는 새로운 공간에 대해 초기화를 하지만, reserve는 초기화하지 않는다.

```cpp
vector <int> vec = {1, 2, 3, 4, 5};

cout << "[initial status] ";
cout << "size : " << vec.size();
cout << ", capacity : " << vec.capacity() << endl;

vec.resize(7);
cout << "[after resize] ";
cout << "size : " << vec.size();
cout << ", capacity : " << vec.capacity() << endl;

vec.reserve(9);
cout << "[after first reserve] ";
cout << "size : " << vec.size();
cout << ", capacity : " << vec.capacity() << endl;

vec.reserve(13);
cout << "[after second reserve] ";
cout << "size : " << vec.size();
cout << ", capacity : " << vec.capacity() << endl;


===== console =====
[initial status] size : 5, capacity : 5
[after resize] size : 7, capacity : 10
[after first reserve] size : 7, capacity : 10
[after second reserve] size : 7, capacity : 13
```
### empty()
```cpp
vector <int> vec1;
vector <int> vec2(5); // {0, 0, 0, 0, 0}

cout << "vec1 is empty : " << vec1.empty() << endl;
cout << "vec2 is empty : " << vec2.empty() << endl;

===== console =====
vec1 is empty : 1
vec2 is empty : 0
```

### shrink_to_fit()
```cpp
vector <int> vec;

vec.push_back(1);
vec.push_back(2);
vec.push_back(3);
vec.push_back(4);
vec.push_back(5);

cout << "[initial status] ";
cout << "size : " << vec.size();
cout << ", capacity : " << vec.capacity() << endl;

vec.shrink_to_fit();
cout << "[after shrink_to_fit] ";
cout << "size : " << vec.size();
cout << ", capacity : " << vec.capacity() << endl;


===== console =====
[initial status] size : 5, capacity : 8
[after shrink_to_fit] size : 5, capacity : 5
```

## [3] 원소 접근(Element Access)
- `reference opertor [i]` : 벡터에서 i에 있는 원소를 반환
- `at(i)` : 벡터에서 i번째에 있는 원소를 반환
- `front()` : 벡터의 첫 번째 원소를 반환
- `back()` : 벡터의 마지막 원소를 반환
- `data()` : 첫 번째 원소에 대한 포인터를 반환

### [i]와 at(i)
- reference operator [i]는 경계 검사(bound checking)를 하지 않는 반면, at(i)는 경계 검사를 한다.

```cpp
vector <int> vec = {1, 2, 3, 4, 5};

cout << vec[7];

===== console =====
0
```

```cpp
// 에러
vector <int> vec = {1, 2, 3, 4, 5};

cout << vec.at(7);
```

### front()와 back()
```cpp
vector <int> vec;

vec.push_back(1);
vec.push_back(2);
vec.push_back(3);

cout << "front : " << vec.front() << ", back : " << vec.back(); 
```
### data()
```cpp
vector<int> vec = {1, 2, 3, 4, 5};

int* pos = vec.data();

for (int i = 0; i < vec.size(); ++i)
    cout << *pos++ << " ";


===== console =====
1 2 3 4 5
```

## [4] 변경자(Modifier)
- `assign(n, e)` : 벡터에 원소 e를 n개 할당한다. 
- `push_back(e)` : 원소 e를 벡터 맨 뒤에 넣는다.
- `pop_back()` : 벡터 맨 뒤에 있는 요소를 제거한다.
- `insert(i, e)` : i번째 자리에 e를 넣는다. 
- `erase(i)` : i번째에 있는 원소를 제거한다.
- `erase(start, end)` : start번째부터 end번째 사이의 원소를 제거한다.(**end번째 원소는 미포함**)
- `clear()` : 벡터에 있는 모든 원소를 제거한다.
- `swap(vector)` : 타입이 같은 두 개의 벡터를 교환한다.
- `emplace(i, e)` : i번째 자리에 e를 넣고 해당 원소의 반복자를 반환한다. 
- `emplace_back(e)` : 벡터 맨 뒤에 e를 넣는다.

### assign(n, e)
### push_back(e)과 pop_back()
### push_back(e)과 emplace_back(e) 비교
### insert(i, e)와 emplace(i, e)
### erase(i) / erase(start, end)
### clear()
### swap(vector)


