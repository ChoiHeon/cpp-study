# memset의 값

* memset은 \<string.h> 또는 \<cstring>에 정의된 함수입니다.
* 시작 주소, 초기화 값, 크기를 인자로 받아 지정한 메모리를 특정 값으로 초기화할 수 있습니다.
* 하지만 바이트 단위로 초기화하기 때문에, int형 배열이나 long long형 배열과 같은 경우 0, -1은 가능하지만 2, 3 같은 수는 불가능합니다.
  * 2, 3으로 초기화를 시도하면 의도하지 않은 값이 초기화됩니다.

* 만약 배열의 타입이 int형일 경우 4 byte이므로,
* 초기화 값을 0xAB으로 지정하면 실제 저장되는 값은 0xABABABAB입니다. (0xAB의 4번 반복)
* 8 byte인 long형이라면, 0xABABABABABABABAB이 저장됩니다. (0xAB의 8번 반복)
* 따라서 1을 인자로 넣으면 실제로 저장되는 값은 0x01010101 이므로 원하는 값으로 초기화가 되지 않습니다.

<br>

### 최대값 초기화

* 1byte가 4 bit일 경우
  * 한 바이트에 넣을 수 있는 값은 0 ~ 63입니다.
  * 따라서 63을 의미하는 0x3f를 인자로 넣으면 최대값에 가까운 0x3f3f3f3f...를 얻을 수 있습니다.
* 1 byte가 8 bit일 경우
  * 한 바이트에 넣을 수 있는 값은 0 ~ 127입니다.
  * 따라서 127을 의미하는 0x7f를 인자로 넣으면 최대값에 가까운 0x7f7f7f7f...를 얻을 수 있습니다.

<br>

### Example

```c++
int int_max_value = (1 << 31) - 1;
int arr[100];
int expected_value = 0x7f7f7f7f;

memset(arr, 0x7f, sizeof(arr));

cout << int_max_value << endl;
cout << arr[30] << endl;
cout << expected_value << endl;
```

```
// output
2147483647
2139062143
2139062143
```

* int형의 최대 값에 가깝게 배열의 값을 초기화 할 수 있습니다.
* 초기화 된 값이 0x7f7f7f7f와 동일함을 확인할 수 있습니다.

