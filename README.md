# sprint_daily_study
코드잇 스프린트 FE 15기 데일리 스터디 내용 정리
- 💡새롭게 알게 된 내용
- 📌메모해둘 내용
- 📑중요하게 생각하는 부분
<hr>

## 💡 커밋하며 알게 된 것
1. notion에서 사용한 사진 파일은 깃허브에 적용 X
2. 커밋된 사진 파일 수정 후 vscode에서 git **pull**해주지 않은 채 add/commit/push할 시에 **non-fast-forward** 에러 발생
-> 깃허브 레포 수정 후 vscode에서 git **pull**하는 것 **습관화**하자~
3. 이미 올라간 커밋 메세지 수정
```bash
$ git rebase -i HEAD~원하는개수

// 위에서 부터 세 번째 커밋을 수정하고 싶으면
$ git rebase -i HEAD~3

// 커밋 메시지 수정
pick 415f8ce 커밋메시지
reword ff77cfa 커밋메시지 // 수정할 커밋
reword 314bccf 커밋메시지 // 수정할 커밋
```

## 🔍 수정하며 궁금해진 점
1. 커밋메시지 제목을 구체적으로 적어주는 것이 좋을까 아니면
   Update.일자 식으로 정형화하는 게 좋을지 고민
