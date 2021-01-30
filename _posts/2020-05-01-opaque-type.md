---
comments: true
title: [Swift ) 불명확 타입(Opaque Type)]
key: 202005011
modify_date: 2020-05-01
picture_frame: shadow
tags:
  - [swift]
---

## 불명확 타입(Opaque Type)
 
Opaque 반환 타입을 갖는 함수나 메소드는 반환 타입 정보를 외부에 숨길 수 있다.
```
// 일반 반환 타입
func intReturyTypeFunc(_ parameter: Int) -> Int {
    return some
}
 
// Opaque 반환 타입
func opaqueReturnTypeFunc(_ parameter: Int) -> some Hashable {
    return some
}
```
이렇게 Opaque 반환타입은 "`some` 키워드 + 프로토콜" 같은 방식으로 반환 타입을 명시하며, 명시한 프로토콜을 채택한다면 어떤 타입이든 반환타입이 될 수 있다는 뜻이다.   
타입 정보를 숨기는 것은 모듈과 그 모듈을 호출하는 코드 사이의 경계에서 유용하다. 반환값의 함수 내부에서 사용하는 타입을 숨길 수 있기 때문이다. << 사실 아직도 유용한 이유를 제대로 이해 못했다.   
 
## 불명확 타입으로 해결할 수 있는 문제
 
공식 문서에 올라온 아스키 아트 모듈 예제를 통해 불명확 타입을 이해해보자.
```
protocol Shape { 
    func draw() -> String
}
 
struct Triangle: Shape { 
    var size: Int 
    func draw() -> String { 
        var result = [String]() 
        
        for length in 1...size { 
            result.append(String(repeating: "*", count: length))
        }
        
        return result.joined(separator: "\n") 
    }
}
 
let smallTriangle = Triangle(size: 3)
print(smallTriangle.draw()) 
// * 
// ** 
// ***
```
먼저 Shape 프로토콜을 정의한 후, Shape을 채택한 Triangle이라는 구조체를 만들고 Shape에서 정의된 draw 메소드를 Triangle에서 구현한다.   
구현한 코드를 실행하기 위해 **smallTriangle**이라는 상수에 Triangle 구조체를 초기화해주는데, 초기화시 size 프로퍼티의 초기값에 3을 할당한다.   
즉, **smallTriangle**은 size 프로퍼티의 값이 3인 Triangle 구조체 타입이다.   
그리고 smallTriangle을 통해 draw 메소드를 실행해보면 계단형 삼각형이 아스키 아트로 출력된다.
```
struct FlippedShape<T: Shape>: Shape { 
    var shape: T
    func draw() -> String { 
        let lines = shape.draw().split(separator: "\n") 
        return lines.reversed().joined(separator: "\n") 
    } 
} 
 
let flippedTriangle = FlippedShape(shape: smallTriangle) 
print(flippedTriangle.draw())
// *** 
// **
// *
```
이번엔 FlippedShape이라는 구조체를 정의했는데, Triangle처럼 Shape을 채택하고 있다.   
FlippedShape의 shape 프로퍼티는 **제네릭**을 사용해 **타입 프로퍼티** 타입으로 정의되었고, `<T: Shape>` 이 부분을 보면 FlippedShape에서 타입 프로퍼티는 **Shape을 채택하는 타입**만이 해당된다는 것을 알 수 있다.   
또한 해당 구조체에서 구현된 draw 메소드는 shape의 값을 반대로 출력한다.   
    
    
또한 해당 구조체에서 구현된 draw 메소드는 shape의 값을 반대로 출력한다.   
해당 구조체를 **flippedTriangle**이라는 상수에 초기화했으며 shape의 초기값은 **smallTriangle**이고, shape에는 Shape을 채택하는 값만이 할당될 수 있기 때문에 Triangle 타입인 **smallTriangle**은 해당된다.   
그리고 초기값 그대로 `flippedTriangle.draw()` 해당 코드의 반환값을 출력하면 `smallTriangle.draw()`에서 출력된 아스키 아트와 반대로 출력된다.
```
struct JoinedShape<T: Shape, U: Shape>: Shape {
    var top: T
    var bottom: U
    
    func draw() -> String { 
        return top.draw() + "\n" + bottom.draw() 
    }
} 
 
let joinedTriangles = JoinedShape(top: smallTriangle, bottom: flippedTriangle) 
print(joinedTriangles.draw())
// *
// **
// ***
// ***
// **
// *
```
JoinedShape이라는 구조체는 프로퍼티가 두개이며, 두 프로퍼티 모두 타입 프로퍼티로 Shape을 채택하는 타입만이 올 수 있다.   
JoinedShape 역시 Shape을 채택하고 있기 때문에 draw 메소드를 구현했다.   
지금까지의 예제와 마찬가지로 joinedTriangles라는 상수에 JoinedShape을 초기화했고, top과 bottom 프로퍼티에 각각 **smallTriangle**과 **flippedTriangle**을 초기값으로 할당해줬다.   
그리고 `joinedTriangles.draw()`의 반환값을 출력해보면 **smallTriangle**과  **flippedTriangle**이 합쳐진 아스키 아트를 볼 수 있다.
    
    
이처럼 특정 기능에 관련된 상세 정보를 노출하면 해당 모듈의 퍼블릭 인터페이스에 포함하려 하지 않았던 타입 정보까지 노출하게 된다.   
**모듈 내부**에서는 다양한 기능들을 구현하고 있으며, 해당 기능을 사용하는 **모듈 외부**에서는 그 과정에서의 상세 정보까지 알아야 할 필요가 없다.   
예제를 보면 **Shape 프로토콜**을 구현한 Triangle, FlippedShape, JoinedShape의 구체적인 타입들을 외부에서는 **Shape 프로토콜**만 알고 있어도 작동시킬 수 있도록 바꿔보고자 **불명확 타입**이라는 기능을 사용하는 것이다.
 
## 불명확 타입 리턴하기
 
불명확 타입은 함수의 반환타입으로도 올 수 있다.   
```
struct Square: Shape { 
    var size: Int
    
    func draw() -> String {
        let line = String(repeating: "*", count: size)
        let result = Array<String>(repeating: line, count: size)
        return result.joined(separator: "\n")
    }
}
 
func makeTrapezoid() -> some Shape {
    let top = Triangle(size: 2)
    let middle = Square(size: 2)
    let bottom = FlippedShape(shape: top)
    
    let trapezoid = JoinedShape( 
        top: top,
        bottom: JoinedShape(top: middle, bottom: bottom)
    )
    return trapezoid 
}
 
let trapezoid = makeTrapezoid()
print(trapezoid.draw())
// *
// **
// **
// **
// **
// *
```
makeTrapezoid라는 함수는 반환타입이 `some Shape`으로 Shape 프로토콜을 채택하는 타입은 모두 반환값으로 올 수 있다는 의미의 **불명확 타입**이다.   
때문에 해당 함수는 실제 반환 타입을 노출하지 않고도 사다리꼴 도형을 반환할 수 있다.   
예제를 보면 해당 함수의 실제 반환 타입은 JoinedShape이다.   
지금은 한개의 사각형을 통해 사다리꼴을 만들었지만, **반환 타입을 변경하지 않고** 다른 방식으로 사다리꼴을 만들도록 함수를 수정할 수 있다.
 
또한 불명확 반환 타입을 제네릭과 함께 사용할 수도 있다.
```
func flip<T: Shape>(_ shape: T) -> some Shape {
    return FlippedShape(shape: shape)
}
 
func join<T: Shape, U: Shape>(_ top: T, _ bottom: U) -> some Shape {
    return JoinedShape(top: top, bottom: bottom)
}
let opaqueJoinedTriangles = join(smallTriangle, flip(smallTriangle))
print(opaqueJoinedTriangles.draw())
// *
// **
// ***
// ***
// **
// *
```
이렇게 Shape을 채택하고 있는 모든 타입들을 파라미터로 받으면 해당 값을 반환 값의 프로퍼티에 바로 할당할 수 있다.   
해당 예제를 보면 아까 **joinedTriangles**와 동일하다고 볼 수 있을 것이다.   
그러나 flip과 join 함수는 반환타입을 `some Shape`으로 한번 더 불명확하게 했기 때문에 엄연하게 다르다.
    
    
반환 타입이 불명확 타입인 함수에는 제약이 있다.   
바로 **"언제나 같은 타입을 반환해야 한다"** 는 것이다.   
 
```
func invalidFlip<T: Shape>(_ shape: T) -> some Shape {
    if shape is Square {
        return shape // error! : return types don't match 
    }
    
    return FlippedShape(shape: shape) // error! : return types don't match 
}
```
만약 이런 함수가 있다면 `some Shape`을 통해 반환 타입이 불명확 타입임을 명시했고, 이때 해당 함수는 오직 하나의 타입을 반환해야 한다.   
그러나 if문을 사용해 조건에 해당하면 파라미터에 할당된 타입이, 조건에 해당되지 않는다면 FlippedShape 타입이 반환된다고 작성해 놓았다.   
해당 함수는 요구사항을 지키지 않았기 때문에 유효하지 않은 코드이며, 해당 함수를 정상적으로 작동시키려면 FlippedShape 내부로 옮겨야 한다.
```
struct FlippedShape<T: Shape>: Shape { 
    var shape: T
    
    func draw() -> String {
        // invalidFlip 함수에 작성됐던 코드
        if shape is Square {
            return shape.draw()
        }
        
        let lines = shape.draw().split(separator: "\n") 
        
        return lines.reversed().joined(separator: "\n")
    }
}
```
이렇게 FlippedShape 내부로 함수를 옮기면 draw 메소드는 반환 타입이 불명확 타입이 아니기 때문에 제약도 없다.
```
func invalidFlip<T: Shape>(_ shape: T) -> some Shape {
    // ...
    return FlippedShape(shape: shap)
}
```
그리고 이제 남아있는 코드를 보면 조건문에 해당되지 않았을 때 FlippedShape 타입으로 반환된다는 것인데 코드상으로는 어차피 shape 파라미터에 값이 할당되는 것이고, 그 말은 즉 FlippedShape 구조체를 초기화할 때 shape에 초기값을 할당해주는 것과 같기 때문에 draw 메소드에 따로 코드를 추가하지 않아도 draw 내에서 조건에 해당하지 않을 경우 shape 파라미터를 사용해 코드가 실행된다.   
    
    
정리하자면,   
**FlippedShape의 shape에 값을 할당하면서 FlippedShape 타입을 반환하는 것 = FlippedShape 초기화시 shape에 초기값  할당**   
이렇게 된다는 것이다.
 
## 불명확 타입 VS 프로토콜 타입
 
불명확 타입을 반환하는 것은 프로토콜 타입을 반환하는 것과 매우 유사해 보이지만, 타입의 아이덴티티 보존에 대해 차이가 있다.   
**불명확 타입이 반환 타입**일 땐 특정한 하나의 타입을 가리킬 수 있으며 함수를 호출할 때 그 타입을 특정할 수 없다.   
그러나 **프로토콜 타입이 반환 타입**일 땐 해당 프로토콜을 준수하는 모든 타입이 반환 타입으로 올 수 있다.   
즉, 프로토콜 타입은 값의 실제 타입에 대한 유연성을 높여주는 역할 을 하며, 불명확 타입을 통해 그 실제 타입을 더 강력하게 보장할 수 있다.
```
// 불명확 타입 반환
func flip<T: Shape>(_ shape: T) -> some Shape { 
    return FlippedShape(shape: shape) 
}
 
// 프로토콜 타입 반환
func protoFlip<T: Shape>(_ shape: T) -> Shape { 
    return FlippedShape(shape: shape) 
}
```
protoFlip 함수는 불명확 타입 반환 예제인 flip과 같은 기능을 하지만 반환 타입이 프로토콜 타입인 함수이며, 언제나 같은 타입의 값을 리턴한다.   
protoFlip 함수는 제약이 없어 항상 같은 타입을 반환하지 않아도 된다. 그저 Shape 프로토콜을 준수하는 타입을 반환하기만 하면 된다.   
때문에 protoFlip은 flip에 비해 함수호출에 대해 좀 더 느슨하며, 다양한 타입들을 반환할 수 있는 유연성을 갖고 있다.   
대신 protoFlip의 반환 타입은 덜 구체적이고 때문에 해당 반환값으로는 타입 정보에 의존하는 많은 작업들을 하기 어렵다.
```
let protoFlippedTriangle = protoFlip(smallTriangle)
let sameThing = protoFlip(smallTriangle)
protoFlippedTriangle == sameThing // error!
```
예를 들어 ==와 같은 연사자를 사용할 수 없다.   
Shape 프로토콜의 요구조건에 == 연사자가 포함되어 있지 않기 때문이다.   
설령 == 연산자를 추가한다쳐도 == 연산자의 왼쪽과 오른쪽에 오는 값들의 각각의 타입을 알아야 한다.   
이러한 상황을 구체적인 타입 정보가 보존되지 않았다는 것인데, 프로토콜 타입을 반환 타입으로 사용했기 때문에 구체적인 타입 정보가 보존되지 않은 것이다.
**즉, 반환 타입이 프로토콜 타입일 경우 해당 프로토콜을 준수하는 모든 타입을 반환할 수 있는 유연성을 얻을 수 있다.   
그러나 유연성을 얻기 위해서는 반환값으로 할 수 있는 몇몇 작업들을 포기해야 한다.**
 
반환 타입이 프로토콜 타입일 경우 발생하는 또 다른 문제는 중첩이 불가능하다는 점이다.   
protoFlip에서 반환된 값은 Shape을 준수하지 않는다고 보기 때문이다.   
반환 타입인 Shape 프로토콜 타입 그 자체는 프로토콜 Shape을 준수하지 않는다.   
즉, **반환 타입이 프로토콜 타입이고 반환값은 해당 프로토콜을 준수하지 않는다**고 보기 때문에 반환값에 해당 프로토콜 타입이 파라미터인 다른 변환을 적용할 수 없다.   
한마디로 `protoFlip(protoFlip(samllTriangle))` 해당 코드는 작성될 수 없는 코드이다.
    
    
반면에 불명확 타입은 프로토콜 타입과는 달리 타입의 아이덴티티를 보존한다. 
```
protocol Generic {
    associcatedtype Item
    var count : Int { get }
    subscript(i: Int) -> Item { get }
}
 
extension Array: Container {  }
```
프로토콜이 연관 타입을 갖고 있기 때문에 Container 프로토콜을 반환 타입으로 사용할 수 없는 상황이다.   
심지어 연관 타입을 함수 본체 외부에서 추정할 수 없기 때문에 제네릭의 제한 조건 `where` 키워드로도 사용할 수 없다.
```
// Error: Protocol with associated types can't be used as a return type.
func makeProtocolContainer<T>(item: T) -> Container {
    return [item]
}
 
// Error: Not enough information to infer C.
func makeProtocolContainer<T, C: Container>(item: T) -> C {
    return [item]
}
```
그러나 만약 반환 타입으로 `some Container`라는 불명확 타입을 사용하면 바람직한 API를 만들 수 있다.   
some Container 값을 
 
#### Reference)
 
[https://wlaxhrl.tistory.com/82](https://wlaxhrl.tistory.com/82)   
[https://soooprmx.com/archives/11092](https://soooprmx.com/archives/11092)
