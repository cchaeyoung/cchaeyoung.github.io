---
title: "[JavaScript] Node.js 기초"
excerpt: "Node.js의 개념과 브라우저 밖에서 JavaScript를 실행하는 방법"

categories:
  - JavaScript
tags:
  - [JavaScript]

permalink: /javascript/nodejs-basics

toc: true
toc_sticky: true

date: 2025-07-21
last_modified_at: 2025-07-21T15:00
---

브라우저가 아닌 환경에서 JavaScript를 실행할 수 있게 해주는 Node.js에 대해 알아보고자 한다.

---

# 🟢 Node.js란?

<mark>**Node.js**</mark>는 구글의 V8 JavaScript 엔진을 기반으로 만들어진 JavaScript 런타임 환경이다.

원래 JavaScript는 웹 브라우저에서만 실행되는 언어였는데, Node.js 덕분에 서버나 로컬 컴퓨터에서도 JavaScript를 실행할 수 있게 되었다.

**런타임 환경**이란 프로그래밍 언어가 실행되는 환경을 의미한다. 브라우저가 JavaScript의 런타임 환경 중 하나라면 Node.js는 **브라우저 밖에서 JavaScript를 실행할 수 있는 또 다른 런타임 환경**이다.

---

# 💻 Node.js 실행 방법

- **기본 실행**

  `node filename.js` 명령어로 프로그램을 실행할 때마다 Node.js가 내 JavaScript 코드를 읽어서 실행해준다.

  ```bash
  node filename.js
  ```

  `filename`에 실행하고자 하는 파일명을 입력하면 된다.

  ```javascript
  console.log("Hello, Node.js!");

  const name = "개발자";
  const greeting = `안녕하세요, ${name}님`;
  console.log(greeting);
  ```

  ```bash
  node hello.js
  ```

  위의 코드를 입력하고, 터미널에서 `node hello.js`를 입력해 보았다.

  ![hello-example](/assets/images/posts_img/javascript/hello-example.png)

  브라우저 없이도 `console.log()`로 결과를 바로 확인할 수 있어서 매우 편리하다.

- **REPL 모드**

  터미널에서 `node`만 입력하면 대화형 JavaScript 환경이 시작된다.

  ![repl](/assets/images/posts_img/javascript/repl.png)

  REPL 모드는 위처럼 코드를 작성하지 않고도 바로바로 실행 결과를 확인할 수 있어서 빠른 테스트나 실험에 유용하다.

  끝내려면 `Ctrl + C`를 두 번 누르거나 `Ctrl + D`를 누르면 된다.

---

# 🌟 Node.js의 주요 특징

- **V8 엔진과 빠른 성능**

  Node.js는 구글의 V8 JavaScript 엔진을 사용한다. V8 엔진은 **Just-In-Time(JIT) 컴파일** 방식을 사용해서 코드를 실행하는 시점에 기계어로 변환한다.

  이 덕분에 인터프리터 언어임에도 불구하고 상당히 빠른 실행 속도를 보여준다.

- **비동기 I/O**

  Node.js는 이벤트 기반의 **비동기 I/O 모델**을 사용한다.

  파일 읽기, 네트워크 통신 등의 작업을 논블로킹 방식으로 처리할 수 있다.

  ```js
  // 비동기 방식으로 파일 읽기
  const fs = require("fs");

  console.log("파일 읽기 시작!");
  fs.readFile("data.txt", "utf8", (err, data) => {
    if (err) throw err;
    console.log("파일 내용:", data);
  });
  console.log("다른 작업"); // 파일 읽기와 동시에 실행
  ```

- **NPM**

  Node.js에는 오픈소스 패키지 관리자 **NPM(Node Package Manager)**이 있어 다양한 라이브러리를 쉽게 설치하고 사용할 수 있다.

  간단한 명령어로 설치해서 사용할 수 있다.

  ```bash
  npm install express
  npm instal axios
  ```

- **크로스 플랫폼**

  Windows, macOS, Linux 등 다양한 운영체제에서 동일하게 작동한다.

  한 번 작성한 Node.js 코드는 어떤 환경에서든 실행할 수 있다.

---
