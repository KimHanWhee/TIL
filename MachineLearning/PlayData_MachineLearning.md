PlayData_MachineLearning (2022/12/12)
===========
ananconda 가상환경 생성

`**conda create -n 파일이름 pip python=버전**`

실행

`**conda activate tf24**`

### 텐서플로우 설치

****************************************************`**pip install tensorflow==2.4**`****************************************************

### 케라스 설치

****************************************************`**pip install keras==2.4**`****************************************************

### 주피터 노트북 설치

********************`conda install jupyter notebook`********************

### matplotlib 설치

**********************************************`**conda install matplotlib**`**********************************************

### scikit-learn 설치

******************************************************`pip install scikit-learn`******************************************************

### Scipy 설치

********************************`**pip install scipy**`********************************

## AI

- 인공지능 vs 머신러닝 vs 딥러닝
    - 인공지능>머신러닝>딥러닝
- **머신러닝(기계학습)**
    - 다양한 모델 사용
    - scikit-learn 라이브러리 사용
- **딥러닝**
    - 비정용 (이미지, 소리)
    - 인공 신경망 기반 모델
        - tensorflow
            - DNN
            - CNN(합성곱 인공신경망) : 이미지 분류
            - RNN
            - GAN
        - pytorch
- **머신러닝**
    - 지도학습
        - 분류 : 종류 예측
        - 회귀 : 값 예측
    - 비지도학습
        - 군집화 : 비슷한 것끼리 묶음
        - 차원 축소 : 시각화 가능

## Data종류

**정형**

(머신러닝, scikit-learn)

- 수치
    - 연속형 = 소수점
    - 이산형 = 정수
- 범주
    - 명목형 : 남, 여
    - 순서형(비교가능) : 대>중>소

************비정형************

(딥러닝, tensorflow, pytorch)

- 이미지
- 소리

## scikit-learn

라이브러리 : Machine Learning (ML)

- 클래스 제공
    - Estimator
        - `fit()` : 훈련
        - `predict()` : 예측
        - Classifier
            - 분류 모델 : 종류 예측
        - Regressor
            - 회귀 모델 : 값 예측
    
    ### LinearRgression
    
    `**from sklearn.linear_model import LinearRegression**`
    
    - 기울기: coef_
    - 절편: intercept_

## ML실습 순서

1. **데이터 수집**
    - 인터넷 이용(크롤링 포함) ⇒ 결측치, 이상치 O
    - 직접 생성(로컬 Data) ⇒ 결측치, 이상치 O
    - 프레임워크(라이브러리) 제공한 Data ⇒ 결측치, 이상치 X
        - scikit-learn, tensorflow
2. **데이터 전처리**
    - null 처리
    - 이상치 처리
    
    <aside>
    💡 **스케일링(scaling)**
    값의 범위 변경 ⇒ 단위 일치
    
    </aside>
    
    <aside>
    💡 **인코딩(scaling)**
    라벨인코딩 : 영문자 ⇒ 숫자
    **원핫인코딩 : 표현하고 싶은 값을 1로 나머지 0으로**
    
    </aside>
    
3. **데이터 셋 분리**
    - 훈련데이터(Training Data)
    - 평가데이터(Test data)
    
    ************과적합(밑 부분에 자세히 설명)************
    
    - 과대 적합
        - 훈련 Data 정확도가 좋고 그 이외의 Data 정확도가 낮음
    - 과소 적합
        - 훈련 Data와 이외의 Data 정확도가 낮음
    - sklearn의 train_test_split 함수 사용
4. **모델 생성**
    - 클래스 사용
        
        예) x = xxxClassifier()
        
        <aside>
        💡 ****************************파라미터 종류
        하이퍼 파라미터** 
        ⇒ 사용자 지정가능
        
        **모델 파라미터** 
        ⇒ 사용자 지정x
        ⇒ 모델이 훈련(학습)을 통해서 찾아야되는 파라미터
        ⇒ 대표적으로 회귀계수
        
        </aside>
        
5. **모델 학습(훈련)**
    
    `**x.fit(Data(feature), 정답(레이블))**` 
    
    - 지도학습
    
    <aside>
    💡 **항상 Data(feature) = 2차원, 정답(레이블) = 1차원**
    
    </aside>
    
    `**x.fit(Data)**` 
    
    - 비지도학습
    - **샘플(sample), DataPoint** : 하나의 **행**
    - **특성(feature)** : 샘플의 속성, 즉 열의 특성을 의미. 통계학에서는 독립변수(설명변수)라고 함.
    - **레이블(label)** = Data(feature)의 값에 대응되는 값
    - **클래스(class)** = 레이블(label)의 종류
6. **예측 및 평가**
    
    `**x.predict()**`
    
    ****************************************************************************************`**kn.score(2차원 배열, 1차원 정답)`** 
    
    - 예측 후 스스로 평가함
    
    ******************************************************************`**accuracy_score(정답, 예측값)**`******************************************************************
    
    - 예측한 값을 `predict()` 로 얻은 뒤에 할당해 주어야함.

## 과적합

**과대적합(overfitting)**

- 훈련 Data에서만 예측성능이 높고 그 이외의 Data는 예측 성능이 낮은 경우 ⇒ **일반화 성능**이 떨어짐

<aside>
❓ **이유?
-** 훈련을 너무 많이 한 경우
- 모델이 복잡한 경우

</aside>

<aside>
💡 **해결 방안
-** 학습량을 줄인다
- 모델 간소화

분류: 하이퍼 파라미터 수용
회귀: 규제(regularization)
          L2 규제(Ridge) ⇒ 릿지
          L1 규제(Lasso) ⇒ 라쏘
          엘라스틱넷(elastic net) ⇒ L2 + L1

</aside>

******************************과소적합(underfitting)******************************

- 훈련 Data 및 이외 Data 모두 예측 성능이 낮은 경우

<aside>
❓ **이유?**
- 훈련을 너무 적게 한 경우(Data가 적은 경우)
- 모델 간소화 경우

</aside>

<aside>
💡 **해결 방안
-** 학습량을 늘린다
- 모델 복잡화

</aside>

### 규제(과대적합 방지)

- **L2 규제(Ridge)**
    - 회귀 계수 값은 **0으로 근접**. 값 결정에 미미함.
- **L1 규제(Lasso)**
    - 회귀 계수 값을 **0으로 만들어버림**.
- **엘라스틱넷(elastic net)**
    - L2 + L1

### 회귀(Regression)

**x에 대한 y의 값 예측**

- 잔차(residual)이 최소가 되게 하는 것
- 직선(기울기와 절편)을 잘 그리면 된다

<aside>
💡 **************************단순회귀**************************
y = w1(기울기)x+w0(절편)

**feature가 여러개가 되는 경우(다중회귀)**
 ⇒ ****y = w1x1 + w2x2 + w3x3 + w4x4 + … + w0

</aside>

- **다항 회귀 변경하는법 (PolynomialFeatures)**
    
    ```python
    from sklearn.preprocessing import PolynomialFeatures
    
    poly = PolynomialFeatures(degree=2, include_bias=False)
    poly.fit(X_train2D) # => 훈련값 할당 (2차원)
    train_poly = poly.transform(X_train2D)
    test_poly = poly.transform(X_test2D)
    ```
    
- ****************손실함수(비용함수) ⇒ (cost function, loss function) → 경사하강법****************
    - **MSE** : 제곱으로 계산 ⇒ **미분**이 가능하기 때문에 가장 많이 사용된다.
    - **MAE** : 절대값으로 계산
    - **R**2** : 결정계수
    - ****************RMSE**************** : MSE에 루트를 씌운 것

**특징**

- 독립성 : feature들 간 독립적 ⇒ 상관계수 이용
- 정규성 : 정규분포따름 ⇒ hist이용
- 선형성 ⇒ 시각화

********평가********

`lr.score()` ⇒ 분류알고리즘에서 사용했던 정확도가 아닌 R2(결정계수)이다.

⇒ 생성된 모델이 얼마나 실제값이 잘 표현되었는지 알려주는 지표.

<aside>
❓ **회귀 알고리즘이 학습하는 것?**
    ⇒ 기울기와 절편을 구하는 것이다.
         `y= W1X + W0`

</aside>

### KNN(K-Nearest Neighbors)

**********************************가장 가까운 k개의 샘플에서 다수의 클래스를 그 샘플의 클래스로 예측한다.**********************************

- **********장점**********
    - 알고리즘이 간단하여 구현하기 쉽다.
    - 훈련이 필요 없다.
    - 수치 기반 데이터 분류 작업에서 성능이 탁월하다.
- ********단점********
    - 데이터의 양이 맣아지면 분류 속도가 느려진다.
    - 차원(벡터)의 크기가 크면 계산량이 많아진다.
    - 거리기반 알고리즘이기 때문에 반드시 ********************************데이터 표준화********************************를 해 주어야 한다.

## 분류 알고리즘(종류 예측)

### 1. 데이터 수집

### 2. 데이터 전처리

### 3. 데이터 분리 (훈련데이터, 테스트데이터)

- **train_test_split**

### 4. 스케일링(표준화 : StandardScale)

- `sc = StandardScaled()`
    
    ```python
    sc.transform(x_train)
    sc.transform(x_test)
    sc.transform(new 값)
    ```
    

### 5. 모델 생성 및 훈련

- `x = xxxclassifier`
    
    ```python
    x.fit(2차원 Data, 1차원 레이블)
    ```
    

### 6. 예측

- `x.predict(2차원Data)`

### 7. 평가

- `x.score(data, label)` : 정확도

## 회귀 알고리즘(값 예측)

### 1. 데이터 수집

### 2. 데이터 전처리

### 3. 데이터 분리 (훈련데이터, 테스트데이터)

- **train_test_split**

### 4. 스케일링(표준화 : StandardScale)

- `sc = StandardScaled()`
    
    ```python
    sc.transform(x_train)
    sc.transform(x_test)
    sc.transform(new 값)
    ```
    

### 5. 모델 생성 및 훈련

- `x = LinearRegression()`
    
    ```python
    x.fit(2차원Data, 1차원 레이블)
    ```
    

### 6. 예측

- `x.predict(2차원Data)`

### 7. 평가

- `x.score(data, label)` : 정확도X ⇒ R**2 (**결정지수**)

<aside>
💡 R은 상관계수(-1 ~ 1)이다

</aside>

## 교차 검증(Cross Validation)

kfold

- `KFold(n_splits=5, shuffle=False, random_state=None)`
    - n_split : 데이터를 몇 등분으로 나눌지
    - shuffle: 데이터 순서 섞기
    - random_state: shuffle로 섞은 데이터 고정하는 역할(seed), 근데 shuffle로 실행될 때마다 순서를 섞어서 그런지 제 기능을 못하는 모양이다.

```python
kf = KFold(n_splits=5, shuffle=False, random_state=None)
gen = kf.split(iris_data)

X_train, X_valid =  next(gen) # => generate함수로 값을 하나씩 꺼내서 사용한다.
X_train, X_valid, len(X_train), len(X_valid)

from sklearn.metrics import accuracy_score
score1_list=[]
score2_list=[]
for train_index, valid_index in kf.split(iris_data): # => 인덱스값 리턴
		# print(train_index, valid_index)
    # 인덱스이용해서 실제 데이터 얻기
    X_train, X_valid = iris_data[train_index], iris_data[valid_index]
    y_train, y_valid = iris_target[train_index], iris_target[valid_index]
    # 모델 훈련
    dt.fit(X_train, y_train)
    # 예측
    pred = dt.predict(X_valid)
    # 평가
    score1 = dt.score(X_valid, y_valid)
    score2 = accuracy_score(y_valid, pred)
    
    score1_list.append(score1)
    score2_list.append(score2)    

print(score1_list)
print(score2_list)
print("평균", np.mean(score1_list))
```

**stratified Fold (불균형 데이터에 사용)**

```python
from sklearn.model_selection import StratifiedKFold
kf = StratifiedKFold(n_splits=3, random_state=None, shuffle=False) # 이슈를 발생시키기 위하여 n_splits를 3으로 지정

from sklearn.metrics import accuracy_score

for i, (train_index, valid_index) in enumerate(kf.split(iris_data, iris_target)):
     label_train = df['species'].iloc[train_index]
     label_valid = df['species'].iloc[valid_index]
```

**cross_val_validate()**

```python
from sklearn.model_selection import cross_validate
scores = cross_validate(dt, iris_data, iris_target, cv=5,
                        scoring="accuracy",return_train_score=True,
                         return_estimator=True)
```

**cross_val_score()**

```python
from sklearn.model_selection import cross_val_score
test_score = cross_val_score(dt, iris_data, iris_target, cv=5,
                            scoring="accuracy")
```
