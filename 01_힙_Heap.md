# 힙 (Heap)

STL의 힙 관련 함수들의 종류와 사용법에 관한 내용을 담고 있습니다.

\<algorithm> 헤더파일을 포함해야 합니다.

<br>

## std::make_heap

시작과 끝을 가리키는 interator를 인자로 받습니다. default로 최대 힙으로 만듭니다.

``` c++
#include <altorithm>
#include <vector>

using namespace std;

void main() {
    vector<int> v { 10, 20, 9, 3, 40, 50 };
    
    make_heap(v.begin(), v.end());	// 최대 힙으로 변환합니다.
    
    cout << v.front() << endl;	// output: 50
}
```

<br>

최소 힙을 만드는 등 정렬의 기준을 추가할 수 있습니다.

```c++
#include <altorithm>
#include <vector>

using namespace std;

void main() {
    vector<int> v { 10, 20, 9, 3, 40, 50 };
    
    make_heap(v.begin(), v.end(), greater<int>());	// 최소 힙으로 변환합니다.
    
    cout << v.front() << endl;	// output: 3
}
```

<br>

## std::push_heap

힙 구조를 가진 객체에 새로운 원소가 삽입되었을 경우, 해당 객체를 힙 구조에 맞게 재정렬합니다.

``` c++
#include <algorithm>
#include <vector>

using namespace std;

void main() {
    vector<int> v { 10, 20, 9, 3, 40, 50 };
    
    make_heap(v.begin(), v.end());	// 최대 힙으로 변환합니다.
    
    v.push_back(60);
    push_heap(v.begin(), v.end());	// 힙 구조에 맞게 재정렬합니다.
    
    cout << v.front() << endl;	// output: 60
}
```

<br>

만약 힙이 사용자가 정의한 정렬기준을 따르고 있다면, push_heap 함수를 호출 시 마지막 인자에 정렬기준 함수를 추가하면 됩니다.

> push_heap(v.begin(), v.end(), greater\<int>());

<br>

## std::pop_heap

힙 구조를 가진 객체에서 목적에 맞는 원소(default=최대 값을 같는 원소)를 제거하기 위해, 해당 원소를 객체의 마지막에 위치시킵니다. 
객체는 힙 구조를 유지합니다.

``` c++
#include <algorithm>
#include <vector>

using namespace std;

void main() {
    vector<int> v { 10, 20, 9, 3, 40, 50 };
    
    make_heap(v.begin(), v.end());	// 최대 힙으로 변환합니다.
    
    pop_heap(v.begin(), v.end());
    
    for (auto e : v)
        cout << e << " ";	// output: 40 20 10 3 9 50
    
    v.pop_back();
}
```

* 결과적으로 힙에서 최대 값을 제거합니다.

<br>

만약 힙이 사용자가 정의한 정렬기준을 따르고 있다면, pop_heap 함수를 호출 시 마지막 인자에 정렬기준 함수를 추가하면 됩니다.

> pop_heap(v.begin(), v.end(), greater\<int>());

<br>

## std:sort_heap

힙을 정렬합니다. 호출한 뒤에는 객체는 힙 구조를 유지하지 않습니다.

``` c++
#include <algorithm>
#include <vector>

using namespace std;

void main() {
    vector<int> v { 10, 20, 9, 3, 40, 50 };
    
    make_heap(v.begin(), v.end());	// 최대 힙으로 변환합니다.
    
    for (auto e : v)
        cout << e << " ";	// output: 50 40 10 3 20 9
    
    sort_heap(v.begin(), v.end());
    
    for (auto e : v)
        cout << e << " ";	// output: 3 9 10 20 40 50
}
```

<br>

## std:is_heap

인자로 받은 객체가 힙 구조를 가지고 있는지 확인합니다. 힙의 목적인 원소(최대 or 최소 or ...)가 가장 앞에 있는지를 참고해 판단합니다.

``` c++
#include <algorithm>
#include <vector>

using namespace std;

void main() {
    vector<int> v { 10, 20, 9, 3, 40, 50 };		// 최대 값이 맨 뒤
    vector<int> u { 50, 10, 40, 9, 3, 20 };		// 최대 값이 맨 앞
    
    cout << is_heap(v.begin(), v.end()) << endl;	// output: 0
    cout << is_heap(u.begin(), u.end()) << endl;	// output: 1
}
```

