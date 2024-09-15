---
title: "[Computer Architecture] 컴퓨터 성능 향상과 평가"
excerpt: "컴퓨터 성능 향상과 평가 방법"

categories:
  - Computer Architecture
tags:
  - [Computer Architecture]

permalink: /computer-architecture/performance-enhancement/

toc: true
toc_sticky: true

date: 2024-09-14
last_modified_at: 2024-09-14
---

# ⚡ 컴퓨터 성능 향상
컴퓨터 시스템의 가격은 하락하고 있는 한 편, 시스템들의 성능과 용량은 계속 향상되고 있다. 

## 🔋 마이크로프로세서 성능 향상

마이크로프로세서의 성능은 **트랜지스터 집적도의 증가**와 **멀티코어 기술**로 크게 향상되었다.
- **트랜지스터 집적도 증가**: 트랜지스터 수가 급격히 증가하여 동시에 처리할 수 있는 작업량이 늘어났다.
- **멀티코어 기술**: 여러 개의 프로세서 코어를 탑재하여 작업을 병렬로 처리할 수 있다. 

비록 클럭 속도는 더 이상 크게 증가하지 않지만, 멀티코어와 높은 집적도로 성능은 여전히 향상되고 있다.

<h3><strong>성능 균형 문제</strong></h3>
최근에는 프로세서 속도가 크게 향상되고 기억 용량도 대폭 증가했으나, **프로세서와 주기억장치 간의 인터페이스에서 병목**이 발생할 수 있다. 이는 프로세서가 신속하게 작업을 처리하더라도, 메모리 접근 속도가 상대적으로 느리면 전체 성능이 제한될 수 있음을 의미한다.

또한, **입출력(I/O) 장치와의 성능 균형 문제**도 존재한다. 현대의 I/O 장치는 데이터 전송 속도가 비약적으로 증가했지만, 프로세서와 I/O 장치 간의 데이터 이동에서 여전히 병목이 발생할 수 있다. 특히 높은 I/O 요구를 가진 응용 프로그램에서는 이러한 성능 균형 문제로 인해 시스템의 전반적인 성능이 저하될 수 있다.


<h3><strong>프로세서의 속도 향상 방안</strong></h3>

1. **프로세서 하드웨어 속도 증가**  
   - 논리 게이트의 크기를 줄이고, 더 많은 게이트를 조밀하게 배치하여 **클럭 속도를 높인다**.
   - 신호의 전파 시간을 감소시켜 전반적인 성능을 향상시킬 수 있다. 

2. **캐시 메모리의 크기와 속도 증가**  
   - 프로세서와 주기억장치 사이에 **캐시를 배치**하여 캐시 액세스 시간을 줄인다. 캐시의 크기와 속도를 증가시키면 데이터 접근 시간이 단축되어 성능이 향상된다.

3. **명령어 실행 속도 향상**  
   - 프로세서의 조직과 구조를 변경하여 명령어 실행 속도를 높일 수 있다.  
    **파이프라이닝**을 통해 명령어의 처리 과정을 여러 단계로 나누어 동시에 진행할 수 있고, **수퍼스칼라 아키텍처**는 한 클럭 사이클에 여러 명령어를 동시에 처리하여 성능을 높인다. 이러한 기술들은 **명령어 처리의 병렬성**을 제공하여 프로세서의 속도를 크게 개선한다.

## 🕰️ 클럭 속도와 회로 밀도 문제

프로세서의 클럭 속도를 높이면 성능이 향상되지만, 동시에 **전력 밀도 문제**가 발생한다. 전력 밀도는 칩의 단위 면적당 소비되는 전력을 의미하며, 클럭 속도가 높아질수록 증가한다. 이는 트랜지스터가 더 빠르게 동작하면서 더 많은 전력을 소모하기 때문이다.

**트랜지스터 하나가 소비하는 전력:** 논리 값이 한 번 바뀔 때 소모되는 에너지 × 시간당 논리 값이 바뀌는 빈도

이러한 전력 소모 문제로 인해, 최신 프로세서들은 클럭 속도를 일정 수준에서 유지하며, 보통 3GHz에서 4GHz 사이로 안정화된 상태를 보인다. 이는 성능 향상과 전력 소비 간의 균형을 맞추기 위한 조치이다.

## 🔄 성능 향상을 위한 새로운 시도 – 멀티코어 (Multicore)

멀티코어 프로세서는 하나의 칩에 여러 개의 프로세서를 배치하여 성능을 향상시키는 기술이다. 
- **큰 용량의 캐시를 공유**하는 여러 프로세서를 하나의 칩에 배치함으로써, 기억장치 회로의 소비전력보다 프로세서 회로의 소비전력이 훨씬 적다. 
- 복잡한 프로세서 하나를 사용하는 대신, 칩 내에 더 **간단한 여러 프로세서를 배치**하면 성능이 더 향상된다. 성능 향상은 복잡도 증가의 제곱근에 비례한다. **소프트웨어**가 여러 프로세서를 효과적으로 활용할 수 있도록 지원한다면, 프로세서 개수만큼의 성능 향상을 기대할 수 있다.

멀티코어 구조는 성능 향상과 전력 효율성을 동시에 고려한 기술로, 성능을 극대화하고 전력 소모를 최소화하는 데 중요한 역할을 한다.

---

# 📊 컴퓨터의 성능 평가
컴퓨터 성능을 평가할 때는 성능, 비용, 크기, 전력 소모, 보안, 신뢰성 등을 고려한다. 성능 평가의 관점은 사용자 관점과 시스템 관점으로 나눌 수 있다.

1. **사용자 관점**  
   **응답 시간 또는 실행 시간**: 컴퓨터가 태스크를 완료하기까지의 총 소요 시간을 의미하며, 디스크 접근, 메모리 접근, 입출력 작업, 운영체제의 오버헤드 및 CPU 시간을 포함한다.

2. **시스템 관점**  
   **처리량 또는 대역폭**: 일정한 시간 동안 처리하는 작업의 양을 의미한다. 

시스템의 종류에 따라 적절한 성과 평가 지표를 적용해야 한다.  
예를 들어, 임베디드 시스템과 데스크톱 PC는 응답 시간을 중요시하며, 서버는 처리량을 중시한다.

## 📈 성능의 정의

- **프로그램의 실행 시간**  
  - 벽시계 시간, 응답 시간, 경과 시간:  
  한 작업을 완료하는 데 필요한 전체 시간으로 디스크 접근, 메모리 접근, 입출력 작업, 운영체제 오버헤드 등 모든 시간을 더한 것이다.
  - CPU 실행 시간 (CPU 시간):  
  프로세서가 순수하게 프로그램을 실행하는 데 소비한 시간이다.

- **성능의 정의**  
    - 성능 = 1 / 수행 시간
    - 성능 = 1 / CPU 수행 시간
    - CPU 수행시간 = 명령어 수 × 명령어 당 클럭 사이클 수 × 사이클당 초 = 명령어 수 × CPI / 클럭 속도

## 🧮 성능에 영향을 미치는 요소
1. **클럭 속도 (Clock Rate)**  
   클럭 신호는 연속적인 신호 파형을 생성하는 수정 결정판에 의해 생성된다. 프로세서의 속도는 클럭 신호에 의해 발생되는 펄스 주파수에 의해 결정된다.

2. **명령어 당 사이클 수 (CPI)**   
    - 하나의 명령어를 수행하기 위해서 소요되는 클럭 사이클 수  
    ![CPI](/assets/images/posts_img/computer-architecture/CPI.png)
    - 주어진 프로그램을 수행하는 데 필요한 프로세서 시간 T  
    ![T](/assets/images/posts_img/computer-architecture/T-1.png)
    - 명령어 실행 및 기억장치 이동시간 등을 고려한 프로세서 시간 T  
    ![T](/assets/images/posts_img/computer-architecture/T-2.png)

## 🚀 암달의 법칙 (Amdahl’s Law)
- 암달의 법칙은 다수의 프로세서를 사용한 프로그램의 잠재적 속도 향상 정도를 다룬다. 
- N개의 프로세서를 가진 병렬 프로세서를 사용하여 프로그램의 병렬 부분을 완전히 이용하는 경우에 얻을 수 있는 속도 향상을 나타낸다.
    ![speedup](/assets/images/posts_img/computer-architecture/speedup.png)

## 🔢 프로세서의 성능 척도

1. **MIPS (Millions of Instructions Per Second)**  
   초당 백만 명령어 수이다.  
     ![MIPS](/assets/images/posts_img/computer-architecture/MIPS.png)

2. **MFLOPS (Millions of Floating Point Operations Per Second)**  
   부동소수점 성능으로, 한 프로그램에서 수행되는 부동소수점 연산들의 수를 (수행 시간 × 10<sup>6</sup>
)으로 나눈 값이다.

## 📏 벤치마크 (benchmark)

벤치마크는 기계 성능의 상대적 평가를 위해 선택되거나 설계된 프로그램이다. 

**벤치마크 프로그램의 바람직한 특성:**
- 고급 언어로 작성되어 서로 다른 기계들에서 호환성이 가져야 한다.
- 특정 종류의 유형에 대표적이어야 한다.
- 쉽게 측정되고 널리 보급될 수 있어야 한다.

**SPEC (System Performance Evaluation Corporation):**
- 참조 모델을 이용하여 각 벤치마크 프로그램에 대한 기본 처리 시간을 정의한다.
- 예를 들어, SPEC CPU2017, SPECweb2009 등이 있다.