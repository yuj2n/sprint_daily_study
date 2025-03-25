# 📝정리 내용

- 자바스크립트로 리퀘 보내기

## 💡 처음 알게 된 사실

### ES 모듈

- import/export와 await을 사용하기 위한 과정

```jsx
// package.json 파일
{
  "type": "module"
}
```

### fetch() 오류 처리

- 오류
    1. URL이나 헤더 정보 오류로 리퀘스트 자체 실패
    2. 리퀘스트는 성공이지만 상태 코드가 실패(4XX, 5XX)
- fetch() 함수는 첫 번째 경우에만 리턴하는 Promise를 reject

→ fetch() 오류 처리 시 Promise의 reject 타이밍과 리스폰스 바디에 돌아오는 내용 생각!

```jsx
export async function getColorSurvey(id) {
  const res = await fetch(`https://learn.codeit.kr/api/color-surveys/${id}`);

  if (!res.ok) {
    throw new Error('데이터를 불러오는데 실패했습니다.');
  }

  const data = await res.json();
  return data;
}
```

- 확실한 오류 처리: 두 번째 경우에도 오류 `throw`

## 📌 기억할 것

### fetch() 기본 문법

```jsx
const res = await fetch('https://learn.codeit.kr/api/color-surveys');
const data = await res.json();
console.log(data); // { count: ... }, {...} ...

// 리스폰스 상태 코드 & 헤더
res.status;
res.headers;

// 리스폰스 바디
await res.json(); // JSON 문자열을 파싱해서 자바스크립트 객체로 변환
await res.text(); // 문자열을 그대로 가져옴
```

### URL 객체

```jsx
const params = { offset: 10, limit: 10 };
const url = new URL('https://learn.codeit.kr/api/color-surveys');
Object.keys(params).forEach((key) => url.searchParams.append(key, params[key]));
const res = await fetch(url);
const data = await res.json();
console.log(data);
```

- 쿼리 파라미터 보낼 때 URL 객체 사용 O

### fetch() 옵션

리퀘 설정 O

- method: `'GET'`, `'POST'`, `'PATCH'`, `'DELETE'` 같은 값으로 설정 O. method 미설정 시 기본 값 `'GET'`
- `header`: 자주 설정하는 헤더는 `'Content-Type': ‘application/json’`
- `body`: JS 객체는 그대로 전달 X → JSON 문자열(`JSON.stringify(data)`)로 변환