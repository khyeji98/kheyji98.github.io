---
comments: true
title: [Swift) Hashable과 Equatable]
key: 202003231
modify_date: 2020-05-11
picture_frame: shadow
tags:
  - [swift]
---
 
## Equqtable
 
Equatable은 **프로토콜**로, **값이 동일한지 아닌지를 비교할 수 있는 타입**이다.   
```
protocol Equatable {
  static func == (lhs: Self, rhs: Self) -> Bool
}
```
즉, Equatable을 준수하는 타입은 "=="와 "!=" 연산자를 사용해 동등성을 비교할 수 있다.   
그리고 스위프트 표준 라이브러리의 대부분 기본 데이터 타입(String, Int, Double 등)은 Equatable을 준수한다.   
 
## Hashable
 
Hashable 역시 **프로토콜**로, **정수 hash를 제공하는 타입**이다.   
표준 라이브러러의 많은 타입들이 Hashable을 준수하는데, 기본적으로 스위프트의 기본타입(String, Int, Double 등)과 Dictionary의 Key와 Enum이 있다.    
 
#### 그렇다면 hash는 뭘까?
**hash**란 해시 함숫에 의해 얻어지는 값으로 해시 값, 해시 코드라고도 한다.
 
a와 b가 같은 타입일 경우, **a==b**이면 **a.hashValue==b.hashValue**이다.   
반대로, a.hashValue==b.hashValue라고 해도 a==b는 true가 아닐 수 있다.   
**동일한 hash 값을 가졌다고 해서 서로 동일한 값일 필요는 없다.**   
 
```
protocol Hashable: Equatable {
  var hashValue: Int { get }
  func hash(into hasher: inout Hasher)
}
```
실제 Hashable 프로토콜을 살펴보면 hash 값을 찾기 위해서 key값인 **hashValue**가 필요하다.   
그리고 더 자세히 보면 Hashable은 Equatable을 상속받고 있는 것을 알 수 있다.
 
### Hashable이 Equatable을 상속받는 이유
 
hash는 반드시 고유한 값이어야 하고, **이 hash가 고유값인지 식별해줄 수 있는 == 함수가 필요하기 때문에** Equatable을 상속받아야 한다.   
기본 데이터 타입인 String, Int, Double 등 역시 이미 Hashable을 상속받고 있기 때문에 자연스럽게 Equatable도 상속받고 있는 것이다.
 
### 사용자 정의 타입에서 Hashable 구현
 
위에서 말한 바에 의하면 Hashable을 상속받으면 Equatable도 자연스레 상속받는 것을 알 수 있다.   
때문에 "전에는" 사용자 정의 타입을 생성할 때 해당 타입을 Hashable로 만드려면 **Equatable에 있는 == 함수를 구현**해줘야 하고, **HashValue**를 만들어줘야 했다.   
그러나 업데이트 이후, **Equatable에 있는 == 함수만 구현**해주면 되고, **HashValue는 자동으로 생성**된다.
 
#### Reference)
 
[https://woongsios.tistory.com/145](https://woongsios.tistory.com/145)   
[https://zeddios.tistory.com/498](https://zeddios.tistory.com/498)
