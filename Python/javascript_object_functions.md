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
  age: 25
};

console.log(Object.entries(user));
// [["name", "John"], ["age", 25]]
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
```

### 속성 수정 : 기존 속성 값 변경

```javascript
const user = {
  name: "John",
  age: 25
};

user.name = "Jane";
user["age"] = 30;
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

---

## 4. 객체 병합 및 복사

### Object.assign() : 여러 객체를 병합

```javascript
const obj1 = {a: 1, b: 2};
const obj2 = {b: 3, c: 4};

const merged = Object.assign({}, obj1, obj2);
console.log(merged);
// {a: 1, b: 3, c: 4}
```

### Spread Operator (...) : 객체 펼치기 및 병합

```javascript
const obj1 = {a: 1, b: 2};
const obj2 = {b: 3, c: 4};

const merged = {...obj1, ...obj2};
console.log(merged);
// {a: 1, b: 3, c: 4}

const copy = {...obj1};
console.log(copy);
// {a: 1, b: 2}
```

---

## 5. 객체 구조 분해

### 객체 구조 분해

```javascript
const user = {
  id: 1,
  name: "John",
  email: "john@example.com"
};

const {name, email} = user;
console.log(name, email);  // John, john@example.com

// 변수 이름 변경
const {name: userName, email: userEmail} = user;
console.log(userName, userEmail);

// 기본값 설정
const {name, phone = "000-0000"} = user;
console.log(phone);  // "000-0000"
```

---

## 6. 객체 변환

### JSON.stringify() : 객체를 JSON 문자열로 변환

```javascript
const user = {
  name: "John",
  age: 25
};

const json = JSON.stringify(user);
console.log(json);
// '{"name":"John","age":25}'
```

### JSON.parse() : JSON 문자열을 객체로 변환

```javascript
const json = '{"name":"John","age":25}';
const user = JSON.parse(json);
console.log(user);
// {name: 'John', age: 25}
```

---

## 7. 객체 검증 및 타입 체크

### typeof 연산자 : 타입 확인

```javascript
const obj = {a: 1};
const arr = [1, 2, 3];

console.log(typeof obj);   // "object"
console.log(typeof arr);   // "object"
console.log(typeof "str"); // "string"
```

### Array.isArray() : 배열 확인

```javascript
console.log(Array.isArray([1, 2, 3]));    // true
console.log(Array.isArray("hello"));      // false
console.log(Array.isArray({a: 1}));       // false
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `Object.keys()` | 모든 키를 배열로 반환 |
| `Object.values()` | 모든 값을 배열로 반환 |
| `Object.entries()` | [키, 값] 쌍 배열 반환 |
| `Object.assign()` | 객체 병합 |
| `JSON.stringify()` | 객체를 JSON 문자열로 변환 |
| `JSON.parse()` | JSON 문자열을 객체로 변환 |
| `delete` | 속성 삭제 |
| `in` | 속성 존재 여부 확인 |
