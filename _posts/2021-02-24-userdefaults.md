---
comments: true
title: [Swift ) UserDefaults를 통한 데이터 저장]
key: 202102241
modify_date: 2021-02-24
picture_frame: shadow
tags:
  - [swift]
  - [TIL]
---
 
## UserDefaults
 
데이터를 저장하는 방법에는 File, Core Data, Netwarok Server DB 등이 있는데, UserDefaults는 그 중에서 **plist**에 데이터를 저장한다.   
 
UserDefaults에 대해 간단히 설명하자면, **사용자의 정보를 저장하는 싱글톤 인스턴스**로 간단한 사용자 정보를 저장하거나 불러올 수 있다.   
그러나 내부적으로 plist 파일에 저장되기 때문에 보안이 강력하지는 않다.   
 
### 주요 항목
 
```
open calss var standard: UserDefaults { get }
 
// 데이터 불러오기
open func object(forKey defaultName: String) -> Any?
 
open func string(forKey defaultName: String)) -> String?
 

```
