---
comments: true
title: [Swift ) 접근제어(Access Control)]
key: 202003291
modify_date: 2020-07-19
picture_frame: shadow
tags:
  - [swift]
---
 
## 접근제어란?
 
접근제어는 코드끼리 상호작용할 때 파일 간 또는 모듈 간에 접근을 제한할 수 있는 기능이다.   
불필요한 접근으로 의도치 않은 결과를 초래하거나 꼭 필요한 부분만 제공하는 것이 아닌 전체 코드 노출의 가능성이 있을 때 **접근제어**를 사용한다.   
접근제어를 제공한다는 것은 **객체 지향의 "은닉화"** 를 제공한다는 뜻이다.   
 
여기서 **은닉화**란 객체 외부에서 객체 내의 자료로 접근하는 것을 제한하고 데이터를 수정 및 조작하는 동작은 내부에 두고 접근(get) 및 설정(set)하는 메소드를 통해 결과만 받는다는 것이다.   
한마디로 **외부에서는 내부 움직임을 알 수 없으며 데이터에 어떤 값이 있는지 또는 어떤 변화가 일어나고 있는지 알 수 없고,** 단지 데이터의 접근을 get, set 메소드를 통해 결과만 받는다.   
그리고 객체지향에서의 이 역할을 스위프트에서 **접근제어**가 하는 것이다.   
    
    
접근제어는 개별 타입(클래스, 구조체, 열거형) 뿐만 아니라, 해당 타입에 속하는 프로퍼티, 메소드, 이니셜라이저, 서브스크립트에 대해 특정 접근 레벨을 지정할 수 있다.   
간단히 보여주자면,
```
public class SomeClass
public struct SomeStruct
public enum SomeEnum
public func
public var/let
public init
public subscript
```
이런식으로 맨 앞에 접근 제어자 키워드를 붙여 특정 접근 레벨을 지정하는 것이다.(public은 접근 제어자 키워드 중 하나이다.)

#### 모듈 및 소스파일
 
**접근제어는 모듈 및 소스파일을 기반**으로 하는데, 모듈은 프레임워크나 앱 번들을 말하는데 우리가 UI요소들을 사용하기 위해 import하는 UIKit도 하나의 모듈이다. `import` 키워드를 사용하는 것은 모두 모듈이라고 볼 수 있다.   
소스파일은 말 그대로 모듈 내의 단일 스위프트 소스 코드 파일, 단일 파일을 말한다.   
즉,

 
#### Reference)
 
[https://zeddios.tistory.com/383](https://zeddios.tistory.com/383)   
[https://velog.io/@zooneon/Swift-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90](https://velog.io/@zooneon/Swift-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)   
[https://seoyoung612.tistory.com/entry/Swift-%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4-Access-control-open-public-internal-file-private-private](https://seoyoung612.tistory.com/entry/Swift-%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4-Access-control-open-public-internal-file-private-private)
