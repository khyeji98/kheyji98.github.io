---
comments: true
title: [Swift ) 함수와 메소드(Function VS Method)]
key: 202004011
modify_date: 2020-10-24
picture_frame: shadow
tags:
  - [swift]
---
 
# Funtion VS Method
 
함수와 메소드, 대충 의미는 알겠지만 차이를 모르고 커뮤니케이션할 때 사용해왔다.   
 
간단하게 말하자면 전역이던, 지역이던 독립적인 기능을 수행하는 **코드조각**을 **함수(function)**,   
클래스, 구조체, 열거형 타입 내에서 정의된 **함수**를 **메소드(Method)** 라고 한다.   
결국 메소드도 함수의 일종이라는 것이고 우리가 흔히 볼 수 있는 ViewController 내에서 정의되는 함수는 **메소드**라고 할 수 있다.   
 
```
func someFunction() {
    // code
}
 
class SomeClass {
 
    func someMethod() {
        // code
    }
    
}
```
아무래도 프로젝트 중 커뮤니케이션을 할 때는 대부분 메소드를 다루기 때문에 함수와 메소드의 차이를 몰랐을 것이다.   
 
그렇다면 알고리즘 코드리뷰할 때는 **함수**라고 해야할까, **메소드**라고 해야할까?   
Command Line Tool에서는 클래스를 만들 일이 드물기 적기 때문에 함수라고 많이들 얘기했던 것이다.   
고로 상황에 따라 함수, 메소드를 사용하는 것이 아닌 그 차이를 명확히 알고 써야할 것!!   
 
그렇다면 이제 함수와 메소드의 차이도 명확히 알았으니 둘에 대해 더 자세히 알아보자.
 
# Function
 
### 기본 함수

함수는 특정 기능을 **반복적**으로 할 때 사용하기 위해 만들어진 코드블럭이다.   
먼저 함수 선언의 기본 형태부터 이해해야 다양한 형태의 함수를 이해할 수 있다.
```
func someFunction(파라미터명: 타입) -> 반환타입 {
  // code
}
```
실제 함수를 선언(정의)한 것과 호출한 것이다.
```
// 선언(정의)
func setData(_ data: String) {
    print("Data: \(data)")
}
// 호출
setData(함수) // "Data: 함수"
```
파라미터를 보면 `_ data: String`으로 되어 있는데 여기서 `_`는 함수를 호출할 때 넘기는 파라미터 앞에 라벨, 즉 **파라미터명을 생략**하기 위해 사용되는 것으로 정식명칭은 underscore라고 한다.
 
만약 파라미터명을 생략하지 않는다면
```
func setData(data: String) {
    print("Data: \(data)")
}
  
setData(data: 함수) // "Data: 함수"
```
이렇게 호출될 것이다.
 
### 튜플(Tuple)
 
함수는 기본적으로 반환값이 하나이다.   
그러나 **튜플**을 사용하면 멀티 반환값을 반환할 수 있는데, 튜플이란 배열과 같지만 변경이 불가능한 배열이라고 볼 수 있다.   
```
func someFunction(a: Int, b: Int) -> (Int, Int) {
    return (a, b)
}
```
여기서 `(Int, Int)`와 `(a, b)`가 튜플을 사용한 멀티 반환값이다.   
 
이 외에도 클로저를 사용한 함수 선언 유형이 있다.

### 클로저(Closure)
 
클로저란 코드 내에서 전달되며 사용되는 코드블럭으로, `{}`으로 구분된다.   
함수 역시 클로저의 한 형태이기 때문에 **이름있는 클로저**라고 보면 된다.   
 
클로저는 할당받기, 파라미터 전달, 값 반환 등이 모두 가능한 1급객체이며, 정의되어 있는 상수나 변수들을 참조하거나 저장할 수 있다.   
클로저에는 여러가지 형태가 있는데 우선 기본 형태부터 이해하자.
```
{ (파라미터) -> 반환타입 in
    // code
}
```
클로저도 함수와 같다고 생각하면 된다.
 
알고리즘을 풀 때 클로저는 아주 유용하게 사용된다.
```
let num = [15, 2, 34, 4]
 
let sortedNum = num.sorted(by: { (a: Int, b: Int) -> Bool in
    return a < b
})
 
print(sortedNum) // [2, 4, 15, 34]
```
이렇게 `()`안에 있는 클로저를 인라인 클로저(Inline Closure)라고 한다.   
 
하지만 굳이 인라인 클로저로 작성하지 않아도 결과는 같다.
```
let num = [15, 2, 34, 4]
 
let sortedNum = num.sorted { (a: Int, b: Int) -> Bool in
    return a < b
}
 
print(sortedNum)
```
클로저는 축약을 통해 다양한 형태로 사용할 수 있다.   
 
#### 타입 생략
 
**타입 생략**은 sorted라는 메소드를 정의할 때 이미 파라미터 타입을 정했기 때문에 클로저를 사용할 때는 파라미터명만 명시하고 파라미터 타입은 생략할 수 있다.
```
let sortedNum = num.sorted { (a, b) -> Bool in
    return a < b
}
```
 
#### 반환 타입 생략
 
**반환 타입 생략** 역시 메소드 정의시 반환타입이 이미 정해졌기 때문에 생략할 수 있다.
```
let sortedNum = num.sorted { (a, b) in
    return a < b
}
```
 
#### 파라미터명 생략
 
어차피 클로저 내에서 정해진 파라미터는 클로저 내에서만 유효한 변수이기 때문에 간단한 코드만 구현할 것이라면 파라미터명을 생략해도 된다.   
```
let sortedNum = num.sorted { $0 < $1 }
```
num 배열을 재배열할 때 원소 두 개만 본다고 생각하면, 앞에 있는 원소가 **$0**이고 뒤에 있는 원소가 **$1**이므로   
`2 < 4`, `4 < 15`, `15 < 34` 이렇게 되어 Int값을 오름차순으로 정렬할 수 있게 된다.   
당연한 것같아 보여도 처음 알고리즘을 공부할 때 바로 이해가 안된건 안비밀 ;)   
 
#### 연산자 메소드
 
**연산자 메소드**는 말 그대로 연산자만 사용할 수 있는 코드를 구현할 것이라면, 연산자만 명시할 수 있다는 것이다.   
대신 연산자 메소드를 사용할 땐 (모든 메소드가 그런지는 모르겠지만) `{}`만으로 구분할 수 없다.
```
let sortedNum = num.sorted(by: <)
```

#### 후행 클로저
 
1)클로저를 어떤 메소드의 파라미터로 사용하고 2)클로저의 구현 코드가 길 경우, **후행 클로저**를 통해 함수의 뒤에 코드를 구현할 수 있다.
```
let sortedNum = num.sorted() { (a, b) in
    return a < b
}
```
이렇게 함수를 `()`로 닫고, 뒤에 `{}` 코드블럭을 통해 구현하는 것이다.
 
    
> 클로저는 많이 사용되고 중요한 파트이기 때문에 공부한 기록을 따로 포스팅할 예정이다.
 
# Method
 
앞서 말한 것처럼 메소드는 클래스, 구조체, 열거형 타입 내에서 정의된 함수를 말한다.   
Swift에서 구조체와 열거형을 정의할 수 있다는 것은 Swift VS C와 Objective-C로 구분지을 수 있는 중요한 차이점이라고 한다.   
Objective-C에서 메소드를 정의할 수 있는 타입은 클래스가 유일하기 때문이다.   
Swift에서는 클래스, 구조체, 열거형 정의의 여부를 선택할 수 있으며, 사용자가 만든 타입에 대한 메소드를 유연하게 정의할 수 있다.   
 
메소드에서도 종류가 나뉘는데, **인스턴스 메소드**와 **타입 메소드**가 있다.
 
### 인스턴스 메소드(Instance Method)
 
인스턴스 메소드는 **특정 타입**의 인스턴스에서 호출되는 메소드로, 구현은 당연히 **특정 클래스/구조체/열거형** 내에서 작성해야 한다.
```
class SomeClass {
 
    var some = 0
 
    func someInstanceMethod() {
        some += 1
    }
 
    func otherInstanceMethod(_ other: Int) {
        some += other
    }
 
    func anotherInstanceMethod() {
        some = 0
    }
}
```
특정 클래스 내에서 3가지 인스턴스 메소드를 구현한 것이고, some이라는 변수 저장 프로퍼티를 선언한 것이다.
 
인스턴스 메소드를 호출하기 위해서는 인스턴스 메소드가 구현된 특정 타입을 변수에 **인스턴스화** 해야한다.
```
let instance = SomeClass() // 인스턴스화
 
instacne.someInstanceMethod() // some = 1
 
instance.otherInstanceMethod(1) // some = 2
 
instance.anotherInstanceMethod() // some = 0
```
인스턴스화없이는 **절대** 인스턴스 메소드를 호출할 수 없다.
 
#### self 속성
 
타입 내에 선언된 모든 프로퍼티에는 "**self**"라는 암시적 프로퍼티, 즉 자기자신을 뜻하는데 인스턴스 자신과 정확하게 동일하다.   
한마디로 이 속성을 통해 인스턴스 메소드 내에서 인스턴스 자체를 참조할 수 있다.   
    
 
사실 열마디 설명보다 코드를 직접보고 이해하는게 더 빠르다.
```
func someInstanceMethod() {
        self.some += 1
    }
```
굳이 self라는 키워드를 쓰지 않아도 인스턴스 프로퍼티를 참조한다고 가정한다.   
 
하지만 인스턴스 프로퍼티와 메소드의 파라미터가 이름이 동일하다면 이러한 경우엔 self 키워드를 무조건 사용해야 한다.
```
class SomeClass {
    
    var some = 0
    
    func otherInstanceMethod(some: Int) {
        self.some += some
    }
}
```
두 some을 구분하기 위해서는 self 키워드를 통해 인스턴스 프로퍼티임을 구분지어야 한다.   
물론 이런 경우를 애초에 만들지 않게 방지하는 것이 가장 좋은 방법이다.
 
만약 self를 사용하지 않는 다면 인스턴스 메소드 내에선 인스턴스 프로퍼티와 파라미터 중 **파라미터**가 우선 순위에 든다.   
 
지금까지의 예시는 클래스 타입이었기 때문에 인스턴스 메소드 내에서 프로퍼티를 수정할 수 있었으나,   
**기본적으로** 값타입인 구조체와 열거형은 해당 인스턴스 메소드 내에서 프로퍼티를 수정할 수 없다.   
 
기본적으로는 수정할 수 없었지만 특정 메소드 내에서라도 구조체나 열거형의 프로퍼티를 수정해야 한다면 해당 메소드의 동작을 변경하도록 선택할 수 있다.
```
struct SomeStruct {
    var some = 0.0, other = 0.0
    
    mutating func someInstanceMethod(a: Double, b: Double) {
        some += a
        other += b
    }
}
 
var another = SomeStruct(some: 1.0, other: 1.0)
another.someInstanceMethod(a: 2.0, b: 1.0)
```
`mutating` 키워드를 인스턴스 메소드 맨앞에 붙여주면 그 인스턴스 메소드만은 구조체나 열거형의 프로퍼티를 수정할 수 있게 된다.
그리고 mutating 메소드는 암시적 self 프로퍼티에 완전히 새로운 인스턴스를 할당할 수 있다.
```
struct SomeStruct {
    var some = 0.0, other = 0.0
    
    mutating func someInstanceMethod(a: Double, b: Double) {
        self = SomeStruct(some: some + a, other: other + b)
    }
}
 
var another = SomeStruct(some: 1.0, other: 2.0)
another.someInstanceMethod(a: 2.0, b: 2.0) // a: 3.0, b: 4.0
```
여기서 `self`는 SomeStruct 자체를 의미하기 때문에 새로운 인스턴스가 되는 것이다.
 
> 그리고 `var another`가 아니라 `let another`였다면 인스턴스 프로퍼티들이 `let`으로 선언되는 것과 같은 효과가 발생한다.
 
### 타입 메소드(Type Method)
 
타입 메소드는 **타입 자체**에서 호출되는 메소드라고 할 수 있는데, 메소드 맨 앞에 `static` 키워드를 붙이면 타입 메소드라고 한다.   
클래스의 경우, `class` 키워드를 사용해 서브 클래스가 슈퍼 클래스의 메소드를 재정의(override)할 수 있다.   
 
> 물론 class-타입 메소드는 구조체나 열거형에서 정의할 수 없다.
 
타입 메소드가 인스턴스 메소드와 어떻게 다른지는 코드로 보면 한번에 알 수 있다.
```
class SomeClass {
 
    static func otherTypeMethod(){
        //code
    }
 
    class func someTypeMethod() {
        // code
    }
}
 
SomeClass.someTypeMethod()
 
SomeClass.otherTypeMethod()
```
인스턴스화를 통해 메소드 호출이 가능했던 인스턴스 메소드와는 다르게,   
바로 타입에 체이닝을 통해 메소드 호출이 가능하다.
 
 
class-타입 메소드는 SomeClass를 채택한다면 재정의할 수 있다.
```
class SubClass: SomeClass {
    override static func otherTypeMethod() {
        // code
    }
}
```
타입 메소드를 재정의하는 것이므로 `class` 키워드에서 `override static` 키워드로 변경하여 붙여준다.   
 
 
타입 메소드 내에서도 `self` 키워드를 사용할 수 있지만, 타입 메소드의 경우 인스턴스가 아니라 **타입 자체**를 의미한다.
 
 
#### Reference
 
[https://zeddios.tistory.com/258](https://zeddios.tistory.com/258)
