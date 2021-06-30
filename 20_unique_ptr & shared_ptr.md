# unique_ptr & shared_ptr

디자인 패턴 RAII은 자원의 획득은 초기화를 의미합니다. 그리고 이에 착안해서 가리키는 객체의 메모리를 효율적으로 관리해주는 스마트 포인터들이 존재합니다.

<br>

## unique_ptr

메모리를 해제하면 효율적으로 메모리를 사용할 수 있지만, 이미 해제된 메모리를 다시 참조하는 경우가 발생해 오류로 인해 프로그램이 종료될 수 있습니다. 

```c++
Data* data = new Data();
Data* data2 = data;

delete data;
delete data2;
```

* data2를 해제하는 과정에서 double free 버그가 발생합니다.

<br>

이러한 경우는 객체의 소유권이 명확하지 않아서 발생하는 문제이며, unique_ptr을 사용하면 해결할 수 있습니다.

```c++
#include <iostream>
#include <memory>

class A {
  int *data;

 public:
  A() {
    std::cout << "자원을 획득함!" << std::endl;
    data = new int[100];
  }

  void some() { std::cout << "일반 포인터와 동일하게 사용가능!" << std::endl; }

  ~A() {
    std::cout << "자원을 해제함!" << std::endl;
    delete[] data;
  }
};

void do_something() {
  std::unique_ptr<A> pa(new A());
  pa->some();
}

int main() { do_something(); }
```

```
// output
자원을 획득함!
일반 포인터와 동일하게 사용가능!
자원을 해제함!
```

* *std::unique_ptr<A> pa(new A());*

  * 이는 A* pa = new A();와 동일한 효과를 가집니다.
  * unique_ptr이 해제될 때 , 자동으로 가리키는 객체의 소멸자를 호출합니다.
  * 다음과 같이 unique_ptr 객체를 가리키려하면 컴파일 에러가 발생합니다.

  ```c++
  std::unique_ptr<A> pa(new A());
  std::unique_ptr<A> pb = pa;  // 컴파일 에러 발생
  ```

  * 하지만 복사가 아닌 소유권의 이동은 가능합니다.

  ```c++
  std::unique_ptr<A> pa(new A());
  std::unique_ptr<A> pb = std::move(pa); // 따로 생성자가 호출되진 않음
  ```

  * get 함수를 통해 주소를 확인할 수 있습니다.

  ```c++
  pa.get();
  ```

<br>

unique_ptr는 함수의 인자로도 전달할 수 있지만, 소유권을 가진 객체가 더 늘어날 수 있으므로 unique_ptr의 원칙에 위배됩니다. 따라서 함수의 인자로 전달하려면 get 함수를 통해서 주소를 전달하면 됩니다.

```c++
int main() {
	// std::unique_ptr<A> pa(new A());
    auto pa = std::make_unique<A>();  // 위와 동일한 코드입니다.
	func(pa.get());
}
```

<br>

추가로 컨테이너 클래스의 원소로 사용하기 위해선, 원소로 넣을 때 move 함수를 이용해야 합니다.

```c++
int main() {
    std::vector<std::unique_ptr<A>> vec;
    std::unique_ptr<A> pa(new A(1));

	// vec.push_back(pa); --> 컴파일 에러 발생
    vec.push_back(std::move(pa));
}
```

<br>

## shared_ptr

유일하게 객체를 가리키는 unique_ptr과는 다르게, 여러 shared_ptr는 하나의 객체를 가리킬 수 있습니다. 해당 객체를 가리키는 shared_ptr의 개수가 0개일 경우, 소멸자를 호출합니다.

```c++
std::shared_ptr<A> p1(new A());
std::shared_ptr<A> p2 = p1;
auto p3 = std::make_shared<A>(p1);

std::cout << p1.use_count();  // 해당 객체를 참조하고 있는 shared_ptr의 개수를 출력합니다.
std::cout << p2.use_count();  // 3
```



