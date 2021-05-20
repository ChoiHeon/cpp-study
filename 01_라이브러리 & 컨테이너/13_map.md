# map

key와 value 쌍으로 구성되어 있는 컨테이너입니다.

노드 기반으로 이루어져있으며 균형 이진 트리 형태입니다.

key의 중복이 불가능합니다.

삽입시 자동으로 정렬됩니다. (기본은 오름차순입니다)

필요에 따라서 동적할당을 합니다.

<br>

## 사용 방법

* 헤더 선언

  > *#include \<*map>

* 객체 생성

  > *map\<key 타입, value 타입> 객체명;*
  >
  > *map<타입1, 타입2> 객체명(복사 객체);*

* 데이터 삽입

  > *객체명.insert({key 값, value 값});*
  >
  > *객체명.insert(pair\<key 타입, vlaue 타입>(key 값, value 값));*
  >
  > *객체명[key 값] = value 값;* 

* 멤버 함수

  > *map<key 타입, value 타입> m;*
  >
  > *m.begin();*
  >
  > *m.end();*
  >
  > *m.rbegin();*
  >
  > *m.rend();*
  >
  > *m.clear();*
  >
  > *m.count(key 값);*
  >
  > *m.empty();*
  >
  > *m.insert(pair 객체);*
  >
  > *m.erase(start, end);*
  >
  > *m.find(key 값);	// 없을 경우 m.end() 반환*
  >
  > *m.swap(map 객체);*
  >
  > *m.upper_bound(key 값);*
  >
  > *m.lower_bound(key 값);*
  >
  > *m.equal_range(key 값);*
  >
  > *m.size();*

