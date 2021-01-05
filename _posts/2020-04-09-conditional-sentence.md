---
comments: true
title: [Swift ) 조건문(if-else/switch)]
key: 202004091
modify_date: 2020-06-01
picture_frame: shadow
tags:
  - [swift]
---
 
# 조건문
 
### 조건문이란?
 
조건문은 조건에 따라 코드의 실행 여부를 판단하는 문장이다.
 
# if-else
 
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
if-else 조건문은
ㅑㄹ
 

 
# guard
 
```
guard 조건문 else {
    // 조건문이 false라면 실행
}
```
 
# switch
 
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
 
그리고 `,`를 통해 여러 값을 하나의 케이스로 처리할 수 있다.
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
 
# #available
 
