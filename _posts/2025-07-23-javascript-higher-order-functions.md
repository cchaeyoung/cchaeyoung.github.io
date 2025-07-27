---
title: "[JavaScript] 고차함수"
excerpt: "map, filter, reduce, find, some, every 등 고차함수의 개념과 활용법"

categories:
  - JavaScript
tags:
  - [JavaScript]

permalink: /javascript/higher-order-functions

toc: true
toc_sticky: true

date: 2025-07-23T02:00:00
last_modified_at: 2025-07-27T00:00:00
---

고차함수는 **함수를 값처럼 다루는** 도구다. 반복문 없이도 배열 데이터를 쉽고 깔끔하게 처리할 수 있어서 현대 JavaScript 개발에서 중요하다.

---

# 🔧 고차함수 기본 개념

## 🎪 고차함수란?

고차함수는 **다른 함수를 매개변수로 받거나 함수를 반환하는 함수**다.

쉽게 말해 함수를 마치 숫자나 문자열처럼 변수에 담고 다른 함수에 전달할 수 있다는 뜻이다.

```javascript
// 함수를 변수에 담기
const sayHello = function (name) {
  return `안녕, ${name}!`;
};

// 함수를 다른 함수에 전달하기
function greetPeople(names, greetFunction) {
  return names.map(greetFunction);
}

const names = ["철수", "영희", "민수"];
const greetings = greetPeople(names, sayHello);
// ["안녕, 철수!", "안녕, 영희!", "안녕, 민수!"]
```

## 📊 왜 고차함수를 쓸까?

고차함수는 반복문보다 코드가 짧고 간결해서 실수를 줄이고 읽기 편하다.

**반복문**

```javascript
// 배열의 모든 숫자를 2배로 만들기
const numbers = [1, 2, 3, 4, 5];
const doubled = [];

for (let i = 0; i < numbers.length; i++) {
  doubled.push(numbers[i] * 2);
}
// [2, 4, 6, 8, 10]
```

**고차함수 방법**

```javascript
// 같은 작업을 고차함수로
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((num) => num * 2);
// [2, 4, 6, 8, 10]
```

반복문은 코드가 길고 직접 배열에 값을 넣어야 해서 실수할 여지가 많다.

위 예시처럼 고차함수를 사용하면 **더 짧고, 읽기 쉽고, 실수를 줄일 수 있다.**

---

# 🗺️ map 함수

`map` 함수는 배열의 **모든 요소를 똑같은 규칙으로 바꿔서** 새로운 배열을 만든다.

마치 도장을 찍는 것처럼, 모든 요소에 동일한 작업을 적용한다.

```javascript
// 숫자를 2배로 만들기
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((num) => num * 2);
// [2, 4, 6, 8]

// 이름 앞에 "안녕, " 붙이기
const names = ["철수", "영희", "민수"];
const greetings = names.map((name) => `안녕, ${name}!`);
// ["안녕, 철수!", "안녕, 영희!", "안녕, 민수!"]
```

- 원본 배열은 그대로 두고 새 배열을 만든다.
- 입력과 출력 배열의 길이가 항상 같다.
- 모든 요소에 동일한 변환 적용한다.

---

# 🔍 filter 함수

`filter` 함수는 배열에서 **조건을 만족하는 요소들만** 골라서 새로운 배열을 만든다.

마치 체로 걸러내는 것처럼, 원하는 것만 통과시키고 나머지는 제거한다.

```javascript
// 짝수만 골라내기
const numbers = [1, 2, 3, 4, 5, 6];
const evenNumbers = numbers.filter((num) => num % 2 === 0);
// [2, 4, 6]
```

- 조건을 만족하는 요소만 포함한다.
- 출력 배열이 입력 배열보다 작거나 같다.
- 원본 배열은 변경되지 않는다.

---

# 📉 reduce 함수

`reduce` 함수는 배열의 모든 요소를 **하나의 값으로 합치는** 함수다.

마치 재료들을 모아서 하나의 요리를 만드는 것처럼, 모든 요소를 조합해서 최종 결과를 만든다.

```javascript
// 숫자들의 합계 구하기
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((total, current) => total + current, 0);
// 15

// 가장 큰 수 찾기
const max = numbers.reduce((biggest, current) => {
  return current > biggest ? current : biggest;
}, 0);
// 5
```

- 배열 전체를 하나의 값으로 축약한다.
- 누적값을 계속 업데이트하면서 진행된다.
- 초기값을 지정할 수 있다.

---

# 🕵️‍♂️ find 함수

`find` 함수는 조건을 처음으로 만족하는 요소 하나만 반환한다.

```js
// 짝수 중 첫 번째 숫자 찾기
const numbers = [1, 3, 4, 6, 8];
const firstEven = numbers.find((num) => num % 2 === 0);
// 4
```

- 조건을 만족하는 첫 번째 요소만 반환된다.
- 만족하는 요소가 없으면 결과는 `undefined`, 아무 값도 찾지 못했다는 뜻이다.
- 반환 결과는 배열이 아니라 요소 하나이다.

---

# ✅ some 함수

`some` 함수는 배열 안에 조건을 만족하는 요소가 하나라도 있는지 확인한다.

```js
// 짝수가 하나라도 있는지 확인하기
const numbers = [1, 3, 5, 7, 8];
const hasEven = numbers.some((num) => num % 2 === 0);
// true
```

- 조건을 만족하는 요소가 하나라도 있으면 true를 반환한다.
- 모든 요소가 조건을 만족하지 않으면 false를 반환한다.
- 조건 확인만 하며, 배열은 변하지 않는다.

---

# 🧪 every 함수

`every` 함수는 배열의 모든 요소가 조건을 만족하는지 확인한다.

```js
// 모든 숫자가 홀수인지 확인하기
const numbers = [1, 3, 5];
const allOdd = numbers.every((num) => num % 2 === 1);
// true
```

- 모든 요소가 조건을 만족하면 true를 반환한다.
- 하나라도 조건을 만족하지 않으면 false를 반환한다.
- 배열 전체의 일관성을 확인할 때 유용하다.

---

# 🎯 함수들을 연결해서 사용하기

고차함수들의 진짜 힘은 **여러 개를 연결해서 사용**할 때 나타난다. 마치 레고 블록을 조립하듯 단계별로 연결할 수 있다.

```javascript
// 학생 데이터 처리 예시
const students = [
  { name: "철수", age: 20, grade: 85 },
  { name: "영희", age: 22, grade: 92 },
  { name: "민수", age: 19, grade: 78 },
  { name: "지원", age: 21, grade: 88 },
  { name: "수진", age: 20, grade: 95 },
];

// 성인 중에서 우수한 학생들의 평균 점수 구하기
const averageGrade =
  students
    .filter((student) => student.age >= 20) // 성인만 선별
    .filter((student) => student.grade >= 85) // 우수한 학생만 선별
    .map((student) => student.grade) // 점수만 추출
    .reduce((sum, grade) => sum + grade, 0) / // 점수 합계
  students.filter((s) => s.age >= 20 && s.grade >= 85).length; // 평균 계산
```

이렇게 여러 고차함수를 연결하면 **읽기 쉽고**, **무엇을 하고 싶은지**가 코드에서 바로 드러난다.

---

고차함수는 단순히 편의 기능이 아니라 **생각하는 방식을 바꿔주는 도구**다. "어떻게 할지" 고민하는 대신 "무엇을 할지"에 집중할 수 있게 해준다.

복잡한 반복문 대신 고차함수를 활용해 더 깔끔하고 효율적인 코드를 작성해보자!
