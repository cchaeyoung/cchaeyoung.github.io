---
title: "[TypeScript] 타입스크립트의 타입 오퍼레이터"
excerpt: "유니언 타입, 인터섹션 타입, keyof, typeof, 인덱스 접근 타입, 조건부 타입"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/type-operators

toc: true
toc_sticky: true

date: 2024-09-29
last_modified_at: 2024-09-29
---

타입스크립트는 다양한 타입 오퍼레이터를 제공하여 타입을 조작하고 결합할 수 있게 해준다. 이를 통해 더 복잡하고 정확한 타입을 정의할 수 있다.

---

# 🔗 유니언 타입 (Union Types)

유니언 타입은 여러 타입 중 하나일 수 있는 값을 나타낸다. `|` 기호를 사용하여 표현한다. 이는 변수가 여러 타입의 값을 가질 수 있을 때 유용하다.

```typescript
let result: number | string;
result = 10; // 유효
result = "hello"; // 유효
result = true; // 에러: boolean은 number | string 타입에 할당할 수 없다.

function printId(id: number | string) {
  console.log("Your ID is: " + id);
}

printId(101); // 유효
printId("202"); // 유효
```

유니언 타입을 사용할 때는 종종 타입 가드를 사용하여 특정 타입에 대한 동작을 정의한다.

```typescript
function printValue(value: number | string) {
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  } else {
    console.log(value.toFixed(2));
  }
}
```

---

# 🎯 인터섹션 타입 (Intersection Types)

인터섹션 타입은 여러 타입을 **모두 만족**하는 타입을 생성한다. `&` 기호를 사용하여 표현한다.

```typescript
type Employee = {
  name: string;
  id: number;
};

type Manager = {
  department: string;
};

type ManagerEmployee = Employee & Manager;

function assignManager(
  employee: Employee,
  department: string
): ManagerEmployee {
  return { ...employee, department };
}

let manager = assignManager({ name: "Chaeng", id: 12345 }, "IT");
console.log(manager); // { name: "Chaeng", id: 12345, department: "IT" }
```

---

# 🔑 keyof 연산자

`keyof` 연산자는 객체 타입의 **모든 키를 유니언 타입**으로 추출한다.

```typescript
interface Person {
  name: string;
  age: number;
  location: string;
}

type PersonKeys = keyof Person; // "name" | "age" | "location"

function getProperty(obj: Person, key: PersonKeys) {
  return obj[key];
}

let person: Person = { name: "Chaeng", age: 20, location: "Seoul" };
console.log(getProperty(person, "name")); // "Chaeng"
console.log(getProperty(person, "gender")); // 에러: "gender"는 PersonKeys 타입에 없다.
```

---

# 🧩 typeof 연산자

타입스크립트에서 `typeof` 연산자는 값의 **타입을 추출**하는 데 사용된다. 이는 **JavaScript**의 `typeof`와는 다르게, **타입 수준**에서 작동한다.

```typescript
let person = { name: "Chaeng", age: 20 };
type Person = typeof person; // { name: string; age: number; }

function greet(someone: Person) {
  console.log(`Hello, ${someone.name}!`);
}

greet({ name: "Bob", age: 25 }); // 유효
```

---

# 🗂 인덱스 접근 타입 (Indexed Access Types)

인덱스 접근 타입을 사용하면 **다른 타입의 특정 속성**의 타입을 추출할 수 있다. 이는 복잡한 타입에서 특정 부분만 사용하고 싶을 때 유용하다.

```typescript
type Person = { age: number; name: string; alive: boolean };
type Age = Person["age"]; // number

type I1 = Person["age" | "name"]; // number | string
type I2 = Person[keyof Person]; // number | string | boolean

function getAge(person: Person): Age {
  return person.age;
}

let age: Age = getAge({ age: 30, name: "Chaeng", alive: true });
console.log(age); // 30
```

---

# 🔄 조건부 타입 (Conditional Types)

조건부 타입을 사용하면 **조건에 따라 다른 타입**을 선택할 수 있다. 이는 **제네릭 타입**을 정의할 때 특히 유용하다.

```typescript
type IsString<T> = T extends string ? true : false;

type A = IsString<string>; // true
type B = IsString<number>; // false

type ArrayOrSingle<T> = T extends any[] ? T : T[];

function wrapInArray<T>(value: T): ArrayOrSingle<T> {
  return Array.isArray(value) ? value : [value];
}

console.log(wrapInArray("hello")); // ["hello"]
console.log(wrapInArray([1, 2, 3])); // [1, 2, 3]
```
