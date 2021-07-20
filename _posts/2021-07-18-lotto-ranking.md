---
comments: true
title: Swift) [2021 Dev-Matching] 로또의 최고 순위와 최저 순위
key: 202107181
modify_date: 2021-07-18
picture_frame: shadow
tags:
  - [Algorithm]
---
 
## 문제설명
 
<p style="text-align:center"><img width="631" alt="KakaoTalk_Photo_2021-07-20-22-28-54" src="https://user-images.githubusercontent.com/50580583/126332499-253339c4-3b49-46e6-a994-7572eddae988.png"></p>   
<p style="text-align:center"><img width="631" alt="KakaoTalk_Photo_2021-07-20-22-28-58" src="https://user-images.githubusercontent.com/50580583/126332500-168191af-3313-4ef4-a94d-0ed5ab34026f.png"></p>   
 
## 코드
 
```
func rank(_ count: Int) -> Int {
    switch count {
    case 0, 1: return 6
    case 2: return 5
    case 3: return 4
    case 4: return 3
    case 5: return 2
    case 6: return 1
    default: return 0
    }
}
 
func solution(_ lottos:[Int], _ win_nums:[Int]) -> [Int] {
    let matchCount = lottos.filter{win_nums.contains($0)}.count
    return [rank(matchCount + lottos.filter{$0==0}.count), rank(matchCount)]
}
```
 
#### Reference)
 
[https://programmers.co.kr/learn/courses/30/lessons/77484](https://programmers.co.kr/learn/courses/30/lessons/77484)   
