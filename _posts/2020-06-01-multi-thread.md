---
comments: true
title: Swift ) 멀티쓰레드로 동작하는 앱 구현시 고려해야 하는 것들
key: 202006011
modify_date: 2020-06-01
picture_frame: shadow
tags:
  - [swift]
---
 
## Thread
 
Thread는 말그대로 실, 가닥이라는 뜻으로 프로그래밍 용어로는 **하나의 프로세스를 구성하는 일련의 실행 코드**를 의미한다. 또한 운영체제의 스케줄러가 관리하는 최소 단위이기도 하다.
 
## Multi-Threading
 
Muti-Threading이란 **여러 개의 스레드(thread)가 동시에 진행되는 것**을 의하는데, 하나의 process 내에 여러 개의 스레드가 존재하고 스레드들은 process의 자원을 공유하되 **실행은 독립적**으로 이뤄지는 구조이다.   
 
### 장점
 
- **메모리 공간과 시스템 자원 소모 감소**
- **프로세스 간 통신 방법에 비해 스레드 간 통신 방법이 간단함**(별도의 자원을 이용하는게 아니라 전역 변수의 공간이나 동적으로 할당된 공간인 Heap 영역을 이용하기 때문)
 
### 단점
 
- **서로 다른 스레드가 데이터와 Heap 영역을 공유하고 있기 때문에 이미 다른 스레드에서 사용중인 변수나 자료구조에 접근하면 엉뚱한 값을 읽어올 수도 있음**
- 병목현상이 발생해 성능이 저하될 가능성이 있음(과도한 lock으로 인한 병목현상을 줄여야 함)
 
### 멀티스레딩 앱 구현시 고려사항
 
가장 기본적으로 **UI 업데이트**에 관련된 작업들은 무조건 **메인 스레드(main thread)** 에서 실행돼야 한다.   
그리고 스레드에 안전하지 않은, **Thread-Unsafe한 변수**는 서로 다른 스레드에서 동시에 접근하면 위험하기 때문에 주의해야 한다.   
 
1. Mutable, Immutable
 

 
2. 프로퍼티 속성
 

 
3. Synchronized
 

 
4. GCD
 

 
5. Class, Struct
 
#### Reference)
 
[https://gwangyonglee.tistory.com/47](https://gwangyonglee.tistory.com/47)   
[https://blog.naver.com/jdub7138/220936452048](https://blog.naver.com/jdub7138/220936452048)
