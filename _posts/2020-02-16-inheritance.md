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
 
자식클래스(subclass)가 부모클래스(superclass)를 상속받으면 서브클래스에서 클래스의 프로퍼티, 메소드, 서브스크립트를 호출하거나 재정의까지 할 수 있다.   
또한 서브클래스에서 상속된 프로퍼티에 프로퍼티 옵저버를 추가해, 서브클래스에서 해당 프로퍼티의 값이 바뀔 때마다 알림을 받을 수 있다.
```
class SuperClass {
    // code
}
 
class SubClass: SuperClass {
    // code
}
```
이렇게 서브클래스가 슈퍼클래스를 상속받는 것이다.
 
### 서브클래싱(Subclassing)
 
서브클래싱은 슈포클래스를 상속받은 서브클래스를 말하는 것으로, 다른 클래스를 상속받아 새로운 클래스를 만드는 것을 **서브클래싱**이라고 한다.
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
서브클래스는 슈퍼클래스를 상속받았기 때문에 서브클래스만 인스턴스화해줘도 슈퍼클래스의 프로퍼티에 접근할 수 있고, 값도 변경할 수 있다.
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
물론 이렇게 슈퍼클래스의 슈퍼클래스의 프로퍼티까지도 접근할 수 있고 값도 변경할 수 있다.
 
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
print(result.superProperty) // 0
```
값을 변경할 수는 없지만 값 읽기는 가능하다.
 
### 오버라이딩(Overriding)
 
아까 말했듯이 서브클래스는 슈퍼클래스를 상속받아 슈퍼클래스의 인스턴스 메소드, 타입 메소드, 인스턴스 프로퍼티, 타입 프로퍼티, 서브스크립트를 모두 **재정의**할 수 있고 이것을 **오버라이딩**이라고 한다.   
재정의는 `override` 키워드를 맨 앞에 붙여 사용하면 되는데, 재정의할 의도가 명확해야 하고 실수에 의해 정의를 매칭하지 않아야 한다.   
잘못된 재정의는 예상치 못한 결과를 가져올 수 있기 때문이다.
 
#### 서브클래스에서 슈퍼클래스의 메소드, 프로퍼티, 서브스크립트 접근하기
 
사실 서브클래스에서 슈퍼클래스의 메소드, 프로퍼티, 서브스크립트를 재정의할 때 슈퍼클래스에서의 정의를 사용하는 것이 유용하다.   
예를 들어 기존 구현을 재정의함과 동시에, 수정된 값을 상속받은 변수에 저장할 수도 있다.   
    
    
슈퍼클래스의 메소드, 프로퍼티, 서브스크립트에 접근하려면 `super` 키워드를 사용해야 한다.
 
예를 들어 someMethod가 상속받은 슈퍼클래스의 메소드라 하고, 현재 someMethod를 재정의하고 있는 것이다.
```
func someMethod() {
    super.someMethod()
    // code
}
```
이렇게 재정의하고 있는 메소드 안에 슈퍼클래스에서 정의된 메소드를 호출하는 것이다.
 
이 
