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
예를 들어 우리가 배열에서 특정 원소를 불러올 때 `array[0]` 이렇게 배열의 index를 통해 값을 가져올 수 있는데, 이 때 `[0]` 이렇게 부를 수 있도록 정의하는 것을 **서브스크립트**라고 한다.   
물론 해당 
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
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
 
let threeTimesTable = TimesTable(multiplier: 3)
print(threeTimesTable[6]) // 18
```

 
#### Reference)
 
[https://velog.io/@zooneon/Swift-%EC%84%9C%EB%B8%8C%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90](https://velog.io/@zooneon/Swift-%EC%84%9C%EB%B8%8C%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)   
[https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-subscript-2288551588f9](https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-subscript-2288551588f9)
