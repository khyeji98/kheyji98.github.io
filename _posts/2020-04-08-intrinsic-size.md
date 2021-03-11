---
comments: true
title: [iOS ) Intrinsic Size]
key: 202004081
modify_date: 2020-04-08
picture_frame: shadow
tags:
  - [AutoLayout]
  - [iOS]
---
 
## Intrinsic Size
 
Intrinsic Size란 해석 그대로 **본질적인 내용의 크기**인데, 우리는 보통 view의 위치와 크기를 정해주지만 경우에 따라 **view 안에 있는 content에 따라** 고유한 크기를 가지며 이를 **Intrinsic Size**라고 한다.   
 
예를 들어, UILabel을 보면
 
이렇게 내부에 있는 content, 즉 text에 따라 width가 달라짐을 알 수 있다.(물론 폰트에 따라 height도 달라질 수 있다)
그리고 이렇게 content에 따라 달라지는 크기를 **Intrinsic size**라고 하는 것이다.   
 
UILabel 외에도 UIButton, UISwitch, UITextField, UITextView, UIImageView 등이 있다.   
 
***
 
그리고 이렇게 Intrinsic size를 갖는 객체들의 메소드를 보면 `invalidateIntrinsicContentSize()`가 있을 것이다.   
이 메소드는 content의 크기가 바뀌었을 때 InrrinsicContentSize 프로퍼티를 통해 값이 갱신되고, 그에 맞게 Auto Layout을 업데이트시켜주는 메소드이다.   
 
 
UIView는 기본적으로 적용이 되어 있기 때문에 크게 신경쓰지 않아도 된다.   
다만, 커스텀뷰를 만들게 되면 `invalidateIntrisicContentSize()` 메소드를 구현해줘야 한다.   
 
다시 또 UILabel로 예를 들어,
```
extension UILabel {
  open override func invalidateIntrinsicContentSize() {
   
//    super.invalidateIntrinsicContentSize()
  
  }
}
```
이렇게 content size를 계산해주는 메소드가 실행되지 않게 extension을 구현해보면,

text에 의해 변경된 content size가 제대로 적용되지 않는 것을 확인할 수 있다.
 
#### Reference )
