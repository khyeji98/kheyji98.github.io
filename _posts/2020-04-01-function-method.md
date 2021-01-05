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
 
그렇다면 알고리즘 코드리뷰할 때는 함수라고 해야할까, 메소드라고 해야할까?   
Command Line Tool에서는 클래스를 만들 일이 드물기 적기 때문에 함수라고 많이들 얘기했던 것이다. 고로 상황에 따라 함수, 메소드를 사용하는 것이 아닌 그 차이를 명확히 알고 써야할 것!!   
 
그렇다면 이제 함수와 메소드의 차이도 명확히 알았으니 둘에 대해 더 자세히 알아보자.
 
# Function
 


# Method


