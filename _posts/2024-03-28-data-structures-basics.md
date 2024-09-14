---
title: "[Data Structures] 기본 자료구조 개념"
excerpt: "스택, 큐, 이진 트리, 이진 힙"

categories:
  - Data Structures
tags:
  - [Data Structures]

permalink: /data-structures/1

toc: true
toc_sticky: true

date: 2024-03-28
last_modified_at: 2024-03-28
---

## 스택과 큐

<br/>

### 스택
스택이란 한 쪽 끝에서만 항목을 삭제하거나 새로운 item을 저장하는 자료구조이다.

push: 새 item을 삽입하는 연산

pop: Top item을 삭제하는 연산

스택은 후입 선출(Last-In First-Out, LIFO)이다.

### 큐
큐란 삽입과 삭제가 양 끝에서 각각 수행되는 자료구조, 즉 먼저 들어온 데이터가 먼저 나가는 자료구조이다.

큐는 선입 선출(First-In First-Out, FIFO)이다.

삽입은 큐의 후단(rear)에서, 삭제는 전단(front)에서 이루어진다.

## 이진 트리와 이진 힙

<br/>

### 트리 용어
루트(Root) : 트리의 최상위에 있는 노드

자식(Child) : 노드 하위에 연결된 노드

부모(Parent) : 노드의 상위에 연결된 노드

이파리(Leaf) : 자식 없는 노드, 외부 노드

형제(Sibling) : 동일한 부모를 가지는 노드

조상(Ancestor) : 루트까지의 경로상에 있는 모든 노드

후손(Descendant) : 노드 아래로 매달린 모든 노드

서브 트리(Subtree) : 노드 자신과 후손으로 구성된 트리

레벨(Level) : 루트는 레벨 1, 아래 층으로 내려가며 레벨 1씩 증가, 레벨은 깊이(Depth)와 동일

높이(Height) : 트리의 최대 레벨

키(Key) : 탐색에 사용되는 노드에 저장된 정보

내부 노드(internal node) : 이파리가 아닌 노드

외부 노드(external or terminal node) : 이파리

자식 노드의 개수를 노드의 차수

모든 이파리의 노드는 자식이 없어서 0차 노드

### 이진 트리
포화 이진 트리(Perfect Binary Tree): 모든 이파리의 깊이가 같고 각 내부 노드가 2개의 자식을 가지는 트리

완전 이진트리(Complete Binary Tree): 마지막 레벨을 제외한 각 레벨이 노드로 꽉 차있고, 마지막 레벨에는 노드가 왼쪽부터 빠짐없이 채워진 트리

### 이진 힙
이진 힙은 완전 이진트리로서 부모의 우선순위가 자식의 우선순위보다 높은 자료구조

우선순위 큐(Priority Queue)를 구현하는 가장 기본적인 자료구조

우선순위 큐(Priority Queue) : 가장 높은 우선순위를 가진 항목에 접근 및 삭제하거나, 임의의 우선순위를 가진 항목의 삽입을 지원하는 자료구조

스택이나 큐도 일종의 우선순위 큐

스택: 가장 마지막으로 삽입된 항목이 가장 높은 우선순위를 가지므로, 최근 시간일수록 높은 우선순위 부여

큐: 먼저 삽입된 항목이 우선순위가 더 높다. 따라서 이른 시간일수록 더 높은 우선순위 부여
이진 힙의 종류

최소 힙 : 키가 작을수록 높은 우선순위

최대 힙 : 키가 클수록 더 높은 우선순위

### 이진 힙 연산의 수행 시간
가장 높은 우선순위를 접근하는 시간 O(1)

이진 힙에서 삽입과 삭제는 힙 속성을 회복시키기 위해 각각 O(logn)