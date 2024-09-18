---
title: "[Frontend] Firebase 설정 및 백엔드 구현"
excerpt: "Firebase 주요 기능 및 Authentication, Cloud Firestore 설정 방법"

categories:
  - Frontend
tags:
  - [Firebase, Frontend]

permalink: /frontend/firebase-setup-backend/

toc: true
toc_sticky: true

date: 2024-09-18
last_modified_at: 2024-09-18
---

> **리액트 인터뷰 가이드**의 11장을 참고하여 작성하였다.

리액트, 리덕스, styled-components, 파이어베이스 백엔드를 기반으로 한 전자기기를 구매할 수 있는 전자상거래 애플리케이션 **One Stop Electronics**를 구축하고자 한다.

Firebase의 주요 기능과 설정 방법, 그리고 백엔드 구현에 대해 설명한다.

---

# 📊 Firebase의 주요 기능

Firebase는 구글에서 제공하는 종합 백엔드 서비스로, 데이터베이스, 사용자 인증, 클라우드 스토리지, 분석 등 다양한 서비스를 제공한다. 주요 기능은 다음과 같다.

- **Realtime Database:** 클라우드 기반 NoSQL 데이터베이스로, 데이터는 JSON 형식으로 저장되며 모든 클라이언트와 실시간으로 동기화된다.
- **Authentication:** 이메일, 비밀번호, 전화번호, 구글, 페이스북, 트위터/X, 깃허브, 애플 등 다양한 인증 정보를 제공하는 백엔드 서비스이다.
- **Cloud Storage:** 대용량 콘텐츠 파일(예: 이미지, 오디오, 동영상 등)을 저장하고 처리할 수 있는 비용 효율적인 스토리지 서비스이다.
- **Google Analytics와 Crashlytics:** 앱과 사용자 참여에 대한 통찰력을 얻는 데 도움이 되는 무료 앱 분석 솔루션이다.

---

# 🔧 Firebase Authentication과 Cloud Firestore 설정

Firebase Authentication과 Cloud Firestore를 설정하여 사용자 인증과 데이터 저장소를 구축한다.

## 🚀 Firebase 프로젝트 생성

1. 구글 계정으로 [Firebase](https://console.firebase.google.com/)에 로그인한다.
2. 'Firebase 프로젝트 시작하기'를 클릭하고 프로젝트 이름을 입력한다.
   ![project-name](/assets/images/posts_img/frontend/project-name.png)
3. Google Analytics 사용 여부를 묻는 옵션에서 사용자 행동, 앱 성과, 사용자 참여도 등을 분석하는 기능이 필요하다면 체크하고, 필요하지 않다면 비활성화를 선택한다. 여기서는 '비활성화'를 선택하여 진행한다.
   ![google-analytics](/assets/images/posts_img/frontend/google-analytics.png)
4. '프로젝트 만들기' 버튼을 클릭하여 프로젝트 설정을 완료한다.

## 🌐 웹 앱에 Firebase 추가

1. 프로젝트 페이지에서 웹 </> 아이콘을 클릭하여 웹 애플리케이션을 생성한다.
   ![select-web](/assets/images/posts_img/frontend/select-web.png)
2. 웹 애플리케이션 이름을 입력한 후 앱 등록을 누른다.
   ![app-name](/assets/images/posts_img/frontend/app-name.png)
3. 자동으로 생성된 Firebase 설정 파일을 복사하여 안전한 장소에 저장한다.
   ![add-firebase-sdk](/assets/images/posts_img/frontend/add-firebase-sdk.png)

## 🛠️ Firebase 제품군 설정

**Firebase Authentication 설정**

1. Firebase 제품군에서 'Authentication'을 클릭하고 '시작하기' 버튼을 누른다.
2. '로그인 방법' 탭에서 이메일/비밀번호 또는 Google 로그인 등의 인증 방법을 활성화한다. 필요한 인증 방법을 선택하고 설정을 저장한다.
   ![login-method](/assets/images/posts_img/frontend/login-method.png)

**Cloud Firestore 설정**

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

# 🔒 파이어베이스 인증과 백엔드 구현하기

## 🔑 파이어베이스 인증을 이용한 가입, 로그인, 로그아웃 구현

Firebase 인증을 활용하여 사용자 인증 기능을 구현하려면 Firebase의 `firebase/auth` 패키지에서 제공하는 여러 함수와 유틸리티를 사용해야 한다. 이 패키지는 로그인, 가입, 로그아웃을 위한 메서드를 제공한다.

**Firebase 인증 API 설정**  
Firebase 앱 인스턴스와 인증 메서드를 가져온다.

```ts
import { firebaseApp } from "@/backend/firebase/config";
import {
  signInWithEmailAndPassword,
  signInWithPopup,
  signInWithRedirect,
  GoogleAuthProvider,
  createUserWithEmailAndPassword,
  updateProfile,
  signOut,
  getAuth,
  onAuthStateChanged,
  NextOrObserver,
  User,
} from "firebase/auth";

const auth = getAuth(firebaseApp);
const googleProvider = new GoogleAuthProvider();
googleProvider.setCustomParameters({
  prompt: "select_account",
});
```

**인증 메서드 구현**  
이메일과 비밀번호를 사용한 로그인, 구글 로그인을 위한 메서드, 사용자 가입, 로그아웃 메서드를 구현한다.

```ts
export const signInEmailAndPassword = async (
  email: string,
  password: string
) => {
  if (!email || !password) return;
  return await signInWithEmailAndPassword(auth, email, password);
};

export const signInGooglePopup = () => signInWithPopup(auth, googleProvider);
export const signInGoogleRedirect = () =>
  signInWithRedirect(auth, googleProvider);

export const signUpEmailAndPassword = async (
  displayName: string,
  email: string,
  password: string
): Promise<User> => {
  const userInfo = await createUserWithEmailAndPassword(auth, email, password);
  await updateProfile(userInfo.user, { displayName });
  return userInfo.user;
};

export const signOutUser = async () => await signOut(auth);
```

**상태 변경 감지**  
사용자의 인증 상태 변경을 감지하고, 애플리케이션 내의 현재 사용자 정보를 업데이트하기 위해 다음 메서드를 사용한다.

```ts
export const onAuthStateChangedListener = (callback: NextOrObserver<User>) =>
  onAuthStateChanged(auth, callback);
```

## 📂 클라우드 스토어 데이터 작업과 컬렉션을 사용한 데이터 관련 작업

Cloud Firestore는 전통적인 SQL 데이터베이스와 달리 데이터를 도큐먼트(document) 형태로 저장하며, 도큐먼트는 컬렉션(collection)으로 구성된다.

**필요한 함수 가져오기**  
Firestore 패키지에서 필요한 함수를 가져온다.

```ts
import {
  getFirestore,
  doc,
  setDoc,
  collection,
  writeBatch,
  query,
  getDocs,
} from "firebase/firestore";
import { Product } from "@/app/store/product/product.types";

export const db = getFirestore();
```

**제품 데이터 삽입**  
제품 데이터를 Firestore에 삽입한다.

```ts
export const insertProductsData = async <T extends Product>(
  collectionKey: string,
  productItems: T[]
) => {
  const collectionRef = collection(db, collectionKey);
  const batch = writeBatch(db);

  productItems.forEach((product) => {
    const docRef = doc(collectionRef);
    batch.set(docRef, product);
  });

  await batch.commit();
};
```

1. 데이터베이스 인스턴스와 컬렉션 참조를 생성한다.
2. 배치 참조를 생성하여 여러 제품 데이터를 한 번에 삽입한다.
3. 각 제품에 대해 도큐먼트 참조를 생성하고, 배치를 업데이트한다.
4. 배치를 커밋하여 여러 레코드를 동시에 삽입한다.

**제품 데이터 조회**

```ts
export const fetchProductsData = async () => {
  const collectionRef = collection(db, "products");
  const queryRef = query(collectionRef);
  const querySnapshot = await getDocs(queryRef);

  return querySnapshot.docs.map((docSnapshot) => docSnapshot.data());
};
```

1. 제품 컬렉션 참조를 생성한다.
2. 쿼리 참조를 생성한다.
3. getDocs 메서드를 호출하여 모든 도큐먼트를 가져온다.
4. 쿼리 스냅숏을 순회하고 결과를 반환한다.

이제 Firebase 인증과 Cloud Firestore 데이터 작업을 통해 애플리케이션의 백엔드 기능을 완성했다.  
이 기능들을 활용하여 사용자 인증과 데이터 관리를 효율적으로 처리할 수 있다.

---

🔗 **구매 링크**

- <small>yes24: <a href="https://www.yes24.com/Product/Goods/130271536">https://www.yes24.com/Product/Goods/130271536</a></small>
- <small>교보문고: <a href="https://product.kyobobook.co.kr/detail/S000214006794">https://product.kyobobook.co.kr/detail/S000214006794</a></small>
