# 📝정리 내용

- React로 웹 사이트 만들기

## 💡 처음 알게 된 사실

### 리액트 라우터

- npm: 패키지 설치와 삭제처럼 패키지 관리 프로그램
- 설치명령: `npm install react-router-dom@6`
- ❗주의: `react-router` 가 아닌 `react-router-dom` 사용하기!!

### 라우트 사용

- 최상위 컴포넌트에 감싸주면 하위 컴포넌트 모든 곳에서 사용 가능

```jsx
import { BrowserRouter } from 'react-router-dom';

function App() {
  return <BrowserRouter> ... </BrowserRouter>;
}
```

### 페이지 나누는 방법

- `Routes` 컴포넌트 내부에 `Route` 컴포넌트 배치해 페이지 나누기
- 일치하는 경로가 없는 경우 빈 페이지로 이동

```jsx
<Routes>
  <Route path="/" element={<HomePage />} />
  <Route path="posts" element={<PostListPage />} />
  <Route path="posts/1" element={<PostPage />} />
</Routes>
```

### 링크

- <a> 태그 대신 `Link` 컴포넌트 사용
- `to` prop으로 이동 경로 정하기

```jsx
<Link to="/posts">블로그</Link>
```

### 하위 페이지 나누기

- `Route` 내부에 `Route` 컴포넌트 배치
- 하위 페이지의 최상위 경로 해당 경로는 `path` prop을 주지 않고 `index` prop 사용

```jsx
<Routes>
  <Route path="/"><HomePage /></Route>
  <Route path="posts" element={<PostLayout />} >
    <Route index element={<PostListPage />}  />
    <Route path="1" element={<PostPage />}  />
  </Route>
</Routes>
```

- `Outlet` 컴포넌트로 공통된 레이아웃 지정

```jsx
import { Outlet } from 'react-router-dom';

function PostLayout() {
  return (
    <div>
      <h1>블로그</h1>
      <hr />
      <Outlet />
    </div>
  );
}

export default PostLayout;
```

### 동적인 경로 다루기

- `:`로 시작하는 문자열 사용 → 경로에 파라미터 지정 가능
- `/posts/:postId` 경로는 `/posts/123` 와 같은 주소로 접속하면 `postId` 파라미터 받음

```jsx
<Routes>
  <Route path="/"><HomePage /></Route>
  <Route path="posts" element={<PostLayout />} >
    <Route index element={<PostListPage />}  />
    <Route path=":postId" element={<PostPage />}  />
  </Route>
</Routes>
```

- 경로 파라미터 사용하려면 `useParams` 훅 사용

```jsx
function PostPage() {
  const { postId } = useParams();
  // ...
}
```

### 쿼리 사용하기

- `useSearchParams` Custom hook으로 `SearchParams` 객체 받기 가능
- `searchParams`객체와 `Setter`함수 배열형으로 리턴
- 쿼리 값은 `searchParams`의 `get`함수로 가져옴

```jsx
import { useSearchParams } from 'react-router-dom';

function PostListPage() {
  const [searchParams, setSearchParams] = useSearchParams();
  const filterQuery = searchParams.get('filter');
  // ...
}
```

- 쿼리 값 변경 후 주소 이동하려면 `Setter` 함수에 객체 넘겨주기
- 객체의 프로퍼티로 쿼리 값 지정 가능

```jsx
setSearchParams({ // ?filter=react 쿼리로 이동
  filter: 'react',
});
```

### Navigate 컴포넌트

리턴 값으로 `Navigate` 컴포넌트를 리턴하면 `to` prop으로 지정한 경로로 이동

```jsx
function PostPage() {
  // ...
  const post = getPost(postId);
  // post가 없는 경우 /posts 페이지로 이동
  if (!post) {
    return <Navigate to="/posts" />;
  }
  // ...
}
```

### useNavigate Hook

`useNavigate` Hook으로 navigate 함수 가져오면 이 함수로 페이지 이동

```jsx
const navigate = useNavigate();

const handleClick = () => {
  // ... 어떤 작업을 한 다음에 페이지를 이동
  navigate('/wishlist');
}
```

- `Link`: 유저 조작 기반 (UI)
- `Navigate`: 조건 만족 시 즉시 이동 (렌더링 타이밍)
- `useNavigate`: 이벤트/비동기 흐름 끝나고 이동 (동적 제어)

| 구분 | 사용 시기 📌 | 예시 💡 |
| --- | --- | --- |
| **`Link`** | 사용자가 클릭해서 이동할 때 | - 메뉴바, 버튼, 이미지 등 클릭 시 페이지 이동
- "홈으로" 링크 등 |
| **`Navigate`** | 렌더링 시 조건에 따라 자동 이동할 때 | - 비회원이 마이페이지 접근 시 로그인 페이지로 이동- 삭제된 상품 접근 시 홈으로 리다이렉트 |
| **`useNavigate`** | 코드 실행 후 동적으로 이동할 때 | - 장바구니에 담은 후 장바구니 페이지로 이동
- 결제 완료 후 주문 완료 페이지로 이동
- 로그인 완료 후 원래 페이지로 돌아가기 |

## 📌 기억할 것