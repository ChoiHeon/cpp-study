# const의 사용

* `const`는 '불변'이라는 의도를 컴파일러와 프로그래머 둘 모두에게 전달할 수 있다는 장점이 있습니다.



### 포인터 상수

* `const`가 *`의 앞 또는 뒤에 오는 것에 따라 의미가 달라집니다.

```c++
char greeting[] = "Hello!";

// const를 사용하지 않을 경우
char* p = greeting; 
p[1] = 'E';
p = nullptr;

// 포인터 타입에 const를 사용할 경우
const char* p = greeting;
p[2] = 'L';		// OK
p = nullptr; 	// Error

// 가리키는 대상에 const를 사용할 경우
char* const p = greeting;
p[3] = 'L'; 	// Error
p = nullptr;	// OK

// 둘 다 const 사용할 경우
const char* const p = greeting;
p[3] = 'L'; 	// Error
p = nullptr; 	// Error
```

<br>

* `*`의 앞 또는 뒤에 있다면 `const`의 구체적인 위치는 중요하지 않습니다.
* 아래의 두 선언은 받아들이는 매개변수의 차이가 없습니다.

```c++
void f1(const Widget *pw); // 상수 Widget 객체에 대한 포인터만 매개변수로 받습니다.

void f2(Widget const *pw); // f1과 동일합니다.
```

<br>

### const와 iterator

* `iterator`가 가리키는 대상을 변경하지 않도록 하려면 `const`를 추가하면 됩니다.
* `iterator`가 가리키는 대상의 값을 변경하지 않도록 하려면 `const_iterator`를 사용해야 합니다.

```c++
std::vector<int> v;

const std:;vector<int>::iterator itr = vec.begin();
*itr = 10;	// OK
++itr;		// Error

std::vector<int>::const_iterator citr = vec.begin();
*citr = 10;	// Error
++citr;		// OK
```

<br>

### 함수와 const

* 매개변수, 반환 값, 멤버 함수 앞, 함수 전체에 `const`의 사용이 가능합니다.

1. 매개변수

   * 함수 내에서 매개변수의 변경을 막습니다.

   ```C++
   void func(const Person* p) {
       p->name = "Heon";	// Error
   }
   ```

<br>

2. 반환 값

   * 포인터나 참조를 반환하는 경우, 대상을 변경하는 것을 막습니다.

   ```c++
   class Point {
   private:
       int x, int y;
       Person(int _x, int _y) : x(_x), y(_y) {};
   public:
       const int& getX() { return x; }
       const int& getY() { return y; }
       
       const Point operator* (const Point& p1, const Point& p2) {
           int newX = p1.getX() + p2.getX();
           int newY = p1.getY() + p2.getY();
           
           return new Point(newX, newY);
       }
   }
   
   // 만약 operator*의 반환형을 const로 선언하지 않으면 다음과 같은 문제가 발생할 수 있습니다.
   Point p1, p2, p3;
   (p1 * p2) = p3;		// Error가 발생하지 않습니다.
   ```

<br>

3. 함수 전체
   * 함수 전체에 대해 `const`이 사용되었을 경우, 이를 상수 멤버 함수라고 합니다.
   * 아래에서 자세히 다루겠습니다.

<br>

### 상수 멤버 함수

* 멤버 함수에 사용됩니다.
* 함수 내에서 멤버 변수 값의 변경을 막습니다.
  * 만약 변경하고 싶다면 해당 멤버 변수에 `mutable`을 사용하면 돱니다.
* **상수 객체만 호출할 수 있습니다.**
  * c++의 핵심 기능 중 하나인 **객체 전달을 '상수 객체에 대한 참조자(reference-to-const)'로 진행하는 것**에 사용됩니다.
* **클래스의 인터페이스를 이해하기 좋게 할 수 있습니다.**
  * 해당 클래스로 만들어진 객체를 변경할 수 있는 또는 변경할 수 없는 함수에 대한 인지를 사용자 쪽에 알릴 수 있습니다.

```c++
class TextBlock {
public:
    const char& operator[] {std::size_t position} const {
        length = strlen(text); // mutable로 선언했으므로 변경이 가능
        return text[position];
    }
    
    char& operator[] {std::size_t position) {
        length = strlen(text); // 당연히 변경이 가능
        return text[position];
    }
                      
private:
	static string text = "Hello World";
    mutable int length;
}
    
int main() {
    TextBlock tb;
    std::cout << tb[0];
    
    const TextBlock ctb;
    std::cout << ctb[0];
}
```

<br>

> **상수 멤버 함수의 의미**
>
> 1. 비트수준 상수성 (물리적 상수성)
>
>    해당 객체를 구성하는 비트들 중 어떠한 것도 바꾸지 않을 때 `const`임을 인정하는 개념입니다. 이는 상수 멤버 함수의 반환형에 대해 `const`가 적용되어 있지 않을 경우 위배됩니다. 따라서 상수 멤버 함수의 반환형에는 `const`가 적용되어야 옳게된 구현입니다.
>
> <br>
>
> 2. 논리적 상수성 (개념적 상수성)
>
>    어쩔 수 없이 상수 멤버 함수 내에서 멤버 변수의 값을 변경해야 하는 경우, 사용자가 알아차리지 못하도록 해야 한다는 개념입니다. `mutable`을 이용해서 구현이 가능합니다.
>
> <br>
>
> 결론적으로 컴파일러 쪽에서 보면 비트수준 상수성을 지키고 개발자는 논리적 상수성을 지켜야 합니다.



<br>

### 상수 멤버 및 비상수 멤버 함수에서 코드 중복을 피하는 법

* 상수, 비상수 객체에 대한 멤버 함수를 정의할 경우, 동일한 코드가 사용될 확률이 높으므로 코드 중복이 발생할 수 있습니다.
* 주요 처리 부분을 구현한 함수를 상수, 비상수 멤버 함수에서 호출하면 되지만, 함수 호출이 두 번씩 되므로 좋은 코드라고는 보기 힘듭니다.
* 따라서 `const` 캐스팅을 이용해서 비상수 멤버 함수가 상수 멤버 함수를 호출하는 방식으로 구현해 코드 중복을 해결할 수 있습니다.
  * 상수 멤버 함수 내에서 비상수 멤버 함수를 호출하는 것은 객체를 변경할 위험이 있기 때문에 지양해야 합니다.

```c++
class TextBlock {
public:
	const char& operator[] (std::size_t position) const {
        // 긴 코드
        
        return text[position];
    }    
    
    char& operator[] (std::size_t position) {
        return
            const_cast<char&>(					// 3. 상수 멤버의 반환값을 비상수로 캐스팅
        		static_cast<const textBlock&>	// 1. 자기 자신을 const로 캐스팅
            		(*this)[position]			// 2. const로 캐스팅된 자신에 대해 상수 멤버 호출
        	);
    }
}
```

