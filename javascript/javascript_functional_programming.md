# 자바스크립트 함수형 프로그래밍 (리액트 필수)

## 1. 불변성 (Immutability)

### 원시 타입과 참조 타입

```javascript
// 원시 타입: 불변
let a = 5;
let b = a;
b = 10;
console.log(a);  // 5 (a는 변하지 않음)

// 참조 타입: 가변
let obj1 = {value: 5};
let obj2 = obj1;
obj2.value = 10;
console.log(obj1.value);  // 10 (obj1도 변함)
```

### 객체의 불변성 유지

```javascript
// 잘못된 방식: 원본 수정
const user = {name: "John", age: 25};
user.age = 26;
console.log(user);  // {name: "John", age: 26} - 원본 수정됨

// 올바른 방식 1: 새 객체 생성
const updated1 = {...user, age: 26};
console.log(user);      // {name: "John", age: 25} - 원본 유지
console.log(updated1);  // {name: "John", age: 26}

// 올바른 방식 2: Object.assign
const updated2 = Object.assign({}, user, {age: 26});
console.log(user);      // {name: "John", age: 25} - 원본 유지
console.log(updated2);  // {name: "John", age: 26}
```

### 배열의 불변성 유지

```javascript
// 잘못된 방식: 배열 수정
const arr = [1, 2, 3];
arr.push(4);
console.log(arr);  // [1, 2, 3, 4] - 원본 수정됨

// 올바른 방식 1: spread 연산자
const arr1 = [1, 2, 3];
const added = [...arr1, 4];
console.log(arr1);    // [1, 2, 3] - 원본 유지
console.log(added);   // [1, 2, 3, 4]

// 올바른 방식 2: concat
const arr2 = [1, 2, 3];
const added2 = arr2.concat(4);
console.log(arr2);     // [1, 2, 3] - 원본 유지
console.log(added2);   // [1, 2, 3, 4]

// 올바른 방식 3: slice + concat
const arr3 = [1, 2, 3];
const added3 = [...arr3.slice(0, 2), 2.5, ...arr3.slice(2)];
console.log(added3);   // [1, 2, 2.5, 3]
```

### 중첩 객체의 불변성

```javascript
const user = {
  name: "John",
  address: {
    city: "Seoul",
    zip: "12345"
  }
};

// 잘못된 방식: 얕은 복사로 중첩 객체는 여전히 참조
const shallow = {...user};
shallow.address.city = "Busan";
console.log(user.address.city);      // "Busan" (원본도 수정됨)

// 올바른 방식: 깊은 복사
const deep = {
  ...user,
  address: {...user.address, city: "Busan"}
};
console.log(user.address.city);      // "Seoul" (원본 유지)
console.log(deep.address.city);      // "Busan"
```

### 리액트에서의 불변성

```javascript
// useState에서 상태 업데이트 (불변성 준수)
const [user, setUser] = useState({name: "John", age: 25});

// 잘못된 방식
const handleChangeAge = () => {
  user.age = 26;
  setUser(user);  // React가 변화를 감지하지 못함
};

// 올바른 방식
const handleChangeAge = () => {
  setUser({...user, age: 26});  // 새 객체 생성
};

// 중첩 객체 업데이트
const [form, setForm] = useState({
  user: {name: "John", age: 25},
  contact: {email: "john@example.com"}
});

const handleChangeName = (newName) => {
  setForm({
    ...form,
    user: {...form.user, name: newName}
  });
};

// 배열 상태 업데이트
const [items, setItems] = useState([1, 2, 3]);

const addItem = () => {
  setItems([...items, 4]);  // 새 배열 생성
};

const removeItem = (index) => {
  setItems(items.filter((_, i) => i !== index));
};

const updateItem = (index, newValue) => {
  setItems(items.map((item, i) => i === index ? newValue : item));
};
```

---

## 2. 순수 함수 (Pure Functions)

### 순수 함수의 특징

```javascript
// 순수 함수: 같은 입력 → 항상 같은 출력, 부작용 없음
function add(a, b) {
  return a + b;
}

add(2, 3);  // 5
add(2, 3);  // 5 (항상 같은 결과)

// 비순수 함수: 외부 상태 의존
let globalCount = 0;

function increment() {
  globalCount++;  // 외부 상태 변경
  return globalCount;
}

increment();  // 1
increment();  // 2 (같은 호출도 다른 결과)

// 비순수 함수: 부작용 있음
function saveUser(user) {
  console.log("Saving...");  // 부작용
  API.post("/users", user);  // 부작용
  return user;
}
```

### 순수 함수 작성

```javascript
// 나쁜 예: 원본 수정
function addToCart(cart, item) {
  cart.items.push(item);  // 원본 수정
  cart.total += item.price;
  return cart;
}

// 좋은 예: 새 객체 반환
function addToCart(cart, item) {
  return {
    items: [...cart.items, item],
    total: cart.total + item.price
  };
}

// 사용
const cart = {items: [], total: 0};
const updatedCart = addToCart(cart, {id: 1, price: 10000});
console.log(cart);         // {items: [], total: 0} - 원본 유지
console.log(updatedCart);  // {items: [...], total: 10000}
```

### 리액트 컴포넌트는 순수 함수여야 함

```javascript
// 순수 함수 컴포넌트
function UserCard({user}) {
  return <div>{user.name}</div>;
}

// 비순수 함수 컴포넌트 (부작용)
function BadUserCard({user}) {
  localStorage.setItem("lastUser", user.id);  // 부작용
  console.log("Component rendered");          // 부작용
  return <div>{user.name}</div>;
}

// 부작용은 useEffect에서 처리
function GoodUserCard({user}) {
  useEffect(() => {
    localStorage.setItem("lastUser", user.id);
  }, [user.id]);

  return <div>{user.name}</div>;
}
```

---

## 3. 일급 객체로서의 함수 (First-Class Functions)

### 함수를 변수에 할당

```javascript
const greet = function(name) {
  return `Hello, ${name}`;
};

console.log(greet("John"));  // Hello, John

const sayHello = greet;
console.log(sayHello("Jane"));  // Hello, Jane
```

### 함수를 인수로 전달

```javascript
function processArray(arr, callback) {
  return arr.map(callback);
}

const numbers = [1, 2, 3];
const doubled = processArray(numbers, x => x * 2);
console.log(doubled);  // [2, 4, 6]

// 여러 콜백
function filter(arr, predicate) {
  return arr.filter(predicate);
}

const evens = filter(numbers, x => x % 2 === 0);
console.log(evens);  // [2]
```

### 함수를 반환

```javascript
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

### 리액트에서의 활용

```javascript
// 고차 컴포넌트 (HOC)
function withDataFetching(url) {
  return function Component(props) {
    const [data, setData] = useState(null);

    useEffect(() => {
      fetch(url)
        .then(r => r.json())
        .then(setData);
    }, []);

    return <div>{data && <p>{data.name}</p>}</div>;
  };
}

const UserComponent = withDataFetching("/api/user");

// Custom Hook
function useAsync(asyncFunction, immediate = true) {
  const [status, setStatus] = useState(immediate ? "pending" : "idle");
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    if (!immediate) return;

    asyncFunction()
      .then(data => {setStatus("success"); setData(data);})
      .catch(error => {setStatus("error"); setError(error);});
  }, [immediate, asyncFunction]);

  return {status, data, error};
}
```

---

## 4. 함수 합성 (Function Composition)

### 함수 조합하기

```javascript
// 개별 함수
const addOne = x => x + 1;
const double = x => x * 2;
const square = x => x * x;

// 함수 합성
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);
const pipe = (...fns) => x => fns.reduce((v, f) => f(v), x);

// 합성 (오른쪽에서 왼쪽으로)
const composed = compose(square, double, addOne);
console.log(composed(5));  // ((5 + 1) * 2) ^ 2 = 144

// 파이프 (왼쪽에서 오른쪽으로)
const piped = pipe(addOne, double, square);
console.log(piped(5));     // ((5 + 1) * 2) ^ 2 = 144
```

### 실용적 예제

```javascript
// 데이터 변환 파이프라인
const users = [
  {id: 1, name: "John", age: 25},
  {id: 2, name: "Jane", age: 30},
  {id: 3, name: "Bob", age: 20}
];

const filterAdults = users => users.filter(u => u.age >= 25);
const mapNames = users => users.map(u => u.name);
const toUpperCase = names => names.map(n => n.toUpperCase());

const pipe = (...fns) => x => fns.reduce((v, f) => f(v), x);
const getAdultNames = pipe(filterAdults, mapNames, toUpperCase);

console.log(getAdultNames(users));  // ["JOHN", "JANE"]
```

---

## 5. 커링 (Currying)

### 커링 개념

```javascript
// 일반 함수
function add(a, b, c) {
  return a + b + c;
}

console.log(add(1, 2, 3));  // 6

// 커링된 함수
function curryAdd(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}

console.log(curryAdd(1)(2)(3));  // 6

// 화살표 함수로
const curryAdd2 = a => b => c => a + b + c;
console.log(curryAdd2(1)(2)(3));  // 6
```

### 커링의 실제 활용

```javascript
// 이벤트 핸들러 생성
const handleClick = (eventType) => (id) => {
  console.log(`${eventType} event on item ${id}`);
};

const handleDelete = handleClick("delete");
const handleEdit = handleClick("edit");

handleDelete(1);  // delete event on item 1
handleEdit(2);    // edit event on item 2

// API 호출 빌더
const apiCall = (method) => (endpoint) => (data) => {
  return fetch(endpoint, {
    method,
    body: JSON.stringify(data)
  }).then(r => r.json());
};

const post = apiCall("POST");
const createUser = post("/users");

createUser({name: "John"});  // POST /users
```

### 리액트에서의 활용

```javascript
// 이벤트 핸들러 생성
function ItemList({items}) {
  const handleDelete = (id) => () => {
    console.log("Delete item", id);
  };

  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>
          {item.name}
          <button onClick={handleDelete(item.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}

// API 호출
const fetchData = (url) => (options) => {
  return fetch(url, options).then(r => r.json());
};

const apiClient = {
  getUser: fetchData("/users"),
  getPost: fetchData("/posts")
};

// 사용
useEffect(() => {
  apiClient.getUser({method: "GET"})
    .then(user => setUser(user));
}, []);
```

---

## 6. 메모이제이션 (Memoization)

### 기본 메모이제이션

```javascript
// 비용이 큰 함수
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

console.time("fibonacci");
fibonacci(40);  // 매우 느림
console.timeEnd("fibonacci");

// 메모이제이션
function memoize(fn) {
  const cache = {};
  return function(...args) {
    const key = JSON.stringify(args);
    if (key in cache) {
      console.log("From cache");
      return cache[key];
    }
    console.log("Computing");
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}

const memoFibonacci = memoize(fibonacci);
console.time("memoized");
memoFibonacci(40);  // Computing... (한 번만 계산)
memoFibonacci(40);  // From cache (캐시에서)
console.timeEnd("memoized");  // 훨씬 빠름
```

### React.memo

```javascript
// Props가 변하지 않으면 리렌더링 스킵
const UserCard = React.memo(({user}) => {
  console.log("UserCard rendered");
  return <div>{user.name}</div>;
});

function App() {
  const [count, setCount] = useState(0);
  const user = {name: "John"};

  return (
    <div>
      <UserCard user={user} />
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
    </div>
  );
}

// 클릭할 때마다 count가 변하지만
// user가 같으면 UserCard는 리렌더링되지 않음
// (매번 새 user 객체가 생성되는 경우)

// 올바른 사용: useMemo
function App() {
  const [count, setCount] = useState(0);
  const user = useMemo(() => ({name: "John"}), []);  // user를 메모이즈

  return (
    <div>
      <UserCard user={user} />
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
    </div>
  );
}
```

### useCallback

```javascript
function Parent() {
  const [count, setCount] = useState(0);

  // 매번 새로운 함수 생성 (자식 컴포넌트가 리렌더링됨)
  const handleClick = () => {
    console.log("Clicked");
  };

  // useCallback으로 함수 메모이즈
  const memoizedHandleClick = useCallback(() => {
    console.log("Clicked");
  }, []);  // 의존성 배열

  return (
    <div>
      <Child onClick={memoizedHandleClick} />
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
    </div>
  );
}

const Child = React.memo(({onClick}) => {
  console.log("Child rendered");
  return <button onClick={onClick}>Click Me</button>;
});
```

---

## 7. 부분 적용 (Partial Application)

### 부분 적용의 개념

```javascript
function add(a, b, c) {
  return a + b + c;
}

// 부분 적용: 일부 인수를 고정
function partial(fn, ...args) {
  return function(...nextArgs) {
    return fn(...args, ...nextArgs);
  };
}

const addOne = partial(add, 1);
console.log(addOne(2, 3));  // 1 + 2 + 3 = 6

const addOneTwo = partial(add, 1, 2);
console.log(addOneTwo(3));  // 1 + 2 + 3 = 6
```

### 실제 활용

```javascript
// API 요청 래퍼
const fetchData = (baseUrl, endpoint, options) => {
  return fetch(`${baseUrl}${endpoint}`, options)
    .then(r => r.json());
};

const apiClient = (baseUrl) => (endpoint) => (options) => {
  return fetchData(baseUrl, endpoint, options);
};

const myApi = apiClient("https://api.example.com");
const getUsers = myApi("/users");
const deleteUsers = myApi("/users");

// 사용
getUsers({method: "GET"});
deleteUsers({method: "DELETE"});
```

---

## 8. 지연 평가 (Lazy Evaluation)

### 필요할 때까지 계산 미루기

```javascript
// 즉시 평가
const numbers = [1, 2, 3, 4, 5];
const result = numbers
  .map(n => n * 2)
  .filter(n => n > 5)
  .reduce((acc, n) => acc + n, 0);

// 중간 배열들이 생성됨

// 지연 평가 (Generator 사용)
function* lazyMap(arr, fn) {
  for (const item of arr) {
    yield fn(item);
  }
}

function* lazyFilter(gen, predicate) {
  for (const item of gen) {
    if (predicate(item)) yield item;
  }
}

const gen = lazyFilter(
  lazyMap([1, 2, 3, 4, 5], n => n * 2),
  n => n > 5
);

for (const value of gen) {
  console.log(value);  // 12, 14
}

// 중간 배열 생성 안 함 (메모리 효율적)
```

---

## 요약 테이블

| 개념 | 설명 | 사용 빈도 |
|------|------|---------|
| 불변성 | 상태 수정 최소화 | ⭐⭐⭐⭐⭐ |
| 순수 함수 | 부작용 제거 | ⭐⭐⭐⭐⭐ |
| 일급 함수 | 함수를 값처럼 다루기 | ⭐⭐⭐⭐⭐ |
| 함수 합성 | 함수 조합 | ⭐⭐⭐⭐ |
| 커링 | 부분 적용 | ⭐⭐⭐ |
| 메모이제이션 | 성능 최적화 | ⭐⭐⭐⭐ |
| 부분 적용 | 함수 정의 간소화 | ⭐⭐⭐ |
| 지연 평가 | 메모리 효율화 | ⭐⭐ |

