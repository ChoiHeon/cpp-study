# LValue & RValue

* LValue는 식별자를 가져서 자신의 상태변화를 저장할 수 있는 것
* RValue는 식별자를 가지지 않아 상태변화를 저장할 수 없는 것
* 따라서 LValue는 대입 연산자 = 의 양 쪽에 올 수 있으며 RValue는 오른쪽에만 올 수 있음



### LValue Reference(Ref)

* LValue를 참조하기 위한 타입
* 선언시 LValue로 초기화해야 사용할 수 있음
* LValue Ref는 LValue의 주소값을 가지고 있음



### RValue Reference(Ref)

* RValue를 참조하기 위한 타입
* 자료형 뒤에 `&`를 추가해서 사용 가능
* move semantics와 perfect forwarding의 구현에 사용됨



### Move Semantics

* RValue에 있는 동적 자원을 다른 메모리에 옳기는 행동

* 자료형 뒤에 `&&`를 추가해서 사용 가능

* 기존에 있던 메모리에 자원을 남기지 않기 때문에 단순히 자원을 복사하는 것보다 더 효율적

* 실제 STL의 `vector::push_back()`은 내부에 데이터 생성시 이동이 가능하다면 복사보다는 이동을 사용

  * 이처럼 vector에 이동을 사용하고 싶다면 이동 생성자에 `noexept `키워드를 추가하는 것이 좋음
  * `noexept`를 추가하지 않으면 재할당 과정에서 에러 발생시, 이미 이동되었던 데이터들이 사라져있을 수 있기 때문

* `std::move()` : 매개변수로 넣은 인자를 RValue로 변환해서 반환

* **Example**

  ```c++
  class A {int array};
  
  template <class T>
  void m_swap(T& a, T& b) {
      T c(move(a)); // move constructor
      a = move(b);  // move assignment operator
      b = move(c);  // move assignment operator
  }
  ```

  * move sematic을 이용한 값의 교환



### Perfect Forwarding

* 제네릭을 사용할 경우, 변수의 타입이 const Lvalue, Lvalue&, Rvalue&& 인지 알 수 없는 문제를 해결할 수 있음

* 매개변수의 제네릭타입 뒤에 `&&`를 추가해서 사용 가능

  * LValue와 RValue 타입 둘 다 받을 수 있음 => universal reference

* `std::forward()` : 매개변수로 넣은 인자가 Rvalue Ref라면 move를 적용해 반환

* **Example**

  ```c++
  template <class T>
  void wrapper(T&& t) {
      g(std::forward(t));
  }
  
  void g(const int& a) { cout << "const int&" << endl; }
  void g(int& a) { cout << "int&" << endl; }
  void g(int&& a) { cout << "int&&" << endl; }
  ```

  



