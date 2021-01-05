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
파라미터를 보면 `_ data: String`으로 되어 있는데 여기서 _ 는 함수를 호출할 때 넘기는 파라미터 앞에 라벨, 즉 **파라미터명을 생략**하기 위해 사용되는 것으로 정식명칭은 underscore라고 한다.
 
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
 


# Method


