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
 
Convenience init은 **보조 이니셜라이저**로, 클래스의 기본 이니셜라이저인 Designated init을 보조하는 역할을 한다.
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
 
#### 슈퍼 클래스와 서브 클래스 사이의 이니셔라이저
 
서브클래스의 designated init은 **반드시** 슈퍼클래스의 이니셜라이저를 호출해야 한다.
```
class SuperClass {
    var superProperty = ""
    
    init(superProperty: String) {
        self.superProperty = superProperty
    }
}
 
class SubClass: SuperClass {
    var subProperty = 0
    
    init(superProperty: String, subProperty: Int) {
        self.subProperty = subProperty // 부모 
        super.init(superProperty: superProperty) // 반드시 호출해야 함
    }
}
```


 
## 필수 이니셜라이저(required init)

#### 생성자의 차이점과 특징을 설명하시오.

#### Reference)
 
[https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-initializer-2%ED%8E%B8-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-initializer-7141cda4ecf2](https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-initializer-2%ED%8E%B8-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-initializer-7141cda4ecf2)   
[https://velog.io/@demianjun/Initializer](https://velog.io/@demianjun/Initializer)
