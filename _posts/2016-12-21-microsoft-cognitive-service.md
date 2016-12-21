---
layout: post
title: "Microsoft Cognitive 를 활용한 감정 인식"
description: "딥러닝 Cognitive API 를 활용하여 감정 데이터를 분석해본다."
date: 2015-12-21
tags: [CV, Machine Learning, Deep Learning]
comments: true
share: true
---

어그제, 그러니까 12월 19일에 인공지능 세미나에 참여하기 위해 마이크로소프트 광화문 한국 지사에 방문하였다. 마이크로소프트 김영욱 부장님께서 최초로 제시된 인공지능 개념, 역사 부터 오늘날 머신러닝의 등장과 딥러닝의 보편화 등등 여러가지를 알려주셨다. 세미나가 진행되면서, 흥미로운 Open API 들에 대해 알게 되었다. 가장 인상깊었던 API는 마이크로소프트의 **Cognitive Service** 이다. 

## Cognitive Service

Microsoft Cognitive Service 에는 여러가지 딥러닝에 대한 API가 존재한다. 대표적으로 **Emotion API** 가 있으며, 사진을 넣어주면, 해당 사진에서 얼굴을 인식한다음 행복한 정도, 슬픈 정도 등의 감정 데이터를 분석해서 JSON 으로 반환해주는 API 이다.

![](./images/cognitive-1.png)

와! 재밌어보인다. 우리도 해보자.

## API Key 발급 받기

본 API 를 사용하기 위해서는 Microsoft 계정 (혹은 Github)을 이용해서 API 사용을 위한 Key 를 발급 받아야한다. [Subscription](https://www.microsoft.com/cognitive-services/en-US/subscriptions) 페이지로 가서 **Emotion - Preview** 를 Subscribe 해주자.

![](./images/cognitive-2.png)

한달에 30,000 번, 1분에 20번의 요청을 무료로 사용할 수 있나보다.

이렇게 API Key 가 발급되었다면, Copy 를 눌러 복사해주자.

## API 사용하기

다음과 같은 정보대로 HTTP Request 를 하면 JSON 형태로 감정 데이터가 반환된다.

* **Method** : `POST`
* **URL** : https://api.projectoxford.ai/emotion/v1.0/recognize
* **Header** : { Content-Type : application/json, Ocp-Apim-Subscription-Key : ***본인의 API Key*** }
* **Body** : { url : ***이미지 파일 주소*** }

![](./images/cognitive-4.jpg)

나는 정말정말 **행복해보이는** 유댕이 사진을 활용해보겠다. 다음과 같은 데이터가 반환된다.

```json
[
  {
    "faceRectangle": {
      "height": 249,
      "left": 391,
      "top": 194,
      "width": 249
    },
    "scores": {
      "anger": 1.989072E-09,
      "contempt": 2.87216767E-06,
      "disgust": 7.153612E-09,
      "fear": 1.48043175E-10,
      "happiness": 0.9993681,
      "neutral": 0.000627897563,
      "sadness": 1.11845463E-06,
      "surprise": 4.71076973E-08
    }
  }
]
```

부정적인 감정인 분노 혹은 역겨움, 두려움 등등의 값은 매우 낮다. (각각 0.000000001989072, 0.000000007153612, 0.000000000148043) 그리고 당연하게도 행복(Happiness) 값이 약 **99.9%** (0.9993681) 를 차지하고 있다.

## 마무리

생각보다 꽤 정확해서 놀라운데, 이를 활용하여 많은 것들을 할 수 있을 것 같다. 특히 IoT 분야에서 사용자의 감정 데이터를 분석해서 활용 할 수 있다는 생각이 든다.

머신러닝이란 기술이 이슈가 된지 얼마 지나지 않아, 그 원리를 깊게 알고 있지 않아도 그 기술을 자유 자재로 활용할 수 있는 시대가 벌써 도래한 것 같다. 세미나에서는 이를 **기술의 민주화** 라는 단어로 표현하셨는데, 앞으로도 이런 기술들이 보편화 되었으면 좋겠다는 생각이 든다.