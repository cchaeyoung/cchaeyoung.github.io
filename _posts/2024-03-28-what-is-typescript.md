---
title: "[TypeScript] 타입스크립트(TypeScript)란?"
excerpt: "타입스크립트의 정의, 주요 특징 및 활용 방법"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/what-is-typescript/

toc: true
toc_sticky: true

date: 2024-09-20
last_modified_at: 2024-09-22
---

# 📖 TypeScript 정의

TypeScript는 JavaScript에 <mark>타입(type)</mark>을 추가한 **확장 언어**이다. 이는 별도의 새로운 언어가 아니며, 정적 타입을 지원하는 프로그래밍 언어이다.

**마이크로소프트**에 의해 개발되었으며, 개발자가 더 **안전하고 효율적인 코드**를 작성할 수 있도록 돕기 위해 만들어졌다. TypeScript는 최종적으로 JavaScript로 컴파일되어 모든 JavaScript 환경에서 실행될 수 있다.

---

# ✨ TypeScript의 주요 특징

<h2>1. 정적 타입 지정</h2>

TypeScript는 변수와 함수 매개변수에 명시적으로 <mark>타입</mark>을 지정할 수 있다. 컴파일 시 타입 검사를 통해 오류를 사전에 발견할 수 있다.

```typescript
function greet(name: string): string {
  return `Hello, ${name}!`;
}

console.log(greet("World")); // Hello, World!
```

<h2>2. 인터페이스와 타입 별칭</h2>

복잡한 데이터 구조를 정의할 수 있는 <mark>인터페이스와 타입 별칭</mark>을 제공하여 이를 통해 코드의 유지보수성과 확장성을 높일 수 있다.

**인터페이스 예시**

```typescript
interface User {
  name: string;
  age: number;
  email: string;
}

const user: User = {
  name: "Alice",
  age: 30,
  email: "alice@example.com",
};
```

**타입 별칭 예시**

```typescript
type Point = {
  x: number;
  y: number;
};

const point: Point = {
  x: 10,
  y: 20,
};
```

<h2>3. 객체 지향 프로그래밍</h2>

클래스, 상속, 인터페이스 등의 <mark>객체 지향 프로그래밍 기능</mark>을 지원하여 코드의 재사용성과 모듈성을 높일 수 있다.

**클래스 예시**

```typescript
class Animal {
  constructor(public name: string) {}

  makeSound(): void {
    console.log(`${this.name} makes a sound.`);
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog("Buddy");
dog.makeSound(); // Buddy barks.
```

<h2>4. 함수형 프로그래밍</h2>
화살표 함수, 제네릭, 타입 추론 등 <mark>함수형 프로그래밍 기능</mark>을 제공하여 간결하고 표현력 있는 코드 작성이 가능하다.

**화살표 함수 예시**

```typescript
const add = (a: number, b: number): number => a + b;
console.log(add(2, 3)); // 5
```

<h2>5. 강력한 IDE 지원</h2>
Visual Studio Code, WebStorm 등의 <mark>IDE</mark>에서 자동 완성, 타입 힌트, 리팩토링 기능을 제공하여 개발 생산성이 향상된다.

---

# 🌟 TypeScript의 장점

- **코드 품질 향상**: 정적 타입 지정으로 인해 런타임 오류를 줄여 코드의 품질이 향상된다.

- **개발 생산성 증가**: IDE의 자동 완성과 타입 힌트 덕분에 코드 작성 속도가 빨라진다.

- **유지보수 용이**: 명확한 타입 정의와 인터페이스로 인해 코드를 쉽게 유지보수할 수 있다.

- **대규모 프로젝트에 적합**: 강력한 타입 시스템과 모듈화 기능 덕분에 대규모 애플리케이션 개발에 이상적이다.

- **JavaScript와의 호환성**: 기존 JavaScript 코드와 완벽하게 호환되며, 점진적인 마이그레이션이 가능하다.

---

# 💡 TypeScript 활용 방법

- **프레임워크와 라이브러리**: React, Angular, Vue.js 등과 함께 사용하여 더 안전한 컴포넌트를 작성할 수 있다.

- **Node.js**: 서버 측 애플리케이션에서도 TypeScript를 사용하여 타입 안전성을 확보할 수 있다.

- **개발 도구**: ESLint, Prettier 등과 통합하여 코드 품질을 더욱 향상시킬 수 있다.

- **테스트**: Jest와 같은 테스트 프레임워크와 함께 사용하여 타입을 기반으로 한 테스트를 작성할 수 있다.
