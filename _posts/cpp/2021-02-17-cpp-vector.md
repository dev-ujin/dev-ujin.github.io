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

> π§μμ±μ€π§

# πλ²‘ν°λ?
- **λμ μΈ λ°°μ΄** : μμμ μΆκ°μ μ­μ κ° μΌμ΄λλ©΄ μλμ μΌλ‘ μ¬λ°°μ΄ν΄μ€λ€. 
- **μμ°¨ μ»¨νμ΄λ(sequence contatiner)** : μλ£λ₯Ό μμλλ‘ μ μ₯νλ κ΅¬μ‘°μ΄λ€.

# πν€λνμΌ
```cpp
#include <vector>
```

# πμμ±κ³Ό μ΄κΈ°ν
- λ²‘ν°λ λμ μ΄κΈ° λλ¬Έμ μμ±μμ ν¬κΈ°λ₯Ό λͺμνμ§ μμλ λλ€.

```cpp
// λΉμ΄μλ λ²‘ν° vec μμ±
vector <int> vec;

// 0μΌλ‘ μ΄κΈ°ν λ λ²‘ν° vec μμ±
vector <int> vec(3); // {0, 0, 0}

// 1, 2, 3μ μμλ‘ κ°μ§λ λ²‘ν° vec μμ±
vector <int> vec = {1, 2, 3};
vector <int> vec{1, 2, 3};
```

# πλ©€λ²ν¨μ
## [1] λ°λ³΅μ(Iterator) κ΄λ ¨ ν¨μ
- `begin()` : μ²« λ²μ§Έ μμλ₯Ό κ°λ¦¬ν€λ λ°λ³΅μ
- `end()` : μ΄λ‘ μ μΌλ‘ λ§μ§λ§ μμμ λ€μμ κ°λ¦¬ν€λ λ°λ³΅μ
- `rbegin()` : μ΄λ‘ μ μΌλ‘ λ§μ§λ§ μμμ λ€μμ κ°λ¦¬ν€λ λ°λ³΅μ (reverse beginning)
- `rend()` : μ²« λ²μ§Έ μμλ₯Ό κ°λ¦¬ν€λ λ°λ³΅μ (reverse end)
- `cbegin()` : μ²« λ²μ§Έ μμλ₯Ό κ°λ¦¬ν€λ μμ λ°λ³΅μ (constant begin)
- `cend()` : μ΄λ‘ μ μΌλ‘ λ§μ§λ§ μμμ λ€μμ κ°λ¦¬ν€λ μμ λ°λ³΅μ (constant end)
- `crbegin()` : μ΄λ‘ μ μΌλ‘ λ§μ§λ§ μμμ λ€μμ κ°λ¦¬ν€λ λ°λ³΅μ (contant reverse begin)
- `crend()` : μ²« λ²μ§Έ μμλ₯Ό κ°λ¦¬ν€λ λ°λ³΅μ (constant reverse end)
 
###### π½ begin()κ³Ό end()λ λ²‘ν°λ₯Ό μ λ°©ν₯μΌλ‘ μνν  λ μ¬μ©νλ€.
```cpp
vecter <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.begin() ; itr != vec.end() ; ++itr) {
    cout << *itr << " ";
}

===== console ===== 
1 2 3 4 5
```

###### π½ r(reverse)μ λ²‘ν°λ₯Ό μ­λ°©ν₯μΌλ‘ μνν  λ μ¬μ©νλ€.
```cpp
vecter <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.rbegin() ; itr != vec.rend() ; ++itr) {
    cout << *itr << " ";
}

===== console =====
5 4 3 2 1
```

###### π½ c(constant)λ λ°λ³΅μκ° κ°λ¦¬ν€λ κ°μ λ³κ²½ν  μ μλ€.
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
// μλ¬
vector <int> vec = {1, 2, 3, 4, 5};

for (auto itr = vec.cbegin() ; itr != vec.cend() ; ++itr) {
    *itr = *itr + 10;
    cout << *itr << " ";
}
```

### πββοΈ μ§λ¬Έ 1 : **r(reverse)**μ΄ μ νμν κΉ?
κ·Έλ₯ κ°λ¨νκ² μμλ§ λ°κΏμ end()μ λ¨Όμ  μ°κ³  begin()μ λμ€μ μ°λ©΄ λλ κ±° μλκ°? rbegin(), rend()λ μ νμνμ§? μ½λμ λ³΄κΈ° μμλΌκ³  κ·Έλ°κ±΄κ°? λΌλ μκ°μ νμλ€. μ½λλ₯Ό λλ €λ³Έ κ²°κ³Ό **λ°λ³΅λ¬Έμμ λ°λ³΅μλ end()λ‘ μμν  μ μλ€.**
```cpp
// μλ¬
for (auto itr = vec.end() ; itr != vec.begin() ; ++itr) {
    ...
}
```

## [2] ν¬κΈ°/μ©λ(Size/Capacity) κ΄λ ¨ ν¨μ

- `size()` : λ²‘ν° μμμ κ°―μ
- `capacity()` : λ©λͺ¨λ¦¬μ ν λΉλ μ©λμ μμμ κ°―μλ‘ νν
- `max_size()` : λ²‘ν°κ° μ΅λλ‘ κ°μ§ μ μλ μμμ κ°―μ
- `resize(n)` : λ²‘ν°μ ν¬κΈ°λ₯Ό nμΌλ‘ μ¬μ€μ 
- `reserve(n)` : λ²‘ν°κ° nκ°μ μμλ₯Ό λ΄μ μ μλλ‘ capacityλ₯Ό μ‘°μ 
- `empty()` : λ²‘ν°κ° λΉμ΄μλμ§ κ²μ¬
- `shrink_to_fit()` : capacityλ₯Ό sizeμ λ§μΆμ΄ μΆμ

### size()μ capacity()
- sizeμ capacity λͺ¨λ κ°λ³μ μΈ μμμ΄λ€.
- capacityλ ν­μ sizeμ κ°κ±°λ ν¬λ€.
- capacityλ sizeκ° μ¦κ°ν  λ κ°μ΄ μ¦κ°νμ§λ§, sizeκ° κ°μνλ€κ³  ν΄μ κ°μ΄ κ°μνμ§λ μλλ€.

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
- max_sizeλ λ²‘ν° μμμ μλ£νμ ν¬κΈ°μ λ°λΉλ‘νλ€.
- κ°μ ν¬κΈ°μ μλ£νμ λ΄λ λ²‘ν°λ max_sizeκ°μ΄ κ°λ€.

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

### resize(n)μ reserve(n)
- resizeλ λ²‘ν°μ sizeλ₯Ό ν­μ nμΌλ‘ λ°κΎΌλ€.
- reserveλ λ²‘ν°μ capacityκ° nλ³΄λ€ μμ κ²½μ°μλ§ nμΌλ‘ λ°κΏ nλ§νΌμ ν¬κΈ°λ₯Ό νλ³΄νλ€.
- resizeλ μλ‘μ΄ κ³΅κ°μ λν΄ μ΄κΈ°νλ₯Ό νμ§λ§, reserveλ μ΄κΈ°ννμ§ μλλ€.

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

## [3] μμ μ κ·Ό(Element Access)
- `reference opertor [i]` : λ²‘ν°μμ iμ μλ μμλ₯Ό λ°ν
- `at(i)` : λ²‘ν°μμ iλ²μ§Έμ μλ μμλ₯Ό λ°ν
- `front()` : λ²‘ν°μ μ²« λ²μ§Έ μμλ₯Ό λ°ν
- `back()` : λ²‘ν°μ λ§μ§λ§ μμλ₯Ό λ°ν
- `data()` : μ²« λ²μ§Έ μμμ λν ν¬μΈν°λ₯Ό λ°ν

### [i]μ at(i)
- reference operator [i]λ κ²½κ³ κ²μ¬(bound checking)λ₯Ό νμ§ μλ λ°λ©΄, at(i)λ κ²½κ³ κ²μ¬λ₯Ό νλ€.

```cpp
vector <int> vec = {1, 2, 3, 4, 5};

cout << vec[7];

===== console =====
0
```

```cpp
// μλ¬
vector <int> vec = {1, 2, 3, 4, 5};

cout << vec.at(7);
```

### front()μ back()
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

## [4] λ³κ²½μ(Modifier)
- `assign(n, e)` : λ²‘ν°μ μμ eλ₯Ό nκ° ν λΉνλ€. 
- `push_back(e)` : μμ eλ₯Ό λ²‘ν° λ§¨ λ€μ λ£λλ€.
- `pop_back()` : λ²‘ν° λ§¨ λ€μ μλ μμλ₯Ό μ κ±°νλ€.
- `insert(i, e)` : iλ²μ§Έ μλ¦¬μ eλ₯Ό λ£λλ€. 
- `erase(i)` : iλ²μ§Έμ μλ μμλ₯Ό μ κ±°νλ€.
- `erase(start, end)` : startλ²μ§ΈλΆν° endλ²μ§Έ μ¬μ΄μ μμλ₯Ό μ κ±°νλ€.(**endλ²μ§Έ μμλ λ―Έν¬ν¨**)
- `clear()` : λ²‘ν°μ μλ λͺ¨λ  μμλ₯Ό μ κ±°νλ€.
- `swap(vector)` : νμμ΄ κ°μ λ κ°μ λ²‘ν°λ₯Ό κ΅ννλ€.
- `emplace(i, e)` : iλ²μ§Έ μλ¦¬μ eλ₯Ό λ£κ³  ν΄λΉ μμμ λ°λ³΅μλ₯Ό λ°ννλ€. 
- `emplace_back(e)` : λ²‘ν° λ§¨ λ€μ eλ₯Ό λ£λλ€.

### assign(n, e)
### push_back(e)κ³Ό pop_back()
### push_back(e)κ³Ό emplace_back(e) λΉκ΅
### insert(i, e)μ emplace(i, e)
### erase(i) / erase(start, end)
### clear()
### swap(vector)


