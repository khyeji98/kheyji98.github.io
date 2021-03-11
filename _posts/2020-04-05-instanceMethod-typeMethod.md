---
comments: true
title: [Swift ) 인스턴스 메소드와 타입 메소드(Instance Method & Type Method)]
key: 202004051
modify_date: 2020-04-05
picture_frame: shadow
tags:
  - [swift]
---
 
## Method
 
먼저 메소드에 대해 간략히 설명하자면, 메소드란 **특정 클래스, 구조체, 열거형 내에서 구현된 함수**를 뜻한다.
 
***
 
### Instance Method
 
인스턴스 메소드는 **특정 타입의 인스턴스에서 호출되는 메소드**로, 해당 타입을 변수나 상수에 **인스턴스화를 하고 호출**해야 한다.   
 
> 인스턴스화를 하지 않는다면 절대 인스턴스 메소드를 호출할 수 없다.
 
```
class SomeClass {
    func someMethod() {
        print("Instance Method 호출")
    }
}
 
let some = SomeClass() // 인스턴스화
some.someMethod() // "Instance Method 호출"
```
 
### Type Method
 
타입 메소드는 **타입 자체에서 호출되는 메소드**로, 특정 타입의 **인스턴스화없이 바로 호출**이 가능하며 `static` 키워드를 메소드 맨 앞에 명시해줘야 한다.
```
struct SomeStruct {
    static func typeMethod() {
        print("type method in struct")
    }
}
 
SomeStruct.typeMethod() // "type method in struct"
```
인스턴스 메소드와 달리 타입 자체에서 바로 호출되는 것을 볼 수 있다.
 
```
class SuperClass {
    class func classTypeMethod() {
        print("class type method in super class")
    }
}
 
class SubClass: SuperClass {
    override class func classTypeMethod() {
        print("overriding class type method from super class")
    }
}
 
SuperClass.classTypeMethod() // "class type method in super class"
SubClass.classTypeMethod() // "overriding class type method from super class"
```
타입 메소드를 구현하는 특정 타입이 클래스라면 `static` 대신 `class` 키워드를 명시해서 서브 클래스가 있을 경우 재정의할 수도 있다.   
 
#### Instance Method와 Type Method의 차이점을 설명하시오.
 
인스턴스 메소드는 특정 타입의 인스턴스화를 통해 호출할 수 있으나, 타입 메소드는 인스턴스화없이 타입 자체를 통해 바로 호출할 수 있다.
 
#### Reference
 
[https://khyeji98.github.io/post/2020/01/28/function-method.html](https://khyeji98.github.io/post/2020/01/28/function-method.html)
