---
title: "[Algorithm] 브루트포스(Brute Force) 알고리즘"
excerpt: "완전탐색 알고리즘인 브루트포스의 개념과 활용"

categories:
  - Algorithm
tags:
  - [Algorithm]

permalink: /algorithm/algorithm-bruteforce/

toc: true
toc_sticky: true

date: 2024-12-30
last_modified_at: 2024-12-30
---

# 🔍 브루트포스란?

**브루트포스(Brute Force)**는 가능한 모든 경우의 수를 탐색하여 문제를 해결하는 알고리즘이다.

**'무식하게 풀기'**, **'완전탐색'**이라고도 불리며, 가능한 <mark>모든 경우의 수</mark>를 확인하여 정답을 찾는다.

- **장점**: 항상 정답을 찾을 수 있다.
- **단점**: 시간이 오래 걸릴 수 있다.

---

# 💡 브루트포스의 특징

## 1️⃣ 구현 방법

브루트포스는 주로 다음과 같은 방법으로 구현한다:

1. **반복문** - 중첩 for문을 사용
2. **재귀함수** - 자기 자신을 호출
3. **순열과 조합** - 모든 경우의 수를 생성

## 2️⃣ 시간 복잡도

대부분의 브루트포스 알고리즘은 **O(N!)**, **O(2^N)**, **O(N^M)** 등의 시간 복잡도를 가진다.  
<mark>입력 크기가 작을 때</mark> 유용하며, 크기가 커질수록 <mark>효율성이 떨어진다</mark>.

---

# 📝 브루트포스 예제

<h2>1. 숫자 조합 찾기</h2>

주어진 배열에서 세 수의 합이 특정 값이 되는 조합 찾기

```javascript
function findThreeSum(arr, target) {
  const result = [];
  for (let i = 0; i < arr.length - 2; i++) {
    for (let j = i + 1; j < arr.length - 1; j++) {
      for (let k = j + 1; k < arr.length; k++) {
        if (arr[i] + arr[j] + arr[k] === target) {
          result.push([arr[i], arr[j], arr[k]]);
        }
      }
    }
  }
  return result;
}

const numbers = [1, 2, 3, 4, 5];
console.log(findThreeSum(numbers, 9)); // [[2,3,4], [1,3,5]]
```

<h2>2. 문자열 패턴 매칭</h2>

텍스트에서 특정 패턴이 존재하는지 확인하기

```javascript
function searchPattern(text, pattern) {
  const n = text.length;
  const m = pattern.length;

  for (let i = 0; i <= n - m; i++) {
    let found = true;
    for (let j = 0; j < m; j++) {
      if (text[i + j] !== pattern[j]) {
        found = false;
        break;
      }
    }
    if (found) return i; // 패턴이 발견된 위치 반환
  }
  return -1; // 패턴을 찾지 못함
}

console.log(searchPattern("HELLO WORLD", "WORLD")); // 6
```

---

# 🚀 브루트포스가 유용한 경우

1. **문제의 범위가 작은 경우**

   - 입력 크기가 작을 때
   - 시간 제한이 넉넉할 때

2. **최적화할 필요가 없는 경우**

   - 빠른 시간 내에 구현이 필요할 때
   - 정확한 답을 보장해야할 때

3. **더 좋은 알고리즘을 찾기 전 기본 접근법으로**
   - 문제 해결의 시작점으로 활용
   - 다른 알고리즘의 정확성을 검증할 때

---

# ⚠️ 브루트포스 사용 시 주의사항

1. **시간 복잡도 고려**  
   브루트포스는 <mark>모든 경우의 수를 탐색</mark>하므로 입력이 커질수록 **실행 시간이 기하급수적으로 증가**한다. 문제의 **시간 제한** 내에 해결이 가능한지 반드시 확인해야 한다.

2. **메모리 사용량**  
   **재귀 호출**을 사용할 경우 <mark>스택 오버플로우</mark>가 발생할 수 있으며, 큰 배열을 생성하는 경우 **메모리 제한**을 초과할 수 있으므로 주의가 필요하다.

3. **최적화 가능성**  
   브루트포스로 해결 가능하더라도, 더 **효율적인 알고리즘**이 존재하는지 검토해보는 것이 좋다. 특히 <mark>시간이나 메모리 제한이 빡빡한 경우</mark>에는 다른 최적화 방법을 고려해볼 필요가 있다.
