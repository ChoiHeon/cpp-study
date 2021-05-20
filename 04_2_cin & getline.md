# cin & getline

cin와 getline을 같이 사용할 때, 다음과 같은 문제가 발생할 수 있습니다.

``` c++
int n;
string s;

cin >> n;
getline(cin, s);

cout << n << endl;
cout << s << endl;
```

```
// input
3
hello world!

// expected output
3
hello world!

// output
3
(개행문자)
```

* 정수 3 입력시 '\\n'이 버퍼에 남아있습니다.
* 버퍼에 남아있는 개행문자가 getline 실행시 읽히면서 바로 함수가 종료됩니다.

<br>
따라서 cin의 버퍼를 비우는 cin.ignore() 함수를 실행해야 합니다.

```c++
int n;
string s;

cin >> n;

cin.ignore(); // 입력 버퍼를 비움

getline(cin, s);

cout << n << endl;
cout << s << endl;
```

