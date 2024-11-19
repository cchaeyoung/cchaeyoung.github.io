---
title: "[Computer Architecture] 컴퓨터 기억장치 시스템 개요 및 캐시 설계"
excerpt: "컴퓨터 기억장치 시스템의 개요와 캐시 설계 요소에 대한 설명"

categories:
  - Computer Architecture
tags:
  - [Computer Architecture]

permalink: /computer-architecture/memory-cache-system/

toc: true
toc_sticky: true

date: 2024-09-24
last_modified_at: 2024-10-27
---

# 🖥️ 컴퓨터 기억장치 시스템 개요

컴퓨터에서 **기억장치(memory)**는 프로그램 명령어와 데이터를 저장하고, 프로그램 실행을 지원하는 핵심 요소이다. 메모리는 **프로세서와 입출력 장치** 사이에서 작업을 수행하며, 컴퓨터가 작동하는 동안 프로그램이 데이터를 저장하고 불러오는 데 필수적이다.

## 📝 기억장치의 주요 특성

기억장치는 다음과 같은 특성에 따라 성능이 결정된다.

- **용량(Capacity)**: 기억장치의 크기를 나타내며, 내부 기억장치의 용량은 바이트(byte) 또는 단어(word) 단위로 측정된다. 외부 기억장치의 용량은 일반적으로 바이트 단위로 표현된다.
- **전송 단위(Transfer Unit)**: 데이터를 읽고 쓸 때 한 번에 전송되는 최소 단위로, 내부 기억장치에서는 데이터 버스의 폭에 의해 결정된다.
- **액세스 방식(Access Method)**: 데이터를 읽고 쓰는 방법에 따라 순차적, 직접, 임의, 연관 액세스 방식으로 나뉜다.

<h3> 기억장치의 계층구조</h3>

기억장치는 성능과 비용의 균형을 맞추기 위해 **계층적으로** 구성된다. 레지스터, 캐시, 주기억장치(RAM), 디스크와 같은 여러 레벨의 기억장치는 용량과 액세스 속도에 따라 상호 작용하며 전체 시스템 성능을 최적화한다.

---

# 💭 캐시 기억장치의 원리

**캐시 기억장치**는 프로세서와 메인 메모리 사이에 위치하여 자주 사용되는 데이터를 저장해 성능을 향상시킨다. 캐시는 작은 용량이지만 매우 빠른 속도로 액세스할 수 있는 메모리로, 주기억장치보다 접근 속도가 훨씬 빠르다.

## 🔄 지역성(Locality) 원리

- **시간적 지역성(Temporal Locality)**: 최근에 사용된 데이터가 다시 사용될 가능성이 높다.
- **공간적 지역성(Spatial Locality)**: 현재 참조된 메모리 주소와 인접한 주소의 데이터가 곧 참조될 가능성이 높다.

---

# 🛠️ 캐시 설계 요소

캐시 설계에서 중요한 요소는 **캐시 크기, 주소 매핑 방식, 교체 알고리즘, 쓰기 정책**이다.

<h2>캐시 크기</h2>

캐시의 크기는 성능에 중요한 영향을 미치며, 너무 작으면 적중률이 떨어지고, 너무 크면 속도가 느려질 수 있다.

<h2>주소 매핑 방식</h2>

- **직접 사상(Direct Mapping)**: 주기억장치의 특정 블록이 캐시의 특정 라인에만 할당된다.
- **연관 사상(Associative Mapping)**: 주기억장치 블록이 캐시의 어느 라인으로도 할당 가능하다.
- **세트 연관 사상(Set Associative Mapping)**: 캐시를 여러 세트로 나누어 각 세트 내에서 연관 사상을 적용한다.

<h2>교체 알고리즘</h2>

캐시가 꽉 찼을 때 어떤 블록을 교체할지 결정하는 알고리즘이다.

- **LRU(최소 최근 사용)**: 가장 오래 사용되지 않은 블록을 교체한다.
- **FIFO(선입선출)**: 캐시에 가장 오래 머문 블록을 교체한다.
- **Random**: 임의로 블록을 교체한다.

<h2>쓰기 정책(Write Policy)</h2>

- **Write-Through**: 데이터를 캐시와 주기억장치에 동시에 기록한다.
- **Write-Back**: 데이터를 캐시에만 기록하고, 캐시가 교체될 때 주기억장치로 반영한다.

---

# 🚀 캐시 조직의 예

캐시 메모리는 **L1, L2, L3**와 같은 **다단계 구조**로 이루어져 있으며, 각 단계는 프로세서에 가까운 순서대로 더 빠르고 작아진다.

- **L1 캐시**: 가장 빠른 캐시로 프로세서 내부에 위치한다.
- **L2 캐시**: L1 캐시보다 크지만 속도가 느리다.
- **L3 캐시**: 시스템 성능을 높이기 위해 더 큰 용량을 제공한다.

<h2>캐시의 크기와 적중률</h2>

캐시의 크기가 커질수록 적중률이 높아지지만, 너무 크면 성능이 저하될 수 있다. 일반적으로 L1 캐시는 32KB~64KB, L2 캐시는 256KB~1MB, L3 캐시는 수 MB~수십 MB 범위를 사용한다.

---

# 📊 기억장치의 성능 평가

기억장치 성능은 **적중률**, **액세스 시간**, **전송 속도** 등 여러 요소에 의해 평가된다. **다단계 기억장치**는 이러한 성능 요소를 최적화하는 중요한 설계 전략으로, 빠른 기억장치와 대용량 기억장치 간의 트레이드오프를 해결한다.