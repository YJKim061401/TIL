# ML 성능 평가지표

### 정확도

문제점 : 데이터 구성에 따라 모델 성능 왜곡 가능성

* 이진분류에서 불균형한 데이터 세트 
* = 불균형한 레이블 값 분포에서 ML 모델의 성능 판단 어려움 

정확도만으로만 모델 성능을 평가하지 않고 여러가지 분류 지표와 함께 사용 



### 오차행렬

##### Confusion_matrix(y_test, pred)

```python 
결과 
array([[405,   0],     
       [ 45,   0]])

       [[TN, FP],  

          [FN, TP]]
```



머신러닝 모델의 예측이 얼마나 잘 한 예측인지를 판단하는 기준

<img src="ML_성능평가지표.assets/Structure-of-the-confusion-matrix-with-TP-FN-FP-and-TN-values.png" alt="Structure of the confusion matrix with TP, FN, FP and TN values. | Download  Scientific Diagram" style="zoom:33%;" />

정확도 = 예측 결과와 실제 값이 동일한 건수 / 전체 데이터 수 

**(TN+TP) / (TN+FP+FN+TP)**

문제점 : 여전히 불균형한 이진 분류 데이터 세트에서는 negative로 예측 정확도 높아지는 경향 발생 (TN커지고 TP 작아짐) 왜? Positive 데이터 건수가 매우 작기 때문에 

그래서 불균형 데이트 세트에서 더 선호되는 평가 지표로는 정밀도와 재현율 



### 정밀도 & 재현율

positive예측 성능에 더 초점을 맞춤 (모두 TP를 높이는데 초점)

**정밀도 = TP/(FP + TP)**  (FN을 낮추는데 초점) 실제 pos 예측 neg

**재현율 = TP / (FN + TP)** (FP를 낮추는데 초점) 실제 neg 예측 pos 

정밀도 & 재현율 모두 높은 수치를 얻는 것이 바람직함 

임계값을 조절하여 정밀도와 재현율의 성능 수치를 상호 보완적으로 조정

**분류결정임계값** : positive 예측값을 결정하는 확률의 기준

임계값을 낮출수록 True의 값이 많아짐



predict() : 예측 값 반환 (0 또는 1)

Predict_proba(): 예측 확률 반환 (0.1233)



Binarizer 클래스를 이용해 분류결ㄷ계값 조절하여 정밀도와 재현율의 성능 수치 상호보완적으로 조정

임계값이 증가할수록 정밀도 값은 높아지지만 재현율 값은 낮아짐 



![output](../../../../MultiCampus_ML/threshold_value.png)

### F1 Score

정밀도와 재현율을 결합한 지표

어느 한쪽으로 치우치지 않는 수치를 나타낼 때 F1스코어가 높음 



### ROC AUC 

FPR(FALSE POSITIVE RATE) 이 변할 때 TPR (TRUE POSITIVE RATE)이 어떻게 변하는지를 나타내는 곡선 

![roc_curve](../../../../MultiCampus_ML/roc_curve.png)

