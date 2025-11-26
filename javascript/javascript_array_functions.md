# 자바스크립트 배열 함수 정리

## 1. 배열 요소 추가 및 제거

### push() : 배열 끝에 요소 추가 (배열 수정)

```javascript
const arr = [1, 2, 3];
arr.push(4);
console.log(arr);  // [1, 2, 3, 4]

// 여러 요소 추가
arr.push(5, 6);
console.log(arr);  // [1, 2, 3, 4, 5, 6]
```

### pop() : 배열 끝에서 요소 제거 및 반환 (배열 수정)

```javascript
const arr = [1, 2, 3, 4];
const removed = arr.pop();
console.log(removed);  // 4
console.log(arr);      // [1, 2, 3]
```

### unshift() : 배열 앞에 요소 추가 (배열 수정)

```javascript
const arr = [2, 3, 4];
arr.unshift(1);
console.log(arr);  // [1, 2, 3, 4]

// 여러 요소 추가
arr.unshift(-1, 0);
console.log(arr);  // [-1, 0, 1, 2, 3, 4]
```

### shift() : 배열 앞에서 요소 제거 및 반환 (배열 수정)

```javascript
const arr = [1, 2, 3, 4];
const removed = arr.shift();
console.log(removed);  // 1
console.log(arr);      // [2, 3, 4]
```

### splice() : 배열의 특정 위치의 요소를 추가/제거 (배열 수정)

```javascript
const arr = [1, 2, 3, 4, 5];

// 인덱스 2부터 2개 제거
arr.splice(2, 2);
console.log(arr);  // [1, 2, 5]

// 인덱스 1부터 1개 제거하고 'a', 'b' 삽입
const arr2 = [1, 2, 3, 4];
arr2.splice(1, 1, 'a', 'b');
console.log(arr2);  // [1, 'a', 'b', 3, 4]
```

---

## 2. 배열 검색 및 포함 여부

### indexOf() : 요소의 첫 번째 인덱스 반환 (없으면 -1)

```javascript
const arr = [1, 2, 3, 2, 1];
console.log(arr.indexOf(2));   // 1
console.log(arr.indexOf(5));   // -1
```

### lastIndexOf() : 요소의 마지막 인덱스 반환

```javascript
const arr = [1, 2, 3, 2, 1];
console.log(arr.lastIndexOf(2));  // 3
console.log(arr.lastIndexOf(1));  // 4
```

### includes() : 요소 포함 여부 반환 (boolean)

```javascript
const arr = [1, 2, 3, 4];
console.log(arr.includes(2));  // true
console.log(arr.includes(5));  // false
```

### find() : 조건을 만족하는 첫 번째 요소 반환

```javascript
const arr = [1, 2, 3, 4, 5];
const result = arr.find(num => num > 3);
console.log(result);  // 4

const users = [{id: 1, name: 'John'}, {id: 2, name: 'Jane'}];
const user = users.find(u => u.id === 2);
console.log(user);  // {id: 2, name: 'Jane'}
```

### findIndex() : 조건을 만족하는 첫 번째 요소의 인덱스 반환

```javascript
const arr = [1, 2, 3, 4, 5];
const index = arr.findIndex(num => num > 3);
console.log(index);  // 3
```

### some() : 조건을 만족하는 요소가 하나라도 있는지 확인 (boolean)

```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.some(num => num > 3));  // true
console.log(arr.some(num => num > 10)); // false
```

### every() : 모든 요소가 조건을 만족하는지 확인 (boolean)

```javascript
const arr = [2, 4, 6, 8];
console.log(arr.every(num => num % 2 === 0));  // true (모두 짝수)

const arr2 = [2, 3, 4, 6];
console.log(arr2.every(num => num % 2 === 0)); // false (3이 홀수)
```

---

## 3. 배열 변환 및 필터링

### map() : 각 요소에 함수를 적용하여 새 배열 반환

```javascript
const arr = [1, 2, 3, 4];
const doubled = arr.map(num => num * 2);
console.log(doubled);  // [2, 4, 6, 8]

const users = [{id: 1, name: 'John'}, {id: 2, name: 'Jane'}];
const names = users.map(u => u.name);
console.log(names);  // ['John', 'Jane']
```

### filter() : 조건을 만족하는 요소만으로 새 배열 반환

```javascript
const arr = [1, 2, 3, 4, 5];
const evenNumbers = arr.filter(num => num % 2 === 0);
console.log(evenNumbers);  // [2, 4]

const users = [{id: 1, name: 'John', age: 25}, {id: 2, name: 'Jane', age: 30}];
const adults = users.filter(u => u.age >= 30);
console.log(adults);  // [{id: 2, name: 'Jane', age: 30}]
```

### reduce() : 배열의 모든 요소를 순회하며 하나의 값으로 축약

```javascript
const arr = [1, 2, 3, 4];
const sum = arr.reduce((acc, num) => acc + num, 0);
console.log(sum);  // 10

// 곱하기
const product = arr.reduce((acc, num) => acc * num, 1);
console.log(product);  // 24

// 객체로 변환
const users = [{id: 1, name: 'John'}, {id: 2, name: 'Jane'}];
const userMap = users.reduce((acc, u) => {
  acc[u.id] = u.name;
  return acc;
}, {});
console.log(userMap);  // {1: 'John', 2: 'Jane'}
```

### reduceRight() : 오른쪽에서부터 요소를 순회하며 축약

```javascript
const arr = [1, 2, 3, 4];
const result = arr.reduceRight((acc, num) => acc - num, 0);
console.log(result);  // -2 (0 - 4 - 3 - 2 - 1)
```

---

## 4. 배열 정렬 및 역순

### sort() : 배열을 정렬 (배열 수정)

```javascript
const arr = [3, 1, 4, 1, 5];
arr.sort();
console.log(arr);  // [1, 1, 3, 4, 5]

// 숫자 정렬 (문자열 비교 피하기)
const numbers = [30, 10, 5, 20];
numbers.sort((a, b) => a - b);
console.log(numbers);  // [5, 10, 20, 30]

// 내림차순
numbers.sort((a, b) => b - a);
console.log(numbers);  // [30, 20, 10, 5]

// 객체 배열 정렬
const users = [{id: 3, name: 'John'}, {id: 1, name: 'Jane'}, {id: 2, name: 'Bob'}];
users.sort((a, b) => a.id - b.id);
console.log(users);  // id 순서로 정렬됨
```

### reverse() : 배열을 역순으로 정렬 (배열 수정)

```javascript
const arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr);  // [5, 4, 3, 2, 1]
```

---

## 5. 배열 결합 및 추출

### concat() : 여러 배열을 결합하여 새 배열 반환

```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const arr3 = [5, 6];
const combined = arr1.concat(arr2, arr3);
console.log(combined);  // [1, 2, 3, 4, 5, 6]

// 요소도 함께 추가 가능
const result = arr1.concat(2.5, arr2);
console.log(result);  // [1, 2, 2.5, 3, 4]
```

### slice() : 배열의 일부를 추출하여 새 배열 반환

```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.slice(1, 4));    // [2, 3, 4]
console.log(arr.slice(2));       // [3, 4, 5]
console.log(arr.slice(-2));      // [4, 5]
console.log(arr.slice());        // [1, 2, 3, 4, 5] (복사본)
```

### join() : 배열의 요소들을 구분자로 연결하여 문자열 반환

```javascript
const arr = [1, 2, 3, 4];
console.log(arr.join());       // 1,2,3,4
console.log(arr.join("-"));    // 1-2-3-4
console.log(arr.join(" "));    // 1 2 3 4
```

### split() : 문자열을 구분자로 나누어 배열 반환 (String 메소드)

```javascript
const text = "apple,banana,orange";
const arr = text.split(",");
console.log(arr);  // ['apple', 'banana', 'orange']
```

---

## 6. 배열 생성

### Array.from() : 유사 배열 또는 반복 가능한 객체를 배열로 변환

```javascript
// 문자열을 배열로
console.log(Array.from("hello"));  // ['h', 'e', 'l', 'l', 'o']

// 숫자 범위 생성
const range = Array.from({length: 5}, (_, i) => i);
console.log(range);  // [0, 1, 2, 3, 4]

// NodeList를 배열로
const elements = Array.from(document.querySelectorAll('.item'));
```

### Array.of() : 전달된 요소들로 배열 생성

```javascript
console.log(Array.of(1, 2, 3));     // [1, 2, 3]
console.log(Array.of(undefined));   // [undefined]
console.log(Array(5));              // [ , , , , ] (5개의 빈 요소)
console.log(Array.of(5));           // [5]
```

### 배열 리터럴

```javascript
const arr = [1, 2, 3, 4];
const arr2 = new Array(1, 2, 3, 4);
```

---

## 7. 배열 길이 및 확인

### length : 배열의 요소 개수

```javascript
const arr = [1, 2, 3, 4];
console.log(arr.length);  // 4

// 길이 수정
arr.length = 2;
console.log(arr);  // [1, 2]
```

### Array.isArray() : 주어진 값이 배열인지 확인

```javascript
console.log(Array.isArray([1, 2, 3]));    // true
console.log(Array.isArray("hello"));      // false
console.log(Array.isArray({a: 1}));       // false
console.log(Array.isArray(null));         // false
```

---

## 8. 배열 순회

### forEach() : 각 요소에 대해 콜백 함수 실행

```javascript
const arr = [1, 2, 3, 4];
arr.forEach(num => {
  console.log(num);
});
// 1, 2, 3, 4

arr.forEach((num, index) => {
  console.log(`Index ${index}: ${num}`);
});

const users = [{id: 1, name: 'John'}, {id: 2, name: 'Jane'}];
users.forEach(u => console.log(u.name));
```

### for...of : 배열 요소 직접 순회

```javascript
const arr = [1, 2, 3, 4];
for (const num of arr) {
  console.log(num);
}

// break, continue 사용 가능
for (const num of arr) {
  if (num === 3) break;
  console.log(num);
}
```

---

## 9. 배열 평탄화

### flat() : 중첩된 배열을 평탄화

```javascript
const arr = [1, [2, 3], [4, [5, 6]]];
console.log(arr.flat());        // [1, 2, 3, 4, [5, 6]] (1단계)
console.log(arr.flat(2));       // [1, 2, 3, 4, 5, 6] (2단계)
console.log(arr.flat(Infinity)); // [1, 2, 3, 4, 5, 6] (모두 평탄화)
```

### flatMap() : map() 후 1단계 flat()

```javascript
const arr = [1, 2, 3];
const result = arr.flatMap(num => [num, num * 2]);
console.log(result);  // [1, 2, 2, 4, 3, 6]
```

---

## 10. 배열 생성 및 채우기

### fill() : 배열의 모든 요소를 특정 값으로 채우기 (배열 수정)

```javascript
const arr = [1, 2, 3, 4, 5];
arr.fill(0);
console.log(arr);  // [0, 0, 0, 0, 0]

// 특정 범위 채우기
const arr2 = [1, 2, 3, 4, 5];
arr2.fill(0, 2, 4);
console.log(arr2);  // [1, 2, 0, 0, 5]
```

### Array.from() with length : 특정 길이의 배열 생성

```javascript
// 0부터 4까지 배열 생성
const arr = Array.from({length: 5}, (_, i) => i);
console.log(arr);  // [0, 1, 2, 3, 4]

// 특정 값으로 채워진 배열
const arr2 = Array.from({length: 3}, () => 0);
console.log(arr2);  // [0, 0, 0]
```

---

## 11. 배열 전개 연산자

### Spread Operator (...) : 배열 펼치기

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// 배열 결합
const combined = [...arr1, ...arr2];
console.log(combined);  // [1, 2, 3, 4, 5, 6]

// 배열 복사
const copy = [...arr1];
console.log(copy);  // [1, 2, 3]

// 중간에 요소 추가
const withNew = [...arr1, 3.5, ...arr2];
console.log(withNew);  // [1, 2, 3, 3.5, 4, 5, 6]
```

---

## 12. 배열 구조 분해

### 배열 구조 분해 (Destructuring)

```javascript
const arr = [1, 2, 3, 4, 5];

// 기본
const [a, b, c] = arr;
console.log(a, b, c);  // 1, 2, 3

// 건너뛰기
const [x, , z] = arr;
console.log(x, z);  // 1, 3

// 나머지 요소
const [first, ...rest] = arr;
console.log(first);  // 1
console.log(rest);   // [2, 3, 4, 5]
```

---

## 요약 테이블

| 함수 | 설명 | 배열 수정 |
|------|------|----------|
| `push()` | 끝에 요소 추가 | O |
| `pop()` | 끝에서 요소 제거 | O |
| `shift()` | 앞에서 요소 제거 | O |
| `unshift()` | 앞에 요소 추가 | O |
| `splice()` | 특정 위치에서 추가/제거 | O |
| `map()` | 각 요소 변환 | X |
| `filter()` | 조건 만족 요소 필터링 | X |
| `reduce()` | 배열 축약 | X |
| `find()` | 조건 만족 첫 요소 찾기 | X |
| `includes()` | 요소 포함 여부 확인 | X |
| `indexOf()` | 요소 위치 찾기 | X |
| `some()` | 일부 요소가 조건 만족 | X |
| `every()` | 모든 요소가 조건 만족 | X |
| `sort()` | 배열 정렬 | O |
| `reverse()` | 배열 역순 | O |
| `concat()` | 배열 결합 | X |
| `slice()` | 일부 추출 | X |
| `join()` | 문자열로 연결 | X |
| `forEach()` | 각 요소 순회 | X |
| `flat()` | 배열 평탄화 | X |

