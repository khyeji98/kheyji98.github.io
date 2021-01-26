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
 
## 에러 처리
 
스위프트에는 에러를 처리하는 4가지 방법이 있다.
 
- 함수, 메소드, 
- do-catch를 통해 에러 처리
- 에러를 선택적 값으로 처리
- 에러가 발생하지 않은 것이라고 주장
 
### throw
 
throw는 말 그대로 에러를 던진다는 것을 의미하는데, 에러가 발생하면 그대로 발생한 에러를 던지고 함수 실행은 그대로 종료한다.
```
func canThrowErrors() throws -> String
```
이렇게 
 
### do-catch

### assert/assertionfailure

### precondition/preconditionfailure

### fetal error
 
#### Reference)
 
[https://gwangyonglee.tistory.com/52](https://gwangyonglee.tistory.com/52)
