---
comments: true
title: [Swift ) 반복문(for-in/while/repeat-while)]
key: 202004181
modify_date: 2020-04-19
picture_frame: shadow
tags:
  - [swift]
---
 
# 반복문

### 반복문이란?
 
반복문이란 특정 코드를 반복적으로 실행하기 위한 것으로, **for-in**과 **while**이 대표적이다.
 
# for-in
 
for-in 반복문은 일정 횟수만큼 특정 코드를 반복할 수 있는데 먼저 기본 형식부터 보고 자세히 톺아보자.
```
for item in items {
    // 반복 실행할 코드
}
```
item과 items가 감이 잡히지 않을 수 있으니 정말 간단한 예제로 보자.
```
for i in 0..<4 {
    print(i)
}
```
item에는 items 내에서 반복될 원소의 변수를 넣어주고, items에는 기본적으로 반복될 횟수를 범위연산자로 넣어준다.
 
> **범위연산자**
> 
> 범위연사자는 보통 **a...b** 또는 **a..<b**와 같은 형식으로 표현한다.   
> 먼저, a...b는 a부터 b까지의 수를 나타낸 것이고 (a,b 포함)   
> a..<b는 a부터 b-1까지의 수를 나타낸 것이다.(a 포함, b 미포함)
 
 
items에 범위연산자를 넣기도 하지만 실제 프로젝트 상에서 가장 많이 사용되는 것은 배열이다.
```
var num = [1, 2, 3, 4, 5]
 
for i in num {
    print(i)
}
```
이렇게 items에 배열을 넣어준다면 item은 당연히 배열 내 원소를 가리키게 된다.
 
# while
 
while 반복문은 for-in과 다르게 반복 횟수를 특정지을 수는 없지만 조건문을 통해 반복 횟수를 조절할 순 있다.
```
while 조건문 {
    // 반복 실행할 코드
}
```

한마디로, **for-in**은 특정 횟수동안 반복하는 것이고 **while**은 특정 조건이 만족하는 동안 반복되는 점이 다르다.
 
# repeat-while
