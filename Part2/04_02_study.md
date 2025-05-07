# 📝정리 내용

- React로 데이터 다루기

## 💡 처음 알게 된 사실

### **콜백으로 초깃값 지정하기**

```jsx
function ReviewForm() {
  const [values, setValues] = useState(() => {
    const savedValues = getSavedValues(); // 처음 렌더링할 때만 실행됨
    return savedValues
  });
  // ...
}
```

- 콜백 형태로 초깃값을 지정해주면 처음 렌더링 시 한 번만 콜백을 실행해 초깃값 생성 → 불필요한 `getSavedValues` 실행 X
- 콜백 함수의 실행이 오래 걸릴 수록 초기 렌더링 길어짐

## 📌 기억할 것

### **참조형 State 사용의 올바른 예**

```jsx
const [count, setCount] = useState(0);

const handleAddClick = async () => {
  await addCount();
  setCount((prevCount) => prevCount + 1);
}
```

```jsx
const [state, setState] = useState({ count: 0 });

const handleAddClick = () => {
  setState({ ...state, count: state.count + 1 }); // 새로운 객체 생성
}
```