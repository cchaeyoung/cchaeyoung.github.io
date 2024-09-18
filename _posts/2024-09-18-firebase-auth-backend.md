---
title: "[Frontend] 리액트 - Firebase 인증 및 백엔드 데이터 관리"
excerpt: "Firebase Authentication을 이용한 사용자 인증 및 Cloud Firestore를 사용한 데이터 관리 방법"

categories:
  - Frontend
tags:
  - [Firebase, Frontend]

permalink: /frontend/firebase-auth-backend/

toc: true
toc_sticky: true

date: 2024-09-18
last_modified_at: 2024-09-18
---

> **리액트 인터뷰 가이드**의 11장을 참고하여 작성하였다.

리액트, 리덕스, styled-components, 파이어베이스 백엔드를 기반으로 한 전자기기를 구매할 수 있는 전자상거래 애플리케이션 **One Stop Electronics**를 구축하고자 한다.

이 애플리케이션은 리액트를 사용하여 프론트엔드를 구현하며, Firebase를 활용하여 백엔드 인증 및 데이터 관리를 처리한다.

리액트의 강력한 컴포넌트 기반 아키텍처와 Firebase의 인증 기능을 통해 프로그래밍의 복잡성을 줄이고, 효율적인 사용자 인증 및 데이터 관리를 실현할 수 있다.

---

# 🔑 Firebase 인증: 가입, 로그인, 로그아웃 구현

Firebase Authentication을 활용하여 사용자의 로그인, 가입, 로그아웃 기능을 구현한다. `firebase/auth` 패키지를 사용하여 이메일 및 비밀번호 로그인, 구글 로그인 등을 처리할 수 있다.

## Firebase 인증 API 설정

먼저 Firebase 앱 인스턴스를 생성하고, 인증 메서드를 가져온다.

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

## 인증 메서드 구현

이메일과 비밀번호를 사용한 로그인, 구글 로그인을 위한 메서드, 사용자 가입, 로그아웃 메서드를 구현한다.

**로그인**
이메일과 비밀번호를 사용하여 사용자를 로그인시키는 메서드이다.

```ts
export const signInEmailAndPassword = async (
  email: string,
  password: string
) => {
  if (!email || !password) return;
  return await signInWithEmailAndPassword(auth, email, password);
};
```

![login-main](/assets/images/posts_img/frontend/login-main.png)

**구글 로그인**  
구글 로그인을 위한 메서드이다.

```ts
export const signInGooglePopup = () => signInWithPopup(auth, googleProvider);
export const signInGoogleRedirect = () =>
  signInWithRedirect(auth, googleProvider);
```

![google-login](/assets/images/posts_img/frontend/google-login.png)

**사용자 가입**  
이메일과 비밀번호를 사용한 사용자 가입 메서드이다.

```ts
export const signUpEmailAndPassword = async (
  displayName: string,
  email: string,
  password: string
): Promise<User> => {
  const userInfo = await createUserWithEmailAndPassword(auth, email, password);
  await updateProfile(userInfo.user, { displayName });
  return userInfo.user;
};
```

![sign-up](/assets/images/posts_img/frontend/sign-up.png)

**로그아웃**
로그아웃 메서드이다.

```ts
export const signOutUser = async () => await signOut(auth);
```

![logout](/assets/images/posts_img/frontend/logout.gif)

## 상태 변경 감지

사용자의 인증 상태 변경을 감지하고, 애플리케이션 내의 현재 사용자 정보를 업데이트하기 위해 다음 메서드를 사용한다.

```ts
export const onAuthStateChangedListener = (callback: NextOrObserver<User>) =>
  onAuthStateChanged(auth, callback);
```

# 📂 Cloud Firestore를 통한 데이터 관리

Cloud Firestore는 전통적인 SQL 데이터베이스와 달리 데이터를 도큐먼트(document) 형태로 저장하며, 도큐먼트는 컬렉션(collection)으로 구성된다.

## Firestore 설정

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

## 제품 데이터 삽입

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

## 제품 데이터 조회

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

Firebase 인증과 Cloud Firestore 작업을 통해 사용자 인증과 데이터 관리 기능을 구축하였다.
이를 활용하여 애플리케이션의 백엔드 작업을 효율적으로 처리할 수 있다.

---

🔗 **구매 링크**

- <small>yes24: <a href="https://www.yes24.com/Product/Goods/130271536">https://www.yes24.com/Product/Goods/130271536</a></small>
- <small>교보문고: <a href="https://product.kyobobook.co.kr/detail/S000214006794">https://product.kyobobook.co.kr/detail/S000214006794</a></small>
