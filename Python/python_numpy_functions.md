# 파이썬 NumPy 함수 정리

## 기본 설정

```python
import numpy as np
```

---

## 1. 배열 생성

### array() : 리스트나 다른 배열 객체를 NumPy 배열로 변환

```python
# 1차원 배열
arr = np.array([1, 2, 3, 4, 5])
print(arr)  # [1 2 3 4 5]

# 2차원 배열
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr)
# [[1 2 3]
#  [4 5 6]]

# 데이터 타입 지정
arr = np.array([1, 2, 3], dtype=float)
print(arr)  # [1. 2. 3.]
```

### zeros() : 모든 요소가 0인 배열 생성

```python
# 1차원
arr = np.zeros(5)
print(arr)  # [0. 0. 0. 0. 0.]

# 2차원
arr = np.zeros((3, 4))
print(arr)
# [[0. 0. 0. 0.]
#  [0. 0. 0. 0.]
#  [0. 0. 0. 0.]]
```

### ones() : 모든 요소가 1인 배열 생성

```python
arr = np.ones((2, 3))
print(arr)
# [[1. 1. 1.]
#  [1. 1. 1.]]
```

### full() : 지정한 값으로 배열 채우기

```python
arr = np.full((2, 3), 7)
print(arr)
# [[7 7 7]
#  [7 7 7]]
```

### arange() : 일정한 간격으로 배열 생성

```python
# 0부터 9까지
arr = np.arange(10)
print(arr)  # [0 1 2 3 4 5 6 7 8 9]

# 2부터 10까지 (10 미포함)
arr = np.arange(2, 10)
print(arr)  # [2 3 4 5 6 7 8 9]

# 2부터 10까지 2씩 증가
arr = np.arange(2, 10, 2)
print(arr)  # [2 4 6 8]
```

### linspace() : 시작과 끝 사이에 균등하게 배열 생성

```python
# 0부터 1까지 5개 요소
arr = np.linspace(0, 1, 5)
print(arr)  # [0.   0.25 0.5  0.75 1.  ]
```

### logspace() : 로그 스케일로 배열 생성

```python
# 10^1 부터 10^3 까지 5개 요소
arr = np.logspace(1, 3, 5)
print(arr)  # [  10.          46.41588834 215.44346901 1000.        ]
```

### eye() : 단위 행렬 생성

```python
arr = np.eye(3)
print(arr)
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]
```

### diag() : 대각선 행렬 생성

```python
arr = np.diag([1, 2, 3])
print(arr)
# [[1 0 0]
#  [0 2 0]
#  [0 0 3]]
```

### random.rand() : 0~1 사이의 난수 배열 생성 (균등 분포)

```python
arr = np.random.rand(3, 4)  # 3x4 배열
print(arr)
```

### random.randn() : 표준 정규 분포에서 난수 배열 생성

```python
arr = np.random.randn(3, 4)
print(arr)
```

### random.randint() : 정수 난수 배열 생성

```python
# 0부터 10까지의 정수 5개
arr = np.random.randint(0, 10, 5)
print(arr)

# 2x3 배열
arr = np.random.randint(1, 100, (2, 3))
print(arr)
```

---

## 2. 배열 정보 조회

### shape : 배열의 형태 (차원과 크기)

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.shape)  # (2, 3)
```

### ndim : 배열의 차원 수

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.ndim)  # 2
```

### size : 배열의 전체 요소 개수

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.size)  # 6
```

### dtype : 배열의 데이터 타입

```python
arr = np.array([1, 2, 3], dtype=float)
print(arr.dtype)  # float64
```

### itemsize : 각 요소의 바이트 크기

```python
arr = np.array([1, 2, 3], dtype=np.int32)
print(arr.itemsize)  # 4
```

### nbytes : 배열 전체의 바이트 크기

```python
arr = np.array([[1, 2, 3], [4, 5, 6]], dtype=np.int32)
print(arr.nbytes)  # 24
```

---

## 3. 배열 변형

### reshape() : 배열의 형태 변경

```python
arr = np.arange(12)
arr = arr.reshape(3, 4)
print(arr)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# 1차원으로 변경
arr = arr.reshape(-1)
print(arr)  # [ 0  1  2  3  4  5  6  7  8  9 10 11]
```

### flatten() : 배열을 1차원으로 펼치기

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
flat = arr.flatten()
print(flat)  # [1 2 3 4 5 6]
```

### ravel() : flatten()과 유사 (뷰 반환 가능)

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
flat = arr.ravel()
print(flat)  # [1 2 3 4 5 6]
```

### transpose() / T : 배열 전치

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
transposed = arr.transpose()
print(transposed)
# [[1 4]
#  [2 5]
#  [3 6]]

# T 속성 사용
print(arr.T)  # 위와 동일
```

### swapaxes() : 축 교환

```python
arr = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
swapped = arr.swapaxes(0, 2)
print(swapped.shape)  # (2, 2, 2)
```

### concatenate() : 배열 연결

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
result = np.concatenate([arr1, arr2])
print(result)  # [1 2 3 4 5 6]

# 2차원
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])
result = np.concatenate([arr1, arr2], axis=0)
print(result)
# [[1 2]
#  [3 4]
#  [5 6]
#  [7 8]]
```

### stack() : 배열을 새로운 축으로 쌓기

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
result = np.stack([arr1, arr2])
print(result)
# [[1 2 3]
#  [4 5 6]]
```

### split() : 배열 분할

```python
arr = np.array([1, 2, 3, 4, 5, 6])
result = np.split(arr, 3)
print(result)  # [array([1, 2]), array([3, 4]), array([5, 6])]
```

---

## 4. 배열 인덱싱과 슬라이싱

### 기본 인덱싱

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr[0])        # [1 2 3]
print(arr[0, 1])     # 2
print(arr[1, -1])    # 6
```

### 슬라이싱

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr[0:2, 0:2])
# [[1 2]
#  [4 5]]

print(arr[:, 1])     # [2 5]
print(arr[1, :])     # [4 5 6]
```

### 부울 인덱싱

```python
arr = np.array([1, 2, 3, 4, 5])
mask = arr > 2
print(arr[mask])  # [3 4 5]

# 조건으로 직접 인덱싱
print(arr[arr % 2 == 0])  # [2 4]
```

### 팬시 인덱싱

```python
arr = np.array([10, 20, 30, 40, 50])
indices = np.array([0, 2, 4])
print(arr[indices])  # [10 30 50]
```

---

## 5. 배열 연산

### 기본 산술 연산

```python
arr = np.array([1, 2, 3, 4, 5])

print(arr + 2)      # [3 4 5 6 7]
print(arr * 2)      # [ 2  4  6  8 10]
print(arr ** 2)     # [ 1  4  9 16 25]
print(arr / 2)      # [0.5 1.  1.5 2.  2.5]

# 배열 간 연산
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
print(arr1 + arr2)  # [5 7 9]
print(arr1 * arr2)  # [ 4 10 18]
```

### 행렬 곱셈

```python
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])

# 행렬 곱셈
result = np.dot(arr1, arr2)
print(result)
# [[19 22]
#  [43 50]]

# @ 연산자로도 가능
result = arr1 @ arr2
print(result)  # 위와 동일
```

### 원소별 연산

```python
arr = np.array([1, 4, 9, 16])

print(np.sqrt(arr))     # [1. 2. 3. 4.]
print(np.exp(arr))      # 지수
print(np.log(arr))      # 로그
print(np.abs(arr))      # 절댓값
print(np.sin(arr))      # 사인
print(np.cos(arr))      # 코사인
```

---

## 6. 집계 함수

### sum() : 합계

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.sum(arr))  # 15

# 축 지정
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(np.sum(arr, axis=0))  # [5 7 9]
print(np.sum(arr, axis=1))  # [6 15]
```

### mean() : 평균

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.mean(arr))  # 3.0

arr = np.array([[1, 2, 3], [4, 5, 6]])
print(np.mean(arr, axis=0))  # [2.5 3.5 4.5]
```

### median() : 중앙값

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.median(arr))  # 3.0
```

### std() : 표준편차

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.std(arr))  # 1.41421356
```

### var() : 분산

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.var(arr))  # 2.0
```

### min() / max() : 최소/최대값

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.min(arr))  # 1
print(np.max(arr))  # 5

# 축 지정
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(np.min(arr, axis=0))  # [1 2 3]
print(np.max(arr, axis=1))  # [3 6]
```

### argmin() / argmax() : 최소/최대값의 인덱스

```python
arr = np.array([1, 5, 3, 2, 4])
print(np.argmin(arr))  # 0
print(np.argmax(arr))  # 1
```

### cumsum() : 누적합

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.cumsum(arr))  # [ 1  3  6 10 15]
```

### cumprod() : 누적곱

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.cumprod(arr))  # [  1   2   6  24 120]
```

---

## 7. 정렬 및 검색

### sort() : 배열 정렬

```python
arr = np.array([3, 1, 4, 1, 5, 9, 2])
sorted_arr = np.sort(arr)
print(sorted_arr)  # [1 1 2 3 4 5 9]

# 2차원 배열
arr = np.array([[3, 1], [4, 2]])
sorted_arr = np.sort(arr, axis=1)
print(sorted_arr)
# [[1 3]
#  [2 4]]
```

### argsort() : 정렬된 인덱스 반환

```python
arr = np.array([3, 1, 4, 1, 5])
indices = np.argsort(arr)
print(indices)  # [1 3 0 2 4]
```

### searchsorted() : 정렬된 배열에서 삽입할 위치 찾기

```python
arr = np.array([1, 2, 3, 4, 5])
print(np.searchsorted(arr, 3.5))  # 3
```

### where() : 조건을 만족하는 인덱스 반환

```python
arr = np.array([1, 2, 3, 4, 5])
indices = np.where(arr > 2)
print(indices)  # (array([2, 3, 4]),)

print(arr[indices])  # [3 4 5]
```

---

## 8. 통계 함수

### percentile() : 백분위수

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print(np.percentile(arr, 25))   # 3.25 (25백분위수)
print(np.percentile(arr, 50))   # 5.5 (중앙값)
print(np.percentile(arr, 75))   # 7.75 (75백분위수)
```

### quantile() : 사분위수 (percentile()의 0~1 버전)

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print(np.quantile(arr, 0.25))  # 3.25
print(np.quantile(arr, 0.5))   # 5.5
```

### corrcoef() : 상관계수

```python
x = np.array([1, 2, 3, 4, 5])
y = np.array([2, 4, 5, 4, 6])
corr = np.corrcoef(x, y)
print(corr)
```

### cov() : 공분산

```python
x = np.array([1, 2, 3, 4, 5])
y = np.array([2, 4, 5, 4, 6])
cov = np.cov(x, y)
print(cov)
```

---

## 9. 선형대수

### linalg.det() : 행렬식 계산

```python
arr = np.array([[1, 2], [3, 4]])
det = np.linalg.det(arr)
print(det)  # -2.0
```

### linalg.inv() : 역행렬 계산

```python
arr = np.array([[1, 2], [3, 4]])
inv = np.linalg.inv(arr)
print(inv)
# [[-2.   1. ]
#  [ 1.5 -0.5]]
```

### linalg.eig() : 고유값과 고유벡터

```python
arr = np.array([[1, 2], [2, 1]])
eigenvalues, eigenvectors = np.linalg.eig(arr)
print(eigenvalues)      # [3. -1.]
print(eigenvectors)
```

### linalg.svd() : 특이값 분해

```python
arr = np.array([[1, 2], [3, 4], [5, 6]])
U, s, Vt = np.linalg.svd(arr)
print(U.shape, s.shape, Vt.shape)
```

### linalg.solve() : 선형 방정식 풀기

```python
# Ax = b 풀기
A = np.array([[1, 2], [3, 4]])
b = np.array([5, 6])
x = np.linalg.solve(A, b)
print(x)
```

---

## 10. 파일 입출력

### save() : 바이너리 파일로 저장

```python
arr = np.array([1, 2, 3, 4, 5])
np.save('array.npy', arr)
```

### load() : 바이너리 파일에서 로드

```python
arr = np.load('array.npy')
print(arr)  # [1 2 3 4 5]
```

### savez() : 여러 배열을 바이너리 파일로 저장

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
np.savez('arrays.npz', arr1=arr1, arr2=arr2)
```

### loadz() : npz 파일에서 로드

```python
data = np.load('arrays.npz')
print(data['arr1'])
print(data['arr2'])
```

### savetxt() : 텍스트 파일로 저장

```python
arr = np.array([1, 2, 3, 4, 5])
np.savetxt('array.txt', arr)
```

### loadtxt() : 텍스트 파일에서 로드

```python
arr = np.loadtxt('array.txt')
print(arr)
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `array()` | 배열 생성 |
| `zeros()` | 0으로 채운 배열 |
| `ones()` | 1로 채운 배열 |
| `arange()` | 일정한 간격의 배열 |
| `linspace()` | 균등한 간격의 배열 |
| `reshape()` | 배열 형태 변경 |
| `flatten()` | 1차원으로 펼치기 |
| `concatenate()` | 배열 연결 |
| `split()` | 배열 분할 |
| `sum()` | 합계 |
| `mean()` | 평균 |
| `std()` | 표준편차 |
| `min()` / `max()` | 최소/최대값 |
| `sort()` | 정렬 |
| `dot()` | 행렬 곱셈 |
| `linalg.inv()` | 역행렬 |
| `save()` / `load()` | 파일 저장/로드 |

