# 📝정리 내용

- Styled Components

## 💡 처음 알게 된 사실

### Nesting 문법

**& 선택자**

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: #6750a4;
  border: none;
  color: #ffffff;
  padding: 16px;

  &:hover,
  &:active {
    background-color: #463770;
  }
`;

export default Button;
```

- hover나 active 되었을 때의 스타일 지정
- & 선택자 = 부모 선택자
- &:hover = .Button:hover

### 컴포넌트 선택자

컴포넌트 내부 타 컴포넌트 선택

![image.png](attachment:4eb28180-388b-43ed-998f-3c5925355d45:image.png)

```jsx
import styled from 'styled-components';
import nailImg from './nail.png';

const Icon = styled.img`
  width: 16px;
  height: 16px;
`;

const StyledButton = styled.button`
  background-color: #6750a4;
  border: none;
  color: #ffffff;
  padding: 16px;

  **& ${Icon}** {
    margin-right: 4px;
  }

  &:hover,
  &:active {
    background-color: #463770;
  }
`;

function Button({ children, ...buttonProps }) {
  return (
    <StyledButton {...buttonProps}>
      <Icon src={nailImg} alt="nail icon" />
      {children}
    </StyledButton>
  );
}

export default Button;
```

- 컴포넌트 선택자로 사용: `${Icon}`같이 컴포넌트 자체를 템플릿 리터럴 안에 넣기
- &와 자손 결합자 사용 시 & 생략 가능!
- `& ${Icon}` = `${Icon}` (권장)

### 다이나믹 스타일링

크기 조절 `size`와 경계선 둥글기 지정 `round`

```jsx
import styled from 'styled-components';

const SIZES = {
  large: 24,
  medium: 20,
  small: 16,
};

const Button = styled.button`
  background-color: #6750a4;
  border: none;
  border-radius: ${({ round }) => round ? `9999px` : `3px`};
  color: #ffffff;
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
  padding: 16px;

  &:hover,
  &:active {
    background-color: #463770;
  }
`;

export default Button;
```

```jsx
import styled from 'styled-components';
import Button from './Button';

const Container = styled.div`
  ${Button} {
    margin: 10px;
  }
`;

function App() {
  return (
    <Container>
      <h1>기본 버튼</h1>
      <Button size="small">small</Button>
      <Button size="medium">medium</Button>
      <Button size="large">large</Button>
      <h1>둥근 버튼</h1>
      <Button size="small" round>
        round small
      </Button>
      <Button size="medium" round>
        round medium
      </Button>
      <Button size="large" round>
        round large
      </Button>
    </Container>
  );
}

export default App;
```

- 표현식 삽입법: (`${ ... }`)로 JS 코드 삽입 가능
- Prop에 따라 컴포넌트 스타일 다르게 적용 가능

### 함수 사용

```jsx
const SIZES = {
  large: 24,
  medium: 20,
  small: 16
};

const Button = styled.button`
  ...
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
`;
```

- 파라미터로 Props를 받고 스타일 코드 리턴
- 템플릿 리터럴의 기능이 아닌 Styled Components의 내부적 처리
- prop 값이 없거나 잘못된 경우 undefined를 문자열 처리 → 잘못된 코드 ⇒ `??` 사용

### 연산자 사용

```jsx
border-radius: ${({ round }) => round ? `9999px` : `3px`};
```

### CSS 함수

```jsx
import styled, { css } from 'styled-components';

const SIZES = {
  large: 24,
  medium: 20,
  small: 16
};

const fontSize = css`
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
`;

const Button = styled.button`
  ...
  ${fontSize}
`;

const Input = styled.input`
  ...
  ${fontSize}
`;
```

- `css` 함수: 반복되는 코드를 한 곳에서 지정하고 여러 곳에 활용
- 함수를 사용하지 않는 단순한 문자열이더라도 `css` 함수 사용 습관화 권장

### 애니메이션

```jsx
@keyframes bounce {
  0% {
    transform: translateY(0%);
  }

  50% {
    transform: translateY(100%);
  }

  100% {
    transform: translateY(0%);
  }
}

.ball {
  animation: bounce 1s infinite;
  background-color: #ff0000;
  border-radius: 50%;
  height: 50px;
  width: 50px;
}
```

- `@keyframes`로 키프레임 애니메이션을 선언한 다음에, 그걸 `animation` 속성에서 이름으로

### `keyframes` 함수

플레이스 홀더 애니메이션: 로딩 동안 미리보기

```jsx
import styled, { keyframes } from 'styled-components';

const placeholderGlow = keyframes`
  50% {
    opacity: 0.2;
  }
`;

export const PlaceholderItem = styled.div`
  background-color: #888888;
  height: 20px;
  margin: 8px 0;
`;

const Placeholder = styled.div`
  animation: ${placeholderGlow} 2s ease-in-out infinite;
`;

export default Placeholder;
```

```jsx
import styled from 'styled-components';
import Placeholder, { PlaceholderItem } from './Placeholder';

const A = styled(PlaceholderItem)`
  width: 60px;
  height: 60px;
  border-radius: 50%;
`;

const B = styled(PlaceholderItem)`
  width: 400px;
`;

const C = styled(PlaceholderItem)`
  width: 200px;
`;

function App() {
  return (
    <div>
      <Placeholder>
        <A />
        <B />
        <C />
      </Placeholder>
    </div>
  );
}

export default App;
```

- `keyframes` 함수가 리턴하는 변수는 단순한 문자열이 아니라 JavaScript 객체
- 반드시 `styled` 함수나 `css` 함수를 통해 사용해야 한다는 것을 주의

### ThemeProvider

Context테마로 설정된 값을 사이트 전체에서 참조하기

```jsx
import { ThemeProvider } from "styled-components";
import Button from "./Button";

function App() {
  const theme = {
    primaryColor: '#1da1f2',
  };

  return (
    <ThemeProvider theme={theme}>
      <Button>확인</Button>
    </ThemeProvider>
  );
}

export default App;
```

- `theme` 객체 내려주기 → `ThemeProvider` 내부 **Styled Components**로 만든 컴포에서는 Props 사용하듯 `theme` 객체 사용 가능

```jsx
const Button = styled.button`
  background-color: ${({ theme }) => theme.primaryColor};
  /* ... */
`;
```

여러 테마 선택 - `useState`  활용

```jsx
import { useState } from 'react';
import { ThemeProvider } from 'styled-components';
import Button from './Button';

function App() {
  const [theme, setTheme] = useState({
    primaryColor: '#1da1f2',
  });

  const handleColorChange = (e) => {
    setTheme((prevTheme) => ({
      ...prevTheme,
      primaryColor: e.target.value,
    }));
  };

  return (
    <ThemeProvider theme={theme}>
      <select value={theme.primaryColor} onChange={handleColorChange}>
        <option value="#1da1f2">blue</option>
        <option value="#ffa800">yellow</option>
        <option value="#f5005c">red</option>
      </select>
      <br />
      <br />
      <Button>확인</Button>
    </ThemeProvider>
  );
}

export default App;
```

**ThemeContext**

```jsx
import { useContext } from 'react';
import { ThemeContext } from 'styled-components';

// ...

function SettingPage() {
  const theme = useContext(ThemeContext); // { primaryColor: '#...' }
}

```

- 테마 설정 페이지 생성 시 테마 값을 일반적 컴포넌트에서 참조
- `ThemeContext`를 불러오고, 이 값은 React Context이기 때문에 `useContext`로 씀

### 버튼 모양 링크

```jsx
<Button href="https://example.com" as="a">
  LinkButton
</Button>
```

- `as` 로 태그 이름을 내려주면 해당하는 태그로 사용
- 굳이 버튼 모양 링크 컴포넌트 생성 필요 X

### 원치 않는 Props가 전달될 때

Prop을 Spread 문법을 사용해서 `<a>` 태그로 전달하는 `Link` 컴포넌트

```jsx
import styled from 'styled-components';

function Link({ className, children, ...props }) {
  return (
    <a {...props} className={className}>
      {children}
    </a>
  );
};

const StyledLink = styled(Link)`
  text-decoration: ${({ underline }) => underline ? `underline` : `none`};
`;

function App() {
  return (
    <StyledLink underline={false} href="https://codeit.kr">
      Codeit으로 가기
    </StyledLink>
  );
}

export default App;
```

**해결방법1** - `underline` 제외

```jsx
function Link({ className, children, **underline,** ...props }) {
  return (
    <a {...props} className={className}>
      {children}
    </a>
  );
};
```

**근본적 해결** - 아예 Prop이 전달되지 않게 만드는 방법(`Transient Prop`: $)

```jsx
import styled from 'styled-components';

function Link({ className, children, ...props }) {
  return (
    <a {...props} className={className}>
      {children}
    </a>
  );
};

const StyledLink = styled(Link)`
  text-decoration: ${({ **$underline** }) => **$underline** ? `underline` : `none`};
`;

function App() {
  return (
    <StyledLink **$underline**={false} href="https://codeit.kr">
      Codeit으로 가기
    </StyledLink>
  );
}

export default App;
```

- `$underline` Prop은 `StyledLink` 안에서만 사용되고, `Link` 로 전달 X

## 📌 기억할 것

### Styled Components

Button 컴포넌트 예시

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: #ededed;
  border: none;
  border-radius: 8px;
`;

function App() {
  return (
    <div>
      <h1>안녕 Styled Components!</h1>
      <Button>확인</Button>
    </div>
  );
}

export default App;
```

- 컴포넌트 생성과 동시에 해당 컴포넌트 스타일 작성 → 편리 & 개발 속도 증가
- React의 단점: 컴포넌트 생성 후 스타일 적용 시 해당 태그 타켓 CSS 코드 JSX 문법으로 따로 작성 필요

### 클래스 이름

```jsx
const StyledApp = styled.div`
  background-color: #000000;
`;

const Dashboard = styled.div`
  font-size: 16px;
`;

function App() {
  return (
    <StyledApp>
      <Dashboard> ... </Dashboard>
    </StyledApp>
  );
}
```

- 클래스 이름을 아예 쓰지 않음으로써 클래스 이름 겹칠 일 X

### 유지 보수

```css
import { css } from 'styled-components';

const shadow20 = css`
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.2);
`;

const shadow40 = css`
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.4);
`;
```

```jsx

import { shadow20 } from '../shadows';

const Card = styled.div`
  ${shadow20}
  ...(다른 CSS 코드)
`;

export default Card;
```

- 스타일 재사용이 필요한 상황에서 JS 변수 생성
- 에디터로 확인 쉬움 / 이름 변경 및 삭제 편리

### 설치

```jsx
npm init react-app 프로젝트 명
```

### 컴포넌트 작성

```jsx
const Button = styled.button`
  background-color: #6750a4;
  border: none;
  color: #ffffff;
  padding: 16px;
`;
```

- tagname: 스타일 적용할 HTML 태그 이름
- 템플릿 리터럴 문법으로 CSS 코드 작성
- 컴포넌트처럼 JSX로 사용 가능

### `styled()` 함수

```jsx
import styled from 'styled-components';
import Button from './Button';

const SubmitButton = styled(Button)`
  background-color: #de117d;
  display: block;
  margin: 0 auto;
  width: 200px;

  &:hover {
    background-color: #f5070f;
  }
`;

function App() {
  return (
    <div>
      <SubmitButton>계속하기</SubmitButton>
    </div>
  );
}

export default App;
```

- `styled.tagname` 만든 컴포넌트는 바로 `styled()` 함수 사용 가능
- 이외 컴포넌트는 따로 처리 필요

```jsx
function TermsOfService({ className }) {
  return (
    <div className={className}>
      ...
    </div>
  );
}
```

- **Styled Components**는 내부적으로 `className` 생성
- JSX 문법으로 직접 만든 컴포넌트는 `className` 정보가 없어 스타일 적용 X

→ `className` 값을 **Prop**으로 따로 내려줘야 `styled()` 함수 사용 가능

- 이때, `styled(TermsOfService)`에서 작성 코드는 `TermsOfService` 내부 `<div>` 태그에 적용

### 글로벌 스타일

폰트 전체 스타일 지정

```jsx
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
  * {
    box-sizing: border-box;
  }

  body {
    font-family: 'Noto Sans KR', sans-serif;
  }
`;

function App() {
  return (
    <>
      <GlobalStyle />
      <div>글로벌 스타일</div>
    </>
  );
}

export default App;
```

- `createGlobalStyle` 함수는 다른 **Styled Components** 함수들과 마찬가지로 템플릿 리터럴 문법으로 사용
- `<style>` 태그로 컴포넌트로 생성, but 실제 `<style>` 태그가 저 위치에 생성 X
- 내부적으로 처리해서 `<head>` 태그 내부에 작성 CSS 코드 삽입