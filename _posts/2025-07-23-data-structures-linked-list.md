---
title: "[Data Structures] 연결리스트"
excerpt: "연결리스트의 구조와 동작 원리"

categories:
  - Data Structures
tags:
  - [Data Structures]

permalink: /data-structures/data-structures-concept/

toc: true
toc_sticky: true

date: 2025-07-23T06:00:00
last_modified_at: 2025-07-27
---

배열은 우리가 가장 많이 사용하는 자료구조지만, 크기가 고정되어 있고 중간에 요소를 삽입하거나 삭제할 때 비효율적이다. 이런 배열의 단점을 해결하기 위해 등장한 것이 바로 **연결리스트**다.

---

# 🔗 연결리스트란?

## 📦 기본 구조

연결리스트는 **노드(Node)** 라는 단위로 구성된다. 각 노드는 **데이터**와 **다음 노드를 가리키는 포인터**를 가지고 있다.

- **데이터 필드**: 리스트의 원소, 즉 데이터 값을 저장하는 곳
- **링크 필드**: 다른 노드의 주소값을 저장하는 장소

![linked-list-node](/assets/images/posts_img/data-structures/linked-list-node.png)

마치 기차처럼 각 칸(노드)이 다음 칸과 연결되어 있는 구조다. 첫 번째 칸을 알면 줄줄이 따라가서 모든 칸에 접근할 수 있다.

![linked-list](/assets/images/posts_img/data-structures/linked-list.png)

```javascript
class Node {
  constructor(data) {
    this.data = data; // 실제 저장할 데이터
    this.next = null; // 다음 노드를 가리키는 포인터
  }
}

// 연결리스트 예시
const node1 = new Node("첫번째");
const node2 = new Node("두번째");
const node3 = new Node("세번째");

node1.next = node2; // 첫번째 → 두번째
node2.next = node3; // 두번째 → 세번째
node3.next = null; // 세번째 → 끝
```

## ⚖️ 배열 vs 연결리스트

<h3>🗃️ 배열 </h3>

배열은 메모리 공간에 데이터가 연속적으로 저장되는 자료구조다.

각 데이터는 인덱스로 빠르게 접근할 수 있어 조회 속도가 매우 빠르다.

하지만 크기가 고정되어 있어, 크기를 변경하려면 새 배열을 만들어야 한다는 단점이 있다.

<h3>🧵 연결리스트</h3>

연결리스트는 데이터가 메모리 상에 흩어져 저장되며, 각 데이터는 다음 데이터의 위치를 가리키는 포인터를 가지고 있다.

따라서 처음부터 순차적으로 하나씩 찾아가야 하기 때문에 조회 속도가 느리다.

하지만 데이터의 삽입과 삭제가 용이하며, 크기를 동적으로 조절할 수 있다는 장점이 있다.

## 💡 언제 사용할까?

**연결리스트가 유리한 경우**

- 데이터의 개수를 미리 알 수 없을 때
- 중간에 삽입/삭제가 자주 일어날 때
- 메모리를 효율적으로 사용해야 할 때

**배열이 유리한 경우**

- 특정 위치의 데이터에 자주 접근할 때
- 데이터 크기가 고정되어 있을 때
- 메모리 사용량을 예측해야 할 때

---

# 🧩 연결 리스트의 종류

## ➡️ 단순 연결 리스트

단순 연결 리스트는 각 노드가 오직 다음 노드만 가리키는 가장 기본적인 형태다.

![singly-linked-list](/assets/images/posts_img/data-structures/singly-linked-list.png)

- 한 방향(앞→뒤)으로만 순회할 수 있다.

- 구현이 간단하고, 메모리 사용량이 적다.

## 🔄 원형 연결 리스트

원형 연결 리스트는 마지막 노드가 다시 첫 번째 노드를 가리켜 원형을 이루는 구조다.

![circular-linked-list](/assets/images/posts_img/data-structures/circular-linked-list.png)

- 리스트의 끝이 없기 때문에, 순환 구조가 필요할 때 유용하다.

## 🔁 이중 연결 리스트

이중 연결 리스트는 각 노드가 이전 노드와 다음 노드 모두를 가리키는 구조다.

![doubly-linked-list](/assets/images/posts_img/data-structures/doubly-linked-list.png)

- 양방향으로 순회할 수 있어 더 유연하다.

- 삭제나 삽입 시 특정 노드를 더 쉽게 접근 가능하지만, 메모리 사용량이 더 많고 구현이 복잡하다.

---

# ✅ 연결리스트의 장단점

<h2>👍 장점</h2>

- 동적으로 크기를 조절할 수 있어 유연하다.

- 중간이나 앞부분에서 삽입/삭제가 빠르게 일어난다.

- 메모리가 연속적으로 할당되지 않아도 되어 효율적으로 사용할 수 있다.

<h2>👎 단점</h2>

- 특정 위치에 접근하려면 처음부터 순차적으로 탐색해야 하므로 느리다.

- 각 노드마다 포인터를 저장해야 하므로 메모리 사용이 증가한다.

- 메모리 상에 흩어져 저장되므로 캐시 효율성이 떨어질 수 있다.
