---
comments: true
title: Collection Types
key: 202003301
modify_date: 2020-03-30
picture_frame: shadow
tags:
  - swift
---

# Collection Types

Swift Collection Types엔 Array, Set, Dictionary가 있는데 주로 Array, Dictionary를 사용한다.   
Array는 순서가 정해져 있으나, Dictionary는 순서가 정해져 있지 않아 key로 값을 찾는다.

> 개발할 때 Swift 컬렉션 사용은 타입을 정확하게 명시하거나 타입 추론을 통해 타입이 명확하다.   
> 타입을 명확하게 명시할 경우, 맞지 않은 타입을 빠르게 찾을 수 있다.

***

## Array
- Array는 `Array<Type>`으로 작성하거나, 간단하게 `[Type]`으로 작성해 타입 추론할 수 있다.
```swift
var food: Array<String> = ["pizza", "chicken", "apple"]
var food = ["pizza", "chicken", "apple"]
```
- 배열에 차례대로 원소를 추가할 수 있으며, 특정 index에 원소를 추가하거나 제거할 수 있다.
```swift
food.append("hamburger") // 배열 끝에 추가
food.insert("pasta", atIndex: 1) // 특정 index에 추가
food.remove(at: 0) // 특정 원소 제거
```
- 배열 내 원소개수를 파악하거나 배열이 비어있는지 확인할 수 있다.
```swift
print(food.count) // 4
print(food.isEmpty) // false
```
- 이 외에도 수많은 메서드나 방법을 통해 배열을 다룰 수 있다.
```swift
food[1...2] = ["sushi", "noodle"]
print(food[0...2]) // ["pasta", "sushi", "noodle"]
print(food.sorted()) // ["hamburger", "noodle", "pasta", "sushi"]
print(food.sorted(by: >)) // ["sushi", "pasta", "noodle", "hamburger"]
for integer in food {
    print(integer)
} // pizza chicken apple hamberger
```
빈 Dictionary를 선언하는 유형은 다양하다.
```swift
var anyArray: Array<Any> = Array<Any>()
var anyArray: Array<Any> = [Any]()
var anyArray = [Any]() // Array로 자동 인식
var anyArray: [Any] = []
```

## Dictionary
- Dictionary는 `Dictionary<keyType, valueType>`로 작성하거나, 간단하게 `[keyType:valueType]`로 작성할 수 있다.   
- keyType은 딕셔너리의 key로 사용될 타입이고, valueType은 딕셔너리의 value로 사용될 타입이다.
```swift
var people: Dictionary<String, Int> = ["john":25, "anne": 20,  "chris": 33]
var people = ["john":25, "anne": 20,  "chris": 33]
```
- 특정 key값으로 value값을 찾을 수 있으며, 특정 key값으로 바로 원소를 추가하거나 value값을 수정할 수 있다.
```swift
print(people["anne"]) // 20
people.updateValue(27, forKey: "bob") // 추가
people.updateValue(22, forKey: "anne") // 수정   

// 간단하게 추가 및 수정   
people["hyeji"] = 23 // 추가
people["bob"] = 40 // 수정
```
빈 Dictionary를 선언하는 유형은 다양하다.
```swift
var anyDictionary: Dictionary<String,Any> = [String: Any]()
var anyDictionary: Dictionary <String,Any> = Dictionary<String, Any>()
var anyDictionary: Dictionary <String,Any> = [:]
var anyDictionary: [String:Any] = Dictionary<String, Any>()
var anyDictionary: [String:Any] = [String: Any]()
var anyDictionary: [String:Any] = [:]
var anyDictionary = [String:Any]()
```

**Swift의 모든 타입(String, Int, Double, Bool)은 기본적으로 hashable하며, 이 모든 타입은 딕셔너리 키로 사용된다.**   
즉, 나만의 타입을 딕셔너리에 넣어 사용하고 싶다면 Swift 표준 라이브러리로부터 Hashable 프로토콜을 만들어 따라야 한다.
