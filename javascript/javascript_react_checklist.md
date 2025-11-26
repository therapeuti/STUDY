# 리액트 필수 JavaScript 체크리스트

## ✅ 1. 변수와 함수

### const/let 차이를 설명할 수 있다

#### var의 문제점

```javascript
// 문제 1: 함수 스코프만 인정
function example() {
  if (true) {
    var x = 1;
  }
  console.log(x);  // 1 (블록 스코프 무시)
}

// 문제 2: 호이스팅(Hoisting)
console.log(y);  // undefined (에러 아님)
var y = 2;

// 문제 3: 재선언 가능
var x = 1;
var x = 2;  // 오류 없음 (의도하지 않은 재선언)
```

#### let vs const

```javascript
// let: 블록 스코프, 재할당 가능, 재선언 불가
let name = "John";
if (true) {
  let name = "Jane";
}
console.log(name);  // "John" (블록 스코프 유지)

name = "Bob";       // OK (재할당 가능)
// let name = "Alice";  // Error (재선언 불가)

// const: 블록 스코프, 재할당 불가, 재선언 불가
const age = 25;
// age = 26;  // Error (재할당 불가)
// const age = 30;  // Error (재선언 불가)

// 단, 객체/배열의 내용은 수정 가능 (참조만 고정)
const user = {name: "John"};
user.name = "Jane";  // OK (객체 내용 수정)
user = {};           // Error (참조 변경 불가)
```

#### 리액트에서의 실전

```javascript
// ❌ 나쁜 예: var 사용
var count = 0;
var handleClick = () => count++;

// ✅ 좋은 예: const 기본, let 필요할 때만
const [count, setCount] = useState(0);

const handleClick = () => {
  setCount(count + 1);
};

// let 사용 예: 루프 변수
for (let i = 0; i < 10; i++) {
  console.log(i);
}

// const 사용 예: 상수나 재할당 안 할 데이터
const API_URL = "https://api.example.com";
const handleSubmit = (e) => {
  e.preventDefault();
};
```

#### 핵심 정리

| 특성 | var | let | const |
|------|-----|-----|-------|
| 스코프 | 함수 | 블록 | 블록 |
| 재할당 | O | O | X |
| 재선언 | O | X | X |
| 호이스팅 | O (undefined) | O (TDZ) | O (TDZ) |
| 리액트 추천도 | ❌ | ✅ | ✅✅ |

**리액트에서의 원칙:**
- 기본은 **const** 사용
- 재할당이 필요하면 **let** 사용
- **var는 절대 금지**

---

### 화살표 함수로 함수를 작성할 수 있다

#### 기본 문법

```javascript
// 1. 매개변수 0개
const greet = () => "Hello";
greet();  // "Hello"

// 2. 매개변수 1개 (괄호 생략 가능)
const square = x => x * x;
square(5);  // 25

// 3. 매개변수 2개 이상 (괄호 필수)
const add = (a, b) => a + b;
add(2, 3);  // 5

// 4. 여러 줄 (중괄호와 return 필수)
const multiply = (a, b) => {
  const result = a * b;
  return result;
};
multiply(2, 3);  // 6

// 5. 객체 반환 시 (괄호로 감싸기)
const createUser = (name, age) => ({name, age});
createUser("John", 25);  // {name: "John", age: 25}
```

#### this 바인딩의 중요성

```javascript
// ❌ 일반 함수: this가 window/undefined
const user = {
  name: "John",
  friends: ["Jane", "Bob"],
  // 일반 함수로 정의하면 this 바인딩 문제
  listFriends: function() {
    this.friends.forEach(function(friend) {
      // 이 this는 window 또는 undefined
      console.log(this.name + "'s friend: " + friend);  // 에러
    });
  }
};

// ✅ 화살표 함수: 외부 this를 상속받음
const user = {
  name: "John",
  friends: ["Jane", "Bob"],
  listFriends: function() {
    this.friends.forEach(friend => {
      // 이 this는 user 객체
      console.log(`${this.name}'s friend: ${friend}`);
    });
  }
};
user.listFriends();
// John's friend: Jane
// John's friend: Bob
```

#### 리액트에서의 사용

```javascript
// ✅ 함수형 컴포넌트에서 이벤트 핸들러
function Counter() {
  const [count, setCount] = useState(0);

  // 화살표 함수로 정의하면 this 바인딩 안 함 (함수형이므로 불필요)
  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}

// ✅ map, filter 등에서 콜백 함수
function UserList({users}) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

// ✅ setTimeout, fetch 등에서
useEffect(() => {
  const timer = setTimeout(() => {
    console.log("After 1 second");
  }, 1000);

  return () => clearTimeout(timer);
}, []);

// ✅ 클래스 컴포넌트에서 메서드 정의
class MyComponent extends React.Component {
  handleClick = () => {
    // 화살표 함수로 정의하면 자동 바인딩
    this.setState({count: this.state.count + 1});
  };

  render() {
    return <button onClick={this.handleClick}>Click</button>;
  }
}
```

#### 화살표 함수 사용 시 주의점

```javascript
// ⚠️ 주의 1: 메서드로 정의할 때 this 문제
const obj = {
  name: "John",
  // 화살표 함수로 메서드 정의 → this가 obj를 가리킬 수 없음
  sayName: () => {
    console.log(this.name);  // undefined (this는 window)
  }
};

// ✅ 일반 함수로 정의해야 함
const obj = {
  name: "John",
  sayName: function() {
    console.log(this.name);  // "John"
  }
};

// ⚠️ 주의 2: arguments 객체 사용 불가
const func = () => {
  console.log(arguments);  // Error: arguments is not defined
};

// ✅ rest 파라미터 사용
const func = (...args) => {
  console.log(args);
};
```

---

### 템플릿 리터럴로 문자열을 만들 수 있다

#### 기본 문법

```javascript
const name = "John";
const age = 25;

// ❌ 이전 방식: 문자열 연결
const message = "Hello " + name + ", you are " + age + " years old";

// ✅ 템플릿 리터럴 (백틱 사용)
const message = `Hello ${name}, you are ${age} years old`;
console.log(message);  // Hello John, you are 25 years old
```

#### 표현식 포함

```javascript
const a = 10;
const b = 20;

// 산술 연산
console.log(`${a} + ${b} = ${a + b}`);  // 10 + 20 = 30

// 조건문
const grade = 85;
console.log(`Grade: ${grade >= 80 ? "A" : "B"}`);  // Grade: A

// 함수 호출
const getName = () => "John";
console.log(`Hello, ${getName()}`);  // Hello, John

// 객체 속성 접근
const user = {name: "John", age: 25};
console.log(`${user.name} is ${user.age} years old`);
// John is 25 years old
```

#### 여러 줄 문자열

```javascript
// ❌ 이전 방식: 복잡함
const html = "<div>\n  <h1>Title</h1>\n  <p>Content</p>\n</div>";

// ✅ 템플릿 리터럴: 자연스러움
const html = `
  <div>
    <h1>Title</h1>
    <p>Content</p>
  </div>
`;

const sql = `
  SELECT id, name, email
  FROM users
  WHERE age > ${minAge}
  ORDER BY name
`;
```

#### 리액트에서의 사용

```javascript
// ✅ 동적 className
function Button({isActive, size}) {
  return (
    <button className={`btn btn-${size} ${isActive ? 'active' : ''}`}>
      Click me
    </button>
  );
}

// ✅ 동적 스타일
function Box({color, size}) {
  const styles = {
    color: color,
    fontSize: `${size}px`,
    padding: `${size / 2}px`
  };
  return <div style={styles}>Box</div>;
}

// ✅ 데이터 표시
function UserProfile({user}) {
  return (
    <div>
      <h1>{`${user.firstName} ${user.lastName}`}</h1>
      <p>{`Email: ${user.email}`}</p>
      <p>{`Age: ${user.age} years old`}</p>
    </div>
  );
}

// ✅ 에러 메시지
function FormField({name, value, error}) {
  return (
    <div>
      <label>{name}</label>
      <input value={value} />
      {error && <p style={{color: 'red'}}>{`Error: ${error}`}</p>}
    </div>
  );
}
```

---

## ✅ 2. 구조 분해 (Destructuring)

### 배열 구조 분해로 값을 추출할 수 있다

#### 기본 문법

```javascript
// ❌ 이전 방식
const arr = [1, 2, 3, 4, 5];
const first = arr[0];
const second = arr[1];
const third = arr[2];

// ✅ 구조 분해
const [first, second, third] = [1, 2, 3, 4, 5];
console.log(first, second, third);  // 1, 2, 3
```

#### 부분 추출

```javascript
const colors = ["red", "green", "blue", "yellow"];

// 선택적으로 추출
const [primary, secondary] = colors;
console.log(primary, secondary);  // red, green

// 건너뛰기
const [first, , third] = colors;
console.log(first, third);  // red, blue

// 나머지 요소
const [primary, secondary, ...rest] = colors;
console.log(primary);   // red
console.log(secondary); // green
console.log(rest);      // ["blue", "yellow"]
```

#### 기본값 설정

```javascript
const arr = [1];

// 없는 요소는 undefined
const [a, b, c] = arr;
console.log(a, b, c);  // 1, undefined, undefined

// 기본값 설정
const [x = 10, y = 20, z = 30] = arr;
console.log(x, y, z);  // 1, 20, 30

// 함수 매개변수에서 기본값
const greet = ([name = "Guest", role = "user"]) => {
  return `${name} is a ${role}`;
};

greet(["John"]);           // John is a user
greet(["Jane", "admin"]);  // Jane is admin
```

#### 리액트에서의 사용

```javascript
// ✅ useState 디스트럭처링 (매우 중요!)
function Counter() {
  // 상태 변수 추출
  const [count, setCount] = useState(0);
  const [name, setName] = useState("John");

  return (
    <div>
      <p>Count: {count}</p>
      <p>Name: {name}</p>
    </div>
  );
}

// ✅ 여러 상태를 배열로 관리할 때
function Form() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  // 또는 배열 구조 분해로
  const [inputs, setInputs] = useState(["", "", ""]);
  const [name, email, message] = inputs;
}

// ✅ 배열 props 받기
function ColorPicker({colors}) {
  const [primary, secondary, tertiary] = colors;
  return (
    <div>
      <span style={{color: primary}}>Primary</span>
      <span style={{color: secondary}}>Secondary</span>
      <span style={{color: tertiary}}>Tertiary</span>
    </div>
  );
}

// 사용: <ColorPicker colors={["red", "green", "blue"]} />
```

---

### 객체 구조 분해로 속성을 추출할 수 있다

#### 기본 문법

```javascript
// ❌ 이전 방식
const user = {
  id: 1,
  name: "John",
  email: "john@example.com",
  age: 25
};

const id = user.id;
const name = user.name;
const email = user.email;

// ✅ 구조 분해
const {id, name, email} = user;
console.log(id, name, email);  // 1, John, john@example.com
```

#### 변수명 변경

```javascript
const user = {
  id: 1,
  name: "John",
  email: "john@example.com"
};

// 변수명을 다르게 하고 싶을 때
const {name: userName, email: userEmail} = user;
console.log(userName, userEmail);  // John, john@example.com

// 원본 객체는 영향 없음
console.log(user.name);  // John
```

#### 기본값 설정

```javascript
const user = {
  id: 1,
  name: "John"
};

// 없는 속성은 undefined
const {id, name, email} = user;
console.log(email);  // undefined

// 기본값 설정
const {id, name, email = "no-email@example.com", role = "user"} = user;
console.log(email);  // no-email@example.com
console.log(role);   // user
```

#### 중첩 객체 분해

```javascript
const user = {
  id: 1,
  name: "John",
  address: {
    city: "Seoul",
    zip: "12345"
  }
};

// 중첩 속성 추출
const {name, address: {city, zip}} = user;
console.log(name, city, zip);  // John, Seoul, 12345

// 부분만 추출
const {address: {city}} = user;
console.log(city);  // Seoul
```

#### 나머지 속성 수집

```javascript
const user = {
  id: 1,
  name: "John",
  email: "john@example.com",
  age: 25,
  role: "admin"
};

// 일부만 추출하고 나머지를 수집
const {id, name, ...rest} = user;
console.log(id, name);    // 1, John
console.log(rest);        // {email: "...", age: 25, role: "admin"}
```

#### 리액트에서의 사용 (매우 중요!)

```javascript
// ✅ Props 디스트럭처링 (필수!)
function UserCard({id, name, email}) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{email}</p>
    </div>
  );
}

// 사용: <UserCard id={1} name="John" email="john@example.com" />

// ✅ 중첩 Props
function UserProfile({user: {name, email}, settings: {theme}}) {
  return (
    <div style={{background: theme === 'dark' ? '#333' : '#fff'}}>
      <h1>{name}</h1>
      <p>{email}</p>
    </div>
  );
}

// ✅ 기본값과 함께
function Button({label = "Click me", onClick = () => {}, disabled = false}) {
  return (
    <button disabled={disabled} onClick={onClick}>
      {label}
    </button>
  );
}

// ✅ API 응답 처리
useEffect(() => {
  fetch("/api/user")
    .then(res => res.json())
    .then(({id, name, email}) => {
      // API 응답에서 필요한 속성만 추출
      setUser({id, name, email});
    });
}, []);

// ✅ 이벤트 핸들러에서
const handleChange = ({target: {name, value}}) => {
  setFormData({...formData, [name]: value});
};

// ✅ useState에서 객체 상태
const [form, setForm] = useState({
  name: "",
  email: "",
  password: ""
});

const {name, email, password} = form;

// ✅ useContext에서
const UserContext = createContext();

function App() {
  const {user, setUser} = useContext(UserContext);
  const {name, email} = user;

  return <div>{name}</div>;
}
```

---

## ✅ 3. Spread/Rest

### spread로 배열/객체를 복사하고 병합할 수 있다

#### 배열 spread

```javascript
// 배열 복사
const arr1 = [1, 2, 3];
const arr2 = [...arr1];
console.log(arr2);  // [1, 2, 3]
console.log(arr1 === arr2);  // false (새로운 배열)

// 배열 병합
const arr3 = [1, 2, 3];
const arr4 = [4, 5, 6];
const merged = [...arr3, ...arr4];
console.log(merged);  // [1, 2, 3, 4, 5, 6]

// 중간에 요소 추가
const arr5 = [1, 2, 3];
const arr6 = [0, ...arr5, 4, 5];
console.log(arr6);  // [0, 1, 2, 3, 4, 5]

// 함수 인자로 사용
const sum = (a, b, c) => a + b + c;
const numbers = [1, 2, 3];
console.log(sum(...numbers));  // 6
```

#### 객체 spread

```javascript
// 객체 복사
const user = {id: 1, name: "John"};
const userCopy = {...user};
console.log(userCopy);  // {id: 1, name: "John"}
console.log(user === userCopy);  // false (새로운 객체)

// 객체 병합
const user = {id: 1, name: "John"};
const address = {city: "Seoul", zip: "12345"};
const merged = {...user, ...address};
console.log(merged);
// {id: 1, name: "John", city: "Seoul", zip: "12345"}

// 속성 추가/덮어쓰기
const user = {id: 1, name: "John", age: 25};
const updated = {...user, age: 26, email: "john@example.com"};
console.log(updated);
// {id: 1, name: "John", age: 26, email: "john@example.com"}

// 속성 제거 (별도 처리 필요)
const user = {id: 1, name: "John", secret: "password"};
const {secret, ...publicUser} = user;
console.log(publicUser);  // {id: 1, name: "John"}
```

#### 리액트에서의 사용 (매우 중요!)

```javascript
// ✅ 상태 업데이트 (불변성 유지)
const [user, setUser] = useState({name: "John", age: 25});

// ❌ 나쁜 예: 직접 수정
user.age = 26;
setUser(user);  // React가 변화를 감지하지 못함

// ✅ 좋은 예: 새 객체 생성
setUser({...user, age: 26});

// ✅ 중첩 객체 업데이트
const [form, setForm] = useState({
  user: {name: "John", age: 25},
  address: {city: "Seoul"}
});

// 특정 속성 업데이트
setForm({
  ...form,
  user: {...form.user, age: 26}
});

// ✅ Props 전달
function Parent() {
  const user = {id: 1, name: "John", email: "john@example.com"};
  return <UserCard {...user} />;
}

// UserCard는 id, name, email을 props로 받음
function UserCard({id, name, email}) {
  return <div>{name}</div>;
}

// ✅ 배열 상태 업데이트
const [items, setItems] = useState([1, 2, 3]);

// 요소 추가
setItems([...items, 4, 5]);

// 요소 제거
setItems(items.filter(item => item !== 2));

// 요소 수정
setItems(items.map(item => item === 2 ? 20 : item));

// ✅ API 응답과 기존 상태 병합
useEffect(() => {
  fetch("/api/users")
    .then(res => res.json())
    .then(data => {
      setUsers({...data});
    });
}, []);
```

---

### rest로 나머지 요소를 수집할 수 있다

#### 함수 매개변수에서 rest

```javascript
// 개별 매개변수
function sum1(a, b, c) {
  return a + b + c;
}
console.log(sum1(1, 2, 3));  // 6

// rest 파라미터: 나머지를 배열로
function sum2(a, ...rest) {
  console.log(a);      // 1
  console.log(rest);   // [2, 3, 4, 5]
  return a + rest.reduce((acc, n) => acc + n, 0);
}
console.log(sum2(1, 2, 3, 4, 5));  // 15

// 여러 개의 고정 매개변수 + rest
function greet(greeting, name, ...hobbies) {
  console.log(greeting);  // "Hello"
  console.log(name);      // "John"
  console.log(hobbies);   // ["reading", "gaming"]
}
greet("Hello", "John", "reading", "gaming");
```

#### 배열 분해에서 rest

```javascript
const colors = ["red", "green", "blue", "yellow", "purple"];

const [primary, secondary, ...rest] = colors;
console.log(primary);   // "red"
console.log(secondary); // "green"
console.log(rest);      // ["blue", "yellow", "purple"]
```

#### 객체 분해에서 rest

```javascript
const user = {
  id: 1,
  name: "John",
  email: "john@example.com",
  age: 25,
  role: "admin"
};

// 특정 속성 추출 + 나머지 수집
const {id, name, ...rest} = user;
console.log(id);    // 1
console.log(name);  // "John"
console.log(rest);  // {email: "...", age: 25, role: "admin"}
```

#### 리액트에서의 사용

```javascript
// ✅ Props에서 일부는 사용하고 나머지는 전달
function CustomButton({label, onClick, ...rest}) {
  return (
    <button onClick={onClick} {...rest}>
      {label}
    </button>
  );
}

// 사용: className, disabled 등을 자동으로 전달
<CustomButton
  label="Click me"
  onClick={() => {}}
  className="primary"
  disabled={false}
/>

// ✅ 여러 Props를 한 번에 처리
function Form({fields, ...formProps}) {
  return (
    <form {...formProps}>
      {fields.map(field => (
        <input key={field} name={field} />
      ))}
    </form>
  );
}

// ✅ API 응답에서 필요한 것만 추출하고 나머지 저장
const fetchUserData = async () => {
  const {id, name, email, ...otherData} = await fetch("/api/user").then(r => r.json());
  setBasicInfo({id, name, email});
  setExtraInfo(otherData);
};

// ✅ 함수형 컴포넌트의 Props
function UserList({users, title, ...listProps}) {
  return (
    <div>
      <h1>{title}</h1>
      <ul {...listProps}>
        {users.map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}

// ✅ 상태 업데이트 시 일부만 변경
const [state, setState] = useState({
  user: {},
  settings: {},
  data: []
});

// 특정 부분만 업데이트
setState({
  ...state,
  user: {...state.user, name: "New Name"}
});
```

---

## ✅ 4. 배열 메서드

### map으로 배열을 변환할 수 있다

#### 기본 문법

```javascript
// 각 요소에 함수 적용
const arr = [1, 2, 3, 4];
const doubled = arr.map(num => num * 2);
console.log(doubled);  // [2, 4, 6, 8]

// 원본 배열은 변경 안 됨
console.log(arr);  // [1, 2, 3, 4]

// 복잡한 변환
const users = [
  {id: 1, name: "John"},
  {id: 2, name: "Jane"},
  {id: 3, name: "Bob"}
];

const names = users.map(user => user.name);
console.log(names);  // ["John", "Jane", "Bob"]

// 인덱스와 원본 배열도 접근 가능
const indexed = arr.map((num, index, array) => ({
  value: num,
  index: index,
  array: array
}));
```

#### 리액트에서의 사용 (매우 중요!)

```javascript
// ✅ 리스트 렌더링 (가장 많이 사용)
function UserList({users}) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

// ✅ 객체에서 특정 속성만 추출하여 표시
function ProductList({products}) {
  return (
    <div>
      {products.map(product => (
        <div key={product.id}>
          <h3>{product.name}</h3>
          <p>${product.price}</p>
        </div>
      ))}
    </div>
  );
}

// ✅ 배열 데이터를 컴포넌트로 변환
function TodoList({todos}) {
  return (
    <ul>
      {todos.map((todo, index) => (
        <TodoItem
          key={todo.id}
          todo={todo}
          index={index}
        />
      ))}
    </ul>
  );
}

// ✅ 데이터 전처리
function Dashboard({rawData}) {
  const processedData = rawData.map(item => ({
    ...item,
    displayValue: item.value.toFixed(2),
    color: item.value > 100 ? "red" : "green"
  }));

  return (
    <div>
      {processedData.map(item => (
        <div key={item.id} style={{color: item.color}}>
          {item.displayValue}
        </div>
      ))}
    </div>
  );
}

// ✅ 조건부 렌더링과 함께
function FilteredList({items, filter}) {
  return (
    <ul>
      {items
        .filter(item => item.category === filter)
        .map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
    </ul>
  );
}

// ⚠️ 주의: key는 index를 사용하면 안 됨
// ❌ 나쁜 예
{items.map((item, index) => <li key={index}>{item}</li>)}

// ✅ 좋은 예
{items.map(item => <li key={item.id}>{item.name}</li>)}
```

---

### filter로 조건에 맞는 요소를 추출할 수 있다

#### 기본 문법

```javascript
const arr = [1, 2, 3, 4, 5];

// 조건에 맞는 요소만 필터링
const evens = arr.filter(num => num % 2 === 0);
console.log(evens);  // [2, 4]

// 원본 배열은 변경 안 됨
console.log(arr);  // [1, 2, 3, 4, 5]

// 객체 배열 필터링
const users = [
  {id: 1, name: "John", age: 25},
  {id: 2, name: "Jane", age: 30},
  {id: 3, name: "Bob", age: 20}
];

const adults = users.filter(user => user.age >= 25);
console.log(adults);
// [{id: 1, name: "John", age: 25}, {id: 2, name: "Jane", age: 30}]

// 문자열 배열 필터링
const words = ["apple", "banana", "apricot", "cherry"];
const aWords = words.filter(word => word.startsWith("a"));
console.log(aWords);  // ["apple", "apricot"]
```

#### 리액트에서의 사용

```javascript
// ✅ 조건에 맞는 항목만 표시
function ActiveUserList({users}) {
  const activeUsers = users.filter(user => user.status === "active");

  return (
    <ul>
      {activeUsers.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

// ✅ 검색 필터링
function SearchableList({items, searchTerm}) {
  const filtered = items.filter(item =>
    item.name.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <ul>
      {filtered.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}

// ✅ 여러 조건의 필터링
function AdvancedFilter({products, minPrice, maxPrice, category}) {
  const filtered = products.filter(product =>
    product.price >= minPrice &&
    product.price <= maxPrice &&
    product.category === category
  );

  return (
    <div>
      {filtered.map(product => (
        <ProductCard key={product.id} product={product} />
      ))}
    </div>
  );
}

// ✅ 배열 상태에서 요소 제거
function ItemList({items, onDelete}) {
  const handleDelete = (id) => {
    const updated = items.filter(item => item.id !== id);
    onDelete(updated);
  };

  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>
          {item.name}
          <button onClick={() => handleDelete(item.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}

// ✅ map + filter 조합
function CombinedExample({users}) {
  const result = users
    .filter(user => user.age >= 18)
    .map(user => ({
      ...user,
      category: user.age >= 65 ? "senior" : "adult"
    }));

  return (
    <div>
      {result.map(user => (
        <div key={user.id}>
          {user.name} - {user.category}
        </div>
      ))}
    </div>
  );
}
```

---

### reduce로 값을 집계할 수 있다

#### 기본 문법

```javascript
const arr = [1, 2, 3, 4];

// 합계 구하기
const sum = arr.reduce((accumulator, current) => {
  return accumulator + current;
}, 0);
console.log(sum);  // 10

// 축약형
const sum = arr.reduce((acc, cur) => acc + cur, 0);
console.log(sum);  // 10

// 초기값 없을 때 (첫 요소가 accumulator 초기값)
const sum = arr.reduce((acc, cur) => acc + cur);
console.log(sum);  // 10

// 곱하기
const product = arr.reduce((acc, cur) => acc * cur, 1);
console.log(product);  // 24

// 최대값 구하기
const max = arr.reduce((acc, cur) => cur > acc ? cur : acc);
console.log(max);  // 4
```

#### 복잡한 사용 예제

```javascript
// 객체로 집계
const transactions = [
  {type: "income", amount: 100},
  {type: "expense", amount: 50},
  {type: "income", amount: 200},
  {type: "expense", amount: 30}
];

const summary = transactions.reduce((acc, t) => {
  if (t.type === "income") {
    acc.income += t.amount;
  } else {
    acc.expense += t.amount;
  }
  return acc;
}, {income: 0, expense: 0});

console.log(summary);
// {income: 300, expense: 80}

// 배열을 객체로 변환
const users = [
  {id: 1, name: "John"},
  {id: 2, name: "Jane"},
  {id: 3, name: "Bob"}
];

const userMap = users.reduce((acc, user) => {
  acc[user.id] = user.name;
  return acc;
}, {});

console.log(userMap);
// {1: "John", 2: "Jane", 3: "Bob"}

// 배열 평탄화
const nested = [[1, 2], [3, 4], [5, 6]];
const flat = nested.reduce((acc, arr) => acc.concat(arr), []);
console.log(flat);  // [1, 2, 3, 4, 5, 6]

// 그룹핑
const items = [
  {category: "fruit", name: "apple"},
  {category: "fruit", name: "banana"},
  {category: "vegetable", name: "carrot"},
  {category: "vegetable", name: "lettuce"}
];

const grouped = items.reduce((acc, item) => {
  if (!acc[item.category]) {
    acc[item.category] = [];
  }
  acc[item.category].push(item.name);
  return acc;
}, {});

console.log(grouped);
// {
//   fruit: ["apple", "banana"],
//   vegetable: ["carrot", "lettuce"]
// }
```

#### 리액트에서의 사용

```javascript
// ✅ 장바구니 합계 계산
function ShoppingCart({items}) {
  const total = items.reduce((acc, item) => {
    return acc + (item.price * item.quantity);
  }, 0);

  return (
    <div>
      {items.map(item => (
        <div key={item.id}>
          {item.name}: ${item.price} x {item.quantity}
        </div>
      ))}
      <h3>Total: ${total.toFixed(2)}</h3>
    </div>
  );
}

// ✅ 상태 통계
function Dashboard({data}) {
  const stats = data.reduce((acc, item) => {
    acc.total++;
    if (item.status === "completed") acc.completed++;
    if (item.status === "pending") acc.pending++;
    return acc;
  }, {total: 0, completed: 0, pending: 0});

  return (
    <div>
      <p>Total: {stats.total}</p>
      <p>Completed: {stats.completed}</p>
      <p>Pending: {stats.pending}</p>
    </div>
  );
}

// ✅ 폼 데이터 처리
function MultiSelectForm({options}) {
  const [selected, setSelected] = useState([]);

  const formData = selected.reduce((acc, optionId) => {
    const option = options.find(o => o.id === optionId);
    acc[option.name] = option.value;
    return acc;
  }, {});

  return (
    <form>
      {/* 폼 입력 */}
      <pre>{JSON.stringify(formData, null, 2)}</pre>
    </form>
  );
}

// ✅ 객체 변환
function DataTransformer({rawData}) {
  const transformed = rawData.reduce((acc, item) => {
    acc[item.id] = {
      ...item,
      processed: true,
      timestamp: new Date().toISOString()
    };
    return acc;
  }, {});

  return <pre>{JSON.stringify(transformed, null, 2)}</pre>;
}
```

---

## ✅ 5. 비동기 처리

### Promise의 개념을 이해한다

#### Promise 기본 구조

```javascript
// Promise 생성
const myPromise = new Promise((resolve, reject) => {
  // 비동기 작업
  const success = true;

  if (success) {
    resolve("성공했습니다!");  // 성공
  } else {
    reject("실패했습니다");    // 실패
  }
});

// Promise 사용
myPromise
  .then(result => {
    console.log("결과:", result);
  })
  .catch(error => {
    console.error("에러:", error);
  });
```

#### Promise의 3가지 상태

```javascript
// 1. Pending (대기): 작업이 진행 중
const promise1 = new Promise((resolve, reject) => {
  // 작업 중...
});
console.log(promise1);  // Promise { <pending> }

// 2. Fulfilled (완료): resolve 호출
const promise2 = new Promise((resolve) => {
  resolve("완료!");
});
promise2.then(result => console.log(result));  // 완료!

// 3. Rejected (실패): reject 호출
const promise3 = new Promise((resolve, reject) => {
  reject("실패!");
});
promise3.catch(error => console.log(error));  // 실패!
```

#### Promise 체이닝

```javascript
fetch("/api/user")
  .then(response => response.json())
  .then(user => {
    console.log("사용자:", user);
    return fetch(`/api/posts/${user.id}`);
  })
  .then(response => response.json())
  .then(posts => {
    console.log("포스트:", posts);
  })
  .catch(error => {
    console.error("에러:", error);
  });
```

#### Promise.all()과 Promise.race()

```javascript
// Promise.all: 모든 Promise가 완료될 때까지 대기
Promise.all([
  fetch("/api/users").then(r => r.json()),
  fetch("/api/posts").then(r => r.json()),
  fetch("/api/comments").then(r => r.json())
])
.then(([users, posts, comments]) => {
  console.log("모든 데이터:", {users, posts, comments});
})
.catch(error => {
  console.error("하나라도 실패하면:", error);
});

// Promise.race: 가장 먼저 완료되는 Promise 반환
Promise.race([
  fetch("/api/fast"),
  fetch("/api/slow")
])
.then(result => console.log("가장 빠른 결과:", result))
.catch(error => console.error("가장 빠른 실패:", error));
```

---

### async/await로 비동기 코드를 작성할 수 있다

#### 기본 문법

```javascript
// ❌ Promise 방식 (복잡함)
function fetchUser() {
  return fetch("/api/user")
    .then(response => response.json())
    .then(data => {
      console.log(data);
      return data;
    })
    .catch(error => console.error(error));
}

// ✅ async/await 방식 (간단함)
async function fetchUser() {
  try {
    const response = await fetch("/api/user");
    const data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error(error);
  }
}

// await는 Promise를 기다림
const user = await fetchUser();
```

#### 순차 vs 병렬 처리

```javascript
// ❌ 순차 처리 (느림): 하나씩 기다림
async function sequential() {
  const users = await fetch("/api/users").then(r => r.json());
  const posts = await fetch("/api/posts").then(r => r.json());
  const comments = await fetch("/api/comments").then(r => r.json());
  return {users, posts, comments};
}

// ✅ 병렬 처리 (빠름): 동시에 요청
async function parallel() {
  const [users, posts, comments] = await Promise.all([
    fetch("/api/users").then(r => r.json()),
    fetch("/api/posts").then(r => r.json()),
    fetch("/api/comments").then(r => r.json())
  ]);
  return {users, posts, comments};
}
```

#### 리액트에서의 사용

```javascript
// ✅ useEffect에서 데이터 페칭
function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        setLoading(true);
        const response = await fetch("/api/users");
        const data = await response.json();
        setUsers(data);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    };

    fetchUsers();
  }, []);

  if (loading) return <div>로딩 중...</div>;
  if (error) return <div>에러: {error.message}</div>;

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

// ✅ 폼 제출 처리
function UserForm() {
  const [isSubmitting, setIsSubmitting] = useState(false);

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      setIsSubmitting(true);
      const response = await fetch("/api/users", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: JSON.stringify({name: "John"})
      });
      const result = await response.json();
      alert("사용자가 생성되었습니다!");
    } catch (error) {
      alert("에러: " + error.message);
    } finally {
      setIsSubmitting(false);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" />
      <button disabled={isSubmitting}>
        {isSubmitting ? "제출 중..." : "제출"}
      </button>
    </form>
  );
}
```

---

### try-catch로 에러를 처리할 수 있다

#### 기본 문법

```javascript
try {
  // 코드 실행
  const result = risky();
} catch (error) {
  // 에러 처리
  console.error("에러 발생:", error.message);
} finally {
  // 항상 실행됨
  console.log("정리 작업");
}
```

#### async/await에서의 에러 처리

```javascript
async function fetchAndProcess() {
  try {
    const response = await fetch("/api/data");

    // HTTP 에러 확인
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    return data;

  } catch (error) {
    console.error("에러가 발생했습니다:", error.message);
    // 기본값 반환
    return null;
  }
}
```

#### 리액트에서의 에러 처리

```javascript
// ✅ 데이터 페칭 시
function DataComponent() {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    const loadData = async () => {
      try {
        const response = await fetch("/api/data");

        if (!response.ok) {
          throw new Error(`Failed to fetch: ${response.status}`);
        }

        const result = await response.json();
        setData(result);
        setError(null);
      } catch (err) {
        setError(err.message);
        setData(null);
      }
    };

    loadData();
  }, []);

  if (error) {
    return <div className="error">에러: {error}</div>;
  }

  if (!data) {
    return <div>로딩 중...</div>;
  }

  return <div>{JSON.stringify(data)}</div>;
}

// ✅ 에러 바운더리 (클래스 컴포넌트)
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = {error: null};
  }

  static getDerivedStateFromError(error) {
    return {error};
  }

  componentDidCatch(error, errorInfo) {
    console.error("에러가 발생했습니다:", error, errorInfo);
  }

  render() {
    if (this.state.error) {
      return <div>에러가 발생했습니다</div>;
    }
    return this.props.children;
  }
}

// 사용: <ErrorBoundary><MyComponent /></ErrorBoundary>
```

---

## ✅ 6. 모듈

### export로 함수/변수를 내보낼 수 있다

#### Named Export (명시적 내보내기)

```javascript
// math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

export const PI = 3.14159;

// 또는 한 번에
function multiply(a, b) {
  return a * b;
}

function divide(a, b) {
  return a / b;
}

export {multiply, divide};
```

#### Default Export (기본값 내보내기)

```javascript
// calculator.js
export default class Calculator {
  add(a, b) {
    return a + b;
  }

  subtract(a, b) {
    return a - b;
  }
}

// 또는
const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000
};

export default config;
```

#### 혼합 사용

```javascript
// utils.js
export function helper() {}
export const VERSION = "1.0.0";

export default class Utils {
  log() {
    console.log("Utils");
  }
}
```

---

### import로 다른 파일의 코드를 가져올 수 있다

#### Named Import

```javascript
// main.js
import {add, subtract, PI} from "./math.js";

console.log(add(2, 3));       // 5
console.log(subtract(5, 2));  // 3
console.log(PI);              // 3.14159
```

#### Default Import

```javascript
// app.js
import Calculator from "./calculator.js";

const calc = new Calculator();
console.log(calc.add(2, 3));  // 5
```

#### 혼합 사용

```javascript
// index.js
import config, {helper, VERSION} from "./utils.js";

console.log(config);
console.log(helper());
console.log(VERSION);
```

#### Import 별칭

```javascript
// main.js
import {add as addition, subtract as subtraction} from "./math.js";

console.log(addition(2, 3));     // 5
console.log(subtraction(5, 2));  // 3
```

#### 모든 것 Import

```javascript
// main.js
import * as math from "./math.js";

console.log(math.add(2, 3));     // 5
console.log(math.subtract(5, 2)); // 3
console.log(math.PI);             // 3.14159
```

#### 리액트에서의 사용

```javascript
// components/UserCard.jsx
export default function UserCard({user}) {
  return <div>{user.name}</div>;
}

// pages/Home.jsx
import UserCard from "../components/UserCard";
import {useState, useEffect} from "react";

export default function Home() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    // 데이터 페칭
  }, []);

  return (
    <div>
      {users.map(user => (
        <UserCard key={user.id} user={user} />
      ))}
    </div>
  );
}

// hooks/useAsync.js
import {useState, useEffect} from "react";

export function useAsync(asyncFunction) {
  const [status, setStatus] = useState("idle");
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    asyncFunction()
      .then(result => {setStatus("success"); setData(result);})
      .catch(error => {setStatus("error"); setError(error);});
  }, []);

  return {status, data, error};
}

// pages/Dashboard.jsx
import {useAsync} from "../hooks/useAsync";

export default function Dashboard() {
  const {status, data, error} = useAsync(() =>
    fetch("/api/data").then(r => r.json())
  );

  if (status === "idle") return <div>준비 중...</div>;
  if (status === "error") return <div>에러: {error.message}</div>;

  return <div>{JSON.stringify(data)}</div>;
}
```

---

## 종합 실습 예제

### 완전한 React 컴포넌트 예제

```javascript
// hooks/useApi.js
import {useState, useEffect} from "react";

export function useApi(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const result = await response.json();
        setData(result);
        setError(null);
      } catch (err) {
        setError(err.message);
        setData(null);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return {data, loading, error};
}

// components/UserProfile.jsx
import {useState} = "react";
import {useApi} from "../hooks/useApi";

export default function UserProfile({userId}) {
  // 구조 분해로 props 받기
  const {data: user, loading, error} = useApi(`/api/users/${userId}`);
  const [isExpanded, setIsExpanded] = useState(false);

  if (loading) return <div>로딩 중...</div>;
  if (error) return <div>에러: {error}</div>;
  if (!user) return <div>사용자 없음</div>;

  // 객체 구조 분해
  const {name, email, address: {city} = {}} = user;

  return (
    <div className={`profile ${isExpanded ? "expanded" : ""}`}>
      <h2>{name}</h2>
      <p>{email}</p>
      {isExpanded && <p>Location: {city}</p>}
      <button onClick={() => setIsExpanded(!isExpanded)}>
        {isExpanded ? "접기" : "펼치기"}
      </button>
    </div>
  );
}

// pages/UserList.jsx
import {useState} from "react";
import UserProfile from "../components/UserProfile";
import {useApi} from "../hooks/useApi";

export default function UserList() {
  const {data: users = [], loading, error} = useApi("/api/users");
  const [searchTerm, setSearchTerm] = useState("");

  // 배열 메서드 활용: filter + map
  const filteredUsers = users
    .filter(user => user.name.toLowerCase().includes(searchTerm.toLowerCase()))
    .map(user => ({...user, displayName: user.name.toUpperCase()}));

  const stats = filteredUsers.reduce((acc, user) => {
    acc.total++;
    if (user.active) acc.active++;
    return acc;
  }, {total: 0, active: 0});

  if (loading) return <div>로딩 중...</div>;
  if (error) return <div>에러: {error}</div>;

  return (
    <div>
      <h1>사용자 목록</h1>

      {/* 검색 필터 */}
      <input
        type="text"
        placeholder="검색..."
        value={searchTerm}
        onChange={e => setSearchTerm(e.target.value)}
      />

      {/* 통계 */}
      <p>{`전체: ${stats.total}, 활성: ${stats.active}`}</p>

      {/* 사용자 목록 렌더링 */}
      <div>
        {filteredUsers.map(user => (
          <UserProfile key={user.id} userId={user.id} />
        ))}
      </div>
    </div>
  );
}
```

---

## 체크리스트 최종 정리

| 항목 | 학습 상태 | 중요도 |
|------|---------|--------|
| const/let 차이 | ⭐⭐⭐⭐⭐ | 필수 |
| 화살표 함수 | ⭐⭐⭐⭐⭐ | 필수 |
| 템플릿 리터럴 | ⭐⭐⭐⭐ | 높음 |
| 배열 구조 분해 | ⭐⭐⭐⭐⭐ | 필수 |
| 객체 구조 분해 | ⭐⭐⭐⭐⭐ | 필수 |
| Spread 연산자 | ⭐⭐⭐⭐⭐ | 필수 |
| Rest 파라미터 | ⭐⭐⭐⭐ | 높음 |
| map() | ⭐⭐⭐⭐⭐ | 필수 |
| filter() | ⭐⭐⭐⭐⭐ | 필수 |
| reduce() | ⭐⭐⭐⭐ | 높음 |
| Promise | ⭐⭐⭐⭐⭐ | 필수 |
| async/await | ⭐⭐⭐⭐⭐ | 필수 |
| try-catch | ⭐⭐⭐⭐⭐ | 필수 |
| export | ⭐⭐⭐⭐⭐ | 필수 |
| import | ⭐⭐⭐⭐⭐ | 필수 |

