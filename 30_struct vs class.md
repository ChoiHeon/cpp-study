# struct vs class

* `struct`와 `class` 모두 멤버 변수와 함수를 선언할 수 있음
* 심지어 `struct`도 **<u>상속</u>**의 사용이 가능함
* 다만 둘 사이에 엄연한 차이점이 존재



### 접근제어 지시자

* 아래의 코드에서 'struct'를 'class'로 변경하면 에러 발생

  ```c++
  struct Point {
      int x, y;
  };
  
  Point p = {1, 2};
  ```

* 이유는 접근제어자(지시자)를 사용하지 않았기 때문

* 접근제어자를 사용하지 않으면 `struct`는 `public`, `class`는 `private`로 자동으로 선언됨

* 또한 접근제어 지시자없이 상속할 경우 `struct`는 `public`으로, `class`는 `private`로 상속됨



### 선택 기준

* 따라서 `struct`와 `class `사이엔 기능적 차이는 없음. 다만 협약(convnetation) 같은 것이  존재
* 일반적으로 `struct`는 여러 객체의 bundle로서 사용
* 이는 `pair` 또는 `tuple`과 유사하지만, 다른 점은 이름을 부여할 수 있다는 점이 특징
* `class`는 어떤 동작(함수)을 할 수 있는지가 중요하며 사용자가 내부에 어떤 데이터가 있는지 알 필요가 없는 것에 사용



### 결론

* `struct`와 `class`는 기능적으로 차이가 없음. 있다면 디폴트 접근제어 지시자가 다르다는 점 정도
* 다만 협약에 의해 `struct`는 bundle로서 여러 객체들을 묶는 용도로 사용되고 
* `class`는 사용자가 내부 데이터에 상관없이 함수를 사용할 때 주로 사용되는 용도

