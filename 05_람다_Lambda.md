# 람다 (Lambda)

람다란 이름이 없는 함수를 의미합니다.

다음과 같은 형태를 가집니다.

> [캡쳐] (매개변수) -> 반환타입 {코드;} (인자);

1. 캡쳐	
   * [=] - 복사 캡쳐
     * 모든 변수나 상수를 복사로 캡쳐
     * 전역 범위까지 가능
   * [&] - 참조 캡쳐
     * 모든 변수나 상수를 참조로 캡쳐
     * 전역 범위까지 가능
   * [this] - 현재 객체 캡쳐
     * 클래스안에서 정의되는 람다는 현재 객체를 참조로 캡쳐할 수 있음
   * [] - 캡쳐하지 않음
2. 매개 변수
   * 일반 함수의 매개변수와 동일
3. 반환 타입
   * 일반 함수의 반환 타입과 동일
4. 코드
   * 실행할 코드
5. 인자
   * 실제로 사용할 때 전할하는 인자

<br>

## 사용법

* 매개변수가 없을 경우
  * \[]() {코드};
  * [] {코드};
* 매개변수가 있을 경우
  * \[](매개변수) {코드};
* 매개변수가 있고 리턴 값이 있을 경우
  * \[] (매개변수) -> 리턴 타입 {코드};
* 즉시 사용
  * \[] (매개변수) -> 리턴 타입 {코드}();

<br>

## Example

```c++
#include <iostream>
#include <functional>

using namespace std;

void MyNameIs(function<string()> name) {
    cout << "My Name Is " << name();
}

int main() {
    function<string()> name = []() {
        return "Choi Heon";
    }
    
    MyNameIs(name);
    
    return 0;
}
```

````
// expected output
My Name Is Choi Heon
````

<br>

다음은 람다를 반환하는 함수 구현입니다.

```c++
#include <iostream>
#include <function>

using namespace std;

function<void()> GetLambdaFunc(int c) {
    switch(c) {
        case 1:
            return []() {
                cout << "1" << endl;
            }
            break;
        case 2:
            return []() {
                cout << "2" << endl;
            }
            break;
    }
}

int main() {
    function<void()> getlambda;
    
    getlambda = GetLambdaFunc(1);
    getlambda();
    
    getlambda = getLambdaFunc(2);
    getlambda();
}
```

```
// expected output
1
2
```

<br>

algorithm 라이브러리의 for_each의 활용입니다.

```c++
int total_elements = 1;
for_each(v.begin(), v.end(), [&total_elements](int i) { total_elements *= i; })
```

<br>

다음은 같은 기능을 펑터와 람다로 구현한 코드입니다.

```c++
struct mod {
    int modulus;
    mod(int n) : modulus(n) {}
    int operator() (int v) { return v % modulus; }
};

int my_mod = 8;
transform(v.begin(), v.end(), u.begin(), mod(my_mod));
```

```c++
int my_mod = 8;
transform(v.begin(), v.end(), u.begin(), [my_mod](int v) -> int { return v % my_mod; });
```



<br>

