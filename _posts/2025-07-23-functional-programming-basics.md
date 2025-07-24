---
title: "[FP] 함수형 프로그래밍이란?"
excerpt: "함수형 프로그래밍의 핵심 원칙"

categories:
  - Software Engineering
tags:
  - [Software Engineering]

permalink: /software-engineering/functional-programming-basics

toc: true
toc_sticky: true

date: 2025-07-23T00:00:00
last_modified_at: 2025-07-24T:01:00
---

함수형 프로그래밍이 무엇인지 알아보고자 한다.

---

# 🔧 함수형 프로그래밍이란?

**함수형 프로그래밍**은 함수를 프로그램의 핵심 구성 요소로 사용하는 프로그래밍 패러다임이다.

데이터를 변경하지 않고 함수들을 조합해서 문제를 해결하는 방식으로 접근한다. 마치 수학의 함수처럼 입력값에 대해 항상 동일한 결과를 반환하는 순수한 함수들을 만들어 사용하는 것이다.

객체지향 프로그래밍과 달리 **"어떻게 할 것인가"** 보다는 **"무엇을 할 것인가"** 에 초점을 맞춘다.

```javascript
// 절차형 방식 (How)
let sum = 0;
for (let i = 0; i < numbers.length; i++) {
  sum += numbers[i];
}

// 함수형 방식 (What)
const sum = numbers.reduce((acc, num) => acc + num, 0);
```

---

# 🏗️ 함수형 프로그래밍의 핵심 원칙

함수형 프로그래밍에는 **4가지 주요 원칙**이 있다.

이 원칙들을 지키면서 코드를 작성하면 버그가 적고 이해하기 쉬운 프로그램을 만들 수 있다.

## 🔒 불변성 (Immutability)

**불변성**은 데이터가 한번 생성되면 변경할 수 없다는 특성이다.

기존 데이터를 직접 수정하지 않고, 변경이 필요할 때는 새로운 데이터를 생성해서 반환한다.

```javascript
// 나쁜 예: 원본 배열을 변경
const numbers = [1, 2, 3];
numbers.push(4); // 원본이 바뀜
console.log(numbers); // [1, 2, 3, 4]

// 좋은 예: 새로운 배열 생성
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4]; // 새로운 배열
console.log(numbers); // [1, 2, 3] (원본 그대로)
console.log(newNumbers); // [1, 2, 3, 4]
```

## ⚡ 순수 함수 (Pure Functions)

**순수 함수**는 같은 입력에 대해 항상 같은 출력을 반환하고, 외부에 영향을 주지 않는 함수이다.

함수 외부의 변수를 변경하거나 읽지 않고, 오직 전달받은 매개변수만 사용한다.

```javascript
// 순수 함수: 항상 같은 결과, 부작용 없음
function add(a, b) {
  return a + b;
}

// 비순수 함수: 외부 변수에 의존
let multiplier = 2;
function multiply(num) {
  return num * multiplier; // 외부 변수 사용
}

// 비순수 함수: 부작용 발생
function addToArray(arr, item) {
  arr.push(item); // 원본 배열 변경
  return arr;
}
```

## 🔗 함수 합성 (Function Composition)

**함수 합성**은 작은 함수들을 조합해서 복잡한 기능을 만드는 것이다.

각 함수는 한 가지 일만 잘하고, 이들을 연결해서 더 큰 문제를 해결한다.

```javascript
// 작은 함수들
const double = (x) => x * 2;
const addOne = (x) => x + 1;
const square = (x) => x * x;

// 함수 합성
const transform = (x) => square(addOne(double(x)));
console.log(transform(3)); // (3 * 2 + 1)² = 49

// 또는 파이프라인 방식
const pipe =
  (...fns) =>
  (value) =>
    fns.reduce((acc, fn) => fn(acc), value);
const transformPipe = pipe(double, addOne, square);
console.log(transformPipe(3)); // 49
```

## 🚫 부작용 없음 (No Side Effects)

**부작용이 없다**는 것은 함수가 외부 상태를 변경하지 않는다는 의미이다.

콘솔 출력, 파일 쓰기, 네트워크 통신 등은 모두 부작용에 해당한다.

```javascript
// 부작용이 있는 함수
function processUser(user) {
  console.log(`Processing ${user.name}`); // 콘솔 출력 (부작용)
  user.processed = true; // 객체 변경 (부작용)
  return user;
}

// 부작용이 없는 함수
function createProcessedUser(user) {
  return {
    ...user,
    processed: true,
  };
}
```

---

# 💎 불변성의 실질적 이점

불변성을 지키면서 프로그래밍하면 **4가지 주요 이점**을 얻을 수 있다.

- **예측 가능한 코드**

  데이터가 변경되지 않으므로 함수의 동작을 예측하기 쉽다.

- **안전한 동시성**

  여러 스레드에서 동시에 접근해도 데이터가 변경되지 않으므로 안전하다.

- **디버깅 용이성**

  데이터 변경 지점이 명확하므로 버그를 찾기 쉽다.

- **시간 여행 디버깅**

  상태 변경 이력을 쉽게 추적하고 이전 상태로 되돌릴 수 있다.

---

함수형 프로그래밍은 **더 안전하고 예측 가능한 코드**를 작성할 수 있게 해주는 강력한 패러다임이다.

완전히 함수형으로 모든 코드를 작성할 필요는 없지만, 핵심 개념들을 이해하고 적절히 활용하면 코드 품질을 크게 향상시킬 수 있을 것이다!
