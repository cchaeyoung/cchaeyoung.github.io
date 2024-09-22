---
title: "[Frontend] Firebase 설정"
excerpt: "Firebase 주요 기능 및 Authentication, Cloud Firestore 설정 방법"

categories:
  - Frontend
tags:
  - [Firebase, Frontend]

permalink: /frontend/react/firebase-setup/

toc: true
toc_sticky: true

date: 2024-09-17
last_modified_at: 2024-09-17
---

Firebase의 주요 기능과 설정 방법에 대한 내용

---

# 🔥 Firebase의 주요 기능

Firebase는 구글에서 제공하는 종합 백엔드 서비스로, 데이터베이스, 사용자 인증, 클라우드 스토리지, 분석 등 다양한 서비스를 제공한다. 주요 기능은 다음과 같다.

- **Realtime Database:** 클라우드 기반 NoSQL 데이터베이스로, 데이터는 JSON 형식으로 저장되며 모든 클라이언트와 실시간으로 동기화된다.
- **Authentication:** 이메일, 비밀번호, 전화번호, 구글, 페이스북, 트위터/X, 깃허브, 애플 등 다양한 인증 정보를 제공하는 백엔드 서비스이다.
- **Cloud Storage:** 대용량 콘텐츠 파일(예: 이미지, 오디오, 동영상 등)을 저장하고 처리할 수 있는 비용 효율적인 스토리지 서비스이다.
- **Google Analytics와 Crashlytics:** 앱과 사용자 참여에 대한 통찰력을 얻는 데 도움이 되는 무료 앱 분석 솔루션이다.

---

# 🔧 Firebase: 인증 및 Cloud Firestore 설정

Firebase Authentication과 Cloud Firestore를 설정하여 사용자 인증과 데이터 저장소를 구축한다.

## 🚀 Firebase 프로젝트 생성

1. 구글 계정으로 [Firebase](https://console.firebase.google.com/)에 로그인한다.
2. 'Firebase 프로젝트 시작하기'를 클릭하고 프로젝트 이름을 입력한다.
   ![project-name](/assets/images/posts_img/frontend/project-name.png)
3. Google Analytics 사용 여부를 묻는 옵션에서 사용자 행동, 앱 성과, 사용자 참여도 등을 분석하는 기능이 필요하다면 체크하고, 필요하지 않다면 비활성화를 선택한다. 여기서는 '비활성화'를 선택하여 진행한다.
   ![google-analytics](/assets/images/posts_img/frontend/google-analytics.png)
4. '프로젝트 만들기' 버튼을 클릭하여 프로젝트 설정을 완료한다.
   ![complete](/assets/images/posts_img/frontend/complete.png)

## 🌐 웹 앱에 Firebase 추가

1. 프로젝트 페이지에서 웹 </> 아이콘을 클릭하여 웹 애플리케이션을 생성한다.
   ![select-web](/assets/images/posts_img/frontend/select-web.png)
2. 웹 애플리케이션 이름을 입력한 후 '앱 등록'을 누른다.
   ![app-name](/assets/images/posts_img/frontend/app-name.png)
3. 자동으로 생성된 Firebase 설정 파일을 복사하여 안전한 장소에 저장한다.
   ![add-firebase-sdk](/assets/images/posts_img/frontend/add-firebase-sdk.png)

## 🔑 Firebase Authentication 설정

1. Firebase 제품군에서 'Authentication'을 클릭하고 '시작하기' 버튼을 누른다.
2. '로그인 방법' 탭에서 이메일/비밀번호 또는 Google 로그인 등의 인증 방법을 활성화한다. 필요한 인증 방법을 선택하고 설정을 저장한다.
   ![login-method](/assets/images/posts_img/frontend/login-method.png)

## 💾 Cloud Firestore 설정

1. Firebase 제품군에서 'Cloud Firestore'를 클릭하고 '데이터베이스 만들기' 버튼을 누른다.
2. 데이터베이스 만들기 창에서 위치를 선택한다. 일반적으로 가장 가까운 위치를 선택하여 데이터 접근 속도를 최적화한다.
   ![create-database](/assets/images/posts_img/frontend/create-database.png)
3. '프로덕션 모드에서 시작'을 선택하고 '만들기'를 클릭하여 데이터베이스를 생성한다.
   ![create-database-mode](/assets/images/posts_img/frontend/create-database-mode.png)
4. '규칙' 탭에서 Firebase의 기본 보안 규칙을 설정한다. 기본적으로 모든 사용자가 데이터베이스의 모든 문서에 대해 읽기 및 쓰기 권한을 갖도록 설정한다.

   ```ts
   rules_version = '2';

   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if true;
       }
     }
   }
   ```

   ![rules-true](/assets/images/posts_img/frontend/rules-true.png)  
   실제 배포 시에는 사용자 인증이나 역할에 따라 접근 권한을 설정하여 보안을 강화해야 한다.

---

# 🔐 Firebase 설정 파일 위치

깃허브 같은 공개 개발 플랫폼에서 Firebase 설정 값을 저장하는 것은 보안상 좋지 않다. 대신, `.env.local` 같은 파일에 설정 값을 저장하고, 이 파일을 프로젝트의 `.gitignore`에 추가하여 보안을 유지하는 것이 좋다.

`.env.local` 파일 예시:

```
VITE_FIREBASE_API_KEY = "yourfirebaseapikey"
VITE_FIREBASE_AUTH_DOMAIN = "yourfirebaseauthdomain"
VITE_FIREBASE_API_KEY = "yourfirebaseprojectid"
VITE_FIREBASE_STORAGE_BUCKET = "yourfirebasestoragebucket"
VITE_FIREBASE_MESSAGING_SENDER_ID = "yourfirebasemessagingsenderid"
VITE_FIREBASE_APP_ID = "yourfirebaseappid"
```

Vite 기반 프로젝트에서는 위 코드처럼 키 값이 `VITE_`로 시작해야 한다.  
이 키들은 `import.meta.env.VITE_`를 통해 접근할 수 있다.

다음과 같은 `config.ts` 파일이 파이어베이스 애플리케이션에 있다면 설정을 초기화하는데 유용하다.

```ts
import { initializeApp } from "firebase/app";

const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
  authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
  projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: import.meta.env.VITE_FIREBASE_SENDER_ID,
  appId: import.meta.env.VITE_FIREBASE_APP_ID,
};

export const firebaseApp = initializeApp(firebaseConfig);
```

이와 같은 방법으로 설정을 관리하면 보안성을 유지하면서 Firebase와 애플리케이션을 원활하게 연동할 수 있다.

---
