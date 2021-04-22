---
comments: true
title: Swift ) Singleton Pattern
key: 202005091
modify_date: 2020-05-09
picture_frame: shadow
tags:
  - [swift]
---
 
## Sigleton Pattern
 
Singleton Pattern이란 **특정 용도의 객체를 하나 생성**하고 **해당 객체를 공용으로 사용하고 싶을 때 사용**하는 디자인 패턴이다.   
싱글톤 패턴으로 생성된 객체는 임의로 메모리에서 해제해주지 않는 이상 **프로그램이 실행되고 끝날 때까지 메모리에 데이터가 유지**된다.   
때문에 주로 환경설정이나 로그인 정보와 같이 한번 설정하면 해당 데이터가 앱을 종료해도 남아있어야 하는 데이터의 저장 용도로 생성하는데 해당 객체에 데이터를 저장해두면 여러 객체에서 접근하여 데이터를 사용할 수 있다.
 
***
 
#### Singleton Pattern 적용X
 
다음과 같이 유저의 정보를 저장하는 클래스를 만들어보자.
```
class UserInfo {
    var id: String?
    var password: String?
    var name: String?
}
```
만약 인스턴스마다 데이터를 입력하는 VC가 다르다면,
```
// AViewController
let userInfo = UserInfo()
userInfo.id = "hyeji"
userInfo.password = "981207"
 
// BViewController
let userInfo = UserInfo()
userInfo.name = "김혜지"
```
이런 식으로 각 VC마다 UserInfo 객체를 만들어서 저장해줄 것이다.   
 
그런데 우리가 착오한 것이 있다.   
이렇게 각 VC마다 UserInfo 객체를 만들어서 저장해줄 경우, 같은 객체를 공유하고 있는 것이 아니라 각각의 객체가 **따로따로** 생성된 것이기 때문에 우리가 원하는 기능이 될 수 없다.   
**이때 필요한 것이 바로 "Singleton Pattern"이다.**
 
#### Singleton Pattern 적용O
 
```
class UserInfo {
    static let shared = UserInfo()
    
    var id: String?
    var password: String?
    var name: String?
    
    private init() { }
}
```
클래스를 정의할 때 내부에 해당 클래스와 같은 타입의 `shared` **타입 프로퍼티**를 생성하여 객체를 생성하지 않아도 인스턴스에 접근이 가능하도록 한다.   
또한 `UserInfo` 클래스의 객체가 여러번 생성되는 것을 막기위해 init() 함수 접근 제어자를 **private**으로 지정해준다.   
```
let userInfo01 = UserInfo.shared
userInfo01.id = "혜지아님"
print(userInfo01.id) // "Optional("혜지아님")"

let userInfo02 = UserInfo.shared
print(userInfo02.id) // "Optional("혜지아님")"

userInfo02.id = "혜지임"
print(userInfo02.id) // "Optional("혜지임")"
```
클래스의 인스턴스에 대한 접근은 하나의 인스턴스를 공유해야 하기 때문에 static으로 선언해줬던 `shared`를 이용한다.
이 때 타입 프로퍼티가 static 전역 변수로 선언되는데, 이 프로퍼티는 지연 생성(lazy)되기 때문에 `UserInfo`라는 클래스의 객체를 생성하기 전까지는 메모리에 올라가지 않는다.
 
### Singleton의 장단점
 
- **장점**
  - 하나의 인스턴스만을 생성해 공유하므로 메모리 낭비를 방지한다.
  - 싱글톤 인스턴스는 "전역 인스턴스"이기 때문에 다른 클래스들과의 자원 공유가 쉽다.
  - 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 사용된다.
- **단점**
  - 너무 많은 데이터를 공유할 경우 다른 클래스의 인스턴스들 간 결합도가 높아져, "개방=폐쇄" 원칙(객체 지향 설계 원칙)을 위배한다.
  - 수정과 테스트가 어려워진다.
  
#### Reference)
