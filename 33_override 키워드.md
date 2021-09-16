# override 키워드

* C++에서 오버라이드는 다형성을 위해 많이 사용됨
* 하지만 매개변수를 추가하거나 반환형이 다른 등의 실수를 컴파일러가 막아주지 않음
* `override` 키워드를 붙이면 이러한 실수를 막을 수 있으며 가독성 또한 높일 수 있음

```c++
class AAA {
public :
	virtual void foo() abstract;
};

class BBB : public AAA {
public:
	virtual void foo(int a) {
		cout << "foo(int a)" << endl;
	}
};
```

* 위와 같은 상황은 올바른 오버라이드가 아니며 이를 막기 위해서 `override` 키워드를 추가해야 함

```c++
class BBB : public AAA {
public:
	virtual void foo(int a) override { // 컴파일 에러 발생
		cout << "foo(int a)" << endl;
	}
};
```



