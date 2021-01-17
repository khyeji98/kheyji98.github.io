---
comments: true
title: [Swift ) 타입 캐스팅(Type Casting)]
key: 202002271
modify_date: 2020-02-28
picture_frame: shadow
tags:
  - [swift]
---
 
# 타입 캐스팅(Type Casting)
 
타입 캐스팅이란 인스턴스의 타입을 확인하거나 인스턴스의 타입을 쉽게 다루기 위해 사용되는 문법인데, `is`와 `as` 연산자를 사용한다.    
이 두 연산자는 값의 타입을 확인하거나 값을 다른 타입으로 변환하는 것으로 매우 간단한 방법이다.
 
### is
 
`is`를 통한 타입 캐스팅은 예제를 보는 것이 가장 이해가 빠를 것이다.
```
class SomeClass {
    var someProperty: String
    
    init(some: String) {
        self.someProperty = some
    }
}
 
var result = SomeClass(some: "some property")
 
if result is SomeClass {
    print("true")
} else {
    print("false")
}
// "true"
```
가장 간단하게 표현해 보자면 이렇게 result가 SomeClass의 인스턴스인지를 확인하는 것이고, 결과로 true가 출력된다.
```
if result.someProperty is String {
    print("true")
} else {
    print("false")
}
// "true"
```
이 경우도 마찬가지로 `result.someProperty`가 "some property"를 반환하기 때문에 "some property"가 String인지 확인하는 것이고, 결과로 true가 출력된다.

### 업 캐스팅(as)
 
업 캐스팅이란 서브클래스에서 슈퍼클래스로 형변환(타입캐스팅)하는 것을 뜻하는데, 쉽게 말해 서브클래스로 초기화했음에도 불구하고 슈퍼클래스의 프로퍼티와 메소드를 사용하기 위해 사용하는 것이다.
```
class SomeClass {
    var someProperty: String
    
    init() {
        self.someProperty = ""
    }
    
    init(some: String) {
        self.someProperty = some
    }

}
 
class OtherClass: SomeClass {
    var otherProperty: Int
    
    override init() {
        self.otherProperty = 0
        
        super.init()
    }
 
    init(some: String, other: Int) {
        self.otherProperty = other
        
        super.init(some: some)
    }
}
 
class AnotherClass: SomeClass {
    var anotherProperty: String
    
    override init() {
        self.anotherProperty = ""
        
        super.init()
    }
    
    init(some: String, another: String) {
        self.anotherProperty = another
        
        super.init(some: some)
    }
}
 
var someClass = SomeClass()
var otherClass1 = OtherClass()
var otherClass2 = OtherClass() as SomeClass
var anotherClass1 = AnotherClass()
var anotherClass2 = AnotherClass() as SomeClass
```
먼저 OtherClass와 AnotherClass가 모두 SomeClass를 상속받은 상태이며,   
변수 otherClass1과 anotherClass는 각각 OtherClass와 AnotherClass를 초기화한 것이고 otherClass2와 anotherClass2는 각각 OtherClass와 AnotherClass를 초기화한 것임에도 `as`를 통해 SomeClass로 업캐스팅된 상태이다.
```
otherClass1.someProperty = "some property"
otherClass1.otherProperty = 5

otherClass2.someProperty = "some property"

anotherClass1.someProperty = "some property"
anotherClass1.anotherProperty = "another property"

anotherClass2.someProperty = "some property"
```
otherClass1과 anotherClass1은 업캐스팅을 하지 않았기 때문에 자기자신의 인스턴스와 슈퍼클래스의 인스턴스 모두 접근할 수 있지만,   
otherClass2와 anotherClass2는 SomeClass로 업캐스팅했기 때문에 슈퍼클래스인 SomeClass의 인스턴스만 접근할 수 있고 정작 초기화한 자기자신의 인스턴스에는 접근할 수 없다.
 
### 다운 캐스팅(as?/as!)
 
업캐스팅과 
