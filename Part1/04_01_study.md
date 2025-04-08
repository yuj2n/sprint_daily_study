# 📝정리 내용
- React로 데이터 다루기

## 💡 처음 알게 된 사실

### 처음 한 번만 실행

- 처음 렌더링 이후

```jsx
useEffect(() => {
  // 실행할 코드
}, []);
```

### 값이 바뀔 때마다 실행

```jsx
useEffect(() => {
  // 실행할 코드
}, [dep1, dep2, dep3, ...]);
```

- 처음 렌더링 이후 1번 실행
- 그 이후 디펜던시 리스트 값 확인해서 바뀌면 실행

### React

- `hasNext` 값이 `true` 면 렌더링, `false` 면 렌더링 X
- `hide` 값이 `true` 면 렌더링 X, `false` 면 렌더링

```jsx
{hasNext && <button onClick={handleLoadMore}>더보기</button>}
{hide || <button onClick={handleLoadMore}>더보기</button>}
```

### 렌더링되지 않는 값들

```jsx
function App() {
  const nullValue = null;
  const undefinedValue = undefined;
  const trueValue = true;
  const falseValue = false;
  const emptyString = '';
  const emptyArray = [];

  return (
    <div>
      <p>{nullValue}</p>
      <p>{undefinedValue}</p>
      <p>{trueValue}</p>
      <p>{falseValue}</p>
      <p>{emptyString}</p>
      <p>{emptyArray}</p>
    </div>
  );
}

export default App;
```

### 주의할 점

```jsx
import { useState } from 'react';

function App() {
  const [num, setNum] = useState(0);

  const handleClick = () => setNum(num + 1);

  return (
    <div>
      <button onClick={handleClick}>더하기</button>
      {num && <p>num이 0 보다 크다!</p>}
    </div>
  );
}

export default App;
```

- 처음 실행했을 때 **숫자 0이 렌더링**
- '더하기' 버튼을 눌러서 `num` 값이 증가하면 `num이 0 보다 크다!` 가 렌더링

⇒ `{(num > 0) && <p>num이 0 보다 크다!</p>}` 로 명확히 하는 것이 안전

## 📌 기억할 것

### 데이터

- 데이터를 불러와서 사용할 속성만 사용 O

### 삼항 연산자 활용

```jsx
import { useState } from 'react';

function App() {
  const [toggle, setToggle] = useState(false);

  const handleClick = () => setToggle(!toggle);

  return (
    <div>
      <button onClick={handleClick}>토글</button>
      {toggle ? <p>✅</p> : <p>❎</p>}
    </div>
  );
}

export default App;
```