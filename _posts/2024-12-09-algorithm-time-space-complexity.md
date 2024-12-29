---
title: "[Algorithm] 알고리즘의 시간 복잡도와 공간 복잡도"
excerpt: "알고리즘의 성능을 평가하는 시간 복잡도와 공간 복잡도 개념 이해"

categories:
  - Algorithm
tags:
  - [Algorithm]

permalink: /algorithm/algorithm-time-space-complexity/

toc: true
toc_sticky: true

date: 2024-12-09
last_modified_at: 2024-12-09
---

# 🕰️ 알고리즘에서 복잡도란 무엇인가?

**복잡도(Complexity)**는 알고리즘의 성능을 측정하는 중요한 지표이다.

알고리즘이 얼마나 효율적으로 문제를 해결하는지 평가하는 기준으로, 주로 **시간 복잡도**와 **공간 복잡도**로 나눈다.

- **시간 복잡도**: 알고리즘이 실행되는 데 걸리는 시간
- **공간 복잡도**: 알고리즘이 수행되는 동안 사용하는 메모리 양

---

# ⏱️ 시간 복잡도

**시간 복잡도**는 알고리즘이 **입력 크기**에 따라 **얼마나 오래 실행되는지**를 나타낸다.

## 🔢 시간 복잡도 표기법

알고리즘의 성능을 수학적으로 표현할 때 주로 **Big-O 표기법**을 사용한다. **Big-O 표기법**은 알고리즘의 시간 복잡도를 **최악의 경우**를 기준으로 나타내며, 알고리즘의 효율성을 쉽게 비교할 수 있게 해준다.

1. **O(1) – 상수 시간**  
   입력 크기와 관계없이 일정한 시간이 걸리는 알고리즘을 의미한다.

   배열의 첫 번째 요소를 접근하는 것과 같은 작업은 O(1)이다.

   ```javascript
   function constantTime(arr) {
     return arr[0]; // 항상 첫 번째 요소 반환
   }
   ```

2. **O(n) – 선형 시간**  
   입력 크기 n에 비례하여 시간이 증가하는 알고리즘을 의미한다.

   배열에서 모든 요소를 순차적으로 검색하는 경우 O(n)이 된다.

   ```javascript
   function linearSearch(arr, target) {
     for (let i = 0; i < arr.length; i++) {
       if (arr[i] === target) return i;
     }
     return -1;
   }
   ```

3. **O(n^2) – 이차 시간**  
   중첩된 반복문을 사용할 때 자주 나타나는 시간 복잡도이다. 이차 시간 복잡도는 입력 크기 n에 대해 시간이 n의 제곱에 비례하여 증가한다.

   버블 정렬이나 선택 정렬 같은 정렬 알고리즘에서 O(n^2)가 발생한다.

   ```javascript
   function bubbleSort(arr) {
     for (let i = 0; i < arr.length; i++) {
       for (let j = 0; j < arr.length - i - 1; j++) {
         if (arr[j] > arr[j + 1]) {
           [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]; // 두 값 교환
         }
       }
     }
     return arr;
   }
   ```

4. **O(log n) – 로그 시간**  
   이진 탐색과 같이, 입력 크기를 절반씩 나누면서 문제를 해결하는 알고리즘에서 나타나는 시간 복잡도이다. 이 알고리즘은 효율적으로 작동하며, 입력 크기가 커져도 시간이 그리 많이 증가하지 않는다.

   정렬된 배열에서 값을 찾기 위해 사용하는 이진 탐색 알고리즘이 O(log n)이다.

   ```javascript
   function binarySearch(arr, target) {
     let low = 0,
       high = arr.length - 1;
     while (low <= high) {
       let mid = Math.floor((low + high) / 2);
       if (arr[mid] === target) return mid;
       else if (arr[mid] < target) low = mid + 1;
       else high = mid - 1;
     }
     return -1;
   }
   ```

5. **O(n log n) – 선형 로그 시간**  
    **합병 정렬(Merge Sort)**이나 **퀵 정렬(Quick Sort)**과 같은 정렬 알고리즘은 **O(n log n)**의 시간 복잡도를 가진다. 이 알고리즘들은 입력 크기에 대해 선형적인 요소와 로그적인 요소가 결합된 형태로 시간이 증가한다.

   병합 정렬의 알고리즘은 O(n log n)이다.

   ```javascript
   function mergeSort(arr) {
     if (arr.length <= 1) return arr;
     const mid = Math.floor(arr.length / 2);
     const left = mergeSort(arr.slice(0, mid));
     const right = mergeSort(arr.slice(mid));
     return merge(left, right);
   }

   function merge(left, right) {
     let result = [];
     while (left.length && right.length) {
       result.push(left[0] < right[0] ? left.shift() : right.shift());
     }
     return result.concat(left, right);
   }
   ```

💡 시간 복잡도가 작은 알고리즘일수록 더 효율적이고, **O(1) < O(log n) < O(n) < O(n log n) < O(n^2)** 순으로 **효율성이 떨어진다.**

---

# 💾 공간 복잡도

**공간 복잡도**는 알고리즘이 실행되는 동안 사용하는 **메모리 양**을 나타낸다.

## 📦 공간 복잡도 표기법

공간 복잡도를 분석할 때도 **Big-O 표기법**을 사용하여 알고리즘이 사용하는 메모리 양을 나타낸다.

1. **O(1) – 상수 공간**  
   입력 크기와 관계없이 일정한 양의 메모리를 사용하는 알고리즘을 의미한다. 이 경우 알고리즘의 공간 복잡도는 입력 크기와 무관하게 일정하다.

   배열에서 첫 번째 요소를 반환하는 알고리즘은 O(1)의 공간 복잡도를 가진다.

   ```javascript
   function constantSpace(arr) {
     let firstElement = arr[0]; // 첫 번째 요소를 저장하는데 고정된 공간만 사용
     return firstElement;
   }
   ```

2. **O(n) – 선형 공간**  
   입력 크기 n에 비례하여 메모리 사용량이 증가하는 알고리즘을 의미한다.

   배열을 그대로 복사하는 알고리즘은 O(n)의 공간 복잡도를 가진다.

   ```javascript
   function copyArray(arr) {
     let newArr = [];
     for (let i = 0; i < arr.length; i++) {
       newArr[i] = arr[i]; // 배열의 크기와 비례하는 공간을 사용
     }
     return newArr;
   }
   ```

3. **O(n^2) – 이차 공간**  
   이차 공간 복잡도는 중첩된 데이터 구조나 배열을 사용해야 할 때 나타난다.

   2D 배열을 생성하는 알고리즘에서는 O(n^2)의 공간 복잡도를 가진다.

   ```javascript
   function create2DArray(n) {
     let arr = [];
     for (let i = 0; i < n; i++) {
       arr[i] = new Array(n); // 2D 배열을 생성, n^2의 공간 사용
     }
     return arr;
   }
   ```

4. **O(log n) – 로그 공간**  
   이 공간 복잡도는 보통 재귀 알고리즘에서 발생한다.

   이진 탐색에서 사용하는 공간은 O(log n)입니다.

   ```javascript
   function binarySearchSpace(arr, target, low, high) {
     if (low > high) return -1;
     let mid = Math.floor((low + high) / 2);
     if (arr[mid] === target) return mid;
     else if (arr[mid] < target)
       return binarySearchSpace(arr, target, mid + 1, high);
     else return binarySearchSpace(arr, target, low, mid - 1);
   }
   ```

5. **O(2^n) – 지수 공간**  
   지수 공간 복잡도는 주로 재귀적인 문제에서 발생하며, 특히 하위 문제를 중복해서 해결할 때 나타난다.

   피보나치 수열을 계산하는 재귀적 알고리즘은 O(2^n)의 공간 복잡도를 가진다.

   ```javascript
   function fibonacci(n) {
     if (n <= 1) return n;
     return fibonacci(n - 1) + fibonacci(n - 2); // 지수적인 공간 복잡도
   }
   ```

💡 공간 복잡도가 작은 알고리즘일수록 더 효율적이고, **O(1) < O(log n) < O(n) < O(n^2) < O(2^n)** 순서로 **효율성이 떨어진다.**

---

# 🚀 복잡도 분석의 중요성

알고리즘을 설계하고 선택하는 과정에서 **시간 복잡도**와 **공간 복잡도**를 이해하는 것은 중요하다. 이를 통해 효율적인 알고리즘을 선택하고 성능을 최적화할 수 있다.

1. **효율적인 자원 관리**  
   메모리가 제한된 환경에서는 공간 복잡도가 중요한 성능 지표가 된다. O(1) 또는 O(n) 공간 복잡도를 가진 알고리즘을 선택하는 것이 효율적이다.
2. **최적화 및 성능 개선**  
   알고리즘의 복잡도를 분석하여 실행 시간을 단축시키고 더 나은 성능을 구현할 수 있다. **O(n)**에서 **O(log n)**로 최적화할 수 있는 경우 성능을 크게 향상시킬 수 있다.
3. **시스템 성능 예측**  
   복잡도 분석을 통해 알고리즘의 성능을 예측하고, 데이터 크기나 시스템 환경에 맞는 최적의 알고리즘을 선택할 수 있다.

---

알고리즘 선택 시 문제의 특성과 데이터 크기를 고려하여 가장 적합한 알고리즘을 선택하는 것이 중요하다.
