---
title: "[Algorithm] 결정 알고리즘(Decision Algorithm)"
excerpt: "결정 알고리즘의 개념, 특징, 예제"

categories:
  - Algorithm
tags:
  - [Algorithm]

permalink: /algorithm/decision-algorithm/

toc: true
toc_sticky: true

date: 2025-01-20
last_modified_at: 2025-01-20
---

# 🔍 결정 알고리즘이란?

**결정 알고리즘(Decision Algorithm)**은 주어진 조건을 만족하는 값을 찾기 위해 **이분 탐색**을 활용하는 알고리즘이다.

답이 될 수 있는 범위에서 중간값을 선택하고, 그 값이 조건을 만족하는지 확인하며 범위를 좁혀나가는 방식으로 동작한다.

![decision](/assets/images/posts_img/algorithm/decision.png)

---

# 📊 결정 알고리즘의 특징

1. **최적화 문제 해결**:

   - 예: "최소 질투심", "최소 시간", "최소 인출 금액" 등.

2. **조건 만족 여부 확인**:

   - 특정 값을 기준으로 조건을 만족하는지 확인하여 범위를 좁힌다.

3. **이분 탐색 응용**:
   - 조건 함수를 정의하고, 이를 기반으로 탐색 범위를 조정한다.
   - 시간 복잡도는 보통 `O(N log K)` (N: 조건 함수 호출 횟수, K: 탐색 범위 크기).

---

# 🔄 결정 알고리즘의 동작 과정

1. **탐색 범위 정의**:

   - 문제에서 찾고자 하는 값의 <mark>최소값</mark>과 <mark>최대값</mark>을 설정한다.

2. **조건 함수 정의**:

   - 특정 값을 기준으로 조건을 만족하는지 확인하는 함수를 작성한다.

3. **이분 탐색 적용**:

   - 탐색 범위의 중간값을 계산하고 조건 함수의 결과에 따라 탐색 범위를 좁힌다.

4. **최적값 반환**:
   - 조건을 만족하는 값 중 <mark>최소값</mark> 또는 <mark>최대값</mark>을 반환한다.

---

# 📦 대표적인 예제

<h2>1. DVD 영상 나누기</h2>

`N`개의 영상이 주어졌을 때, 이를 `M`개의 DVD에 나눠 담으려고 한다. DVD의 **최소 용량** 크기를 구하는 문제이다.

```javascript
function canDivide(sizes, capacity, count) {
  let dvdCount = 1;
  let sum = 0;

  for (let size of sizes) {
    if (sum + size > capacity) {
      dvdCount++;
      sum = size;
    } else {
      sum += size;
    }
  }

  return dvdCount <= count;
}

function findMinDVDSize(sizes, m) {
  let left = Math.max(...sizes); // 한 영상의 최대 크기
  let right = sizes.reduce((a, b) => a + b, 0); // 모든 영상의 합
  let result = right;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (canDivide(sizes, mid, m)) {
      result = mid;
      right = mid - 1;
    } else {
      left = mid + 1;
    }
  }

  return result;
}

const videoSizes = [1, 2, 3, 4, 5, 6, 7, 8, 9];
console.log(findMinDVDSize(videoSizes, 3)); // 결과: 17
```

위 코드는 `canDivide` 함수로 주어진 용량으로 DVD를 나눌 수 있는지 확인하고, `findMinDVDSize` 함수로 이분 탐색으로 최소 용량을 찾는다.

용량이 17일 때를 예로 들면:

- 첫 번째 DVD: 1 + 2 + 3 + 4 + 5 = 15
- 두 번째 DVD: 6 + 7 = 13
- 세 번째 DVD: 8 + 9 = 17

이렇게 3개의 DVD에 모든 영상을 담을 수 있고, 이보다 더 작은 용량으로는 3개의 DVD에 담을 수 없으므로 17이 최소 용량이 된다.

<h2>2. 나무 자르기</h2>

특정 높이로 나무들을 잘랐을 때, 잘린 나무 조각의 합이 `M`미터 이상이 되는 높이의 **최댓값**을 구하는 문제이다.

```javascript
function getWoodAmount(trees, height) {
  return trees.reduce((sum, tree) => {
    return sum + (tree > height ? tree - height : 0);
  }, 0);
}

function findMaxHeight(trees, required) {
  let left = 0;
  let right = Math.max(...trees);
  let result = 0;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);
    let amount = getWoodAmount(trees, mid);

    if (amount >= required) {
      result = mid;
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return result;
}

const trees = [20, 15, 10, 17];
console.log(findMaxHeight(trees, 7)); // 결과: 15
```

위 코드는 `getWoodAmount` 함수로 잘린 나무의 총량을 계산하고, `findMaxHeight` 함수로 이분 탐색을 통해 최대 높이를 찾는다.

높이가 15일 때를 예로 들면:

- 20m 나무: 5m 획득 (20 - 15)
- 15m 나무: 0m 획득 (15 - 15)
- 10m 나무: 0m 획득 (높이가 더 낮음)
- 17m 나무: 2m 획득 (17 - 15)

총 7m의 나무를 얻을 수 있고, 이보다 더 높은 높이로 자르면 7m를 얻을 수 없으므로 15가 최대 높이가 된다.

---

# ⚠️ 결정 알고리즘 주의사항

1. **범위 설정**

   - 정답이 될 수 있는 범위를 정확히 설정해야 한다.
   - 범위가 잘못되면 정답을 찾을 수 없다.

2. **결정 함수 구현**

   - 특정 값이 조건을 만족하는지 판단하는 함수가 정확해야 한다.
   - 결정 함수의 시간 복잡도도 고려해야 한다.

3. **최적해 갱신**

   - 조건을 만족하는 값들 중 최적의 값을 찾아야 한다.
   - 문제의 요구사항에 따라 최대값 또는 최소값을 구해야 한다.
