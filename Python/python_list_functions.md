# 파이썬 리스트 함수 정리

## 1. 리스트 생성

### list() : 리스트 생성

```python
# 빈 리스트
lst = list()
print(lst)  # []

# 다른 시퀀스를 리스트로 변환
lst = list("hello")
print(lst)  # ['h', 'e', 'l', 'l', 'o']

lst = list(range(5))
print(lst)  # [0, 1, 2, 3, 4]
```

### 리터럴 표기법 : [] 으로 직접 생성

```python
lst = []
print(lst)  # []

lst = [1, 2, 3, 4, 5]
print(lst)  # [1, 2, 3, 4, 5]

lst = ['apple', 'banana', 'orange']
print(lst)  # ['apple', 'banana', 'orange']

# 혼합 타입
lst = [1, 'hello', 3.14, True]
print(lst)  # [1, 'hello', 3.14, True]
```

---

## 2. 요소 접근

### [] : 인덱스로 요소 접근

```python
lst = [10, 20, 30, 40, 50]
print(lst[0])   # 10
print(lst[2])   # 30
print(lst[-1])  # 50 (마지막 요소)
print(lst[-2])  # 40 (마지막에서 두 번째)
```

### 슬라이싱 : 리스트의 일부 추출

```python
lst = [10, 20, 30, 40, 50]
print(lst[1:4])    # [20, 30, 40]
print(lst[:3])     # [10, 20, 30]
print(lst[2:])     # [30, 40, 50]
print(lst[::2])    # [10, 30, 50] (2칸씩)
print(lst[::-1])   # [50, 40, 30, 20, 10] (역순)
```

---

## 3. 요소 추가

### append() : 리스트 끝에 요소 추가

```python
lst = [1, 2, 3]
lst.append(4)
print(lst)  # [1, 2, 3, 4]

lst.append('hello')
print(lst)  # [1, 2, 3, 4, 'hello']
```

### insert() : 지정한 위치에 요소 추가

```python
lst = [1, 2, 4, 5]
lst.insert(2, 3)
print(lst)  # [1, 2, 3, 4, 5]

lst.insert(0, 0)
print(lst)  # [0, 1, 2, 3, 4, 5]
```

### extend() : 리스트의 끝에 다른 리스트의 모든 요소 추가

```python
lst = [1, 2, 3]
lst.extend([4, 5, 6])
print(lst)  # [1, 2, 3, 4, 5, 6]

# 문자열도 가능 (각 문자가 요소로 추가됨)
lst = ['a', 'b']
lst.extend('cd')
print(lst)  # ['a', 'b', 'c', 'd']
```

### += 연산자 : extend()와 동일

```python
lst = [1, 2, 3]
lst += [4, 5, 6]
print(lst)  # [1, 2, 3, 4, 5, 6]
```

---

## 4. 요소 제거

### remove() : 첫 번째 해당 값을 제거

```python
lst = [1, 2, 3, 2, 4]
lst.remove(2)
print(lst)  # [1, 3, 2, 4]

# 없는 값 제거 시 ValueError 발생
# lst.remove(10)  # ValueError
```

### pop() : 지정한 인덱스의 요소를 제거하고 반환

```python
lst = [1, 2, 3, 4, 5]
value = lst.pop()
print(value)  # 5
print(lst)    # [1, 2, 3, 4]

value = lst.pop(1)
print(value)  # 2
print(lst)    # [1, 3, 4]

# 빈 리스트에서 pop 시 IndexError 발생
# [].pop()  # IndexError
```

### del : 지정한 인덱스의 요소 삭제 (또는 슬라이스)

```python
lst = [1, 2, 3, 4, 5]
del lst[2]
print(lst)  # [1, 2, 4, 5]

# 슬라이스 삭제
lst = [1, 2, 3, 4, 5]
del lst[1:4]
print(lst)  # [1, 5]
```

### clear() : 모든 요소 삭제

```python
lst = [1, 2, 3, 4, 5]
lst.clear()
print(lst)  # []
```

---

## 5. 요소 검색

### index() : 첫 번째 해당 값의 인덱스 반환

```python
lst = [10, 20, 30, 20, 40]
print(lst.index(20))  # 1

print(lst.index(40))  # 4

# 없는 값 검색 시 ValueError 발생
# lst.index(50)  # ValueError
```

### count() : 해당 값이 몇 개인지 세기

```python
lst = [1, 2, 2, 3, 2, 4]
print(lst.count(2))  # 3

print(lst.count(1))  # 1

print(lst.count(5))  # 0
```

### in : 요소가 리스트에 있는지 확인

```python
lst = [1, 2, 3, 4, 5]
print(1 in lst)   # True
print(10 in lst)  # False
```

---

## 6. 리스트 정렬 및 역순

### sort() : 리스트를 제자리에서 정렬 (원본 변경)

```python
lst = [3, 1, 4, 1, 5, 9, 2, 6]
lst.sort()
print(lst)  # [1, 1, 2, 3, 4, 5, 6, 9]

# 역순 정렬
lst = [3, 1, 4, 1, 5]
lst.sort(reverse=True)
print(lst)  # [5, 4, 3, 1, 1]

# 문자열 정렬
lst = ['banana', 'apple', 'cherry']
lst.sort()
print(lst)  # ['apple', 'banana', 'cherry']
```

### sorted() : 정렬된 새로운 리스트 반환 (원본 유지)

```python
lst = [3, 1, 4, 1, 5]
sorted_lst = sorted(lst)
print(sorted_lst)  # [1, 1, 3, 4, 5]
print(lst)         # [3, 1, 4, 1, 5] (원본 유지)

# 역순 정렬
sorted_lst = sorted(lst, reverse=True)
print(sorted_lst)  # [5, 4, 3, 1, 1]
```

### reverse() : 리스트를 역순으로 정렬 (원본 변경)

```python
lst = [1, 2, 3, 4, 5]
lst.reverse()
print(lst)  # [5, 4, 3, 2, 1]
```

### 슬라이싱으로 역순 : 원본 유지

```python
lst = [1, 2, 3, 4, 5]
reversed_lst = lst[::-1]
print(reversed_lst)  # [5, 4, 3, 2, 1]
print(lst)           # [1, 2, 3, 4, 5] (원본 유지)
```

---

## 7. 리스트 복사

### copy() : 얕은 복사본 생성

```python
lst = [1, 2, 3]
lst_copy = lst.copy()
lst_copy[0] = 10
print(lst)       # [1, 2, 3]
print(lst_copy)  # [10, 2, 3]
```

### 슬라이싱으로 복사 : [:] 사용

```python
lst = [1, 2, 3]
lst_copy = lst[:]
lst_copy[0] = 10
print(lst)       # [1, 2, 3]
print(lst_copy)  # [10, 2, 3]
```

### 깊은 복사 : copy.deepcopy() 사용 (중첩된 리스트의 경우)

```python
import copy

lst = [1, [2, 3], 4]
lst_shallow = lst.copy()
lst_deep = copy.deepcopy(lst)

# 얕은 복사: 중첩 객체는 참조
lst_shallow[1][0] = 20
print(lst[1])  # [20, 3] (원본도 변경됨)

# 깊은 복사: 완전히 독립적
lst_deep[1][0] = 30
print(lst[1])  # [20, 3] (원본은 변경 안 됨)
```

---

## 8. 리스트 길이 및 합계

### len() : 리스트의 길이 반환

```python
lst = [1, 2, 3, 4, 5]
print(len(lst))  # 5

lst = []
print(len(lst))  # 0
```

### sum() : 리스트 요소의 합계 반환

```python
lst = [1, 2, 3, 4, 5]
print(sum(lst))  # 15

# 초기값 설정
lst = [1, 2, 3]
print(sum(lst, 10))  # 16
```

### max() : 최댓값 반환

```python
lst = [3, 1, 4, 1, 5, 9]
print(max(lst))  # 9

lst = ['apple', 'banana', 'cherry']
print(max(lst))  # cherry
```

### min() : 최솟값 반환

```python
lst = [3, 1, 4, 1, 5, 9]
print(min(lst))  # 1

lst = ['apple', 'banana', 'cherry']
print(min(lst))  # apple
```

---

## 9. 리스트 순회

### for 루프로 순회

```python
lst = [1, 2, 3, 4, 5]
for item in lst:
    print(item)  # 1, 2, 3, 4, 5
```

### enumerate() : 인덱스와 요소를 함께 순회

```python
lst = ['apple', 'banana', 'cherry']
for index, item in enumerate(lst):
    print(f"{index}: {item}")
# 0: apple
# 1: banana
# 2: cherry

# 시작 인덱스 지정
for index, item in enumerate(lst, 1):
    print(f"{index}: {item}")
# 1: apple
# 2: banana
# 3: cherry
```

---

## 10. 리스트 이해식 (List Comprehension)

### 기본 형태 : 새로운 리스트 생성

```python
# 기본
lst = [x for x in range(5)]
print(lst)  # [0, 1, 2, 3, 4]

# 연산 포함
lst = [x * 2 for x in range(5)]
print(lst)  # [0, 2, 4, 6, 8]

# 조건 포함
lst = [x for x in range(10) if x % 2 == 0]
print(lst)  # [0, 2, 4, 6, 8]

# if-else 포함
lst = [x if x % 2 == 0 else x * 10 for x in range(5)]
print(lst)  # [0, 10, 2, 30, 4]
```

---

## 11. 다른 시퀀스와의 상호작용

### zip() : 여러 리스트를 묶기

```python
lst1 = [1, 2, 3]
lst2 = ['a', 'b', 'c']
zipped = list(zip(lst1, lst2))
print(zipped)  # [(1, 'a'), (2, 'b'), (3, 'c')]

# 언팩
for num, char in zip(lst1, lst2):
    print(f"{num}: {char}")
# 1: a
# 2: b
# 3: c
```

### map() : 함수를 각 요소에 적용

```python
lst = [1, 2, 3, 4, 5]
result = list(map(lambda x: x * 2, lst))
print(result)  # [2, 4, 6, 8, 10]

def square(x):
    return x ** 2

result = list(map(square, lst))
print(result)  # [1, 4, 9, 16, 25]
```

### filter() : 조건을 만족하는 요소 필터링

```python
lst = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result = list(filter(lambda x: x % 2 == 0, lst))
print(result)  # [2, 4, 6, 8, 10]

def is_even(x):
    return x % 2 == 0

result = list(filter(is_even, lst))
print(result)  # [2, 4, 6, 8, 10]
```

---

## 12. 리스트 비교 및 기타

### == : 두 리스트가 같은지 확인

```python
lst1 = [1, 2, 3]
lst2 = [1, 2, 3]
lst3 = [1, 2, 4]

print(lst1 == lst2)  # True
print(lst1 == lst3)  # False
```

### != : 두 리스트가 다른지 확인

```python
lst1 = [1, 2, 3]
lst3 = [1, 2, 4]

print(lst1 != lst3)  # True
```

### 리스트 연결 : + 연산자

```python
lst1 = [1, 2, 3]
lst2 = [4, 5, 6]
lst3 = lst1 + lst2
print(lst3)  # [1, 2, 3, 4, 5, 6]
```

### 리스트 반복 : * 연산자

```python
lst = [1, 2, 3]
result = lst * 3
print(result)  # [1, 2, 3, 1, 2, 3, 1, 2, 3]

result = ['a'] * 5
print(result)  # ['a', 'a', 'a', 'a', 'a']
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `append()` | 끝에 요소 추가 |
| `insert()` | 지정 위치에 요소 추가 |
| `extend()` | 다른 리스트의 모든 요소 추가 |
| `remove()` | 첫 번째 해당 값 제거 |
| `pop()` | 요소 제거하고 반환 |
| `clear()` | 모든 요소 삭제 |
| `index()` | 해당 값의 인덱스 반환 |
| `count()` | 해당 값의 개수 세기 |
| `sort()` | 제자리에서 정렬 |
| `reverse()` | 역순으로 정렬 |
| `copy()` | 얕은 복사본 생성 |
| `len()` | 리스트의 길이 |
| `sum()` | 요소의 합계 |
| `max()` | 최댓값 |
| `min()` | 최솟값 |

