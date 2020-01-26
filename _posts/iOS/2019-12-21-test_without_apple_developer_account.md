---
layout: post
title: iOS) 개발자 계정 등록하지 않고 아이폰으로 테스트하기
tags: iOS Developer-Account build
categories: iOS
---
아이폰으로 Xcode를 빌드하기 위해서는 몇 가지만 체크하면 된다.



1. Xcode와 iOS 버전 확인
2. 애플 개발자 계정 추가하기
3. 앱 서명하기(sign the app)



### 1. Xcode와 iOS 버전 확인

#### 1.1 Xcode 버전 확인

<img src="{{ site.url }}/assets/img/post_img/191221/1.png">

Xcode 버전은 사진과 같이 상단 메뉴 바에서 <strong>Xcode - About Xcode </strong>를 눌러보면 확인할 수 있다.



#### 1.2 iOS 버전 확인

<img src="{{ site.url }}/assets/img/post_img/191221/2.png">

영어

- <strong>General - About</strong>

한글

- <strong>설정 - 일반 - 정보</strong>



여기서 <strong>Xcode와 iOS의 버전(소수점)이 동일한지 확인</strong>해주면 된다.

두 버전이 같지 않다면, 쉽게 맞출 수 있는 방법으로 둘다 최신으로 업데이트해주면 된다.

(19.12.21 기준 Xcode 최신 버전 11.3, iOS 최신 버전 13.3)



### 2. 애플 개발자 계정 추가하기

<img src="{{ site.url }}/assets/img/post_img/191221/3.png">

개발자 계정 추가는 메뉴에서 <strong>Xcode - Preferences - Accounts - +버튼</strong>으로 Apple 계정의 ID와 PW를 입력하면 된다.



<img src="{{ site.url }}/assets/img/post_img/191221/4.png">

계정 추가를 마친 화면은 위의 사진과 같다.(개인정보는 가렸어요.)



### 3. 앱 서명하기 (sign the app)

sign을 임의로 저렇게 번역했는데, 사실 정확하게 의미를 전달했는지 잘 모르겠다ㅋㅋ

<img src="{{ site.url }}/assets/img/post_img/191221/5.png">

사진과 같이 왼쪽 메뉴에서 프로젝트를 클릭하고 상단에 <strong>Signing & Capabilities</strong>를 눌러 나오는 내용을 확인한다.

여기에서 확인한 부분은 다음과 같다.

1. Automatically manage signing에 체크가 되어 있는지
2. Team이 아까 2번에서  추가한 계정으로 되어 있는지



이제 아이폰을 연결하고 첫 번째 사진의 빨간 박스 부분을 두 번째 사진과 같이 바꿔준다.

<img src="{{ site.url }}/assets/img/post_img/191221/6.png" alt="pic1">

​	

<img src="{{ site.url }}/assets/img/post_img/191221/7.png" alt="pic2">



그리고 빌드를 하면 끝이 난다.

참고로 빌드할 때, 나오는 keychain은 따로 변경하지 않았다면, 맥의 비밀번호를 입력하면 된다.

<img src="{{ site.url }}/assets/img/post_img/191221/8.png">

또, 맥과 아이폰이 같은 네트워크에 연결되어 있다면 <strong>Window - Device and Simulators</strong>에서 <strong>Connect via network</strong> 박스에 체크해줌으로써 맥과 아이폰을  연결하지 않고  블루투스로도 빌드가 가능하다.



혹시라도 잘못된 부분이 있으면 알려주세요!









