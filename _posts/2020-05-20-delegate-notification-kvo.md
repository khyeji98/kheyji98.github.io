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
 
***
 
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
 
#### 참고 : [https://khyeji98.github.io/post/2020/05/01/delegate-pattern.html](https://khyeji98.github.io/post/2020/05/01/delegate-pattern.html)
 
## Notification
 
Notification은 이벤트 발생 여부를 `NotificationCenter`라는 **싱글턴 객체**를 통해서 옵저버를 등록한 객체들에게 post하는데, `Notification Name`이라는 key 값을 통해 보내고 받을 수 있다.   
 
```
// 1. Notification(이벤트 발생 여부)을 보내는 ViewController
class SomeViewController: UIViewController {
    @IBOutlet weak var someBtn: UIButton!
    
    @IBAction func someBtnClicked(_ sender: UIButton) {
        guard let backgroundColor = self.view.backgroundColor else { return }
        
        // Notification에 object와 dictionary 형태의 userInfo를 같이 실어서 보낸다.
        NotificationCenter.default.post(name: Notification.Name("notification"), object: self.someBtn, userInfo: ["backgroundColor": backgroundColor])
    }
}
 
// 2. Notification을 받는 ViewController
class OtherViewController: UIViewController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 옵저버 추가
        NotificationCenter.default.addObserver(self, selector: #selector(receiveNotification(noti:)), name: Notification.Name("notification"), object: nil)
    }
    
    deinit {
        NotificationCenter.default.removeObserver(self)
    }
    
    @objc func receiveNotification(noti: Notification) {
        // Notification으로 받은 object와 userInfo
        guard let object = noti.object as? UIButton else { return }
        print(object.titleLabel?.text ?? "empty")
        
        guard let userInfo = noti.userInfo as? [String:UIColor], let backgroundColor = userInfo["backgroundColor"] else { return }
        print(backgroundColor)
    }
}
```
 
## KVO
 
KVO는 A 객체에서 B 객체의 프로퍼티가 변화됨을 감지할 수 있는 패턴으로, Delegate와 Notification이 주로 Controller와 다른 객체 사이의 관계를 다룬다면 KVO는 **객체와 객체 사이의 관계**를 다루는데에 적합하다.   
메소드나 다른 액션에 의한 이벤트에 발생하는 것이 아닌, **프로퍼티의 상태에 따라** 발생하는 패턴이다.   
 
#### 참고 : [https://khyeji98.github.io/post/2020/05/14/kvo.html](https://khyeji98.github.io/post/2020/05/14/kvo.html)
 
## 장단점
 
### Delegate
 
- **장점**
  - 프로토콜에 필요한 메소드들이 명확하게 명시됨
  - 컴파일 시 프로토콜의 구현되지 않은 메소드가 있다면 알려줌
  - 로직의 흐름을 따라가기 쉬움
  - 프로토콜 메소드로 이벤트 발생을 알려주는 것 뿐만 아니라 정보도 받을 수 있음
  - 커뮤니케이션 과정을 유지하고 모니터링하는 제 3의 객체가 필요없음  *ex) NotificationCenter*
- **단점**
  - 많은 코드 라인 필요
  - delegate 설정에 nil이 할당되지 않게 주의해야함(만약 delegate에 nil이 할당된다면 crash를 일으킬 수 있음)
  - 순환 참조를 조심해야 함
  - 많은 객체들에게 이벤트 발생을 알려주는 것이 어렵고 비효율적임
 
### Notification
 
- **장점**
  - 많은 코드 라인이 필요없이 구현 가능
  - 다수의 객체들에게 동시에 이벤트 발생을 알릴 수 있음
  - Notification 관련 정보를 `Any?` 타입의 `object`, `[AnyHashable:Any]?` 타입의 `userInfo`로 전달할 수 있음
- **단점**
  - key 값으로 `Notification Name`과 `userInfo`를 서로 맞추기 때문에 컴파일시 Notification이 정상 작동하는지 확인 불가
  - 추적이 쉽지 않을 수 있음
  - post 이후 정보를 받을 수 없음
 
### KVO
 
- **장점**
  - 두 객체 사이의 정보를 맞춰주는 것이 쉬움
  - new/old value를 쉽게 얻을 수 있음
  - key path로 옵저빙하기 때문에 nested objects도 옵저빙할 수 있음
- **단점**
  - `NSObject`를 상속받는 객체에서만 사용 가능
  - `dealloc`될 때 옵저버를 지워야 함
  - 많은 value를 감지할 때는 많은 조건문 필요
  
### 언제? 무엇을?
 
만약 커스텀 객체의 프로퍼티에 KVO 패턴을 적용시킬 것이라면 `didSet`이나 `willSet`으로 대체가 가능하지만, 다른 사람이 구성한 모듈의 프로퍼티는 코드 수정을 최대한 피해야 하기 때문에 KVO가 더 적합하다.   
**즉, KVO는 다른 사람이 구성한 모듈의 프로퍼티의 상태 변화를 감시할 때 적합하다.**
 
Delegate와 Notification은 언제 사용해야 할지 명확하게 답을 낼 수 없지만, **Delegate가 Notification보다 추적에 용이하기 때문에 더 권장하고 많이 사용하는 편이다.**   
 
그러나 **하나의 이벤트로 인해 많은 뷰들이 업데이트되어야 한다면 Notification이 적합할 것이다.**
 
***
 
- **Delegate** : 추적에 용이하므로 주로 사용
- **Notification** : 하나의 이벤트로 인해 많은 뷰나 객체가 업데이트되어야 할 때 사용
- **KVO** : 커스텀 프로퍼티에도 사용 가능하나, 다른 사람이 구성한 모듈의 프로퍼티 상태를 감시해야할 때 사용
 
#### Reference)
 
[https://wnstkdyu.github.io/2018/01/19/threepattern/](https://wnstkdyu.github.io/2018/01/19/threepattern/)
