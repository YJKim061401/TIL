# Logistic Regression

* 선형 회귀 방식을 기반으로 하되 시그모이드 함수
* 선형 회귀 방식을 분류에 적용한 알고리즘 
* predict_proba()라는 예측 확률을 기반으로 분류한 것 처럼
* 시그모이드 함수의 최적선을 찾고 이 시그모이드 함수의 반환값을 확률로 간주해 분류를 결정



### 로지스틱 회귀 예제 - 위스콘신 유방암 데이터 세트 이용하여 암 여부 판단

```python
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline

from sklearn.datasets import load_breast_cancer
from sklearn.linear_model import LogisticRegression

cancer = load_breast_cancer()

from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split

# 선형 회귀 계열의 로지스틱 회귀는 데이터의 정규 분포도에 따라
# 예측 성능 영향을 받을 수 있으므로
# 먼저 정규 분포 형태의 표준 스케일링을 적용한 뒤
# 학습/테스트 데이터 세트 분리 

# 표준화 작업 (평균이 0 분산 1로 데이터 분포도 변환)
scaler = StandardScaler()
data_scaled = scaler.fit_transform(cancer.data)

x_train,x_test,y_train,y_test = train_test_split(data_scaled, cancer.target, test_size=0.3,random_state=0)

# 로지스틱 회귀를 이용해 학습 및 예측 수행
from sklearn.metrics import accuracy_score, roc_auc_score
lr_clf = LogisticRegression(solver='liblinear')
lr_clf.fit(x_train,y_train)
lr_preds = lr_clf.predict(x_test)

# 정확도와 roc_auc 측정
print('accuracy : {0:.3f}'.format(accuracy_score(y_test,lr_preds)))
print('roc_auc : {0:.3f}'.format(roc_auc_score(y_test,lr_preds)))

[output]
accuracy : 0.977
roc_auc : 0.972
```

* 버전 변경으로 solver='liblinear' 적어줌!
* 이전 버전은 default 가 solver='liblinear' 였음 
* 현재 버전은 default가 solver='lbfgs'
*  solver : weight 값을 최적화 유형을 구분하는 것 



#### Logistic Regression 클래스의 주요 하이퍼 파라미터

penalty : 규제 유형 설정 (l1,l2) l2가 기본

c : 규제 강도를 조절하는 alpha값의 역수

c값이 작을수록 규제 강도가 커짐 

```python
# GridSearchCV 이용하여 하이퍼 파라미터 최적화
from sklearn.model_selection import GridSearchCV
params = {'penalty':['l2','l1'],
'C':[0.01,0.1,1,1,5,10]}

grid_clf = GridSearchCV(lr_clf,param_grid=params,scoring='accuracy',cv=3)
grid_clf.fit(data_scaled,cancer.target)
print('최적 하이퍼 파라미터 : {0}, 최적 평균 정확도 {1:.3f}'.format(grid_clf.best_params_, grid_clf.best_score_))

[output]
최적 하이퍼 파라미터 : {'C': 0.1, 'penalty': 'l2'}, 최적 평균 정확도 0.979
```



* 로지스틱 회귀는 가볍고 빠르고 예측 성능도 뛰어남
* 로지스틱 회귀를 이진 분류의 기본 모델로 사용하는 경우가 많음
* 희소한 데이터 세트 분류에도 뛰어난 성능을 보여 텍스트 분석에도 자주 사용 

