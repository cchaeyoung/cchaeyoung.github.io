---
title: "[TypeScript] 타입스크립트의 이넘(Enum)"
excerpt: "이넘의 개념, 숫자 열거형, 문자열 열거형, 이니셜라이즈된 열거형, 혼합 열거형, 사용 예제"

categories:
  - TypeScript
tags:
  - [TypeScript]

permalink: /typescript/enums

toc: true
toc_sticky: true

date: 2024-09-23 12:00:00
last_modified_at: 2024-09-29
---

<mark>이넘(Enum)</mark>은 타입스크립트에서 제공하는 **특별한 타입**으로, **명명된 상수**들의 집합을 정의하는 데 사용된다. **이넘**은 코드의 **가독성**을 높이고, 관련된 상수들을 **그룹화**하는 데 유용하다.

**숫자 열거형**, **문자열 열거형**, **혼합 열거형** 등 다양한 형태로 사용할 수 있어 여러 상황에 적용할 수 있다.

---

# 🚀 이넘의 선언과 기본 사용

이넘은 `enum` 키워드를 사용하여 정의한다. 기본적으로 이넘의 각 멤버는 0부터 시작하는 숫자 값을 가진다.

```typescript
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

console.log(Direction.Up); // 출력: 0
console.log(Direction.Down); // 출력: 1
console.log(Direction.Left); // 출력: 2
console.log(Direction.Right); // 출력: 3
```

---

# 🔢 숫자 열거형

**숫자 열거형**은 이넘의 기본 형태이다.  
각 멤버는 명시적으로 **숫자 값을 할당**할 수 있으며, 할당하지 않은 멤버는 **이전 멤버의 값에 1을 더한 값**을 가진다.

```typescript
enum StatusCode {
  OK = 200,
  BadRequest = 400,
  Unauthorized, // 401
  Forbidden, // 402
}

console.log(StatusCode.OK); // 출력: 200
console.log(StatusCode.Unauthorized); // 출력: 401
```

---

# 🎨 문자열 열거형

**문자열 열거형**은 각 멤버에 **문자열 값을 할당**하는 방식이다.  
**문자열 열거형**의 모든 멤버는 **반드시 초기화**되어야 한다.

```typescript
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE",
}

console.log(Color.Red); // 출력: "RED"
console.log(Color.Green); // 출력: "GREEN"
```

---

# 🔀 문자열 및 숫자 혼합 열거형

타입스크립트는 **문자열과 숫자** 값을 혼합하여 사용하는 **열거형**을 지원한다.

```typescript
enum Mixed {
  A,
  B = "B",
  C = 100,
  D,
}

console.log(Mixed.A); // 출력: 0
console.log(Mixed.B); // 출력: "B"
console.log(Mixed.C); // 출력: 100
console.log(Mixed.D); // 출력: 101
```

이렇게 하면 **다양한 유형**의 값을 하나의 이넘으로 처리할 수 있다.

---

# 🧮 이니셜라이즈된 열거형

**이니셜라이즈된 열거형**은 멤버의 값을 **계산된 값으로 초기화**할 수 있다. 이 방식은 값의 조합이나 **비트 연산**과 같은 로직을 포함할 때 유용하게 사용된다.

```typescript
enum FileAccess {
  Read = 1 << 0, // 1
  Write = 1 << 1, // 2
  Execute = 1 << 2, // 4
}

console.log(FileAccess.Read); // 출력: 1
console.log(FileAccess.Write); // 출력: 2
console.log(FileAccess.Execute); // 출력: 4
```

---

# 💡 열거형의 사용 예제

**이넘**은 다양한 상황에서 **유용하게 사용**될 수 있다.  
예를 들어, **API 응답 상태**를 표현하거나 **사용자 역할**을 정의하는 데 사용할 수 있다.

```typescript
enum ApiResponse {
  Success = "SUCCESS",
  Error = "ERROR",
  Pending = "PENDING",
}

function handleResponse(response: ApiResponse) {
  switch (response) {
    case ApiResponse.Success:
      console.log("요청이 성공했습니다.");
      break;
    case ApiResponse.Error:
      console.log("오류가 발생했습니다.");
      break;
    case ApiResponse.Pending:
      console.log("요청이 처리 중입니다.");
      break;
  }
}

handleResponse(ApiResponse.Success); // 출력: "요청이 성공했습니다."
```

---

**이넘**은 타입스크립트에서 관련된 상수들을 **그룹화**하고 코드의 **가독성**을 높이는 데 매우 유용한 기능이다.

**이넘을 적절히 사용하면** 코드의 **유지보수성**과 **안정성**을 크게 향상시킬 수 있다.
