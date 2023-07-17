---
layout: single
title: "useContext"
categories: code
tags: React-Hook
toc: true
author_profile: false
sidebar:
nav: "counts"
---

## useContext와 Context API

리액트는 component Tree 형태이며
일반적으로는 부모 컴포넌트가 자식 컴포넌트에
prop을 전달하는 형식이다.

그러나 이러한 방식이 전역에 전달해야 하는 prop의 경우
매우 비효율적인 방법이 된다.

이것을 해결하기 위해 사용하는 것이 바로 Context API이다

### Context API

context는 앱 안에서 전역적으로 사용되는 데이터들을
여러 컴포넌트들끼리 쉽게 공유할 수 있는 방법을 제공해준다

이에 props Drilling처럼 최하위 컴포넌트에 prop를 전달하기 위해
그 prop가 필요하지 않은 컴포넌트들에도 데이터를 입력하는 방식을
벗어나 앱 컴포넌트에서 데이터를 등록하고
useContext를 이용해 그 데이터를 꺼내 사용하면 된다.

그러나 이렇게 만병통치약 같은 context 마구 남발해선 안된다.

### Context 는 꼭 필요할때만!

context를 사용하면 컴포넌트를 재사용하기 어려워 질 수 있다.
Prop drilling을 피하기 위한 목적이라면 Component Composition(컴포넌트 합성)
을 먼저 고려해보자

## useContext

### App.js

```javascript
import React, { useState, useRef, useEffect } from "react";
import Page from "./components/Page";
import { ThemeContext } from "./context/ThemeContext";

export default function App() {
  const [isDark, setIsDark] = useState(false);

  return (
    <ThemeContext.Provider value={{ isDark, setIsDark }}>
      <Page />
    </ThemeContext.Provider>
  );
}
```

### ThemeContext

```javascript
import { createContext } from "react";

export const ThemeContext = createContext(null);
```

### Page.js

```javascript
import Content from "./Content";
import Footer from "./Footer";
import Header from "./Header";

const Page = () => {
  return (
    <div className="page">
      <Header />
      <Content />
      <Footer />
    </div>
  );
};

export default Page;
```

### Header.js

```javascript
import React, { useContext } from "react";
import { ThemeContext } from "../context/ThemeContext";

export default function Header() {
  const { isDark } = useContext(ThemeContext);
  return (
    <header
      style={{
        backgroundColor: isDark ? "black" : "lightgray",
        color: isDark ? "white" : "black",
      }}
    >
      <h1>Welcome 홍길동!</h1>
    </header>
  );
}
```
