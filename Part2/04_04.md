# 📝정리 내용

- React로 데이터 다루기

## 💡 처음 알게 된 사실

### **useRef 예시**

- 이미지 크기 구하기

```jsx
import { useRef } from 'react';

function Image({ src }) {
  const imgRef = useRef();

  const handleSizeClick = () => {
    const imgNode = imgRef.current;
    if (!imgNode) return;

    const { width, height } = imgNode;
    console.log(`${width} x ${height}`);
  };

  return (
    <div>
      <img src={src} ref={imgRef} alt="크기를 구할 이미지" />
      <button onClick={handleSizeClick}>크기 구하기</button>
    </div>
  );
}
```

### 🔍Quiz

> 리액트에서 DOM 노드를 참조할 때 사용할 수 있는 Prop은 _**ref**__ 이다.
이때 Prop으로 전달하는 `Ref` 객체는 `useRef`를 사용하면 만들 수 있다.
> 

## 📌 기억할 것

### useRef

- React에서 DOM 요소나 값 저장 시 사용하는 `Hook`
- `current` 프로퍼티 활용
- 용도
    1. DOM 요소에 직접 **접근**
    2. 렌더링과 무관한 **값 저장** (예: 이전 값 저장, 타이머 **ID** 등)

```jsx
import { useRef } from 'react';
// ...
 const inputRef = useRef();

 const handleClearClick = () => {
   const inputNode = inputRef.current;
   if(!inputNode) return;
 
   inputNode.value = '';
   onChange(name, null);
 };
```

### useEffect 활용

- 미리보기 기능 추가

```jsx
const [preview, setPreview] = useState();
// ...
useEffect(()=> {
     if (!value) return;
      const nextPreview = URL.createObjectURL(value);
      setPreview(nextPreview);
      
      return () => {
        setPreview();
        URL.revokeObjectURL(nextPreview);
      }
   }, [value])
   // ...
   return (
    <div>
      <img src={preview} alt="이미지 미리보기" />
      <input type="file" onChange={handleChange} ref={inputRef} />
      <button type="button" onClick={handleClearClick}>
        X
      </button>
    </div>
  );
```

- Q1. `const nextPreview = URL.createObjectURL(value);` 에서 value는 뭘까?
    
    ```jsx
    const [values, setValues] = useState({
    	imgFile: null,     // ✅ 파일 객체가 들어오는 곳
    	title: '',         // 텍스트
    	calorie: 0,        // 숫자
    	content: '',       // 텍스트
    });
    
    <FileInput
      name="imgFile"
      value={values.imgFile}
      onChange={handleChange}
    />
    ```
    
    - value prop으로 value의 `imgFile`값만 전달됨.
    - FileInput 컴포넌트에서 value는 초기에는 null값, 파일 선택 후 e.target.files[0]을 가리킴.
- Q2. `setPreview();`를 `setPreview(’’);`라고 하면 안될까?

→ `''` → `<img src="">`는 빈 경로 요청을 만들 수도 있어 권장 X

### Side Effect

- 프로그래밍에선 외부에 부수적인 작용을 뜻함
- ex. `console.log`

### Side Effect와 useEffect

- useEffect는 side effect 실행 시 사용
- 리액트 외부 데이터나 상태 변경 시 사용
    - DOM 노드 직접 변경
    - 브라우저에 데이터 저장
    - 네트워크 리퀘스트 전달

**페이지 정보 변경**

```jsx
useEffect(() => {
  document.title = title; // 페이지 데이터를 변경
}, [title]);
```

**네트워크 요청**

```jsx
useEffect(() => {
  fetch('https://example.com/data') // 외부로 네트워크 리퀘스트
    .then((response) => response.json())
    .then((body) => setData(body));
}, [])
```

**데이터 저장**

```jsx
useEffect(() => {
  localStorage.setItem('theme', theme); // 로컬 스토리지에 테마 정보를 저장
}, [theme]);
```

참고: `localStorage` 는 웹 브라우저에서 데이터를 저장할 수 있는 기능입니다.

**타이머**

```jsx

useEffect(() => {
  const timerId = setInterval(() => {
    setSecond((prevSecond) => prevSecond + 1);
  }, 1000); // 1초마다 콜백 함수를 실행하는 타이머 시작

  return () => {
    clearInterval(timerId);
  }
}, []);

```

참고: `setInterval`함수 사용 시 일정한 시간마다 콜백 함수를 실행 가능

### Request

- `onclick` 이벤트 핸들러 함수로 네트워크 리퀘스트 전송 O
- 페이지가 열리자마자 데이터를 불러오기 위해 `useEffect` 사용 O

→ 둘 다 되면 뭘 쓰지❓

⇒ `useEffect`는 동기화(컴포넌트 내부 데이터와 리액트 외부 데이터 일치)에 유용

```jsx
import { useState } from 'react';

const INITIAL_TITLE = 'Untitled';

function App() {
  const [title, setTitle] = useState(INITIAL_TITLE);

  const handleChange = (e) => {
    const nextTitle = e.target.value;
    setTitle(nextTitle);
    document.title = nextTitle;
  };

  const handleClearClick = () => {
    const nextTitle = INITIAL_TITLE;
    setTitle(nextTitle);
    document.title = nextTitle;
  };

  return (
    <div>
      <input value={title} onChange={handleChange} />
      <button onClick={handleClearClick}>초기화</button>
    </div>
  );
}

export default App;
```

- `title`변경 후 `document.title`도 동시 변경
- `setTitle` 함수 작성마다 같이 변경해주는 것 잊을 수 있음

**useEffect 사용 예시**

```jsx
// ...
  const handleChange = (e) => {
    const nextTitle = e.target.value;
    setTitle(nextTitle);
  };

  const handleClearClick = () => {
    setTitle(INITIAL_TITLE);
  };

  useEffect(() => {
    document.title = title;
  }, [title]);
// ...
```

- `document.title`을 매번 신경쓰지 않아도 됨 → 편리
- 첫 렌더링 시 ‘Untitled’ 값 적용 효과
- 예측 가능성 ⬆ / 반복 코드 최소화

⇒ useEffect는 리액트 내부와 외부 데이터 일치 활용에 탁월

### 정리 함수

- 브라우저 **메모리 누수** **방지**
- ex) 이미지 파일이 **변경/삭제** 시 둘 다에 대한 사이드 이펙트 처리

```jsx
useEffect(() => {
  // 사이드 이펙트

  return () => {
    // 사이드 이펙트에 대한 정리
  }
}, [dep1, dep2, dep3, ...]);
```

- 정리 함수 실행 시점❓
    - 새 콜백 함수 호출 전(앞서 실행한 콜백의 사이드 이펙트 정리)
    - 컴포넌트 제거 전 실행(맨 마지막 실행한 콜백의 사이드 이펙트 정리)