---
layout: post
title: "node.js에서 vhost 사용하기"
description: "Express.js의 vhost를 사용하면 한 서버에서 여러 사이트를 운영하는 것이 가능하다."
date: 2015-10-31
tags: [Javascript, Server, Node.js]
comments: true
share: true
---

![](/images/nodejs.jpg)

Apache 혹은 Nginx 서버 위에서 돌아가는 PHP 등의 경우는 Apache가 내부에서 프록싱을 해주어서 한 서버에서 여러 사이트를 돌리는게 가능하다. 물론 node.js의 경우에도 노드 서버 앞에 Apache나 Nginx를 둬서 프록싱을 맡겨 버리는 방법도 있다. 하지만 node.js 에서 직접 이런 기능을 구현할 수 있는데, `vhost` 를 이용하는 방법이다.

Express 3.x 버전까지는 vhost가 포함되어 있었는데, 4.x 버전부터 [독립된 모듈](https://github.com/expressjs/vhost)이 되었다. npm을 이용해서 다운로드 받을 수 있다.

	$ npm install vhost

이와 관한 자세한 내용은 [http://expressjs.com/guide/migrating-4.html](http://expressjs.com/guide/migrating-4.html) 를 참고하자.

어쨌든 Express 4.x 유저들은 이전에 작성된 vhost 사용 관련 문서를 참고할 수 없게 되었다. 딱히 많이 변경된 것은 없지만, 본 문서에서는 Express 4.x 버전을 기준으로 서술한다.

본론으로 들어가기 전에 Express 모듈과 vhost 모듈을 설치해주고, js에서 require 해주자.

~~~js
var express = require('express');
var vhost = require('vhost');
~~~

그리고 Express 모듈을 이용하여 express 어플리케이션을 2개 생성해주자.

~~~js
var app1 = express();
var app2 = express();
~~~

그리고 다음과 같이 어플리케이션별로 라우팅 설정을 해준다.

~~~js
app1.get("/", function(req, res) {
	res.send("app1");
});


app2.get("/", function(req, res) {
	res.send("app2");
});
~~~

그리고 메인 어플리케이션 하나를 정의해준다.

~~~js
var app = express();
~~~

마지막으로 vhost 를 메인 어플리케이션에 use 시켜준다음 서버를 실행한다. (서브 도메인에 관한 세팅은 이미 되어 있어야 한다.)

~~~js
app.use(vhost("app1.rozix.net", app1));
app.use(vhost("app2.rozix.net", app2));

app.listen(80);
~~~

설정한 도메인에 따라 실행되는 어플리케이션이 다름을 볼 수 있다. 직접 접속해보자.
