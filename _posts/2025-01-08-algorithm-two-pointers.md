---
title: "[Algorithm] 투 포인터(Two Pointers) 알고리즘"
excerpt: "효율적인 배열 탐색을 위한 투 포인터 알고리즘"

categories:
  - Algorithm
tags:
  - [Algorithm]

permalink: /algorithm/algorithm-two-pointers/

toc: true
toc_sticky: true

date: 2025-01-08
last_modified_at: 2025-01-08
---

# 📚 투 포인터란?

**투 포인터(Two Pointers) 알고리즘**은 배열에서 두 개의 포인터를 이용해 원하는 결과를 찾는 알고리즘이다.

1차원 배열에서 **두 개의 포인터를 조작**하면서 원하는 결과를 얻어내는 방식으로, **연속된 구간을 처리**할 때 유용하다.

---

# 💡 투 포인터의 특징

1. **시간 복잡도 개선**

   - 일반적으로 `O(n²)`을 `O(n)`으로 줄일 수 있다.
   - 브루트포스로 해결하면 비효율적인 문제들을 효과적으로 해결한다.

2. **공간 복잡도 효율성**

   - 추가적인 공간을 거의 사용하지 않는다.
   - 기존 배열에서 포인터만 이동

3. **적용 가능한 경우**

   - <mark>정렬된 배열에서의 검색</mark>
   - <mark>부분 배열의 합 계산</mark>
   - <mark>중복 요소 제거</mark>
   - <mark>특정 조건을 만족하는 구간 찾기</mark>

---

# 🎯 투 포인터의 구현 방법

투 포인터는 크게 **두 가지 방식**으로 구현할 수 있다.

<h2>1. 양쪽 끝에서 시작하는 방식</h2>

두 포인터를 배열의 **양쪽 끝**에서 시작하여 중앙으로 이동하는 방식이다.

주로 **정렬된 배열**에서 두 원소를 찾는 문제에 사용된다.

```javascript
let left = 0;
let right = arr.length - 1;

while (left < right) {
  // 조건에 따라 left++ 또는 right--
}
```

<h2>2. 같은 방향으로 이동하는 방식</h2>

두 포인터가 **같은 방향**으로 이동하면서 조건을 검사하는 방식이다.

주로 **연속된 부분 배열**을 찾는 문제에 사용된다.

```javascript
let start = 0;
let end = 0;

while (end < arr.length) {
  // 조건에 따라 start++ 또는 end++
}
```

---

# 🌟 투 포인터의 활용 예제

## 1. 정렬된 배열에서 특정 합 찾기

정렬된 배열에서 **두 수의 합이 특정 값**이 되는 경우를 찾는 문제다.

```javascript
function findPairSum(arr, target) {
  let left = 0;
  let right = arr.length - 1;
  const result = [];

  while (left < right) {
    const sum = arr[left] + arr[right];

    if (sum === target) {
      result.push([arr[left], arr[right]]);
      left++;
      right--;
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }

  return result;
}

const sortedArr = [1, 2, 3, 4, 5, 6, 7];
console.log(findPairSum(sortedArr, 7)); // [[2, 5], [3, 4]]
```

<h2>2. 중복 요소 제거</h2>
정렬된 배열에서 **중복 요소**를 제거하는 문제다.

```javascript
function removeDuplicates(arr) {
  if (arr.length === 0) return 0;

  let i = 0;

  for (let j = 1; j < arr.length; j++) {
    if (arr[i] !== arr[j]) {
      i++;
      arr[i] = arr[j];
    }
  }

  return i + 1; // 새로운 배열의 길이
}

const arr = [1, 1, 2, 2, 3, 4, 4];
const newLength = removeDuplicates(arr);
console.log(arr.slice(0, newLength)); // [1, 2, 3, 4]
```

---

# ⚡ 시간 복잡도 분석

투 포인터 알고리즘의 시간 복잡도는 대부분의 경우 `O(n)`이다. 이는 각 포인터가 배열을 **최대 한 번씩**만 훑기 때문이다.

- 일반적인 브루트포스: `O(n²)`
- 투 포인터 사용: `O(n)`

이러한 시간 복잡도의 개선은 특히 **큰 데이터셋**을 다룰 때 매우 중요한 장점이 된다.

---

# 💡 주의사항과 팁

1. **정렬의 중요성**

   - 많은 투 포인터 문제는 **정렬된 배열**을 전제로 한다.
   - 정렬되지 않은 배열의 경우, 정렬 후 적용해야 할 수 있다.

2. **경계 조건 처리**

   - 포인터가 배열의 범위를 벗어나지 않도록 주의한다.
   - 빈 배열, 단일 요소 배열 등의 예외 케이스를 고려한다.

3. **포인터 이동 조건**

   - 문제의 조건에 따라 적절한 포인터 이동 전략을 수립한다.
   - 불필요한 반복을 피하기 위한 최적화를 고려한다.
