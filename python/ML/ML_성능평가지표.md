# ML 성능 평가지표

### 정확도

문제점 : 데이터 구성에 따라 모델 성능 왜곡 가능성

* 이진분류에서 불균형한 데이터 세트 

정확도만으로만 모델 성능을 평가하지 않음



### 오차행렬

머신러닝 모델의 예측이 얼마나 잘 한 예측인지를 판단하는 기준

<img src="ML_성능평가지표.assets/Structure-of-the-confusion-matrix-with-TP-FN-FP-and-TN-values.png" alt="Structure of the confusion matrix with TP, FN, FP and TN values. | Download  Scientific Diagram" style="zoom:33%;" />

정확도 = 예측 결과와 실제 값이 동일한 건수 / 전체 데이터 수 

**(TN+TP) / (TN+FP+FN+TP)**

문제점 : negative로 예측 정확도 높아지는 경향 발생 (TN커지고 TP 작아짐)



### 정밀도 & 재현율

positive예측 성능에 더 초점을 맞춤

**정밀도 = TP/(FP + TP)**

**재현율 = TP / (FN + TP)**

정밀도 & 재현율 모두 높은 수치를 얻는 것이 바람직함 

임계값을 조절하여 정밀도와 재현율의 성능 수치를 상호 보완적으로 조정

**분류결정임계값** : positive 예측값을 결정하는 확률의 기준

임계값을 낮출수록 True의 값이 많아짐

### F1 Score

### ROC AUC 