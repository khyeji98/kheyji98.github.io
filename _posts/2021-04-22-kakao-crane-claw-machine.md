---
comments: true
title: Swift) [2019 카카오 개발자 겨울 인턴십] 크레인 인형뽑기 게임
key: 202104221
modify_date: 2021-04-22
picture_frame: shadow
tags:
  - [Algorithm]
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
 
- `newBoard`
  - 인형을 뽑으면 그 자리의 값을 0으로 변경해야 하기 때문에 값 변경이 가능한 변수를 생성
  - 처음 board 값을 newBoard에 저장하고 인형뽑을 때마다 값 변경
- `basket`
  - 바구니 역할
  - 바구니에서 가장 마지막 인형을 알아야 인형이 터진 인형의 갯수를 구할 수 있기 때문에 생성
- `result`
  - 터진 인형의 갯수를 저장하기 위해 생성
- `pick`
  - 해당 열에 인형이 있는지 확인하고, 있다면 해당 열에서 가장 위에 있는 인형의 종류를 저장하기 위해 생성
- `index`
  - 뽑은 인형이 있는 행의 위치를 저장하기 위해 생성
  - index와 지금 인형을 뽑은 열(i)의 위치에 있는 값을 0으로 변경(인형을 뽑았으므로 해당 위치에는 인형이 없어졌기 때문)
- `last`
  - 바구니에 인형이 있다면, 가장 최근에 담긴 인형의 종류를 저장하기 위해 생성
  - 가장 최근에 담긴 인형의 종류(last)와 지금 뽑은 인형의 종류(pick[i-1])가 같은지 비교
    - 같다면 : last 제거
    - 다르다면 : 바구니에 pick[i-1] 추가
