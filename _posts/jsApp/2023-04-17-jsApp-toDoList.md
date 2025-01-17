---
layout: single
title: "TO Do List"
categories: code
tags: javascript-App
toc: true
author_profile: false
sidebar:
nav: "counts"
---

# To Do List 만들기

이번엔 일정을 작성할 수 있는 기능을 추가할 것이다.

폼에 일정을 작성하면 그 일정이 추가되는 방식으로
제작할 것이다.

```javascript
const toDoForm = document.querySelector("#todo-form");
const toDoInput = toDoForm.querySelector("input");
const toDoList = document.querySelector("#todo-list");

function paintToDo(newTodo) {
  const li = document.createElement("li");
  const span = document.createElement("span");
  li.appendChild(span);
  span.innerHTML = newTodo;
  toDoList.appendChild(li);
}

function handleToDoSubmit(e) {
  e.preventDefault();
  const newTodo = toDoInput.value;
  toDoInput.value = "";
  paintToDo(newTodo);
}

toDoForm.addEventListener("submit", handleToDoSubmit);
```

# 코드

form안 input에 작성된 값을 newTodo라는 변수로 저장<br>
js를 이용해 li>span 형식으로 작성하기 위해<br>
createElement로 각각 생성한 뒤<br>
appendChild를 이용해 자식요소로 지정<br>
생성된 변수들을 appendChild를 이용해 toDoList에 자식요소로 대입<br>

## 문제점

list에 item들을 추가할 수 있지만,
지울 수 없는 점
새로고침이 되면 모든 item들이 사라진다는 점

# toDo를 삭제하는 button 추가하기

```javascript
const toDoForm = document.querySelector("#todo-form");
const toDoInput = toDoForm.querySelector("input");
const toDoList = document.querySelector("#todo-list");

function deleteToDo(e) {
  const li = e.target.parentElement;
  li.remove();
}

function paintToDo(newTodo) {
  const li = document.createElement("li");
  const span = document.createElement("span");
  span.innerHTML = newTodo;
  const btn = document.createElement("button");
  btn.innerHTML = "❌";
  btn.addEventListener("click", deleteToDo);
  li.appendChild(span);
  li.appendChild(btn);
  toDoList.appendChild(li);
}

function handleToDoSubmit(e) {
  e.preventDefault();
  const newTodo = toDoInput.value;
  toDoInput.value = "";
  paintToDo(newTodo);
}

toDoForm.addEventListener("submit", handleToDoSubmit);
```

## 코드

변수 btn을 createElement로 생성하고<br>
appendChild로 li에 자식요소로 지정한다<br>
btn이 클릭 되었을 때 해당 item이 지워질 수 있게
이벤트 리스너와 함수 추가<br>
여기서 문제가 어떠한 item들이 클릭 되었는지 알기 위해<br>
this의 부모노드의 정보를 가져오고 해당 부모를 삭제<br>

# 번외
처음 submit을 했을 때 item이 추가되고<br>
그 다음 item을 추가하기 위해 submit을 했을 때<br>
deleteToDo 함수까지 실행이 되어서<br>
다음 item이 추가되는 것이 아닌<br>
해당 item이 삭제되는 현상이 발생했다.<br>

무엇이 문제인지 찾아봤으나 javascript 파일엔 문제가 없다고 판단<br>

HTMl파일을 열어보니<br>

```HTML
    <form id="todo-form">
      <input
        type="text"
        placeholder="Write a To Do and Press Enter."
        required
      />
    <ul id="todo-list"></ul>
    </form>
```

이렇게 해당 form안에 ul이 들어있어 발생한 이슈였다<br>
ul의 자리를 form밖으로 빼내어 주니 해당 이슈는 바로 해결되었다.<br>
