# 자바스크립트 고급 개념 (리액트 필수)

## 1. this의 이해

### this 바인딩의 4가지 규칙

```javascript
// 1. 일반 함수 호출: this는 undefined (strict mode) 또는 window
function greet() {
  console.log(this);
}
greet();  // undefined (strict mode)

// 2. 메소드 호출: this는 객체
const user = {
  name: "John",
  greet: function() {
    console.log(this.name);  // "John"
  }
};
user.greet();

// 3. 생성자 함수: this는 새 객체
function User(name) {
  this.name = name;
}
const user = new User("John");
console.log(user.name);  // "John"

// 4. call/apply/bind: this를 명시적으로 지정
function greet() {
  console.log(`Hello, ${this.name}`);
}
const user = {name: "John"};
greet.call(user);      // Hello, John
greet.apply(user);     // Hello, John
const boundGreet = greet.bind(user);
boundGreet();          // Hello, John
```

### 화살표 함수의 this

```javascript
const user = {
  name: "John",
  greet: function() {
    // 화살표 함수는 외부 this를 상속받음
    const sayName = () => {
      console.log(this.name);  // "John"
    };
    sayName();
  }
};
user.greet();

// 리액트에서
class MyComponent extends React.Component {
  constructor() {
    super();
    this.state = {count: 0};
  }

  // 메소드: this 바인딩 필요
  handleClick = () => {
    this.setState({count: this.state.count + 1});
  };

  // 또는 constructor에서 bind
  constructor() {
    super();
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState({count: this.state.count + 1});
  }
}
```

---

## 2. 프로토타입과 프로토타입 체인

### 프로토타입 기본

```javascript
// 모든 객체는 프로토타입을 가짐
const user = {name: "John"};
console.log(Object.getPrototypeOf(user));

// 프로토타입에 메소드 추가
const userProto = {
  greet() {
    return `Hello, ${this.name}`;
  }
};

const user = Object.create(userProto);
user.name = "John";
console.log(user.greet());  // Hello, John
```

### 생성자 함수와 프로토타입

```javascript
function User(name) {
  this.name = name;
}

// 프로토타입에 메소드 추가
User.prototype.greet = function() {
  return `Hello, ${this.name}`;
};

const user = new User("John");
console.log(user.greet());  // Hello, John
console.log(user.constructor === User);  // true
```

### 프로토타입 체인

```javascript
// 객체 → 클래스 → Object.prototype → null
function Animal(name) {
  this.name = name;
}

Animal.prototype.makeSound = function() {
  console.log("Some sound");
};

function Dog(name, breed) {
  Animal.call(this, name);
  this.breed = breed;
}

// 프로토타입 상속
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.makeSound = function() {
  console.log("Woof!");
};

const dog = new Dog("Buddy", "Golden");
console.log(dog.name);      // "Buddy"
dog.makeSound();            // "Woof!"
```

---

## 3. 클래스 (Class Syntax)

### 클래스 기본

```javascript
// ES6 클래스 (프로토타입의 문법 설탕)
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    return `Hello, ${this.name}`;
  }

  getAge() {
    return this.age;
  }
}

const user = new User("John", 25);
console.log(user.greet());   // Hello, John
console.log(user.getAge());  // 25
```

### 상속

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  makeSound() {
    console.log("Some sound");
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);  // 부모 생성자 호출
    this.breed = breed;
  }

  makeSound() {
    console.log("Woof!");
  }

  getInfo() {
    return `${this.name} is a ${this.breed}`;
  }
}

const dog = new Dog("Buddy", "Golden");
console.log(dog.getInfo());  // Buddy is a Golden
dog.makeSound();             // Woof!
```

### 접근 제한자

```javascript
class User {
  constructor(name, password) {
    this.name = name;
    this._password = password;  // 관례상 private (실제로는 접근 가능)
    #privateField = "private";   // 실제 private (# 사용)
  }

  // public 메소드
  getInfo() {
    return this.name;
  }

  // private 메소드
  #validatePassword() {
    return this._password.length > 8;
  }

  checkPassword(pwd) {
    return this.#validatePassword() && this._password === pwd;
  }
}

const user = new User("John", "password123");
console.log(user.getInfo());        // John
console.log(user._password);        // "password123" (접근 가능)
// console.log(user.#privateField);  // Error: private field
```

### 정적 메소드와 속성

```javascript
class Math {
  static PI = 3.14159;

  static add(a, b) {
    return a + b;
  }

  static multiply(a, b) {
    return a * b;
  }
}

console.log(Math.PI);              // 3.14159
console.log(Math.add(2, 3));       // 5
console.log(Math.multiply(2, 3));  // 6

// 인스턴스에서는 접근 불가
const calc = new Math();
// console.log(calc.PI);  // undefined
```

### 리액트에서의 클래스 컴포넌트

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: 0};
  }

  componentDidMount() {
    console.log("Component mounted");
  }

  componentDidUpdate(prevProps, prevState) {
    console.log("Component updated");
  }

  componentWillUnmount() {
    console.log("Component unmounted");
  }

  handleClick = () => {
    this.setState({count: this.state.count + 1});
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

---

## 4. 이벤트 위임 (Event Delegation)

### 이벤트 버블링과 캡처

```javascript
// 이벤트 버블링: 자식에서 부모로 전파
document.getElementById("parent").addEventListener("click", (e) => {
  console.log("Parent clicked");
});

document.getElementById("child").addEventListener("click", (e) => {
  console.log("Child clicked");
});

// child 클릭 시:
// "Child clicked"
// "Parent clicked"
```

### 이벤트 위임

```html
<ul id="list">
  <li><button class="delete">Delete</button></li>
  <li><button class="delete">Delete</button></li>
  <li><button class="delete">Delete</button></li>
</ul>

<script>
// 비효율적: 각 버튼에 이벤트 리스너 추가
document.querySelectorAll(".delete").forEach(btn => {
  btn.addEventListener("click", handleDelete);
});

// 효율적: 부모에 이벤트 리스너 추가
document.getElementById("list").addEventListener("click", (e) => {
  if (e.target.classList.contains("delete")) {
    handleDelete(e);
  }
});
</script>
```

### 리액트에서는 자동 처리됨

```javascript
function ItemList({items}) {
  const handleDelete = (id) => {
    // 삭제 처리
  };

  const handleClick = (e) => {
    if (e.target.classList.contains("delete")) {
      const id = e.target.dataset.id;
      handleDelete(id);
    }
  };

  return (
    <ul onClick={handleClick}>
      {items.map(item => (
        <li key={item.id}>
          {item.name}
          <button className="delete" data-id={item.id}>
            Delete
          </button>
        </li>
      ))}
    </ul>
  );
}
```

---

## 5. 메모리 관리와 가비지 컬렉션

### 메모리 누수 예방

```javascript
// 메모리 누수 예: 사용하지 않는 참조 유지
let data = [];
function addData() {
  data.push(new Array(1000000).fill("*"));
}

// 리스너 제거 실패
const element = document.getElementById("myElement");
element.addEventListener("click", handler);
// 나중에 element를 제거하면 리스너도 제거해야 함
element.removeEventListener("click", handler);
```

### 리액트에서 메모리 누수 방지

```javascript
// useEffect에서 정리 함수 작성
useEffect(() => {
  const handleResize = () => {
    console.log("Resized");
  };

  window.addEventListener("resize", handleResize);

  // 정리 함수: 컴포넌트 언마운트 시 실행
  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);

// API 요청 취소
useEffect(() => {
  const controller = new AbortController();

  fetch("/api/users", {signal: controller.signal})
    .then(r => r.json())
    .then(data => setUsers(data))
    .catch(err => {
      if (err.name !== "AbortError") {
        console.error(err);
      }
    });

  return () => controller.abort();  // 정리
}, []);

// 타이머 정리
useEffect(() => {
  const timeoutId = setTimeout(() => {
    console.log("After 1 second");
  }, 1000);

  return () => clearTimeout(timeoutId);
}, []);
```

---

## 6. WeakMap과 WeakSet

### 약한 참조 (Weak References)

```javascript
// Map: 강한 참조 유지
const map = new Map();
let obj = {name: "John"};
map.set(obj, "value");
obj = null;
console.log(map.size);  // 1 (여전히 메모리 점유)

// WeakMap: 약한 참조 (키가 가비지 컬렉션되면 엔트리도 제거)
const weakMap = new WeakMap();
let obj = {name: "John"};
weakMap.set(obj, "value");
obj = null;
// 가비지 컬렉션 후 엔트리 자동 제거
```

### 비공개 데이터 저장

```javascript
// WeakMap으로 비공개 데이터 구현
const privateData = new WeakMap();

class User {
  constructor(name, password) {
    privateData.set(this, {
      password: password,
      lastLogin: null
    });
    this.name = name;
  }

  checkPassword(pwd) {
    return privateData.get(this).password === pwd;
  }
}

const user = new User("John", "secret");
console.log(user.name);         // "John"
console.log(user.password);     // undefined
console.log(user.checkPassword("secret"));  // true
```

---

## 7. Proxy와 Reflect

### Proxy를 이용한 데이터 접근 제어

```javascript
const user = {
  name: "John",
  age: 25
};

const proxy = new Proxy(user, {
  get(target, property) {
    console.log(`Accessing ${property}`);
    return target[property];
  },
  set(target, property, value) {
    console.log(`Setting ${property} to ${value}`);
    if (property === "age" && value < 0) {
      throw new Error("Age cannot be negative");
    }
    target[property] = value;
    return true;
  }
});

console.log(proxy.name);    // Accessing name → "John"
proxy.age = 30;             // Setting age to 30
// proxy.age = -5;          // Error: Age cannot be negative
```

### Reflect 사용

```javascript
const user = {name: "John", age: 25};

const proxy = new Proxy(user, {
  get(target, property) {
    console.log(`Get ${property}`);
    // Reflect를 사용하면 더 깔끔함
    return Reflect.get(target, property);
  },
  set(target, property, value) {
    console.log(`Set ${property}`);
    return Reflect.set(target, property, value);
  }
});
```

---

## 8. Symbol

### Symbol의 기본 사용

```javascript
// 고유한 값 생성
const id1 = Symbol("id");
const id2 = Symbol("id");

console.log(id1 === id2);  // false (각각 고유함)

const user = {
  [id1]: "private-id-1",
  name: "John"
};

console.log(Object.keys(user));      // ["name"]
console.log(user[id1]);              // "private-id-1"
```

### 잘 알려진 Symbol

```javascript
// Symbol.iterator: 반복 가능한 객체
const iterable = {
  data: [1, 2, 3],
  [Symbol.iterator]() {
    let index = 0;
    return {
      next: () => {
        if (index < this.data.length) {
          return {value: this.data[index++], done: false};
        }
        return {done: true};
      }
    };
  }
};

for (const value of iterable) {
  console.log(value);  // 1, 2, 3
}
```

---

## 9. Generator와 Iterator

### Generator 함수

```javascript
function* countUp(max) {
  for (let i = 1; i <= max; i++) {
    yield i;
  }
}

const generator = countUp(3);
console.log(generator.next());  // {value: 1, done: false}
console.log(generator.next());  // {value: 2, done: false}
console.log(generator.next());  // {value: 3, done: false}
console.log(generator.next());  // {value: undefined, done: true}

// for...of에서 사용 가능
for (const num of countUp(3)) {
  console.log(num);  // 1, 2, 3
}
```

### 무한 시퀀스

```javascript
function* infinite() {
  let i = 0;
  while (true) {
    yield i++;
  }
}

const gen = infinite();
console.log(gen.next().value);  // 0
console.log(gen.next().value);  // 1
console.log(gen.next().value);  // 2
```

### 양방향 통신

```javascript
function* echo() {
  while (true) {
    const value = yield;
    console.log(`Received: ${value}`);
  }
}

const gen = echo();
gen.next();  // Generator 시작
gen.next("Hello");   // Received: Hello
gen.next("World");   // Received: World
```

---

## 10. 모듈 시스템 (import/export)

### CommonJS (Node.js)

```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = {add};

// main.js
const {add} = require("./math");
console.log(add(2, 3));  // 5
```

### ES6 모듈

```javascript
// math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

export default class Calculator {
  add(a, b) {return a + b;}
}

// main.js
import Calculator, {add, subtract} from "./math.js";

console.log(add(2, 3));           // 5
console.log(subtract(5, 2));      // 3

const calc = new Calculator();
console.log(calc.add(2, 3));      // 5
```

### 리액트에서의 사용

```javascript
// components/Button.jsx
export default function Button({label, onClick}) {
  return <button onClick={onClick}>{label}</button>;
}

// pages/Home.jsx
import Button from "../components/Button";

export default function Home() {
  const handleClick = () => console.log("Clicked");
  return <Button label="Click Me" onClick={handleClick} />;
}
```

---

## 11. 정규표현식 (Regular Expressions)

### 정규표현식 기본

```javascript
// 리터럴 방식
const regex1 = /hello/i;  // i: 대소문자 무시

// 생성자 방식
const regex2 = new RegExp("hello", "i");

// 테스트
console.log(/hello/.test("Hello World"));     // false
console.log(/hello/i.test("Hello World"));    // true

// 매칭
console.log("Hello World".match(/hello/i));   // ["Hello"]
console.log("Hello World".match(/l/g));       // ["l", "l"]
```

### 자주 사용하는 정규표현식

```javascript
// 이메일 검증
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
console.log(emailRegex.test("john@example.com"));  // true

// 숫자만
const numberRegex = /^\d+$/;
console.log(numberRegex.test("12345"));  // true
console.log(numberRegex.test("123a45")); // false

// URL
const urlRegex = /^https?:\/\/.+/;
console.log(urlRegex.test("https://example.com")); // true

// 전화번호
const phoneRegex = /^\d{3}-\d{4}-\d{4}$/;
console.log(phoneRegex.test("010-1234-5678"));  // true
```

### 리액트에서의 사용

```javascript
function FormValidator() {
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");

  const validateEmail = (e) => {
    const value = e.target.value;
    setEmail(value);

    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(value) && value) {
      setError("Invalid email");
    } else {
      setError("");
    }
  };

  return (
    <div>
      <input type="email" value={email} onChange={validateEmail} />
      {error && <p style={{color: "red"}}>{error}</p>}
    </div>
  );
}
```

---

## 요약 테이블

| 개념 | 설명 | 중요도 |
|------|------|--------|
| this 바인딩 | 함수 컨텍스트 이해 | ⭐⭐⭐⭐⭐ |
| 프로토타입 | 자바스크립트 상속 메커니즘 | ⭐⭐⭐⭐ |
| 클래스 | 현대적 객체 지향 프로그래밍 | ⭐⭐⭐⭐⭐ |
| 이벤트 위임 | 효율적 이벤트 처리 | ⭐⭐⭐⭐ |
| 메모리 관리 | 메모리 누수 방지 | ⭐⭐⭐⭐ |
| Proxy/Reflect | 고급 객체 접근 제어 | ⭐⭐⭐ |
| Symbol | 고유한 속성 식별자 | ⭐⭐⭐ |
| Generator | 지연 평가와 상태 관리 | ⭐⭐⭐ |
| 모듈 시스템 | 코드 구조화 | ⭐⭐⭐⭐⭐ |
| 정규표현식 | 문자열 패턴 매칭 | ⭐⭐⭐⭐ |

