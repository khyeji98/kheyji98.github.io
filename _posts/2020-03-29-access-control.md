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
즉, 이렇게 **모듈별, 파일별로 접근제어를 제공**한다는 것이다.
 
## 접근제어 레벨(Access Level)
 
접근제어는 접근수준 키워드를 통해 구현하며, 접근레벨 키워드에는 open, public, internal, fileprivate, private가 있다.   
접근이 가장 높은, 접근 제한이 가장 낮은 키워드부터 설명을 할 것이다.
 
### oepn
 
open 키워드는 **개방 접근레벨**로 접근제한이 가장 낮다.   
open 접근은 클래스와 클래스의 멤버에만 사용할 수 있으며, open 접근으로 정의된 클래스는 정의된 모듈 밖의 다른 모듈에서도 상속할 수 있다.   
또한 open 접근으로 정의된 클래스의 멤버는 해당 멤버가 정의된 모듈 밖의 다른 모듈에서도 재정의할 수 있다.   
 
클래스를 open 접근으로 정의한다는 것은 **해당 클래스를 다른 모듈에서도 부모클래스(super class)로 사용하겠다는 목적으로 정의된 것**이다.
 
### public
 
public 키워드는 **공개 접근레벨**로 public 접근으로 정의된 요소는 어디서든 사용할 수 있다.   
public 접근은 open 접근과 비슷하지만 명확한 차이가 있다.
 
#### open VS public
 
open과 public 접근으로 정의된 프로퍼티, 메소드 등은 모든 모듈 및 소스파일 내에서 **사용**할 수 있다.   
그래서 open과 public 접근 모두 일반적으로 프레임워크에 공용 인터페이스를 지정할 때 사용된다.   
그러나, open과 public에는 차이가 있다.
 
**public은 모듈 외부에서 상속할 수 없다.**   
open과 public의 공통점을 설명할 때 "사용"이라는 키워드에 강조를 했었다.   
oepn과 public은 모듈의 내외부, 소스파일의 내외부에서 모두 **사용**은 가능하지만 public의 경우 모듈의 외부에서 **상속**은 불가능하다.
```
// SomeSourceFile.swift
// SomeFramework
// Created by Hyeji on ...
 
public class PublicClass {
    public init(){
        // code
    }
}
```
예를 들어 이렇게 SomeFramework 모듈 안에 있는 SomeSourceFile에 PublicClass라는 public 접근 클래스를 정의했다고 가정해보자.
```
// 소스파일 in 외부에 있는 다른 모듈
 
import SomeFramework
 
// 사용
let publicClass = PublicClass() // ok!
 
// 상속
class SomeClass: PublicClass { // error!
    // code
}
```
이렇게 사용과 상속이 다르고, public은 외부 모듈에서 사용은 가능하나, 상속이 불가능하다는 것을 알 수 있다.   
그렇기 때문에 open의 접근제한이 public보다 더 낮은 것이다.
 
### internal
 

 
### fileprivate

### private

#### Reference)
 
[https://zeddios.tistory.com/383](https://zeddios.tistory.com/383)   
[https://velog.io/@zooneon/Swift-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90](https://velog.io/@zooneon/Swift-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)   
[https://seoyoung612.tistory.com/entry/Swift-%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4-Access-control-open-public-internal-file-private-private](https://seoyoung612.tistory.com/entry/Swift-%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4-Access-control-open-public-internal-file-private-private)
