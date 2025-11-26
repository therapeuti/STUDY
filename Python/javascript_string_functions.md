# 자바스크립트 문자열 함수 정리

## 1. 문자열 대소문자 변환

### toUpperCase() : 모든 문자를 대문자로 변환

```javascript
const text = "hello world";
console.log(text.toUpperCase());  // HELLO WORLD
```

### toLowerCase() : 모든 문자를 소문자로 변환

```javascript
const text = "HELLO WORLD";
console.log(text.toLowerCase());  // hello world
```

---

## 2. 문자열 검색 및 위치

### indexOf() : 부분 문자열의 위치를 찾음 (없으면 -1 반환)

```javascript
const text = "hello world";
console.log(text.indexOf("world"));  // 6
console.log(text.indexOf("xyz"));    // -1
```

### includes() : 문자열 포함 여부를 boolean으로 반환

```javascript
const text = "hello world";
console.log(text.includes("world"));  // true
console.log(text.includes("xyz"));    // false
```

---

## 3. 문자열 분할 및 결합

### split() : 문자열을 구분자로 분할하여 배열 반환

```javascript
const text = "hello world python";
console.log(text.split(" "));  // ['hello', 'world', 'python']

const text2 = "apple,banana,orange";
console.log(text2.split(","));  // ['apple', 'banana', 'orange']
```

---

## 4. 문자열 공백 처리

### trim() : 문자열의 양쪽 끝에서 공백 제거

```javascript
const text = "  hello world  ";
console.log(text.trim());  // hello world
```

---

## 5. 문자열 길이 및 문자 접근

### length : 문자열의 길이 반환

```javascript
const text = "hello";
console.log(text.length);  // 5
```

### slice() : 문자열의 일부를 추출

```javascript
const text = "hello world";
console.log(text.slice(0, 5));   // hello
console.log(text.slice(6));      // world
```

---

## 6. 문자열 포함 여부 확인

### startsWith() : 문자열이 특정 문자로 시작하는지 확인

```javascript
const text = "hello world";
console.log(text.startsWith("hello"));  // true
```

### endsWith() : 문자열이 특정 문자로 끝나는지 확인

```javascript
const text = "hello world";
console.log(text.endsWith("world"));  // true
```

---

## 7. 문자열 치환

### replace() : 부분 문자열을 다른 문자열로 치환

```javascript
const text = "hello world world";
console.log(text.replace("world", "python"));  // hello python world
```

### replaceAll() : 모든 부분 문자열을 다른 문자열로 치환

```javascript
const text = "hello world world";
console.log(text.replaceAll("world", "python"));  // hello python python
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `toUpperCase()` | 대문자로 변환 |
| `toLowerCase()` | 소문자로 변환 |
| `indexOf()` | 부분 문자열 위치 검색 |
| `includes()` | 부분 문자열 포함 여부 확인 |
| `split()` | 구분자로 분할 |
| `trim()` | 양쪽 공백 제거 |
| `slice()` | 문자열 일부 추출 |
| `startsWith()` | 특정 문자로 시작하는지 확인 |
| `endsWith()` | 특정 문자로 끝나는지 확인 |
| `replace()` | 부분 문자열 치환 |
| `replaceAll()` | 모든 부분 문자열 치환 |
