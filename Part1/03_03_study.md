# 📝정리 내용

- 개발 협업

## 📌 기억할 것

### Organization

![image.png](attachment:8f76359b-308b-48a8-a48e-f6d5969ef425:image.png)

- 프로젝트와 저장소 관리 도구로 보안 향상
- **Projects**
    - 할 일 **목록 관리**
    - 진행 상황 **시각화**
    - 작업 **우선순위**

![image.png](attachment:f18bfd12-a69a-4fdf-a8a1-4a3ed593022d:image.png)

- **Teams**
    - collaborator 그룹화
    - PR, Code Review, CodeOwners등에 활용

### Issues

![image.png](attachment:518d3264-9bb1-453a-b9b5-c66e5f9ffdb0:image.png)

- 버그 리포트, 기능 요청
- 프로젝트 문제 추적 및 해결
- 협업 및 의사소통 강화

### Pull Request

![image.png](attachment:8756541b-291d-4b70-b57e-37d79b45ef18:image.png)

- 장점
    - 버그 확인 O
    - 시간 제약 X → 의견 자유롭게 교환
    - 효율적이고 품질 높은 코드
- 개인 프로젝트
    - 체계적인 검토 및 문서화
    - 자동화된 documentation의 기능(단위 기록)
    - 복구 가능
- 팀 프로젝트
    - 지식 공유
    - 코드 품질 개선
    - 코드 작성 목적 공유(팀뿐만 아닌 본인 또한)

### PR Merge

1. **merge commit**을 만들며 합치기
    
    ![image.png](attachment:43961056-7b48-42ae-82d3-83beaddd2ec1:image.png)
    
    - 두 브랜치의 변경 사항 모두 유지하며 병합
    - 장점
        - 브랜치의 히스토리 유지 → 프로젝트 진행 상황 명확
        - 사용이 쉬움
    - 단점
        - 팀 규모 ⬆ → 히스토리 복잡
2. **Squash and merge** 하기
    
    ![image.png](attachment:8982f2b3-9483-4d4d-8c55-fc536fad2da4:image.png)
    
    - 모든 변경 사항을 하나의 커밋으로 압축
    - **장점**
        - 커밋 히스토리 간단
        - 주요 사항만 압축 병합
    - **단점**
        - 작업 상세 이력 손실
        - 개별 맥락&작업 정보 손실로 추후 문제 해결의 ****어려움
        - 커밋 ****아이디 병합으로 여럿이 작업 시 복잡한 문제 야기(github에는 기록 존재)
3. **Rebase and merge** 하기
    
    ![image.png](attachment:cd8953af-01d0-4a5e-8462-69b0d1b825ab:image.png)
    
    - 현 브랜치를 target 브랜치에 재위치 시킨 후 병합
    - 장점
        - 깨끗하고 선형적인 커밋 히스토리 생성
        
          → 히스토리 파악 및 코드 변화 이해
        
    - 단점
        - 관련 커밋 ID 변화로 혼란 초래(브랜치 분기 시 더 복잡)
        - 여러 개발자 동시 작업 시 복잡한 충돌 야기
        - PR별로 나눠져 있던 작업이 하나의 히스토리로 병합
        - 특정 기능이 어디부터 어디까지의 커밋으로 구현된지 알기 어려움
        
    
    → 팀 프로젝트 시 ~~merge commit~~ 이외에 **squash**나 **rebase** 방식으로 커밋 이력 정리하기
    

### Fork

- 기존 repository와 완전히 분리
- 자유롭게 변경 사항 반영
- 일반적 규모에서는 **브랜치**로 협업 → 큰 규모에는 코드 수정 권한 관리와 개별 저장소 작업이 쉬운 **fork**
- **오픈소스 기여**
    - 버그 보고
    - 문서 개선
    - 테스트 작성
    - 패키지 기여(
    - Good First Issue 레이블 활용: [https://goodfirstissue.dev](https://goodfirstissue.dev/)/(원하는 언어로 필터링하여 contribution할 수 있는 이슈 찾아보기)

### PR 충돌

- 복잡한 충돌의 경우 local 해결
- 충돌 최소화
    - 주기적인 git merge feat
    - 작은 단위의 PR
    - 파일 작게 만들기
    - 동료와 잦은 커뮤니케이션 수행

### 좋은 커밋

- 의미있는 단위의 작업
- 생성된 커밋은 동작이 가능한 형태
- 커밋 메시지는 명확하고 간결하게 작성

| type | 설명 |
| --- | --- |
| feat | 기능 개발 |
| docs | 주석/ReadMe 등 문서화  |
| test | 테스트  |
| fix | 버그나 typo 등 수정사항 |
| chore | 코드와 관련 없는 내용 수정 |
| ci | CI/CD 등 관련 작업 수행 |
| style | 스타일 수정 |