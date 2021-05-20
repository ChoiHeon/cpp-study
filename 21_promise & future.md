# promise & future

멀티 스레드 환경에서 값을 동기화하여 공유하는 것이 아닌, 함수처럼 결과 반환을 기다리는 식으로 작성하고자 할  때 사용합니다.

<br>

```c++
#include <stdio.h>
#include <iostream>
#include <future>  // promise와 future를 이용하기 위한 라이브러리
#include <thread>  // thread를 이용하기 위한 라이브러리
using namespace std;

// 쓰레드를 위한 함수 (파라미터는 결과를 받기 위한 promise, 반복문의 횟수)
void thread_function(promise<int>* p, int count)
{
  int ret = 0;  // 결과 변수
    
  // 반복문의 횟수만큼 더한다.
  for (int i = 0; i < count; i++)
  {
    ret += i;
  }
    
  p->set_value(ret);  // 결과를 set_value로 넘긴다.
}

int main()
{
  promise<int> p;
  future<int> data = p.get_future();
  
  // 쓰레드를 실행하여 promise를 던지고, 반복문의 횟수를 10을 설정한다.
  thread _th(thread_function, &p, 10);
  
  // data.get()을 하면 promise가 set_value할 때까지 기다린다.
  // 내부적으로 data.wait이 실행된다.
  cout << data.get() << endl;
  
  // thread를 종료한다.
  _th.join();
  return 0;
}
```

*   *future\<int> data = p.get_future();*

  * primise에 set_value 함수를 통해서 값을 넣고
  * future에서 get_value 함수를 통해 값을 얻는 구조입니다.

* *cout << data.get() << endl;*

  * future의 get은 promise의 get_value를 기다립니다.

* 두 객체의 set_value()와 get()은 한 번만 호출이 가능합니다.

  * shared_future 객체를 사용하면 여러번 get 사용이 가능합니다.

    ```c++
    promise<int> p;
    share_future<int> f = p.get_future();
    
    thread _th(thread_function, &p, 10);
    
    cout << f.get() << endl;
    cout << f.get() << endl;
    ```

<br>
기존에 이미 작성한 코드가 있다면 promise 대신, packaged_task를 사용합니다. 

```c++
#include <stdio.h>
#include <iostream>
#include <future>
#include <thread>
using namespace std;

int thread_function(int count)
{
    int ret = 0;
    
    for (int i = 0; i < count; i++) {
        ret += i;
    }
    return ret;
}

int main()
{
    packaged_task<int(int)> task(thread_function);
    shared_future<int> data = task.get_future();
    
    thread _th(move(task), 10);
    
    cout << data.get() << endl;
    cout << data.get() << endl;
    
    _th.join();
    return 0;
}
```

* 이전의 코드와 달리 스레드가 반환값을 가집니다. 
  * 반환값은 packaged_task와 연결된 future에서 get을 통해 얻을 수 있습니다.
* *packaged_task<int(int)> task(thread_function);*
  * thread_function 함수에서 packaged_task를 사용하겠다는 것을 표시합니다.
  * \<int(int)> 는 각각 반환형과 인자입니다.
* *thread _th(move(task), 10);*
  * packaged_task를 통해서 스레드레 함수를 전달합니다.

<br>
위 처럼 복잡한 과정대신, async로 간단하게 할 수 있습니다.

```c++
#include <stdio.h>
#include <iostream>
#include <future>
#include <thread>

using namespace std;

int thread_function(int count) {
    int ret = 0;
    for (int i = 0; i < count; i++)
    	ret += i;
    return ret;
}

int main()
{
    shared_future<int> data = async(thread_function, 10);
    cout << data.get() << endl;
    return 0;
}
```



```c++
#include <iostream>
#include <future>
#include <thread>

using namespace std;

int main() {
    shared_future<int> f = async([](int count) -> int {
        int ret = 0;
        for (int i = 0; i < count; i++) 
            ret += i;
        return ret;
    }, 10);
    
    cout << f.get() << endl;
    return 0;
}
```



### 출처

https://nowonbun.tistory.com/735