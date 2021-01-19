---
comments: true
title: [Swift ) 고차함수(Map, Filter, Reduce)]
key: 202003121
modify_date: 2020-09-20
picture_frame: shadow
tags:
  - [swift]
---

# 고차함수
 
### 고차함수란?
 
**고차함수**는 함수를 전달인자(파라미터)로 받거나 함수를 결과로 반환하는 함수를 말한다.   
스위프트에서 함수는 1급시민이기에 다른 함수를 인자로 받거나 반환할 수 있다고 한다.   
 
또한 고차함수는 함수의 내부코드를 건드리지 않고 외부에서 실행흐름을 추가할 수 있어 **함수의 재활용성, 재사용성**의 이점을 얻을 수 있다.   
고차함수에는 **Map, Filter, Reduce**가 있다.
 
### Map
 
Map은 데이터를 변형할 때 사용하는데, **기존 데이터를 변형**하여 새로운 콜렉션을 생성하는 함수로 **배열 내부 원소를 하나씩 mapping한다**고 할 수 있다.   
각 요소의 값을 변경하거나 해당 결과들을 새로운 배열로 반환하고자 할 때 사용한다.
```
var nums = [1, 2, 3, 4, 5]
var newNums = nums.map{$0 + 1}
print(newNums) // [2, 3, 4, 5, 6]
```
map의 클로저는 주로 매개변수, 반환타입, 반환키워드 등을 최대한 축약시킨 **후행 클로저**로 사용한다.   
 
> 클로저의 축약에 대한 자세한 내용은 [클로저 포스팅](https://khyeji98.github.io/post/2020/02/07/closure.html)을 통해 볼 수 있다.
 
map을 통해 nums라는 배열 내 각각의 원소에 **순차적으로** 접근하여 $0에 순차적으로 받고, 1씩을 더한 원소들을 newNums라는 새로운 배열에 정의한 것이다.
```
var nums = [1, 2, 3, 4, 5]
nums = nums.map{$0 + 1}
print(nums) // [2, 3, 4, 5, 6]
```
물론 이렇게 새로운 콜렉션에 정의할 필요없이 mapping된 원소들을 원래 배열에 새로 정의해도 된다.
    
    
Map의 사용목적과 원리만을 보면 for문과 다를 바 없어보이지만 map의 여러 이점때문에 for문보다 map의 사용을 권장하고 있다.   
 
- **코드의 간결성**
- **재사용에 용이함**
- **컴파일러 최적화: 성능 좋음**
 
만약 같은 코드를 map이 아닌 for문을 사용했다면,
```
var nums = [1, 2, 3, 4, 5]
var newNums = [Int]()

for num in nums {
    newNums.append(num + 1)
}

print(newNums)
```
매우 간단한 예제임에도 불구하고 코드라인의 수가 차이난다.   
물론 더 복잡하고 다양한 조건들이 추가되면 둘의 차이가 현저하게 느껴질 것이다.
 
### Filter
 
Filter는 데이터를 추출할 때 사용하는데, 기존 데이터에서 조건에 맞게 내부의 값을 걸러 새로운 콜렉션으로 반환한다.   
Filter 역시 
 
### Reduce

#### Reference)
 
[https://shark-sea.kr/entry/Swift-%EA%B3%A0%EC%B0%A8%ED%95%A8%EC%88%98-Map-Filter-Reduce-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0](https://shark-sea.kr/entry/Swift-%EA%B3%A0%EC%B0%A8%ED%95%A8%EC%88%98-Map-Filter-Reduce-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
