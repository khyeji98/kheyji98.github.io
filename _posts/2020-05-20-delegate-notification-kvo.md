---
comments: true
title: Swift ) Delegate, Notification, KVO 정리
key: 202005201
modify_date: 2020-05-20
picture_frame: shadow
tags:
  - [swift]
---
 
세 패턴 모두 특정 이벤트가 A에서 일어나면 B에 알려주는 패턴으로, 특히 Delegate와 Notification은 우리가 흔히 접하거나 구현해봤던 패턴이다.   
그러나 세 패턴을 언제, 어디서, 무엇을 위해 사용하면 좋을지에 대해서는 제대로 모르기 때문에 제대로 알고 넘어가고자 한다.   
 
## Delegate
 
Delegate는 보통 **Protocol**을 이용하는데, Protocol이란 **일종의 기능 명세서**로 Delegate로 지정된 객체가 실행해야 하는 메소드들을 "정의만" 한다.
 
```
// 1. 프로토콜 선언
protocol SomeProtocol: AnyObject {
    func someFunction(_ someProperty: String)
}
 
// 2. delegate 프로퍼티 생성
class SomeView: UIView {
    // 순환 참조를 막기 위해 weak var로 선언해야 한다
    weak var delegate: SomeProtocol?
 
// 3. delegate가 동작할 부분에서 메소드 호출
    @IBActioin func someBtnClicked(_ sender: UIButton) {
        self.delegate?.someFunction("clicked")
    }
}
 
class SomeViewController: UIViewController {
    var someView: SomeView?
    
    init() {
        self.view = SomeView()
        
// 4. delegate를 대신 실행할 곳이 어딘지 알려주기
        self.view?.delegate = self
    }
}
 
// 5. delegate를 대신 실행할 곳에서 프로토콜 준수하기
extension SomeViewController: SomeProtocol {
    func someFunction(_ someProperty: String) {
        print(someProperty)
    }
}
```
이렇게 구현되어 있을 경우, 만약 SomeView에서 `someBtnClicked()`에 연결되어 있는 버튼을 클릭한다면 "clicked"라고 출력될 것이다.   
 
#### 참고 : [Delegate Pattern](https://khyeji98.github.io/post/2020/05/01/delegate-pattern.html)
 
## Notification

## KVO
 

 
#### 참고 : [KVO](https://khyeji98.github.io/post/2020/05/14/kvo.html)
 
## 장단점
 
### Delegate

### Notification

### KVO
 
#### Reference)
 
