# 운동 복지 웹앱

## 파일

- `index.html`: 가족 조회 및 관리자 겸용 화면
- `manifest.webmanifest`: 모바일 홈 화면 설치용 manifest
- `firestore.rules`: Firebase Console에 붙여 넣을 Firestore 보안 규칙

## Firebase Authentication

Firebase Console > Authentication > Sign-in method에서 아래 로그인 방식을 켭니다.

- Google
- 이메일/비밀번호
- 익명

전화 로그인은 현재 사용하지 않습니다. 이메일 계정은 Firebase Console > Authentication > Users에서 가족 계정을 직접 추가해서 쓰는 방식이 가장 단정합니다. 익명 로그인은 부모님 Android 앱이 걸음 수를 자동 업로드할 때 사용합니다.

한 번 로그인하면 Firebase Auth의 로컬 로그인 유지 설정 때문에 같은 브라우저에서는 로그아웃하거나 브라우저 데이터를 지우기 전까지 계속 로그인 상태가 유지됩니다.

## 가족 접근 권한

웹 화면은 로그인만으로는 열리지 않습니다. 로그인한 사용자의 UID가 Firestore의 `allowedUsers`에 등록되어 있어야 합니다.

```text
allowedUsers/{UID}
```

조회 전용 가족 계정:

```text
role: "viewer"
```

관리자 계정:

```text
role: "admin"
```

관리자 계정으로 로그인하면 `index.html` 안에서 기록 관리 탭과 걸음 수/운동 인증 사진 저장 기능이 열립니다.

## 배포 전 체크

1. Firebase Console > Firestore Rules에 `firestore.rules` 내용을 게시합니다.
2. Firebase Console > Authentication에서 가족 계정을 만듭니다.
3. 각 계정으로 한 번 로그인해서 화면에 표시되는 UID를 확인합니다.
4. Firestore에 `allowedUsers/{UID}` 문서를 만들고 `role`을 넣습니다.
5. GitHub Pages에는 이 `app` 폴더 안 파일들을 올립니다.
