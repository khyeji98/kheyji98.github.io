---
comments: true
title: [iOS ) Foundation Kit]
key: 202004201
modify_date: 2020-04-20
picture_frame: shadow
tags:
  - [iOS]
---
 
## Foundation Kit
 
Foundation Kit 즉, Foundation 프레임워크란 **Cocoa Touch 프레임워크에 포함**된 프레임워크로 **프로그램의 중심**을 담당하는 프레임워크이다.   
Foundation은 원시 데이터 타입과 컬렉션 타입 및 운영체제 서비스를 사용해 어플리케이션의 기본적인 기능을 관리하며, Foundation 프레임워크에서 정의한 클래스와 프로토콜 및 데이터 타입은 iOS, MacOS, tvOS 등 모든 애플의 SDK에서 사용된다.   
 
때문에 Foundation 프레임워크를 상속하지 않으면 거의 아무것도 못한다고 볼 수 있다.   
 
### 주요 기능
 
Foundation 내에 포함된 클래스들은 앞에 `NS`가 붙으며 주요 기능들이 있다.
 
#### 기본
 
- Number, Data, String : **원시 데이터 타입** 사용
- **Collection** : Array, Dictionary, Set 등
- Date and Time : **날짜와 시간** 계산 및 비교
- Unit and Measurement : 물리적 차원을 숫자로 표현 및 단위 간 변환
- Data Formattin : 숫자, 날짜, 측정값 등을 문자열로 변환하거나 그 반대 작업
- Filter and Sort : 컬렉션 요소 필터 및 정렬
 
#### 어플리케이션 지원
 
- Resources : **어플리케이션 에셋과 번들 데이터에 접근 지원**
- **Notification** : 정보 퍼뜨리거나 받아들이는 기능 지원
- App Extension : 확장 어플리케이션과의 상호작용 지원
- Error and Exceptions : API와의 상호작용에서 발생할 수 있는 문제에 대한 대처 지원
 
#### 파일 및 데이터 관리
 
- **File System** : 파일이나 폴더 생성 및 읽기, 쓰기
- Archives and Serialization : 속성 목록, JSON, 바이너리 파일들을 객체로 변환하거나 그 반대 작업
- iCloud : 사용자의 iCloud 계정을 통해 데이터 동기화
 
#### 네트워킹
 
- URL Loading System : 표준 인터넷 프로토콜을 통해 **URL과 상호작용 및 서버 통신**
- Bonjour : 로컬 네이트워크를 위한 작업
 
#### Reference )
 
[https://velog.io/@wan088/iOS-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC-CocoaTouch-Foundation-UIkit-sjjzdqmte4](https://velog.io/@wan088/iOS-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC-CocoaTouch-Foundation-UIkit-sjjzdqmte4)
