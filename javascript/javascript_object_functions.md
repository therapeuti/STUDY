# 자바스크립트 객체 함수 정리

## 1. 객체 생성 및 접근

### 객체 리터럴 : 객체 생성의 기본 방식

```javascript
const user = {
  id: 1,
  name: "John",
  age: 25,
  email: "john@example.com"
};

console.log(user.name);           // John
console.log(user["age"]);         // 25
```

### new Object() : 빈 객체 생성

```javascript
const obj = new Object();
obj.name = "John";
obj.age = 25;
console.log(obj);  // {name: 'John', age: 25}
```

### Object.create() : 특정 프로토타입을 가진 객체 생성

```javascript
const proto = {
  greet() {
    return `Hello, ${this.name}`;
  }
};

const user = Object.create(proto);
user.name = "John";
console.log(user.greet());  // Hello, John
```

---

## 2. 객체 키 및 값 처리

### Object.keys() : 객체의 모든 키를 배열로 반환

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

console.log(Object.keys(user));
// ["name", "age", "email"]
```

### Object.values() : 객체의 모든 값을 배열로 반환

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

console.log(Object.values(user));
// ["John", 25, "john@example.com"]
```

### Object.entries() : 객체의 [키, 값] 쌍을 배열로 반환

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

console.log(Object.entries(user));
// [["name", "John"], ["age", 25], ["email", "john@example.com"]]

// 순회
Object.entries(user).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

### for...in : 객체의 키를 순회

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

for (const key in user) {
  console.log(`${key}: ${user[key]}`);
}
```

---

## 3. 객체 수정 및 추가

### 속성 추가 : 새로운 속성 추가

```javascript
const user = {
  name: "John"
};

user.age = 25;
user["email"] = "john@example.com";

console.log(user);
// {name: 'John', age: 25, email: 'john@example.com'}
```

### 속성 수정 : 기존 속성 값 변경

```javascript
const user = {
  name: "John",
  age: 25
};

user.name = "Jane";
user["age"] = 30;

console.log(user);
// {name: 'Jane', age: 30}
```

### delete 연산자 : 속성 삭제

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

delete user.email;
console.log(user);
// {name: 'John', age: 25}
```

### in 연산자 : 속성 존재 여부 확인

```javascript
const user = {
  name: "John",
  age: 25
};

console.log("name" in user);   // true
console.log("email" in user);  // false
```

### hasOwnProperty() : 속성 존재 여부 확인 (프로토타입 제외)

```javascript
const user = {
  name: "John",
  age: 25
};

console.log(user.hasOwnProperty("name"));      // true
console.log(user.hasOwnProperty("toString"));  // false
```

---

## 4. 객체 병합 및 복사

### Object.assign() : 여러 객체를 병합

```javascript
const obj1 = {a: 1, b: 2};
const obj2 = {b: 3, c: 4};
const obj3 = {d: 5};

const merged = Object.assign({}, obj1, obj2, obj3);
console.log(merged);
// {a: 1, b: 3, c: 4, d: 5}

// 첫 번째 객체에 병합 (주의: 원본 수정됨)
Object.assign(obj1, obj2);
console.log(obj1);
// {a: 1, b: 3, c: 4}
```

### Spread Operator (...) : 객체 펼치기 및 병합

```javascript
const obj1 = {a: 1, b: 2};
const obj2 = {b: 3, c: 4};

// 객체 병합
const merged = {...obj1, ...obj2};
console.log(merged);
// {a: 1, b: 3, c: 4}

// 객체 복사
const copy = {...obj1};
console.log(copy);
// {a: 1, b: 2}

// 새 속성 추가하며 병합
const extended = {...obj1, d: 5, e: 6};
console.log(extended);
// {a: 1, b: 2, d: 5, e: 6}
```

### JSON.parse(JSON.stringify()) : 깊은 복사

```javascript
const user = {
  name: "John",
  address: {
    city: "Seoul",
    zip: "12345"
  }
};

const deepCopy = JSON.parse(JSON.stringify(user));
deepCopy.address.city = "Busan";

console.log(user.address.city);      // Seoul (원본 유지)
console.log(deepCopy.address.city);  // Busan
```

---

## 5. 객체 비교 및 동등성

### 객체 비교 : 참조 비교

```javascript
const obj1 = {a: 1};
const obj2 = {a: 1};
const obj3 = obj1;

console.log(obj1 === obj2);  // false (다른 참조)
console.log(obj1 === obj3);  // true (같은 참조)
```

### 깊은 비교 함수 작성

```javascript
function deepEqual(obj1, obj2) {
  if (obj1 === obj2) return true;

  if (obj1 == null || obj2 == null) return false;
  if (typeof obj1 !== "object" || typeof obj2 !== "object") return false;

  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);

  if (keys1.length !== keys2.length) return false;

  return keys1.every(key => deepEqual(obj1[key], obj2[key]));
}

console.log(deepEqual({a: 1}, {a: 1}));           // true
console.log(deepEqual({a: {b: 2}}, {a: {b: 2}})); // true
```

---

## 6. 객체 동결 및 잠금

### Object.freeze() : 객체 동결 (수정 불가)

```javascript
const user = {
  name: "John",
  age: 25
};

Object.freeze(user);

user.age = 30;  // 무시됨
console.log(user.age);  // 25

delete user.name;  // 무시됨
console.log(user.name);  // "John"
```

### Object.seal() : 객체 봉인 (속성 추가/삭제 불가, 수정은 가능)

```javascript
const user = {
  name: "John",
  age: 25
};

Object.seal(user);

user.age = 30;      // OK
user.email = "john@example.com";  // 무시됨
delete user.name;   // 무시됨

console.log(user);  // {name: 'John', age: 30}
```

### Object.preventExtensions() : 객체 확장 금지 (속성 추가만 불가)

```javascript
const user = {
  name: "John",
  age: 25
};

Object.preventExtensions(user);

user.age = 30;                    // OK
user.email = "john@example.com";  // 무시됨
delete user.name;                 // OK

console.log(user);  // {age: 30}
```

### Object.isFrozen() / isSealed() / isExtensible() : 상태 확인

```javascript
const obj = {a: 1};

console.log(Object.isExtensible(obj));  // true

Object.freeze(obj);
console.log(Object.isFrozen(obj));      // true
console.log(Object.isExtensible(obj));  // false
```

---

## 7. 속성 설명자

### Object.defineProperty() : 속성의 상세 설정

```javascript
const user = {};

Object.defineProperty(user, "name", {
  value: "John",
  writable: true,    // 수정 가능
  enumerable: true,  // for...in에서 열거됨
  configurable: true // 재설정 가능
});

user.name = "Jane";  // OK
console.log(user.name);  // Jane
```

### Object.defineProperties() : 여러 속성 동시 설정

```javascript
const user = {};

Object.defineProperties(user, {
  id: {
    value: 1,
    writable: false,
    enumerable: true
  },
  name: {
    value: "John",
    writable: true,
    enumerable: true
  },
  _password: {
    value: "secret",
    writable: true,
    enumerable: false  // 숨겨진 속성
  }
});

console.log(Object.keys(user));  // ['id', 'name']
```

### Object.getOwnPropertyDescriptor() : 속성 설명자 확인

```javascript
const user = {name: "John"};

const descriptor = Object.getOwnPropertyDescriptor(user, "name");
console.log(descriptor);
// {value: 'John', writable: true, enumerable: true, configurable: true}
```

---

## 8. 객체 구조 분해

### 객체 구조 분해 (Destructuring)

```javascript
const user = {
  id: 1,
  name: "John",
  email: "john@example.com",
  address: {
    city: "Seoul",
    zip: "12345"
  }
};

// 기본 분해
const {name, email} = user;
console.log(name);   // "John"
console.log(email);  // "john@example.com"

// 변수 이름 변경
const {name: userName, email: userEmail} = user;
console.log(userName);   // "John"

// 기본값 설정
const {name, phone = "000-0000"} = user;
console.log(phone);  // "000-0000"

// 중첩 분해
const {address: {city, zip}} = user;
console.log(city);  // "Seoul"

// 나머지 속성
const {name, ...rest} = user;
console.log(rest);
// {id: 1, email: 'john@example.com', address: {...}}
```

---

## 9. 객체 변환

### JSON.stringify() : 객체를 JSON 문자열로 변환

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

const json = JSON.stringify(user);
console.log(json);
// '{"name":"John","age":25,"email":"john@example.com"}'

// 들여쓰기 (가독성 좋음)
const prettyJson = JSON.stringify(user, null, 2);
console.log(prettyJson);
// {
//   "name": "John",
//   "age": 25,
//   "email": "john@example.com"
// }

// 특정 속성만 직렬화
const filtered = JSON.stringify(user, ["name", "age"]);
console.log(filtered);  // '{"name":"John","age":25}'
```

### JSON.parse() : JSON 문자열을 객체로 변환

```javascript
const json = '{"name":"John","age":25,"email":"john@example.com"}';
const user = JSON.parse(json);
console.log(user);
// {name: 'John', age: 25, email: 'john@example.com'}
```

---

## 10. 객체 검증 및 타입 체크

### typeof 연산자 : 타입 확인

```javascript
const obj = {a: 1};
const arr = [1, 2, 3];
const fn = () => {};

console.log(typeof obj);   // "object"
console.log(typeof arr);   // "object" (배열도 object)
console.log(typeof fn);    // "function"
console.log(typeof "str"); // "string"
console.log(typeof 123);   // "number"
console.log(typeof true);  // "boolean"
```

### instanceof 연산자 : 인스턴스 확인

```javascript
const obj = {};
const arr = [];
const date = new Date();

console.log(obj instanceof Object);  // true
console.log(arr instanceof Array);   // true
console.log(date instanceof Date);   // true
```

### Object.prototype.toString.call() : 정확한 타입 확인

```javascript
const obj = {};
const arr = [];

console.log(Object.prototype.toString.call(obj));   // [object Object]
console.log(Object.prototype.toString.call(arr));   // [object Array]
console.log(Object.prototype.toString.call(null));  // [object Null]
```

---

## 11. 객체 순회 및 변환

### Object.keys() + map() : 키 순회하며 변환

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

const transformed = Object.keys(user).reduce((acc, key) => {
  acc[key.toUpperCase()] = user[key];
  return acc;
}, {});

console.log(transformed);
// {NAME: 'John', AGE: 25, EMAIL: 'john@example.com'}
```

### Object.entries() + map() : 키-값 쌍 변환

```javascript
const user = {
  name: "John",
  age: 25,
  email: "john@example.com"
};

const doubled = Object.fromEntries(
  Object.entries(user).map(([key, value]) => {
    return [key, typeof value === "number" ? value * 2 : value];
  })
);

console.log(doubled);
// {name: 'John', age: 50, email: 'john@example.com'}
```

### Object.fromEntries() : 키-값 쌍 배열을 객체로 변환

```javascript
const entries = [["name", "John"], ["age", 25], ["email", "john@example.com"]];

const user = Object.fromEntries(entries);
console.log(user);
// {name: 'John', age: 25, email: 'john@example.com'}

// Map에서 객체로 변환
const map = new Map([["a", 1], ["b", 2]]);
const obj = Object.fromEntries(map);
console.log(obj);  // {a: 1, b: 2}
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `Object.keys()` | 모든 키를 배열로 반환 |
| `Object.values()` | 모든 값을 배열로 반환 |
| `Object.entries()` | [키, 값] 쌍 배열 반환 |
| `Object.assign()` | 객체 병합 |
| `Object.create()` | 프로토타입이 있는 객체 생성 |
| `Object.freeze()` | 객체 동결 |
| `Object.seal()` | 객체 봉인 |
| `Object.defineProperty()` | 속성 상세 설정 |
| `JSON.stringify()` | 객체를 JSON 문자열로 변환 |
| `JSON.parse()` | JSON 문자열을 객체로 변환 |
| `Object.fromEntries()` | 키-값 쌍을 객체로 변환 |
| `for...in` | 객체 키 순회 |
| `delete` | 속성 삭제 |
| `in` | 속성 존재 여부 확인 |
| `hasOwnProperty()` | 자신의 속성 여부 확인 |

