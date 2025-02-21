# 📝정리 내용

- **위클리 페이퍼** 내용 정리

https://github.com/yuj2n/sprint_weekly_paper/blob/main/Topic/week1.md

## 💡 처음 알게 된 사실

### iframe

- 사용처: 지도, 결제창, 강의

### Request Bin

![image.png](attachment:ccc02f60-82b6-497d-b385-55cdcd52ad9e:image.png)

- 간단한 서버로 **리퀘스트** 확인 가능

### Autocomplete

- 이전에 입력한 값 보여줌
- required와 달리 **on**이라는 값 지정해줘야 동작

### Link

- **font**, **css**파일, **icon**에 쓰임
- **a**태그: 사이트 주소

### 동적인 OG 태그

```html
<head>
    <meta property="og:title" content={data?.title}>
</head>
```

- 이런 경우엔 `data?.title` 에 해당하는 데이터를 먼저 받고 나서 HTML을 생성해야 함.
- 이를 위해서 프론트엔드 서버에서 데이터를 받아서 HTML을 생성한 뒤 전달!
- 또는 소스 코드를 빌드하는 단계에서 미리 데이터를 받아 HTML을 생성하는 방법 존재

## 📌기억할 것

### 가로 마진 일정하게

![image.png](attachment:06160c76-0fa8-4362-9deb-ed45f9efdb47:image.png)

```html
<span class="chip">섬</span>
<span class="chip">해변</span>
<span class="chip">오두막</span>
```

```css
.chip {
  background-color: #dedede;
  text-align: center;
  display: inline-block;
  width: 100px;
  padding: 16px;
  margin-right: 24px;
  border-radius: 9999px;
}

.chip:first-child {
  margin-left: 24px;
}
```

### 캐스케이드

```css
.description {
	color: black;
}

.description.book-info {
	color: green;
}

.description {
	color: white; /* 마지막에 적용된 white로 적용 */
}
```

- 또한 선택자가 **복잡할수록** 명시도 점수가 높아 **우선적으로** 캐스케이딩

### 상속의 우선순위

```css
#header > .description {
  color: #bb0000;
}

.accent { /* 가장 가까운 부모 속성으로 채택됨 */
  color: #00cc00;
}
```

### HTML - 링크의 상대주소

```html
<a href="./movie"> <!-- **./** : 현재 폴더 -->
<a href="../index.html"> <!-- **../** : 상위 폴더 -->
<a href="/index.html"> <!-- **/** : 최상위 폴더 -->
```

- …/ : 폴더 이름 처럼 취급

### 목차

```html
<a href="#인터넷의_역사">인터넷의 역사</a><br>
<h2 id="인터넷의_역사">인터넷의 역사</h2> <!-- id와 #뒤의 값 일치해야함. -->
```

### 리스트 스타일링

![image.png](attachment:c8cc6622-1c89-411e-9d37-b62d5b9d9f21:image.png)

```html
<style>
	ul {
		**list-style**: **none**;
	}
	
	ul > li {
		**display**: **inline-block**;
		border: 1px solid #dddddd;
		border-radius: 24px;
		padding: 8px;
	}
</style>
```

- list-style: **none**; / display: **inline-block**;

### 테이블 스타일링

```css
table {
	border-collapse: collapse; 
	/* border-spacing: 2px; -> 간격 늘림 */
}
```

- table → flex / grid를 더 많이 쓰게 됨

### 비디오

```html
<video src="codeit-logo.mp4" autoplay muted controls>
<!-- 크롬에서는 autoplay와 muted를 같이 써야 동작 -->
```

### 오디오

```html
<audio src="codeit-logo.mp3" controls autoplay>
```

- audio도 **controls**가 있어야 화면에 **표시**
- **autoplay** 속성: 크롬 X / **사파리 O**

### Label

![image.png](attachment:a47f2de6-a51e-4a0f-8b00-a96b8af6c801:image.png)

```html
<label **for**="signup-email">이메일</label>
<input **id**="signup-email" name="email" type="email">
```

- input 옆에 붙은 이름

### 주소

> http://127.0.0.1:3000/?email=html%40codeit.kr&password=ilovehtml&password_repeat=ilovehtml
> 
- http://127.0.0.1:3000/(현재 주소) + ? + **Query string**

### Action

```html
<form action="https://google.com/search">
      <input name="q">
      <button>검색</button>
    </form>
```

- action 속성으로 다른 주소 불러오기 가능

### Input

- checkbox: 여러 항목 중 여러 개 선택
- radio: 여러 항목 중 하나 선택
- Select: 정해진 값 중 하나 선택(option과 함께)

→ 공통적으로 **name**값은 **고정**, **value**값 **다르게**

**다른 예시**

```html
<input name="avatar" type="file" accept=".png,.jpg">
```

```css
input::placeholder { color : white; }
```

### Script

```html
<body>
  ..
  <script src="like.js"></script> <!-- body태그 맨 마지막에-->
</body>
```

### 메타 태그

- **OG 태그 사용**
• [카카오톡 디버거](https://developers.kakao.com/tool/debugger/sharing)
• [페이스북 디버거](https://developers.facebook.com/tools/debug/)
• [트위터](https://cards-dev.twitter.com/validator)