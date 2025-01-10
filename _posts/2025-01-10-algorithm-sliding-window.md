---
title: "[Algorithm] 슬라이딩 윈도우(Sliding Window) 알고리즘"
excerpt: "배열이나 문자열을 효율적으로 처리하는 슬라이딩 윈도우 알고리즘"

categories:
  - Algorithm
tags:
  - [Algorithm]

permalink: /algorithm/algorithm-sliding-window/

toc: true
toc_sticky: true

date: 2025-01-10
last_modified_at: 2025-01-10
---

# 📚 슬라이딩 윈도우란?

**슬라이딩 윈도우(Sliding Window) 알고리즘**은 배열이나 문자열에서 **일정 크기의 윈도우**를 이동시키면서 윈도우 내의 데이터를 처리하는 알고리즘이다.

여기서 **'윈도우'**는 배열에서 연속된 구간을 보는 창문이라고 생각하면 된다.

예를 들어, 배열 `[1, 2, 3, 4, 5]`에서 크기가 3인 윈도우로 본다면:

- 첫 번째 윈도우: `[1, 2, 3]`
- 두 번째 윈도우: `[2, 3, 4]`
- 세 번째 윈도우: `[3, 4, 5]`

이처럼 윈도우는 마치 창문처럼 이동하면서 배열의 연속된 부분을 차례대로 확인한다.

윈도우를 한 칸씩 이동시키면서 **이전 윈도우와의 차이를 계산**하는 방식으로, 매번 전체를 다시 계산하지 않고 변화하는 부분만 처리한다.

---

# 💡 슬라이딩 윈도우의 특징

1. **효율적인 연산**

   - 중복 계산을 피할 수 있다.
   - 한 번의 순회로 모든 윈도우를 처리할 수 있다.

2. **시간 복잡도 개선**

   - 일반적인 방식: `O(n*k)` → 슬라이딩 윈도우: `O(n)`
   - `n`은 배열의 길이, `k`는 윈도우의 크기

3. **적용 가능한 경우**

   - <mark>고정 크기 윈도우의 합 또는 평균</mark>
   - <mark>연속된 부분 배열의 최대/최소값</mark>
   - <mark>문자열 패턴 매칭</mark>
   - <mark>최대 K개의 연속된 요소</mark>

---

# ⚙️ 슬라이딩 윈도우의 구현 방법

슬라이딩 윈도우는 **고정 크기**와 **가변 크기** 두 가지 방식으로 구현할 수 있다.

<h2>1. 고정 크기 윈도우</h2>

윈도우의 크기가 고정되어 있는 경우다.

주로 연속된 `k`개의 요소를 처리할 때 사용한다.

```javascript
let start = 0;
let end = k - 1; // k는 윈도우 크기

while (end < arr.length) {
  // 윈도우 내 데이터 처리
  start++;
  end++;
}
```

<h2>2. 가변 크기 윈도우</h2>

윈도우의 크기가 조건에 따라 변하는 경우다.

특정 조건을 만족할 때까지 윈도우를 조절한다.

```javascript
let start = 0;
let end = 0;

while(end < arr.length) {
    // 조건에 따라 윈도우 크기 조절
    if(조건 만족) end++;
    else start++;
}
```

---

# 🌟 슬라이딩 윈도우의 활용 예제

<h2>1. 연속된 K개의 수의 최대 합</h2>

배열에서 **연속된 K개 원소의 합이 최대**가 되는 값을 찾는 문제다.

```javascript
function maxSumOfK(arr, k) {
  if (arr.length < k) return null;

  // 첫 번째 윈도우의 합 계산
  let sum = 0;
  for (let i = 0; i < k; i++) {
    sum += arr[i];
  }

  let maxSum = sum;

  // 윈도우 이동하면서 합 계산
  for (let i = k; i < arr.length; i++) {
    sum = sum - arr[i - k] + arr[i]; // 이전 값 빼고 새로운 값 더하기
    maxSum = Math.max(maxSum, sum);
  }

  return maxSum;
}

const arr = [1, 4, 2, 10, 2, 3, 1, 0, 20];
console.log(maxSumOfK(arr, 4)); // 28 (sum of 3,1,0,20)
```

<h2>2. 최소 길이 부분 배열</h2>

배열에서 **합이 특정 값 이상**이 되는 **최소 길이의 연속된 부분 배열**을 찾는 문제다.

```javascript
function minSubArrayLen(arr, target) {
  let start = 0;
  let end = 0;
  let sum = 0;
  let minLen = Infinity;

  while (end < arr.length) {
    sum += arr[end];

    while (sum >= target) {
      minLen = Math.min(minLen, end - start + 1);
      sum -= arr[start];
      start++;
    }

    end++;
  }

  return minLen === Infinity ? 0 : minLen;
}

const arr = [2, 3, 1, 2, 4, 3];
console.log(minSubArrayLen(arr, 7)); // 2 (부분 배열 [4, 3])
```

---

# ⚡ 시간 복잡도 분석

슬라이딩 윈도우 알고리즘의 시간 복잡도는 대부분의 경우 `O(n)`이다. 이는 배열의 각 요소를 최대 한 번씩만 처리하기 때문이다.

- 일반적인 방식: `O(n*k)`
- 슬라이딩 윈도우: `O(n)`

이러한 시간 복잡도의 개선은 특히 **윈도우의 크기가 큰 경우**에 매우 효과적이다.

---

# ⚠️ 주의사항과 팁

1. **윈도우 크기 결정**

   - 문제의 요구사항에 맞는 윈도우 크기를 선택한다.
   - 고정 크기인지 가변 크기인지 먼저 파악한다.

2. **초기 윈도우 처리**

   - 첫 번째 윈도우는 별도로 처리해야 할 수 있다.
   - 배열의 크기가 윈도우보다 작은 경우를 고려한다.

3. **경계 조건 확인**

   - 배열의 시작과 끝 부분에서의 처리를 주의한다.
   - 윈도우가 배열 범위를 벗어나지 않도록 한다.

4. **최적화 고려**

   - 불필요한 계산을 피하기 위해 이전 결과를 활용한다.
   - 조건에 따라 윈도우 크기를 효율적으로 조절한다.
