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
 
#### Reference)
