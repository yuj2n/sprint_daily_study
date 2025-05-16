# 📝정리 내용

- React로 데이터 다루기

## 💡 처음 알게 된 사실

### `map`으로 렌더링

```jsx
import items from './pokemons';

function Pokemon({ item }) {
  return (
    <div>No.{item.id} {item.name}</div>
  );
}

function App() {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>
          <Pokemon item={item} />
        </li>
      ))}
    </ul>
  );
}
 
export default App;
```

- 반드시 JSX의 중괄호 안에 `map` 함수 사용해야하는 것은 X

### `Sort`로 정렬

```jsx
import { useState } from 'react';
import items from './pokemons';

function Pokemon({ item }) {
  return (
    <div>No.{item.id} {item.name}</div>
  );
}

function App() {
  const [direction, setDirection] = useState(1);
  const handleAscClick = () => setDirection(1);
  const handleDescClick = () => setDirection(-1);
  const sortedItems = items.sort((a, b) => direction * (a.id - b.id));

  return (
    <div>
      <div>
        <button onClick={handleAscClick}>도감번호 순서대로</button>
        <button onClick={handleDescClick}>도감번호 반대로</button>
      </div>
      <ul>
        {sortedItems.map((item) => (
          <li key={item.id}>
            <Pokemon item={item} />
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```

- id 순서대로 / 반대로 정렬

### `filter`로 삭제

```jsx
import { useState } from 'react';
import mockItems from './pokemons';

function Pokemon({ item, onDelete }) {
  const handleDeleteClick = () => onDelete(item.id);

  return (
    <div>
       No.{item.id} {item.name}
      <button onClick={handleDeleteClick}>삭제</button>
    </div>
  );
}

function App() {
  const [items, setItems] = useState(mockItems);

  const handleDelete = (id) => {
    const nextItems = items.filter((item) => item.id !== id);
    setItems(nextItems);
  };

  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>
          <Pokemon item={item} onDelete={handleDelete} />
        </li>
      ))}
    </ul>
  );
}

export default App;
```

- 삭제 기능: `filter`와 배열형 `state` 활용

### Key를 내려주자

- 각 요소 렌더링 시 key Prop을 내려줘야 함!

```jsx
import items from './pokemons';

function Pokemon({ item }) {
  return (
    <div>No.{item.id} {item.name}</div>
  );
}

function App() {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.name}>
          <Pokemon item={item} />
        </li>
      ))}
    </ul>
  );
}

export default App;
```

- 가장 바깥쪽 최상위 태그에 key Prop 지정
- 반드시 id일 필요없이 고유한 값이면 가능(ex. 포켓몬 이름)

## 📌 기억할 것

### 단축키

| 멀티 커서 선택하기 | Ctrl + Shift + L |
| --- | --- |
| 직접 멀티 커서 만들기 | Alt + 클릭 |
| 찾아 바꾸기 | F2 |
| 해당 파일 이동 | Ctrl + 클릭 |
| 줄 이동 | Alt + ⬆⬇ |
| 줄 복사 | Alt + Shift + ⬆⬇ |