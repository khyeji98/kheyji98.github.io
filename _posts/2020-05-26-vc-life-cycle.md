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
 
### loadView()
 
**화면에 띄워줄 view를 만드는 메소드**로, view를 만들고 메모리에 올린다.   
사용자가 이 메소드를 직접 호출하면 안되지만, 스토리보드나 nib 파일을 사용하지 않는다면 이 메소드를 오버라이드해서 뷰를 만들고 뷰 계층을 구성해야 한다.   
 
### viewDidLoad()
 
**뷰의 컨트롤러가 메모리에 로드된 후에 호출**되며 시스템에 의해 자동으로 호출된다.   
보통 사용자에게 화면이 보여지기 전에 데이터를 뿌려주는 행위에 대한 코드를 작성하며, **리소스를 초기화하거나 초기화면을 구성하는 용도**로 쓰인다.   
이 메소드는 ViewController 생에 **"딱 한번"** 호출되므로, 한 번만 있을 행위에 대한 코드는 이 메소드 안에 정의해줘야 한다.
 
### viewWillAppear()
 
뷰 컨트롤러의 화면 올라온 후, **뷰가 화면에 나타나기 직전에 컨트롤러에게 알리는 역할로 호출**된다.   
 
#### Reference)
