---
layout: post
title: "Agar.io 서버 구축하기"
description: "웹게임 Agar.io 커스텀 서버를 구축하는 법을 알아본다."
date: 2015-08-03
tags: [Javascript]
comments: true
share: true
---

![](/images/agario.png)

최근 해외도 그렇고 국내도 그렇고, [agar.io](http://agar.io) 라는 웹 게임이 굉장히 유행하고 있다. 그 유행에 따라 커스텀 서버도 많이 등장하고 있는 추세인데, 우리 같은 일반인들도 Agar.io 커스텀 서버를 직접 구축할 수 있다. [github.com](http://github.com) 에 최근 많은 agar.io 클론이 풀렸기 때문인것 같다.

나는 수많은 Agar.io 클론중에 [Ogar Project](https://github.com/OgarProject/Ogar)를 택했다. 딱히 이유는 없고, 예전에 아무거나 다운받아서 서버를 돌려봤는데, 정상적으로 돌아가지 않아서 포기했던적이 있는데, 활동하고 있는 한 카페에서 어떤분이 커스텀 서버를 돌리고 계셔서 추천받은 클론 버전이다.

## 서버 다운로드

https://github.com/OgarProject/Ogar

이 Github 저장소에서 OgarProject 를 다운받아주자. (우측 하단의 Download Zip을 누르거나, git 명령어를 통해 직접 클론 받자)

본인은 리눅스(우분투) 환경에 Git 명령어를 사용하여 직접 Clone 을 받아보겠다.

```
git clone git://github.com/OgarProject/Ogar.git Ogar
```

해당 명령어를 통해 원하는 폴더에다가 Clone 해준다. 그리고 생성된 Ogar 폴더 내부로 들어가서 node.js의 ws 모듈을 설치해 주어야 한다. agar.io 는 socket.io 모듈을 사용한 통신 대신 Websocket을 차용하였다.

```
npm install ws
```

조금 기다리고 나면, 모든 준비가 완료 되었다. 이제 node 명령어를 사용하여 서버를 열어보자.

## 구동하기

아래의 명령어를 입력해준다.

```
sudo node Ogar
```

공식 메뉴얼에서는 sudo가 없지만, root 권한 없이 실행하면 오류가 뜬다. sudo 를 붙이거나 root 계정으로 실행하도록 하자.

```
[Game] Ogar – An open source Agar.io server implementation
[Game] Config not found… Generating new config
[Game] Loaded stats server on port 88
[Game] Listening on port 443
[Game] Current game mode is Free For All
```

이렇게 뜬다면 성공한 것이다.

## 접속하기

Ogar Project에서는 따로 프론트엔드 (접속하는 부분) 부분을 배포하지 않는다. 신기하게도 agar.io 본 서버가 커스텀 서버의 접속기 역할을 할 수 있다. 노린건지 아닌지는 모르겠다.

http://agar.io/?ip=서버_아이피:443
“서버 아이피”를 본인의 서버 아이피로 바꿔준뒤 웹브라우저로 접속해보자. 정 접속하는 부분도 본인의 서버로 돌리고 싶다면, Agar.io 본섭의 HTML /CSS/JS 를 긁어와서 본인의 서버에서 웹서버를 열어도 무방할 듯 싶다.
