---
title: "[JavaScript] 자바스크립트(JavaScript)란?"
excerpt: "자바스크립트의 정의와 주요 특징, 활용"

categories:
  - JavaScript
tags:
  - [JavaScript]

permalink: /javascript/what-is-javascript/

toc: true
toc_sticky: true

date: 2024-11-18
last_modified_at: 2024-11-18
---

# 📖 JavaScript 정의

JavaScript는 웹 페이지에 <mark>동적 기능</mark>을 추가하기 위해 만들어진 프로그래밍 언어이다. 1995년 넷스케이프에서 개발되었으며, 현재는 웹 브라우저뿐만 아니라 서버(Node.js), 모바일 앱 개발 등 다양한 분야에서 사용되고 있다.

---

# ✨ JavaScript의 주요 특징

<h2>1. 동적 타입 언어</h2>

JavaScript는 변수의 타입을 <mark>자동으로 결정</mark>하는 동적 타입 언어이다.
변수에 값을 할당하면, 해당 값에 맞는 타입으로 자동으로 변환된다.

```javascript
let number = 42; // 숫자
let text = "Hello"; // 문자열
let isTrue = true; // 불리언
let data = null; // null
let empty; // undefined
```

<h2>2. 이벤트 기반 프로그래밍</h2>

사용자의 **클릭**, **키보드 입력** 등 <mark>이벤트</mark>에 반응하여 동작을 수행할 수 있다.

```javascript
document.getElementById("button").addEventListener("click", (e) => {
  console.log("버튼이 클릭되었습니다!");
  console.log("이벤트 타겟:", e.target);
});
```

<h2>3. 비동기 처리</h2>

JavaScript는 <mark>비동기 작업</mark>을 효율적으로 처리할 수 있는 기능을 제공한다. `Promise`와 `async/await`를 사용해 비동기 작업을 동기적으로 처리할 수 있다.

```javascript
async function getData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("데이터 요청 중 오류 발생:", error);
  }
}
```

<h2>4. 일급 객체로서의 함수</h2>

JavaScript에서 함수는 <mark>일급 객체</mark>로 취급된다. 함수를 변수에 할당하거나 다른 함수의 인자로 전달할 수 있다.

```javascript
const sayHello = function (name) {
  return `Hello, ${name}!`;
};

const greet = sayHello;
console.log(greet("World")); // Hello, World!
```

---

# 🌟 JavaScript의 장점

- **쉬운 학습 곡선**: 직관적인 문법으로 초보자도 쉽게 시작할 수 있다.
- **넓은 생태계**: npm을 통해 수많은 라이브러리와 프레임워크를 사용할 수 있다.
- **다양한 활용**: 프론트엔드, 백엔드, 모바일 앱 등 다양한 플랫폼에서 사용 가능하다.
- **실시간 상호작용**: 웹 페이지에 동적 기능을 쉽게 추가할 수 있다.

---

# 💡 JavaScript 활용 분야

<h2>1. 웹 프론트엔드</h2>

- React, Vue.js, Angular 등 프레임워크로 SPA 구축
- DOM 조작과 이벤트 핸들링
- Canvas, WebGL을 사용한 웹 그래픽스/게임 개발
- CSS 애니메이션과 사용자 인터랙션 구현

<h2>2. 백엔드 개발</h2>

- Node.js 기반 서버 애플리케이션
- Express, Nest.js로 REST API 구현
- WebSocket을 활용한 실시간 통신
- MongoDB, MySQL 등 데이터베이스 연동

<h2>3. 모바일 앱 개발</h2>

- React Native로 iOS/Android 네이티브 앱
- Ionic으로 하이브리드 앱
- PWA(Progressive Web App) 구현
