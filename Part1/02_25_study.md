# 📝정리 내용

- Git

## 💡 처음 알게 된 사실

### Merge Conflict

```bash
git merge --abort
```

- merge conflict 시, **merge** 자체를 **취소**하는 방법
- 사용하는 경우
    - **Conflict** 발생 파일이 **많아** Conflict를 **최소화**할 방식으로 파일들을 **재수정**하고 커밋 후 머지를 하고 싶거나
    - 나중에 머지하고 싶을 때

### Reset

![image.png](attachment:dd826952-da43-4d0b-8ffc-da33c4636c15:image.png)

- 과거의 커밋으로 `reset`을 한다고 그 **이후의 커밋**들이 **삭제 X**, 남아있음
- 과거의 커밋뿐만 아니라 현재 HEAD가 가리키는 커밋 **이후의 커밋**으로도 가능

### Reset & Checkout의 차이

- Reset

![image.png](attachment:1f90bdb8-c7c6-4cfe-83ac-abb6b2745b42:image.png)

- Checkout

![image.png](attachment:baf78884-e416-4411-bce8-2ba931aa44e1:image.png)

![image.png](attachment:9a3099a7-52ab-440e-a0f2-07e40ef029cf:image.png)

- HEAD가 특정 커밋을 **직접 가리키게** 하는 이유: **과거**의 **특정 커밋**에서 **새 브랜치**를 만들고 싶을 때

| git reset | git checkout |
| --- | --- |
| `HEAD`가 가리키던 브랜치가 **다른 커밋**을 가리키도록 한다  | `HEAD` 자체가 **다른 커밋**이나 **브랜치**를 가리키도록 한다 |
| `HEAD`도 결국 간접적으로 다른 커밋을 가리키게되는 효과가 생긴다 | 브랜치를 통하지 않고, 커밋을 직접적으로 가리키는 `HEAD`를 Detached HEAD라고 한다  |

### Blame

```bash
git blame [파일명]
git show [commit hash]
```

- 프로그램 문제 시 어떤 파일의 특정 코드를 누가 작성한 지 알 수 있음

### Revert

![image.png](attachment:f669a38e-8f70-41dc-8f3e-8c0760cccfab:image.png)

- 현 커밋의 **이전** 커밋과 **이후** 커밋이 동일
- remote 레포에 올라간 커밋 취소 시 사용
- `reset`을 할 시 git push X

```bash
git revert [commit hash]..[commit hash]
git push
```

- 이 때 앞의 commit은 포함되지 않음

### Reflog

```bash
git reset --hard [commit hash]
git reflog
```

- `reset` ****이후 commit hash를 몰라 되돌아가기 어려울 때 **`reflog`**
- 헤드가 가리켜왔던 커밋 정보 기록

### Stash

```bash
git stash
git stash list // 저장 내용 확인
git stash **apply** // 저장 내용 불러오기 
git stash apply stash@{0}
git stash **drop** stash@{N} // 번호 안 적어줄 시 최근 것 삭제
git stash clear // 전체 내용 삭제
git stash **pop** // 저장 내용 불러옴과 동시에 삭제
```

- 최근 커밋 이후 작업 내용 모두 스택에 옮김
- working directory 내부는 다시 최근 커밋 상태로 초기화
- 사용
    1. 작업 중 브랜치 이동이 필요한 경우
    2. 잘못된 브랜치에서 작업한 경우

### Cherry-pick

```bash
git cherry-pick [commit hash]
```

- cherry picker: 본인에게 유리한 것만 선택하는 사람
- 원하는 작업 커밋들만 가져와 현 브랜치에 추가

### 커밋 병합

```bash
git reset --soft [commit hash]
git add .
git commit -m "커밋메시지"
```

- **soft/mixed** 옵션으로 `reset` 후 add, commit하면 2개의 커밋을 1개로 **병합** 가능
- **amend** 옵션은 **마지막** 커밋에 한해서 사용 가능

## 📌 기억할 것

### Fast-Forward

![image.png](attachment:bca1c2b1-856d-4400-bae1-d1126349bc33:image.png)

```bash
git merge premium
```

### Rebase

```bash
git rebase [브랜치명]
// conflict 수정 후
git rebase --continue
```

- merge 직전의 커밋으로 `reset`
- merge와 rebase의 차이
    1. rebase는 새 커밋 생성 X
    2. rebase로 만들어진 커밋 히스토리는 merge보다 **깔끔**

→ 두 브랜치의 병합 정보가 필요한 경우: merge, 커밋 히스토리의 정돈이 중요한 경우: rebase

### 작업 단위

- main 브랜치에서 push하면 **main 내용만** remote 레포의 main 브랜치로 전송
- **sub** 브랜치의 내용 **전송 X**

### .gitignore

![image.png](attachment:80900fd7-9559-4bd7-93d0-d5f54f2c6903:image.png)

- github에서 .gitignore 옵션에서 프로그래밍 언어 설정 시 **해당 언어**에 **맞게** Git에 의해 버전 관리 **필요**가 **없는** 파일 이름이 정리된 **.gitignore** 파일 자동 생성