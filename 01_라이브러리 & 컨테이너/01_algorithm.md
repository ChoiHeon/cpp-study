# algorithm

* **unique(시작 주소, 종료 주소);**

  * 연속된 중복 원소를 객체의 뒤로 보냅니다. 따라서 정렬된 상태의 객체를 대상으로 사용해야 합니다.
  * return: 중복된 원소들의 시작 주소를 반환합니다.
  * 다음과 같은 활용이 가능합니다.

  ```c++
  vector v = {1, 2, 3, 1, 2, 3, 4};
  
  sort(v.begin(), v.end());  // 정렬은 필수
  v.erase(unique(v.begin(), v.end()), v.end);  // 중뵥된 값의 시작 주소를 통해 원소를 제거
  ```

<br>

* **find(시작 주소, 종료 주소, 값)**
  * 시작 주소부터 종료 주소 전까지 값을 탐색합니다.
  * return: 값을 찾았다면 해당 값의 주소를, 없다면 종료 주소를 반환합니다.
  * string 라이브러리의 find()와는 다릅니다.

<br>

* **binary_search(시작 주소, 종료 주소, 값)**
  * 시작 주소부터 종료 주소 전까지 값을 이진탐색으로 탐색합니다.
  * return: 값이 있는지 여부를 true 또는 false를 반환합니다.

<br>

* **min_element(시작 주소, 종료 주소) / max_element(시작 주소, 종료 주소)**
  * return: 가장 작거나 / 큰 값의 주소를 반환합니다.

<br>

* **reverse(시작 주소, 종료 주소)	**
  * 객체를 거꾸로 정렬합니다.
  * 별도로 반환하는 값은 없습니다.

<br>

* **transform(시작 주소, 종료 주소, 시작 주소2, 규칙[함수])**
  * 시작 주소부터 종료 주소까지 원소들을 규칙에 맞게 시작 주소부터 변환시켜 저장하는 함수힙니다.

<br>

* **for_each(시작 주소, 종료 주소, 실행 함수)**

  * 시작 주소부터 종료 주소 전까지 실행함수를 수행합니다.
  * 실행 함수는 인자를 하나만 받는 함수 객체입니다.
  * 다음은 실행 함수의 예시입니다.

  ```c++
  void func(const Type &a);
  ```

<br>

* **prev_permutation(시작 주소, 종료 주소) / next_permutation(시작 주소, 종료 주소)**

  * 이전 / 다음 순열을 구하는 함수입니다.
  * prev_permutation을 사용하기 위해선 greater, next_permutation은 less로 정렬한 후 사용해야 합니다.
  * return: 다음 순열이 있다면 true, 없다면 false를 반환합니다.
  * 다음처럼 응용시 모든 경우의 순열을 구할 수 있습니다.

  ``` c++
  vector<int> v;
  v.sort(v.begin(), v.end());
  
  do {
      
  }while (next_permutation(v.begin(), v.end()));
  ```

  * 외에도 조합(combination)을 구하는 코드에도 사용할 수 있습니다.

  ```c++
  // 5개의 원소 중 3개를 조합하는 방법
  vector<int< v = {1, 2, 3, 4, 5};
  vector<bool> u = {false, false, true, true};
  
  do {
      vector<int> w;
      for (int i = 0; i < 5; i++)
          if (u[i])
              w.pusb_back(v[i]);
      cout << w << end;
  } while (next_permutation(u.begin(), u.end());
  ```

<br>

* **remove(시작 반복자, 마지막 반복자, 값)**

  * 시작 반복자부터 마지막 반복자까지 원소와 값이 일치한다면 해당 원소를 맨 뒤로 이동시킵니다.
  * 이동시킨 원소들의 시작 위치(반복자)를 반환합니다.

* **remove_if(시작 반복자, 마지막 반복자, 조건)**

  * 범위 내에 조건을 만족하는 원소들을 뒤로 보냅니다.
  * 보낸 원소들의 시작 위치(반복자)를 반환합니다.

  ```c++
  #include <algorithm>
  #include <cctype>
  #include <iostream>
  #include <string>
  
  int main() {
      std::string str1 = "Test string";
   	str1.erase(std::remove(str1.begin(), str1.end(), ' '), str1.end());
      cout << str1 << endl;
      
      std::string str2 = "Test \t string with \n\n whitespace";
      str1.erase(std::remove(str1.begin(), str1.end(), [](unsigned char c) { return std::isspace(c); }), str2.end());
      cout << str2 << endl;
  }
  ```
  
  ```
  // expected output
  Teststring
  Teststringwithwhitespace
  ```

<br>

* count(시작 반복자, 마지막 반복자, 값)
  * 범위 내의 값과 일치하는 원소의 개수를 반환합니다.
* count_if(시작 반복자, 마지막 반복자, 조건)
  * 범위 내의 조건과 일치하는 원소의 개수를 반환합니다.