# 📝정리 내용

- Styled-Components

## 💡 처음 알게 된 사실

### 태그 함수

1. 템플릿 리터럴 문법으로 실행 가능한 함수
- `strings`에는 입력한 문자열이 배열로 나옴. `values` 는 빈 배열로 출력

```jsx
function h1(strings, ...values) {
  return [strings, values];
}
const result = h1`color: pink;`;
console.log(result); // [['color: pink;'], []]
```

1. 템플릿 리터럴에 값 삽입
- `strings`에 값 삽입 앞뒤의 문자열이 잘려 배열로 들어감. `values`삽입 값이 배열로 들어감

```jsx
function h1(strings, ...values) {
  return [strings, values];
}
const backgroundColor = 'black';
const result2 = h1`
  background-color: ${backgroundColor};
  color: pink;
`;
console.log(result2);
// [['\n  background-color: ', ';\n  color: pink;\n'], ['black']]
```

```jsx
function h1(strings, ...values) {
  // React 컴포넌트를 만든다
  function Component({ children, ...props }) {
    // 템플릿 리터럴에서 받은 값을 CSS 코드로 만든다
    let style = '';
    for (let i = 0; i < strings.length; ++i) {
      style += strings[i];
      // 삽입된 값이 함수이면 props를 가지고 실행한 값을 CSS에 넣는다.
      if (typeof values[i] === 'function') {
        const fn = values[i];
        style += fn(props);

        // 그 외에 값이 존재하면 CSS에 문자열로 넣는다.
      } else if (values[i]) {
        style += values[i];
      }
    }

    // CSS 코드에 따라 클래스 이름을 만든다
    const className = `my-sc-${style.length}`;

    // `<style>` 태그로 만든 CSS 코드를 렌더링한다
    return (
      <>
        <style>{`.${className} {${style}}`}</style>
        <h1 className={className}>{children}</h1>
      </>
    );
  }
  return Component;
}

const backgroundColor = 'black';
const StyledH1 = h1`
  color: pink;
  ${({ dark }) => dark && 'background-color: black;'}
`;

function App() {
  return <StyledH1 dark>Hello World</StyledH1>;
}

export default App;
```

1. 템플릿 리터럴로 태그 함수 `h1` 실행 → `StyledH1`컴포넌트 생성
2. `App` 컴포넌트 렌더링 시 `StyledH1` 컴포넌트도 렌더링
3. `StyledH1` 컴포넌트에서 CSS 코드 생성 후 `<style>` 태그로 넣음. 이때 함수로 삽입된 값(`${({ dark }) => dark && 'background-color: black;'}` 부분)은 함수 → Props를 가지고 실행해 CSS로 생성. 우리 코드에서는 `dark` 라는 값이 있기 때문에, CSS에는 `background-color: black;` 이라는 값으로 반영된다.

⇒ 실제 출력!!

```jsx
<style>
  .my-sc-60 { color: pink; background-color: black; }
</style>
<h1 class="my-sc-60">Hello</h1>
```