---
comments: true
title: Swift ) 스택(Stack)
key: 202103101
modify_date: 2021-03-10
picture_frame: shadow
tags:
  - [데이터 구조]
---
 
## 스택(Stack)
 
스택은 나중에 입력된 것이 먼저 출력되는 후입선출 즉, **LIFO**(Last In-First Out) 데이터 구조를 나타낸다.   
개별 요소에 무작위 접근을 허용하는 배열과는 달리, 스택은 개별 요소에 접근하는 방법을 강하게 제한한 인터페이스를 제공한다.   
iOS 프로그래밍에서는 주로 Navigation Controller에서 스택을 사용한다.   
 
<p style="text-align:center"><img width="437" alt="KakaoTalk_Photo_2021-03-17-11-17-13" src="https://user-images.githubusercontent.com/50580583/111404602-634bb880-8712-11eb-941c-a6b0aeb46cc2.png"></p>
 
### 메소드
 
- push : 스택의 맨 위에 데이터를 쌓는다.
- pop : 스택의 맨 위에 있는 데이터를 빼낸다.
 
### 구현
 
```
public struct Stack<T> {
    private var elements = [T]()
    
    public init() {}
    
    public mutating func pop() -> T? {
        return self.elements.popLast() // 맨 위의 요소를 반환하고 삭제
    }
    
    public mutating func push(_ element: T) {
        self.elements.append(element)
    }
    
    public func peek() -> T? {
        return self.elements.last // 맨 위의 요소를 반환(삭제하지 않음)
    }
    
    public var isEmpty: Bool {
        return self.elements.isEmpty
    }
    
    public var count: Int {
        return self.elements.count
    }
}
```
이렇게 스택을 구현하고 직접 실행을 해봤더니
```
var myStack = Stack<Int>()
myStack.push(5) // [5]
myStack.push(4) // [5, 4]
myStack.push(3) // [5, 4, 3]
myStack.push(2) // [5, 4, 3, 2]
myStack.push(1) // [5, 4, 3, 2, 1]
myStack.pop() // 1
myStack.pop() // 2
myStack.pop() // 3
```
정말 `pop()` 메소드를 호출했을 때 가장 마지막에 추가한 요소부터 반환되는 것을 확인할 수 있었다.

#### Reference)
 
