---
comments: true
title: [Swift ) 타입 캐스팅(Type Casting)]
key: 202002271
modify_date: 2020-02-28
picture_frame: shadow
tags:
  - [swift]
---
 
## 타입 캐스팅(Type Casting)
 
타입 캐스팅이란 인스턴스의 타입을 확인하거나 인스턴스의 타입을 쉽게 다루기 위해 사용되는 문법인데, `is`와 `as` 연산자를 사용한다.    
이 두 연산자는 값의 타입을 확인하거나 값을 다른 타입으로 변환하는 것으로 매우 간단한 방법이다.
 
## is
 
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

## 업 캐스팅(as)
 
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
 
## 다운 캐스팅(as?/as!)
 
업캐스팅과 반대로 다운 캐스팅은 슈퍼클래스에서 서브클래스로 형변환(타입캐스팅)하는 것이며, 역시 서브클래스의 프로퍼티나 메소드를 사용하기 위해 사용한다.
다운 캐스팅에는 `as?`와 `as!` 두가지 연산자로 나뉜다.   
 
- as? : 타입변환에 성공하면 옵셔널값으로 할당, 실패하면 nil 할당
- as! : 타입변환에 성공하면 강제 언래핑된 값 할당, 실패하면 런타임 에러(무조건 성공할 경우에만 사용)
 
다운캐스팅은 실제 프로젝트에서 너무나도 많이 사용되기 때문에 예제가 아닌 실제 프로젝트에 작성된 코드를 가져와봤다.   
tableView를 사용할 때 tableViewDelegate 프로토콜 메소드 중에서 `tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell` 이 메소드를 구현할 때 사용한 코드인데,
```
if let cell = tableView.dequeueReusableCell(withIndentifier: "Title") as? TitleTableCell {
    // TitleTableCell 인스턴스 사용하는 코드들
}
```
이렇게 `if let`과 `as?`를 사용하는 방법도 있고
```
let cell = tableView.dequeueReusableCell(withIdentifier: "Title") as! TitleTableCell
// TitleTableCell 인스턴스 사용하는 코드들
```
이렇게 as!만을 사용하는 방법도 있다.   
`tableView.dequeueReusableCell(withIdentifier:)`은 UITableViewCell 타입이고 나는 UITableViewCell을 상속받은 TitleTableCell의 인스턴스에 접근할 것이기 때문에 다운캐스팅을 통해 접근하는 것이다.
 
#### Reference)
 
[https://jinnify.tistory.com/16](https://jinnify.tistory.com/16)   
[https://zeddios.tistory.com/265](https://zeddios.tistory.com/265)
