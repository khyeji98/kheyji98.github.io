---
comments: true
title: [Swift ) 서브스크립트(Subscript)]
key: 202003241
modify_date: 2020-03-24
picture_frame: shadow
tags:
  - [swift]
---
 
# 서브스크립트(Subscript)
 
### 서브스크립트란?
 
서브스크립트는 콜렉션, 리스트, 시퀀스 타입의 개별 요소에 접근할 수 있는 지름길을 제공한다.   
추가적인 메소드없이 특정 값을 할당하거나 가져올 수 있기 때문에 지름길이라고 비유한 것이다.   
간단히 말해 우리가 배열에서 특정 원소를 불러올 때 `array[0]` 이렇게 배열의 index를 통해 값을 가져올 수 있는데, 이 때 `[0]` 이렇게 부를 수 있도록 정의하는 것을 **서브스크립트**라고 한다.
```
subscript(index: Int) -> Int {
	get {
		// 서브스크립트를 통해 반환
	}
	
	set(newValue) {
		// 서브스크립트를 통해 값 할당
	}
}
```
서브스크립트 역시 get, set 모두 가능하거나 get-only일 수 있는데, 서브스크립트를 정의하는 코드는 당연히 각 타입 body 또는 extension 내에 위치해야 한다.
```
struct TimesTable { // 구구단!
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index 
        // 서브스크립트에 입력하는 정수만큼 곱하는 것.
        // set 없이 읽기 전용
    }
}
let threeTimesTable = TimesTable(multiplier: 3) // 구구단 3단
print("six times three is \(threeTimesTable[6])") // 서브스크립트에 [6] 입력됬으니 3*6 해서 18출력됩니다.
```
 
#### Reference)
 
