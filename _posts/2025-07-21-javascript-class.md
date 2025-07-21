---
title: "[JavaScript] 클래스"
excerpt: "JavaScript ES6 클래스 문법과 기본 사용법"

categories:
  - JavaScript
tags:
  - [JavaScript]

permalink: /javascript/class

toc: true
toc_sticky: true

date: 2025-07-21T00:00:00
last_modified_at: 2025-07-21T14:00:00
---

JavaScript로 클래스 문법을 사용해 객체를 만들고 관리하는 방법을 알아보고자 한다.

---

# 🏫 클래스란?

클래스는 같은 종류의 객체를 만들기 위한 틀이다.

책이라는 개념을 프로그램으로 만든다면, 이 클래스로부터 여러 권의 책 객체를 생성할 수 있다.

각 책 객체는 제목, 저자 같은 공통된 속성과 책을 열고 읽는 행동을 가질 수 있다.

```js
class Book {
  constructor(title, author) {
    this.title = title; // 속성: 제목
    this.author = author; // 속성: 저자
  }

  open() {
    // 행동: 열기
    console.log(`${this.title}을(를) 펼쳤습니다.`);
  }
}

// 책 객체 만들기
const book1 = new Book("자바스크립트 입문", "김개발");
const book2 = new Book("파이썬 기초", "박코딩");

book1.open(); // "자바스크립트 입문을(를) 펼쳤습니다."
book2.open(); // "파이썬 기초을(를) 펼쳤습니다."
```

하나의 클래스로 여러 개의 비슷한 객체를 쉽게 만들 수 있다.

# 📝 기본 문법

## 🚀 생성자 (Constructor)

`constructor`는 객체를 만들 때 자동으로 실행되는 초기화 함수이다. 여기서 객체의 초기값을 설정한다.

```js
class Book {
  constructor(title, pages) {
    console.log("새로운 책이 생성됩니다!");
    this.title = title;
    this.pages = pages;
    this.currentPage = 1; // 기본값 설정
  }
}
```

생성자의 이름은 반드시 `constructor`여야 하며, 다른 이름은 사용할 수 없다.

## 🔧 메서드 (Method)

클래스 내부에 정의한 함수로, 객체가 수행할 수 있는 행동을 의미한다.

메서드는 객체의 속성에 접근해서 상태를 변경하거나 작업을 수행할 수 있다.

```js
class Book {
  read(pageCount) {
    this.currentPage += pageCount;
    console.log(`${pageCount}페이지를 읽었습니다.`);
  }
}

const book = new Book("자바스크립트 입문", 200);
book.read(50); // "50페이지를 읽었습니다."

book.read(30); // 30페이지 더 읽기
```

메서드는 그 객체만의 데이터를 사용할 수 있다.

## 🔒 Private 필드

`#`을 붙이면 외부에서 접근할 수 없는 비공개 속성을 만들 수 있다.

객체 내부에서만 사용 가능하고, 외부에서 직접 변경하는 것을 막아 데이터 보호에 효과적이다.

```js
class Book {
  #bookmark; // 비공개 속성

  constructor(title) {
    this.title = title;
    this.#bookmark = 1;
  }
}
```

책갈피 위치같이 외부에서 함부로 바꾸면 안 되는 데이터를 보호할 때 사용한다.

외부에서 `#bookmark`에 직접 접근하면 에러가 발생한다.

## 📌 Static (정적) 메서드

`static`을 붙이면 클래스 자체에서 바로 사용할 수 있는 메서드가 된다.

이 메서드는 객체를 생성하지 않고도 바로 호출할 수 있다.

```js
class Book {
  static library = "중앙도서관";

  static comparePages(book1, book2) {
    // ...
  }
}
```

보통 공통된 기능이나 헬퍼 함수, 유틸리티 함수에 사용한다.

---

클래스는 비슷한 객체들을 체계적으로 만들고 관리하는 도구이다.

클래스를 사용하면 코드가 더 깔끔해지고 재사용성이 높아지므로, 클래스를 활용해 효율적으로 코드를 작성해보자!
