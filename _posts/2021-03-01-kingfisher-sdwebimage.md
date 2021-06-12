---
comments: true
title: Swift) Kingfisher와 SDWebImage
key: 202103011
modify_date: 2021-06-10
picture_frame: shadow
tags:
  - [swift]
---
 
먼저 캐싱에 대해 먼저 알아보자.   
 
#### 캐싱(Caching)
 
캐싱이란 오래걸리는 작업을 저장해두었다가, 동일 작업을 수행해야 할 때 **저장된 결과를 가져와 사용하는 것**을 의미한다.   
캐싱에는 **이미지 캐싱**과 **도메인으로 웹페이지 접속할 경우 IP 캐싱**이 있는데, iOS에서 이미지 캐싱 처리를 할 땐 보통 `NSCache`와 `FileManager` 두 클래스를 이용한다.   
 
- `NSCache`
  - **메모리 캐싱** 방식 : iOS에서 자체적으로 제공하는 기능, 기기 종료시 캐싱 내용 사라짐, 처리속도가 빠르나 저장공간이 작음
  - 데이터를 key-value 형태로 저장
  - 캐싱 데이터가 너무 많은 메모리를 사용할 시, 자동으로 캐싱 메모리 삭제
- `FileManager`
  - **디스크 캐싱** 방식 : 캐싱 데이터가 자체 디렉토리를 만들어 기기 내부에 아카이빙, 기기 종료시에도 저장되어 있음(선택사항), 저장공간은 크지만 처리속도가 느린 편
   
---
   
## Kingfisher
 
앞선 설명처럼 iOS에선 이미지 캐싱을 할 때 보통 NSCache와 FileManager 클래스를 사용하는데, Kingfisher는 두 클래스를 이용해서 좀 더 쉽게 이미지를 캐싱할 수 있도록 만들어진 라이브러리이다.   

 
### Kingfisher 기능
 
- 비동기 이미지 다운로드 및 캐싱
- URLSession 기반 네트워킹
- 메모리와 디스크를 위한 다중 계층 캐시 제공
- GIF 이미지 지원
- 유용한 이미지 프로세서 & 필터 기능 제공
- UIImageView, UIButton에 대한 Extension 기능 제공
- SwiftUI도 제공
 
```
if let url = URL(string: self.imgUrl) {
    self.imgView.kf.setImage(with: url)
}
```
보통 Kingfisher로 이미지 캐싱을 구현할 때 이런 코드 형태인데,   
 
- **Kingfisher가 url로부터 이미지 다운**
- **다운받은 이미지를 메모리와 디스크 캐시에 저장**
- **ImageView에 디스플레이**
 
이런 step으로 진행된다.   
**첫 다운로드 때 캐시에 저장하기 때문에** 추후 같은 url을 통한 이미지 캐싱 요청시, 캐시로부터 데이터를 바로 가져와 매우 빠른 속도로 처리할 수 있다.   
   
#### processor
 
ImageProcessor는 **이미지나 데이터를 다른 이미지로 변환**하도록 도와줘 Kingfisher를 좀 더 유연하게 만드는 기능인데, `options` 파라미터에서 설정할 수 있다.   
processor는 "cornerRadius 효과, 사이즈 재설정, 블러 처리, 틴트 컬러 설정, 샘플이미지 다운로드"와 같은 다양한 내장 프로세서를 제공한다.   
 
#### cancelDownTaask
 
예를 들어, collectionView나 tableView를 통해 여러 이미지들이 세팅된다면 사용자가 빠르게 스크롤할 때 이미지 캐싱 작업량이 많아져 버벅이는 현상이 발생할 수 있다.   
이때 스크롤을 통해 이미 사라진 cell의 이미지 캐싱 작업은 불필요해지기 때문에 해당 cell의 **이미지 캐싱 작업은 취소**시킬 수 있고, 이를 통해 Kingfisher의 퍼포먼스가 향상된다.   
 
collectionView나 tableView의 `didEndDisplaying`을 감지하는 함수에서 `cell.imgView.kf.cancelDownTask()`라는 코드 한줄을 추가하면 디스플레이가 종료된 cell의 이미지 캐싱 작업만이 취소된다.   
 
## SDWebImage
 

 
## Kingfisher와 SDWebImage
 
SDWebImage를 사용하다가 Kingfisher가 나오면서 많은 개발자들이 Kingfisher로 이동했다고 한다.   
**Kingfisher**는 **Swift**로, **SDWebImage**는 **Objectvie-C**로 구현되어 있기 때문에 Kingfisher가 체감상 더 빠른 느낌이라는데, 사실 직접 대용량 이미지를 캐싱하거나 GIF를 캐싱해본 적이 없어 아직까지 큰 차이를 체감하진 못했다.   
 
그러나 레퍼런스를 찾아 공부하던 중, [이미지 캐싱 라이브러리의 성능을 비교한 테스트 자료](https://gist.github.com/linearhw/a0677b967b741abf9b8a903c37d3bcc9)를 보고 참고했다.   
 
리사이즈없이 테스트했을 땐 중간 해상도부터 비교가 가능했는데, Kingfisher의 메모리 사용량이 크게 상승하면서 CPU가 튀거나 스크롤시 버벅이는 현상이 나타났다. 그리고 고해상도를 캐싱할 땐 SDWebImage 역시 CPU 튐 현상이 발생하였지만, Kingfihser는 backBtn을 누르면 버벅이는 현상까지 나타났다. *SDWebImage는 backBtn을 눌러서 나오면 바로 메모리 사용량이 줄어듬*   
 
리사이즈를 포함했을 땐 SDWebImage가 중간 해상도부터 메모리 사용량과 캐싱 타임이 Kingfisher에 비해 상승했고, 높은 해상도를 캐싱할 때에도 역시 SDWebImage에서 메모리와 CPU 튀는 현상이 나타났다.   
   
정리하자면...   
   
- **리사이즈 미포함**   
  - (중간 해상도부터) `Kingfisher`의 메모리 사용량 증가, CPU 튐/버벅임 현상 발생   
- **리사이즈 포함**   
  - (중간 해상도부터) `SDWebImage`의 메모리 사용량과 캐싱 타임 상승, 메모리와 CPU 튐 현상 발생   
 
 
물론 Kingfisher의 "backBtn으로 인한 버벅임 현상"은 `KingfisherManager.shared.downloader.cnacelAll()`을 통해 메모리 사용량을 줄일 수 있다. *이 부분은 향후 테스트를 통해 한번 확인할 예정이다.*   
 
#### Reference)
 
[https://gist.github.com/linearhw/a0677b967b741abf9b8a903c37d3bcc9](https://gist.github.com/linearhw/a0677b967b741abf9b8a903c37d3bcc9)   
[https://duwjdtn11.tistory.com/594](https://duwjdtn11.tistory.com/594)
