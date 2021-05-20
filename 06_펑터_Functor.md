# 펑터 (Functor)

펑터는 함수처럼 ()과 함께 사용할 수 있는 객체입니다.

대표적으로 \<algorithm> 라이브러리의 sort 함수는 `조건`을 지정할 수 있습니다. 이런 `조건`을 펑터로 삽입할 수 있습니다.

<br>
다음은 펑터를 사용하지 않는 경우입니다.

```c++
#include <iostream>
#include <algorithm>

bool compare(int n1, int n2) {
    return n1 < n2;
}

int main(void) {
    int arr[] = {5, 3, 2, 1, 7, 8}
    
    std::sort(arr, arr+6, compare);
}
```

<br>

다음은 클래스 멤버를 사용해 조건을 전달하는 경우입니다.

```c++
#include <iostream>
#include <list>

template <class T>
class Compare {
    
private:
	T _Boundary;
    
public:
    Compare(const T& N) : _Boundary(N) {}
    bool operator() (const T& N) {
        return N >= _Boundary
    }
}

int main(void) {
    std::list<int> list;
    
    // 생략 (10, 100, 5, 4, 70, 20 삽입)
    
    list.remove_if(Compare<int>(10));
    
    for (auto i : list)
        std::cout << i << std:;endl;
}
```

```
// expected output
5
4
```

<br>

STL에는 몇 가지 미리 정의된 펑터들이 있습니다. 정확히는 \<funtional> 헤더에 존재합니다.

```c++
#include <iostream>
#include <vector>
#include <functional>
#include <algorithm>

using namespace std;

int main() {
    vector<int> v;
    // 100 1000 1020 500 삽입
    
    sort(v.begin(), v.end(), greater<int>());
    for (auto i : v)
        cout << i << endl;
}
```

```
// expected output
100
1000
1020
500
```



