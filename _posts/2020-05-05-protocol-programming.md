---
comments: true
title: [Swfit ) 프로토콜 지향 프로그래밍(Protocol Programming)]
key: 202005051
modify_date: 2021-01-02
picture_frame: shadow
tags:
  - [swift]
---
 
## 프로토콜 지향 프로그래밍(Protocol-Oriented Programming)
 
기존의 객체 지향 프로그래밍에서는 공통된 기능을 Class 상속을 통해 구현하는데, 스위프트 역시 많은 부분이 Class로 이루어져 있다.   
```
Class UIViewController { }
```
스위프트에서는 대표적으로 UIViewController가 클래스 타입으로 정의되어 있다.

클래스는 상속이 가능하지만 구조체와 열거형의 경우 상속 개념을 통해 공통 기능을 모듈화하여 사용할 수 없기 때문에 **공통 기능 구현**을 위해서는 다른 방법을 이용해야 했다.   
이에 대해 **프로토콜과 익스텐션**을 답했으며, 이를 통해 클래스의 상속과 같이 공통된 기능을 수현할 수 있게 되어 스위프트는 **프로토콜 지향 프로그래밍(POP)** 이 된 것이다.
 
### 프로토콜과 익스텐션
 
> 프로토콜은 따로 포스팅이 되어있으니 간단하게 설명만 할 예정. -> [프로토콜 포스팅](https://khyeji98.github.io/post/2020/03/01/protocol.html)
 
- 프로토콜 : 특정 영할을 수행하기 위한 에소드, 프로퍼티 등 사항들을 한군데에 모아놓은 청사진
- 익스텐션 : 기존 타입의 기능을 확장하도록 도와주는 기능
 
즉 **프로토콜**에는 다른 곳에서 프로토콜을 채택할 때 반드시 구현해야 하는 내용들이 담겨있고, **익스텐션**에는 기존 타입의 기능들을 확장시켜 준다.
 
만약 프로토콜을 채택하는 데이터 타입을 만들 때마다 코드는 중복될 것이다. 뿐만 아니라 추후 이들을 유지보수한다면 정의한 모든 데이터 타입의 코드를 하나하나 변경해줘야 한다.   
이러한 단점을 극복하고자 우리는 **프로토콜 초기구현**을 알아둬야 한다.

### 프로토콜 초기구현
 
프로토콜 초기구현은 구현해야 할 내용들이 담겨있는 **프로토콜**과, 타입의 기능을 확장시켜주는 **익스텐션**의 결합으로 만들어진다.   
 
정의된 프로토콜을 채택한 타입 내부에서 일일이 모든 프로토콜 내 요구사항을 구현할 필요없이 익스텐션을 통해 미리 프로토콜의 요구사항을 구현해 놓을 수 있다.
```
protocol Person {
    var name: String { get }
    var age: Int { get }
    
    func getAge() -> Int
}
 
// 프로토콜 초기구현
extension Person {
    func getAge() -> Int {
        return self.age
    }
}
 
struct Student: Person {
    var name: String
    var age: Int
}
 
let student1 = Student(name: "hyeji", age: 23)
print(student1.getAge())  // 23
```
이렇게 프로토콜과 프로토콜 초기구현을 작성해 놓으면 해당 프로토콜을 준수하는 구조체는 프로토콜의 메소드를 따로 구현할 필요없이 사용할 수 있게 된다.   
 
> 물론 변형이 필요하다면 원래 했던 것처럼 재정의해서 사용할 수 있다.
 
또한 여러 타입에서 해당 프로토콜의 기능을 사용하고 싶을 때 채택만 하면 사용이 가능하다.   
 
여기서 제네릭을 함께 사용한다면 더욱 유연한 프로토콜 사용이 가능해진다.
 
### 프로토콜 with 제네릭과 연관타입
 
```
// 프로토콜 정의
protocol Box {
    associatedtype Item
    
    var items: [Item] { get set }
    
    mutating func addItem(item: Item)
}
// 프로토콜 초기구현
extension Box {
    mutating func addItem(item: Item) {
        items.append(item)
    }
}

// Box 프로토콜을 준수하는 제네릭 타입 구조체 정의
struct StructBox<T>: Box {
    var items: [T]
    
    typealias Item = T
}

var intBox: StructBox<Int> = StructBox(items: [0, 1])
var stringBox: StructBox<String> = StructBox(items: ["A", "B"])
```
예제를 보면 Box 프로토콜 내부에 `associatedtype` 키워드가 있는데, 이건 해당 프로토콜 채택하는 데이터 타입이 제네릭 타입을 사용할 경우 사용하는 것이다.
 
### POP의 장점
 
- **가볍고 안전하다.**
 
상속은 참조타입이기 때문에 참조 추적에 의해 속도가 다소 느리다.   

- **값타입의 상속 효과**
 
값타입에서도 마치 클래스처럼 공통된 기능을 쉽게 구현할 수 있다.
 
- **수평적인 기능 확장**
 
**클래스**는 하나의 슈퍼클래스 상속만 가능하고 수직적인 구조를 고려해야 하지만, **프로토콜**은 마치 블럭처럼 수평 구조로 기능을 추가할 수 있다.
 
- **제네릭의 활용**
 
제닉과 연관값 기능을 통해 보다 유연한 대처를 할 수 있어 강력해졌다.
 
#### Reference)
 
[https://duwjdtn11.tistory.com/618](https://duwjdtn11.tistory.com/618)
