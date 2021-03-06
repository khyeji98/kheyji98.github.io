---
comments: true
title: Swift ) 조건문(if-else, guard, switch, #available)
key: 202001121
modify_date: 2020-06-01
picture_frame: shadow
tags:
  - [swift]
---
 
## 조건문이란?
 
조건문은 조건에 따라 코드의 실행 여부를 판단하는 문장이다.
 
## if-else
 
조건의 참과 거짓을 판단하고 실행 여부를 결정하는데 if 블럭에서 구현한 코드는 **조건문이 true**인 경우에만 실행된다.
```
if 조건문 {
    // 조건문이 true라면 실행
} else {
    // 조건문이 false라면 실행
}
```
조건문은 항상 Bool 타입을 반환해야 하며 연사자도 사용 가능하고, 변수 자체가 Bool 타입이라면 그냥 변수만 와도 된다.
```
var some = false
 
if some {
    // some이 true라면 실행
} else {
    // some이 false라면 실행
}
```
물론 조건문을 두 개 이상 줄 수도 있다.
```
if 조건문1 {
    // 조건문1이 true라면 실행
} else if 조건문2 {
    // 조건문1은 false고 조건문2가 true라면 실행
} else {
    // 조건문1과 2가 모두 false라면 실행
}
```
if-else 조건문은 위에서부터 차례대로 조건을 판단하기 때문에 원하는 결과와 효율을 위해서 **가장 까다로운 조건**을 먼저 처리하는 것이 좋다.   
 
또한 내가 가장 고민하는 부분인데, if-else 블록 안에 if-else 블록을 추가하게 되면 코드가 계속 안쪽으로 파고드는 "**피라미드 오브 둠(pyramid of doom)**" 현상을 띄게 될 수 있어 주의해야 한다. 차선의 해결법으로는 guard나 switch 같은 다른 조건문을 사용할 수 있는지 확인해보는 것이다.
 
### 삼항연산자
 
삼항연산자는 true/false로만 구분되는 if-else 조건문을 **한줄로** 간단하게 줄일 수 있는 방법이다.
```
var some = false
 
if some {
    print("some은 true입니다")
} else {
    print("some은 false입니다")
}
```
이 if-else 조건문을 삼항연산자로 줄여보자면,
```
var some = false
 
some ? print("some은 true입니다") : print("some은 false입니다") // "some은 false입니다"
```
이렇게 조건문 뒤에 물음표(?)를 붙이고 `true일 때 실행할 코드 : false일 때 실행할 코드`를 붙여주면 **삼항연산자**가 된다.   
간단한 코드라면 이렇게 여러줄을 한줄로 줄여 메모리를 줄이는 것도 효율적인 코드 작성이라고 볼 수 있다.
  
### guard
 
조건문으로는 주로 if-else가 많이 사용되지만 옵셔널 바인딩용으로만 알고 있던 guard도 조건문에 속한다.
 
 
guard 조건문과 if-else 조건문의 차이점은, guard 조건문은 else가 꼭 필요하고 조건문이 true일 때 실행할 코드가 없다는 것이다.
```
guard 조건문 else {
    // 조건문이 false라면 실행
}
```
guard 조건문은 후속 코드가 실행되기 전 조건에 만족하는지 확인하는 절차용으로 사용되어, 주로 차후 에러를 막기 위해 특정 조건을 만족하는지 확인하기 위해 사용된다.
 
또다른 장점으로는, 중첩 코드를 막을 수 있어 if-else의 피라미드 오브 둠과 같은 현상을 방지할 수 있고 때문에 guard 조건문을 많이 사용해도 코드의 깊이가 deep해지지 않는다.
그러나 실전에서는 if-else를 많이 사용하며 guard는 옵셔널 바인딩 때 많이 사용된다.
 
## switch
 
switch문은 하나의 값을 통해 값이 케이스와 일치하면 해당 구문이 실행된다.
```
switch 비교값 {
case 케이스1:
    // 비교값이 케이스1과 일치하면 실행
case 케이스2:
    // 비교값이 패턴2와 일치하면 실행
...
default:
    // 비교값과 일치하는 케이스가 없을 때 실행
}
```
케이스마다 실행될 코드가 반드시 입력되어 있어야 하며, default도 반드시 있어야 한다.   
명시적으로 `break`를 해주지 않아도 알아서 break가 작동된다.
 
그리고 쉼표(,)를 통해 여러 값을 하나의 케이스로 처리할 수 있다.
```
switch 비교값 {
case 케이스1, 케이스2, 케이스3:
    // 비교값이 케이스1이나 2나 3과 일치하면 실행
case 케이스4:
    // 비교값이 케이스4와 일치하면 실행
default:
    // 비교값과 일치하는 케이스가 없을 때 실행
}
```
 
> 참고로 비교값을 튜플로 넣어주면 케이스도 튜플로 넣어줘야 한다.
 
## #available
 
*이건 프로젝트 진행할 때 종종 쓰이는 조건문인데 알아두면 매우 유용하기 때문에 미리 공부해 두는 것이 좋다.*
 
iOS 버전에 따라 API를 제공하는 경우 앱 자체에서 제한을 두거나 다른 API를 사용하도록 분기두는 경우 사용하는 조건문이다.
```
if #available(플랫폼 이름과 버전, *) {
    // 해당 버전부터 실행될 코드
} else {
    // 해당 버전보다 낮은 버전일 때 실행될 코드
}
```
#available은 조건에 맞는지 판단하는 것이 아닌 **해당 버전을 포함한 그 이상의 버전**인지를 확인하는 것이다.
물론 조건에 넣을 플랫폼 이름과 버전은 쉼표(,)를 통해 여러개를 나열해 넣을 수 있다.
 
### @available
 
@available은 함수(메소드), 클래스, 프로토콜 앞에 놓이는 조건문으로, 타입 또는 프로토콜이 적용되는 플랫폼/OS를 나타낸다.
deployment target과 관련있어 #available과 다르게 컴파일타임에 에러 또는 경고를 띄운다.
```
@available(iOS 12, *)
```
이런 조건문이 앞에 붙은 함수, 클래스, 프로토콜은 iOS 12를 포함한 그 이상의 버전에서만 사용할 수 있다.   
 
**🔔버전에 관련된 조건문 키워드는 [zedd님 포스팅](https://zeddios.tistory.com/647)을 통해 더 알아볼 수 있다.**   
 
#### Reference)
[https://zeddios.tistory.com/647](https://zeddios.tistory.com/647)
