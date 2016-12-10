---
layout: post
title: "HTML5 WebStorage API 사용하기"
description: "HTML5에서 지원하는 WebStorage API로 웹브라우저에 데이터를 저장하는 방법을 알아본다."
date: 2016-12-11
tags: [Javascript]
comments: true
share: true
---

![](/images/html5.jpg)

## 소개

HTML5에는 브라우저 자체에서 데이터를 저장할 수 있는 객체를 제공한다. 바로 **Local Storage**와 **Session Storage** 이다. 둘의 차이점은 단순히 Local Storage는 데이터의 유효기간이 존재하지 않고, Session Storage 는 웹브라우저 종료시 데이터가 소멸된다는 점이다. 그 외에는 다른 점이 없다.

## 쿠키와의 차이점

쿠키도 WebStorage API 도 둘다 브라우저에 데이터를 저장한다는 점은 동일하다. 하지만 굳이 쿠키가 있는 상황에서 괜히 새로운 API 를 만든 것은 아니다.

* **쿠키는 매 Request 마다 Header 에 포함되어 전송된다.** 이는 브라우징을 느리게 하는 원인이 될 수 있다.
* 쿠키는 암호화 되지 않고 전송되며, 로컬에 텍스트파일 형식으로 저장되어 있어 **보안이 취약**하다.
* 반면에 쿠키는 **단순 문자열**로 저장되어, 일일히 파싱을 해주어야 한다. 하지만 WebStorage는 **Key-Value** 형식으로 저장되어 관리하기 쉽다.
* 쿠키는 4kb의 **저장공간 제한**이 존재한다. WebStrage API 는 그런거 없다.

다만, WebStorage API 는 **같은 도메인에서만 데이터가 공유**되어, 서브 도메인이 달라지면 공유할 수 없다는 사소한 단점도 존재한다. www.my.domain 과 m.my.domain 끼리는 데이터 공유가 불가능하다.

## 사용

위에서 언급했듯이, Local Storage 객체와 Session Storage 객체는 유효기간 존재 유무만 다르며 나머지는 모두 똑같으니 여기서는 Local Storage 만 사용해보도록 하겠다.

**데이터 저장**

```javascript
localStorage.setItem("foo", "bar"); //setItem 메소드를 사용하는 방법
localStorage.foo = "bar" //객체에 직접 접근하는 방법
localStorage['foo'] = "bar" //딕셔너리 형태로 접근하는 방법
```

localStorage 객체 자체에 데이터가 저장되기 때문에 여러가지 방법으로 데이터에 접근할 수 있다.

**데이터 조회**

```javascript
localStorage.getItem("foo"); //getItem 메소드를 사용하는 방법
localStorage.foo; //객체에 직접 접근하는 방법
localStorage['foo']; //딕셔너리 형태로 접근하는 방법
```

모두 결과는 "bar" 이다.

**모든 데이터 삭제**

```javascript
localStorage.clear();
```

**Array 혹은 Object 저장**

WebStorage는 문자열 형식으로 밖에 저장할 수 없어 어쩔수 없이 배열이나 객체를 Stringify 해준뒤 저장해야한다.

```javascript
var bar = {
  foo1: "bar1",
  foo2: "bar2",
  foo3: "bar3"
}

localStorage.setItem("foo", JSON.stringify(bar));
```

또한 다음과 같이 문자열을 객체로 바꿔 불러온다.

```javascript
var bar = localStorage.getItem("foo");

JSON.parse(bar);
```
