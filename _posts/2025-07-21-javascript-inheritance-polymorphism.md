---
title: "[JavaScript] 상속과 다형성"
excerpt: "JavaScript에서 클래스 상속과 다형성을 구현하는 방법"

categories:
  - JavaScript
tags:
  - [JavaScript]

permalink: /javascript/inheritance-polymorphism

toc: true
toc_sticky: true

date: 2025-07-21T02:00:00
last_modified_at: 2025-07-21T15:00
---

JavaScript **클래스의 상속과 다형성**을 사용해 코드의 재사용성을 높이고 유연한 프로그램을 만드는 방법을 알아보고자 한다.

---

# 📚 상속이란?

**상속**은 기존 클래스의 속성과 메서드를 **자식 클래스가 물려받는 것**이다.

예시로, 모든 책의 공통 기능(제목, 저자, 열기, 닫기)을 가진 `Book` 클래스가 있다면, 이를 상속받아 `EBook`, `AudioBook` 같은 특별한 종류의 책을 만들 수 있다.

```js
class Book {
  constructor(title, author) {
    this.title = title;
    this.author = author;
  }

  read() {
    console.log(`${this.title}을(를) 읽습니다.`);
  }
}

class EBook extends Book {
  constructor(title, author, fileSize) {
    super(title, author); // 부모 생성자 호출
    this.fileSize = fileSize;
  }

  download() {
    console.log(`${this.title} (${this.fileSize}MB)를 다운로드합니다.`);
  }

  read() {
    console.log(`전자책 "${this.title}"을(를) 태블릿으로 읽습니다.`);
  }
}

const ebook = new EBook("JS 입문", "김코드", 10);
ebook.read(); // 부모 메서드
ebook.download(); // 자식 고유 메서드
```

`EBook`은 `Book`의 **모든 기능을 물려받으면서** 동시에 **자신만의 기능(`download`)을 추가**할 수 있다.

이렇게 상속을 통해 중복 코드를 줄이고, 새로운 기능을 쉽게 추가할 수 있다.

---

# 🔗 extends와 super

- `extends`는 다른 클래스를 상속받을 때 사용한다.

- `super`는 부모 클래스의 생성자나 메서드를 호출할 때 사용한다.

```js
class AudioBook extends Book {
  constructor(title, author, duration) {
    super(title, author);
    this.duration = duration;
  }

  read() {
    console.log(
      `오디오북 "${this.title}"을(를) ${this.duration}분 동안 듣습니다.`
    );
  }
}
```

`super()`는 생성자에서 반드시 먼저 호출해야 하며, `super.메서드()`는 부모의 기능을 활용할 때 사용된다.

---

# 🎭 메서드 오버라이딩

메서드 오버라이딩은 **부모 클래스의 메서드를 자식 클래스에서 다시 정의하는 것**이다.

```js
class PaperBook extends Book {
  read() {
    console.log(`종이책 "${this.title}"을(를) 펼쳐 읽습니다.`);
  }
}
```

**같은 메서드 이름(`read()`)** 이지만 **각 클래스에 따라 동작이 달라진다.**

---

# 🌟 다형성이란?

다형성은 같은 메서드 호출이 **객체의 타입**에 따라 다르게 동작하는 능력이다.

```js
function startReading(book) {
  book.read(); // 어떤 책이든 read()만 호출
}

const books = [
  new Book("기본책", "홍길동"),
  new EBook("전자책", "이코드", 15),
  new PaperBook("소설책", "박문학"),
  new AudioBook("오디오북", "김보이스", 90),
];

books.forEach(startReading);
```

**같은 `read()` 메서드를 호출**하지만, **각 객체의 종류에 따라 다르게 동작**한다. 이것이 다형성이다.

---

상속과 다형성을 활용하면 **코드의 재사용성을 높이고**, **새로운 기능을 쉽게 추가할 수 있으며**, **유지보수가 간편한** 프로그램을 만들 수 있다!
