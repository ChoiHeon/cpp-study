# 복사 생성자

클래스의 객체 생성시 이미 존재하는 객체를 복사하여 생성하는 방법이 존재합니다. 이 때 일반적인 생성자 대신 호출할 수 있는 생성자를 복사 생성자라고 합니다.

<br>

```c++
class AAA {

public:
    int n;
	AAA(int _n) : n(_n) {}
    AAA(const AAA& a) n(a.n) {}
}

int main() {
    AAA a1(10);	// 일반 생성자 호출
    AAA a2(a1); // 복사 생성자 호출
    
    AAA a3(AAA(20)); // 일반 생성자만 호출
    
    return 0;
}
```

* 13줄: 컴파일러가 굳이 임시 객체를 생성하지 않고 일반 생성자를 호출합니다.

  