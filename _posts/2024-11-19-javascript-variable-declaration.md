---
title: "[JavaScript] 변수 선언 방식(var, let, const)"
excerpt: "자바스크립트의 변수 선언 방식과 스코프"

categories:
  - JavaScript
tags:
  - [JavaScript]

permalink: /javascript/variable-declaration/

toc: true
toc_sticky: true

date: 2024-11-19
last_modified_at: 2024-11-19
---

# 🔍 변수 선언이란?

변수는 데이터를 저장하는 **컨테이너**이다. 자바스크립트에서는 `var`, `let`, `const` 세 가지 방식으로 변수를 선언할 수 있다.

---

# ⚡️ var

`var`는 자바스크립트에서 가장 오래된 변수 선언 방식이다. `var`로 선언된 변수는 **함수 스코프(function-scoped)**를 가진다. 즉, `var`로 선언된 변수는 선언된 함수 내에서만 유효하며, 함수 외부에서는 접근할 수 없다.

<h2>var의 특징</h2>

- **함수 스코프**: `var`로 선언된 변수는 함수 내부에서만 유효하다. 함수 외부에서는 접근할 수 없다.
- **재선언 가능**: 같은 스코프 내에서 `var`로 선언된 변수는 재선언이 가능하다.
- **호이스팅**: `var`는 호이스팅에 의해 변수 선언이 해당 스코프의 최상단으로 끌어올려진다. 그러나 변수의 초기화는 끌어올려지지 않는다.

```javascript
console.log(name); // undefined
var name = "John"; // 변수 선언 및 초기화
var name = "Jane"; // 재선언 가능
name = "Mike"; // 재할당 가능
console.log(name); // "Mike" 출력

function showName() {
  var userName = "John";
  console.log(userName); // "John" 출력
}
// console.log(userName);     // ReferenceError
```

이 예시는 `var`의 호이스팅과 재선언, 재할당이 가능한 특징을 모두 보여준다.

---

# 🎯 let

`let`은 ES6에서 도입된 변수 선언 방식이다. `let`으로 선언된 변수는 **블록 스코프(block-scoped)**를 가진다. 즉, 변수가 선언된 블록 내에서만 유효하며, 블록 외부에서는 접근할 수 없다.

<h2>let의 특징</h2>

- **블록 스코프**: `let`으로 선언된 변수는 블록 내부에서만 유효하다. 블록 외부에서는 접근할 수 없다.
- **재선언 불가**: 같은 스코프 내에서 이미 선언된 변수를 다시 선언할 수 없다.
- **재할당 가능**: 변수의 값을 변경할 수 있다.

```javascript
let count = 1; // 변수 선언 및 초기화
count = 2; // 재할당 가능
// let count = 3;    // SyntaxError: 재선언 불가능

if (true) {
  let blockScope = "Hello"; // 블록 스코프 내 변수
  console.log(blockScope); // "Hello" 출력
}
// console.log(blockScope);    // ReferenceError
```

이 예시는 `let`의 재할당은 가능하지만 재선언이 불가능하고, 블록 스코프를 가지는 특징을 보여준다.

---

# 🔒 const

`const`는 ES6에서 도입된 상수를 선언하는 키워드이다. `const`로 선언된 변수는 블록 스코프를 가지며, 한 번 할당된 값을 변경할 수 없다.

<h2>const의 특징</h2>

- **블록 스코프**: `const`로 선언된 변수는 블록 내부에서만 유효하다.
- **재선언 불가**: 같은 스코프 내에서 이미 선언된 변수를 다시 선언할 수 없다.
- **재할당 불가**: 한 번 할당된 값을 변경할 수 없다.
  선언과 동시에 초기화: 선언 시 반드시 값을 할당해야 한다.
- **선언과 동시에 초기화 필수**: `const` 변수는 선언 시 반드시 값을 할당해야 한다.

```javascript
const MAX_SIZE = 100; // 상수 선언
// MAX_SIZE = 200;             // TypeError: 재할당 불가
// const MAX_SIZE = 150;       // SyntaxError: 재선언 불가

const user = { name: "John" }; // 객체 선언
user.name = "Jane"; // 객체의 속성은 변경 가능
// user = { name: "Mike" };    // TypeError: 객체 자체 재할당 불가
```

이 예시는 `const`의 재선언과 재할당이 불가능한 특징, 그리고 객체를 다룰 때의 특징을 보여준다.

---

# 🤔 언제 var, let, const를 사용할까?

- **`var`**: 과거의 코드와 호환성을 유지하거나, 함수 스코프를 명확히 하기 위해 사용할 수 있다. 그러나 새로운 코드에서는 var 대신 let이나 const를 사용하는 것이 좋다.
- **`let`**: 값이 변경될 가능성이 있는 변수는 let으로 선언한다. 블록 스코프를 따르기 때문에 더 안전하게 변수를 관리할 수 있다.
- **`const`**: 값이 변경되지 않을 상수를 선언할 때 const를 사용한다. 재할당이 불가능하므로, 코드의 의도를 명확히 전달할 수 있다.

---
