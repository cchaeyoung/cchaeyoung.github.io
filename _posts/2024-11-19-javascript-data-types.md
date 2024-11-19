---
title: "[JavaScript] 데이터 타입(Data Types)"
excerpt: "자바스크립트의 데이터 타입과 특징"

categories:
  - JavaScript
tags:
  - [JavaScript]

permalink: /javascript/javascript-data-types/

toc: true
toc_sticky: true

date: 2024-11-19 22:00:00
last_modified_at: 2024-11-19

---

# 📚 데이터 타입이란?

데이터 타입은 프로그래밍에서 다루는 데이터의 종류를 의미한다. 자바스크립트의 데이터 타입은 크게 **원시 타입(Primitive Type)**과 **참조 타입(Reference Type)**으로 구분된다.

---

# 💫 원시 타입 (Primitive Types)

원시 타입은 가장 기본적인 데이터 형태를 의미하며, 변수에 값이 직접 저장된다.

## 🔢 Number

자바스크립트에서 `Number` 타입은 정수와 실수를 구분하지 않는 하나의 숫자 타입이다. 부동소수점 형식을 따르며, 정수, 실수뿐만 아니라 `Infinity`와 `NaN`(Not a Number) 값도 표현할 수 있다.

```javascript
let integer = 10; // 정수
let float = 10.5; // 실수
let infinity = Infinity; // 양의 무한대
let naN = NaN; // Not a Number
```

## 📝 String

`String` 타입은 텍스트 데이터를 나타내는 타입이다. **작은따옴표('')**, **큰따옴표("")**, 또는 **백틱(``)**을 사용하여 문자열을 정의할 수 있으며, 특히 백틱을 사용한 템플릿 리터럴은 문자열 내에 변수나 표현식을 쉽게 삽입할 수 있게 해준다.

```javascript
let single = '작은따옴표';
let double = "큰따옴표";
let template = `템플릿 리터럴: ${single}`; // 템플릿 리터럴 사용
```

## ✅ Boolean

`Boolean` 타입은 `true`와 `false` 두 가지 값만 가질 수 있는 논리 타입이다. 주로 조건문에서 사용되며, 특정 조건의 참/거짓을 판단할 때 사용된다.

```javascript
let isTrue = true;
let isFalse = false;
```

## ❓ Null & Undefined

자바스크립트에서 **'값이 없음'**을 나타내는 두 가지 특별한 타입이다. `null`은 의도적으로 값이 없음을 나타낼 때 사용하며, `undefined`는 값이 할당되지 않은 상태를 나타낸다.

```javascript
let nullValue = null;
let undefinedValue; // 값을 할당하지 않으면 undefined
```

## 🔐 Symbol

`Symbol`은 ES6에서 추가된 원시 타입으로, 유일한 식별자를 만들 때 사용된다. `Symbol`로 생성된 값은 고유하며, 동일한 설명을 가진 `Symbol`이라도 서로 다른 값으로 취급된다.

```javascript
const symbol1 = Symbol("description");
const symbol2 = Symbol("description");
console.log(symbol1 === symbol2); // false
```

---

# 🔄 참조 타입 (Reference Types)

참조 타입은 여러 개의 값을 하나의 단위로 구성한 복합 데이터 타입이다.

## 📦 Object

`Object`는 키와 값으로 구성된 프로퍼티들의 집합이다. 자바스크립트에서 가장 기본적인 참조 타입으로, 다양한 데이터를 하나의 단위로 구조화하여 저장할 수 있다.

```javascript
const person = {
  name: "John",
  age: 30,
  isMarried: false,
};

console.log(person.name); // 'John'
console.log(person["age"]); // 30
```

## 📋 Array

`Array`는 여러 개의 값을 순차적으로 나열한 자료구조이다. 자바스크립트의 배열은 서로 다른 타입의 요소도 하나의 배열에 포함될 수 있다.

```javascript
const mixedArray = ["apple", 42, true, { name: "John" }];
console.log(mixedArray[0]); // "apple" (문자열)
console.log(mixedArray[1]); // 42 (숫자)
console.log(mixedArray.length); // 4
```

## ⚙️ Function

`Function`은 실행 가능한 코드 블록을 정의한 객체이다. 자바스크립트에서 함수는 일급 객체로 취급되어 변수에 할당할 수 있고, 다른 함수의 매개변수로 전달하거나 반환값으로 사용할 수 있다.

```javascript
function add(a, b) {
  return a + b;
}

const multiply = function (a, b) {
  return a * b;
};

const calculate = function (func, a, b) {
  return func(a, b);
};
```

---

# 🔍 타입 확인하기

자바스크립트에서는 `typeof` 연산자를 사용하여 데이터 타입을 확인할 수 있다.

```javascript
console.log(typeof 42); // "number"
console.log(typeof "Hello"); // "string"
console.log(typeof true); // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof null); // "object"
console.log(typeof {}); // "object"
console.log(typeof []); // "object"
console.log(typeof function () {}); // "function"
```

💡 **`typeof null`**이 `"object"`를 반환하는 이유는 자바스크립트 초기 설계의 **버그**로, 지금도 그대로 유지되고 있다.

---

# ⚖️ 원시 타입 vs 참조 타입

- **원시 타입**
  - 값이 직접 저장됨
  - 값의 복사가 이루어짐
  - 불변성(Immutability)을 가짐

- **참조 타입**
  - 값의 참조(메모리 주소)가 저장됨
  - 참조의 복사가 이루어짐
  - 가변성(Mutability)을 가짐

```javascript
// 원시 타입
let x = 10;    // 값이 직접 저장됨
let y = x;     // x의 값을 복사
x = 20;        // x를 변경해도 y에는 영향 없음
console.log(x); // 20
console.log(y); // 10

// 참조 타입
let obj1 = { value: 10 };  // 참조 주소 저장
let obj2 = obj1;           // obj1의 참조를 복사
obj1.value = 20;           // obj1의 값을 변경하면 obj2도 영향을 받음
console.log(obj1.value); // 20
console.log(obj2.value); // 20
```
