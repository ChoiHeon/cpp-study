# set

연관 컨테이너(associative container) 중 하나로 노드 기반 컨테이너입니다.

균형 이진 트리(Balanced Binary Tree) 로 구현되어 있으며 원소들의 중복을 허용하지 않습니다.

원소들은 자동으로 정렬됩니다. (기본적으로 less, 오름차순입니다.)

<br>

다음과 같이 선언함으로써 사용할 수 있습니다.

```c++
#include <set>
```

<br>

* **생성자**

  * 원소의 타입을 int로 가정했을 경우입니다.

  ```c++
  set<int> s;  // 기본적인 생성자
  set<int> s(pred);  // 정렬 기준을 지정
  set<int, compare> s // 다음과 같이 정렬 기준을 지정 가능
  set<int> s2(s1);  // s1을 복사
  ```

  * 다음은 정렬 조건을 지정하는 예시입니다.

  ```c++
  struct MyOrder {
      bool operator() (const string& left, const string& right) {
          if (left.size() == right.size())
              return left < right;
          else
              return left.size() > right.size();
      }
  }
  
  int main() {
      set<string, MyOrder> s;
     	// 이후 위에 정의된 비교함수에 따라 ㅈ
  }
  ```

  

<br>

* **begin() / end()**
  * 시작 반복자, 끝 반복자를 반환합니다.

<br>

* **rbegin() / rend()**
  * 마지막 반복자, 처음 반복자를 반환합니다.

<br>

* **clear()**
  * 모든 원소를 제거합니다.

<br>

* **count(값)**
  * 값과 일치하는 원소의 개수를 반환합니다.
  * 기본적으로 0 or 1이지만, 원소의 중복을 허용하는  multiset에서 사용됩니다.

<br>

* **empty()**
  * 비었는지 여부를 반환합니다.

<br>

* **insert(값)**
  * 값을 원소로 삽입합니다.
  * pair<interator, bool>을 반환합니다.
    * 각각 삽입한 원소의 위치와 삽입 성공 여부를 의미합니다.
* **insert(삽입 위치, 값)**
  * 삽입할 위치부터 삽입이 가능한 위치를 탐색한 후에 값을 원소로 삽입합니다.

<br>

* **erase(값)**
  * 값과 일치하는 원소를 제거합니다.

* **erase(삭제할 원소의 반복자)**
  * 지정한 원소를 제거합니다.

* **erase(시작 반복자, 끝 반복자)**
  * 범위의 원소를 제거합니다.

<br>

* **find(값)**
  * 값과 일치하는 원소의 반복자를 반환합니다.
  * 없다면 end()를 반환합니다.

<br>

* **upper_bound(값)**
  * 값보다 큰 원소들 중 가장 작은 원소의 반복자를 반환합니다.
* **lower_bound(값)**
  * 값보다 작은 원소들 중 가장 큰 원소의 반복자를 반환합니다.

* **equal_range(값)**
  * pair<iterator, iterator>를 반환합니다.
  * 각 iterator는 upper_bound와 lower_bound의 결과와 같습니다.

<br>

* **key_comp()**
  * 정렬 기준 조건자를 반환합니다.