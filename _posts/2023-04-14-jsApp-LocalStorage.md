---
layout: single
title: "LocalStorage"
categories: code
tags: javascript-App
toc: true
author_profile: false
sidebar:
nav: "counts"
---

# LocalStorage란?

유저의 아이디를 저장하는 것은 매우 흔한 일이다.
그러니 당연하게도 API가 존재하는데
LocalStorage라는 API이다.

## 사용 할 메소드

많은 메소드 중 우리가 사용할 메소드는 setItem이다.

```javascript
localStorage.setItem("username","jun)
//이런 식으로 키, 값을 저장할 수 있다.
```

.setItem : 값을 저장
.getItem : 값을 불러옴
.removeItem : 값을 삭제함

localStorage에 값을 저장했다면
이제 새로고침을 해도 유저 아이디가 삭제되지 않는 함수를 작성하면 된다.

```javascript
function onLoginSubmit(e) {
  e.preventDefault();
  loginForm.classList.add(HIDDEN_CLASSNAME);
  const username = loginInput.value;
  localStorage.setItem(USERNAME_KEY, username);
  paintGreetings(username);
}

function paintGreetings(username) {
  greeting.innerText = `Hello ${username}`;
  greeting.classList.remove(HIDDEN_CLASSNAME);
}

const savedUsername = localStorage.getItem(USERNAME_KEY);

if (savedUsername === null) {
  loginForm.classList.remove(HIDDEN_CLASSNAME);
  loginForm.addEventListener("submit", onLoginSubmit);
} else {
  paintGreetings(savedUsername);
}
```

## 코드 설명

함수는 이렇게 세 가지이다.
첫 번째 onLoginSubmit 함수는 로그인폼이 submit 되었을 때 실행되며 로컬스토리지에
username이라는 키에 값을 입력하여
새로고침이 되어도 유저의 아이디가 키,값으로 남아있을 수 있게 실행한다.
<br>
두 번째 함수는
매개변수를 활용하여
반복되는 구문을 줄이기 위한 함수이며
유저 아이디를 보여줄 때 실행된다
<br>
세 번째 조건문은
유저 아이디 username키의 값이 존재할 때와 그렇지 않을 때
각각 로그인 폼과 유저 아이디를 보여주는 조건문이다.
