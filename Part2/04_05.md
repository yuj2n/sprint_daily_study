# 📝정리 내용

- React로 데이터 다루기

---

해결 안된 문제 

https://www.codeit.kr/topics/handling-data-with-react/lessons/5081

- 추가적으로 복습할 부분: React로 데이터 다루기 2-5챕터
- 만들어볼 React 프로젝트 기능:
1. **페이지네이션**
2. **검색 기능**
3. **입력 폼**
4. **별점**
5. **글 작성/수정/삭제**
6. **Context**

---

## 💡 처음 알게 된 사실

### exhaustive-deps 규칙

- 문제 상황

```jsx
import { useEffect, useState } from 'react';

function App() {
  const [count, setCount] = useState(0);
  const [num, setNum] = useState(0);

  const addCount = () => {
    setCount(c => c + 1);
    console.log(`num: ${num}`);
  }

  const addNum = () => setNum(n => n + 1);

  useEffect(() => {
    console.log('timer start');
    const timerId = setInterval(() => {
      addCount();
    }, 1000);

    return () => {
      clearInterval(timerId);
      console.log('timer end');
    };
  }, []);

  return (
    <div>
      <button onClick={addCount}>count: {count}</button>
      <button onClick={addNum}>num: {num}</button>
    </div>
  );
}

export default App;
```

버튼 클릭 시  `num` 스테이트 변경되도 0만 출력됨

이유❓: 과거의 `num` 스테이트 지속 참조

→ 경고 규칙인  `react-hooks/exhaustive-deps` (항상 최신 값으로 useEffect나 useCallback 사용 권장)

⇒  Prop이나 State와 관련된 값은 되도록이면 빠짐없이 **디펜던시**에 **추가**

### **useCallback으로 함수 재사용하기**

- 위 코드에서 `useEffect(() ⇒ {//…}, [addCount]);`로 작성 시 문제
    - `count` 변경 시마다 `addCount` 새로 생성

```jsx
const addCount = useCallback(() => {
    setCount((c) => c + 1);
    console.log(`num: ${num}`);
  }, [num]);
```

→ `addCount`를 불필요하게 새로 생성하지 않게 `useCallback`로 감싸주기

⇒  `useCallback` 의 디펜던시 리스트 값이 바뀔 때만 함수를 새로 생성

### Context

- 의미: 맥락, 어떤 상황에 대한 정보
- ex) 언어 선택 상황을 **여러 컴포넌트**에 **공유**하고 싶은 경우
- `Props drilling`의 해결 기능!

<aside>
💡

**생성**

```jsx
import { createContext } from 'react';

const LocaleContext = createContext('ko');
```

🎨 **적용**

- `Context` 사용 시 반드시 **값 공유 범위** 정하기!!
- `Context` 객체의 `Provider` 컴포넌트로 범위 규정 가능
- `Provider`의 `value` prop으로 공유 값 내려주면 됨

```jsx
import { createContext } from 'react';

const LocaleContext = createContext('ko');

function App() {
  return (
    <div>
       ... 바깥의 컴포넌트에서는 LocaleContext 사용불가

       <LocaleContext.Provider value="en">
          ... Provider 안의 컴포넌트에서는 LocaleContext 사용가능
       </LocaleContext.Provider>
    </div>
  );
}
```

✨ **사용**

- `useContext` Hook 사용 시, 값을 가져와서 사용 가능

```jsx
import { createContext, useContext } from 'react';

const LocaleContext = createContext('ko');

function Board() {
  const locale = useContext(LocaleContext);
  return <div>언어: {locale}</div>;
}

function App() {
  return (
    <div>
       <LocaleContext.Provider value="en">
          <Board />
       </LocaleContext.Provider>
    </div>
  );
}
```

**🌟 활용**

- Provider 역할의 컴포넌트 하나 생성
- 내부에 State 생성해 value로 넘겨주기
- useLocale과 같이 useContext로 값을 가져오는 커스텀 Hook 작성 가능

→ Context에서 쓰는 State 값을 반드시 작성한 함수로만 사용가능하여 안전한 코드 작성 O(ex. 다른 곳에서도 쓰는데 다른 데로 옮겨서 에러가 나는 경우 **방지**)

```jsx
import { createContext, useContext, useState } from 'react';

const LocaleContext = createContext({});

export function LocaleProvider({ children }) {
  const [locale, setLocale] = useState();
  return (
    <LocaleContext.Provider value={{ locale, setLocale }}>
      {children}
    </LocaleContext.Provider>
  );
}

export function useLocale() {
  const context = useContext(LocaleContext);

  if (!context) {
    throw new Error('반드시 LocaleProvider 안에서 사용해야 합니다');
  }

  const { locale } = context;
  return locale;
}

export function useSetLocale() {
  const context = useContext(LocaleContext);

  if (!context) {
    throw new Error('반드시 LocaleProvider 안에서 사용해야 합니다');
  }

  const { setLocale } = context;
  return setLocale;
}
```

💭**궁금한 점**

1. `createContext()`와 같이 기본값 미설정하면?

→ 기본 값이 undefined로 설정

1. `Provider`가 있어도 `value` prop 안 넘겨주면 기본값일까?

→ 값 준다하고 안 준 셈이라 오히려 undefined 전달! ⇒ `Provider`의 value 넘겨주기

1. 커스텀 훅을 Context.Provider 외부에서 쓰면 값이 존재할까?

→ X, 따라서 error를 throw 해야 함.

</aside>

| 상황 | useContext 결과 |
| --- | --- |
| `Provider` ❌ | 기본값 `'ko'` 사용 |
| `Provider` 외부 | 기본값 `'ko'` 사용 |
| `Provider` 내부 + value 있음 | `value` 사용 (예: `'en'`) |
| `Provider` 내부 + value 없음 | `undefined` (주의!) |

| 도구 | 주 역할/용도 | 전역 상태 | 서버 상태 | 특징 요약 | 사용 난이도 | 사용 시점 추천 💡 |
| --- | --- | --- | --- | --- | --- | --- |
| **React Context** | 전역 상태 공유 | ✅ | ❌ | React 내장, 매우 기본적, 단순 공유에는 좋음, 로직 복잡하면 비효율적 | ⭐⭐ | 간단한 테마, 언어, 로그인 상태 공유 등 |
| **Redux** | 복잡한 전역 상태 관리 | ✅ | ❌ | 엄격한 구조, 디버깅/미들웨어 좋음, boilerplate 많음 | ⭐⭐⭐⭐ | 대규모 앱, 복잡한 비즈니스 로직 필요 시 |
| **Recoil** | React 친화적인 전역 상태 공유 | ✅ | ❌ | atom/selector 기반, 사용 쉬움, 컴포넌트 간 공유에 유리 | ⭐⭐ | Redux는 과하고 Context는 부족한 상황 |
| **React Query** | 서버 상태 관리 (fetch, cache 등) | ❌ | ✅ | 데이터 패칭 자동화, 캐싱/리페치 관리 탁월, 클라이언트 상태는 부적합 | ⭐⭐ | API 중심 앱, 리스트 뷰/상세 등 서버 통신 필요 시 |
| **SWR** | 서버 상태 관리 (간단한 용도) | ❌ | ✅ | Vercel 제작, 간단한 fetch/cache에 적합, Next.js와 궁합 좋음 | ⭐ | 가벼운 SSR/SSG 기반 앱, 빠른 prototyping |
| **Flux** | 상태 관리 설계 철학 (패턴) | ✅ | ❌ | Redux의 기반 개념, 직접 구현은 잘 안 함 | ⭐⭐⭐ | 이론 공부용, 설계 철학 이해용 |

### 결론

- Context API 쓰다가 문제점이 발견되면 Recoil등 다른 것 사용해보기

## 📌 기억할 것

### 되도록 파라미터 활용하기

- useCallback 사용 코드 개선

```jsx
 const addCount = (log) => {
    setCount((c) => c + 1);
    console.log(log);
  }
  // ...
  useEffect(() => {
    console.log('timer start');
    const timerId = setInterval(() => {
      **addCount(`num ${num}`)**;
    }, 1000);

    return () => {
      clearInterval(timerId);
      console.log('timer end');
    };
  }, [num]);
  // ...
```

- `addCount`에서 `num`을 직접 참조 X & `useCallback` X → 파라미터로 받아오기!

⇒ `num` 변경 시마다 타이머 재시작의 **명확성** ⬆

### Hook의 규칙

- 반드시 리액트 컴포넌트 함수 내부에서 사용
- 컴포넌트 함수의 최상위에서만 사용(조건문, 반복문 내부 X)

| 방식 | 초깃값 계산 시점 | 추천 상황 |
| --- | --- | --- |
| `useState(값)` | 컴포넌트 렌더링 때마다 평가됨 | 가벼운 값 |
| `useState(() => 값)` | 최초 렌더 시에만 평가됨 | 계산 비용이 크거나 복잡할 때 |

### 로컬 스토리지에서 초깃값 불러오기

```jsx
const [user, setUser] = useState(() => {
  const saved = localStorage.getItem('user');
  return saved ? JSON.parse(saved) : null;
});
```

### **이전 State를 참조해서 State 변경**

비동기 함수에서 최신 State 값을 가져와서 새로운 State 값을 만들 때

```jsx
setState((prevState) => {
  // ...
  return nextState
});
```

### **useEffect**

- 사이드 이펙트 정리(Cleanup)하기

```jsx
useEffect(() => {
  // 사이드 이펙트

  return () => {
    // 정리
  }
}, [dep1, dep2, dep3, ...]);
```

### **useRef**

**생성하고 DOM 노드에 연결하기**

```jsx
const ref = useRef();
// ...
return <div ref={ref}>안녕 리액트!</div>;
```

### **DOM 노드 참조하기**

```jsx
const node = ref.current;
if (node) {
  // node를 사용하는 코드
}
```

### **useCallback**

함수를 매번 새로 생성하는 것이 아니라 디펜던시 리스트가 변경될 때만 함수를 생성

```jsx
const handleLoad = useCallback((option) => {
  // ...
}, [dep1, dep2, dep3, ...]);
```

### **useAsync**

비동기 함수의 로딩, 에러 처리를 하는 데 사용할 수 있는 함수

- 함수를 `asyncFunction` 이라는 파라미터로 추상화
- `wrappedFunction` 이라는 함수를 만들어 사용하는 방식

```jsx
function useAsync(asyncFunction) {
  const [pending, setPending] = useState(false);
  const [error, setError] = useState(null);

  const wrappedFunction = useCallback(async (...args) => {
    setPending(true);
    setError(null);
    try {
      return await asyncFunction(...args);
    } catch (error) {
      setError(error);
    } finally {
      setPending(false);
    }
  }, [asyncFunction]);

  return [pending, error, wrappedFunction];
}
```

### **useToggle**

`toggle` 함수를 호출할 때마다 `value` 값이 참/거짓으로 번갈아가며 바뀝니다.

ON/OFF 스위치 같은 걸 만들 때 유용하겠죠?

```jsx
function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);
  const toggle = () => setValue((prevValue) => !prevValue);
  return [value, toggle];
}
```

### **useTimer**

- `start` 실행 시 `callback` 파라미터로 넘겨 준 함수를 `timeout` 밀리초마다 실행
- `stop`  실행 시 정지
- `setInterval` 이란 함수는 웹 브라우저에 함수를 등록해서 일정한 시간 간격마다 실행
- 실행마다 사이드 이펙트 생성, 미사용 시 정리
- `clearInterval` 함수로 사이드 이펙트 정리⭐

```jsx
function useTimer(callback, timeout) {
  const [isRunning, setIsRunning] = useState(false);

  const start = () => setIsRunning(true);

  const stop = () => setIsRunning(false);

  useEffect(() => {
    if (!isRunning) return;

    const timerId = setInterval(callback, timeout); // 사이드 이펙트 발생
    return () => {
      clearInterval(timerId); // 사이드 이펙트 정리
    };
  }, [isRunning, callback, timeout]);
  
  return [start, stop];
}
```