# 📝정리 내용

## 💡 처음 알게 된 사실

### CSS 버전

- 버전 업그레이드 시 기능 논의 기간에 따라 버전 업그레이드가 늦어질 수 있음 → 모듈(ex. 선택자) 단위로 새 기능 추가하여 최신 기능 사용 가능

### Box-sizing

```css
.content {
	width: 400px;  /* 너비 = 400px + 40px(padding + border) = 440px */
	box-sizing: **border-box**; 
}
```

- 실제 width 설정 값과 다르게 너비가 나오는 경우 box-sizing의 border-box로 설정 가능
- border-box는 width: 400px을 content + padding + border의 총합으로 만듦

### Overflow

![image.png](attachment:dcf6b49c-177a-4636-bf50-4cd2c0a3b560:image.png)

```css
.content {
	overflow: **scroll**; /* hidden, auto(넘치면 스크롤)도 있음 */
	**white-space: nowrap**; /* 띄어쓰기, 줄바꿈 안함 */
}
```

- **가로**로 **스크롤** 하고 싶은 경우 → **white-space** 사용 (이때 **shift**키를 누르면 가로스크롤 가능)

### 마진 상쇄

- 이웃하는 요소들과 부모 태그와 자식 태그 사이에도 **마진 상쇄**가 일어나 **겹칠 수 있음**
- 부모 요소에 **border**나 **padding**으로 경계가 생기는 경우 **마진 상쇄 X**

### 선택자 붙여쓰기

```css
p#book.delay.book-info { /* p태그이면서 delay, book-info class를 가진 태그 */
		background-color: #c76546;
}
```

- 여러 조건 동시에 만족하는 요소 선택 시 사용

## 📌기억할 것

### **CSS 핵심 개념 - 다양한 색상 단위**

![image.png](attachment:c4b10c95-9063-46a2-bd08-6e7e2dd4eb8f:image.png)

- 가끔 **반투명**도 사용할 일이 있음!

### 코멘트

```jsx
/* 코드에 대한 설명 적기! */ 
```

- 내가 만든 클래스가 어떤 **용도**인지 적어두자

### 텍스트 스타일링

```css
<a style="**text-decoration: none**" href="https://codeit.kr">밑줄 없는 링크</a>
```

- 밑줄 없는 링크: **text-decoration: none;**

### 배경 이미지

```css
.card {
	background-**image**: **url**('chicken.png');
	background-**repeat**: no-repeat;
	background-position: center;
	background-size: **cover**; /* 이미지 비율을 유지하며 영역 꽉 채움 */
}
```

- background-size: **contain**;은 이미지가 잘리지 않는 선에서 최대 크기 배치
- cover 값을 자주 사용

```css
.card {
	background-image: 
		**linear-gradient**(90deg, rgba(0,0,0,1) 40%, rgba(0,0,0,0)),
		**url**('chicken.png');
	background-repeart: no-repeat;
	background-position: center;
	background-size: **cover**; /* 이미지 비율을 유지하며 영역 꽉 채움 */
}
```

- 90**deg**: **가로**로 **그라데이션**
- linear-gradient + url : 이미지와 그라데이션을 합쳐 **글씨가 잘 보이도록** 함

### 그림자

![image.png](attachment:b755bfa8-7182-4e88-b2b6-069dab022ca2:image.png)

```css
.card {
	box-shadow: 10px 15px 20px 5px rgba(0, 0, 0, 0.4);
	/* 가로, 세로, 블러, 그림자 퍼짐 */
}
```

### 불투명도

![image.png](attachment:e76cbdf0-38e9-42fa-a3ab-8ba7adb2eded:image.png)

```jsx
.button {
	**opacity**: 0.5 /* 태그 전체가 반투명 */
}
```

- 배경색만 반투명 → rgba 활용!

### 여백 자동으로 채우기

```css
width: 520px; /* 반드시 너비가 정해져 있어야 자동으로 채울 수 있음 */
margin: 16px **auto**;
```

### 테두리

```css
.box {
  **border-radius**: 8px; /* border가 없는 요소에도 적용 가능! */
}
```

### 인라인

- 너비나 높이 지정 X
- 예외적으로 **<img>**는 가능
- **display: inline-block;**으로 인라인 속성에 크기 부여 가능

### Float

```css
.content {
	float: right; /* 맨 오른쪽으로 배치되며 블록 안의 인라인이 자리 비켜줌 */
}
```

### 자식, 자손

```css
.book-container > .title { /* 자식 선택자 */
	color: white;
	font-size: 16px;
}

.book-container .title { /* 자손 선택자 */
	color: white;
	font-size: 16px;
}
```

### 가상 클래스

```css
a:hover {
	text-decoration: underlined;
}

a:active {
	color: yellow;
}

a:focus {
	text-decoration: underlined;
	border: 1px solid lightblue;
}
```

### N번째 자식 선택자

```css
/* 1부터 시작 */
.gallery :nth-child(even) { ... }
.gallery :nth-child(2n+1) { ... }
.gallery :first-child { ... }
.gallery :last-child { ... }
```

### Border-box

```css
* { /* 모든 곳에 border-box 적용 */
  box-sizing: border-box;
}
```

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

- 또한 선택자가 복잡할수록 명시도 점수가 높아 우선적으로 캐스케이딩

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

- table → flex/grid를 더 많이 쓰게 됨

### 비디오

```html
<video src="codeit-logo.mp4" autoplay muted controls>
<!-- 크롬에서는 autoplay와 muted를 같이 써야 동작 -->
```
