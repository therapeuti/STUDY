# 자바스크립트 배열 함수 정리

## 1. 배열 요소 추가 및 제거

### push() : 배열 끝에 요소 추가

```javascript
const arr = [1, 2, 3];
arr.push(4);
console.log(arr);  // [1, 2, 3, 4]
```

### pop() : 배열 끝에서 요소 제거

```javascript
const arr = [1, 2, 3, 4];
const removed = arr.pop();
console.log(removed);  // 4
console.log(arr);      // [1, 2, 3]
```

---

## 2. 배열 검색

### indexOf() : 요소의 첫 번째 인덱스 반환

```javascript
const arr = [1, 2, 3, 2, 1];
console.log(arr.indexOf(2));   // 1
```

### includes() : 요소 포함 여부 반환

```javascript
const arr = [1, 2, 3, 4];
console.log(arr.includes(2));  // true
```

### find() : 조건을 만족하는 첫 번째 요소 반환

```javascript
const arr = [1, 2, 3, 4, 5];
const result = arr.find(num => num > 3);
console.log(result);  // 4
```

---

## 3. 배열 변환

### map() : 각 요소에 함수를 적용하여 새 배열 반환

```javascript
const arr = [1, 2, 3, 4];
const doubled = arr.map(num => num * 2);
console.log(doubled);  // [2, 4, 6, 8]
```

### filter() : 조건을 만족하는 요소만으로 새 배열 반환

```javascript
const arr = [1, 2, 3, 4, 5];
const evens = arr.filter(num => num % 2 === 0);
console.log(evens);  // [2, 4]
```

### reduce() : 배열의 모든 요소를 순회하며 하나의 값으로 축약

```javascript
const arr = [1, 2, 3, 4];
const sum = arr.reduce((acc, num) => acc + num, 0);
console.log(sum);  // 10
```

---

## 4. 배열 정렬

### sort() : 배열을 정렬

```javascript
const arr = [3, 1, 4, 1, 5];
arr.sort();
console.log(arr);  // [1, 1, 3, 4, 5]

// 숫자 정렬
const numbers = [30, 10, 5, 20];
numbers.sort((a, b) => a - b);
console.log(numbers);  // [5, 10, 20, 30]
```

### reverse() : 배열을 역순으로 정렬

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
const combined = arr1.concat(arr2);
console.log(combined);  // [1, 2, 3, 4]
```

### slice() : 배열의 일부를 추출하여 새 배열 반환

```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.slice(1, 4));    // [2, 3, 4]
console.log(arr.slice(2));       // [3, 4, 5]
```

### join() : 배열의 요소들을 구분자로 연결하여 문자열 반환

```javascript
const arr = [1, 2, 3, 4];
console.log(arr.join());       // 1,2,3,4
console.log(arr.join("-"));    // 1-2-3-4
```

---

## 6. 배열 길이

### length : 배열의 요소 개수

```javascript
const arr = [1, 2, 3, 4];
console.log(arr.length);  // 4
```

---

## 7. 배열 순회

### forEach() : 각 요소에 대해 콜백 함수 실행

```javascript
const arr = [1, 2, 3, 4];
arr.forEach(num => {
  console.log(num);
});
```

---

## 8. 배열 전개

### Spread Operator (...) : 배열 펼치기

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];
console.log(combined);  // [1, 2, 3, 4, 5, 6]
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `push()` | 끝에 요소 추가 |
| `pop()` | 끝에서 요소 제거 |
| `shift()` | 앞에서 요소 제거 |
| `unshift()` | 앞에 요소 추가 |
| `map()` | 각 요소 변환 |
| `filter()` | 조건 만족 요소 필터링 |
| `reduce()` | 배열 축약 |
| `find()` | 조건 만족 첫 요소 찾기 |
| `includes()` | 요소 포함 여부 확인 |
| `indexOf()` | 요소 위치 찾기 |
| `sort()` | 배열 정렬 |
| `reverse()` | 배열 역순 |
| `concat()` | 배열 결합 |
| `slice()` | 일부 추출 |
| `join()` | 문자열로 연결 |
| `forEach()` | 각 요소 순회 |
