---
title: "[Frontend] Vite로 리액트 프로젝트 초기화 및 기본 설정"
excerpt: "Vite 템플릿으로 리액트 프로젝트를 초기화하고 필수 라이브러리 설치 방법"

categories:
  - Frontend
tags:
  - [Frontend]

permalink: /frontend/vite-react-setup/

toc: true
toc_sticky: true

date: 2024-09-16
last_modified_at: 2024-09-16
---

> **리액트 인터뷰 가이드**의 11장을 참고하여 작성하였다.

리액트, 리덕스, styled-components, 파이어베이스 백엔드를 기반으로 한 전자기기를 구매할 수 있는 전자상거래 애플리케이션 **One Stop Electronics**를 구축하고자 한다.

이 애플리케이션은 다양한 UI 컴포넌트를 구현하고, styled-components를 사용하여 스타일을 적용한다. Firebase Authentication을 활용하여 등록된 사용자의 신원을 확인하며, Firebase 백엔드와 통합해 데이터를 효과적으로 관리한다. 최종적으로, 애플리케이션을 배포하여 사용자들이 접근할 수 있도록 할 예정이다.

---

# ⚙️ 도구 설치

기기에 최신 버전의 [Node.js와 npm](https://nodejs.org/en)을 설치해야 한다.

---

# 🏗 프로젝트의 스캐폴딩 및 구성

## 🚀 Vite 템플릿으로 프로젝트 초기화

`degit`을 활용하여 RTK 기반의 프로젝트 구조를 생성한다. 아래 명령어를 터미널에 입력하여 기본 프로젝트 구조를 설정한다.

```bash
npx degit reduxjs/redux-templates/packages/vite-template-redux onestop-electronics
```

이 명령어는 `reduxjs/redux-templates`의 Vite 템플릿을 사용하여 `onestop-electronics`라는 이름의 새 프로젝트 디렉토리를 생성한다.

## 📦 라이브러리 설치

**리액트 라우터 및 React Intl 설치**

애플리케이션 내부에서 페이지 간 이동을 관리하기 위해 `react-router-dom`을 설치하고, 다국어 지원을 위해 `react-intl` 라이브러리를 설치한다.

```bash
npm install --save react-router-dom
npm install --save react-intl
```

- **react-router-dom:** 리액트 애플리케이션 내에서 라우팅을 쉽게 관리할 수 있게 해주는 라이브러리
- **react-intl:** 다양한 언어를 지원하는 애플리케이션을 만드는 데 도움을 주는 라이브러리로, FormatJS 기반

**styled-components 및 Firebase 설치**

컴포넌트 기반 스타일을 작성하기 위해 `styled-components`를 사용하고자 한다.

```bash
npm install --save styled-components
npm install --save-dev @types/styled-components
```

Firebase 패키지를 설치하여 사용자 인증과 데이터 저장과 같은 백엔드 기능을 구현할 수 있는 기반을 마련한다.

```bash
npm install --save firebase
```

## 📂 폴더 구조 설정

기술 스택에 맞게 폴더를 추가했다.

- **app/store:** store 폴더는 액션 생성기, 리듀서, 셀렉터 등 RTK의 다양한 컴포넌트를 생성하는 데 사용된다.
- **assets:** 이미지와 아이콘 파일을 보관한다.
- **backend:** 파이어베이스와 연관된 API와 전자상거래 애플리케이션 데이터를 보관한다.
- **features:** 웹 애플리케이션의 메인 페이지를 보관한다.
- **i18n:** 다국어 기능 관련 파일을 보관한다.

```text
one-stop-electronics/
│
├── .vscode/              # VSCode 설정 파일
├── node_modules/         # 의존성 모듈
├── src/                  # 소스 코드 디렉터리
│   ├── app/              # 애플리케이션 관련 파일
│   ├── assets/           # 이미지, 폰트 등의 정적 리소스
│   ├── backend/          # 백엔드 관련 파일
│   │   └── firebase/     # Firebase 설정 파일
│   ├── components/       # UI 컴포넌트
│   ├── features/         # 주요 기능 모듈
│   ├── i18n/             # 다국어 지원 파일
│   ├── App.css           # 전역 스타일
│   ├── App.tsx           # 메인 React 컴포넌트
│   ├── constants.tsx     # 상수 정의 파일
│   ├── custom.d.ts       # 타입 정의 파일
│   ├── global.styles.tsx # 전역 스타일 정의
│   ├── index.css         # 기본 CSS 파일
│   ├── main.tsx          # 메인 엔트리 파일
│   ├── setupTests.ts     # 테스트 설정 파일
│   └── vite-env.d.ts     # Vite 환경 설정 타입 파일
│
├── .env.local            # 환경변수 설정 파일
├── .gitignore            # Git 무시 파일
├── database.rules.json   # Firebase 데이터베이스 규칙
├── index.html            # HTML 템플릿
├── package-lock.json     # 의존성 잠금 파일
├── package.json          # 의존성 및 스크립트 정의 파일
├── README.md             # 프로젝트 설명 파일
├── tsconfig.json         # TypeScript 설정 파일
├── tsconfig.node.json    # Node.js TypeScript 설정 파일
└── vite.config.ts        # Vite 설정 파일
```

---

🔗 **구매 링크**

- <small>yes24: <a href="https://www.yes24.com/Product/Goods/130271536">https://www.yes24.com/Product/Goods/130271536</a></small>
- <small>교보문고: <a href="https://product.kyobobook.co.kr/detail/S000214006794">https://product.kyobobook.co.kr/detail/S000214006794</a></small>
