---
layout: post
title: "[Javscript 기초] 1강 - 자바스크립트 소개"
description: ""
date: 2013-08-16
tags: [Javascript]
comments: true
share: true
---

자바스크립트는 **객체 기반의 스크립트 프로그래밍 언어**로써, 보통은 웹브라우져에서 작동되지만 최근에는 node.js의 등장을 기점으로 다른 플랫폼으로도 많은 이식이 되고 있는 추세입니다. 

필자는 자바스크립트를 굉장히 많이 사용합니다. 거의 모든곳에서 자바스크립트로 코딩을 하고 있다고 해도 과언이 아닐정도로요. 지금의 자바스크립트는 더이상 웹브라우저에서 DOM을 조작하기 위해 사용하는 단순한 언어가 아닙니다. 자바스크립트는 점점 더 복잡해지고, 새로운 기술은 제가 글을 쓰고 있는 이 시점에서도 계속 등장하고 있습니다. 

가장먼저, 프론트엔드 웹 개발을 위한 [React](https://facebook.github.io/react), [AngularJS](https://angularjs.org/), [Vue](https://vuejs.org/) 등의 여러 라이브러리와 프레임워크, 웹 서버개발을 위한 [node.js](https://nodejs.org/ko/), 데스크탑 앱을 개발을 위한 [NW.JS](https://nwjs.io/)와 [Electron](http://electron.atom.io/), 모바일 앱 개발을 위한 [React Native](https://facebook.github.io/react-native/) 등이 존재합니다. 심지어 로보틱스와 IoT를 위한 [Johnny-Five](http://johnny-five.io/)라는 플랫폼도 존재합니다. 

이런 새로운 기술들을 제대로 다루기 위해서는 그 기반인 자바스크립트부터 제대로 알고 있어야 한다고 생각합니다. 그렇기에 본 강의의 궁극적인 목표는 **Javascript 생태계의 여러 기술을 제대로 다루기 위한 Javascript 기초 공부** 입니다.

자, 이제 본격적으로 Javascript에 대해 알아봅시다!

## 특징

##### 프로토타입 기반 객체 지향 언어

자바스크립트는 객체지향 언어이긴 하지만, 여러분들이 흔히 생각하는 클래스를 생성하고 그 클래스를 사용하여 객체를 생성하는 일반적인 객체 지향 언어가 아닙니다. 자바스크립트는 클래스가 존재 하지 않는 (class-less) **프로토타입 기반 객체 지향 언어** 입니다. 