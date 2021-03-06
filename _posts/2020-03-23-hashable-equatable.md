---
comments: true
title: [Swift) Hashable VS Equatable]
key: 202003231
modify_date: 2020-05-11
picture_frame: shadow
tags:
  - [interview]
  - [swift]
---
 
## Hashable
 
Hashable은 **프로토콜**로, 정수 hash를 제공하는 타입이다.   
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
 
## Equqtable
 
Equatable 역시 **프로토콜**로, **값이 동일한지 아닌지를 비교할 수 있는 타입**이다.   

 
## Hashable VS Equatable

#### Hashable은 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오.

#### Reference)
