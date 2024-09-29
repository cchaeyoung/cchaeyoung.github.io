---
title: "[TypeScript] 타입스크립트의 인터페이스"
excerpt: "인터페이스의 정의, 문법, 기본 사용법, 병합, 상속, 인덱스 시그니처"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/interfaces

toc: true
toc_sticky: true

date: 2024-09-23 10:00:00
last_modified_at: 2024-09-29
---

<mark>인터페이스</mark>는 타입스크립트에서 객체의 구조를 정의하는 강력한 방법이다. 코드의 타입 안정성을 높이고, 명확한 계약을 제공한다.

---

# 📜 인터페이스 정의와 기본 문법

인터페이스는 `interface` 키워드를 사용하여 정의한다. 객체가 가져야 할 프로퍼티와 메서드를 명시한다.

```typescript
interface Person {
  name: string;
  age: number;
  greet(): void;
}

const person: Person = {
  name: "Chaeng",
  age: 25,
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  },
};
```

---

# 🔍 선택적 프로퍼티와 읽기 전용 프로퍼티

프로퍼티 이름 뒤에 `?`를 붙여 **선택적 프로퍼티**를, `readonly` 키워드를 사용하여 **읽기 전용 프로퍼티**를 정의할 수 있다.

```typescript
interface Car {
  readonly brand: string;
  model: string;
  year?: number;
}

const myCar: Car = { brand: "Toyota", model: "Corolla" };
const yourCar: Car = { brand: "Honda", model: "Civic", year: 2022 };
// myCar.brand = "Ford"; // 에러: 읽기 전용 프로퍼티는 재할당할 수 없다.
```

---

# 🌐 인터페이스 확장 (상속)

인터페이스는 다른 인터페이스를 **확장**할 수 있다. 이를 통해 코드 재사용성을 높일 수 있다.

```typescript
interface Animal {
  name: string;
}

interface Pet extends Animal {
  owner: string;
}

const dog: Pet = {
  name: "Buddy",
  owner: "Chaeng",
};
```

---

# 🔗 인터페이스 병합

타입스크립트에서는 같은 이름의 인터페이스를 여러 번 선언할 수 있으며, 이들은 자동으로 **병합**된다.

```typescript
interface Box {
  height: number;
  width: number;
}

interface Box {
  scale: number;
}

let box: Box = { height: 5, width: 6, scale: 10 };
```

이 기능은 라이브러리의 타입 정의를 확장할 때 유용하게 사용될 수 있다.

---

# 📦 인덱스 시그니처

인덱스 시그니처를 사용하면 **동적으로 프로퍼티를 추가**할 수 있는 객체를 정의할 수 있다.

```typescript
interface StringDictionary {
  [key: string]: string;
}

let fruits: StringDictionary = {
  apple: "red",
  banana: "yellow",
  cherry: "red",
};

fruits.grape = "purple"; // 유효
```

인덱스 시그니처는 객체의 모든 프로퍼티가 같은 타입을 가질 때 유용하다.

---

# ⚙️ 함수 타입 인터페이스

인터페이스를 사용하여 **함수의 타입**을 정의할 수 있다.

```typescript
interface MathFunc {
  (x: number, y: number): number;
}

const add: MathFunc = (x, y) => x + y;
const subtract: MathFunc = (x, y) => x - y;
```

---

# 🏷 클래스와 인터페이스

클래스는 인터페이스를 **구현**할 수 있다. 이를 통해 클래스가 특정 구조를 따르도록 강제할 수 있다.

```typescript
interface Printable {
  print(): void;
}

class Book implements Printable {
  constructor(private title: string) {}

  print() {
    console.log(`Printing: ${this.title}`);
  }
}

const book = new Book("TypeScript Guide");
book.print(); // "Printing: TypeScript Guide"
```

---

인터페이스는 타입스크립트에서 코드의 구조와 타입을 정의하는 핵심적인 도구이다. 잘 설계된 인터페이스를 사용하면 코드의 가독성과 유지보수성을 크게 향상시킬 수 있다.
