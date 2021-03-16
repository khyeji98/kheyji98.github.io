---
comments: true
title: Swift ) 반복문(for-in, while, repeat-while)
key: 202001181
modify_date: 2020-04-19
picture_frame: shadow
tags:
  - [swift]
---
 
## 반복문이란?
 
반복문이란 특정 코드를 반복적으로 실행하기 위한 것으로, **for-in**과 **while**이 대표적이다.
 
## for-in
 
for-in 반복문은 일정 횟수만큼 특정 코드를 반복(순회)할 수 있는데,
```
for item in items {
    // 반복 실행할 코드
}
```
item은 순회하는 상수(변수)를 뜻하고 items는 순회하는 대상을 뜻한다.   
순회대상으로는 범위를 나타내는 데이터 또는 순서가 있는 집단 자료형 데이터가 올 수 있다.
```
for i in 0..<4 {
    print(i)
} // 0 1 2 3
```
순회대상에 범위를 나타내는 데이터가 올 경우 **범위연산자**로 표현한다.
 
> **범위연산자**
> 
> 범위연사자는 보통 **a...b** 또는 **a..<b**와 같은 형식으로 표현한다.   
> - a...b : a부터 b까지의 수 (a,b 포함)   
> - a..<b : a부터 b-1까지의 수 (a 포함, b 미포함)
 
 
items에 범위를 나타내는 데이터가 오기도 하지만 프로젝트 상에서는 주로 순서가 있는 집단 자료형 데이터를 사용한다.   
집단 자료형 데이터로는 **배열(Array), 딕셔너리(Dictionary), 집합(Set), 문자열**이 해당된다.
```
var num = [1, 2, 3, 4, 5]
 
for i in num {
    print(i)
} // 1 2 3 4 5
```
집단 자료형 데이터에 문자열이 왜 있을까?   
문자열도 Character 타입의 데이터들이 모여있는 집단 자료형 데이터이기 때문에 순회대상에 해당된다.
```
var str = "string"
 
for i in str {
    print(i)
} // s t r i n g
```
문자열 자체를 순회대상에 넣으면 Character 타입으로 반환된다.
 
## while
 
while 반복문은 for-in과 다르게 반복 횟수를 특정지을 수는 없지만 조건문을 통해 반복 횟수를 조절할 순 있다.
```
while 조건문 {
    // 반복 실행할 코드
}
```
"조건문으로 어떻게 반복문이 가능하냐"라고 생각할 수 있는데 변수의 값을 계속해서 바꿔주면 코드가 반복된다.
```
var num = 0
 
while num <= 5 {
    num += 1
}
 
print(num) // 6
```
반복문은 주로 for-in을 사용하는 편이지만 while이 필요한 상황이 있다.   
바로, **실행 횟수가 명확하지 않은 경우, 실행 횟수 기반으로 순회할 수 없는 경우**   
 
한마디로, **for-in**은 특정 횟수동안 순회하고 싶을 때 사용하는 것이고 **while**은 특정 조건이 만족하는 동안 순회하고 싶을 때 사용하는 것이다.
 
## repeat-while
 
가물가물하지만 처음 프로그래밍 언어로 C++을 배울 때 배웠던 do-while과 비슷한 구문이 swift에서 repeat-while 구문인 것 같다.   
 
repeat-while도 while을 사용하는 것을 보니 조건문을 기반으로 순회하는 반복문인데, while과 다른점은 조건문이 false일 때에도 최소 한번의 코드 실행이 있다는 점이다.
```
var num = 0
 
while num < 0 {
    num += 1
}
print(num) // 0
```
while 반복문이었을 때는 `num += 1`이 한번도 실행되지 않았다.
```
var num = 0

repeat {
    num += 1
} while ( num < 0)

print(num) // 1
```
그러나 repeat-while 반복문일 때는 조건문 결과가 false임에도 `num += 1`이 한번 실행되었다.
즉, repeat-while은 **적어도 한번은 꼭** 실행해야 하는 경우에 사용하는 것이다.
 
#### Reference)
 
[https://duwjdtn11.tistory.com/460](https://duwjdtn11.tistory.com/460)
