# range-based for loop

* 일반적인 for  반복문보다 가독성을 높일 수 있음
* 컨테이너 같은 자료구조 내 모든 요소를 안전하게 접근할 수 있음



### 사용 방법

```c++
attr(optional) for (init_statement(optional) range_declaration : range_expression)
    loop_statement
```

* attr - [attribute](https://en.cppreference.com/w/cpp/language/attributes)
* init_statement - 해당 for문에서 사용할 변수를 선언 또는 초기화, C++20부터 가능
* range_declaration - 자료구조 내의 요소와 같은 타입의 변수를 선언, 일반적으로 `auto` 타입을 사용
* range_expression - suitable sequence (배열 또는 `begin()`과 `end()`가 정의된 객체)



### 내부 구현

* 다음은 C++20부터 사용된 구현 내용

  ```c++
  //init-statement
  
  auto && __range = range_expression;
  auto __begin = begin_expr;
  auto __end = end_expr;
  
  for ( ; __begin != __end; ++__begin) {
  	range_declaration = *__begin;
      
      //loop_statement
  }
  ```



### Example

```c++
#include <iostream>
#include <vector>
 
int main() {
    std::vector<int> v = {0, 1, 2, 3, 4, 5};
 
    for (const int& i : v) // access by const reference
        std::cout << i << ' ';
    std::cout << '\n';
 
    for (auto i : v) // access by value, the type of i is int
        std::cout << i << ' ';
    std::cout << '\n';
 
    for (auto&& i : v) // access by universal reference, the type of i is int&
        std::cout << i << ' ';
    std::cout << '\n';
 
    const auto& cv = v;
 
    for (auto&& i : cv) // access by f-d reference, the type of i is const int&
        std::cout << i << ' ';
    std::cout << '\n';
 
    for (int n : {0, 1, 2, 3, 4, 5}) // the initializer may be a braced-init-list
        std::cout << n << ' ';
    std::cout << '\n';
 
    int a[] = {0, 1, 2, 3, 4, 5};
    for (int n : a) // the initializer may be an array
        std::cout << n << ' ';
    std::cout << '\n';
 
    for ([[maybe_unused]] int n : a)  
        std::cout << 1 << ' '; // the loop variable need not be used
    std::cout << '\n';
 
    for (auto n = v.size(); auto i : v) // the init-statement (C++20)
        std::cout << --n + i << ' ';
    std::cout << '\n';
 
}
```

```
// output
0 1 2 3 4 5 
0 1 2 3 4 5 
0 1 2 3 4 5 
0 1 2 3 4 5 
0 1 2 3 4 5 
0 1 2 3 4 5 
1 1 1 1 1 1 
5 5 5 5 5 5
```

