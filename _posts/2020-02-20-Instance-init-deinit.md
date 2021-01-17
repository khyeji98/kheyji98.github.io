---
comments: true
title: [Swift ) 인스턴스 생성과 소멸]
key: 202002201
modify_date: 2020-09-12
picture_frame: shadow
tags:
  - [swift]
---
 
# 인스턴스
 
간단히 말해 클래스나 구조체나 열거형에서 생성된 객체, 즉 정의된 클래스를 실제로 사용하는 것을 **인스턴스**라고 한다.   
그리고 초기화는 인스턴스들을 사용하기 위한 필수 과정으로 초기화된 인스턴스는 소멸할 때가 되면 소멸한다.
 
### 이니셜라이저(Initializer)
 
위에서 말한 초기화 과정을 이니셜라이저라고 하며, `init()`을 통해 초기화를 구현 할 수 있다.
```
class SomeClass {
    var someProperty = 0
    
    init() {
        print("initailizer")
    }
}
 
var classResult = SomeClass() // "initailizer"

struct SomeStruct {
    var someProperty: Int
    
    init() {
        self.someProperty = 0
    }
}
 
var structResult = SomeStruct()
print(structResult.someProperty) // 0
```
이렇게 `init()`이라고 정의된 것을 이니셜라이저라고 하며 변수에 초기화됨과 동시에 자동으로 init이 호출된다.   
 
기본값과 초기값이 헷갈릴 수도 있는데 프로퍼티 정의와 동시에 할당해주는 값을 **기본값**, `init()`을 통하거나 타입의 초기화 후 할당해주는 값을 **초기값**이라고 한다.   
만약 기본값을 미리 할당해준다면 초기값을 굳이 설정해주지 않아도 된다.
    
    
이니셜라이저도 함수나 메소드와 같이 파라미터를 가질 수 있는데,
```
class SomeClass {
    var someProperty = 0
    
    init(_ parameter: Int) {
        self.someProperty = parameter
    }
}
 
var classResult = SomeClass(5)
print(classResult.someProperty) // 5
```
예제에 나온 이니셜라이저는 클래스가 초기화될 때 5라는 값을 파라미터로 받아 someProperty에 할당하는 것으로, 애초에 자동완성으로 `SomeClass()`는 뜨지 않는다.   
참고로 이니셜라이저는 하나의 타입에 여러개 정의할 수 있다.
```
class SomeClass {
    var someProperty = 0
    
    init(_ parameter: Int) {
        self.someProperty = parameter
    }
    
    init() {
        print("initializer")
    }
}
 
var classResult = SomeClass()
```
만약 이렇게 이니셜라이저가 두개라면 클래스를 초기화할 때 파라미터가 있는 이니셜라이저로 초기활할 것인지, 파라미터가 없는 이니셜라이저로 초기화할 것인지 선택할 수 있다.
    
    
그리고 이니셜라이저를 정의할 때 파라미터에서 값을 받아 프로퍼티에 할당해야 하는데 해당 파라미터에 값을 할당하지 않을 경우가 있을 수 있다. 프로젝트할 땐 여러가지 경우의 수가 있으니까..;   
만약 파라미터를 설정해야 하는데 해당 파라미터 값이 없을 수도 있을 수도 있는 상황이라면,
```
class SomeClass {
    var someProperty = 0
    var optionalProperty: String?
    
    init(some: Int, optional: String) {
        self.someProperty = some
        self.optionalProperty = optional
    }
}
 
var classResult = SomeClass(some: 5, optional: "")
```
이렇게 애초에 값이 없을 수도 있는, 파라미터의 값을 할당받는, 프로퍼티를 옵셔널로 설정해 ""로 값을 주지 않으면 된다.
```
class SomeClass {
    var someProperty = 0
    var optionalProperty: String?
    
    init(some: Int, optional: String?) {
        self.someProperty = some
        self.optionalProperty = optional
    }
}
 
var classResult = SomeClass(some: 5, optional: nil)
```
또한 이렇게 파라미터 자체를 옵셔널 타입으로 설정하는 방법도 있다.   
파라미터 자체가 옵셔널 타입이라면 파라미터에 nil 값을 할당해도 실행이 잘 된다.
    
    
```
class SomeClass {
    let someProperty: Int
    var optionalProperty: String?
    
    init(some: Int, optional: String?) {
        self.someProperty = some
        self.optionalProperty = optional
    }
}
```
참고로 초기화까지만 값을 할당받고 이후 값의 변경이 없어야 하는 프로퍼티는 상수(let)로 정의해 초기값까지만 할당해주면 된다.

#### 기본 이니셜라이저 VS 멤버와이즈 이니셜라이저
 
[클래스 VS 구조체](https://khyeji98.github.io/post/2020/01/22/struct-class.html) 포스팅에서도 설명한 적 있는데 정말 간단히 나눠 설명할 수 있다.
    
    
먼저 구조체는 **기본 이니셜라이저**와 **멤버와이즈 이니셜라이저** 모두 사용할 수 있다.   
그러나 둘을 사용하는 경우가 다른데,
```
struct SomeStruct {
    var someProperty: Int
}
 
var result = SomeStruct(someProperty: 0)
```
이렇게 구조체의 프로퍼티에 기본값을 정의하지 않을 경우엔 초기화시 **멤버와이즈 이니셜라이저**만을 사용해야하고
```
struct SomeStruct {
    var someProperty: Int = 0
}
 
var result1 = SomeStruct()
var result2 = SomeStruct(someProperty: 0)
```
기본값을 정의한다면 **기본 이니셜라이저**와 **멤버와이즈 이니셜라이저** 모두 사용할 수 있다.
    
    
구조체와 달리 클래스는 경우와 상관없이 **기본 이니셜라이저**만을 사용할 수 있다.
```
class SomeClass {
    var someProperty: Int = 0
    var optionalProperty: String?
}
 
var classResult = SomeClass()
```
 
#### 이니셜라이저 실패
 
이니셜라이저의 파라미터로 전달된 값이 정상적인 범주에 들지 않을 가능성이 있어, 이러한 경우 nil을 반환하게 한다.   
이것을 실패할 가능성이 있는 이니셜라이저라고 한다.
```
class SomeClass {
    var someProperty: Int = 0
    var optionalProperty: String?
    
    init?(some: Int, optional: String) {
        if some > 10000 {
            return nil
        }
        
        self.someProperty = some
        self.optionalProperty = optional
    }
}
 
var result1 = SomeClass(some: 5, optional: "optional")
var result2 = SomeClass(some: 10200, optional: "failure")
 
print(result2?.someProperty) // nil
print(result2?.optionalProperty) // nil
```
some 파라미터로 전달된 값이 if문에 해당되어 nil로 반환되었으며, result1엔 초기화에 성공했으나 result2엔 초기화에 실패한 것이다.   
때문에 result2에 초기화된 프로퍼티 값이 모두 nil로 반환된다.
 
> `init?`으로 초기화한 변수 result1, result2는 모두 옵셔널 타입인 SomeClass? 타입이다.
 
### 디이니셜라이저(Deinitializer)
 
디이니셜라이저란 인스턴스가 메모리에서 해제되기 직전에 호출되는 것으로, 해제되기 직전에 인스턴스왁 관련하여 정리 작업을 실행할 수 있다.   
그리고 **디이니셜라이저는 클래스에서만 구현할 수 있다.**
```
class SomeClass {
    var someProperty: Int = 0
    var optionalProperty: String
    
    init(some: Int, optional: String) {
        self.someProperty = some
        self.optionalProperty = optional
    }
    
    deinit {
        print("deinitializer")
    }
}
 
var result: SomeClass? = SomeClass(some: 5, optional: "optional")
print(result?.optionalProperty) // "Optional(optional)"
 
result = nil // "deinitializer"
```
이렇게 클래스를 초기화할 때부터 **옵셔널타입으로 초기화**해줘야 나중에 nil을 할당할 수 있고, 그래야 메모리에서 해제할 수 있다.   
`return = nil`이 실행되는 순간 메모리가 해제되는 것인데 메모리가 해제되기 직전, `deinit`이 실행된다.   
    
    
#### 그렇다면 왜 "optional" 이 아니라 "Optional(optional)"으로 출력되었을까?
 
그건 바로 변수 result가 SomeClass?인 옵셔널타입으로 선언되었기 때문이고, `result.optionalProperty` 값을 부를 때 옵셔널타입인 채로 불렀기 때문이다.   
그리고 이미 작성했을 때부터 옵셔널을 벗겨주지 않았기 때문에 `print(result?.optionalProperty)` 이 코드라인에서 waning이 떴을 것이다.   
    
    
그렇다면 어떻게 해야 안전하게 옵셔널을 벗기고 값을 불러올 수 있을까?
```
var result: SomeClass? = SomeClass(some: 5, optional: "optional")
 
if let result = result {
    print(result.optionalProperty)
} else {
    print("'result' is optional")
}
// "optional"
```
이렇게 `if let`을 통해 옵셔널 바인딩을 해주면 변수인 옵셔널 result가 아니라 if문에 선언된 상수 result으로 프로퍼티에 안전하게 접근할 수 있다.
 
#### Reference)
 
[https://seoyoung612.tistory.com/entry/swift%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8%EA%B8%B0%EB%B3%B8%EB%AC%B8%EB%B2%9508-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EC%83%9D%EC%84%B1%EA%B3%BC-%EC%86%8C%EB%A9%B8](https://seoyoung612.tistory.com/entry/swift%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8%EA%B8%B0%EB%B3%B8%EB%AC%B8%EB%B2%9508-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EC%83%9D%EC%84%B1%EA%B3%BC-%EC%86%8C%EB%A9%B8)   
[https://velog.io/@leeyoungwoozz/Swift-%EB%AC%B8%EB%B2%95-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EC%83%9D%EC%84%B1-%EB%B0%8F-%EC%86%8C%EB%A9%B8](https://velog.io/@leeyoungwoozz/Swift-%EB%AC%B8%EB%B2%95-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EC%83%9D%EC%84%B1-%EB%B0%8F-%EC%86%8C%EB%A9%B8)
