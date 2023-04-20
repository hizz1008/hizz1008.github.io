---
layout: single
title: "Dos에 저장하기"
categories: code
tags: javascript-App
toc: true
author_profile: false
sidebar:
nav: "counts"
---

# To Do list 로컬스토리지에서 추가, 삭제

```javascript
const toDoForm = document.querySelector("#todo-form");
const toDoInput = toDoForm.querySelector("input");
const toDoList = document.querySelector("#todo-list");

const TODOS_KEY = "todos";

let toDos = [];

function saveToDos() {
  localStorage.setItem(TODOS_KEY, JSON.stringify(toDos));
}

function deleteToDo(e) {
  const li = e.target.parentElement;
  li.remove();
  toDos = toDos.filter((toDo) => toDo.id !== parseInt(li.id));
  saveToDos();
}

function paintToDo(newTodo) {
  const li = document.createElement("li");
  li.id = newTodo.id;
  const span = document.createElement("span");
  span.innerHTML = newTodo.text;
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
  const newTodoObj = {
    text: newTodo,
    id: Date.now(),
  };
  toDos.push(newTodoObj);
  paintToDo(newTodoObj);
  saveToDos();
}

toDoForm.addEventListener("submit", handleToDoSubmit);

const savedToDos = localStorage.getItem(TODOS_KEY);

if (savedToDos !== null) {
  const parsedToDos = JSON.parse(savedToDos);
  toDos = parsedToDos;
  parsedToDos.forEach(paintToDo);
}
```

# Dos에 저장하기

to do list를 추가, 삭제할 수 있으나 여전히 새로고침을 하면 모두 사라진다.<br>
이것을 해결하기 위해 앞에서 사용했던 로컬스토리지를 다시 한 번 사용할 것이다.<br>
<br>
toDos라는 배열을 생성하고 함수를 만들어 로컬스토리지<br>
setItem을 사용해 ("todos",toDos)로 저장했다.<br>

## JSON

JSON은 자바스크립트 객체를 표현하기 위한 경량의 데이터 교환 형식으로<br>
JSON은 텍스트로 구성되어 있으며, 쉽게 읽을 수 있고 쉽게 작성할 수 있다<br>
또한, 다양한 프로그래밍 언어에서 사용할 수 있으므로,<br>
서로 다른 플랫폼 간에 데이터를 교환하는 데 사용된다.<br>

### JSON.stringify

todos키의 값이 배열 형식이 아니라 텍스트로 저장된다는 것이다.<br>
이것을 해결하기 위해 <strong>JSON.stringify(xxx)</strong>을 사용했다.<br>

그러나 새로고침을 하면 로컬스토리지엔 남아있지만<br>
화면에 출력이 되지 않는다.<br>

### JSON.parse

자바스크립트에선 단순한 string을 가지고<br>
자바스크립트 오브젝트로 만들어주는 기능이 있다.<br>
<strong>JSON.parse</strong>를 이용해 단순한 배열을<br>
js가 이해할 수 있는 array로 만들 수 있다는 것이다.<br>

## 로컬스토리지 item에 id 할당

화면에 출력된 to do 내용을 삭제할 때 HTML에선 지워지지만<br>
로컬스토리지엔 남아있어 새로고침을 하면 지우기 전으로 돌아가는 문제가 있다.<br>
또한 같은 내용이 있는 item이 있다면 삭제 버튼을 눌렀을 때 어떤 item을<br>
클릭했는지 로컬스토리지에서 알 수 없기에 item에 각각 id를 주기로 했다.<br>

또한 삭제하려 하는 item을 제외하기 위해 .filter메소드를 사용했다<br>
원본 배열을 직접 변경하지 않고 새로운 배열을 반환하는 filter메소드를<br>
사용한 이유는 함수형 프로그래밍의 중요한 개념 중 하나인 불변성을<br>
유지할 수 있기 때문이다.<br>

## 함수형 프로그래밍과 불변성 유지

함수형 프로그래밍은 함수의 조합을 이용해 소프트웨어를 작성하는 것을 강조한다<br>
이는 상태를 변경하지 않고 입력 값, 출력 값 사이의 관계에 집중하는 이론이며<br>
함수의 부작용을 최소화 하려고 하기 때문에 함수가 실행되면서 함수 밖의 상태를 변경하거나,<br>
외부에 영향을 미치는 것을 지양한다.<br>
그렇기 때문에 앞서 얘기한 불변성을 강조하는데<br>
한번 생성된 데이터가 변경되지 않는다는 것을 의미하며<br>
이를 통해 코드의 복잡도를 낮추고<br>
디버깅과 테스트를 쉽게 할 수 있다는 장점이 있다.<br>
