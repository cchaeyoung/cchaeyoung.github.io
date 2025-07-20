---
title: "XML 기본 구조와 문법"
excerpt: "XML의 기본 개념과 문법 규칙, 구성 요소"

categories:
  - Data Formats
tags:
  - [Data Formats]

permalink: /data-formats/xml-basics

toc: true
toc_sticky: true

date: 2025-07-16
last_modified_at: 2025-07-20T23:00
---

XML의 기본 구조와 문법에 대해서 알아보고자 한다.

---

# 🔖 XML이란?

XML이란 `eXtensible Markup Language` 의 약자로,

데이터를 **트리 구조**으로 표현하기 위해 만들어진 텍스트 기반 마크업 언어이다.

## ⭐ 주요 특징

- **사용자 정의 태그 사용 가능**  
  HTML과는 다르게 태그를 직접 정의할 수 있다.

- **데이터와 구조를 분리**  
  데이터를 구조화하여 다양한 시스템에서 손쉽게 교환하거나 저장할 수 있다.

- **플랫폼 및 언어에 독립적**  
  다양한 환경과 프로그래밍 언어에서 손쉽게 활용할 수 있다.

- **계층적 구조(트리 구조)**  
  태그가 중첩될 수 있어 복잡한 데이터 구조도 표현할 수 있다.

# 📐 XML 기본 문법 규칙

XML 작성을 위해선 아래 규칙을 따라야 한다.

1. 모든 태그는 닫혀야 한다.

   ```xml
   <!-- 올바른 예 -->
   <book>Programming</book>
   <image src="photo.jpg"/>

   <!-- 잘못된 예 -->
   <book>Programming
   <image src="photo.jpg">
   ```

2. 태그는 대소문자를 구분한다.

   ```xml
   <!-- 올바른 예 -->
   <Book>Programming</Book>

   <!-- 잘못된 예 -->
   <Book>Programming</book>
   ```

3. 태그는 적절히 중첩되어야 한다.

   ```xml
   <!-- 올바른 예 -->
   <book><title>XML Guide</title></book>

   <!-- 잘못된 예 -->
   <book><title>XML Guide</book></title>
   ```

4. 속성 값은 따옴표로 감싸야 한다.

   ```xml
   <!-- 올바른 예 -->
   <book id="123" title="XML Guide">

   <!-- 잘못된 예 -->
   <book id=123 title=XML Guide>
   ```

5. XML 선언

   XML 문서는 선택적으로 XML 선언으로 시작할 수 있다.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   ```

   - `version`: XML 버전 (주로 1.0 사용)
   - `encoding`: 문자 인코딩 (UTF-8, UTF-16 등)

# 🏗️ XML 구성 요소

1. 요소

   XML의 기본 구성 단위로, 시작 태그와 종료 태그로 둘러싸인 부분이다.

   ```xml
   <!-- 내용이 있는 요소 -->
   <title>XML Programming</title>

   <!-- 빈 요소 (두 가지 표현 방법) -->
   <image src="photo.jpg"></image>
   <image src="photo.jpg"/>
   ```

2. 속성

   시작 태그 내에서 요소에 대한 추가 정보를 제공한다.

   ```xml
   <book id="123" category="programming" published="2024">
     XML Guide
   </book>
   ```

   - 하나의 요소에서 속성명은 유일해야 한다.
   - 속성 값은 반드시 따옴표로 감싸야 한다.
   - 속성 순서는 중요하지 않는다.

3. 텍스트 노드

   요소 사이에 포함되는 실제 데이터이다.

   ```xml
   <author>김철수</author>
   <description>이 책은 XML의 기초를 다룹니다.</description>
   ```

4. 주석

   코드에 설명을 추가하기 위해 사용되며, 파서가 무시한다.

   ```xml
   <!-- 이것은 주석입니다 -->
   <book>
     <!-- 책 제목을 저장하는 요소 -->
     <title>XML Guide</title>
   </book>
   ```

5. CDATA 섹션

   특수 문자를 포함한 텍스트를 그대로 표현할 때 사용한다.

   ```xml
   <code>
     <![CDATA[
       if (x < y && y > z) {
         console.log("조건 만족");
       }
     ]]>
   </code>
   ```

---
