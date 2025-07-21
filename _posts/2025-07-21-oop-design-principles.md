---
title: "[OOP] 객체지향 설계 원칙(SOLID)"
excerpt: "SOLID 원칙과 좋은 객체 설계 가이드라인"

categories:
  - Software Engineering
tags:
  - [Software Engineering]

permalink: /software-engineering/oop-design-principles

toc: true
toc_sticky: true

date: 2025-07-21
last_modified_at: 2025-07-21T14:00
---

좋은 객체지향 설계란 무엇일까?

---

# 왜 설계 원칙이 필요한가?

코드는 한 번 작성하고 끝나는 것이 아니다.

시간이 지나면서 기능 추가, 버그 수정, 요구사항 변경이 반복적으로 발생한다.

**좋은 설계**는 변경이 쉽지만, **나쁜 설계**라면 작은 변경에도 많은 부분을 수정해야 한다.

1️⃣ 하나의 클래스가 너무 많은 책임을 가지고 있거나,  
2️⃣ 변경 이유가 여러 가지 섞여 있거나,  
3️⃣ 다른 곳에서 재사용하기 어려운 구조라면,

이러한 설계는 유지보수를 어렵게 만든다.

따라서 **객체지향 설계 원칙**을 따르는 것이 중요하다.

# 💡 SOLID 원칙

SOLID는 객체지향 설계의 5가지 핵심 원칙이다.

## 🅢 단일 책임 원칙

`SRP: Single Responsibility Principle`

**하나의 클래스**는 **하나의 목적**을 위해서 생성되며, 클래스가 제공하는 모든 서비스는 **하나의 책임**을 수행하는 데 집중되어 있어야 한다는 원칙이다.

> 하나의 클래스는 하나의 일만 해야 한다.

```js
class Book { ... }        // 책 내용 관리
class BookPrinter { ... } // 출력 책임
class BookSaver { ... }   // 저장 책임
```

각 클래스는 단 하나의 책임만 가지므로, 유지보수와 테스트가 쉬워진다.

## 🅞 개방 폐쇄 원칙

`OCP: Open-Closed Principle`

소프트웨어 구성요소(컴포넌트, 클래스, 모듈, 함수)는 확장에는 열려있고, 변경에는 닫혀있어야 한다는 방식이다.

> 새로운 기능을 추가할 때 기존 코드는 수정하지 말고, 새로운 코드를 수정해라.

```js
class Book {
  read() {
    throw new Error("구현 필요");
  }
}

class PaperBook extends Book {
  read() {
    return "종이책을 읽습니다";
  }
}

class EBook extends Book {
  read() {
    return "전자책을 읽습니다";
  }
}
```

새로운 책 타입을 추가할 때 기존 `Book` 클래스를 수정하지 않고 확장할 수 있다.

## 🅛 리스코프 치환의 원칙

`LSP: Liskov Substitution Principle`

서브 타입(상속받은 하위 클래스)은 어디서나 자신의 기반 타입(상위 클래스)로 교체할 수 있어야 한다는 원칙이다.

> 부모 클래스 대신 자식 클래스를 사용해도 문제없어야 한다.

```js
class Book {
  open() {
    return true;
  }
}

class DigitalBook extends Book {
  open() {
    console.log("앱을 실행합니다");
    return true; // 동일한 결과 반환
  }
}
```

`Book`을 사용하는 코드가 `DigitalBook`으로 대체되어도 동일하게 동작한다.

## 🅘 인터페이스 분리의 원칙

`ISP: Interface Segregation Principle`

한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 원칙이다.

> 필요하지 않은 기능을 강제로 구현하게 하지 마라.

```js
class Readable {
  read() {}
}

class Listenable {
  listen() {}
}

class EBook extends Readable {
  /* 읽기만 */
}
class AudioBook extends Listenable {
  /* 듣기만 */
}
```

각 클래스가 자신에게 필요한 기능만 구현하므로 불필요한 의존성이 줄어든다.

## 🅓 의존성 역전의 원칙

`DIP: Dependency Inversion Principle`

객체에서 어떤 클래스를 참조해서 사용하는 경우, 그 클래스를 직접 참조하는 것이 아니라 그 대상의 상위 요소인 추상 클래스나 인터페이스로 참조하라는 원칙이다.

> 구체적인 것보다 추상적인 것에 의존해라

```js
class Book {
  constructor(title, storage) {
    this.title = title;
    this.storage = storage; // 어떤 저장소든 사용 가능
  }

  save() {
    this.storage.save(this.title);
  }
}
```

`Book` 클래스는 구체적인 저장소가 아닌 저장소 인터페이스에 의존하므로 저장 방식을 자유롭게 바꿀 수 있다.

---

이처럼 SOLID 원칙을 지키면 변경에 유연하고, 확장하기 쉬우며, 이해하기 쉬운 코드를 만들 수 있다.
