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

 
#### Reference)
