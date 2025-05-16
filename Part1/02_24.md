# 📝정리 내용

- 보충 학습 내용

## 💡 처음 알게 된 사실

### `main` 제외 브랜치 복사

![image](https://github.com/user-attachments/assets/08e077de-ba3c-4a63-9c37-9d65fda137e8)

- `main` 브랜치만 가져오는 옵션, `Basic-본인이름` 브랜치 필요 → ✔ 해제
- 다른 방법도 있음

## 📌 기억할 것

### 1. 내 브랜치 가져오기

```bash
git clone -b Basic-본인이름 --single-branch {저장소 URL}
```

- `Basic-본인이름` 브랜치를 로컬로 clone (`remote` origin → `local`)
- --single-branch 옵션: Basic-본인이름 브랜치 하나만 가져오기

### 2. 작업 브랜치 생성

```bash
git checkout -b Basic-본인이름-sprint1
```

- 브랜치가 `main`이 아닌 `Basic-내이름` 이어야 함!

### 3. Push

```bash
git push origin Basic-본인이름-sprint1
```

- 작업 중이던 내 브랜치로 `push`
- Basic-내이름이 아닌 Basic-내이름-sprint1

### 4. Pull Request

![image](https://github.com/user-attachments/assets/81c05a7a-c728-4e7b-b48c-91fc5a9e397f)

- 베이스 선택 시
    - 베이스 레포지토리 선택하기: `codeit-bootcamp-frontend`
    - 베이스 브랜치 선택하기: `Basic-본인이름`
- 이때 내 **브랜치**명이 **Basic-내이름-sprint1**인지 확인!!

## 두번째 과제부터..

- 원본 레포지토리의 `Basic-본인이름` 브랜치를 로컬의 `Basic-본인이름` 브랜치와 연결

```bash
git fetch upstream
git pull upstream Basic-전유진
```

### 작업 브랜치 생성

```bash
git checkout -b Basic-본인이름-sprint2
```

- 앞의 과정 **2**~**4** 반복
