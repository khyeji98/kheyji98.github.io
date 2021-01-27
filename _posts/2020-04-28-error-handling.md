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
 
지금까지 throw, throws, try를 사용한 에러 발생과 던지기에 대해 공부했다면, 이젠 던져진 에러를 어떻게 처리할지에 대해 알아볼 것이다.
 
### do-catch
 
**do**절 안에는 에러가 발생할 때 throw하겠다고 지정한 함수를 `try` 키워드와 함께 호출하고, **catch**절에서 그룹화된 에러 케이스들을 조건문처럼 나열한다.
```
do {
    try 에러 발생시 던질 함수 호출
    // 에러가 발생하지 않았을 때 실행될 코드
} catch 에러 케이스1 {
    // error handling code
} catch 에러 케이스2 where 조건 {
    // error handling code
} catch 에러 케이스3, 에러 케이스4 where 조건 {
    // error handling code
} catch {
    // 그룹화된 에러 케이스 외에 발생한 error handling code
}
```
do-catch문의 기본 형태는 이렇게 되어 있다.   
조건에 부합할 때 발생한 에러 케이스를 처리할 수도 있고, 두 개 이상의 에러 케이스를 쉼표(,)를 사용해 묶을 수 있다.
```
var vendingMachine = VendingMachine()
vendingMachine.coinsDeposited = 8
 
do {
    try buyFavoriteSnack(person: "Alice", vendingMachine: vendingMachine)
    print("Success! Yum.")
} catch VendingMachineError.invalidSelection {
    print("Invalid Selection.")
} catch VendingMachineError.outOfStock {
    print("Out of Stock.")
} catch VendingMachineError.insufficientFunds(let coinsNeeded) {
    print("Insufficient funds. Please insert an additional \(coinsNeeded) coins.")
} catch {
    print("Unexpected error: \(error).")
}
// "Insufficient funds. Please insert an additional 2 coins."
```
아까 열거형을 통해 그룹화한 에러 케이스를 적용해 보자면 이렇게 작성할 수 있다.   
그리고 코인 10개가 필요한데 8개만 넣었으므로 코인이 부족할 때 발생하는 `VendingMAchineError.insufficientFunds(coinNeeded:)` 에러 케이스에 해당한 것이고, 해당 케이스로 catch되었을 때의 코드가 실행된 것이다.
 
### try?
 
`try?`를 사용한 에러 처리는 **에러를 선택적 값으로 변환**해 처리하는 방법인데, 옵셔널과 유사한 방식이라고 할 수 있다.   
해당 방법은 **에러를 던지는 함수가 반환값이 있을 때** 사용할 수 있다.
```
func someThrowingFunction() throws -> Int {
    // code
}

let x = try? someThrowingFunction()
```
someThrowingFunction은 Int값을 반환하는 함수인데, throws 처리된 함수이다.   
그리고 x라는 상수는 해당 함수가 반환하는 값을 할당받을 상수로 someThrowingFunction이 에러를 발생시키면 옵셔널 값, 즉 **nil을 할당**한다는 것이다.
```
let y: Int?
 
do {
    y = try someThrowingFunction()
} catch {
    y = nil
}
```
`let x = try? someThrowingFunction()` 해당 코드라인은 위와 같은 코드를 간결하게 작성한 것이다.   
에러 케이스가 없는 것을 보아, 에러가 발생하면 무조건 nil을 할당한다는 것을 알 수 있다.
```
func fetchData() -> Data? {
    if let data = try? fetchDataFromDisk() { return data }
    if let data = try? fetchDataFromServer() { return data }
    return nil
}
```
이렇게 if-let과 함께 사용하면 더 활용도있게 사용할 수 있다.
    
### try!
 
`try!`
그리고 throws 처리된 함수일지라도 때에 따라 에러가 발생하지 않을 수 있다.   
이런 경우엔 try! 처리를 해도 된다.
```
let photo = try! loadImage(atPath: "./Resources/John Appleseed.jpg")
```
loadImage(atPath:) 함수는 지정된 경로에서 이미지 리소스를 로드하거나 이미지를 로드할 수 없는 경우 에러를 발생시키는 함수이다.   

 
### assert/assertionfailure

### precondition/preconditionfailure

### fetal error
 
#### Reference)
 
[https://gwangyonglee.tistory.com/52](https://gwangyonglee.tistory.com/52)
