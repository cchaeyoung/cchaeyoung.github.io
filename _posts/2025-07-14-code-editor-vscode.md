---
title: "[Code Editor] VS Code 시작하기"
excerpt: "VS Code의 주요 특징과 기본 기능"

categories:
  - Code Editor
tags:
  - [Code Editor]

permalink: /code-editor/vscode

toc: true
toc_sticky: true

date: 2025-07-14
last_modified_at: 2025-07-20T20:00
---

코드 에디터인 VS Code의 기본 기능에 대해 알아보고자 한다.

---

# 💻 VS Code란?

**VS Code(Visual Studio Code)** 는 마이크로소프트에서 개발한 무료 코드 에디터다. 단순한 텍스트 에디터를 넘어서 통합 개발 환경(IDE)의 기능을 제공하고 현재 전 세계 개발자들에게 가장 인기 있는 에디터 중 하나다.

## ⚡ VS Code의 주요 특징

- **가볍고 빠름**: 일렉트론 기반임에도 불구하고 빠른 시작 속도와 반응성을 제공한다.

- **확장성**: 수만 개의 확장 프로그램을 통해 거의 모든 언어와 프레임워크를 지원한다.

- **통합 터미널**: 별도의 터미널 프로그램 없이 에디터 내에서 명령어를 실행할 수 있다.

- **Git 통합**: Git 기능이 기본적으로 내장되어 있어 버전 관리를 쉽게 할 수 있다.

---

# 🚀 주요 기능

- **인텔리센스**

  **VS Code**는 코드 작성 중에 자동 완성, 매개변수 정보, 빠른 정보 등을 제공한다. 변수를 입력하다 보면 자동으로 변수명이 제안되는 등 정보가 **자동으로 표시**된다.

  이런 기능 덕분에, 일일이 기억하지 않아도 되고 오타나 실수를 줄일 수 있어 매우 편리하다!!

  ![intellisense](/assets/images/posts_img/code-editor/intellisense.png)

  위 예시처럼 `console.l`만 입력해도 자동으로 `console.log`가 추천되어 빠르게 작업할 수 있다.

- **통합 터미널**

  **VS Code**는 에디터 내부에 **터미널**을 제공한다.

  코드 창 하단에서 바로 명령어를 실행하거나 프로그램을 실행할 수 있다.

  ![terminal](/assets/images/posts_img/code-editor/terminal.png)

  위와 같이 `test.js` 파일에 작성한 코드를 `node test.js` 명령어로 실행하면 "Hello" 출력 결과를 즉시 확인할 수 있다.

- **멀티 커서**

  `Alt` 키를 누른 채 마우스로 여러 위치를 클릭하면 동시에 **여러 줄에 커서를 생성**할 수 있다. 같은 내용을 여러 줄에 입력하거나 수정할 때 매우 유용하다.

  ![cursor](/assets/images/posts_img/code-editor/cursor.png)

- **코드 접기/펼치기**

  VS Code는 함수, 객체, 조건문 등의 블록 구조에 대해 접기/펼치기 기능을 제공한다.

  긴 코드를 정리하고 필요한 부분만 집중해서 볼 수 있어 코드 가독성이 높아진다.

  - 펼친 상태

    ![unfold](/assets/images/posts_img/code-editor/unfold.png)

  - 접은 상태

    ![fold](/assets/images/posts_img/code-editor/fold.png)

---

VS Code는 강력한 기본 기능만으로도 개발 생산성을 크게 향상시켜준다.

추가로 확장 프로그램을 활용하면 더욱 편리하게 코드를 작성할 수 있다.

VS Code와 함께 효율적인 코딩을 시작해보자!
