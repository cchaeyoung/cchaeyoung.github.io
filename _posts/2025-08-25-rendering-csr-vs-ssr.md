---
title: "[Rendering] CSR vs SSR: 클라이언트 사이드 렌더링과 서버 사이드 렌더링 비교"
excerpt: "CSR과 SSR의 차이점, 장단점"

categories:
  - Rendering
tags:
  - [Rendering]

permalink: /rendering/csr-vs-ssr

toc: true
toc_sticky: true

date: 2025-08-25
last_modified_at: 2025-08-25
---

웹 애플리케이션을 개발할 때 렌더링 방식을 선택하는 것은 중요한 결정 중 하나다.

**SSR(Server-Side Rendering)** 과 **CSR(Client-Side Rendering)** 은 웹 페이지를 렌더링하는 두 가지 방식이다.

<mark>CSR(Client-Side Rendering)</mark>과 <mark>SSR(Server-Side Rendering)</mark> 각각의 특징을 이해하고, 프로젝트에 맞는 방식을 선택해보자.

---

# 📱 CSR

**CSR (Client-Side Rendering)** 은 브라우저에서 JavaScript로 HTML을 만드는 방식이다.

```javascript
// API로 데이터만 받아오고
fetch("/api/posts")
  .then((response) => response.json())
  .then((posts) => {
    // JavaScript로 HTML을 만든다
    posts.forEach((post) => {
      // DOM 조작으로 화면에 추가...
    });
  });
```

서버는 데이터(JSON)만 보내주는 방식이고, 브라우저가 JavaScript로 HTML을 직접 만든다.

## ⚙️ CSR 동작 과정

1. 사용자가 웹사이트 접속
2. 서버에서 빈 HTML + JavaScript 번들 전송
3. 브라우저에서 JavaScript 다운로드 및 파싱
4. JavaScript 실행으로 DOM 생성
5. 화면에 컨텐츠 표시

## 💡 CSR의 장단점

**장점**

- **빠른 페이지 전환**: 페이지 이동 시 필요한 데이터만 가져와 화면을 업데이트하므로 전환이 매끄럽다.
- **풍부한 사용자 경험**: SPA(Single Page Application) 구현이 가능해 동적인 UI와 부드러운 인터랙션 제공한다.
- **서버 부하 감소**: 렌더링 작업을 클라이언트에서 처리해 서버 부담이 줄어든다.
- **캐싱 효과**: 한 번 로드된 JavaScript는 브라우저에 캐싱되어 반복 사용 시 속도가 빨라진다.

**단점**

- **초기 로딩 시간**: JavaScript를 다운로드하고 실행하는 데 시간이 필요하다.
- **SEO 어려움**: 검색 엔진이 빈 HTML만 보게 될 수 있어 SEO 최적화에 불리하다.
- **JavaScript 의존성**: JavaScript가 비활성화된 환경에서는 사이트 이용이 어렵다.

---

# 🖥️ SSR

**SSR(Server-Side Rendering)** 은 서버에서 완성된 HTML을 만들어서 브라우저에 보내주는 방식이다.

```javascript
app.get("/", (req, res) => {
  const users = getUsers(); // 데이터 가져오기

  // 서버에서 HTML 완성해서 전송
  res.render("index", { users });
});
```

이처럼 **SSR**은 서버가 완성된 HTML을 만들어서 보내주는 방식이다.

## ⚙️ SSR 동작 과정

1. 사용자가 웹사이트 접속
2. 서버에서 데이터 조회
3. 서버에서 완전한 HTML 생성
4. 클라이언트로 렌더링된 HTML 전송
5. 브라우저에서 즉시 컨텐츠 표시

브라우저는 받은 HTML을 그대로 보여주기만 하면 된다.

## 💡 SSR의 장단점

**장점**

- **빠른 초기 페이지 로드**: 서버에서 미리 렌더링한 HTML을 보내주기 때문에 페이지 요청 시 바로 내용을 볼 수 있다.
- **SEO 친화적**: 검색 엔진이 페이지 내용을 쉽게 읽을 수 있어 검색 순위에 유리하다.
- **JavaScript 독립성**: 브라우저가 JavaScript를 완전히 실행하지 않아도 기본 내용을 표시할 수 있다.

**단점**

- **서버 부담 증가**: 요청이 들어올 때마다 서버가 HTML을 렌더링해야 해서 서버 자원이 더 필요하다.
- **페이지 이동 시 전체 새로고침**: 매번 서버에서 새로운 HTML 요청이 발생하므로 속도가 느릴 수 있다.

---

# 🤔 언제 어떤 방식을 선택할까?

## ⚡ CSR을 선택하는 경우

- **대시보드, 관리자 페이지** 등 로그인 후 사용하는 내부 툴
- **실시간 데이터**가 중요한 애플리케이션
- **복잡한 상호작용**이 많은 웹앱
- SEO가 중요하지 않은 경우

## 🚀 SSR을 선택하는 경우

- **블로그, 뉴스 사이트** 등 콘텐츠 중심 웹사이트
- **SEO가 중요한** 마케팅 사이트
- **초기 로딩 속도**가 중요한 경우
- 검색 엔진 노출이 필요한 경우

---

# 🔄 하이브리드 접근: SSG와 ISR

최근에는 **SSG(Static Site Generation)** 나 **ISR(Incremental Static Regeneration)** 같은 하이브리드 방식도 인기를 얻고 있다.

- **SSG**: 빌드 시점에 미리 정적 HTML 생성
- **ISR**: 정적 생성 + 필요시 서버에서 재생성

이런 방식들은 **SSR의 SEO 장점**과 **CSR의 성능 장점**을 모두 가져갈 수 있어서, `Next.js` 같은 프레임워크에서 널리 사용되고 있다.

---

CSR과 SSR은 각각의 장단점이 명확하기 때문에 **프로젝트의 요구사항**에 따라 적절한 방식을 선택하는 것이 중요하다.

- **SEO가 중요**하다면 → SSR
- **복잡한 사용자 인터랙션**이 중요하다면 → CSR
- **두 장점을 모두** 원한다면 → Next.js 같은 하이브리드 프레임워크
