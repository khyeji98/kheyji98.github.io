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
    
    
아직 각 함수에 대한 자세한 설명은 안했지만, 고차함수의 사용목적과 원리만을 보면 for문과 다를 바 없어보이지만 고차함수의 여러 이점때문에 **for문보다 고차함수의 사용을 권장**하고 있다.   
 
- **코드의 간결성**
- **재사용에 용이함**
- **컴파일러 최적화: 성능 좋음**
 
각 함수들을 for문과 비교해 보면 이 이점들을 더 한눈에 알아볼 수 있을 것이다.
 
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
 
그리고 만약 같은 코드를 map이 아닌 for문을 사용했다면,
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
 
Filter는 데이터를 추출할 때 사용하는데, 기존 데이터에서 **조건에 맞게 내부의 값을 걸러** 새로운 콜렉션으로 반환한다.   
map과 다른 점으로, Filter는 조건을 통해 내부의 값을 거르기 때문에 반드시 **Bool타입을 반환하는 함수를 전달인자로** 넣어야 한다.
```
var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var evenNums = nums.filter{($0 % 2) == 0}
print(evenNums) // [2, 4, 6, 8, 10]
```
예제를 보면 `($0 % 2) == 0`은 2로 나누었을 때가 나머지가 0, 즉 짝수에 해당되는 값만 추출한다는 것이다.   
또한 해당 코드라인을 보면 전달인자인 함수는 Bool 타입을 반환하기 때문에 전달인자로써 알맞다.   
 
물론 Filter 역시,
```
var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
nums = nums.filter{($0 % 2) == 0}
print(nums) // [2, 4, 6, 8, 10]
```
이렇게 원래의 콜렉션에 새로운 값들을 정의할 수 있다.

그리고 map과 마찬가지로 for문과 다를 바 없어 보이겠지만,
```
var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var evenNums = [Int]()

for num in nums {
    if num % 2 == 0 {
        evenNums.append(num)
    }
}

print(evenNums) // [2, 4, 6, 8, 10]
```
이렇게 감결한 filter에 비해 조금 더 복잡해진다.   
아무래도 filter는 조건문이 추가되기 때문에 for문과의 차이가 map보다 더 잘 나타날 것이다.
 
### Reduce
 
Reduce도 데이터를 결합, 즉 합치기 위해 사용된다.   
말 그대로 기존 데이터에서 **내부의 값들을 결합**해 결합된 하나의 새로운 값을 반환하는 것이다.   
```
var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var sumNums = nums.reduce(0) { (first, second) -> Int in
    return first + second
}
print(sumNums)
```
앞서 설명한 map, filter와 다른 점이 있는데, reduce는 초기값을 입력해야 한다.   
여기서 초기값은 `(0)`으로 우리는 초기값없이 순수한 nums의 결합값을 원하기 때문에 0을 입력했다.   
map과 
```
var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var sumNums = nums.reduce(0){$0 + $1}
print(sumNums)
```

reduce를 이렇게 표현할 수도 있지만,
```
var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var sumNums = nums.reduce(0, {$0 + $1})
print(sumNums)
```
이렇게 표현할 수도 있으며,

 
#### Reference)
 
[https://shark-sea.kr/entry/Swift-%EA%B3%A0%EC%B0%A8%ED%95%A8%EC%88%98-Map-Filter-Reduce-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0](https://shark-sea.kr/entry/Swift-%EA%B3%A0%EC%B0%A8%ED%95%A8%EC%88%98-Map-Filter-Reduce-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
