---
comments: true
title: [Swift ) Struct VS Class]
key: 202001311
modify_date: 2020-01-31
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
 
인스턴스를 생성한 구조체는 기본적으로 *멤버와이즈 이니셜라이저*로 초기화할 수 있는데,
```
struct SomeStruct {
    var some: Int
}
 
var initializer = SomeStruct(some: 2)
```
이렇게 

 
# Class
 
### 클래스 정의
 
클래스는 `class`라는 키워드로 정의된다.
```
class 클래스 이름 {
    // code : 프로퍼티 혹은 메소드
}
```

### 구조체 VS 클래스

#### 공통점

#### 차이점
