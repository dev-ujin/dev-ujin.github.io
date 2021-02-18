---
layout: post
title: "[C++] STL :: Vector"
date: 2021-02-17 22:07:00 0800
categories: cpp
tags: cpp
comments: 1
changefreq: daily
priority: 1
---
# 헤더파일/선언/초기화/멤버함수

# 🏁벡터란?
**동적인 배열**. 원소의 추가와 삭제가 일어나면 자동적으로 재배열해준다. 

# 🏁헤더파일
```cpp
#include <vector>
```

# 🏁선언과 초기화
- 벡터는 동적이기 때문에 선언부에 크기를 명시하지 않아도 된다.
- 벡터 요소의 초기화 디폴트는 `0`이다.
```cpp
vector <int> vec;
vector <int> vec(3); // {0, 0, 0}
vector <int> vec = {1, 2, 3};
```

# 🏁멤버함수
## 반복자
- `begin()` : 첫 번째 원소를 가리키는 반복자
- `end()` : 마지막 원소를 가리키는 반복자
- `rbegin()` : 마지막 원소를 가리키는 반복자 (reverse beginning)
- `rend()` : 첫 번째 원소를 가리키는 반복자 (reverse end)
- `cbegin()` : 첫 번째 원소를 가리키는 상수 반복자 (constant begin)
- `cend()` : 마지막 원소를 가리키는 상수 반복자 (constant end)
- `crbegin()` : 마지막 원소를 가리키는 반복자 (contant reverse begin)
- `crend()` : 첫 번째 원소를 가리키는 반복자 (constant reverse end)  

> `r(reverse)`는 역방향으로 벡터를 순회하고 싶을 때 사용한다.

```cpp
vecter <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.begin() ; itr != vec.end() ; ++itr) {
    cout << *itr << " ";
}
```
```console
1 2 3 4 5
```
```cpp
vecter <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.rbegin() ; itr != vec.rend() ; ++itr) {
    cout << *itr << " ";
}
```
```console
5 4 3 2 1
```

> `c(constant)`는 반복자가 가리키는 값을 변경할 수 없다.

```cpp
vector <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.begin() ; itr != vec.end() ; ++itr) {
    *itr = *itr + 10;
    cout << *itr << " ";
}
```
```console
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


### 🙋‍♀️ 의문점 1 : **r(reverse)**는 왜 필요하지?
그냥 간단하게 순서만 바꿔서 end()을 먼저 쓰고 begin()을 나중에 쓰면 되는 거 아닌가? rbegin(), rend()는 왜 필요하지? 코드상 보기 예쁘라고 그런건가? 라는 생각을 했었다. 코드를 돌려본 결과 **반복문에서 반복자는 end()로 시작할 수 없다.**
```cpp
// 에러
for (auto itr = vec.end() ; itr != vec.begin() ; ++itr) {
    ...
}
```

## 크기 / 용량

- size() : 벡터 요소의 갯수
- max_size() : 벡터가 최대로 가질 수 있는 요소의 갯수
- capacity() : 

## 의문점
- 크기 동적인데 max size가 어딨어?
- capacity 모야?
- 
```cpp
```
```cpp
```

### 벡터에 원소를 넣는 법
#### 1. 대입 연산자(=)를 이용한다.
v[0] = 100;
####
```cpp
// 1. 대입 연산자(=)를 이용한다.
v[0] = 100;
// 2. at(index) 함수를 이용
```