---
comments: true
title: [Cocoapod 버전 업데이트 에러 해결 방법]
key: 202102071
modify_date: 2021-02-08
picture_frame: shadow
tags:
  - [iOS]
  - [Xcode]
---
 
만약 코코아팟 버전 업데이트도 몰랐던 나처럼 완전 "컴맹+아마추어 개발자"라면 코코아팟 설치와 버전 업데이트 명령어가 같다는 것을 꼭꼭꼭 알아두자..
 
```
$ sudo gem install cocoapods
```
 
지금은 알지만 처음엔 몰라서 혼자 구글에 허둥지둥 검색하면서 고군분투했던 기억이..
  
  
***
  
  
아무튼 여느 때와 같이 코코아팟 버전을 1.10.0에서 1.10.1로 업데이트하려는데..   
 
<p style="text-align:center"><img width="690" alt="KakaoTalk_Photo_2021-02-08-15-58-35" src="https://user-images.githubusercontent.com/50580583/107186940-86ef5500-6a28-11eb-8802-a6980f3b6d34.png"></p>   
 
갑자기 이런 듣도 보도 못한 에러가...😭
    
    
구글링해보니
```
$ xcode-select --install
```
command line tools 설치 여부를 확인하는 방법과
```
$ brew install cocoapods --build-from-source
```
homebrew를 통해 install하는 방법과
```
xcode 삭제후 재설치..^^
```
이런 각종 방법들을 모두 동원해보았지만 내 에러는 해결되지 않았다ㅜㅜ   
    
    
그러던 중 발견한 마지막 방법
```
$ sudo rm -rf /Library/Developer/CommandLineTools
```
먼저 기존에 설치된 command line tools를 아예 삭제하고,
```
$ xcode-select --install
```
다시 command line tools 설치,
```
$ git --version
```
오류 처리 여부를 확인하고,
```
$ sudo gem install cocoapods
```
다시 버전 업데이트!!   
 
그리고 확인한 결과   
 
<p style="text-align:center"><img width="329" alt="KakaoTalk_Photo_2021-02-08-16-08-26" src="https://user-images.githubusercontent.com/50580583/107186946-88208200-6a28-11eb-84f9-99e767ed6e1c.png"></p>   
 
짠!   
**드디어 성공** 😂
    
    
혼자 눈물을 훔치며 Xcode를 삭제했다가 다시 설치하고 이리저리 시간을 허비했었지만 이렇게 성공하고나니 시간 낭비와 좌절은 기억도 나지 않더라..^^
 
#### 정리해보면..
 
1. 기존 command line tools 삭제
2. command line tools 다시 설치
3. 에러 처리 여부 확인
4. 코코아팟 버전 업데이트
5. 코코아팟 버전 확인
 
#### Reference)
 
[https://velog.io/@lv14/CocoaPods-%EC%B4%88%EA%B8%B0%ED%99%94-%EC%98%A4%EB%A5%98-%EC%B2%98%EB%A6%AC](https://velog.io/@lv14/CocoaPods-%EC%B4%88%EA%B8%B0%ED%99%94-%EC%98%A4%EB%A5%98-%EC%B2%98%EB%A6%AC)
