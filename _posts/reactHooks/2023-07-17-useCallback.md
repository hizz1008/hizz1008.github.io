---
layout: single
title: "useCallback"
categories: code
tags: React-Hook
toc: true
author_profile: false
sidebar:
nav: "counts"
---

useCallback 또한 Memoization 기법으로 컴포넌트의 성능을 최적화 하는 기법
useMemo는 자주 쓰이는 값을 캐싱해주어 값이 필요할 때 마다 메모리에서 꺼내와 재사용

useCallback도 똑같다 다만 인자로 전달한 콜백함수 그자체를 Memoization 해준다는 것이다.

```javascript
const calculate = useCallback(
  (num) => {
    return num + 1;
  },
  [item]
);
```

## useCallback이 필요한 이유

```javascript
const someFunction = () => {
  console.log(`some Func: number : ${number}`);
  return;
};

useEffect(() => {
  console.log("someFunction이 변경되었습니다.");
}, [someFunction]);
```

먼저 someFunction이라는 함수를 만들어주고
그것을 useEffect를 이용해 변경이 되었을 때에만 로그가
찍힐 수 있게 코드를 작성했다

### 자바스크립트가 함수를 저장하는 방법

그러나 해당 someFunction의 변경이 아닌 다른 곳에서 변경이 일어나도
useEffect가 실행되는데 그것은

자바스크립트에선 함수를 일급 객체로 취급한다.
함수 내부의 객체는 다른 메모리 공간에 저장되고 함수의 이름이 저장된 메모리 공간의 주소로 할당된다.
그럼으로 변수는 메모리 공간 안에 저장된 객체를 참조하고 있는 것이다.

렌더링이 다시 될 때 함수 안에 객체를 다시 생성해서 또 다른 메모리 공간에 저장이 될 것이고
그럼 그 메모리 주소가 다시 바뀌기 때문에 useEffect가 실행되는 것이다.

결론적으로 함수 내부의 객체 즉 코드가 변하지 않았어도 렌더링이 될 때 새롭게 작성 됨으로
주소도 새로 할당되고 불필요하게 렌더링 되는 것이다
이것을 막기 위해 함수 자체를 Memoiaziton 해주는 것이 useCallback이다.
