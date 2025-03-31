# 📝정리 내용

- React 웹 개발 시작하기

## 💡 처음 알게 된 사실

### 꿀팁

- F2키 누르고 값 수정 시 해당 파일 내 동일 값 전부 수정
- State Lifting: 자식 컴포넌트 State를 부모 컴포넌트로 올려주는 것
- 각 컴포넌트의 state를 한 곳에서 관리하려면 State Lifting 후 props로 내려주기 ㄱㄴ

## 📌 기억할 것

### State

- 상태 변경 시 화면 그려내는 동작

```jsx
import { useState } from 'react';
// ...
  const [num, setNum] = useState(1);
// ...
```

- num: state의 이름
- setNum: 값 변경

### 참조형 State

JS의 자료형

- 기본형
- 참조형

```jsx
// ... 
  const [gameHistory, setGameHistory] = useState([]);

  const handleRollClick = () => {
    const nextNum = random(6);
    gameHistory.push(nextNum);
    setGameHistory(gameHistory); // state가 제대로 변경되지 않는다!
  };

// ...
```

- `gameHistory` state는 배열 값 자체 X, 그 배열의 주솟값을 참조

**→** 값 변경 O, 주솟값 변경 X 

**→** 참조 주솟값이 동일하므로 상태 변화없다고 판단

⇒ 참조형 `state` 활용 시 반드시 새 참조형 값 생성해 `state` 변경

### Spread 문법(…)

```jsx
// ... 

  const [gameHistory, setGameHistory] = useState([]);

  const handleRollClick = () => {
    const nextNum = random(6);
    setGameHistory([...gameHistory, nextNum]); // state가 제대로 변경된다!
  };

// ...
```