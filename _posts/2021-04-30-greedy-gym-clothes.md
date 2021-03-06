---
comments: true
title: Swift) [탐욕법] 체육복
key: 202104301
modify_date: 2021-04-30
picture_frame: shadow
tags:
  - [Algorithm]
---
 
## 문제설명
 
<img width="629" alt="KakaoTalk_Photo_2021-04-30-21-32-46" src="https://user-images.githubusercontent.com/50580583/116695489-a7152b80-a9fb-11eb-9267-7698a446df12.png">
<img width="627" alt="KakaoTalk_Photo_2021-04-30-21-32-50" src="https://user-images.githubusercontent.com/50580583/116695493-a8465880-a9fb-11eb-9127-4035da338f7c.png">
 
## 코드
 
```
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
  - 체육복을 빌려줄 수 있는 학생이 계속해서 변동되므로, `reserve`의 값을 초기값으로 한 변수
  - 계속해서 변동되는 값 할당
- `realLost`
  - 마지막까지 체육복을 빌리지 못한 학생들을 저장하는 변수
  - `solution()`에서 반환할 값
 
