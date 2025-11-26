# 파이썬 문자열 함수 정리

## 1. 문자열 대소문자 변환

### upper() : 모든 문자를 대문자로 변환

```python
text = "hello world"
print(text.upper())  # HELLO WORLD
```

### lower() : 모든 문자를 소문자로 변환

```python
text = "HELLO WORLD"
print(text.lower())  # hello world
```

### capitalize() : 첫 번째 문자를 대문자로, 나머지를 소문자로 변환

```python
text = "hello world"
print(text.capitalize())  # Hello world
```

### title() : 각 단어의 첫 번째 문자를 대문자로 변환

```python
text = "hello world python"
print(text.title())  # Hello World Python
```

### swapcase() : 대문자와 소문자를 서로 바꿈

```python
text = "Hello World"
print(text.swapcase())  # hELLO wORLD
```

---

## 2. 문자열 검색 및 위치

### find() : 부분 문자열의 위치를 찾음 (없으면 -1 반환)

```python
text = "hello world"
print(text.find("world"))  # 6
print(text.find("xyz"))    # -1
```

### rfind() : 오른쪽에서부터 부분 문자열을 찾음

```python
text = "hello hello world"
print(text.rfind("hello"))  # 6
```

### index() : find()와 같지만 없으면 ValueError 발생

```python
text = "hello world"
print(text.index("world"))  # 6
# print(text.index("xyz"))  # ValueError 발생
```

### count() : 부분 문자열이 몇 번 나타나는지 세기

```python
text = "hello hello hello"
print(text.count("hello"))  # 3

text = "aabbccdd"
print(text.count("c"))  # 2
```

---

## 3. 문자열 포함 여부 확인

### in / not in : 문자열 포함 여부 확인

```python
text = "hello world"
print("world" in text)      # True
print("xyz" in text)        # False
print("xyz" not in text)    # True
```

### startswith() : 문자열이 특정 문자로 시작하는지 확인

```python
text = "hello world"
print(text.startswith("hello"))  # True
print(text.startswith("world"))  # False
```

### endswith() : 문자열이 특정 문자로 끝나는지 확인

```python
text = "hello world"
print(text.endswith("world"))  # True
print(text.endswith("hello"))  # False
```

---

## 4. 문자열 치환

### replace() : 부분 문자열을 다른 문자열로 치환

```python
text = "hello world world"
print(text.replace("world", "python"))  # hello python python

# 개수 제한
print(text.replace("world", "python", 1))  # hello python world
```

---

## 5. 문자열 분할 및 결합

### split() : 문자열을 구분자로 분할하여 리스트 반환

```python
text = "hello world python"
print(text.split())  # ['hello', 'world', 'python']

text = "apple,banana,orange"
print(text.split(","))  # ['apple', 'banana', 'orange']

# 분할 개수 제한
text = "a,b,c,d"
print(text.split(",", 2))  # ['a', 'b', 'c,d']
```

### rsplit() : 오른쪽에서부터 분할

```python
text = "a,b,c,d"
print(text.rsplit(",", 1))  # ['a,b,c', 'd']
```

### splitlines() : 줄바꿈을 기준으로 분할

```python
text = "hello\nworld\npython"
print(text.splitlines())  # ['hello', 'world', 'python']
```

### join() : 리스트의 요소들을 구분자로 연결하여 하나의 문자열로 생성

```python
words = ["hello", "world", "python"]
print(" ".join(words))  # hello world python
print("-".join(words))  # hello-world-python
```

---

## 6. 문자열 공백 처리

### strip() : 문자열의 양쪽 끝에서 공백 제거

```python
text = "  hello world  "
print(text.strip())  # hello world

# 특정 문자 제거
text = "###hello###"
print(text.strip("#"))  # hello
```

### lstrip() : 왼쪽 끝에서만 공백 제거

```python
text = "  hello world  "
print(text.lstrip())  # hello world
```

### rstrip() : 오른쪽 끝에서만 공백 제거

```python
text = "  hello world  "
print(text.rstrip())  # hello world  (왼쪽 공백은 유지)
```

---

## 7. 문자열 포맷팅

### format() : 문자열에 값을 삽입

```python
# 위치 기반
print("{} {}".format("hello", "world"))  # hello world

# 인덱스 기반
print("{1} {0}".format("world", "hello"))  # hello world

# 이름 기반
print("{name} is {age} years old".format(name="John", age=25))
# John is 25 years old
```

### f-string (Python 3.6+) : 문자열에 변수를 직접 삽입

```python
name = "John"
age = 25
print(f"{name} is {age} years old")  # John is 25 years old

# 표현식 포함
x = 10
y = 20
print(f"{x} + {y} = {x + y}")  # 10 + 20 = 30
```

### % 포맷팅 : 구식 방식의 문자열 포맷팅

```python
name = "John"
age = 25
print("%s is %d years old" % (name, age))  # John is 25 years old
```

---

## 8. 문자열 길이 및 문자 접근

### len() : 문자열의 길이 반환

```python
text = "hello"
print(len(text))  # 5
```

### 인덱싱 : 특정 위치의 문자 접근

```python
text = "hello"
print(text[0])   # h
print(text[-1])  # o (마지막 문자)
```

### 슬라이싱 : 문자열의 일부를 추출

```python
text = "hello world"
print(text[0:5])   # hello
print(text[6:])    # world
print(text[-5:])   # world
print(text[::2])   # hlowrd (2칸씩)
print(text[::-1])  # dlrow olleh (역순)
```

---

## 9. 문자열 변환 및 확인

### isdigit() : 문자열이 모두 숫자인지 확인

```python
print("123".isdigit())    # True
print("12a".isdigit())    # False
```

### isalpha() : 문자열이 모두 알파벳인지 확인

```python
print("hello".isalpha())      # True
print("hello123".isalpha())   # False
```

### isalnum() : 문자열이 알파벳과 숫자로만 이루어졌는지 확인

```python
print("hello123".isalnum())   # True
print("hello 123".isalnum())  # False (공백 포함)
```

### isspace() : 문자열이 모두 공백인지 확인

```python
print("   ".isspace())   # True
print(" a ".isspace())   # False
```

### isupper() : 문자열이 모두 대문자인지 확인

```python
print("HELLO".isupper())   # True
print("Hello".isupper())   # False
```

### islower() : 문자열이 모두 소문자인지 확인

```python
print("hello".islower())   # True
print("Hello".islower())   # False
```

---

## 10. 문자열 정렬 및 채우기

### center() : 문자열을 지정된 너비의 중앙에 배치

```python
text = "hello"
print(f"'{text.center(15)}'")      # '     hello     '
print(f"'{text.center(15, '*')}'") # '*****hello*****'
```

### ljust() : 문자열을 왼쪽 정렬하고 채우기

```python
text = "hello"
print(f"'{text.ljust(15)}'")      # 'hello          '
print(f"'{text.ljust(15, '-')}'") # 'hello----------'
```

### rjust() : 문자열을 오른쪽 정렬하고 채우기

```python
text = "hello"
print(f"'{text.rjust(15)}'")      # '          hello'
print(f"'{text.rjust(15, '-')}'") # '----------hello'
```

### zfill() : 숫자 앞에 0을 채우기

```python
print("42".zfill(5))   # 00042
print("-42".zfill(5))  # -0042
```

---

## 11. 기타 유용한 함수

### ord() : 문자의 유니코드 값 반환

```python
print(ord('A'))  # 65
print(ord('a'))  # 97
```

### chr() : 유니코드 값을 문자로 변환

```python
print(chr(65))  # A
print(chr(97))  # a
```

### repr() : 문자열의 표현을 반환 (따옴표 포함)

```python
text = "hello\nworld"
print(repr(text))  # 'hello\nworld'
print(text)        # hello
                   # world
```

### ascii() : 아스키 값으로 표현 가능한 문자열 반환

```python
print(ascii("hello"))  # 'hello'
print(ascii("한글"))   # '\ud55c\uae00'
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `upper()` | 대문자로 변환 |
| `lower()` | 소문자로 변환 |
| `capitalize()` | 첫 글자만 대문자 |
| `title()` | 각 단어 첫 글자 대문자 |
| `find()` | 부분 문자열 위치 검색 |
| `replace()` | 부분 문자열 치환 |
| `split()` | 구분자로 분할 |
| `join()` | 리스트를 문자열로 연결 |
| `strip()` | 양쪽 공백 제거 |
| `startswith()` | 특정 문자로 시작하는지 확인 |
| `endswith()` | 특정 문자로 끝나는지 확인 |
| `isdigit()` | 숫자로만 이루어졌는지 확인 |
| `isalpha()` | 알파벳으로만 이루어졌는지 확인 |
| `format()` | 문자열에 값 삽입 |

