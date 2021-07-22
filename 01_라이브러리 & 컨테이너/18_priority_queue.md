# priority_queue

* 우선순위 큐
* `#include <queue>`를 선언해서 사용 가능

<br>

#### 생성자

* `priority_queue<T, Container, Compare>` : 원하는 자료형과 컨테이너, 비교 함수를 넣습니다.
  * 비교 함수는 `less<T>`또는 `greater<T>`를 사용하거나 별도로 `struct`를 정의한 뒤, 비교 함수를 구현해야 합니다. (람다 함수는 힘듧)
  * 비교 함수에서 false를 반환하면 왼쪽, true를 반환하면 오른쪽의 인자의 우선순위가 더 높습니다.

<br>

#### 삽입 및 삭제

* push(element): 원소를 삽입합니다.
* pop(): top의 원소를제거합니다.

<br>

#### 조회

* top()

<br>

#### 기타

* empty()
* size()

<br>

### Example

**[최대 힙 구현 1]**

```c++
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

template <class T>
struct Compare {
	bool operator() (const T& a, const T& b) const {
		return a < b;
	}
};

int main() {
	priority_queue<int, vector<int>, Compare<int>> queue;

	queue.push(3);
	queue.push(4);
	queue.push(1);
	queue.push(100);

	while (queue.size() > 0) {
		cout << queue.top() << endl;
		queue.pop();
	}
	
	return 0;
}
```

<br>

**[최대 힙 구현 2]**

```c++
#include <iostream>
#include <vector>
#include <queue>

using namespace std;


int main() {
	priority_queue<int, vector<int>, less<int>> queue;

	queue.push(3);
	queue.push(4);
	queue.push(1);
	queue.push(100);

	while (queue.size() > 0) {
		cout << queue.top() << endl;
		queue.pop();
	}
	
	return 0;
}
```

<br>