---
comments: true
title: Swift ) 스택(Stack)과 큐(Queue)
key: 202103102
modify_date: 2021-03-10
picture_frame: shadow
tags:
  - [자료구조]
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
 
## 큐(Queue)
 
큐는 스택과 반대로 먼저 입력된 데이터가 먼저 출력되는 선입선출, 즉 **FIFO**(First In-First Out) 데이터 구조를 나타낸다.
 
<p style="text-align:center"><img width="656" alt="KakaoTalk_Photo_2021-03-17-11-38-00" src="https://user-images.githubusercontent.com/50580583/111408742-13bcbb00-8719-11eb-87ca-92f068260a03.png"></p>
 
### 메소드 및 프로퍼티
 
- enqueue : 큐의 맨 뒤에 새로운 요소 추가
- dequeue : 큐의 첫 번째 요소를 제거한 뒤 반환
- peek : 큐의 첫 번째 요소를 반환하되 제거하지 않음
- clear : 큐를 비움
- insert : 큐의 특정 인덱스 위치에 요소 삽입
- removeAtIndex : 큐의 특정 인덱스 위치에 있는 요소 제거
- capacity : 큐 용량을 가져오거나 설정하기 위한 read/wirte 프로퍼티
 
### 구현
 
```
public struct Queue<T> {
    private var data = [T]()
    
    public init() {}
    
    public mutating func dequeue() -> T? {
        return data.removeFirst()
    }
    
    public func peek() -> T? {
        return data.first
    }
    
    public mutating func enqueue(_ element: T) {
        data.append(element)
    }
    
    public mutating func clear() {
        data.removeAll()
    }
    
    public var count: Int {
        return data.count
    }
    
    // 큐의 용량 반환
    public var capacity: Int {
        get {
            return data.capacity
        }
        set {
            data.reserveCapacity(newValue)
        }
    }
    
    public func isFull() -> Bool {
        return count == data.capacity
    }
    
    public func isEmpty() -> Bool {
        return data.isEmpty
    }
}
 
var queue = Queue<Int>()
queue.enqueue(3) // [3]
queue.enqueue(2) // [3, 2]
queue.enqueue(1) // [3, 2, 1]
queue.dequeue() // 3
queue.peek() // 2
queue.count // 2 = [2, 1]
```
 
### 더블 스택으로 큐 구현
 
배열의 마지막 요소를 제거하는 연산이 **더블 스택**에서는 필요하지 않기 때문에 수행속도가 더 빠르고 효율적임을 활용한 방법이다.   
 
<p style="text-align:center"><img width="395" alt="KakaoTalk_Photo_2021-03-17-12-15-12" src="https://user-images.githubusercontent.com/50580583/111410975-1ae5c800-871d-11eb-84ca-1be3f7246c20.png"></p>
 
```
public struct DoubleStack<T> {
    private var leftStack = [T]() // 호출 안됨
    private var rightStack = [T]() // 호출 안됨
    
    public init() {}
    
    public mutating func enqueue(_ element: T) {
        rightStack.append(element)
    }
    
    public mutating func dequeue() -> T? {
        if leftStack.isEmpty {
            leftStack = rightStack.reversed()
            rightStack.removeAll()
        }
        return leftStack.popLast()
    }
    
    public var isEmpty: Bool {
        return rightStack.isEmpty && leftStack.isEmpty
    }
    
    public var peek: T? {
        return leftStack.isEmpty ? rightStack.last : leftStack.first
    }
}
 
var doubleStack = DoubleStack<Int>()
doubleStack.enqueue(3) // rightStack = [3], leftStack = []
doubleStack.enqueue(2) // rightStack = [3, 2], leftStack = []
doubleStack.enqueue(1) // rightStack = [3, 2, 1], leftStack = []
doubleStack.dequeue() // rightStack = [], leftStack = [1, 2, 3]
doubleStack.dequeue()
doubleStack.dequeue()
print(doubleStack.isEmpty)
```
 
#### Reference)
 
