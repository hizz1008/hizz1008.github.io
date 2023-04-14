---
layout: single
title: "setInterval, setTimeout"
categories: code
tags: javascript-App
toc: true
author_profile: false
sidebar:
nav: "counts"
---

# jsApp에 시계 추가하기

시계를 추가하기 위해선
interval과 setTimeout이라는 개념을 알아야 한다.

## interval과 setTimeout의 차이점

interval은 "매번" 일어나야 하는 무언가를 말한다.<br>
예를 들어 "매 2초" 라고 하면 이것은 interval이라는 것이다.<br>
즉 매 2초마다 무슨 일이 일어나게 하고 싶을 때 쓰는 것이 interval이다.<br>

interval은 javascript가 해당 라인을 보자마자 실행된다.<br>
그러나 이렇게 바로 실행되는 것을 원하지 않고<br>
몇 초를 기다린 후 실행되길 원한다면 setTimeout을 사용하면 된다.<br>
이 둘은 비슷하게 생겼으나 동작은 완전히 다르다

```javascript
setInterval(함수 이름, 5000);
//이 라인이 시작할 때 함수를 실행한 뒤
//5 초마다 실행된다.
```

```javascript
setTimeout(함수 이름, 5000);
//라인이 시작되고 5초 뒤에 함수를 실행한다.
```

## Date object

자바스크립트에 내장된 메소드로 일, 월, 년, 시간, 분, 초 등 여러가지 정보를 가져올 수 있다.

```javascript
const date = new Date();

date.getDate();
//해당 날짜
```

## 시계 코드

```javascript
const clock = document.querySelector("h2#clock");

function getClock() {
  const date = new Date();
  const houre = String(date.getHours()).padStart(2, "0");
  const minutes = String(date.getMinutes()).padStart(2, "0");
  const seconds = String(date.getSeconds()).padStart(2, "0");
  clock.innerHTML = `${houre}:${minutes}:${seconds}`;
}
getClock();
setInterval(getClock, 1000);
```
