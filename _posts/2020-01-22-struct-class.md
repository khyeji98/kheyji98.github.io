---
comments: true
title: [Swift ) Struct VS Class]
key: 202001221
modify_date: 2020-01-22
picture_frame: shadow
tags:
  - [swift]
---
 
# Struct VS Class
 
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
이렇게 구조체를 초기화하고 내부 인스턴스에 접근하고 싶다면 마침표(.)를 통해 접근할 수 있다.
```
var initializer = SomeStruct(some: 2)
let newSome = initializer.some
initializer.someMethod()
```
내부 프로퍼티 값 변경은 구조체를 변수(var)에 초기화했을 경우에만 가능하다.
```
struct SomeStruct {
    let some: String
}
 
var initializer = SomeStruct(some: "some")
initializer.some = "other" // error! : 'some' is a 'let' constant
```
물론 내부 프로퍼티가 상수로 선언된 경우에도 마침표(.)를 통해 접근할 수 없다.
 
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
`SomeClass()`라고 
 
# 구조체 VS 클래스

#### 공통점

#### 차이점
