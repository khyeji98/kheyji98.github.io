---
comments: true
title: [Swift ) 에러 처리(Error Handling)]
key: 202004281
modify_date: 2020-12-16
picture_frame: shadow
tags:
  - [swift]
---
 
## 에러
 
스위프트에서 Error는 프로토콜이며, 정확한 타입으로 제시되어 있지 않다.   
고로 Error 프로토콜을 상속해 사용하는데 구조체와 클래스, 열거형 중에서 열거형(Enum)을 주로 사용한다.
 
### 에러 표시와 던지기
 
열거형으로 Error를 그룹화하면 케이스별로 에러를 처리하는데에 편리하다.
```
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```
공식문서의 예제를 인용해보자.   
해당 열거형은 자동 판매기에서의 에러를 케이스별로 그룹화한 것이고 에러 처리를 하기 위해 에러를 발생시켜보자.   
 
에러는 `throw`를 통해 발생시킬 수 있다.
```
throw
    VendingMachineError.insufficientFunds(coinsNeeded: 5)
```
해당 에러는 자동 판매기에 5개의 추가 동전이 필요함을 나타내는 에러이다.
 
### throw
 
throw는 말 그대로 에러를 던진다는 것을 의미하는데, 에러가 발생하면 그대로 **발생한 에러를 던지고 함수 실행은 그대로 종료**한다.
```
// 에러를 던질 수 있는 함수
func canThrowErrors() throws -> String
 
// 함수 내에서 에러를 처리해야 하는 함수
func cannotThrowErrors() -> String
```
이렇게 함수가 반환타입을 지정할 경우에는 `throws` 키워드를 화살표(->) 앞에 명시한다.   
물론 `throws` 키워드를 명시한 함수만이 에러를 전파할 수 있으며, 에러를 던진다고 명시하지 않은 함수는 함수 내에서 에러를 처리해야 한다.
 
***
 
```
struct Item {
    var price: Int
    var count: Int
}
 
class VendingMachine {
    var inventory = [
        "Candy Bar": Item(price: 12, count: 7),
        "Chips": Item(price: 10, count: 4),
        "Pretzels": Item(price: 7, count: 11)
    ]
    var coinsDeposited = 0

    func vend(itemNamed name: String) throws {
        guard let item = inventory[name] else {
            throw VendingMachineError.invalidSelection
        }

        guard item.count > 0 else {
            throw VendingMachineError.outOfStock
        }

        guard item.price <= coinsDeposited else {
            throw VendingMachineError.insufficientFunds(coinsNeeded: item.price - coinsDeposited)
        }

        coinsDeposited -= item.price

        var newItem = item
        newItem.count -= 1
        inventory[name] = newItem

        print("Dispensing \(name)")
    }
}
```
VendingMachine 클래스에 정의된 vend(itemNamed:) 메소드를 보면 `throws` 키워드를 명시해 **에러를 던지는 함수로 지정**했고, inventory[name]이 옵셔널일 경우 VendingMAchineError.invalidSelection를 통해 **에러를 전파**할 것이다.
**throws는 에러를 던질 함수**에, **throw는 에러를 전파할 곳**에 사용하는 키워드이다.
 
그리고 vend(itemNamed:)는 에러를 전파하는 메소드이기 때문에 해당 메소드를 호출할 때마다 **do-catch**를 사용해 에러를 처리하거나 계속 전파해야 한다.
    
    
```
let favoriteSnacks = [
    "Alice": "Chips",
    "Bob": "Licorice",
    "Eve": "Pretzels",
]
 
func buyFavoriteSnack(person: String, vendingMachine: VendingMachine) throws {
    let snackName = favoriteSnacks[person] ?? "Candy Bar"
    try vendingMachine.vend(itemNamed: snackName)
}
```
먼저 throws 처리된 함수를 호출할 땐 `try` 키워드를 앞에 붙여줘야 한다.   
vend(itemNamed:)는 throws 처리된 함수이기 때문에 try 처리를 해줬다.
```
struct PurchasedSnack {
    let name: String
    
    init(name: String, vendingMachine: VendingMachine) throws {
        try vendingMachine.vend(itemNamed: name)
        self.name = name
    }
}
```
이니셜라이저 역시 이렇게 throws 처리를 할 수 있다.
 
## 에러 처리
 
지금까지 
 
### do-catch
 
지금까지 에러 발생과 
 
### assert/assertionfailure

### precondition/preconditionfailure

### fetal error
 
#### Reference)
 
[https://gwangyonglee.tistory.com/52](https://gwangyonglee.tistory.com/52)
