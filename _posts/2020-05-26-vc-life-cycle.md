---
comments: true
title: Swift ) ViewController 생명주기(Life Cycle)
key: 202005261
modify_date: 2020-05-26
picture_frame: shadow
tags:
  - [swift]
---
 
## ViewController 생명주기
 
앱을 구셩하는 모든 ViewController들은 각각 생명주기를 갖고 있는데, **ViewController가 화면에 보였다가 사라지는 주기**를 생명주기라고 한다.   
    
    
<p style="text-align:center"><img width="510" alt="KakaoTalk_Photo_2021-05-04-19-16-53" src="https://user-images.githubusercontent.com/50580583/116989888-53615580-ad0d-11eb-8d6a-c4504fbdc33f.png"></p>
    
    
### 1. loadView()
 
**화면에 띄워줄 view를 만드는 메소드**로, view를 만들고 메모리에 올린다.   
사용자가 이 메소드를 직접 호출하면 안되지만, 스토리보드나 nib 파일을 사용하지 않는다면 이 메소드를 오버라이드해서 뷰를 만들고 뷰 계층을 구성해야 한다.   
 
### 2. viewDidLoad()
 
**뷰의 컨트롤러가 메모리에 로드된 후에 호출**되며 시스템에 의해 자동으로 호출된다.   
보통 사용자에게 화면이 보여지기 전에 데이터를 뿌려주는 행위에 대한 코드를 작성하며, **리소스를 초기화하거나 초기화면을 구성하는 용도**로 쓰인다.   
이 메소드는 ViewController 생에 **"딱 한번"** 호출되므로, 한 번만 있을 행위에 대한 코드는 이 메소드 안에 정의해줘야 한다.
 
### 3. viewWillAppear(_:)
 
뷰 컨트롤러의 화면 올라온 후, **뷰가 화면에 나타나기 직전에 컨트롤러에게 알리는 역할로 호출**된다.   
`viewDidLoad()`와는 달리, **화면 전환을 통해 다른 뷰로 이동했다가 되돌아올 때 재호출**되므로 화면이 나타날 때마다 수행해야하는 작업을 정의하기에 좋다.   
 
<p style="text-align:center"><img width="590" alt="KakaoTalk_Photo_2021-05-04-19-21-09" src="https://user-images.githubusercontent.com/50580583/116992206-a5f04100-ad10-11eb-98f4-5c77cc687621.png"></p>
 
### 4. viewDidAppear(_:)
 
view가 데이터와 함께 완전히 화면에 나타난 후 호출된다.   
 
### 5. viewWillDisappear(_:)
 
다음 뷰 컨트롤러로 전환되기 전이나 뷰 컨트롤러가 사라지기 직전에 호출된다.   
 
### 6. viewDidDisappear(_:)
 
**뷰 컨트롤러가 화면에서 사라지고 나서 호출**되므로, 화면이 사라지고 나서 필요없어지거나 멈춰야하는 작업들을 이 메소드에 정의하면 된다.   
주로 notification이나 observer 삭제 또는 해제를 이 메소드에서 수행한다.   
 
***
 
#### 부록) didReceiveMemoryWarning()
 
시스템 메모리가 부족하면 시스템은 뷰 컨트롤러에 메모리가 부족하다는 메세지를 보내는데, 이 때 호출되는 메소드이다.   
또한 시스템 메모리가 부족하게 되면 뷰 컨트롤러가 파기되는데, 뷰 컨트롤러가 파기되기 직전에 이 메소드가 실행된다.   
때문에 이 메소드에서 해제할 수 있는 메모리를 해제하여 최대한 메모리를 확보하고 강제 종료를 막을 수 있다.   
 
#### Reference)
 
[https://jcsoohwancho.github.io/2019-09-21-iOS-%EB%B7%B0%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC%EC%9D%98-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0/](https://jcsoohwancho.github.io/2019-09-21-iOS-%EB%B7%B0%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC%EC%9D%98-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0/)
