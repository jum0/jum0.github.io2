---
layout: post
title: 한 줄 삭제 단축키
tags: iOS shortcut 
categories: iOS
---
VSCode에는 한 줄 전체를 삭제하는 단축키가 있는데, Xcode에는 그런 기능이 없다ㅠ

그래서 찾아보니 두 가지 방법을 통해서 비슷한 기능을 할 수 있다는 것을 알게 되었다.



1. ctrl + A + K + K
2. Xcode 설정을 통한 단축키 만들기



#### 1. Ctrl + A + K + K

1번은 기능의 조합인데, ctrl + A는 커서의 위치를 현재 커서가 있는 라인의 맨 앞으로 옮기는 단축키이다. 그리고 ctrl + K는 현재 커서가 있는 라인에서 커서의 위치 뒤에 있는 것들을 지우는  단축키이다. 그래서 K를 두 번 눌러주게 되면 내용 지우기 + 내용이 없어서 라인 지우기로 되어,  한 줄 전체를 삭제하는  기능을 하게 된다.



#### 2. Xcode 설정을 통한 단축키 만들기

단축키를 생성하는 방법은 다음과 같다.

<img src="{{ site.url }}/assets/img/post_img/191227/1.png">

Xcode를 실행하고 <strong>Xcode - Preferences</strong>를 클릭한다.



<img src="{{ site.url }}/assets/img/post_img/191221/2.png">

Key Bidings 메뉴를 들어간 후, delete를 검색한다. Delete Line이라는 단축키가 있는데, 위의 사진과 다르게 오른쪽 부분이 비워져 있어서 원하는 단축키를 눌러 등록하면 된다.

참고로 키를 눌러서 등록할 때, <strong>'누른 키 조합 is bound to 머시기'</strong> 이렇게 나오는 경우는 다른 단축키와 중복되었다는 것을 의미하므로 다른 키 조합을 이용해야 한다.



혹시라도 잘못된 부분이 있으면 알려주세요!
