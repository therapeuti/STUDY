# 파이썬 Pandas 함수 정리

## 기본 설정

```python
import pandas as pd
import numpy as np
```

---

## 1. 데이터프레임 생성

### DataFrame() : 딕셔너리로 데이터프레임 생성

```python
data = {
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [25, 30, 35],
    'city': ['Seoul', 'Busan', 'Daegu']
}
df = pd.DataFrame(data)
print(df)
#       name  age   city
# 0    Alice   25  Seoul
# 1      Bob   30  Busan
# 2  Charlie   35  Daegu
```

### Series() : 1차원 데이터 생성

```python
s = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])
print(s)
# a    10
# b    20
# c    30
# d    40
```

### read_csv() : CSV 파일 읽기

```python
df = pd.read_csv('file.csv')
print(df.head())
```

### read_excel() : Excel 파일 읽기

```python
df = pd.read_excel('file.xlsx')
print(df.head())
```

---

## 2. 데이터프레임 정보 확인

### head() : 처음 n개 행 출력 (기본값: 5)

```python
df = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie', 'David'],
    'age': [25, 30, 35, 40]
})
print(df.head(2))
#      name  age
# 0   Alice   25
# 1     Bob   30
```

### tail() : 마지막 n개 행 출력 (기본값: 5)

```python
print(df.tail(2))
#        name  age
# 2  Charlie   35
# 3    David   40
```

### info() : 데이터프레임의 정보 출력 (열 이름, 타입, null 개수 등)

```python
df.info()
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 4 entries, 0 to 3
# Data columns (total 2 columns):
#  #   Column  Non-Null Count  Dtype
# ---  ------  --------  -----
#  0   name    4         object
#  1   age     4         int64
```

### describe() : 수치 데이터의 통계 정보 출력 (평균, 표준편차, 사분위수 등)

```python
df.describe()
#        age
# count  4.0
# mean  32.5
# std    7.906
# min   25.0
# 25%   28.75
# 50%   32.5
# 75%   36.25
# max   40.0
```

### shape : 데이터프레임의 크기 반환 (행, 열)

```python
print(df.shape)  # (4, 2)
```

### columns : 열 이름 반환

```python
print(df.columns)  # Index(['name', 'age'], dtype='object')
print(df.columns.tolist())  # ['name', 'age']
```

### index : 행 인덱스 반환

```python
print(df.index)  # RangeIndex(start=0, stop=4, step=1)
```

### dtypes : 각 열의 데이터 타입 반환

```python
print(df.dtypes)
# name    object
# age      int64
```

### len() : 행의 개수 반환

```python
print(len(df))  # 4
```

---

## 3. 데이터 접근

### [] : 열 접근

```python
df = pd.DataFrame({
    'name': ['Alice', 'Bob'],
    'age': [25, 30]
})

# 단일 열 (Series 반환)
print(df['name'])
# 0    Alice
# 1      Bob

# 여러 열 (DataFrame 반환)
print(df[['name', 'age']])
#     name  age
# 0  Alice   25
# 1    Bob   30
```

### loc[] : 레이블 기반 접근 (행과 열)

```python
df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6]
}, index=['x', 'y', 'z'])

# 특정 행
print(df.loc['x'])
# A    1
# B    4

# 특정 위치의 값
print(df.loc['x', 'A'])  # 1

# 범위 선택
print(df.loc['x':'y'])
#    A  B
# x  1  4
# y  2  5
```

### iloc[] : 위치 기반 접근 (정수 인덱스)

```python
# 첫 번째 행
print(df.iloc[0])
# A    1
# B    4

# 특정 위치의 값
print(df.iloc[0, 1])  # 4

# 범위 선택
print(df.iloc[0:2, 0:1])
#    A
# x  1
# y  2
```

### at[] : 특정 위치의 단일 값 빠르게 접근

```python
print(df.at['x', 'A'])  # 1
```

### iat[] : 위치 기반으로 단일 값 빠르게 접근

```python
print(df.iat[0, 0])  # 1
```

---

## 4. 데이터 필터링

### 조건으로 필터링

```python
df = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [25, 30, 35]
})

# 단일 조건
print(df[df['age'] > 25])
#        name  age
# 1       Bob   30
# 2  Charlie   35

# 여러 조건 (AND)
print(df[(df['age'] > 25) & (df['age'] < 35)])
#    name  age
# 1   Bob   30

# 여러 조건 (OR)
print(df[(df['age'] < 26) | (df['age'] > 34)])
#        name  age
# 0    Alice   25
# 2  Charlie   35

# NOT 조건
print(df[~(df['age'] > 25)])
#     name  age
# 0  Alice   25
```

### isin() : 특정 값들에 포함되는지 확인

```python
print(df[df['name'].isin(['Alice', 'Charlie'])])
#        name  age
# 0    Alice   25
# 2  Charlie   35
```

### str.contains() : 문자열 포함 여부로 필터링

```python
df = pd.DataFrame({
    'product': ['Apple Juice', 'Orange Juice', 'Apple Pie']
})

print(df[df['product'].str.contains('Apple')])
#       product
# 0 Apple Juice
# 2  Apple Pie
```

---

## 5. 데이터 정렬

### sort_values() : 특정 열의 값으로 정렬

```python
df = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [30, 25, 35]
})

# 오름차순
print(df.sort_values('age'))
#        name  age
# 1       Bob   25
# 0    Alice   30
# 2  Charlie   35

# 내림차순
print(df.sort_values('age', ascending=False))
#        name  age
# 2  Charlie   35
# 0    Alice   30
# 1       Bob   25

# 여러 열로 정렬
df = pd.DataFrame({
    'dept': ['A', 'B', 'A'],
    'name': ['Alice', 'Bob', 'Charlie'],
    'salary': [3000, 3500, 2500]
})
print(df.sort_values(['dept', 'salary']))
```

### sort_index() : 인덱스로 정렬

```python
df = pd.DataFrame({
    'value': [10, 20, 30]
}, index=['c', 'a', 'b'])

print(df.sort_index())
#     value
# a      20
# b      30
# c      10
```

---

## 6. 데이터 수정

### [] : 열 수정

```python
df = pd.DataFrame({
    'name': ['Alice', 'Bob'],
    'age': [25, 30]
})

df['age'] = df['age'] + 1
print(df)
#     name  age
# 0  Alice   26
# 1    Bob   31
```

### loc[] : 특정 값 수정

```python
df.loc[0, 'age'] = 27
print(df)
#     name  age
# 0  Alice   27
# 1    Bob   31
```

### assign() : 새로운 열 추가 (원본 유지)

```python
df2 = df.assign(city=['Seoul', 'Busan'])
print(df2)
#     name  age   city
# 0  Alice   27  Seoul
# 1    Bob   31  Busan
```

### rename() : 열 이름 변경

```python
df = pd.DataFrame({
    'old_name': [1, 2, 3],
    'age': [25, 30, 35]
})

df_renamed = df.rename(columns={'old_name': 'new_name'})
print(df_renamed)
#    new_name  age
# 0         1   25
# 1         2   30
# 2         3   35
```

### drop() : 열 또는 행 삭제

```python
df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6],
    'C': [7, 8, 9]
})

# 열 삭제
df_drop = df.drop('B', axis=1)
print(df_drop)
#    A  C
# 0  1  7
# 1  2  8
# 2  3  9

# 행 삭제
df_drop = df.drop(0, axis=0)
print(df_drop)
#    A  B  C
# 1  2  5  8
# 2  3  6  9
```

---

## 7. 데이터 결합

### concat() : 데이터프레임 연결 (행 또는 열 방향)

```python
df1 = pd.DataFrame({
    'name': ['Alice', 'Bob'],
    'age': [25, 30]
})

df2 = pd.DataFrame({
    'name': ['Charlie'],
    'age': [35]
})

# 행 방향 연결 (기본값)
df_concat = pd.concat([df1, df2], ignore_index=True)
print(df_concat)
#        name  age
# 0    Alice   25
# 1      Bob   30
# 2  Charlie   35

# 열 방향 연결
df3 = pd.DataFrame({
    'city': ['Seoul', 'Busan']
})
df_concat = pd.concat([df1, df3], axis=1)
print(df_concat)
#     name  age   city
# 0  Alice   25  Seoul
# 1    Bob   30  Busan
```

### merge() : 두 데이터프레임을 공통 열 기준으로 병합

```python
df1 = pd.DataFrame({
    'key': [1, 2, 3],
    'value_x': ['a', 'b', 'c']
})

df2 = pd.DataFrame({
    'key': [1, 2, 4],
    'value_y': ['A', 'B', 'D']
})

# INNER JOIN (기본값)
print(pd.merge(df1, df2, on='key'))
#    key value_x value_y
# 0    1       a       A
# 1    2       b       B

# LEFT JOIN
print(pd.merge(df1, df2, on='key', how='left'))
#    key value_x value_y
# 0    1       a       A
# 1    2       b       B
# 2    3       c     NaN

# OUTER JOIN
print(pd.merge(df1, df2, on='key', how='outer'))
#    key value_x value_y
# 0    1       a       A
# 1    2       b       B
# 2    3       c     NaN
# 3    4     NaN       D
```

### join() : 인덱스를 기준으로 병합

```python
df1 = pd.DataFrame({
    'value_x': [1, 2, 3]
}, index=['A', 'B', 'C'])

df2 = pd.DataFrame({
    'value_y': [10, 20, 30]
}, index=['A', 'B', 'C'])

df_joined = df1.join(df2)
print(df_joined)
#    value_x  value_y
# A        1       10
# B        2       20
# C        3       30
```

---

## 8. 데이터 집계

### groupby() : 그룹별로 데이터 집계

```python
df = pd.DataFrame({
    'dept': ['A', 'B', 'A', 'B'],
    'salary': [3000, 3500, 3200, 3800]
})

# 부서별 평균 급여
print(df.groupby('dept')['salary'].mean())
# dept
# A    3100
# B    3650

# 여러 집계 함수
print(df.groupby('dept')['salary'].agg(['mean', 'sum', 'count']))
#      mean   sum  count
# dept
# A    3100   6200      2
# B    3650   7300      2
```

### sum() : 합계

```python
df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6]
})

print(df.sum())
# A     6
# B    15

# 행 방향 합계
print(df.sum(axis=1))
# 0     5
# 1     7
# 2     9
```

### mean() : 평균

```python
print(df.mean())
# A    2.0
# B    5.0
```

### median() : 중앙값

```python
print(df.median())
# A    2.0
# B    5.0
```

### std() : 표준편차

```python
print(df.std())
# A    1.0
# B    1.0
```

### min() / max() : 최소/최대값

```python
print(df.min())
# A    1
# B    4

print(df.max())
# A    3
# B    6
```

### count() : null이 아닌 값의 개수

```python
df_with_null = pd.DataFrame({
    'A': [1, 2, None],
    'B': [4, None, 6]
})

print(df_with_null.count())
# A    2
# B    2
```

---

## 9. 결측치 처리

### isnull() / isna() : null 값 확인

```python
df = pd.DataFrame({
    'A': [1, 2, None],
    'B': [4, None, 6]
})

print(df.isnull())
#        A      B
# 0  False  False
# 1  False   True
# 2   True  False

print(df.isna())  # isnull()과 동일
```

### notnull() / notna() : null이 아닌 값 확인

```python
print(df.notnull())
#       A      B
# 0  True   True
# 1  True  False
# 2  False  True
```

### fillna() : null 값 채우기

```python
# 고정값으로 채우기
print(df.fillna(0))
#      A    B
# 0  1.0  4.0
# 1  2.0  0.0
# 2  0.0  6.0

# 평균값으로 채우기
print(df.fillna(df.mean()))
#      A    B
# 0  1.0  4.0
# 1  2.0  5.0
# 2  1.5  6.0

# 앞의 값으로 채우기 (forward fill)
print(df.fillna(method='ffill'))
#      A    B
# 0  1.0  4.0
# 1  2.0  4.0
# 2  2.0  6.0
```

### dropna() : null 값이 있는 행 또는 열 삭제

```python
# null이 있는 행 삭제
print(df.dropna())
#      A    B
# 0  1.0  4.0

# null이 있는 열 삭제
print(df.dropna(axis=1))
# Empty DataFrame

# 모든 값이 null인 행만 삭제
print(df.dropna(how='all'))
#      A    B
# 0  1.0  4.0
# 1  2.0  NaN
# 2  NaN  6.0
```

---

## 10. 문자열 작업

### str.upper() : 대문자로 변환

```python
df = pd.DataFrame({
    'name': ['alice', 'bob', 'charlie']
})

print(df['name'].str.upper())
# 0     ALICE
# 1       BOB
# 2   CHARLIE
```

### str.lower() : 소문자로 변환

```python
print(df['name'].str.lower())
# 0      alice
# 1        bob
# 2    charlie
```

### str.len() : 문자열 길이

```python
print(df['name'].str.len())
# 0    5
# 1    3
# 2    7
```

### str.split() : 문자열 분할

```python
df = pd.DataFrame({
    'text': ['a-b-c', 'x-y-z']
})

print(df['text'].str.split('-', expand=True))
#    0  1  2
# 0  a  b  c
# 1  x  y  z
```

### str.replace() : 문자열 치환

```python
print(df['name'].str.replace('a', 'A'))
# 0     Alice
# 1       bob
# 2   chArlie
```

### str.contains() : 문자열 포함 확인

```python
print(df['name'].str.contains('a'))
# 0     True
# 1    False
# 2     True
```

---

## 11. 데이터 타입 변환

### astype() : 데이터 타입 변환

```python
df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': ['4', '5', '6']
})

# 문자열을 정수로 변환
df['B'] = df['B'].astype(int)
print(df.dtypes)
# A     int64
# B     int64

# 정수를 문자열로 변환
df['A'] = df['A'].astype(str)
print(df.dtypes)
# A    object
# B     int64
```

### to_numeric() : 숫자로 변환

```python
s = pd.Series(['1', '2', 'three', '4'])
print(pd.to_numeric(s, errors='coerce'))
# 0    1.0
# 1    2.0
# 2    NaN
# 3    4.0
```

---

## 12. 파일 저장

### to_csv() : CSV 파일로 저장

```python
df.to_csv('output.csv', index=False)
```

### to_excel() : Excel 파일로 저장

```python
df.to_excel('output.xlsx', index=False)
```

### to_json() : JSON 파일로 저장

```python
df.to_json('output.json')
```

### to_sql() : 데이터베이스에 저장

```python
# import sqlalchemy
# engine = sqlalchemy.create_engine('sqlite:///database.db')
# df.to_sql('table_name', engine, if_exists='replace')
```

---

## 13. 기타 유용한 함수

### unique() : 고유값 반환

```python
df = pd.DataFrame({
    'color': ['red', 'blue', 'red', 'green', 'blue']
})

print(df['color'].unique())
# ['red' 'blue' 'green']
```

### value_counts() : 값의 개수 세기

```python
print(df['color'].value_counts())
# red      2
# blue     2
# green    1
```

### duplicated() : 중복 행 확인

```python
df = pd.DataFrame({
    'A': [1, 2, 2, 3],
    'B': [4, 5, 5, 6]
})

print(df.duplicated())
# 0    False
# 1    False
# 2     True
# 3    False
```

### drop_duplicates() : 중복 행 제거

```python
print(df.drop_duplicates())
#    A  B
# 0  1  4
# 1  2  5
# 3  3  6
```

### sample() : 무작위로 행 샘플링

```python
print(df.sample(2))  # 2개 행 무작위 선택
```

### apply() : 함수를 각 행/열에 적용

```python
df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6]
})

# 열에 함수 적용
print(df.apply(lambda x: x.sum()))
# A     6
# B    15

# 행에 함수 적용
print(df.apply(lambda x: x.sum(), axis=1))
# 0     5
# 1     7
# 2     9
```

### applymap() / map() : 각 요소에 함수 적용

```python
print(df.applymap(lambda x: x * 2))
#    A   B
# 0  2   8
# 1  4  10
# 2  6  12
```

### pivot_table() : 피벗 테이블 생성

```python
df = pd.DataFrame({
    'dept': ['A', 'B', 'A', 'B'],
    'month': [1, 1, 2, 2],
    'sales': [100, 200, 150, 250]
})

pt = df.pivot_table(values='sales', index='dept', columns='month', aggfunc='sum')
print(pt)
# month   1      2
# dept
# A     100.0  150.0
# B     200.0  250.0
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `head()` | 처음 n개 행 출력 |
| `tail()` | 마지막 n개 행 출력 |
| `info()` | 데이터프레임 정보 |
| `describe()` | 통계 정보 |
| `shape` | 크기 (행, 열) |
| `columns` | 열 이름 |
| `dtypes` | 데이터 타입 |
| `sort_values()` | 값으로 정렬 |
| `groupby()` | 그룹별 집계 |
| `merge()` | 데이터프레임 병합 |
| `fillna()` | null 값 채우기 |
| `dropna()` | null 값 삭제 |
| `astype()` | 데이터 타입 변환 |
| `to_csv()` | CSV로 저장 |
| `apply()` | 함수 적용 |
| `value_counts()` | 값 개수 세기 |

