---
title: "[Algorithm] 이분 탐색(Binary Search)"
excerpt: "이분 탐색 알고리즘의 개념과 예제 문제"

categories:
  - Algorithm
tags:
  - [Algorithm]

permalink: /algorithm/binary-search/

toc: true
toc_sticky: true

date: 2025-01-19
last_modified_at: 2025-01-19

future: true
published: true
---

# 🔍 이분 탐색이란?

**이분 탐색(Binary Search)**은 **정렬된 배열**에서 특정 값을 찾는 알고리즘이다. 중간값을 기준으로 배열을 절반으로 나누어 탐색 범위를 좁혀가며 원하는 값을 찾아낸다.

<h3>이분 탐색의 특징</h3>

- 반드시 **정렬된 배열**에서만 사용할 수 있다.
- 탐색할 때마다 범위가 절반으로 줄어든다.
- 매우 큰 데이터에서 효율적인 탐색이 가능하다.
- **시간 복잡도**는 `O(log N)`으로, 선형 탐색에 비해 훨씬 빠르다. (선형 탐색: `O(N)`)

![binary-search](/assets/images/posts_img/algorithm/binary-search.png)

위 그림은 `[1, 3, 5, 7, 9, 11, 13, 15]` 배열에서 9를 찾는 이분 탐색 과정이다.

---

# 📊 이분 탐색의 동작 과정

1. **초기화**: 탐색 범위의 시작점(left)과 끝점(right)을 설정한다.
2. **중간값 계산**: 현재 범위의 중간 위치(mid)를 계산한다.
3. **비교**:
   - 중간값이 찾는 값과 같으면 탐색을 완료하고 중간 인덱스를 반환한다.
   - 중간값이 찾는 값보다 크면, 오른쪽 범위는 제외하고 왼쪽 범위로 탐색 범위를 좁힌다.
   - 중간값이 찾는 값보다 작으면, 왼쪽 범위는 제외하고 오른쪽 범위로 탐색 범위를 좁힌다.
4. **반복**: 찾는 값을 찾을 때까지 2-3단계를 반복한다.

---

# 🌟 대표적인 예제

<h2>1. 기본적인 이분 탐색</h2>

**정렬된 배열**에서 **특정 값의 인덱스**를 찾는 기본적인 이분 탐색 문제이다.

이분 탐색은 중간값을 기준으로, 찾고자 하는 값이 중간값보다 작으면 왼쪽 절반을, 크면 오른쪽 절반을 탐색하는 방식이다. 이를 반복하여 원하는 값을 찾거나 범위가 없을 때까지 진행한다.

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid; // 찾는 값의 인덱스 반환
    }

    if (arr[mid] > target) {
      right = mid - 1; // 왼쪽 부분 탐색
    } else {
      left = mid + 1; // 오른쪽 부분 탐색
    }
  }

  return -1; // 찾는 값이 없는 경우
}

const arr = [1, 3, 5, 7, 9, 11, 13, 15];
console.log(binarySearch(arr, 7)); // 결과: 3
```

위 코드는 배열에서 7이 어느 위치에 있는지 찾아 해당 인덱스를 반환한다.  
배열의 중간값인 7을 찾아서, 그 위치인 3을 반환하게 된다.

<h2>2. Lower Bound / Upper Bound</h2>

**Lower Bound**와 **Upper Bound**는 정렬된 배열에서 특정 값이 처음 또는 마지막으로 나타나는 위치를 찾는 문제이다.

**Lower Bound**는 배열에서 주어진 값 이상이 처음 나타나는 위치를 찾는다. 예를 들어, 배열에서 값 2 이상의 첫 번째 값을 찾고 싶을 때 사용한다.

**Upper Bound**는 배열에서 주어진 값보다 큰 값이 처음 나타나는 위치를 찾는다. 예를 들어, 배열에서 값 2보다 큰 첫 번째 값을 찾고 싶을 때 사용한다.

```javascript
// Lower Bound: 찾고자 하는 값 이상이 처음 나타나는 위치
function lowerBound(arr, target) {
  let left = 0;
  let right = arr.length;

  while (left < right) {
    let mid = Math.floor((left + right) / 2);

    if (arr[mid] >= target) {
      right = mid;
    } else {
      left = mid + 1;
    }
  }

  return left;
}

// Upper Bound: 찾고자 하는 값을 초과하는 값이 처음 나타나는 위치
function upperBound(arr, target) {
  let left = 0;
  let right = arr.length;

  while (left < right) {
    let mid = Math.floor((left + right) / 2);

    if (arr[mid] > target) {
      right = mid;
    } else {
      left = mid + 1;
    }
  }

  return left;
}

const arr = [1, 2, 2, 2, 3];
console.log(lowerBound(arr, 2)); // 결과: 1
console.log(upperBound(arr, 2)); // 결과: 4
```

**Lower Bound**: 2 이상이 처음 나타나는 위치는 인덱스 1이다. 따라서 `lowerBound(arr, 2)`는 1을 반환한다.

**Upper Bound**: 2보다 큰 값이 처음 나타나는 위치는 인덱스 4이다. 따라서 `upperBound(arr, 2)`는 4를 반환한다.

---

# ⚠️ 이분 탐색 주의사항

1. **배열 정렬 필수**

   - 이분 탐색은 **정렬된 배열**에서만 동작한다.
   - 배열을 정렬하는 데 드는 비용도 고려해야 한다.

2. **중간값 계산 시 오버플로우 주의**

   - `(left + right) / 2` 대신 `left + (right - left) / 2`를 사용해야 한다.
   - `left + (right - left) / 2`는 두 값 `left`와 `right`의 합이 아닌, 두 값의 차이를 먼저 계산하고 나누기 때문에 오버플로우를 피할 수 있다.

3. **무한 루프 방지**

   - `while` 조건문과 종료 조건을 정확히 설정해야 한다.
   - `left`와 `right` 포인터가 적절히 이동하는지 확인한다.
   - 탐색 범위가 계속 줄어들도록 구현해야 한다.
