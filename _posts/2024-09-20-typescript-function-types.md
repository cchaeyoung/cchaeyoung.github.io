---
title: "[TypeScript] 함수 타입"
excerpt: "타입스크립트 함수 타입의 정의, 매개변수와 반환값 타입 지정, 선택적 매개변수, 기본 매개변수, 나머지 매개변수, 콜백 함수, 그리고 화살표 함수의 타입 지정"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/function-types

toc: true
toc_sticky: true

date: 2024-09-20
last_modified_at: 2024-09-29
---

# 🛠 타입스크립트에서 함수 타입

타입스크립트에서는 **함수의 타입**을 정의할 수 있다. 함수 타입은 **매개변수의 타입**과 **반환값의 타입**을 명시한다.

```typescript
(매개변수1: 타입1, 매개변수2: 타입2, ...) => 반환값 타입
```

예를 들어, 두 개의 숫자를 받아서 그 합을 반환하는 함수의 타입을 정의하면 다음과 같다

```typescript
(a: number, b: number) => number;
```

---

# ✍️ 함수의 매개변수에 타입 지정하기

함수의 **매개변수에 타입을 지정**하여 해당 타입의 값만 전달될 수 있도록 제한할 수 있다. 매개변수 이름 뒤에 **콜론(:)**과 함께 타입을 명시한다.

```typescript
function greet(name: string) {
  console.log(`Hello, ${name}!`);
}

greet("Chaeng"); // Hello, Chaeng!
greet(123); // 에러: 'number' 타입의 인수는 'string' 타입의 매개변수에 할당될 수 없다.
```

---

# 🔙 함수의 반환값에 타입 지정하기

함수의 **반환값에 타입을 지정**하여 해당 타입의 값만 반환되도록 할 수 있다. 함수 선언의 매개변수 목록 뒤에 **콜론(:)**과 함께 반환값의 타입을 명시한다.

```typescript
function add(a: number, b: number): number {
  return a + b;
}

const result = add(3, 4); // result의 타입은 number
```

---

# 🎯 선택적 매개변수와 기본 매개변수

## ❓ 선택적 매개변수 (옵셔널 파라미터)

함수의 매개변수를 **선택적으로** 받을 수 있도록 **옵셔널 파라미터**를 사용할 수 있다. 옵셔널 파라미터는 매개변수 이름 뒤에 **물음표(?)**를 붙여 표시한다.

## ⚙️ 기본 매개변수

타입스크립트에서는 함수의 매개변수에 **기본값을 지정**할 수 있다. 이를 통해 인자가 전달되지 않았을 때 사용할 기본값을 설정할 수 있다.

```typescript
function greet(name: string, age?: number, country: string = "Korea") {
  if (age) {
    console.log(
      `Hello, ${name}! You are ${age} years old. You are from ${country}.`
    );
  } else {
    console.log(`Hello, ${name}! You are from ${country}.`);
  }
}

greet("Chaeng"); // Hello, Chaeng! You are from Korea.
greet("Bob", 25, "Canada"); // Hello, Bob! You are 25 years old. You are from Canada.
```

---

# ➕ 나머지 매개변수 사용하기

타입스크립트에서는 함수의 매개변수로 임의의 개수의 인수를 받을 수 있는 **나머지 매개변수**를 지원한다. 나머지 매개변수는 매개변수 이름 앞에 **점 세 개(...)**를 붙여 표시한다.

```typescript
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}

console.log(sum(1, 2, 3)); // 6
console.log(sum(4, 5, 6, 7)); // 22
```

나머지 매개변수는 배열 형태로 전달되며, 함수 내부에서 배열로 사용할 수 있다.

---

# 🔄 함수 타입과 콜백

**콜백 함수**는 다른 함수에 **인자로 전달되는 함수**이다. 타입스크립트에서는 **콜백 함수의 타입**도 명시적으로 지정할 수 있다.

```typescript
function doSomething(callback: (result: number) => void) {
  const result = 42;
  callback(result);
}

doSomething((num) => {
  console.log(`The result is ${num}`);
});
```

---

# 🏹 화살표 함수와 함수 타입

화살표 함수(Arrow Function)는 **함수를 더 간결하게 작성할 수 있는 방법**을 제공한다. 화살표 함수는 **=>** 기호를 사용하여 정의한다. 화살표 함수의 타입도 일반 함수와 동일한 방식으로 정의할 수 있다.

```typescript
const add = (a: number, b: number): number => {
  return a + b;
};

const multiply = (a: number, b: number): number => a * b;

console.log(add(3, 4)); // 7
console.log(multiply(3, 4)); // 12
```

위의 예시에서 **add 함수**는 **중괄호({})**를 사용하여 함수 본문을 정의하고 **return** 키워드를 사용하여 값을 반환한다. 반면, **multiply 함수**는 **return** 키워드를 생략하고 함수 본문을 간략하게 작성하였다.
