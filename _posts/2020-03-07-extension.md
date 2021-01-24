---
comments: true
title: [Swift ) 확장(Extension)]
key: 202003071
modify_date: 2020-11-24
picture_frame: shadow
tags:
  - [swift]
---
 
## 확장이란?
 
extenstion은 기존의 클래스, 구조체, 열거형의 기능을 추가해 확장시킬 때 사용하는 것으로, 타입에 새로운 기능을 추가할 순 있으나 기존의 기능을 재정의하는 것은 불가능하다.   
**정말 말 그래도 영역 넓히기, 확장!!**   
 
```
extension 확장할 타입명: 상속받을 타입이나 프로토콜 {
    // 새로운 기능들
}
```
확장의 기본 형태는 이런 형태인데, 기존 타입 선언과 크게 다르지 않다.   
역시 상속받을 타입이나 프로토콜이 있다면 확장을 통해 상속받아 기능을 구현해도 된다.(물론 상속받는 것 없이 확장해도 된다)   
보통 코드를 깔끔하게 보기 위해 상속받을 타입이나 프로토콜은 확장을 통해 상속받고 extension에서 기능을 구현하고는 한다.
    
    
#### 확장을 통해 추가할 수 있는 것들
 
- 연산 속성(Computed Properties)
- 이니셜라이저(Initializer)
- 메소드(Methods)
- 서브스크립트(Subscripts)
- 중첩 타입(Nested Types)
 
## 연산 속성
 
확장을 통해 연산 속성은 추가할 수 있으나 저장 속성은 추가할 수 없다.   
왜냐하면 저장 속성을 추가하면 추가 메모리가 필요한데, extension은 메모리 확장을 못하기 때문이다.
```
extension Double {
    var km: Double {
        return self * 1_1000.0
    }
}
```
공식문서에 있는 아주 간단한 예제를 보여준 것인데, 실제 프로젝트에서도 Double, Int, String, UI타입들 등등을 확장해 사용한다.
 
## 이니셜라이저
 
확장을 통해 기본 타입에 새로운 편의 이니셜라이저는 추가할 수 있는데, 새로운 지정 이니셜라이저(designated initializer)나 디이니셜라이저(deinitializer)를 추가할 순 없다.   
즉, 지정 이니셜라이저와 디이니셜라이저는 기존 타입에 정의되어야 한다.
 
## 메소드
 
메소드는 인스턴스 메소드, 타입 메소드 모두 확장을 통해 추가할 수 있다.
```
extension SomeClass {
    func intanceMethod() {
        // code
    }
    
    static func typeMethod() {
        // code
    }
}
 
SomeClass.typeMethod()
 
var some = SomeClass()
some.typeMethod()
```
물론 mutating 인스턴스 메소드도 확장을 통해 추가할 수 있다.
 
## 서브스크립트
 
확장을 통해 새로운 서브스크립트를 추가할 수 있다.
```
extension Int {
  subscript(var digitIndex: Int) -> Int {
    var decimalBase = 1
    while digitIndex > 0 {
      decimalBase *= 10
      --digitIndex
    }
    return (self / decimalBase) % 10
  }
}
 
746381295[0]
// returns 5
746381295[1]
// returns 9
746381295[2]
// returns 2
746381295[8]
// returns 7
```
 
## 중첩 타입
 
클래스, 구조체, 열거형에 확장을 통해 새로운 중첩 타입을 추가할 수 있다.
```
extension Int {
    enum SomeEnum {
        case Some, Other, Another
    }
    
    var result: SomeEnum {
        switch self {
        case 0:
            return .Some
        case 1:
            return .Other
        default:
            return .Another
        }
    }
}
```
이렇게 Int타입을 확장해 SomeEnum이라는 열거형을 중첩으로 추가하는 것이다.
    
    
*확장에 대한 설명은 굉장히 간단하지만, 프로젝트에서 정말 많이 사용하는 스위프트 문법 중 하나이다.*
    
    
#### Reference)
 
[http://minsone.github.io/mac/ios/swift-extensions-summary](http://minsone.github.io/mac/ios/swift-extensions-summary)   
[https://gwangyonglee.tistory.com/48](https://gwangyonglee.tistory.com/48)
