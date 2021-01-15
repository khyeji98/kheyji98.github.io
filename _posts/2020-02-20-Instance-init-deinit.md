---
comments: true
title: [Swift ) 인스턴스 생성과 소멸]
key: 202002201
modify_date: 2020-09-12
picture_frame: shadow
tags:
  - [swift]
---
 
# 인스턴스
 
간단히 말해 클래스나 구조체나 열거형에서 생성된 객체, 즉 정의된 클래스를 실제로 사용하는 것을 **인스턴스**라고 한다.   
그리고 초기화는 인스턴스들을 사용하기 위한 필수 과정으로 초기화된 인스턴스는 소멸할 때가 되면 소멸한다.
 
### 이니셜라이저(Initializer)
 
위에서 말한 초기화 과정을 이니셜라이저라고 하며, `init()`을 통해 초기화를 구현 할 수 있다.
```
class SomeClass {
    var someProperty = 0
    
    init() {
        print("initailizer")
    }
}
 
var classResult = SomeClass() // "initailizer"

struct SomeStruct {
    var someProperty: Int
    
    init() {
        self.someProperty = 0
    }
}
 
var structResult = SomeStruct()
print(structResult.someProperty) // 0
```
이렇게 `init()`이라고 정의된 것을 이니셜라이저라고 하며 변수에 초기화됨과 동시에 자동으로 init이 호출된다.   
 
기본값과 초기값이 헷갈릴 수도 있는데 프로퍼티 정의와 동시에 할당해주는 값을 **기본값**, `init()`을 통하거나 타입의 초기화 후 할당해주는 값을 **초기값**이라고 한다.   
만약 기본값을 미리 할당해준다면 초기값을 굳이 설정해주지 않아도 된다.
    
    
이니셜라이저도 함수나 메소드와 같이 파라미터를 가질 수 있는데,
```
class SomeClass {
    var someProperty = 0
    
    init(_ parameter: Int) {
        self.someProperty = parameter
    }
}
 
var classResult = SomeClass(5)
print(classResult.someProperty) // 5
```
예제에 나온 이니셜라이저는 클래스가 초기화될 때 5라는 값을 파라미터로 받아 someProperty에 할당하는 것으로, 애초에 자동완성으로 `SomeClass()`는 뜨지 않는다.   
참고로 이니셜라이저는 하나의 타입에 여러개 정의할 수 있다.
```
class SomeClass {
    var someProperty = 0
    
    init(_ parameter: Int) {
        self.someProperty = parameter
    }
    
    init() {
        print("initializer")
    }
}
 
var classResult = SomeClass()
```
만약 이렇게 이니셜라이저가 두개라면 클래스를 초기화할 때 파라미터가 있는 이니셜라이저로 초기활할 것인지, 파라미터가 없는 이니셜라이저로 초기화할 것인지 선택할 수 있다.

### 디이니셜라이저(Deinitializer)

