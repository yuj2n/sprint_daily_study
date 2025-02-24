# 📝정리 내용
- 웹 퍼블리싱 - CSS

## 💡 처음 알게 된 사실

### **CSS** - **구글 폰트**

```jsx
<body style="font-family: **'Noto Sans KR'**, sans-serif">
...
</body>
```

- 위에서 Noto Sans에 **작은 따옴표**를 넣어준 건, 중간에 띄어쓰기가 있기 때문.
띄어쓰기가 있는 글꼴은 이런 식으로 작은따옴표로 감싸줘야 함.

### **오픈그래프 - 소셜 공유 미리보기**

```jsx
 <meta property=”og:title” content=”Weekly Codeit”>
 <meta property=”og:url” content=”https://~”>
 <meta property=”og:image” content=”https://~”>
 <meta property=”og:description” content=”이번 주차에 공부한 내용”>
```

- 페북 공유 디버거 검색 후 url을 디버그하면 미리보기 정보 확인 가능!

### **구글 애널리틱스 - 방문자 수 확인**

1. **애널리틱스** 사이트 방문 후 전처리
2. 비즈니스 목표: 웹 또는 앱 **트래픽** 파악
3. netlify로 배포된 내 웹의 **url 링크** 입력
4. Google 태그 설정 탭에서 코드 내 <head> 태그에 **<script>태그 넣기**
5. **Deploys** 탭에서 사이트에 업로드 → 구글 애널리틱스 **설치**
6. 설치 테스트 통과 이후 애널리틱스 사이트에서 **보고서** 탭에 **실시간 개요** 확인 가능
- **다양한 수치** 측정 가능

❓ 홈페이지도 있고 모바일 앱도 있는 경우에 어떻게 여러가지 **속성**을 만들 수 있는지

### Codepen

![image](https://github.com/user-attachments/assets/9c1b7297-8a21-4c61-b96f-7db0e5cfed5c)


- 간단히 코드 작성 후 실행해보고 공유 가능한 서비스
- 다른 사람들이 만든 로그인 페이지 예시를 보며 코드 공부 가능!

### Whatwg

- html 표준 문서 확인 가능 → 영어 & 이해 어려움

### MDN

https://developer.mozilla.org/ko/

- whatwg에 비해 이해하기 쉽고 정확한 편

## 📌기억할 것

### **CSS - 여백**

```jsx
<div style=”width: **100%**”>
```

- “width: **100%**”를 설정하면 화면에 내용을 **꽉 차게** 할 수 있음

➕ 또한 배경 색이 있는 내용에 너비를 정할 경우, 배경 색도 같이 줄어들기 때문에 <div> 태그로 **한번 더 감싸준 후** 너비 설정

### **CSS - 여백**

```jsx
<body style="margin:0">
	<div style="margin: 0 auto">
			...
			// 가로 여백 자동 채움
	</div>
</body>
```

- <body> 태그에 기본적으로 margin 값이 들어있기 때문에 “**margin: 0**” 설정

➕ “margin: 0 auto”: 바깥 여백 중 **가로 여백**을 자동으로 채움 → 윈도우 창 크기 조절해도 내용은 고정되며 좌우 여백 값만 바뀜(참고:  auto는 margin의 가로에서만 동작)

### **도메인 설정**

- 도메인: google.com이나 [wikipedia.org](http://wikipedia.org)같은 사이트 주소, 유료로 1년 단위 등록 가능
- **[도메인 설정 방법]**
    1. **도메인 등록:** AWS같은 도메인 등록 업체의 대행 서비스로 구매 가능
    2. **Netlify에서 도메인 추가**: 도메인 등록 후 Netlify 사이트의 내 프로젝트에 들어가면 Domain management 메뉴에서 내가 등록한 도메인 입력 시 도메인 추가 가능. 
    3. **도메인 관리 사이트에서 연결 설정하기**: 도메인 등록한 사이트에서 DNS 관리 메뉴에서 A 레코드라는 규칙 추가(Host: @, Value: 75.2.60.5 → 내 도메인 들어왔을때 Netlify 서버에 물어봐주세요!)
    4. **설정 확인**: DNSChecker 사이트에서 루트 도메인의 A 레코드 확인 시 설정값이 잘 보여야 함.
    - 레코드가 모두 반영되면 Netlify에서도 확인하고 도메인이 설정됐다고 나오며 주소창에 도메인 입력 후 접속 시 사이트가 잘 나옴
