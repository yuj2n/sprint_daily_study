# 📝정리 내용

- CSS 레이아웃

## 💡 처음 알게 된 사실

### Sticky

```css
.green {
	background-color: green;
	width: 100%;
	heigth: 5rem;
	position: sticky;
	top: 0; /* 브라우저 화면 기준으로 맨위에 닿을 때 고정 */
}
```

- fixed: 원래 배치 흐름에서 빠져나옴
- sticky: 원래 위치에서 공간 차지
- 특성: 부모 요소 안에 갇혀있음

### 쌓임 맥락

```css
header {
  position: sticky;
  top: 0;
  z-index: 1;
}

main {
  position: relative;
  z-index: 0;
}
```

- header태그에 nav바를 만들어놓으면 무슨 일이 있어도 main태그 내용보다 앞쪽에 보임

### Display

```css
div {
	display: flex;
	flex-direction: row-reverse; or justify-content: flex-end;
}
```

- `flex-direction: row-reverse;` = `justify-content: flex-end;`

### 간격

```css
.container {
	display: flex;
	flex-wrap: wrap;
	gap: 60px 30px; /* 이 때, 세로 60px, 가로 30px은 세로 정렬을 해도 변동 X */
}
```

- 정렬 축을 바꿔도 세로/가로 순서가 변하지 않는 이유: grid와 같이 쓰기 때문

### 요소 채우기

```css
div {
	display: flex;
	flex-grow: 1; or flex-shrink: 0; 
}
```

- `flex-grow: **1;**` → 빈 공간을 채우고 싶을 때(기본 값: 0)
- `flex-shrink: **0**;` → 요소의 크기를 원하는 대로 고정(기본 값: 1)

### Flex-basis

- 대부분의 경우 width/height를 잘 정해주면 문제없이 동작
- 기본값: `flex-basis: auto;`
- flexbox에서 크기를 정하고 싶을 때

```css
div {
	flex: 1 0 100px; /* flex-grow, flex-shrink, flex-basis 순 */
}
```

- **장점**: `width: 100px`과 같지만 flex-basis로 값 설정 시 **flex**로 **짧게** 작성 가능

### Inline-flex

![image.png](attachment:dbebf582-2bb8-4fe1-b453-051a679444a7:image.png)

```css
.new-window-link {
  display: inline-flex;
  align-items: center;
  gap: 4px;
}
```

- `display: flex`라고 하면 그 안에서는 플렉스박스의 규칙에 따라 배치되고, 그 바깥에서 플렉스박스 전체에 대해서는 마치 `display: block`처럼 위에서 아래로 배치 → `display: inline-flex;`

### Grid

![image.png](attachment:6a8239d2-7b46-43cc-9ed2-dfbf64d238b9:image.png)

```css
div {
	display: grid;
	grid-template: 200px 200px 100px / 300px 100px 300px /* 세로 가로(row, column) 순 */
}
```

```css
div {
	display: grid;
	grid-template: repeat(6, 1fr) / minmax(200px, 1fr) minmax(200px, 1fr) 1fr;
}
```

- `minmax()` 에도 **fr**을 쓸 수 있지만 **max**에만 가능!
- 여러 구간을 나눌 때 `repeat(6, 1fr)`와 같이 씀

### Grid 요소 배치

```css
div2 {
	grid-row: 3 / span 2;
	grid-column: 2 / -2;
}
```

- 숫자는 셀 번호 X, **grid 라인** 번호!
- 첫 번째 값은 기준을 잡아줘야 하므로 span 사용 X

### 이름으로 배치

![image.png](attachment:c071cafc-22e4-44a8-ba57-4a9079bb6268:image.png)

```css
div {
	display: grid;
	grid-templates-areas:
		"r g ."
		"r b b"
}
div { grid-area: r; }
```

- r이 세로로 연속으로 이어진 경우 2칸의 너비를 가짐
- 숫자로 이름 지어주면 작동 X → r1

## 📌 기억할 것

### Absolute

```css
div1 { /* 조상 위치는 그대로, 자손 위치 자유롭게 배치 가능 */
	position: relative; 
}

div2 { 
	position: absolute; 
	inset: 1rem;
}
```

- 가장 가까운 **포지셔닝**이 된 **조상 요소**를 **기준**으로 위치 잡음
- ex) 부모: none; 조상: relative → 조상 기준으로 자리 잡음
- **relative**와 차이: 원 배치에서 **자리** 차지 **X**
- 크기 미정 시, 내용만큼의 크기를 가지며 width가 없어도 left, right 둘 다 줄 경우 크기 생김
- `inset: 0;` (top, right, bottom, left: 0;)

### Fixed

```css
.green {
	background-color: green;
	width: 100%;
	height: 5rem;
	position: fixed;
	top:0;
	left: 0;
}

.content {
	margin-top: 5rem;
}
```

- navigation 바

### Z-index

```css
.div {
	...
	position: sticky;
	z-index: 1; /* 요소가 겹칠 때 더 위에 위치 */
}

.div2 {
	position: sticky;
}
```

- 맨 앞에 배치하는 기능으로 - 값도 사용 가능

### 📑Position

| **Position** |                         배치 |  원래 자리 차지 |    flexbox 영향  |
| --- | --- | --- | --- |
| relative | 요소 원래 위치 기준 배치/원래 자리 차지 |            O |            O |
| absolute | 가까운 포지셔닝 된 조상 요소 기준 배치(static 제외) |            X |            X |
| fixed | 브라우저 화면 기준 고정 배치(nav바 만들 시 margin 필요) |            X |            X |
| sticky | 원 위치에 배치되어 있다가 정해진 위치에 브라우저 스크롤 될 시 고정 배치  |            O |            O |

### 정렬

- **기본** 축 정렬: justify-content
- **교차** 축 정렬: align-items

### Flexbox안에 배치

- `relative`, `sticky`는 요소의 원래 자리를 차지하기 때문에 flexbox의 영향받음
- `absolute`랑 `fixed`는 요소의 원래 자리에서 쏙 빠져버리기 때문에 글의 흐름에서 빠지는 거랑 마찬가지로, flexbox랑 상관없이 배치

❓세로로 늘어나거나 줄어들게 하는 방법

![image.png](attachment:caf97174-45f4-489a-9dda-3c9e298079ee:image.png)

[20250228_230847.mp4](attachment:91de3a5d-718f-40c6-9867-2b557dce6b89:20250228_230847.mp4)

### 요소 간 여백

- `display: flex;`가 적용된 경우에는 margin보다 **gap** 주기!!