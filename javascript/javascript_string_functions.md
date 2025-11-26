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

### lastIndexOf() : 오른쪽에서부터 부분 문자열을 찾음

```javascript
const text = "hello hello world";
console.log(text.lastIndexOf("hello"));  // 6
```

### includes() : 문자열 포함 여부를 boolean으로 반환

```javascript
const text = "hello world";
console.log(text.includes("world"));  // true
console.log(text.includes("xyz"));    // false
```

### search() : 정규표현식으로 검색하여 위치 반환

```javascript
const text = "hello world";
console.log(text.search("world"));  // 6
console.log(text.search(/w/));      // 6
```

---

## 3. 문자열 포함 여부 확인

### startsWith() : 문자열이 특정 문자로 시작하는지 확인

```javascript
const text = "hello world";
console.log(text.startsWith("hello"));  // true
console.log(text.startsWith("world"));  // false
```

### endsWith() : 문자열이 특정 문자로 끝나는지 확인

```javascript
const text = "hello world";
console.log(text.endsWith("world"));  // true
console.log(text.endsWith("hello"));  // false
```

---

## 4. 문자열 치환

### replace() : 첫 번째 부분 문자열을 다른 문자열로 치환

```javascript
const text = "hello world world";
console.log(text.replace("world", "python"));  // hello python world
```

### replaceAll() : 모든 부분 문자열을 다른 문자열로 치환

```javascript
const text = "hello world world";
console.log(text.replaceAll("world", "python"));  // hello python python

// 정규표현식 사용
console.log(text.replace(/world/g, "python"));  // hello python python
```

---

## 5. 문자열 분할 및 결합

### split() : 문자열을 구분자로 분할하여 배열 반환

```javascript
const text = "hello world python";
console.log(text.split(" "));  // ['hello', 'world', 'python']

const text2 = "apple,banana,orange";
console.log(text2.split(","));  // ['apple', 'banana', 'orange']

// 분할 개수 제한
const text3 = "a,b,c,d";
console.log(text3.split(",", 2));  // ['a', 'b']
```

### join() : 배열의 요소들을 구분자로 연결하여 문자열 생성

```javascript
const words = ["hello", "world", "python"];
console.log(words.join(" "));  // hello world python
console.log(words.join("-"));  // hello-world-python
```

---

## 6. 문자열 공백 처리

### trim() : 문자열의 양쪽 끝에서 공백 제거

```javascript
const text = "  hello world  ";
console.log(text.trim());  // hello world
```

### trimStart() / trimLeft() : 왼쪽 끝에서만 공백 제거

```javascript
const text = "  hello world  ";
console.log(text.trimStart());  // hello world
console.log(text.trimLeft());   // hello world  (같음)
```

### trimEnd() / trimRight() : 오른쪽 끝에서만 공백 제거

```javascript
const text = "  hello world  ";
console.log(text.trimEnd());   // "  hello world"
console.log(text.trimRight()); // "  hello world" (같음)
```

---

## 7. 문자열 포맷팅

### Template Literals (템플릿 리터럴) : 문자열에 변수를 직접 삽입

```javascript
const name = "John";
const age = 25;
console.log(`${name} is ${age} years old`);  // John is 25 years old

// 표현식 포함
const x = 10;
const y = 20;
console.log(`${x} + ${y} = ${x + y}`);  // 10 + 20 = 30
```

### concat() : 여러 문자열을 연결

```javascript
const text1 = "hello";
const text2 = "world";
console.log(text1.concat(" ", text2));  // hello world
```

### repeat() : 문자열을 지정된 횟수만큼 반복

```javascript
const text = "abc";
console.log(text.repeat(3));  // abcabcabc
```

---

## 8. 문자열 길이 및 문자 접근

### length : 문자열의 길이 반환

```javascript
const text = "hello";
console.log(text.length);  // 5
```

### 인덱싱 : 특정 위치의 문자 접근

```javascript
const text = "hello";
console.log(text[0]);      // h
console.log(text[4]);      // o
console.log(text[text.length - 1]);  // o (마지막 문자)
```

### charAt() : 지정된 위치의 문자 반환

```javascript
const text = "hello";
console.log(text.charAt(0));  // h
console.log(text.charAt(4));  // o
```

### charCodeAt() : 지정된 위치의 문자의 유니코드 값 반환

```javascript
console.log("A".charCodeAt(0));  // 65
console.log("a".charCodeAt(0));  // 97
```

### substring() : 문자열의 일부를 추출 (음수 처리 안됨)

```javascript
const text = "hello world";
console.log(text.substring(0, 5));   // hello
console.log(text.substring(6));      // world
```

### substr() : 문자열의 일부를 추출 (deprecated - 사용 권장하지 않음)

```javascript
const text = "hello world";
console.log(text.substr(0, 5));   // hello
console.log(text.substr(6, 5));   // world
```

### slice() : 문자열의 일부를 추출 (음수 인덱스 지원)

```javascript
const text = "hello world";
console.log(text.slice(0, 5));   // hello
console.log(text.slice(6));      // world
console.log(text.slice(-5));     // world
console.log(text.slice(1, -1));  // ello worl
```

---

## 9. 문자열 변환 및 확인

### isNaN() / Number.isNaN() : 숫자인지 확인

```javascript
console.log(isNaN("123"));       // false (숫자로 변환 가능)
console.log(isNaN("abc"));       // true
console.log(Number.isNaN("123")); // false (더 정확한 확인)
```

### parseInt() / parseFloat() : 문자열을 숫자로 변환

```javascript
console.log(parseInt("123"));        // 123
console.log(parseInt("123.45"));     // 123
console.log(parseFloat("123.45"));   // 123.45
```

### Number() : 문자열을 숫자로 변환

```javascript
console.log(Number("123"));      // 123
console.log(Number("123.45"));   // 123.45
console.log(Number("abc"));      // NaN
```

### String() : 다른 타입을 문자열로 변환

```javascript
console.log(String(123));     // "123"
console.log(String(true));    // "true"
console.log(String(null));    // "null"
```

---

## 10. 문자열 정렬 및 패딩

### padStart() : 문자열의 앞에 특정 문자를 채우기

```javascript
const text = "5";
console.log(text.padStart(3, "0"));  // 005
console.log(text.padStart(5, "*"));  // ****5
```

### padEnd() : 문자열의 뒤에 특정 문자를 채우기

```javascript
const text = "5";
console.log(text.padEnd(3, "0"));   // 500
console.log(text.padEnd(5, "*"));   // 5****
```

---

## 11. 문자열 패턴 매칭

### match() : 정규표현식과 일치하는 부분 배열 반환

```javascript
const text = "hello world hello";
console.log(text.match(/hello/));    // ['hello']
console.log(text.match(/hello/g));   // ['hello', 'hello']
```

### matchAll() : 정규표현식과 일치하는 모든 부분의 반복자 반환

```javascript
const text = "hello world hello";
const matches = [...text.matchAll(/hello/g)];
console.log(matches);  // 모든 매칭 결과
```

---

## 12. 기타 유용한 함수

### toString() : 값을 문자열로 변환

```javascript
const num = 123;
console.log(num.toString());  // "123"

const arr = [1, 2, 3];
console.log(arr.toString());  // "1,2,3"
```

### valueOf() : 문자열의 원시값 반환

```javascript
const text = new String("hello");
console.log(text.valueOf());  // "hello"
```

### localeCompare() : 문자열 비교 (알파벳 순서)

```javascript
console.log("a".localeCompare("b"));   // -1 (a가 앞)
console.log("b".localeCompare("a"));   // 1  (b가 뒤)
console.log("a".localeCompare("a"));   // 0  (같음)
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `toUpperCase()` | 대문자로 변환 |
| `toLowerCase()` | 소문자로 변환 |
| `indexOf()` | 부분 문자열 위치 검색 |
| `includes()` | 부분 문자열 포함 여부 확인 |
| `replace()` | 부분 문자열 치환 |
| `replaceAll()` | 모든 부분 문자열 치환 |
| `split()` | 구분자로 분할 |
| `join()` | 배열을 문자열로 연결 |
| `trim()` | 양쪽 공백 제거 |
| `slice()` | 문자열 일부 추출 |
| `substring()` | 문자열 일부 추출 |
| `charAt()` | 특정 위치 문자 반환 |
| `startsWith()` | 특정 문자로 시작하는지 확인 |
| `endsWith()` | 특정 문자로 끝나는지 확인 |
| `repeat()` | 문자열 반복 |
| `padStart()` | 앞에 문자 채우기 |
| `padEnd()` | 뒤에 문자 채우기 |

