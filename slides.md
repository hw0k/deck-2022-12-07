---
theme: 'eloc'
fonts:
  sans: '-apple-system'
  mono: 'D2Coding'
layout: 'center'
class: 'text-center'
---

# 리모트 데이터 상태 관리를 잘 하기 위한 여정

Humanscape 남현욱

---

## 시작하기 전

- 리모트 데이터
- 상태 관리
- 리모트 데이터 상태 관리

---

## 리모트 데이터

- 외부 요소에서 가지고 온 데이터
- 주로 REST API?

---

## 상태 관리

- 사용자 인터페이스의 상태를 관리하는 것
- Form Control, 표시 여부 등 세세한 것 하나하나

---

## 리모트 데이터 상태 관리

- 사용자 인터페이스의 상태를 관리하는 것
    - with 리모트 데이터를 그에 맞추어


---

## 리모트 데이터 상태 관리

- 사용자 인터페이스의 상태를 관리하는 것
    - with 리모트 데이터를 그에 맞추어
- 쉽지 않음

---

## 쉽지 않게 하는 원인 1

- 로딩/에러 상태
- 의존된 리모트 데이터

---

## 쉽지 않게 하는 원인 1

```jsx
if (error) {
  return <Error />;
}
if (loading) {
  return <Spinner />;
}
return <Component />;
```

---

## 쉽지 않게 하는 원인 1

```jsx
<ErrorBoundary>
  <Suspense fallback={<Spinner />}>
    <Component />
  </Suspense>
</ErrorBoundary>
```

---

## 쉽지 않게 하는 원인 1

```jsx
<ErrorBoundary>
  <Suspense fallback={<Spinner />}>
    <Component2 />
  </Suspense>
</ErrorBoundary>

const Component2 = () => (
  <ErrorBoundary>
    <Suspense fallback={<Spinner />}>
      <Component />
    </Suspense>
  </ErrorBoundary>
);

// ...
```

---

## 쉽지 않게 하는 원인 2

- 다른 것을 참조하거나, 같이 보내주거나 하는 행위가 API마다 다를 수 있음
- 같은 소스를 불러올 수 있는 경로가 여러 가지인 경우가 있음

---

## 쉽지 않게 하는 원인 2

```json
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repell",
    "body": "quia et suscipit.."
  },
  {
    "userId": 1,
    "id": 2,
    "title": "qui est esse",
    "body": "est rerum tempore vitae.."
  },
  // ...
]
```

---

## 쉽지 않게 하는 원인 2

```json{3,9}
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repell",
    "body": "quia et suscipit.."
  },
  {
    "userId": 1,
    "id": 2,
    "title": "qui est esse",
    "body": "est rerum tempore vitae.."
  },
  // ...
]
```
---

## 쉽지 않게 하는 원인 2

```json{3,4,5,6}
[
  {
    "user": {
      "id": 1,
      "name": "John Doe"
    },
    "id": 1,
    "title": "sunt aut facere repell",
    "body": "quia et suscipit.."
  },
  // ...
]
```

---

## 쉽지 않게 하는 원인 2

- `GET /me/comments`
- `GET /posts/:postId/comments`

---
class: 'text-center'
---

## 쉽지 않게 하는 원인 3

사용자 경험을 위해 같은 걸 두 번 불러오면<br>불편하기 때문에 <b>캐싱... 앗!</b>

---

## 생각해본 솔루션

- API 형태 같이 설계하기
- 제어해야 할 상태로 보지 않기
- 캐시 정규화

---
class: 'text-center'
---

## API 형태 같이 설계하기

처음부터 사실 <b>같이 설계</b>하면<br>되는 거 아닌가요?

---

## 제어해야 할 상태로 보지 않기

- [TanStack Query](https://tanstack.com/query/v4)
- [SWR](https://swr.vercel.app/ko)
- Just 알아서 해주세요

---

## 캐시 정규화

- [normalizr](https://github.com/paularmstrong/normalizr)

---

## Q&A
