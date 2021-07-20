---
comments: true
title: Swift) [2020 카카오 인턴십] 키패드 누르기
key: 202107051
modify_date: 2021-07-06
picture_frame: shadow
tags:
  - [Algorithm]
---
 
## 문제설명
 
<p style="text-align:center"><img width="634" alt="KakaoTalk_Photo_2021-07-20-22-03-49" src="https://user-images.githubusercontent.com/50580583/126329011-8d4df6ad-d808-4cce-827e-21478f6bc0c9.png"></p>   
<p style="text-align:center"><img width="628" alt="KakaoTalk_Photo_2021-07-20-22-03-53" src="https://user-images.githubusercontent.com/50580583/126329018-074340fe-3e91-4e71-92a5-7baa53046740.png"></p>   
 
## 코드
 
```
func solution(_ numbers:[Int], _ hand:String) -> String {
    var result = ""
    var tap = ""
    var leftHand = 10
    var rightHand = 12
    
    numbers.forEach{
        var num = $0 == 0 ? 11 : $0
        switch num {
            case 1, 4, 7:
                tap = "L"
            case 3, 6, 9:
                tap = "R"
            case 2, 5, 8, 11:
                let leftGap = (leftHand - num).magnitude
                let rightGap = (rightHand - num).magnitude
                let leftDistance = (leftGap/3) + (leftGap%3)
                let rightDistance = (rightGap/3) + (rightGap%3)
                if leftDistance == rightDistance {
                    tap = hand == "left" ? "L" : "R"
                } else {
                    tap = leftDistance > rightDistance ? "R" : "L"
                }
            default: break
        }
        result += tap
        if tap == "L" {
            leftHand = num
        } else if tap == "R" {
            rightHand = num
        }
    }
    return result
}
```
 
- *은 10, 0은 11, #은 12로 가정하고, 풀이.   
 
#### Reference)
 
[https://programmers.co.kr/learn/courses/30/lessons/67256](https://programmers.co.kr/learn/courses/30/lessons/67256)   
 
