# 파이썬 딕셔너리 함수 정리

## 1. 딕셔너리 생성

### dict() : 딕셔너리 생성

```python
# 빈 딕셔너리
d = dict()
print(d)  # {}

# 키-값 쌍으로 생성
d = dict(name="John", age=25)
print(d)  # {'name': 'John', 'age': 25}

# 리스트의 튜플로 생성
d = dict([('name', 'John'), ('age', 25)])
print(d)  # {'name': 'John', 'age': 25}
```

### 리터럴 표기법 : {} 또는 {:} 으로 직접 생성

```python
d = {}
print(d)  # {}

d = {'name': 'John', 'age': 25}
print(d)  # {'name': 'John', 'age': 25}

d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
print(d)  # {'name': 'John', 'age': 25, 'city': 'Seoul'}
```

---

## 2. 요소 접근 및 추가

### [] : 키로 값에 접근

```python
d = {'name': 'John', 'age': 25}
print(d['name'])  # John
print(d['age'])   # 25

# 없는 키 접근 시 KeyError 발생
# print(d['city'])  # KeyError
```

### get() : 키로 값에 접근 (없으면 None 반환)

```python
d = {'name': 'John', 'age': 25}
print(d.get('name'))     # John
print(d.get('city'))     # None

# 기본값 설정
print(d.get('city', 'Unknown'))  # Unknown
```

### [] : 새로운 키-값 쌍 추가

```python
d = {'name': 'John'}
d['age'] = 25
print(d)  # {'name': 'John', 'age': 25}

d['city'] = 'Seoul'
print(d)  # {'name': 'John', 'age': 25, 'city': 'Seoul'}
```

---

## 3. 딕셔너리 정보 조회

### len() : 딕셔너리의 요소 개수 반환

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
print(len(d))  # 3
```

### keys() : 모든 키를 반환 (dict_keys 객체)

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
print(d.keys())  # dict_keys(['name', 'age', 'city'])

# 리스트로 변환
print(list(d.keys()))  # ['name', 'age', 'city']
```

### values() : 모든 값을 반환 (dict_values 객체)

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
print(d.values())  # dict_values(['John', 25, 'Seoul'])

# 리스트로 변환
print(list(d.values()))  # ['John', 25, 'Seoul']
```

### items() : 모든 키-값 쌍을 반환 (dict_items 객체)

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
print(d.items())  # dict_items([('name', 'John'), ('age', 25), ('city', 'Seoul')])

# 리스트로 변환
print(list(d.items()))  # [('name', 'John'), ('age', 25), ('city', 'Seoul')]
```

---

## 4. 요소 확인 및 포함

### in : 키가 딕셔너리에 있는지 확인

```python
d = {'name': 'John', 'age': 25}
print('name' in d)   # True
print('city' in d)   # False
print('John' in d)   # False (값은 확인 안 함)
```

### not in : 키가 딕셔너리에 없는지 확인

```python
d = {'name': 'John', 'age': 25}
print('city' not in d)  # True
print('name' not in d)  # False
```

---

## 5. 요소 수정 및 삭제

### [] : 기존 키의 값 수정

```python
d = {'name': 'John', 'age': 25}
d['age'] = 26
print(d)  # {'name': 'John', 'age': 26}
```

### update() : 여러 키-값 쌍을 한 번에 추가 또는 수정

```python
d = {'name': 'John', 'age': 25}
d.update({'age': 26, 'city': 'Seoul'})
print(d)  # {'name': 'John', 'age': 26, 'city': 'Seoul'}

# 다른 딕셔너리로도 가능
d2 = {'country': 'Korea'}
d.update(d2)
print(d)  # {'name': 'John', 'age': 26, 'city': 'Seoul', 'country': 'Korea'}
```

### pop() : 키를 제거하고 해당 값을 반환

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
value = d.pop('age')
print(value)  # 25
print(d)      # {'name': 'John', 'city': 'Seoul'}

# 없는 키 제거 시 KeyError 발생
# d.pop('country')  # KeyError

# 기본값 설정
value = d.pop('country', 'Unknown')
print(value)  # Unknown
```

### popitem() : 마지막 항목 (키, 값) 쌍을 제거하고 반환

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
item = d.popitem()
print(item)  # ('city', 'Seoul')
print(d)     # {'name': 'John', 'age': 25}
```

### del : 키를 삭제

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
del d['age']
print(d)  # {'name': 'John', 'city': 'Seoul'}

# 없는 키 삭제 시 KeyError 발생
# del d['country']  # KeyError
```

### clear() : 모든 요소 삭제

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
d.clear()
print(d)  # {}
```

---

## 6. 딕셔너리 복사

### copy() : 딕셔너리의 얕은 복사본 생성

```python
d = {'name': 'John', 'age': 25}
d_copy = d.copy()
d_copy['age'] = 26
print(d)      # {'name': 'John', 'age': 25}
print(d_copy) # {'name': 'John', 'age': 26}
```

### 깊은 복사 : copy.deepcopy() 사용 (중첩된 딕셔너리의 경우)

```python
import copy

d = {'name': 'John', 'info': {'age': 25, 'city': 'Seoul'}}
d_shallow = d.copy()
d_deep = copy.deepcopy(d)

# 얕은 복사: 중첩 객체는 참조
d_shallow['info']['age'] = 26
print(d['info']['age'])  # 26 (원본도 변경됨)

# 깊은 복사: 완전히 독립적
d_deep['info']['age'] = 27
print(d['info']['age'])  # 26 (원본은 변경 안 됨)
```

---

## 7. 기본값이 있는 요소 접근

### setdefault() : 키가 없으면 기본값 설정, 값 반환

```python
d = {'name': 'John'}
value = d.setdefault('age', 25)
print(value)  # 25
print(d)      # {'name': 'John', 'age': 25}

# 이미 있는 키
value = d.setdefault('name', 'Jane')
print(value)  # John
print(d)      # {'name': 'John', 'age': 25}
```

---

## 8. 딕셔너리 병합

### | 연산자 : 두 딕셔너리 병합 (Python 3.9+)

```python
d1 = {'name': 'John', 'age': 25}
d2 = {'city': 'Seoul', 'country': 'Korea'}
d3 = d1 | d2
print(d3)  # {'name': 'John', 'age': 25, 'city': 'Seoul', 'country': 'Korea'}

# 겹치는 키는 뒤의 딕셔너리 값으로 덮어씀
d1 = {'name': 'John', 'age': 25}
d2 = {'age': 26, 'city': 'Seoul'}
d3 = d1 | d2
print(d3)  # {'name': 'John', 'age': 26, 'city': 'Seoul'}
```

### |= 연산자 : 기존 딕셔너리에 다른 딕셔너리 병합 (Python 3.9+)

```python
d1 = {'name': 'John', 'age': 25}
d2 = {'city': 'Seoul', 'country': 'Korea'}
d1 |= d2
print(d1)  # {'name': 'John', 'age': 25, 'city': 'Seoul', 'country': 'Korea'}
```

---

## 9. 딕셔너리 순회

### for 루프로 키 순회

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
for key in d:
    print(key)  # name, age, city
```

### for 루프로 값 순회

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
for value in d.values():
    print(value)  # John, 25, Seoul
```

### for 루프로 키-값 쌍 순회

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
for key, value in d.items():
    print(f"{key}: {value}")
# name: John
# age: 25
# city: Seoul
```

---

## 10. 기타 유용한 함수

### fromkeys() : 주어진 키들로 딕셔너리 생성 (모든 값은 동일)

```python
keys = ['name', 'age', 'city']
d = dict.fromkeys(keys)
print(d)  # {'name': None, 'age': None, 'city': None}

# 모든 값을 같은 값으로 설정
d = dict.fromkeys(keys, 'N/A')
print(d)  # {'name': 'N/A', 'age': 'N/A', 'city': 'N/A'}
```

### sorted() : 딕셔너리의 키를 정렬된 리스트로 반환

```python
d = {'name': 'John', 'age': 25, 'city': 'Seoul'}
print(sorted(d))  # ['age', 'city', 'name']

# 역순 정렬
print(sorted(d, reverse=True))  # ['name', 'city', 'age']
```

### len() : 딕셔너리의 길이

```python
d = {'name': 'John', 'age': 25}
print(len(d))  # 2
```

### type() : 딕셔너리의 타입 확인

```python
d = {'name': 'John'}
print(type(d))  # <class 'dict'>
```

---

## 11. 딕셔너리 비교

### == : 두 딕셔너리가 같은지 확인

```python
d1 = {'name': 'John', 'age': 25}
d2 = {'name': 'John', 'age': 25}
d3 = {'name': 'John', 'age': 26}

print(d1 == d2)  # True
print(d1 == d3)  # False
```

### != : 두 딕셔너리가 다른지 확인

```python
d1 = {'name': 'John', 'age': 25}
d3 = {'name': 'John', 'age': 26}

print(d1 != d3)  # True
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `get()` | 키로 값 접근 (없으면 None) |
| `keys()` | 모든 키 반환 |
| `values()` | 모든 값 반환 |
| `items()` | 모든 키-값 쌍 반환 |
| `pop()` | 키 제거하고 값 반환 |
| `popitem()` | 마지막 항목 제거하고 반환 |
| `clear()` | 모든 요소 삭제 |
| `update()` | 여러 항목 추가/수정 |
| `copy()` | 얕은 복사본 생성 |
| `setdefault()` | 키 없으면 기본값 설정 |
| `fromkeys()` | 주어진 키로 새 딕셔너리 생성 |
| `in` | 키 존재 여부 확인 |

