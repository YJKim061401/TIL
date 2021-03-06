# 머신러닝에서의 데이터 전처리 과정

**ML 알고리즘** 은 데이터에 기반하고 있기 때문에 어떤 데이터를 입력하느냐에 따라 결과도 크게 달라짐



### 사이킷런 ML 알고리즘 적용 전 기본 처리 사항

1. 결손값 처리
   - NaN, Null 값 허용 안되므로 고정값으로 변환해야함
   - 평균값 대체, 해당 피처 제외 등

2. 문자열 값 처리

   * 문자열 값을 입력 값으로 허용하지 않음

   * 인코딩 처리하여 숫자형으로 변환

   * 카테고리형 피처는 코드값으로 표현

     * 대표적 인코딩 방식
       * 레이블 인코딩 : 문자열 카테고리 값을 숫자형 카테고리 값으로 변환 
       * 원핫 인코딩

   * 텍스트형 피처는 피처 벡터화 기법으로 벡터화 시킴

     * #### 피처 벡터화 : 텍스트를 숫자형 벡터 값으로 변환하는 것

3. 피처 스케일링

   * 서로 다른 변수의 값 범위를 일정한 수준으로 맞추는 작업
   * 표준화(standardization)와 정규화(normalization)
   * 사이킷런에서 제공 
   * StandardScaler()
   * MinMaxScaler()



## 피처 스케일링

### StandardScaler()

* 개별 피처를 가우시안 정규 분포로 변환 
* 데이터가 가우시안 분포를 가지고 있다고 가정함 
  * Support Vector Machine
  * Linear Regression
  * Logistic Regression

```python
from sklearn.preprocessing import StandardScaler
# standardscaler객체 생성
scaler = StandardScaler()

# fit()과 transform() 호출 
scaler.fit(df)
df_scaled = scaler.transform(df)

# transform() 하면 데이터 세트가 ndarray로 반환
# ndarray를 다시 dataframe으로 변환
df_scaled = pd.DataFrame(data=df_scaled,columns=data.feature_names)
```

* 결과 : 모든 컬럼 값의 평균이 0에 아주 가까운 값으로, 분산은 1에 아주 가까운 값으로 변환 



### MinMaxScaler()

* 데이터 값을 0과 1사이의 범위 값으로 변환 (음수값이 있다면 -1에서 1값으로 변환)
* 데이터의 분포가 가우시안 분포가 아닐 경우에 적용가능

```python
from sklearn.preprocessing import MinMaxScaler

# minmaxscaler객체 생성
scaler = MinMaxScaler()

# fit()과 transform()호출
scaler.fit(df)
df_scaled = scaler.transform(df)

# transform() 하면 데이터 세트가 ndarray로 반환
# ndarray를 다시 dataframe으로 변환
df_scaled = pd.DataFrame(data=df_scaled,columns=data.feature_names)
```

* 결과 : 모든 피처에 0에서 1사이의 값으로 변환되는 스케일링이 적용 



### 유의점!

학습 데이터 세트와 테스트 데이터 세트에 **Scaler객체를 이용해 **fit()과 transform()을 적용하면 테스트 데이터 세트로는 다시 fit()을 수행하지 않고 학습 데이터 세트로 fit()을 수행한 결과를 이용해 transform() 변환을 적용해야함

즉, 학습 데이터로 fit()이 적용된 스케일링 기준 정보를 그대로 테스트 데이터에 적용

`scaler.fit(df)` 



1. 가능한 전체 데이터의 스케일링 변환을 적용한 뒤 학습과 테스트 데이터로 분리

   scaler.fit() --> scaler.transform() --> train_test_split()

2. 불가능한 경우 테스트 데이터 변환 시에는 fit()이나 fit_transform()을 적용하지 않고 핛습 데이터로 이미 fit()된 Scaler객체를 이용해 transform()으로 반환 

## ML 분류 예측 수행 프로세스 

sklearn에서 제공하는 메소드 

* Fit() : ML 모델 학습
* predict() : 학습된 모델의 예측 

fit()과 predict() 메소드 사용해서 학습과 예측 결과 리턴 



* 데이터 세트 형태
* data : 피처 데이터 세트 (ndarray)
* target : 분류일 경우 레이블 값, 회귀일 경우 숫자 결과값 데이터 세트 (ndarray)
* target_names : 개별 레이블 이름 (ndarray or list)
* feature_names : 피처 이름 (ndarray or list)
* DESCR : 데이터 세트 설명, 각 피처 설명 (string)



### 모델 구축 프로세스

### 1. 피처의 가공, 변경, 추출을 수행하는 피처 처리

### 2. ML 알고리즘 학습/예측 수행 fit() / predict()

### 3. 모델 평가

### 위의 1,2,3 단계를 반복적으로 수행 



