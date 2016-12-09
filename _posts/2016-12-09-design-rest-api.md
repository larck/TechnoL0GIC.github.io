---
layout: post
title: "RESTful한 API 디자인 가이드"
description: "REST(REpresentational Safe Transfer) 원리를 따르는 API 디자인 방법을 알아본다."
date: 2016-12-09
tags: [Javascript, Server, REST]
comments: true
share: true
---

> 엄격한 의미로 REST는 네트워크 아키텍처 원리의 모음이다. 여기서 ‘네트워크 아키텍처 원리’란 자원을 정의하고 자원에 대한 주소를 지정하는 방법 전반을 일컫는다. *-위키백과*

REST(Representational Safe Transfer)는 서버에 존재하는 자원에 접근하기 위한 URI 설계 원칙이자 방법이다. 이 REST 원리를 따르는 시스템을 RESTful 하다고 칭한다.

사실 REST 자체가 제한적인 원칙 따위가 있는 것이 아니고, 일종의 권고안이기에 디자인 하는 사람 나름대로 만들 수 있는 것이다. 그래서 REST**ful**이라는 표현을 사용하는 것이다.

SOAP 방식은 `HTTP/XML` 을 주로 사용하는데, REST 는 `HTTP/Json` 을 사용한다. 주로 JSON을 주고받으면서 통신을 한다는 뜻이다.

## 구성

REST API 는 크게 `리소스`, `메소드`, `메세지` 로 구성되어 있다.

만약 *"ID가 l0gic인 회원의 상세한 정보를 서버로부터 얻고싶다"* 라는 상황이라면, '회원'은 `리소스`, 'ID가 l0gic' 이라는 정보는 `메세지`, '얻고싶다' 라는 행위는 `메소드` 가 된다.

이 구성요소에 대한 자세한 내용을 아래에서 알아보자.

### 리소스

리소스는 URI(Uniform Resource Identifier)의 형태로 표현된다. 여기서 URI란 인터넷에 있는 자료를 표현하는 **유일한 주소** 이다. 위에서 가정된 상황에서는 domain/users/l0gic 로 ID가 l0gic인 유저의 정보를 얻어올 수 있다.

또한 domain/users 라는 상위 리소스에 접근하면, 모든 회원의 정보를 얻어올 수 있도록 디자인 해야한다.

참고로 가급적 여러 하위 리소스를 가지고 있는 경우의 상위 리소스는 복수형으로 사용하는게 좋다. /user/l0gic 의 형태 보다는 /user**s**/l0gic 의 형태가 좋다는 이야기다.

### 메소드

메소드는 자원에 대한 사용자의 행위를 정의한다.

HTTP 에서는 흔히 알려져 있는 `GET` 혹은 `POST` 를 제외하고도 다소 생소한 2개의 메소드를 제공한다. 바로 `PUT` 과 `DELETE` 이다. 이와 같은 4개의 서로다른 메소드를 사용하여, 같은 URI에 들어오는 요청이라도 메소드에 따라 목적이 달라지게 설계해야한다.

* `POST` : 자원 생성
* `GET` : 자원 조회
* `PUT` : 자원 수정
* `DELETE` : 자원 삭제

모든 요청을 `POST` 메소드로만 처리하는 것은 올바르지 않은 REST URI 디자인이다.

### 메세지

자원에 대한 행위의 상세한 내용을 정의한다. HTTP Payload (Body) 로 표현되며, HTTP State 와 같은 Meta Data는 제외된다. 이는 Header 에 표시하는데, 아래에 자세히 서술해 놓았다.

ID가 user_id_01 이고, name은 user_name, email은 user_email@user.domain 인 회원을 생성하려는 상황을 가정하자. 우리는 User를 **추가** 하려는 것이므로 HTTP Method 는 `POST` 를 사용한다. 또한 요청할 URI는 domain/users 이다. 여기서 우리는 이 유저의 **세부 사항**을 작성하여 서버에 보내주어야 한다. 일반적으로 JSON의 형태를 사용하여 전송한다.

```JSON
{
  id: 'user_id_01',
  name: 'user_name',
  email: 'user_email@user.domain'
}
```

## 파라미터

리소스에 접근하기 위한 URI를 디자인 할 때 파라미터를 무분별하게 남발해서는 안된다. 예를 들어 서버에 있는 l0gic 이라는 유저 데이터에 접근하기 위한 URI 는

`domain/getUser.php?id=l0gic` 처럼 디자인 하지 않고, `domain/user/l0gic`
와 같이 오브젝트의 멤버변수를 따라가듯이 디자인을 해야한다. 파라미터의 사용은 데이터의 **필터링**을 위해 사용한다.

## 메타데이터

URI에 접근하여, 접근에 대한 응답 상태를 Body (HTML 부분) 처리의 결과 (성공여부 등)은 HTTP Status 로 표현한다.

http://localhost/user/l0gic
에 접근했을 경우 사용자가 존재하지 않으면, HTTP Status 는 404 (not found) 가 된다.

## 예시

상황에 따라 리소스, 메소드, 메세지를 어떻게 활용하는지 예시를 통해 알아보자.

| 상황                                       | 메소드    | 리소스 (URI)           | 메시지 (Body)                               |
| ---------------------------------------- | ------ | ------------------- | ---------------------------------------- |
| 특정 회원 (l0gic) 조회                         | GET    | domain/users/l0gic  | 없음                                       |
| 모든 회원 조회                                 | GET    | domain/users        | 없음                                       |
| 특정 회원 (user01) 생성 (name은 user_name, email은 user_email@example.domain) | POST   | domain/users        | {  id: 'user01', name: 'user_name',  email: 'user_email@example.domain'} |
| 특정 회원 (user01) 삭제                        | DELETE | domain/users/user01 | 없음                                       |
| 특정 회원 (l0gic) 데이터 업데이트                   | PUT    | domain/users/l0gic  | {  id: 'l0gic',  name: '조동현',  email: 'contact@l0gic.me'} |
