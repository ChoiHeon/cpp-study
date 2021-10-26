# static 키워드

* static 키워드는 선언된 스코프(scope)에 따라서 의미가 달라집니다.

* 전역 스코프에서 선언될 경우, 선언된 파일 내에서만 접근이 가능합니다.

* struct 또는 class 내에서 선언된 경우, 해당 타입의 인스턴스가 여러 개 생성되어도 static으로 선언된 변수 1개만을 공유합니다.

* 지역 스코프(블록) 내에서 선언된 경우, static duration으로 적용됩니다.

  * 만약 함수 내에 static을 사용했다면, 해당 함수의 첫 호출 시에만 초기화가 발생하며, 이후에 호출되어도 초기화가 발생하기 않습니다.

  > auto duration: 블록이 끝나면 자동으로 메모리에서 삭제됩니다.
  >
  > static duration: 한 번만 초기화되며 프로세스가 종료될 때까지 남아있습니다.



### global vs static 변수

* global 변수는 external linkage를 가지므로 다른 파일에서 접근할 수 있습니다.
* static 변수는 현재 파일 내에서만 접근할 수 있으므로 다른 파일의 같은 식별자를 가진 변수와 충돌이 발생하지 않습니다.
* 둘 다 static initialization이므로 선언과 함께 초기화를 하지 않으면 default value 또는 널(NULL)을 갖습니다.