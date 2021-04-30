---
comments: true
title: Swift) [탐욕법] 체육복
key: 202104301
modify_date: 2021-04-30
picture_frame: shadow
tags:
  - [코딩테스트]
---
 
## 문제설명
 
<img width="629" alt="KakaoTalk_Photo_2021-04-30-21-32-46" src="https://user-images.githubusercontent.com/50580583/116695489-a7152b80-a9fb-11eb-9267-7698a446df12.png">
<img width="627" alt="KakaoTalk_Photo_2021-04-30-21-32-50" src="https://user-images.githubusercontent.com/50580583/116695493-a8465880-a9fb-11eb-9127-4035da338f7c.png">
 
## 코드
 
```
import Foundation
 
func solution(_ n:Int, _ lost:[Int], _ reserve:[Int]) -> Int {
    var newReserve = reserve.filter{!lost.contains($0)}
    let realLost = lost.filter{!reserve.contains($0)}.filter{
        if let front = newReserve.firstIndex(of: $0-1) {
            newReserve.remove(at: front)
        } else if let back = newReserve.firstIndex(of: $0+1) {
            newReserve.remove(at: back)
        } else {
            return true
        }
        return false
    }
    return n - realLost.count
}
```
- `newReserve`
- `realLost`
