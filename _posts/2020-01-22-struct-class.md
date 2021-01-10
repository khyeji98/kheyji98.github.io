---
comments: true
title: [Swift ) Struct VS Class]
key: 202001221
modify_date: 2020-01-22
picture_frame: shadow
tags:
  - [swift]
---
 
# Struct와 Class
 
Struct와 Class는 데이터를 용도에 맞게 **묶어서 표현할 때 용이한 타입**으로, 프로퍼티와 메소드를 통해 구조화된 데이터와 기능을 가질 수 있어 하나의 새로운 **사용자 정의 데이터 타입**을 만드는 것이다.   
둘의 구조가 거의 유사하지만 Struct(구조체)의 인스턴스는 **값 타입**이고, Class(클래스)의 인스턴스는 **참조 타입**이다.   
 
# Struct
 
### 구조체 정의
 
구조체는 `struct`라는 키워드로 정의된다.
```
struct 구조체 이름 {
    // code : 프로퍼티 혹은 메소드
}
```
 
### 구조체 인스턴스 생성 및 초기화
 
구조체는 인스턴스를 생성하고 사용자 정의 이니셜라이저를 구현하지 않으면 기본적으로 멤버와이즈 이니셜라이저를 사용한다.
```
struct SomeStruct {
    var some: Int
}
 
var initializer = SomeStruct(some: 2)
```
`SomeStruct(some: 2)` 이렇게 구조체 내부 프로퍼티를 파라미터(매개변수)로 갖는 것을 **멤버와이즈 이니셜라이저**라고 한다.
```
var initializer = SomeStruct(some: 2)
let newSome = initializer.some
initializer.someMethod()
```
이렇게 구조체를 초기화하고 내부 인스턴스에 접근하고 싶다면 마침표(.)를 통해 접근할 수 있다.
```
struct SomeStruct {
    let some: String
}
 
var initializer = SomeStruct(some: "some")
initializer.some = "other" // error! : 'some' is a 'let' constant
```
내부 프로퍼티 값 변경은 구조체를 변수(var)에 초기화했을 경우에만 가능하다.
물론 내부 프로퍼티가 상수로 선언됐다면 값을 변경할 수 없다.
 
만약 같은 구조체를 초기화한 두 변수가 있는데, 둘 중 하나의 변수에서 내부 프로퍼티 값을 변경하면 나머지 변수에서 같은 프로퍼티 값도 변경될까?
```
struct SomeStruct {
    var property: Int
}
 
var someInit = SomeStruct(property: 0)
var otherInit = SomeStruct(property: 1)
someInit.property = 2
 
print(someInit.property) // 2
print(otherInit.property) // 1
```
정답은 "아니다".   
구조체가 **값 타입**이라는 것은 내부 인스턴스가 다른 곳으로 넘겨지거나 어떤 행동을 취할 때 **무조건 복사**되는 것이고, 초기화된 변수는 인스턴스가 복사된 것이기 때문에 그 변수 내에서만 유효한 값인 것이다.
 
# Class
 
### 클래스 정의
 
클래스는 `class`라는 키워드로 정의된다.
```
class 클래스 이름 {
    // code : 프로퍼티 혹은 메소드
}
```
 
### 클래스 인스턴스 생성 및 초기화
 
클래스는 인스턴스를 생성한 후, 구조체와 달리 기본적인 이니셜라이저를 통해 초기화한다.
    
    
> 참고로 클래스 내부 **저장 프로퍼티**는 객체를 만드는 시점에 무조건 초기값이 있어야 한다.   
 
```
class SomeClass {
    var some: Int = 0
}
 
var initializer = SomeClass()
```
`SomeClass()` 이렇게 초기화하는 것이 기본적인 이니셜라이저이며, 클래스 역시 마침표(.)를 통해 인스턴스에 접근할 수 있다.   
```
class SomeClass {
    var some: Int = 0
}
 
var initializer = SomeClass()
initializer.some = 1 // some = 1
```
그리고 클래스 역시 마침표(.)를 통해 내부 프로퍼티 값을 변경할 수 있다.
 
여기까지는 구조체와 클래스가 별 차이없어보이지만,
```
class SomeClass {
    var some = 0
}
 
let someInit = SomeClass()
someInit.some = 1 // some = 1
```
구조체와 달리 클래스는 초기화할 때 상수(let)로 선언해도 내부 프로퍼티 값을 변경할 수 있다.   
클래스가 참조 타입이기 때문인데, **참조 타입**은 인스턴스를 복사하는 것이 아닌 **동일한 기존 인스턴스에 대해 참조**하는 것이다.   
    
그렇다면 같은 클래스를 참조하는 두 변수가 있을 때를 통해 알아보자.
```
var someInit = SomeClass()
someInit.some = 1
print(someInit.some) // 1

var otherInit = someInit
otherInit.some = 2
print(someInit.some) // 2
```
otherInit이라는 변수의 some 프로퍼티 값을 변경한 것인데 someInit이라는 변수의 some 프로퍼티 값이 변경되었다.   
즉, `var otherInit = someInit`에서 알 수 있듯이 **otherInit이 someInit을 참조한 것이다.**

### 클래스 인스턴스의 소멸
 
클래스의 인스턴스는 참조 타입이기 때문에 더 이상 참조할 필요가 없을 때 **메모리에서 해제**된다.   
메모리에서 해제되기 직전에 **deinit**이라는 내부 메소드가 호출되고, 이것을 디이셜라이저(Deinitializer)라고 한다.
```
class SomeClass {
    var some = 0
    
    deinit {
        print("deinit")
    }
}
 
var someInit: SomeClass? = SomeClass()
someInit = nil // "deinit"
```
someInit이라는 변수에 nil을 할당해줘야 인스턴스가 해제되기 때문에 someInit이 옵셔널이어야 하고,   
`var someInit: SomeClass?`만 해주면 초기화된 것이 아니기 때문에 `var someInit: SomeClass? = SomeClass()` 이렇게 옵셔널임을 명시하고 초기화까지 해줘야 한다.   
그리고 앞서 말했다시피, deinit 메소드는 인스턴스 소멸 직전에 호출되기 때문에 **소멸 전 데이터를 저장**해야 하거나 **소멸되는 것을 알려야 할 때** deinit 메소드 내에서 코드를 구현해줘야 한다. 
 
# Struct VS Class

### Struct
 
 - C언어 등의 구조체보다 다양한 기능 제공
- **값 타입** : 인스턴스가 넘겨지거나 어떤 행동을 취할 때 **무조건 복사**됨
- 상속불가 : 
- Swift 대부분의 큰 뼈대 구성중(Int, Double, String, Dictionary, Array, Set)
 
### Class
 
- 전형적인 OOP(객체지향 프로그래밍) 관점에서의 클래스(객체지향 프로그래밍 글 참고)
- **참조 타입** : 인스턴스의 참조 정보 즉, **값의 메모리 위치**를 넘김(같은 클래스를  초기화한 두 변수 사례를 잘 이해해야 함)
- 단일상속 : 
- Apple 프레임워크 대부분의 큰 뼈대 구성중

<p style="text-align:center"><img width="784" alt="KakaoTalk_Photo_2021-01-10-18-13-09" src="https://user-images.githubusercontent.com/50580583/104118997-1218f480-5370-11eb-8876-137b82683580.png"></p>
    
    
### 구조체는 언제 사용하나요?
 
- 연관된 값들을 모아 하나의 데이터 타입으로 표현하고자 할 때
- 참조가 아닌 복사를 원할 때
- 자신을 상속할 필요가 없거나 자신이 다른 타입을 상속받을 필요도 없을 때
 
#### What Does It Mean?
 
 - 값타입 VS 참조타입 : 작성안함
 - 초기화 : 작성안함
- 객체지향 프로그래밍 : 작성안함
- 프레임워크 : 작성안함

#### Reference)
[https://www.zehye.kr/swift/2020/01/15/19swift_grammer12/](https://www.zehye.kr/swift/2020/01/15/19swift_grammer12/)   
[https://velog.io/@michael00987/Swift-%EA%B0%92-%ED%83%80%EC%9E%85%EA%B3%BC-%EC%B0%B8%EC%A1%B0-%ED%83%80%EC%9E%852020.10.29](https://velog.io/@michael00987/Swift-%EA%B0%92-%ED%83%80%EC%9E%85%EA%B3%BC-%EC%B0%B8%EC%A1%B0-%ED%83%80%EC%9E%852020.10.29)
