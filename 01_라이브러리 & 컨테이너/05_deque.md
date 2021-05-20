# deque 

#include \<deque>를 선언함으로서 사용할 수 있습니다.

deque는 double ended queue로 양방향에서 삭제와 삽입을 할 수 있습니다.

벡터(vector)에서 제공하는 대부분의 기능을 제공하지만 모든 원소가 메모리상으로 연속적임을 보장할 수 없습니다. 즉, 포인터 연산을 통한 원소의 접근의 안전성을 보장할 수 없습니다.

벡터는 할당받은 메모리가 꽉차면 새로 할당받는 방식이지만, 데크는 메모리 상에 분산하여 데이터를 저장하므로 더 효율적입니다. 떄문에 벡터와 다르게 capacity와 reserve 함수가 없습니다.

중간 위치에 삽입 및 삭제가 빈번하다면 list의 사용을 고려해야 합니다.

<br>

* **operator =**
  * 데크의 내용을 복사합니다.

<br>

* 다음은 **vector와 동일하게** 사용되는 함수입니다.
  * size
  * resize
  * empty
  * operator []
  * at
  * front
  * back
  * assign
  * push_back
  * pop_back
  * insert
  * erase
  * swap
  * clear

<br>

* **push_front(값) / pop_front()**
  * 데크의 앞에 값을 추가하거나 삭제합니다.