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
 
Designated init는 스위프트의 기본 초기화 이니셜라이저로, **클래스의 모든 프로퍼티가 초기화** 될 수 있도록 구현해줘야 한다.   
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
만약 Designated init의 파라미터에서 **클래스 프로퍼티 중 하나라도 빠진다면 바로 에러가 발생**한다.   
 
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
        self.init(some: some, other: 0)
    }
}
```
Designated init의 파라미터 중 일부를 기본값으로 설정해서, 예제처럼 Convenience init 안에서 Designated init을 호출해 초기화할 수 있다.   
즉, 클래스 프로퍼티 중 일부만 초기화를 해준 후 다른 이니셜라이저를 호출해 전체 초기화를 수행하는 것이고 때문에 Convenience init을 사용하려면 **무조건 Designated init을 먼저 선언**해야 한다.   
이러한 convenience init은 중복되는 초기화 코드를 방지하기 위해 사용된다.
 
#### 슈퍼 클래스와 서브 클래스 사이의 이니셔라이저
 

 
## 필수 이니셜라이저(required init)

#### 생성자의 차이점과 특징을 설명하시오.

#### Reference)
