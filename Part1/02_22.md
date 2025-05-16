# 📝정리 내용
- Git

## 💡 처음 알게 된 사실

### Revert

- reset에 대해 찾아보다 알게 됨.
- **reset**은 **위험부담**으로 잘 가용하지 않는 반면, **revert**는 협업 시 팀원들에게 영향없이 커밋 되돌리기 가능
- **reset**과 **차이**점: 돌아가고자 하는 과거 커밋과 현재 커밋 사이의 다른 커밋들을 제거하지 않고 특정 커밋만을 되돌릴 수 있는 명령어
- 명령어 사용 즉시 커밋 반영 → 메시지를 남기려면 즉시 커밋되지 않게 하는 옵션 사용

```bash
git revert **--no-commit** [commit hash] 
git commit -m "revert한 이유"
```

### 최신 커밋 수정

```bash
git commit --amend
```

### Aliasing

```bash
git config alias.history 'log --pretty=oneline
-> git history = git log --pretty=oneline
```

### Show & Diff

```bash
git show [commit hash]  // 특정 커밋 변경 사항 
git diff [commit hash] [commit hash]  // 두 커밋의 차이
```

### HEAD 기준 Reset

```bash
git reset --hard **7f3d** 
= git reset --hard **HEAD^**
```

- 2단계 이전 커밋을 가리키고 싶을 때

```bash
git reset --hard **HEAD~2**
```

### Tag

- 프로젝트 주요 버전의 시작점에 태그 달기
- **중요한 커밋**들은 태그 달아주면 프로젝트 이력 **파악** 시 도움

```bash
git tag [태그 이름] [커밋 아이디]
git show [태그 이름]
```

## 📌 기억할 것

### Git과 Github 차이

<img src="https://github.com/user-attachments/assets/f55c798e-1901-4d84-903e-fcef419b3153" width="70%" height="70%">

- Git: 버전 관리(지난 과정 확인 및 백업) / 협업 가능 툴
- Github: git으로 관리하는 프로젝트 올려둘 수 있는 사이트(원격 저장소)

### 레포지토리

- 커밋이 저장되는 곳
- **.git** 디렉토리(버전별 변경 사항 정보)
- 프로젝트 디렉토리 자체 X
- 커밋: 프로젝트 디렉토리의 특정 모습을 하나의 버전으로 남긴 것

### Staging area

- **존재 이유**: 모든 변경 사항을 **commit**에 반영하고 싶지 않을 수 있음
- 따라서 add를 통해 **staging area**를 거쳐야만 **commit**이 가능
- **index**라고도 불림

### 파일의 상태

<img src="https://github.com/user-attachments/assets/f5c80ed5-553b-4974-aaf7-eed9e49d8818" width="70%" height="70%">

- **Untracked** : 생성 후 한 번도 add하지 않은 상태
- **Tracked**
    - *Staged  : add된 경우*
    - *Unmodified : commit된 이후 수정 X*
    - *Modified*

### Reset

- **add** 취소: git **reset** 파일명
- 특정 커밋으로 이동, 그 이후 커밋 **삭제**&**보존** 옵션 제공
- 협업 시, reset 후 **push X**. 저장소에 push 하면 **error**가 나지만,

  **--force** 옵션으로 강제로 덮게 된다면 reset 된 **commit**으로 덮어지기 때문이다

<img src="https://github.com/user-attachments/assets/d6958f24-eb91-41a0-bed0-d044e90757e0" width="70%" height="70%">

| --soft | 커밋만 취소하고 파일 변경 내용은 보존 (stage 상태 유지) |
| --- | --- |
| --mixed | 커밋을 취소하고 stage는 비우지만, 파일 변경 사항은 보존 |
| --hard | 커밋을 취소하고, stage 및 파일 변경 사항까지 모두 삭제 |

**※** git reset --hard 실행 후 다시 이전으로 돌리고 싶은 경우 **git pull**

### Position 속성

- top, right, bottom, left
- +값은 안으로 -값은 밖으로
