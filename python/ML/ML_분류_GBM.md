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

