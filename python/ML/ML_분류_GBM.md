# GBM (Gradient Boosting Machine)

여러개의 약한 학습기를 순차적으로 학습-예측하면서 잘못 예측한 데이터에 가중치 부여를 통해 오류를 개선해 나가면서 학습하는 방식 

성능은 좋은데 속도는 느림

#### 1. AdaBoost

#### 2. GBM 

AdaBoost와 GBM의 차이점은 가중치를 부여하는 방식

* GBM에서는 가중치를 부여할 때 Gradient Descent를 사용

#### Gradient Descent

오류값 = 실제값 - 예측값 

오류식 = 실제 결과값 - 예측함수 

h(x) = y - F(x)

위의 오류식을 최소화하는 방향성을 가지고 반복적으로 가중치 값을 업데이트 하는 것 = Gradient Descent

```python
from sklearn.ensemble import GradientBoostingClassifier
from sklearn.metrics import accuracy_score
import time
import warnings
warnings.filterwarnings('ignore')

X_train,X_test, y_train, y_test = get_human_dataset()

# GBM 수행시간 측정
start_time = time.time()

gb_clf = GradientBoostingClassifier(random_state=0)
gb_clf.fit(X_train,y_train)
gb_pred = gb_clf.predict(X_test)
gb_accuracy = accuracy_score(y_test,gb_pred)

print('GBM 정확도 : {0:.4f}'.format(gb_accuracy))
print('GBM 수행 시간 : {0:.1f}초'.format(time.time()-start_time))

[output]
GBM 정확도 : 0.9393
GBM 수행 시간 : 531.1초

# 결과
# 기본 하이퍼 파라미터만으로도 93.93%의 예측 정확도로
# 앞의 튜닝된 하이퍼 파라미터로 재학습 및 예측/평가한 
# 랜덤 포레스트보다 나은 예측 성능을 나타냄 
# 랜덤 포레스트 예측 정확도 : 0.9165

# 일반적으로 GBM이 랜덤 포레스트보다 예측 성능이 조금 뛰어난 경우가 많음
# 문제 : 시간이 오래걸리고 하이퍼 파라미터 튜닝 노력도 필요함
# 데이터 커지면 커질수록 너무 오래 걸려서
# 하이퍼 파라미터 튜닝하기 많이 어려움 

# 랜덤 포레스트의 경우 상대적으로 빠른 수행 시간을 보장해주기 때문에 더 쉽게 예측 결과 도출 가능 
```

#### GBM 주요 하이퍼 파라미터

n_estimators : weak learner 개수 (default : 100)

* 개수가 많을수록 예측 성능 일정 수준까지 좋아질 수 있으나 시간 오래 걸림

Learning_rate : GBM학습 진행할 때 적용하는 학습률 (default:0.1)

* 0-1사이의 값
* 작은 값 적용하면 업데이트 되는 값이 작아져서 최소 오류값을 찾아 예측 성능이 높아지지만 시간 오래걸림

Subsample : weak learner 학습에 사용하는 데이터 샘플링 비율 (default:1)

* e.g. 1 = 전체 학습 데이터 기반으로 학습
* e.g. 0.5 = 학습 데이터의 50%
* 과적합이 염려되는 경우 1보다 작은 값으로 설정 



```python
# GBM하이퍼 파라미터 및 튜닝 
# 이번꺼는 실행 안시킬거임 (너무 오래걸려서)
from sklearn.model_selection import GridSearchCV

params = {
    'n_estimators':[100,500],
    'learning_rate':[0.05,0.1]
}

grid_cv = GridSearchCV(gb_clf,param_grid =params, cv=2,verbose=1)
grid_cv.fit(X_train,y_train)
print('최적 하이퍼 파라미터:\n', grid_cv.best_params_)
print('최고 예측 정확도: {0:.4f}'.format(grid_cv.best_score_))

# 최적으로 학습된 estimator로 예측 수행
gr_pred = grid_cv.best_estimator_.predict(X_test)
gb_accuracy = accuracy_score(y_test,gb_pred)
print('GBM 정확도:{0:.4f}'.format(gb_accuracy))
```



# XGBoost (eXtra Gradient Boost)

* https://xgboost.readthedocs.io/en/latest/python/python_api.html
* 분류에 있어서 뛰어난 예측 성능
  * 일반적으로 분류와 회귀 영역에서 뛰어난 예측 성능 발휘
* 빠른 수행시간
  * 일반적인 GBM은 순차적으로 weak learner가 가중치를 증감하는 방식으로 학습하기 때문에 전반적으로 속도가 느림
  * XGBoost는 병렬 수행 가능 
* 과적합 규제
  * 표준 GBM의 경우 과적합 규제 기능이 없으나
  * XGBoost는 자체에 과적합 규제 기능이 있어서 과적합에 좀 더 강한 내구성이 있음 
* 가지치기
* 교차 검증 내장
* 결손값 자체 처리

XGBoost의 조기 중단 기능 (Early Stopping)

* 지정한 수만큼의 부스팅 반복 작업이 종료되지 않더라도 예측 오류가 더 이상 개선되지 않으면 중간에 중지해서 수행 시간을 단축 
* 반복 횟수를 단축할 경우, 예측 성능 최적화가 안된 상태에서 학습이 종료 될 수 있으므로 주의

evals 파라미터에 학습 데이터 세트와 eval 데이터 세트를 명기해주면 평가를 eval 데이터 세트에 수행하면서 조기 중단 적용 가능

조기중단을 수행하려면 반드시 eval파라미터에 eval데이터 세트를 명기해주어야 함

eval_set : 성능 평가를 수행할 평가용 데이터 세트를 설정

eval_metric : 평가 세트에 적용할 성능 평가 방법, 분류일 경우 주로 **'error(분류 오류)'** , **'logloss'**를 사용

* logloss : 모델이 예측한 확률 값을 직접적으로 반영하여 평가 



```python
import xgboost as xgb
from xgboost import plot_importance
import pandas as pd
import numpy as np
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import warnings
warnings.filterwarnings('ignore')

dataset = load_breast_cancer()
X_features = dataset.data
y_label = dataset.target

cancer_df = pd.DataFrame(data = X_features, columns =dataset.feature_names)
cancer_df['target'] = y_label
cancer_df.head(10)

print(dataset.target_names)
print(cancer_df['target'].value_counts())

# malignant (악성) = 0
# benign (양성) = 1

X_train,X_test, y_train,y_test = train_test_split(X_features, y_label, test_size=0.2,random_state=156)
print(X_train.shape, X_test.shape)

# 학습/테스트 데이터 세트를 DMatrix로 변환
dtrain = xgb.DMatrix(data =X_train, label = y_train)
dtest = xgb.DMatrix(data=X_test,label=y_test)

# 하이퍼 파라미터 설정 (딕셔너리 형태)
params = {'max_depth':3,
'eta': 0.1, # 학습율
'objective':'binary:logistic', # 예제 데이터가 0 또는 1인 이진분류이므로 목적함수는 이진로지스틱 (binary:logistic)
'eval_metric':'logloss', # 오류 함수의 평가 성능 지표를 logloss
'early_stoppings':100 # 조기 중단 할 수 있는 최소 반복 횟수
}

num_rounds = 400 # 부스팅 반복 횟수는 400회

# train 데이터 세트는 'train', evaluations(test) 데이터세트는 'eval'로 명기
wlist = [(dtrain,'train'),(dtest,'eval')]
# 하이퍼 파라미터와 early stopping파라미터를 train()함수의 파라미터로 전달
xgb_model = xgb.train(params=params,dtrain=dtrain,num_boost_round=num_rounds,early_stopping_rounds=100,evals=wlist)

# 학습이 완료, 이제 이를 이용해 테스트 데이터 세트 예측 수행
pred_probs = xgb_model.predict(dtest)
print('predict() 수행 결과값을 10개만 표시, 예측 확률값으로 표시됨')
print(np.round(pred_probs[:10],3))

# 예측 값을 결정하는 로직 추가
# 예측 확률이 0.5보다 크면 1, 그렇지 않으면 0으로 예측값 결정해 리스트 객체인 preds에 저장
preds = [1 if x > 0.5 else 0 for x in pred_probs]
print('예측값 10개만 표시:',preds[:10])
```

