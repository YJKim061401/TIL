# 분류

* 지도학습의 대표적 유형 
* 기존 데이터가 어떤 레이블에 속한지 알고리즘을 통해 패턴을 이지하고 새롭게 관측된 데이터에 대한 레이블 판별

# 2. 앙상블 학습

* 다양한 분류기의 예측 결과를 결합함으로써 단일 분류기보다 신뢰성이 높은 예측값을 얻는 것이 목표 
* 대부분의 정형 데이터 분류 시에는 앙상블이 뛰어난 성능
* 랜덤 포레스트 & 그래디언트 부스팅 알고리즘이 대표적 
* 앙상블 학습의 유형
  * 보팅 (voting)
    * 여러개의 분류기가 투표를 통해 최종 예측 결과를 결정 
    * 서로 다른 알고리즘을 가진 분류기를 결합
    * e.g. linear regression, knn, support vector machine 3개의 알고리즘이 같은 데이터 세트에 대해 학습하고 예측한 결과 가지고 최종 예측 결과 선정
  * 배깅 (bagging)
    * 여러개의 분류기가 투표를 통해 최종 예측 결과를 결정 
    * 각각의 분류기가 모두 같은 유형의 알고리즘 기반, 데이터 샘플링을 서로 다르게 학습 수행
    * e.g. Decision tree로 여러 분류기가 학습으로 개별 예측 
  * 부스팅 (boosting)
    * 앞에서 학습한 분류기가 예측이 틀린 데이터에 대해서는 올바르게 예측할 수 있도록 다음 분류기에게는 가중치를 부여하면서 학습과 예측을 진행 

### 보팅의 유형 (hard / soft)

#### hard

다수결 원칙 

예측한 결과값들중 다수의 분류기가 결정한 예측값을 최종 보팅 결과값으로 선정하는 것

#### soft

분류기들의 레이블 값 결정 확률을 모두 더하고 이를 평균해서 이들 중 확률이 가장 높은 레이블 값을 최종 보팅 결과값으로 선정 

일반적으로 soft voting방법 이용 



```python
# 개별 모델은 로지스틱 회귀와 KNN
lr_clf = LogisticRegression(solver='liblinear')
knn_clf = KNeighborsClassifier(n_neighbors=8)

# 개별 모델을 소프트 보팅 기반의 앙상블 모델로 구현한 분류기
vo_clf = VotingClassifier(estimators=[('LR',lr_clf),('KNN',knn_clf)],voting='soft')

X_train,X_test,y_train,y_test = train_test_split(cancer.data, cancer.target, test_size=0.2,random_state=156)

# votingclassifier 학습/예측/평가
vo_clf.fit(X_train, y_train)
pred = vo_clf.predict(X_test)
print('Voting분류기 정확도 : {0:.4f}'.format(accuracy_score(y_test,pred)))

classifiers = [lr_clf,knn_clf]
for classifier in classifiers:
    classifier.fit(X_train,y_train)
    pred = classifier.predict(X_test)
    class_name = classifier.__class__.__name__
    print('{0}정확도 : {1:.4f}'.format(class_name, accuracy_score(y_test,pred)))

[output]
Voting분류기 정확도 : 0.9561
LogisticRegression정확도 : 0.9474
KNeighborsClassifier정확도 : 0.9386
```

* 결과
* 보팅 분류기의 정확도가 조금 높게 나타남
* 보팅으로 여러개의 분류기를 결합한다고 해서 무조건 성능이 향상되지는 않음
* 그래도 보팅, 배깅, 부스팅 등의 앙상블 방법은 전반적으로 다른 단일 ML 알고리즘보다는 어느정도 뛰어난 예측 성능을 가지는 경우가 있음 
* 고정된 데이터 세트에서 단일 ML 알고리즘이 뛰어난 성능을 발휘하더라도 현실 세계는 다양한 변수와 예측이 어려운 규칙으로 구성되어 있기 때문에 다양한 관점을 가진 알고리즘이 서로 결합해서 더 나은 성능을 실제 환경에서 이끌어낼수있음