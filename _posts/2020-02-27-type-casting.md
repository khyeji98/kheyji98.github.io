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

### 업 캐스팅
 
업 
 
### 다운 캐스팅
