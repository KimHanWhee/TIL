PlayData_MachineLearning (2022/12/12 ~ 2022/12/16)
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
        - Regression
            - 회귀 모델 : 값 예측
        
        <aside>
        💡 LogisticRegression ⇒ 예외적으로 분류 모델이다.
        
        </aside>
        
    
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

## 분류

## 회귀(Regression)

**x에 대한 y의 값 예측**

- 잔차(residual)이 최소가 되게 하는 것
- 직선(기울기와 절편)을 잘 그리면 된다

<aside>
💡 **************************단순회귀**************************
y = w1(기울기)x+w0(절편)

**feature가 여러개가 되는 경우(다중회귀)**
 ⇒ ****y = w1x1 + w2x2 + w3x3 + w4x4 + … + w0

</aside>

- **********************다항 회귀**********************
    - PloynomialFeatures 이용
        - 과적합 발생 가능성 높음
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

- **독립성** : feature들 간 독립적(**다중공선성** 문제발생) ⇒ 상관계수 이용
- **정규성** : 정규분포따름 ⇒ hist이용
- **선형성** ⇒ 시각화

********평가********

`lr.score()` ⇒ 분류알고리즘에서 사용했던 정확도가 아닌 R2(결정계수)이다.

⇒ 생성된 모델이 얼마나 실제값이 잘 표현되었는지 알려주는 지표.

<aside>
❓ **회귀 알고리즘이 학습하는 것?**
    ⇒ 기울기와 절편을 구하는 것이다.
         `y= W1X + W0`

</aside>

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
    - 영향력이 낮은 feature들에 해당되는 회귀 계수 값을 **0으로 근접**. 값 결정에 미미함.
- **L1 규제(Lasso)**
    - 영향력이 낮은 feature들에 해당되는 회귀 계수 값을 **0으로 만들어버림**.
- **엘라스틱넷(elastic net)**
    - L2 + L1

### KNN(K-Nearest Neighbors)

**********************************가장 가까운 k개의 샘플에서 다수의 클래스를 그 샘플의 클래스로 예측한다.**********************************

- **********장점**********
    - 알고리즘이 간단하여 구현하기 쉽다.
    - 훈련이 필요 없다.
    - 수치 기반 데이터 분류 작업에서 성능이 탁월하다.
- ********단점********
    - 데이터의 양이 맣아지면 분류 속도가 느려진다.
    - 차원(벡터)의 크기가 크면 계산량이 많아진다.
    - 거리 기반 알고리즘이기 때문에 반드시 ********************************데이터 표준화********************************를 해 주어야 한다.

## 분류 알고리즘(종류 예측)

### 1. 데이터 수집

### 2. 데이터 전처리

### 3. 데이터 분리 (훈련데이터, 테스트데이터)

- **train_test_split**

### 4. 스케일링(표준화 : StandardScaler)

- `sc = StandardScaler()`
    - 평균을 0, 분산을 1로 만들어줌
    
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
    sc.fit(x_train) 
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

- 기본적으로 여러가지 데이터를 반환해줌

```python
from sklearn.model_selection import cross_validate
scores = cross_validate(dt, iris_data, iris_target, cv=5,
                        scoring="accuracy",return_train_score=True,
                         return_estimator=True)
```

**cross_val_score()**

- test_score(검증 데이터)만 반환

```python
from sklearn.model_selection import cross_val_score
test_score = cross_val_score(dt, iris_data, iris_target, cv=5,
                            scoring="accuracy")
```

## 평가 지표

- ******분류******
    - 정확도(accuracy)
    - 정밀도(precision)
    - 재현율(recall)
- ******회귀******
    - R2(결정계수
    - MSE
    - MAE

## 선형모델

### 분류

### 로지스틱 회귀(logistic regression)

`**LogisticRegression(penalty='12', C=1.0)**`

- 기본적으로 L2규제(Ridge)됨. 규제 강도는 C 파라미터 사용.
- Ridge/Lasso 와 다르게 값이 작을수록 규제가 강해진다. 즉, 규제하면 할수록 0에 근사하는 feature들이 늘어난다.
1. y = W1X + W0 으로 구함
2. 회귀식에서 나온 값(예측값)
3. 활성화 함수(activation function) : 확률갑(0~1) 압출 [음성확률, 양성확률] ⇒ 확률값의 총 합은 1
    - **이진분류**
        - **시그모이드(sigmoid)**
            - 활성화 함수
            
            ```python
            # 시그모이드 함수
            from scipy.special import expit
            expit(선형방정식 연산 값)
            # 확률 출력
            ```
            
    - **다중분류**
        - **소프트 맥스(Softmax)**
            - 활성화 함수
            - 값이 일정이상 크면 값을 더 크게 설정하게 만든다.
            - 내부적으로 이진분류 여러번 시행.
        - **********확률**********
            - Probability: 0~1 (경우의 수)
            - Stochastic: 랜덤, 무작위
    - **용도**
        - 비선형
        - 특정 범위로 Data압축할 때 ⇒ 0~1
4. 확률값 중 더 큰값을 가진 class(종류)로 분류한다.

<aside>
💡 ********************함수종류********************

비용(손실)함수 : 회귀에서의 평가 지표 ⇒ MSE, MAE, R2…
최적의 기울기(가중치) 구함

활성화 함수 : 선형 ⇒ 비선형, 임의의 값을 특정범위로 압출
⇒ 시그모이드(sigmoid), 소프트 맥스(softmax), 렐루(ReLu)

</aside>

- **predict_proba**(값)
    - 넣어준 값에 대한 확률 출력, 다음 코드의 경우에는 [”Bream”, “Smelt”] 값들에 대한 확률이다.
    
    ```python
    lr.predict_proba(X_test_bream_smelt)
    '''
                  ['Bream', 'Smelt']
    ['Bream', 'Bream', 'Bream', 'Bream', 'Smelt', 'Bream', 'Bream', 'Bream', 'Smelt']
    array([[9.99519284e-01, 4.80716220e-04], ==> Bream
           [9.92393891e-01, 7.60610858e-03], ==> Bream
           [9.94739349e-01, 5.26065097e-03], ==> Bream
           [9.86879297e-01, 1.31207034e-02], ==> Bream
           [2.94381468e-02, 9.70561853e-01], ==> Smelt
           [9.81104791e-01, 1.88952091e-02], ==> Bream
           [9.99386081e-01, 6.13918916e-04], ==> Bream
           [9.94227953e-01, 5.77204706e-03], ==> Bream
           [1.91841997e-02, 9.80815800e-01]])==> Smelt
    '''
    ```
    

### 회귀

### LinearRegression

### ************확률적 경사하강법 모델************

- **확률적 경사하강법, SGDclassifier (Stochastic Gradient Descent)**
    - scikit-learn 제공
    - 무작위로 Data를 **하나씩** 추출해서 훈련하는 모델
    - `loss = "log-loss" (1.1버전에서는 log)` ⇒ cross entropy, loss
    - `learning-rate` ⇒ **학습율**, 그래프상에서 보폭 역할
        - 보폭이 작으면 시간이 오래 걸림, 반대로 너무 크면 최적의값을 그냥 지나쳐 버릴 수도 있다.
        - 미분이용
- **미니 배치 경사하강법**
    - 무작위로 Data를 **여러개**를 묶음으로 ****추출해서 훈련하는 모델
    - batch size는 적절한 그기가 성능에 좋다.
- **배치 경사하강법**
    - Data를 **전부** 추출해서 훈련하는 모델

<aside>
💡 **경사하강법 알고리즘
y = w1 * x + w0
⇒** 손실함수(loss function)가 반환되는 값(잔차)이 최소가 되는 경우

</aside>

### 손실 함수(loss function)

- ********분류********
    - **이진분류: 이진 크로스 엔트로피(binary cross entropy)**
    - **다중분류: 크로스 엔트로피 (cross entropy)**
- ********회귀********
    - **MAE**
    - **MSE**
- **max_iter** = epoch 반복 횟수
    - 내부적으로 성능이 좋아지지 않으면(loss값이 더 이상 작아지지않는 경우) 중단된다.
    
    <aside>
    💡 기준?
    loss > best_los - tol (허용 오차)
    * tol=None 지정 시 무조건 반복횟수 만큼 실행됨
    * early stopping ⇒ 어떤 모델들은 훈련중에  loss값이 더 이상 나아지지 않으면 중간에 중단시키는 모델이 있다.
    
    </aside>
    

## 분류 평가 지표

- **이진분류**
    - ****0: (음성, negative)****
    - ****1: (양성, positive)****
- ********************오차행렬(confusion matrix) 이용********************
    
    ![image](https://user-images.githubusercontent.com/84313936/208068786-0fb6a464-ae80-49bf-bd48-baedf3eacae5.png)

    
    - **정확도(accuracy_score)**
        - 일치한 개수 / 전체Data = TN + TP / TN + FP + FN + TP
    - **정밀도(precision_score)**
        - 예측값과 실제값이 양성으로 일치한 개수 / 양성으로 예측한 값 = TP / TP + FP
    - **재현율(recall_score)**
        - 예측값과 실제값이 양성으로 일치한 개수 / 실제값이 양성인 개수 = TP / TP + FN ⇒ 업무상 리스크가 매우 크다.
    - **조화 평균(F1 Score)**
        - 정밀도와 재현율이 조화로운지
        
        <aside>
        💡 정확도, 정밀도, 재현율은 클 수록 좋다.
        
        </aside>
        

### 신뢰 레벨 (confidence score)

- 낮을수록 **덜** 엄격해짐
    - 정밀도 down
    - 재현율 up
- 높을수록 **더** 엄격해짐
    - 정밀도 up
    - 재현율 down
