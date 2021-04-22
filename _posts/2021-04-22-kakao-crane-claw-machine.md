---
comments: true
title: Swift) [2019 카카오 개발자 겨울 인턴십] 크레인 인형뽑기 게임
key: 202104221
modify_date: 2021-04-22
picture_frame: shadow
tags:
  - [코딩테스트]
---
 
## [2019 카카오 개발자 겨울 인턴십] 크레인 인형뽑기 게임
 
### 문제설명
 
<img width="592" alt="KakaoTalk_Photo_2021-04-22-20-36-55" src="https://user-images.githubusercontent.com/50580583/115708094-88cf8000-a3aa-11eb-9c97-7b12296046f1.png">
<img width="516" alt="KakaoTalk_Photo_2021-04-22-20-36-59" src="https://user-images.githubusercontent.com/50580583/115708109-8c630700-a3aa-11eb-8b67-b488f75ce7dd.png">
<img width="582" alt="KakaoTalk_Photo_2021-04-22-20-37-04" src="https://user-images.githubusercontent.com/50580583/115708115-8d943400-a3aa-11eb-855b-1a0ba348045b.png">
<img width="595" alt="KakaoTalk_Photo_2021-04-22-20-37-07" src="https://user-images.githubusercontent.com/50580583/115708117-8f5df780-a3aa-11eb-84e0-89b091798436.png">
 
### 코드
 
```
import Foundation
 
func solution(_ board:[[Int]], _ moves:[Int]) -> Int {
    var newBoard = board
    var basket = [Int]()
    var result = 0
    
    for i in moves {
        if let pick = newBoard.filter({$0[i-1] != 0}).first, let index = newBoard.firstIndex(of: pick) {
        
            newBoard[index][i-1] = 0
            
            if let last = basket.last, last == pick[i-1] {
                basket.removeLast()
                result += 2
            } else {
                basket.append(pick[i-1])
            }
        }
    }
    return result
}
```
 
 
