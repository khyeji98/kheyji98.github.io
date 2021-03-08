---
comments: true
title: [Swift ) 생성자의 특징과 차이(Designated/Convenience/Required)]
key: 202004022
modify_date: 2020-04-02
picture_frame: shadow
tags:
  - [interview]
  - [swift]
---
 
## 지정 이니셜라이저(designated init)
 
designated init는 스위프트의 기본 초기화 이니셜라이저로, **클래스의 모든 프로퍼티가 초기화** 될 수 있도록 구현해줘야 한다.   
기본 이니셜라이저이기 때문에 클래스 내부에 반드시 한 개 이상의 `init()`이 있어야 하고, 구현시 별도의 키워드없이 `init()`만 호출해주면 된다.
```
class SomeClass {
    var some: String = ""
    var other: Int = 0
    
    init(someValue: String, otherValue: Int) {
        self.some = someValue
        self.other = otherValue
    }
}
```
만약 designated init의 파라미터에서 **클래스 프로퍼티 중 하나라도 빠진다면 바로 에러가 발생**한다.   
 
예제에선 초기화의 파라미터와 클래스의 프로퍼티 차이를 보여주기 위해 some과 someValue, other과 otherValue로 명시했지만,
```
class SomeClass {
    var some: String = ""
    var other: Int = 0
    
    init(some: String, other: Int) {
        self.some = some
        self.other = other
    }
}
```
변수와 상수의 차이가 있기 때문에 이렇게 같은 이름을 사용해도 무방하다.   
 
## 편의 이니셜라이저(convenience init)
 
convenience init은 **보조 이니셜라이저**로, 클래스의 기본 이니셜라이저인 designated init을 보조하는 역할을 한다.
```
class SomeClass {
    var some: String = ""
    var other: Int = 0
    
    init(some: String, other: Int) {
        self.some = some
        self.other = other
    }
    
    convenience init(some: String) {
        self.init(some: some, other: 10) // 반드시 호출해야 함
    }
}
 
let test = SomeClass(some: "test") // SomeClass(some: "test", other: 10)
```
designated init의 파라미터 중 일부를 기본값으로 설정해서, 예제처럼 convenience init 안에서 designated init을 호출해 초기화해야한다.   
즉, 클래스 프로퍼티 중 일부만 초기화를 해준 후 다른 이니셜라이저를 호출해 전체 초기화를 수행하는 것이고 때문에 convenience init을 사용하려면 **무조건 designated init을 먼저 선언**해야 한다.   
이러한 convenience init은 중복되는 초기화 코드를 방지하기 위해 사용된다.
 
#### 이니셜라이저의 상속 조건
 
- 서브 클래스가 designated init을 정의하지 않은 경우, **슈퍼 클래스의 designated init**을 상속받는다.(슈퍼 클래스에 convenience init도 있다면 convenience init까지 자동 상속)
```
class SuperClass {
    var superProperty = ""
    
    init(superProperty: String) {
        self.superProperty = superProperty
    }
    
    convenience init() {
        self.init(superProperty: "convenience initializer")
    }
}
 
class SubClass: SuperClass {
    var subProperty = 0
}
 
let testOne = SubClass(superProperty: "designated initializer") // 슈퍼 클래스의 "designated init" 자동 상속
let testTwo = SubClass() // 슈퍼 클래스의 "convenience init"까지 자동 상속
```
- 서브 클래스가 슈퍼 클래스의 designated init을 **모두 "상속" 또는 "override"** 한 경우, 자동으로 **슈퍼 클래스의 convenience init**을 상속받는다.
```
class SuperClass {
    var superProperty = ""
    
    init(superProperty: String) {
        self.superProperty = superProperty
    }
    
    convenience init() {
        self.init(superProperty: "convenience initializer")
    }
}
 
class SubClass: SuperClass {
    var subProperty = 0
    
    init(superProperty: String, subProperty: Int) {
        // 부모 클래스의 이니셜라이저를 호출하기 전, 서브 클래스 프로퍼티 초기화해야 한다
        self.subProperty = subProperty
        
        // 서브 클래스의 designated init은 "반드시" 슈퍼 클래스의 이니셜라이저를 호출해야 한다
        super.init(superProperty: superProperty)
    }
    
    override convenience init(superProperty: String) {
        self.init(superProperty: superProperty, subProperty: 1)
    }
}
 
let testOne = SubClass() // 슈퍼 클래스의 "convenience init" 자동 상속
let testTwo = SubClass(superProperty: "test")
let testThree = SubClass(superProperty: "test test", subProperty: 2)
```
 
## 필수 이니셜라이저(required init)
 
required init은 모든 서브 클래스에서 **반드시 재정의해야 하는 이니셜라이저**로, 구현할 때와 호출할 때 모두 `required` 키워드를 명시해야 한다.   
또한 반드시 재정의해야 하기 때문에 재정의, 즉 **상속**이 기본으로 포함되어 있으며 재정의하지 않으면 컴파일 에러가 발생하게 된다.   
때문에 상속을 염두에 두고 클래스를 만들 때에는 required init의 포함 유무를 생각해봐야 한다.
```
class SuperClass {
    var superProperty = ""
    
    required init(superProperty: String) {
        self.superProperty = superProperty
    }
}
 
class SubClass: SuperClass {
    var subProperty = ""
    
    init(subProperty: String) {
        self.subProperty = subProperty
        super.init(superProperty: "in SubClass")
    }
}
// error!
```
테스트로 required init을 재정의하지 않았더니, 이렇게 에러가 발생했다.
 
그래서 발생한 에러를 fix했더니,
```
class SuperClass {
    var superProperty = ""
    
    required init(superProperty: String) {
        self.superProperty = superProperty
    }
}
 
class SubClass: SuperClass {
    var subProperty = ""
    
    init(subProperty: String) {
        self.subProperty = subProperty
        super.init(superProperty: "in SubClass") // super.init()도 안하면 error!
    }
    
    // error를 fix했을 때
    required init(superProperty: String) {
        fatalError("init(superProperty:) has not been implemented")
    }
}
 
let test = SubClass(subProperty: "test")
```
이렇게 SubClass 안에 required init 재정의 코드가 생겼다.
 
#### 생성자의 차이점과 특징
 
- 지정 이니셜라이저(designated init) : 
- 편의 이니셜라이저(convenience init) :
- 필수 이니셜라이저(required init) :
 
#### Reference)
 
[https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-initializer-2%ED%8E%B8-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-initializer-7141cda4ecf2](https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-initializer-2%ED%8E%B8-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-initializer-7141cda4ecf2)   
[https://velog.io/@demianjun/Initializer](https://velog.io/@demianjun/Initializer)
