---
title: "[OOP] 객체란 무엇인가? - 객체지향의 본질"
excerpt: "객체의 정의와 객체지향 프로그래밍을 사용하는 이유"

categories:
  - Software Engineering
tags:
  - [Software Engineering]

permalink: /software-engineering/what-is-object

toc: true
toc_sticky: true

date: 2025-07-21T00:00:00
last_modified_at: 2025-07-21T13:00
---

객체지향 프로그래밍을 배울 때 가장 먼저 마주하는 질문은 "객체란 무엇인가?"이다. 단순히 클래스 문법을 익히는 것을 넘어서, 왜 객체를 만들어야 하는지 그 본질을 이해해보자!

---

# 🤔 객체란 무엇인가?

**객체**는 현실 세계의 사물이나 개념을 프로그램에서 표현한 것이다. 객체는 고유한 **상태**와 **행동**을 가지며, 자신만의 **책임**을 담당한다.

- 책: 제목, 저자, 페이지 수(상태) + 펼치기, 넘기기(행동)
- 사람: 이름, 나이(상태) + 걷기, 말하기(행동)
- 스마트폰: 배터리 상태, 앱 목록, 전화번호(상태) + 전화 걸기, 앱 실행, 사진 찍기(행동)

위처럼 주변의 모든 것이 객체가 될 수 있다.

<mark>프로그래밍에서의 객체</mark>는 위 현실 개념을 **코드로 추상화한 구조**이다.

```js
// 책 객체 예시
class Book {
  constructor(title, author, totalPages) {
    this.title = title; // 상태
    this.author = author; // 상태
    this.totalPages = totalPages; // 상태
    this.currentPage = 1; // 상태
    this.isOpened = false; // 상태
  }

  open() {
    // 행동
    this.isOpened = true;
    console.log(`${this.title}을(를) 펼쳤습니다.`);
  }

  nextPage() {
    // 행동
    if (this.isOpened && this.currentPage < this.totalPages) {
      this.currentPage++;
      console.log(`${this.currentPage}페이지로 넘어갔습니다.`);
    }
  }

  close() {
    // 행동
    this.isOpened = false;
    console.log(`${this.title}을(를) 덮었습니다.`);
  }
}

const myBook = new Book("객체지향 프로그래밍", "김개발", 300);
myBook.open(); // 객체에게 메시지 전달
myBook.nextPage(); // 책 객체가 자신의 상태를 변경
```

- `class Book`: 책을 나타내는 클래스 정의
- `constructor`: 책 객체가 생성될 때 초기 상태값(제목, 저자, 총 페이지 수 등) 설정
- 상태: `title`, `author`, `totalPages`, `currentPage`, `isOpened` — 객체가 가지는 데이터(속성)
- 행동(메서드): `open()`, `nextPage()`, `close()` — 객체가 수행하는 기능
- `myBook.open()` 호출 시 객체에게 “책을 펼쳐라”라는 메시지를 보내서 상태를 변경, 동작 수행

---

# ❓ 왜 객체를 만들어야 하는가?

## ⚠️ 절차지향의 한계

**절차지향 프로그래밍**에서는 데이터와 함수가 분리되어 있다.

```js
// 절차지향 방식
let bookTitle = "자바스크립트 입문";
let bookAuthor = "김개발";
let currentPage = 1;
let isOpened = false;

function openBook() {
  isOpened = true;
  console.log(`${bookTitle}을(를) 펼쳤습니다.`);
}

function nextPage() {
  if (isOpened && currentPage < 300) {
    currentPage++;
    console.log(`${currentPage}페이지로 넘어갔습니다.`);
  }
}

openBook(); // 어떤 책을 펼치는 건지 불명확
currentPage = -10; // 데이터가 보호되지 않음
bookTitle = null; // 실수로 데이터 손상 가능
```

위처럼 관련된 데이터와 함수가 흩어져 있어 관계를 파악하기 어렵고, 여러 함수가 같은 데이터를 조작하기 때문에 예상치 못한 부작용이 발생할 수 있다.

## 💡 객체지향의 장점

<mark>객체지향 프로그래밍</mark>는 위의 절차지향의 문제들을 해결한다.

1. **캡슐화**

   ```js
   class Book {
     #currentPage = 1; // private 필드 (외부에서 직접 접근 불가)

     constructor(title, author, totalPages) {
       this.title = title;
       this.author = author;
       this.totalPages = totalPages;
       this.isOpened = false;
     }

     nextPage() {
       if (this.isOpened && this.#currentPage < this.totalPages) {
         this.#currentPage++;
       }
     }

     getCurrentPage() {
       return this.#currentPage;
     }
   }

   const myBook = new Book("자바스크립트 입문", "김개발", 300);
   myBook.nextPage();
   // myBook.#currentPage = 999;  // 에러! 직접 접근 불가
   ```

   이처럼 데이터를 보호하고 안전한 인터페이스만 제공한다.

2. **현실 세계 모니터링**

   ```js
   class Book {
     constructor(title, author, totalPages) {
       this.title = title;
       this.author = author;
       this.totalPages = totalPages;
       this.currentPage = 1;
       this.isOpened = false;
     }

     open() {
       this.isOpened = true;
       console.log(`${this.title}을(를) 펼쳤습니다.`);
     }

     read() {
       if (this.isOpened) {
         console.log(
           `${this.title}의 ${this.currentPage}페이지를 읽고 있습니다.`
         );
       }
     }
   }
   ```

   코드가 직관적이고 현실 세계의 개념과 일치하여 이해하기 쉽다.

3. **재사용성과 확장성**

   ```js
   class EBook extends Book {
     constructor(title, author, totalPages, fileSize) {
       super(title, author, totalPages); // 공통 기능 상속
       this.fileSize = fileSize;
     }

     download() {
       console.log(`${this.title} (${this.fileSize}MB)을(를) 다운로드합니다.`);
     }
   }

   class AudioBook extends Book {
     constructor(title, author, totalPages, duration) {
       super(title, author, totalPages);
       this.duration = duration;
     }

     play() {
       console.log(`${this.title}을(를) 재생합니다. (${this.duration}분)`);
     }
   }
   ```

   공통 기능은 상속하고, 고유 기능만 추가하여 코드 재사용성을 높일 수 있다.

---

# 🎯 객체의 핵심 개념

1. **책임**

   각 객체는 명확한 책임을 가져야 한다.

   ```js
   class Book {
     // 책의 상태와 행동만 책임
     constructor(title, author, totalPages) {
       this.title = title;
       this.author = author;
       this.totalPages = totalPages;
       this.currentPage = 1;
       this.isOpened = false;
     }

     open() {
       /* 책 열기 */
     }
     nextPage() {
       /* 페이지 넘기기 */
     }
     close() {
       /* 책 닫기 */
     }
   }

   class Library {
     // 도서관의 책 관리만 책임
     constructor() {
       this.books = [];
     }

     addBook(book) {
       /* 책 추가 */
     }
     findBook(title) {
       /* 책 찾기 */
     }
     removeBook(title) {
       /* 책 제거 */
     }
   }
   ```

2. **협력**

   객체들은 서로 협력하여 더 큰 기능을 수행한다.

   ```js
   class Reader {
     constructor(name) {
       this.name = name;
       this.currentBook = null;
     }

     borrowBook(library, bookTitle) {
       const book = library.findBook(bookTitle); // Library와 협력
       if (book) {
         this.currentBook = book;
         book.open(); // Book과 협력
         console.log(`${this.name}이(가) ${bookTitle}을(를) 빌렸습니다.`);
       }
     }

     readPage() {
       if (this.currentBook) {
         this.currentBook.nextPage(); // Book 객체에게 작업 위임
       }
     }
   }
   ```

3. **메시지 전달**

   객체는 메서드 호출을 통해 서로 소통한다.

   ```js
   const library = new Library();
   const jsBook = new Book("자바스크립트 입문", "김개발", 300);
   const reader = new Reader("홍길동");

   // 메시지 전달 예시
   library.addBook(jsBook); // Library에게 "책을 추가해줘"
   reader.borrowBook(library, "자바스크립트 입문"); // Reader에게 "책을 빌려줘"
   reader.readPage(); // Reader에게 "페이지를 읽어줘"
   jsBook.close(); // Book에게 "닫혀줘"
   ```

---
