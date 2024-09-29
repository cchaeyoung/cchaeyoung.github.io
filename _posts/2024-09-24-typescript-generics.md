---
title: "[TypeScript] 제네릭"
excerpt: "제네릭의 정의, 기본 사용법, 인터페이스와 타입 별칭에서의 활용, 타입 제약"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/generics

toc: true
toc_sticky: true

date: 2024-09-24
last_modified_at: 2024-09-29
---

# 🧩 제네릭의 정의와 기본 사용법

<mark>제네릭</mark>은 타입스크립트에서 다양한 타입에 대해 재사용 가능한 컴포넌트를 만들 수 있게 해주는 기능이다. 제네릭을 사용하면 특정 타입에 종속되지 않고 여러 타입에서 동작하는 컴포넌트를 작성할 수 있다.

제네릭을 사용하지 않으면 각 타입마다 별도의 함수를 작성해야 하지만, 제네릭을 사용하면 **하나의 함수로 여러 타입을 처리**할 수 있다.

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("myString"); // 타입: string
let output2 = identity<number>(100); // 타입: number
```

이 예제에서 `<T>`는 타입 변수로, 사용자가 제공한 타입으로 대체된다.

---

# 🔄 제네릭 함수

**제네릭 함수**는 다양한 타입의 인자를 받아 작업할 수 있는 함수를 만들 수 있게 해준다. 이를 통해 코드 중복을 줄이고 타입 안정성을 유지할 수 있다.

```typescript
function reverseArray<T>(array: T[]): T[] {
  return array.reverse();
}

const numbers = reverseArray<number>([1, 2, 3, 4, 5]);
const strings = reverseArray<string>(["a", "b", "c", "d"]);
```

---

# 📜 제네릭 인터페이스

인터페이스에도 **제네릭**을 사용할 수 있다. 이를 통해 재사용 가능한 인터페이스를 정의할 수 있다. **제네릭 인터페이스**는 다양한 타입에 대해 동일한 구조를 가진 객체를 정의할 때 유용하다.

```typescript
interface GenericIdentityFn<T> {
  (arg: T): T;
}

function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: GenericIdentityFn<number> = identity;
```

이 예제에서 `GenericIdentityFn` 인터페이스는 어떤 타입 `T`에 대해서도 동작하는 함수의 구조를 정의한다.

---

# 🏗️ 제네릭 클래스

**클래스**에서도 제네릭을 사용하여 재사용 가능한 컴포넌트를 만들 수 있다. **제네릭 클래스**는 클래스의 프로퍼티나 메서드가 여러 타입에서 작동해야 할 때 유용하다.

```typescript
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;

  constructor(zero: T, addFn: (x: T, y: T) => T) {
    this.zeroValue = zero;
    this.add = addFn;
  }
}

let numberCalculator = new GenericNumber<number>(0, (x, y) => x + y);
console.log(numberCalculator.add(5, 10)); // 출력: 15

let stringCalculator = new GenericNumber<string>("", (x, y) => x + y);
console.log(stringCalculator.add("Hello, ", "World!")); // 출력: "Hello, World!"
```

이 예제에서 `GenericNumber` 클래스는 숫자와 문자열 모두에 대해 작동한다.

---

# 🏷️ 제네릭 타입 별칭

타입 별칭에서도 **제네릭**을 사용할 수 있다. 이를 통해 재사용 가능한 타입을 정의할 수 있다. **제네릭 타입 별칭**은 복잡한 타입을 간단하게 표현하고 재사용할 때 유용하다.

```typescript
type GenericArray<T> = Array<T>;

const numberArray: GenericArray<number> = [1, 2, 3];
const stringArray: GenericArray<string> = ["a", "b", "c"];

type GenericFunc<T> = (arg: T) => T;

const echoNumber: GenericFunc<number> = (x) => x;
const echoString: GenericFunc<string> = (x) => x;
```

이 예제에서 `GenericArray`와 `GenericFunc`는 다양한 타입에 대해 재사용할 수 있는 타입 별칭이다.

---

# 🔒 제네릭 타입 제약

**제네릭 타입**에 특정 조건을 부여하여 사용할 수 있는 타입을 제한할 수 있다. 이는 특정 프로퍼티나 메서드가 존재하는 타입만 사용하고 싶을 때 유용하다.

```typescript
interface Lengthwise {
  length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length); // 이제 .length 속성이 있다고 확신할 수 있다
  return arg;
}

loggingIdentity([1, 2, 3]); // 성공
loggingIdentity({ length: 10, value: 3 }); // 성공
loggingIdentity(3); // 오류, number에는 .length가 없다
```

이 예제에서 `T extends Lengthwise`는 `T`가 `Lengthwise` 인터페이스를 확장해야 한다는 것을 의미한다. 즉, `T`는 반드시 `length` 프로퍼티를 가져야 한다.

---

# 🔑 keyof 연산자와 제네릭

`keyof` 연산자를 **제네릭**과 함께 사용하여 객체의 속성에 안전하게 접근할 수 있다. 이는 특정 객체의 속성 이름을 타입으로 가져와 해당 속성에 대한 타입 안전성을 제공한다.

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

let x = { a: 1, b: 2, c: 3, d: 4 };

getProperty(x, "a"); // 성공
getProperty(x, "m"); // 오류: 인수의 타입 '"m"'은 '"a" | "b" | "c" | "d"' 타입의 매개변수에 할당될 수 없다.
```

이 기능을 사용하면, 객체의 속성을 동적으로 접근하면서도 **타입스크립트**의 타입 검사를 통해 오류를 예방할 수 있다. 이를 통해 더욱 안전하고 재사용 가능한 코드를 작성할 수 있다.

---

**제네릭**은 타입스크립트에서 유연하고 재사용 가능한 코드를 작성하는 데 매우 유용한 기능이다.

**제네릭**을 잘 활용하면 타입 안정성을 유지하면서도 다양한 타입에 대응할 수 있는 컴포넌트를 만들 수 있다. 이를 통해 코드의 재사용성이 높아지고, 타입 관련 버그를 줄일 수 있다.
