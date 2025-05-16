# 📝정리 내용

- 인터렉티브 자바스크립트 - 이벤트

## 💡 처음 알게 된 사실

### 이벤트 핸들러

- 등록 방법
    1. btn.onclick = function() {} 
    2. `<button onclick=”func()” />` 
    
    → 1,2는 여러 번 등록 시 덮어씀
    
    3. btn.addEventListener(’click’, event); ← 여러 번 등록 시 모두 **작동**
- 주의할 점
    - `btn.removeEventListener(’click’, func() { });`로 이벤트 삭제 시 event에 함수를 직접 넣으면 작동 X → 외부에 함수 작성 후 **전달**
    - `btn.addEventListener(’click’, event1());` 와 같이 소괄호를 붙여주게 되면 함수를 호출하게 되어 undefined가 전달되어 등록 X

### 이벤트 버블링

- = 이벤트 전파
- 한 요소의 이벤트 발생 시 부모 요소로 전파되어 동일 동작 이벤트가 차례로 동작
- `event.stopPropagation();`으로 방지 가능

### 이벤트 위임(Delegation)

- 버블링 개념을 활용
- 이벤트 핸들러의 불필요한 사용 → 성능 저하

→ 부모 요소에서 한 번에 관리

```jsx
const toDoList = document.querySelector('#to-do-list');

function updateToDo(event) {
  if (event.target.classList.contains('item')) { // li 태그 클릭 시 클릭이벤트 발생 방지
      event.target.classList.toggle('done');
  }
}

toDoList.addEventListener('click', updateToDo);
```

### 브라우저의 기본 동작

- `event.preventDefault();`

### 마우스 버튼 이벤트

 <img src="https://github.com/user-attachments/assets/ba82456a-1e67-4496-bc27-c3688cd4e81a" width="50%" height="50%">

1. clientXY: 클라이언트 영역 내 마우스 좌표(화면의 좌측 상단의 모서리 위치를 (0, 0))
2. offsetXY: 이벤트 발생한 target 기준(대상의 좌측 상단의 모서리 위치를 (0, 0))
3. pageXY: 전체 문서 기준

### 마우스 이벤트 타입

- `mouseover/mouseout`과 `mouseenter/mouseleave`의 차이
    1. `mouseenter` 는 버블링 발생 X(자식 요소 접근도 이벤트 발생)
    2. `mouseenter` 는 자식 요소의 영역 계산 X (영역을 구분하기 때문에 자식에서 부모로 가면 동작)

### input 태그 다루기

- input(입력) ≠ change(값 변경)
- change 인식: focus 빠져나갈 때 & 값 입력 중 Enter 키 입력

## 📌 기억할 것

### 마우스 이벤트

| **이벤트 타입** | **설명** |
| --- | --- |
| **`mousedown`** | **마우스 버튼을 누르는 순간** |
| **`mouseup`** | **마우스 버튼을 눌렀다 떼는 순간** |
| **`click`** | **왼쪽 버튼을 클릭한 순간** |
| **`dblclick`** | **왼쪽 버튼을 빠르게 두 번 클릭한 순간** |
| **`contextmenu`** | **오른쪽 버튼을 클릭한 순간** |
| **`mousemove`** | **마우스를 움직이는 순간** |
| **`mouseover`** | **마우스 포인터가 요소 위로 올라온 순간** |
| **`mouseout`** | **마우스 포인터가 요소에서 벗어나는 순간** |
| **`mouseenter`** | **마우스 포인터가 요소 위로 올라온 순간 (버블링이 일어나지 않음)** |
| **`mouseleave`** | **마우스 포인터가 요소에서 벗어나는 순간 (버블링이 일어나지 않음)** |

### 포커스 이벤트

| **이벤트 타입** | **설명** |
| --- | --- |
| **`focusin`** | **요소에 포커스가 되는 순간** |
| **`focusout`** | **요소로부터 포커스가 빠져나가는 순간** |
| **`focus`** | **요소에 포커스가 되는 순간 (버블링이 일어나지 않음)** |
| **`blur`** | **요소로부터 포커스가 빠져나가는 순간 (버블링이 일어나지 않음)** |

### 입력 이벤트

| **이벤트 타입** | **설명** |
| --- | --- |
| **`change`** | **입력된 값이 바뀌는 순간** |
| **`input`** | **값이 입력되는 순간** |
| **`select`** | **입력 양식의 하나가 선택되는 순간** |
| **`submit`** | **폼을 전송하는 순간** |

### 스크롤 이벤트

| **이벤트 타입** | **설명** |
| --- | --- |
| **`scroll`** | **스크롤 바가 움직일 때** |

### 윈도우 창 이벤트

| **이벤트 타입** | **설명** |
| --- | --- |
| **`resize`** | **윈도우 사이즈를 움직일 때 발생** |

### 공통 프로퍼티

| **프로퍼티** | **설명** |
| --- | --- |
| **`type`** | **이벤트 이름 ('click', 'mouseup', 'keydown' 등)** |
| **`target`** | **이벤트가 발생한 요소** |
| **`currentTarget`** | **이벤트 핸들러가 등록된 요소** |
| **`timeStamp`** | **이벤트 발생 시각(페이지가 로드된 이후부터 경과한 밀리초)** |
| **`bubbles`** | **버블링 단계인지를 판단하는 값** |

### 마우스 이벤트

| **프로퍼티** | **설명** |
| --- | --- |
| **`button`** | **누른 마우스의 버튼 (0: 왼쪽, 1: 가운데(휠), 2: 오른쪽)** |
| **`clientX, clientY`** | **마우스 커서의 브라우저 표시 영역에서의 위치** |
| **`pageX, pageY`** | **마우스 커서의 문서 영역에서의 위치** |
| **`offsetX, offsetY`** | **마우스 커서의 이벤트 발생한 요소에서의 위치** |
| **`screenX, screenY`** | **마우스 커서의 모니터 화면 영역에서의 위치** |
| **`altKey`** | **이벤트가 발생할 때 alt키를 눌렀는지** |
| **`ctrlKey`** | **이벤트가 발생할 때 ctrl키를 눌렀는지** |
| **`shiftKey`** | **이벤트가 발생할 때 shift키를 눌렀는지** |
| **`metaKey`** | **이벤트가 발생할 때 meta키를 눌렀는지 (window는 window키, mac은 cmd키)** |

### 키보드 이벤트

| **프로퍼티** | **설명** |
| --- | --- |
| **`key`** | **누른 키가 가지고 있는 값** |
| **`code`** | **누른 키의 물리적인 위치** |
| **`altKey`** | **이벤트가 발생할 때 alt키를 눌렀는지** |
| **`ctrlKey`** | **이벤트가 발생할 때 ctrl키를 눌렀는지** |
| **`shiftKey`** | **이벤트가 발생할 때 shift키를 눌렀는지** |
| **`metaKey`** | **이벤트가 발생할 때 meta키를 눌렀는지 (window는 window키, mac은 cmd키)** |

### MouseEvent.button

| **값** | **내용** |
| --- | --- |
| **0** | **마우스 왼쪽 버튼** |
| **1** | **마우스 휠** |
| **2** | **마우스 오른쪽 버튼** |
| **3** | **X1 (일반적으로 브라우저 뒤로 가기 버튼)** |
| **4** | **X2 (일반적으로 브라우저 앞으로 가기 버튼)** |

### MouseEvent.relatedTarget

- `mouseenter, mouseleave, mouseover, mouseout` 이벤트에는 `relatedTarget`이라는 프로퍼티가 존재
- `target` 프로퍼티가 **이벤트가 발생한 요소**를 담고 있다면, `relatedTarget` 프로퍼티는 **이벤트가 발생하기 직전(또는 직후)에 마우스가 위치해 있던 요소**

### KeyboardEvent.type

| **이벤트 타입** | **설명** |
| --- | --- |
| **`keydown`** | **키보드의 버튼을 누르는 순간** |
| **`keypress`** | **키보드의 버튼을 누르는 순간 ('a', '5' 등 출력이 가능한 키에서만 동작하며, Shift, Esc 등의 키에는 반응하지 않음)** |
| **`keyup`** | **키보드의 버튼을 눌렀다 떼는 순간** |

### KeyboardEvent.key vs KeyboardEvent.code

- 키보드 이벤트 객체에는 `key`와 `code` 프로퍼티가 자주 사용
- `key`: **사용자가 누른 키가 가지고 있는 값**
- `code`: **누른 키의 물리적인 위치**

### 스크롤 이벤트

- `scroll` 이벤트는 보통 `window` 객체에 이벤트 핸들러를 등록하고 `window` 객체의 프로퍼티와 함께 자주 활용
- `scrollY` 프로퍼티 활용 시 스크롤된 특정한 위치를 기준으로 이벤트 핸들러 동작
- 스크롤 방향(위로 스크롤 중인지/아래로 스크롤 중인지)을 기준으로 이벤트 핸들러가 동작하게끔 활용
