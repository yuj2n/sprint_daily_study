# 📝정리 내용

- React로 데이터 다루기

## 💡 처음 알게 된 사실

### 네트워크 로딩과 에러

```jsx
const handleLoad = async (options) => {
  let result;
  try {
    setLoadingError(null);
    setIsLoading(true);
    result = await getFoods(options);
  } catch (error) {
    setLoadingError(error);
    return;
  } finally {
    setIsLoading(false);
  }

  const {
    foods,
    paging: { nextCursor },
  } = result;
  if (!options.cursor) {
    setItems(foods);
  } else {
    setItems((prevItems) => [...prevItems, ...foods]);
  }
  setCursor(nextCursor);
};
```

- `try` 블록에서 error state를 초기화하고 loading state는 `true` 로 생성
- 에러 발생 시 `catch` 블록에서 error state 변경
- 함수 실행 종료를 위해 `return`
- `finally` 블록에서는 다시 loading state를 `false` 로 생성
- `catch` 블록에서 함수가 종료되었을 때도 loading state가 `false` 로 변경

```jsx
{cursor && (
  <button disabled={isLoading} onClick={handleLoadMore}>
    더보기
  </button>
)}
{loadingError?.message && <p>{loadingError.message}</p>}
```

- `disabled` 속성으로 isLoading값 넘겨주어 **중복 요청 방지**
- 조건부 렌더링으로 loadingError.message 존재 시만 메시지 보여줌
- 옵셔널 체이닝으로 값이 존재하지 않더라도 **에러**가 **발생 X**, **안전**하게 **접근** 가능

### 검색 기능

```jsx
const [search, setSearch] = useState('');

// ...

const handleSearchSubmit = (e) => {
  e.preventDefault();
  setSearch(e.target['search'].value);
};

// ...

<form onSubmit={handleSearchSubmit}>
  <input name="search" />
  <button type="submit">검색</button>
</form>
```

### 제어 컴포넌트

- input 태그의 `value`속성을 지정하고 사용하는 컴포넌트
- 장점: 값 예측 Easy, input 사용 값 여러 곳에서 쉽게 변경 가능 → React에서 권장!
- state와 prop이냐보다 React로 `value` 지정하는 것이 핵심
- 예시:  [폼 값을 객체 하나로 처리](https://www.notion.so/1ce2526f72c180f88198d54d51d52aee?pvs=21)

### 비제어 컴포넌트

- input 태그 `value`속성 지정 X
- **파일** 선택 input의 경우 반드시 비제어 컴포넌트로 작성해야 함.

## 📌 기억할 것

### 입력 폼

```jsx
const handleTitleChange = (e) => setTitle(e.target.value);

const handleCalorieChange = (e) => {
  const nextCalorie = Number(e.target.value) || 0;
  setCalorie(nextCalorie);
};

const handleContentChange = (e) => setContent(e.target.value);
```

- 각 스테이트 값을 `value` Prop으로 각 함수를 `onChange` Prop으로 input에 내려줌.

### 입력 폼2

```jsx
const handleSubmit = (e) => {
    e.preventDefault();
    console.log(values);
  };
  
function sanitize(type, value) {
  switch (type) {
    case 'number':
      return Number(value) || 0;

    default:
      return value;
  }
}

const handleChange = (e) => {
  const { name, value, type } = e.target;

  setValues((prevValues) => ({
    ...prevValues,
    [name]: sanitize(type, value),
  }));
};
```

### 표준 이벤트 Prop

| 종류 | 마음대로 바꿔도 됨? | 예시 |
| --- | --- | --- |
| 사용자 정의 prop (onDelete, onSomething 등) | ✅ **가능** | `<MyComponent onRemove={handleDelete} />` |
| DOM 이벤트 prop (onChange, onClick 등) | ❌ **불가능** | `<input onChange={...} />`만 가능 |

### HTML과 다른 점

**onChange**

- 입력 값 변경 시마다 핸들러 함수 실행
- `oninput` 이벤트와 동일

**htmlFor**

- <label /> 태그에서 사용하는 속성
- JS 반복문 키워드 `for`와 겹치기 때문에 `htmlFor` 사용

### 폼 다루는 기본적 방법

- state값을 생성하고 input의 `value` prop으로 state 값을 내려줌
- onChange Prop으로 핸들러 함수 넘겨주기

```jsx
const [checkIn, setCheckIn] = useState('2022-01-01');
const handleCheckInChange = (e) => setCheckIn(e.target.value);

<label htmlFor="checkIn">체크인</label>
<input id="checkIn" type="date" name="checkIn" value={checkIn} onChange={handleCheckInChange} />
```

### 폼 값을 객체 하나로 처리

```jsx
function TripSearchForm() {
  const [values, setValues] = useState({
    location: 'Seoul',
    checkIn: '2022-01-01',
    checkOut: '2022-01-02',
  })

  const handleChange = (e) => {
    const { name, value } = e.target;
    setValues((prevValues) => ({
      ...prevValues,
      [name]: value,
    }));
  }
    
  return (
    <form>
      <h1>검색 시작하기</h1>
      <label htmlFor="location">위치</label>
      <input id="location" name="location" value={values.location} placeholder="어디로 여행가세요?" onChange={handleChange} />
      <label htmlFor="checkIn">체크인</label>
      <input id="checkIn" type="date" name="checkIn" value={values.checkIn} onChange={handleChange} />
      <label htmlFor="checkOut">체크아웃</label>
      <input id="checkOut" type="date" name="checkOut" value={values.checkOut} onChange={handleChange} />
      <button type="submit">검색</button>
    </form>
  )
}
```

### 기본 `submit` 동작 방지

- HTML 폼의 기본 동작은 `submit` 타입의 버튼 누를 시 **페이지 이동**!
- 이벤트 객체의 `preventDefault`로 `submit` **동작 방지** 가능

```jsx
const handleSubmit = (e) => {
  e.preventDefault();
  // ...
}
```