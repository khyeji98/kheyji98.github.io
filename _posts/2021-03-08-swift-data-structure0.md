---
comments: true
title: Swift ) 반복기, 시퀀스, 컬렉션
key: 202103081
modify_date: 2021-03-08
picture_frame: shadow
tags:
  - [데이터 구조]
---
 
## 반복기(Iterator)
 
반복기는 `IteratorProtocol` 프로토콜에 부합하는 범용 타입으로, IteratorProtocol 프로토콜의 유일한 목적은 컬렉션을 반복 순회하는 `next()` 메소드를 통해 **컬렉션의 반복 상태를 캡슐화**하는 것이다.
```
public protocol IteratorProtocol  {
    // Iterator로 순회하여 가져온 요소의 타입 
    associatedtype Element

    // 시퀀스에서 다음 요소를 반환하거나, 다음 요소가 없을 경우 nil 반환 
    public mutating func next() -> Self.Element? 
}
```
 
## 시퀀스(Sequence)
 
시퀀스는 `Sequence` 프로토콜에 부합하는 범용 타입으로, `for...in`으로 **반복 순회**할 수 있다.   
한마디로 컬렉션 타입이 포함된 시퀀스 타입의 IteratorProtocol을 반환하는, **팩토리 반복기**로 생각할 수 있다.
```
public protocol Sequence {
    // 시퀀스 순회 인터페이스와 그 순회 상태를 캡슐화하는 타입
    associatedtype Iterator: IteratorProtocol
    
    // for...in 순회할 때 자동으로 호출되는 메소드 : 시퀀스를 순회해서 가져온 요소를 반환
    public func makeIterator() -> Self.Iterator 
}
```
 
## 컬렉션(Collection)
 
컬렉션은 `Collection` 프로토콜에 부합하는 범용 타입으로, **위치를 특정할 수 있는 다중 경로 시퀀스**를 제공한다.   
즉 컬렉션을 순회하면서 요소들을 인덱스 값으로 저장하고, 해당 인덱스 값으로 특정 요소를 가져올 수 있다.

### 컬렉션 프로토콜에 부합하는 타입 정의
 
컬렉션 프로토콜에 부합하는 타입을 만들기 위해서는 다음 4가지를 정의해야 한다.
 
- `startIndex`와 `endIndex` 프로퍼티
- 특정 인덱스 위치에 삽입하기 위한 `index(after:)` 메소드
- 요소에 읽기 전용 이상으로 접근하기 위한 서브스크립트
 
#### Reference)
 
Swift Data Structure and Algorithm | 스위프트 데이터 구조와 알고리즘(프로그래밍의 튼튼한 기초) 책
