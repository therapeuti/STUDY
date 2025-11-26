# 자바스크립트 ES6+ 핵심 기능 (리액트 필수)

## 1. 화살표 함수 (Arrow Functions)

### 기본 문법

```javascript
// 기존 함수
function add(a, b) {
  return a + b;
}

// 화살표 함수
const add = (a, b) => {
  return a + b;
};

// 축약형 (한 줄 반환)
const add = (a, b) => a + b;

// 매개변수 하나일 때 괄호 생략
const square = x => x * x;

// 매개변수 없을 때
const greet = () => "Hello";
```

### this 바인딩

```javascript
// 화살표 함수는 자신의 this를 가지지 않음
const user = {
  name: "John",
  friends: ["Jane", "Bob"],
  listFriends: function() {
    this.friends.forEach(friend => {
      console.log(`${this.name}'s friend: ${friend}`);
      // this가 user를 가리킴
    });
  }
};

user.listFriends();
// John's friend: Jane
// John's friend: Bob
```

### 리액트에서의 사용

```javascript
// 이벤트 핸들러
const handleClick = () => {
  console.log("clicked");
};

// map에서 많이 사용
const numbers = [1, 2, 3];
const doubled = numbers.map(n => n * 2);

// 콜백 함수
setTimeout(() => {
  console.log("after 1 second");
}, 1000);
```

---

## 2. let과 const (변수 선언)

### var의 문제점과 let/const의 해결책

```javascript
// var의 문제: 함수 스코프, 호이스팅 문제
var x = 1;
if (true) {
  var x = 2;
}
console.log(x);  // 2 (블록 스코프 무시됨)

// let: 블록 스코프, 재할당 가능
let y = 1;
if (true) {
  let y = 2;
}
console.log(y);  // 1 (블록 스코프 유지)

// const: 블록 스코프, 재할당 불가능
const z = 1;
// z = 2;  // Error: Assignment to constant variable

// 객체/배열은 내용 수정 가능 (참조는 불변)
const user = {name: "John"};
user.name = "Jane";  // OK
user = {};           // Error
```

### 리액트에서의 사용

```javascript
// 리액트에서는 const를 기본으로 사용
const MyComponent = () => {
  const [count, setCount] = useState(0);
  const handleClick = () => setCount(count + 1);

  return <button onClick={handleClick}>{count}</button>;
};

// let은 변수값이 변할 때만 사용
let index = 0;
while (index < 10) {
  console.log(index);
  index++;
}
```

---

## 3. 템플릿 리터럴 (Template Literals)

### 기본 문법

```javascript
const name = "John";
const age = 25;

// 기존 문자열 연결
console.log("Hello " + name + ", you are " + age + " years old");

// 템플릿 리터럴
console.log(`Hello ${name}, you are ${age} years old`);
```

### 표현식 포함

```javascript
const a = 10;
const b = 20;

console.log(`${a} + ${b} = ${a + b}`);
console.log(`Is ${a > b} true?`);
console.log(`Function call: ${(() => "result")()}`);
```

### 여러 줄 문자열

```javascript
const html = `
  <div>
    <h1>Hello World</h1>
    <p>This is a template literal</p>
  </div>
`;

console.log(html);
```

### 리액트에서의 사용

```javascript
// 동적 클래스명
const className = `btn btn-${isActive ? 'active' : 'inactive'}`;

// 스타일 객체
const styles = {
  color: "red",
  fontSize: `${size}px`
};

// JSX에서
<div className={`container ${isOpen ? 'open' : 'closed'}`}>
  Content
</div>
```

---

## 4. 디스트럭처링 (Destructuring)

### 배열 디스트럭처링

```javascript
// 기존 방식
const arr = [1, 2, 3, 4, 5];
const first = arr[0];
const second = arr[1];

// 디스트럭처링
const [first, second] = [1, 2, 3, 4, 5];
console.log(first, second);  // 1, 2

// 건너뛰기
const [a, , c] = [1, 2, 3];
console.log(a, c);  // 1, 3

// 나머지 요소
const [x, ...rest] = [1, 2, 3, 4, 5];
console.log(x);     // 1
console.log(rest);  // [2, 3, 4, 5]

// 기본값
const [name = "Guest", role = "user"] = ["John"];
console.log(name, role);  // John, user
```

### 객체 디스트럭처링

```javascript
const user = {
  id: 1,
  name: "John",
  email: "john@example.com",
  age: 25
};

// 기본
const {name, email} = user;
console.log(name, email);  // John, john@example.com

// 변수명 변경
const {name: userName, email: userEmail} = user;
console.log(userName, userEmail);

// 기본값
const {name, phone = "000-0000", address = "Unknown"} = user;
console.log(phone, address);  // 000-0000, Unknown

// 중첩 디스트럭처링
const user2 = {
  id: 1,
  name: "John",
  address: {
    city: "Seoul",
    zip: "12345"
  }
};

const {address: {city, zip}} = user2;
console.log(city, zip);  // Seoul, 12345

// 나머지 속성
const {name, ...rest} = user;
console.log(rest);
// {id: 1, email: 'john@example.com', age: 25}
```

### 리액트에서의 사용

```javascript
// Props 디스트럭처링
function UserCard({name, email, age}) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{email}</p>
      <p>{age}</p>
    </div>
  );
}

// useState 디스트럭처링
const [count, setCount] = useState(0);

// API 응답
const {data, error, loading} = fetchUser();

// 함수 매개변수
const handleChange = ({target: {value}}) => {
  console.log(value);
};
```

---

## 5. 기본 매개변수 (Default Parameters)

### 기본 문법

```javascript
// 기존 방식
function greet(name) {
  name = name || "Guest";
  console.log(`Hello ${name}`);
}

// 기본 매개변수
function greet(name = "Guest") {
  console.log(`Hello ${name}`);
}

greet();           // Hello Guest
greet("John");     // Hello John
```

### 고급 예제

```javascript
// 객체 기본값
function createUser({name = "Guest", age = 18, role = "user"} = {}) {
  return {name, age, role};
}

createUser();                    // {name: 'Guest', age: 18, role: 'user'}
createUser({name: "John"});      // {name: 'John', age: 18, role: 'user'}
createUser({name: "John", age: 25}); // {name: 'John', age: 25, role: 'user'}

// 동적 기본값
function asyncAction(data, callback = () => {}) {
  callback(data);
}
```

### 리액트에서의 사용

```javascript
// Props에 기본값
function Button({label = "Click me", onClick = () => {}, disabled = false}) {
  return (
    <button disabled={disabled} onClick={onClick}>
      {label}
    </button>
  );
}

// useEffect 기본값
function useFetch(url, options = {}) {
  const {method = "GET", headers = {}} = options;
  // ...
}
```

---

## 6. 전개 연산자 (Spread Operator)

### 배열 전개

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// 배열 결합
const combined = [...arr1, ...arr2];
console.log(combined);  // [1, 2, 3, 4, 5, 6]

// 배열 복사
const copy = [...arr1];
console.log(copy);  // [1, 2, 3]

// 요소 추가
const withNew = [0, ...arr1, 3.5, ...arr2, 7];
console.log(withNew);  // [0, 1, 2, 3, 3.5, 4, 5, 6, 7]

// 함수 인자로 사용
const sum = (a, b, c) => a + b + c;
console.log(sum(...arr1));  // 6
```

### 객체 전개

```javascript
const user = {id: 1, name: "John"};
const address = {city: "Seoul", zip: "12345"};

// 객체 병합
const merged = {...user, ...address};
console.log(merged);
// {id: 1, name: 'John', city: 'Seoul', zip: '12345'}

// 속성 추가/덮어쓰기
const updated = {...user, age: 25, name: "Jane"};
console.log(updated);
// {id: 1, name: 'Jane', age: 25}

// 나머지는 제거
const {id, ...rest} = user;
console.log(rest);  // {name: 'John'}
```

### 리액트에서의 사용

```javascript
// Props 전달
<UserCard {...user} />

// 상태 업데이트
const [user, setUser] = useState({name: "John", age: 25});

// 1. 속성 추가
setUser({...user, age: 26});

// 2. 중첩 객체 업데이트
const [form, setForm] = useState({
  user: {name: "John", age: 25},
  contact: {email: "john@example.com"}
});

setForm({
  ...form,
  user: {...form.user, age: 26}
});

// 3. 배열 업데이트
const [items, setItems] = useState([1, 2, 3]);
setItems([...items, 4, 5]);
```

---

## 7. 고차 함수 (Higher-Order Functions)

### 함수를 반환하는 함수

```javascript
// 커링 (Currying)
function multiply(a) {
  return function(b) {
    return a * b;
  };
}

const double = multiply(2);
console.log(double(5));  // 10
console.log(double(10)); // 20

// 화살표 함수로
const multiply2 = a => b => a * b;
const triple = multiply2(3);
console.log(triple(5));  // 15
```

### 함수를 매개변수로 받는 함수

```javascript
// 콜백 함수
function processArray(arr, callback) {
  return arr.map(callback);
}

const numbers = [1, 2, 3];
const doubled = processArray(numbers, n => n * 2);
console.log(doubled);  // [2, 4, 6]

// 함수형 프로그래밍
const compose = (f, g) => x => f(g(x));
const addOne = x => x + 1;
const double = x => x * 2;
const addOneThenDouble = compose(double, addOne);
console.log(addOneThenDouble(5));  // (5 + 1) * 2 = 12
```

### 리액트에서의 사용

```javascript
// HOC (Higher-Order Component)
function withLogger(Component) {
  return (props) => {
    useEffect(() => {
      console.log("Component mounted:", Component.name);
      return () => console.log("Component unmounted");
    }, []);
    return <Component {...props} />;
  };
}

const EnhancedComponent = withLogger(MyComponent);

// Custom Hook (고차 함수)
function useAsync(asyncFunction) {
  const [status, setStatus] = useState("idle");
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    asyncFunction().then(
      result => {setStatus("success"); setData(result);},
      error => {setStatus("error"); setError(error);}
    );
  }, []);

  return {status, data, error};
}
```

---

## 8. 클로저 (Closures)

### 클로저 개념

```javascript
// 클로저: 함수가 자신의 스코프 밖의 변수에 접근
function outer(x) {
  return function inner(y) {
    return x + y;  // x는 outer의 변수
  };
}

const addFive = outer(5);
console.log(addFive(3));   // 8
console.log(addFive(10));  // 15
```

### 비공개 변수 생성

```javascript
function createCounter() {
  let count = 0;  // 비공개 변수

  return {
    increment() {
      return ++count;
    },
    decrement() {
      return --count;
    },
    getCount() {
      return count;
    }
  };
}

const counter = createCounter();
console.log(counter.increment());  // 1
console.log(counter.increment());  // 2
console.log(counter.decrement());  // 1
console.log(counter.count);        // undefined (접근 불가)
```

### 리액트에서의 사용

```javascript
// useState의 내부 구현 (클로저 활용)
function useState(initialValue) {
  let state = initialValue;

  const setState = (newValue) => {
    state = newValue;
    reRender();
  };

  return [state, setState];
}

// Custom Hook
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    const item = window.localStorage.getItem(key);
    return item ? JSON.parse(item) : initialValue;
  });

  const setValue = (value) => {
    const valueToStore = value instanceof Function ? value(storedValue) : value;
    setStoredValue(valueToStore);
    window.localStorage.setItem(key, JSON.stringify(valueToStore));
  };

  return [storedValue, setValue];
}
```

---

## 9. Promise와 비동기 처리

### Promise 기본

```javascript
// Promise 생성
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success!");
  }, 1000);
});

// Promise 사용
myPromise
  .then(result => console.log(result))
  .catch(error => console.error(error));

// Promise 체이닝
fetch("/api/users")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

### 여러 Promise 다루기

```javascript
// Promise.all(): 모든 Promise가 완료될 때까지 대기
Promise.all([
  fetch("/api/users"),
  fetch("/api/posts"),
  fetch("/api/comments")
])
.then(([usersRes, postsRes, commentsRes]) => {
  return Promise.all([
    usersRes.json(),
    postsRes.json(),
    commentsRes.json()
  ]);
})
.then(([users, posts, comments]) => {
  console.log({users, posts, comments});
});

// Promise.race(): 가장 먼저 완료되는 Promise 반환
Promise.race([
  fetch("/api/fast"),
  fetch("/api/slow")
]).then(result => console.log("First to complete:", result));
```

### 리액트에서의 사용

```javascript
// useEffect에서 Promise 사용
useEffect(() => {
  fetch("/api/users")
    .then(res => res.json())
    .then(data => setUsers(data))
    .catch(error => setError(error));
}, []);

// 데이터 페칭 HOC
function withDataFetching(url) {
  return (Component) => {
    return (props) => {
      const [data, setData] = useState(null);
      const [loading, setLoading] = useState(true);
      const [error, setError] = useState(null);

      useEffect(() => {
        fetch(url)
          .then(res => res.json())
          .then(data => {
            setData(data);
            setLoading(false);
          })
          .catch(error => {
            setError(error);
            setLoading(false);
          });
      }, []);

      return <Component data={data} loading={loading} error={error} {...props} />;
    };
  };
}
```

---

## 10. async/await (Promise의 문법 설탕)

### 기본 문법

```javascript
// Promise 방식
function fetchUser() {
  return fetch("/api/user")
    .then(res => res.json());
}

// async/await 방식
async function fetchUser() {
  const res = await fetch("/api/user");
  const data = await res.json();
  return data;
}

// 사용
const user = await fetchUser();
console.log(user);
```

### 에러 처리

```javascript
async function fetchUser() {
  try {
    const res = await fetch("/api/user");
    if (!res.ok) throw new Error("Failed to fetch");
    const data = await res.json();
    return data;
  } catch (error) {
    console.error("Error:", error);
    throw error;
  }
}
```

### 여러 비동기 작업

```javascript
// 순차 처리
async function fetchSequential() {
  const users = await fetch("/api/users").then(r => r.json());
  const posts = await fetch("/api/posts").then(r => r.json());
  return {users, posts};
}

// 병렬 처리 (더 빠름)
async function fetchParallel() {
  const [users, posts] = await Promise.all([
    fetch("/api/users").then(r => r.json()),
    fetch("/api/posts").then(r => r.json())
  ]);
  return {users, posts};
}
```

### 리액트에서의 사용

```javascript
// useEffect에서 async/await
useEffect(() => {
  const fetchData = async () => {
    try {
      setLoading(true);
      const response = await fetch("/api/users");
      const data = await response.json();
      setUsers(data);
    } catch (error) {
      setError(error);
    } finally {
      setLoading(false);
    }
  };

  fetchData();
}, []);

// 버튼 클릭 시
const handleSubmit = async (e) => {
  e.preventDefault();
  try {
    setLoading(true);
    const response = await fetch("/api/users", {
      method: "POST",
      headers: {"Content-Type": "application/json"},
      body: JSON.stringify(formData)
    });
    const result = await response.json();
    setUsers([...users, result]);
  } catch (error) {
    setError(error);
  } finally {
    setLoading(false);
  }
};
```

---

## 11. 조건부 렌더링과 논리 연산자

### && 연산자

```javascript
const isLoggedIn = true;
const user = {name: "John"};

// && 연산자 (왼쪽이 true일 때만 오른쪽 실행)
console.log(isLoggedIn && user.name);  // "John"
console.log(!isLoggedIn && user.name); // false
```

### || 연산자

```javascript
const user = null;
const defaultUser = {name: "Guest"};

// || 연산자 (왼쪽이 false일 때 오른쪽 사용)
const currentUser = user || defaultUser;
console.log(currentUser);  // {name: "Guest"}
```

### ?? 널리시 코얼레싱 (Nullish Coalescing)

```javascript
const value = null;
const value2 = undefined;
const value3 = 0;
const value4 = "";

console.log(value ?? "default");    // "default"
console.log(value3 ?? "default");   // 0 (0은 falsy지만 null/undefined 아님)
console.log(value4 ?? "default");   // "" (빈 문자열도 null/undefined 아님)
```

### 리액트에서의 사용

```javascript
function UserProfile({user, isLoading}) {
  return (
    <div>
      {isLoading && <div>Loading...</div>}
      {!isLoading && user && <h1>{user.name}</h1>}
      {!isLoading && !user && <p>No user found</p>}
    </div>
  );
}

// 더 간단하게
function UserProfile({user = null, isLoading = false}) {
  return (
    <div>
      {isLoading && <div>Loading...</div>}
      {!isLoading && (user ? <h1>{user.name}</h1> : <p>No user</p>)}
    </div>
  );
}
```

---

## 요약 테이블

| 기능 | 설명 | 리액트 사용도 |
|------|------|-------------|
| 화살표 함수 | 짧은 함수 문법, this 바인딩 | ⭐⭐⭐⭐⭐ |
| let/const | 블록 스코프 변수 | ⭐⭐⭐⭐⭐ |
| 템플릿 리터럴 | 문자열 보간 | ⭐⭐⭐⭐ |
| 디스트럭처링 | 객체/배열 분해 | ⭐⭐⭐⭐⭐ |
| 기본 매개변수 | 함수 매개변수 기본값 | ⭐⭐⭐⭐ |
| 전개 연산자 | 배열/객체 펼치기 | ⭐⭐⭐⭐⭐ |
| 고차 함수 | 함수형 프로그래밍 | ⭐⭐⭐⭐ |
| 클로저 | 비공개 상태 | ⭐⭐⭐⭐ |
| Promise | 비동기 처리 | ⭐⭐⭐⭐ |
| async/await | Promise 문법 설탕 | ⭐⭐⭐⭐⭐ |

