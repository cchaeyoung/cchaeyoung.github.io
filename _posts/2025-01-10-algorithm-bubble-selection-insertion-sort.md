---
title: "[Algorithm] 버블 정렬, 선택 정렬, 삽입 정렬"
excerpt: "버블 정렬, 선택 정렬, 삽입 정렬의 개념과 구현"

categories:
  - Algorithm
tags:
  - [Algorithm]

permalink: /algorithm/bubble-selection-insertion-sort/

toc: true
toc_sticky: true

date: 2025-01-17
last_modified_at: 2025-01-17
---

# 🔄 정렬 알고리즘이란?

**정렬 알고리즘**은 데이터를 특정한 순서대로 배열하는 알고리즘이다. 보통 숫자는 **오름차순**이나 **내림차순**으로, 문자열은 **사전 순서**로 정렬한다.

이번 포스트에서는 가장 기본적인 세 가지 정렬 알고리즘 **버블 정렬**, **선택 정렬**, **삽입 정렬**을 알아보고자 한다.

---

# 🫧 버블 정렬 (Bubble Sort)

**버블 정렬**은 인접한 두 원소를 비교하여 필요한 경우 위치를 교환하는 방식으로 동작한다. 마치 거품이 수면으로 올라오는 것처럼 큰 값이 끝으로 이동하는 모습에서 이름이 유래했다.

**동작 과정**

- 첫 번째 원소와 두 번째 원소를 비교하여 정렬한다.
- 두 번째 원소와 세 번째 원소를 비교하여 정렬한다.
- 이런 식으로 끝까지 진행한다.
- 위 과정을 배열이 정렬될 때까지 반복한다.

아래는 배열 `[5, 3, 8, 4, 2]`를 <mark>버블 정렬</mark>한 과정이다. 각 단계에서 인접한 두 원소를 비교하여 교환하며 정렬된다.

![bubble sort](/assets/images/posts_img/algorithm/bubble-sort.png)

```javascript
function bubbleSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}
```

**특징**

- **시간복잡도**: O(n²)
- **공간복잡도**: O(1)
- **장점**: 교환 횟수가 **버블 정렬**보다 적다.
- **단점**: 항상 **O(n²)**의 시간복잡도를 가진다.

---

# 🎯 선택 정렬 (Selection Sort)

**선택 정렬**은 배열에서 최소값을 찾아 맨 앞으로 이동시키는 과정을 반복하는 정렬 알고리즘이다.

**동작 과정**

- 전체 원소 중 최소값을 찾는다.
- 최소값을 맨 앞 원소와 교환한다.
- 맨 앞 원소를 제외한 나머지 원소들 중 최소값을 찾는다.
- 위 과정을 반복한다.

아래는 배열 `[5, 3, 8, 4, 2]`를 <mark>선택 정렬</mark>한 과정이다. 각 단계에서 최소값을 찾아 맨 앞으로 이동시키며 정렬된다.

![selection sort](/assets/images/posts_img/algorithm/selection-sort.png)

```javascript
function selectionSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIdx = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIdx]) {
        minIdx = j;
      }
    }
    if (minIdx !== i) {
      [arr[i], arr[minIdx]] = [arr[minIdx], arr[i]];
    }
  }
  return arr;
}
```

**특징**

- **시간복잡도**: O(n²)
- **공간복잡도**: O(1)
- **장점**: 교환 횟수가 **버블 정렬**보다 적다.
- **단점**: 항상 **O(n²)**의 시간복잡도를 가진다.

---

# 📥 삽입 정렬 (Insertion Sort)

**삽입 정렬**은 마치 카드를 정렬하는 방식과 유사하게, 새로운 원소를 이미 정렬된 배열 부분의 적절한 위치에 삽입하는 방식이다.

**동작 과정**

- 두 번째 원소부터 시작한다.
- 이전 원소들과 비교하여 적절한 위치에 삽입한다.
- 세 번째 원소를 이전 원소들과 비교하여 삽입한다.
- 위 과정을 반복한다.

아래는 배열 `[5, 3, 8, 4, 2]`를 <mark>삽입 정렬</mark>한 과정이다. 각 단계에서 새로운 원소를 이미 정렬된 부분에 삽입하며 정렬된다.

![insertion sort](/assets/images/posts_img/algorithm/insertion-sort.png)

```javascript
function insertionSort(arr) {
  const n = arr.length;

  for (let i = 1; i < n; i++) {
    let current = arr[i];
    let j = i - 1;

    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = current;
  }
  return arr;
}
```

**특징**

- **시간복잡도**: O(n²)
- **공간복잡도**: O(1)
- **장점**:
  - 이미 정렬된 배열에 대해 **O(n)**의 시간복잡도를 가진다.
  - **안정적인** 정렬 방식이다.
- **단점**: 배열이 거의 정렬되지 않은 경우 **비효율적**이다.

---

# 📊 성능 비교

세 가지 정렬 알고리즘의 성능을 비교하면 다음과 같다.

| 알고리즘      | 평균 시간복잡도 | 최악 시간복잡도 | 공간복잡도 | 안정성 |
| ------------- | --------------- | --------------- | ---------- | ------ |
| **버블 정렬** | O(n²)           | O(n²)           | O(1)       | 안정   |
| **선택 정렬** | O(n²)           | O(n²)           | O(1)       | 불안정 |
| **삽입 정렬** | O(n²)           | O(n²)           | O(1)       | 안정   |

**선택 정렬이 불안정한 이유**: 값이 같은 요소를 교환할 때 기존의 상대적인 순서가 유지되지 않기 때문이다.

<h3>🤔 어떤 정렬을 사용해야 하는가?</h3>

- **버블 정렬**: **구현이 간단**하거나 **학습용**으로 적합하다.
- **선택 정렬**: **교환 횟수**를 최소화할 때 유용하다.
- **삽입 정렬**: **거의 정렬된 배열**이나 **작은 데이터셋**에 적합하다.
