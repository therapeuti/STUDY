# 파이썬 scikit-learn 함수 정리

## 기본 설정

```python
import sklearn
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn import datasets
import numpy as np
import pandas as pd
```

---

## 1. 데이터 분할

### train_test_split() : 데이터를 훈련/테스트 세트로 분할

```python
from sklearn.model_selection import train_test_split

X = np.array([[1, 2], [3, 4], [5, 6], [7, 8]])
y = np.array([0, 1, 0, 1])

# 기본 분할 (8:2)
X_train, X_test, y_train, y_test = train_test_split(X, y)

# 비율 지정
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)

# 무작위 시드 지정 (재현성)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

### cross_val_score() : 교차 검증으로 모델 평가

```python
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier

X = np.array([[1, 2], [3, 4], [5, 6], [7, 8]])
y = np.array([0, 1, 0, 1])

model = RandomForestClassifier()
scores = cross_val_score(model, X, y, cv=5)
print(scores)        # 각 fold의 점수
print(scores.mean()) # 평균 점수
```

### cross_validate() : 여러 지표로 교차 검증

```python
from sklearn.model_selection import cross_validate
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier()
scores = cross_validate(
    model, X, y,
    cv=5,
    scoring=['accuracy', 'precision', 'recall']
)
print(scores)
```

---

## 2. 데이터 전처리

### StandardScaler() : 데이터 표준화 (평균 0, 표준편차 1)

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X = np.array([[1, 100], [2, 200], [3, 300]])

# 훈련 데이터로 스케일러 학습
X_scaled = scaler.fit_transform(X)
print(X_scaled)
# [[-1.22474487 -1.22474487]
#  [ 0.          0.        ]
#  [ 1.22474487  1.22474487]]

# 테스트 데이터 변환
X_test = np.array([[4, 400]])
X_test_scaled = scaler.transform(X_test)
print(X_test_scaled)
```

### MinMaxScaler() : 데이터를 0~1 범위로 정규화

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X = np.array([[1, 100], [2, 200], [3, 300]])
X_scaled = scaler.fit_transform(X)
print(X_scaled)
# [[0.  0. ]
#  [0.5 0.5]
#  [1.  1. ]]
```

### OneHotEncoder() : 범주형 데이터를 원-핫 인코딩

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder()
X = np.array([['red'], ['blue'], ['green'], ['red']])
X_encoded = encoder.fit_transform(X).toarray()
print(X_encoded)
# [[0. 0. 1.]
#  [0. 1. 0.]
#  [1. 0. 0.]
#  [0. 0. 1.]]
```

### LabelEncoder() : 문자열 레이블을 정수로 변환

```python
from sklearn.preprocessing import LabelEncoder

encoder = LabelEncoder()
y = np.array(['cat', 'dog', 'cat', 'bird'])
y_encoded = encoder.fit_transform(y)
print(y_encoded)  # [1 2 1 0]

# 역변환
y_original = encoder.inverse_transform(y_encoded)
print(y_original)  # ['cat' 'dog' 'cat' 'bird']
```

### Imputer() / SimpleImputer() : 결측치 처리

```python
from sklearn.impute import SimpleImputer
import numpy as np

imputer = SimpleImputer(strategy='mean')  # 평균으로 채우기
X = np.array([[1, 2], [3, np.nan], [5, 6]])
X_imputed = imputer.fit_transform(X)
print(X_imputed)
# [[1. 2.]
#  [3. 4.]
#  [5. 6.]]
```

### PolynomialFeatures() : 다항식 특성 생성

```python
from sklearn.preprocessing import PolynomialFeatures

poly = PolynomialFeatures(degree=2)
X = np.array([[1, 2], [3, 4]])
X_poly = poly.fit_transform(X)
print(X_poly.shape)  # (2, 6)
```

---

## 3. 특성 선택 및 추출

### SelectKBest() : 상위 K개의 특성 선택

```python
from sklearn.feature_selection import SelectKBest, f_classif

X = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])
y = np.array([0, 0, 1, 1])

selector = SelectKBest(score_func=f_classif, k=2)
X_selected = selector.fit_transform(X, y)
print(X_selected.shape)  # (4, 2)
```

### PCA() : 주성분 분석 (차원 축소)

```python
from sklearn.decomposition import PCA

X = np.array([[1, 2], [3, 4], [5, 6], [7, 8]])
pca = PCA(n_components=1)
X_pca = pca.fit_transform(X)
print(X_pca.shape)  # (4, 1)
print(pca.explained_variance_ratio_)  # 설명 분산 비율
```

### TruncatedSVD() : 특이값 분해 (희소 행렬용)

```python
from sklearn.decomposition import TruncatedSVD
from scipy.sparse import csr_matrix

X = csr_matrix([[1, 2], [3, 4], [5, 6]])
svd = TruncatedSVD(n_components=1)
X_svd = svd.fit_transform(X)
print(X_svd.shape)
```

---

## 4. 분류 모델

### LogisticRegression() : 로지스틱 회귀 (분류)

```python
from sklearn.linear_model import LogisticRegression

X = np.array([[1, 2], [3, 4], [5, 6], [7, 8]])
y = np.array([0, 0, 1, 1])

model = LogisticRegression()
model.fit(X, y)
predictions = model.predict(X)
print(predictions)  # [0 0 1 1]

# 확률 예측
probabilities = model.predict_proba(X)
print(probabilities)
```

### DecisionTreeClassifier() : 의사결정 트리

```python
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(max_depth=3)
model.fit(X, y)
predictions = model.predict(X)
print(predictions)
```

### RandomForestClassifier() : 랜덤 포레스트

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X, y)
predictions = model.predict(X)
print(predictions)

# 특성 중요도
print(model.feature_importances_)
```

### SVC() / SVM : 서포트 벡터 머신

```python
from sklearn.svm import SVC

model = SVC(kernel='rbf')
model.fit(X, y)
predictions = model.predict(X)
print(predictions)
```

### KNeighborsClassifier() : K-최근접 이웃

```python
from sklearn.neighbors import KNeighborsClassifier

model = KNeighborsClassifier(n_neighbors=3)
model.fit(X, y)
predictions = model.predict(X)
print(predictions)
```

### GaussianNB() : 나이브 베이즈

```python
from sklearn.naive_bayes import GaussianNB

model = GaussianNB()
model.fit(X, y)
predictions = model.predict(X)
print(predictions)
```

---

## 5. 회귀 모델

### LinearRegression() : 선형 회귀

```python
from sklearn.linear_model import LinearRegression

X = np.array([[1], [2], [3], [4], [5]])
y = np.array([2, 4, 6, 8, 10])

model = LinearRegression()
model.fit(X, y)
predictions = model.predict(X)
print(predictions)

print(model.coef_)      # 계수
print(model.intercept_) # 절편
```

### Ridge() / Lasso() / ElasticNet() : 규제 회귀

```python
from sklearn.linear_model import Ridge, Lasso, ElasticNet

# Ridge (L2 규제)
ridge = Ridge(alpha=1.0)
ridge.fit(X, y)

# Lasso (L1 규제)
lasso = Lasso(alpha=0.1)
lasso.fit(X, y)

# ElasticNet (L1 + L2 규제)
elastic = ElasticNet(alpha=1.0, l1_ratio=0.5)
elastic.fit(X, y)
```

### SVR() : 서포트 벡터 회귀

```python
from sklearn.svm import SVR

model = SVR(kernel='rbf')
model.fit(X, y)
predictions = model.predict(X)
print(predictions)
```

### DecisionTreeRegressor() : 의사결정 트리 회귀

```python
from sklearn.tree import DecisionTreeRegressor

model = DecisionTreeRegressor()
model.fit(X, y)
predictions = model.predict(X)
print(predictions)
```

### RandomForestRegressor() : 랜덤 포레스트 회귀

```python
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(n_estimators=100, random_state=42)
model.fit(X, y)
predictions = model.predict(X)
print(predictions)
```

---

## 6. 모델 평가

### accuracy_score() : 정확도 (분류)

```python
from sklearn.metrics import accuracy_score

y_true = np.array([0, 1, 0, 1])
y_pred = np.array([0, 1, 1, 1])
acc = accuracy_score(y_true, y_pred)
print(acc)  # 0.75
```

### precision_score() : 정밀도 (분류)

```python
from sklearn.metrics import precision_score

prec = precision_score(y_true, y_pred)
print(prec)  # 양성 예측 중 실제 양성의 비율
```

### recall_score() : 재현율 (분류)

```python
from sklearn.metrics import recall_score

rec = recall_score(y_true, y_pred)
print(rec)  # 실제 양성 중 예측 양성의 비율
```

### f1_score() : F1 스코어 (분류)

```python
from sklearn.metrics import f1_score

f1 = f1_score(y_true, y_pred)
print(f1)  # 정밀도와 재현율의 조화평균
```

### confusion_matrix() : 혼동 행렬

```python
from sklearn.metrics import confusion_matrix

cm = confusion_matrix(y_true, y_pred)
print(cm)
# [[1 0]
#  [0 2]]
```

### classification_report() : 분류 보고서

```python
from sklearn.metrics import classification_report

report = classification_report(y_true, y_pred)
print(report)
```

### roc_auc_score() : ROC-AUC 점수

```python
from sklearn.metrics import roc_auc_score

y_scores = np.array([0.1, 0.9, 0.3, 0.8])
auc = roc_auc_score(y_true, y_scores)
print(auc)
```

### mean_squared_error() : 평균제곱오차 (회귀)

```python
from sklearn.metrics import mean_squared_error

y_true = np.array([1, 2, 3, 4, 5])
y_pred = np.array([1.1, 2.1, 2.9, 4.2, 4.9])
mse = mean_squared_error(y_true, y_pred)
print(mse)
```

### mean_absolute_error() : 평균절대오차 (회귀)

```python
from sklearn.metrics import mean_absolute_error

mae = mean_absolute_error(y_true, y_pred)
print(mae)
```

### r2_score() : R² 스코어 (회귀)

```python
from sklearn.metrics import r2_score

r2 = r2_score(y_true, y_pred)
print(r2)
```

---

## 7. 샘플 데이터셋

### load_iris() : 아이리스 데이터셋

```python
from sklearn.datasets import load_iris

iris = load_iris()
X = iris.data
y = iris.target
print(X.shape)  # (150, 4)
print(y.shape)  # (150,)
```

### load_digits() : 손글씨 숫자 데이터셋

```python
from sklearn.datasets import load_digits

digits = load_digits()
X = digits.data
y = digits.target
print(X.shape)  # (1797, 64)
```

### load_wine() : 와인 데이터셋

```python
from sklearn.datasets import load_wine

wine = load_wine()
X = wine.data
y = wine.target
```

### load_breast_cancer() : 유방암 데이터셋

```python
from sklearn.datasets import load_breast_cancer

cancer = load_breast_cancer()
X = cancer.data
y = cancer.target
```

### make_classification() : 합성 분류 데이터 생성

```python
from sklearn.datasets import make_classification

X, y = make_classification(
    n_samples=100,
    n_features=10,
    n_informative=5,
    n_classes=2,
    random_state=42
)
```

### make_regression() : 합성 회귀 데이터 생성

```python
from sklearn.datasets import make_regression

X, y = make_regression(
    n_samples=100,
    n_features=5,
    noise=10,
    random_state=42
)
```

---

## 8. 파이프라인

### Pipeline() : 여러 단계를 하나의 파이프라인으로 구성

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier())
])

pipeline.fit(X_train, y_train)
predictions = pipeline.predict(X_test)
```

### ColumnTransformer() : 열별로 다른 전처리 적용

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder

ct = ColumnTransformer([
    ('scaler', StandardScaler(), ['age', 'income']),
    ('encoder', OneHotEncoder(), ['gender', 'city'])
])

X_transformed = ct.fit_transform(X)
```

---

## 9. 하이퍼파라미터 튜닝

### GridSearchCV() : 그리드 서치로 최적 파라미터 찾기

```python
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier

param_grid = {
    'n_estimators': [10, 50, 100],
    'max_depth': [3, 5, 7],
    'min_samples_split': [2, 5, 10]
}

grid_search = GridSearchCV(
    RandomForestClassifier(),
    param_grid,
    cv=5
)
grid_search.fit(X_train, y_train)
print(grid_search.best_params_)
print(grid_search.best_score_)
```

### RandomizedSearchCV() : 랜덤 서치로 최적 파라미터 찾기

```python
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint

param_dist = {
    'n_estimators': randint(10, 100),
    'max_depth': randint(3, 20)
}

random_search = RandomizedSearchCV(
    RandomForestClassifier(),
    param_dist,
    n_iter=10,
    cv=5,
    random_state=42
)
random_search.fit(X_train, y_train)
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `train_test_split()` | 데이터 분할 |
| `cross_val_score()` | 교차 검증 |
| `StandardScaler()` | 표준화 |
| `MinMaxScaler()` | 정규화 |
| `OneHotEncoder()` | 원-핫 인코딩 |
| `LabelEncoder()` | 레이블 인코딩 |
| `LogisticRegression()` | 로지스틱 회귀 |
| `DecisionTreeClassifier()` | 의사결정 트리 |
| `RandomForestClassifier()` | 랜덤 포레스트 |
| `SVC()` | 서포트 벡터 머신 |
| `LinearRegression()` | 선형 회귀 |
| `accuracy_score()` | 정확도 |
| `precision_score()` | 정밀도 |
| `recall_score()` | 재현율 |
| `confusion_matrix()` | 혼동 행렬 |
| `Pipeline()` | 파이프라인 |
| `GridSearchCV()` | 그리드 서치 |

