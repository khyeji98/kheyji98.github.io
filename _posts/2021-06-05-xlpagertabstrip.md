---
comments: true
title: Swift) XLPagerTabStrip 라이브러리로 커스텀 탭 구현하기
key: 202106051
modify_date: 2021-06-06
picture_frame: shadow
tags:
  - [swift]
---
 
pod init을 했다면 Podfile에 XLPagerTabStrip 팟을 추가해준다.   
```
$ pod 'XLPagerTabStrip', '~> 9.0'
```
 
XLPagerTabStrip을 사용할 땐 MainVC와 하위뷰인 ChildVC들이 필요한데, MainVC와 ChildVC들 모두   
```
import XLPagerTabStrip
```
XLPagerTabStrip을 임명해야 한다.
 
그리고 이렇게 **MainVC**는 아예 `UIViewController` 대신 `ButtonBarPagerTabStripViewController`를 상속받고,   
```
class MainVC : ButtonBarPagerTabStripViewController { }
```
 
**ChildVC들**은 추가로 `IndicatorInfoProvider`을 상속받는다.   
```
class Child1VC: UIViewController, IndicatorInfoProvider { }
```
 
스토리보드에서 MainVC에 TabBar로 CollectionView를 추가하고, `ButtonBarView`를 상속시킨다.   
 
<p style="text-align:center"><img width="256" alt="KakaoTalk_Photo_2021-06-06-20-46-56" src="https://user-images.githubusercontent.com/50580583/121861486-d32f0680-cd34-11eb-910c-761aa4fa3cae.png"></p>   
 
#### Reference)
 
[https://github.com/xmartlabs/XLPagerTabStrip](https://github.com/xmartlabs/XLPagerTabStrip)
