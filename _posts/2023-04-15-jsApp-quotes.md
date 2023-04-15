---
layout: single
title: "랜덤 명언 표시하기"
categories: code
tags: javascript-App
toc: true
author_profile: false
sidebar:
nav: "counts"
---

# random quotes

변수 quotes를 안에 명언을 배열로 각 10개씩 만들었다.<br>
이것을 호출하기 위해선<br>
0 부터 배열의 길이인 10사이의 숫자들을 랜덤한 형식으로<br>
호출해야 한다.

## Math module

Math 객체는 수학에서 자주 사용하는 상수와 함수들을 미리 구현해 놓은 자바스크립트 표준 내장 객체이다.
생성자가 존재하지 않아서 따로 인스턴스를 생성하지 않더라도 Math 객체의 모든 method나 property를 바로 사용할 수 있다.
<br>
사용할 함수는 random(), round()함수 이다.

### Math.random()

0~1 사이의 랜덤한 숫자를 제공

### Math.round(x)

소수점 첫 번째 자리에서 반올림 후 반환

### Math.ceil(x)

인수와 같거나 큰 수 중에서 가장 작은 정수 반환

### Math.floor(x)

인수와 같거나 작은 수 중에서 가장 큰 정수 반환

```javascript
const quotes = [
  {
    quote: "I never dreamed about success, I worked for it",
    author: "Estee Lauder",
  },
  {
    quote: "Do not try to be original, just try to be good.",
    author: "Paul Rand",
  },
  {
    quote: "Do not be afraid to give up the good to go for the great",
    author: "John D. Rockefeller",
  },
  {
    quote:
      "If you cannot fly then run. If you cannot run, then walk. And if you cannot walk, then crawl, but whatever you do, you have to keep moving forward.",
    author: "Martin Luther King Jr.",
  },
  {
    quote:
      "Our greatest weakness lies in giving up. The most certain way to succeed is always to try just one more time.",
    author: "Thomas Edison",
  },
  {
    quote:
      "The fastest way to change yourself is to hang out with people who are already the way you want to be",
    author: "REid Hoffman",
  },
  {
    quote:
      "Money is like gasoline during a road trip. You do not want to run out of gas on your trip, but you are not doing a tour of gas stations",
    author: "Tim O Reilly",
  },
  {
    quote:
      "Some people dream of success, while other people get up every morning and make it happen",
    author: "Wayne Huizenga",
  },
  {
    quote:
      "The only thing worse than starting something and falling.. is not starting something",
    author: "SEth Godin",
  },
  {
    quote:
      "If you really want to do something, you will find a way. If you do not, you will find an excuse.",
    author: "Jim Rohn",
  },
];

const author = document.querySelector(".author");
const quote = document.querySelector(".quote");

const todaysQuote = quotes[Math.floor(Math.random() * quotes.length)];

quote.innerHTML = todaysQuote.quote;
author.innerHTML = todaysQuote.author;
```

## 코딩

10개의 배열로 이루어진 변수 quotes를<br>
Math module을 이용하여 랜덤한 숫자로 배열을 선택하도록 작성
