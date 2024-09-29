---
title: "[TypeScript] 타입스크립트 기본 데이터 타입"
excerpt: "타입스크립트의 기본 데이터 타입에 대한 설명과 예시"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/basic-types/

toc: true
toc_sticky: true

date: 2024-09-20
last_modified_at: 2024-09-24
---

# 🧩 기본 타입

- **`string`**
- **`number`**
- **`boolean`**
- **`object`**
- **`Array`**
- **`tuple`**
- **`any`**
- **`null`**
- **`undefined`**

## 1. `string` ✍️

`string` 타입은 문자 데이터를 나타낸다. 작은따옴표(`'`), 큰따옴표(`"`), 또는 백틱(`` ` ``)을 사용하여 문자열을 정의할 수 있다.

```typescript
let greeting: string = "Hello, TypeScript!";
let name: string = "chaeyoung";
```

## 2. `number` 🔢

`number` 타입은 정수와 실수를 모두 포함하는 숫자 데이터를 나타낸다.

```typescript
let age: number = 20;
let height: number = 6.5;
```

## 3. `boolean` ✅

`boolean` 타입은 논리형 타입으로, true 또는 false 값을 가질 수 있다. 주로 조건문에서 사용된다.

```typescript
let isActive: boolean = true;
let hasAccess: boolean = false;
```

## 4. `object` 🏗️

`object` 타입은 객체 데이터 구조를 나타낸다. 배열이나 함수도 포함된다.

```typescript
let user: object = {
  name: "Bob",
  age: 25,
};
```

## 5. `Array` 📋

`Array` 타입은 여러 값을 저장할 수 있는 배열을 나타낸다. 대문자 `Array`로 표기해야 한다.

- 문자열 요소만 담긴 배열

```typescript
let fruits: Array<string> = ["apple", "banana", "orange"];
// 또는
let fruits: string[] = ["apple", "banana", "orange"];
```

- 숫자 요소만 담긴 배열

```typescript
let numbers: Array<number> = [1, 2, 3, 4, 5];
// 또는
let numbers: number[] = [1, 2, 3, 4, 5];
```

- 문자와 숫자가 섞인 배열

```typescript
let mixed: Array<string | number> = ["apple", 1, "banana", 2];
// 또는
let mixed: (string | number)[] = ["apple", 1, "banana", 2];
```

## 6. `tuple` 📏

`tuple` 타입은 고정된 수의 요소를 가질 수 있는 배열이다. 각 요소는 서로 다른 타입을 가질 수 있다.

```typescript
let person: [string, number] = ["Alice", 30];
```

## 7. `any` 🔄

`any` 타입은 타입 검사를 무시할 수 있게 해주고 모든 타입을 허용하겠다는 의미이다. 다양한 타입의 값을 가질 수 있지만, 사용하는 것은 권장되지 않는다. 대신, 구체적인 타입을 사용하는 것이 좋다. 하지만 잘 활용하면 자바스크립트와 같은 유연함을 유용하게 사용할 수 있다.

```typescript
let uncertain: any = 42;
uncertain = "Now I'm a string!";
```

## 8. `null` ❌

`null` 타입은 "값이 없음"을 나타내는 타입이다. 값이 없을 경우 명시적으로 `null`을 사용해야 한다.

```typescript
let emptyValue: null = null;
```

## 9. `undefined` 🔍

`undefined` 타입은 변수가 선언되었지만 값이 할당되지 않은 상태를 나타냅니다. 변수의 기본값은 `undefined`입니다.

```typescript
let notAssigned: undefined = undefined;
```

각 타입의 특성과 사용법을 잘 이해하고 활용함으로써 더욱 효율적이고 안정적인 코드를 작성할 수 있다.
