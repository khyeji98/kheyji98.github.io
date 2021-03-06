---
comments: true
title: Swift ) Delegate Pattern
key: 202005011
modify_date: 2020-05-01
picture_frame: shadow
tags:
  - [swift]
---
 
## Delegate Pattern
 
Delegate Pattern은 디자인 패턴 중 하나로, 어떤 객체의 행동을 대신할 수 있도록 **권한을 위임**하는 패턴이다.   
우리가 흔히 볼 수 있는 UITableViewDelegate와 UICollectionViewDelegate를 보면 알 수 있듯이, 위임받는 대리자가 위임받고자 하는 프로토콜을 채택하는 방식으로 위임한다.
 
delegate pattern에는 위임자와 대리자, 두가지 역할이 있다.
 
#### 위임자
- 프로토콜을 인스턴스로 갖는 객체
- 대리자에 대한 참조 유지
- 이벤트 발생 시, 대리자에게 알림
 
#### 대리자
- 커스텀 컨트롤러 객체
- 채택한 프로토콜 클래스 메소드 구현
 
***
 
> **iOS에서는 델리게이트 패턴은 즉, 프로토콜이라고 할 수 있는데 왜 굳이 delegate pattern이라고 따로 정의할까??**   
> 프로토콜은 swift 언어의 특성이고 delegate pattern을 사용하기 위한 방법으로 프로토콜을 사용할 것이다.
 
```
// TableViewCell
protocol TableViewCellDelegate: class {
    func btnClicked()
}
 
class TableViewCell: UITableViewCell {
 
    weak var delegate: TableViewCellDelegate?
    
    @IBAction func btnClicked(_ sender: UIButton) {
        self.delegate?.btnClicked()
    }
}
```
이렇게 TableViewCell의 권한을 위임할 프로토콜을 선언하고 위임자에서 호출하면,
```
// ViewController
class ViewController: UIViewController {
    
    @IBOutlet weak var tableView: UITableView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // 이것 또한 델리게이트 패턴
        self.tableView.delegate = self
        self.tableView.dataSource = self
    }
}
extension ViewController: TableViewCellDelegate {
    func btnClicked() {
        // ViewController에서 TableViewCell 대신 실행할 코드
    }
}
extension ViewController: UITableViewDelegate, UITableViewDataSource {
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "TableViewCell", for: indexPath) as! TableViewCell
        cell.delegate = self
        return cell
    }
}
```
대리자에서 해당 프로토콜을 채택하고 메소드를 구현한다.   
그리고 반드시 `cell.delegate = self`와 같이 해당 위임을 어떤 대리자가 받는지 알려줘야 한다.
 
### Delegate Pattern을 활용하는 이유
 
위임을 통해 객체가 분리된 상태로 통신이 이루어지기 때문에 객체의 구체적인 타입을 알 필요가 없고, **재사용 및 유지 관리가 쉬운 코드**를 작성할 수 있다.
 
#### Reference)
 
[https://velog.io/@delmasong/Delegate-pattern-in-iOS-x1k6f9jzx8](https://velog.io/@delmasong/Delegate-pattern-in-iOS-x1k6f9jzx8)
