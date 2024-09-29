---
title: "[TypeScript] 타입 별칭"
excerpt: "타입 별칭의 정의, 기본 사용법, 복잡한 타입 구조 생성, 재사용과 확장"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/type-alias

toc: true
toc_sticky: true

date: 2024-09-23 09:00:00
last_modified_at: 2024-09-29
---

<mark>타입 별칭</mark>은 타입스크립트에서 기존 타입에 새로운 이름을 부여하는 기능이다. 이를 통해 코드의 가독성과 재사용성을 높일 수 있다.

---

# ✍️ 타입 별칭의 정의와 기본 사용법

타입 별칭은 `type` 키워드를 사용하여 정의한다. 기본 타입부터 복잡한 객체 타입까지 다양한 형태의 타입에 별칭을 지정할 수 있다.

```typescript
type UserID = number;
type UserName = string;

type User = {
  id: UserID;
  name: UserName;
};

const user: User = {
  id: 1,
  name: "Chaeng",
};
```

---

# 📝 리터럴 타입과 타입 별칭

타입 별칭은 리터럴 타입과 함께 사용하여 특정 값들의 집합을 나타내는 데 유용하다.

```typescript
type Direction = "North" | "South" | "East" | "West";

function move(direction: Direction) {
  console.log(`Moving ${direction}`);
}

move("North"); // 유효
move("Northeast"); // 에러: "Northeast"는 Direction 타입이 아니다
```

---

# 🔗 타입 별칭을 이용한 복잡한 타입 구조 생성

타입 별칭을 사용하여 복잡한 타입 구조를 만들 수 있다. 이는 코드의 가독성을 높이고 타입 정의를 중앙화하는 데 도움이 된다.

```typescript
type Coordinates = [number, number];
type RGB = [number, number, number];

type Pixel = {
  position: Coordinates;
  color: RGB;
};

const pixel: Pixel = {
  position: [10, 20],
  color: [255, 128, 0],
};
```

---

# ♻️ 타입 별칭의 재사용과 확장

타입 별칭은 다른 타입 별칭을 참조하여 새로운 타입을 만들 수 있다. 이를 통해 타입 정의를 모듈화하고 재사용할 수 있다.

```typescript
type BasicAddress = {
  street: string;
  city: string;
};

type AddressWithPostal = BasicAddress & {
  postalCode: string;
};

const address: AddressWithPostal = {
  street: "123 Main St",
  city: "Anytown",
  postalCode: "12345",
};
```

---

# 🧩 타입 별칭과 타입 추론

타입스크립트의 타입 추론 기능은 타입 별칭과 함께 사용될 때 더욱 강력해진다.

```typescript
type Config = {
  endpoint: string;
  apiKey: string;
};

const createApi = (config: Config) => {
  return {
    fetch: () => {
      console.log(`Fetching from ${config.endpoint} with key ${config.apiKey}`);
    },
  };
};

const api = createApi({
  endpoint: "https://api.example.com",
  apiKey: "abc123",
});
// api의 타입이 자동으로 추론됨
api.fetch(); // 타입 안전성 보장
```

---

타입 별칭은 타입스크립트에서 코드를 더 읽기 쉽고 유지보수하기 쉽게 만든다.  
복잡한 타입을 간단한 이름으로 표현할 수 있어 코드의 가독성을 크게 향상시킬 수 있고, 다른 타입 관련 기능들과 함께 사용하면 더욱 강력한 타입 시스템을 구축할 수 있다.
