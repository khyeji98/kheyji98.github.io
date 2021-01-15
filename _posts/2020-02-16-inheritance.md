---
comments: true
title: [Swift ) 상속(Inheritance)]
key: 202002161
modify_date: 2020-04-25
picture_frame: shadow
tags:
  - [swift]
---
 
# 상속(Inheritance)
 
클래스, 구조체, 열거형 중에서 상속받을 수 있는건 클래스 뿐이다. 그것도 프로토콜과 달리 **하나의 클래스**만 상속받을 수 있다.   
때문에 상속은 클래스가 다른 타입과 차별둘 수 있는 중요한 특징이다.   
 
### 상속이란?
 
자식클래스(subclass)가 부모클래스(superclass)를 상속받으면 자식클래스에서 부모클래스의 프로퍼티, 메소드, 서브스크립트를 호출하거나 재정의까지 할 수 있다.   
또한 부모클래스에서 상속된 프로퍼티에 프로퍼티 옵저버를 추가해, 자식 클래스에서 해당 프로퍼티의 값이 바뀔 때마다 알림을 받을 수 있다.
```
class SuperClass {
    // code
}
 
class SubClass: SuperClass {
    // code
}
```
이렇게 자식클래스가 부모클래스를 상속받는 것이다.
 
### 서브클래싱(Subclassing)
 
서브클래싱은 부모클래스를 상속받은 자식클래스를 말하는 것으로, 다른 클래스를 상속받아 새로운 클래스를 만드는 것을 **서브클래싱**이라고 한다.
```
class SuperClass {
    var superProperty = 0
}
 
class SubClass: SuperClass {
    var subProperty = 10
}
```
이렇게 각 클래스에 프로퍼티가 정의되어 있는데,
```
var result = SubClass()
result.superProperty = 5
```
자식클래스는 부모클래스를 상속받았기 때문에 자식클래스만 인스턴스화해줘도 부모클래스의 프로퍼티에 접근할 수 있고, 값도 변경할 수 있다.
```
class SubSubClass: SubClass {
    var subSubProperty = 20
}
```
SuperClass를 상속받았던 SubClass를 또 상속받는 SubSubClass를 정의하고, 이 클래스에 새로운 프로퍼티 subSubProperty도 정의했다.
```
var result = SubSubClass()
result.superProperty = 1
result.subProperty = 11
result.subSubProperty = 21
```
물론 이렇게 부모클래스의 부모클래스의 프로퍼티까지도 접근할 수 있고 값도 변경할 수 있다.
 
```
class SuperClass {
    var superProperty: Int {
        return 0
    }
}
```
만약 SuperClass에 정의된 superProperty가 get-only 프로퍼티였다면?
```
var result = SubSubClass()
print(result.superProperty)
```
값을 변경할 수는 없지만 값 읽기는 가능하다.
 
### 오버라이딩(Overriding)
 
아까 
