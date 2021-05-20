# 튜플

2개 이상의 값을 하나의 객체로 묶을 수 있습니다.

<br>

## 사용 방법

* 헤더 선언

  > *#include \<tuple>*

* 생성 방법

  > *std::tuple<타입1, 타입2, ... , 타입k> 변수명 = make_tuple(값1, 값2, ... , 값k)*

* 접근 방법

  > *std::get<번호>(튜플변수명)*

* 교환

  > *std::swap(튜플1, 튜플2)*

  * 사용하기 위해선 두 튜플내 값들의 개수와 타입 순서가 같아야 합니다.

* 대입

  > *std::tie(변수1, 변수2, ... , 변수k) = 튜플*

  * 변수들에 튜플이 가진 값들을 대입합니다.
  * 변수들과 튜플의 값들의 개수과 타입 순서가 같아야 합니다.

* 연산자 =

  > 튜플1 = 튜플2

  * 튜플2의 값들을 튜플1에 복사합니다.
  * 값들의 개수과 타입의 순서가 같아야 합니다.

  

<br>

## Example

```c++
#include <iostream>
#include <string>
#include <tuple>

using namespace std;

tuple<int, string> getAgeNName() {
   	int age;
    string name;
    
    cout << "나이: ";
    cin >> age;
    
    cout << "이름: ";
    cin >> name;
    
    return make_tuple(age, name);
}

int main() {
    tuple<int, string> personInfo;
    personInfo = getAgeNName();
    
    cout << "나이: " << get<0>(personInfo) << endl;
    cout << "이름: " << get<1>(personInfo) << endl;
    
    return 0;
}
```

```
// input
나이: 12
이름: Hong

// output
나이: 12
이름: Hong
```

