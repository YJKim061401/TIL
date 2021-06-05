# Distance Formula

## 1. Euclidean Distance

![img](distance formula.assets/dis2.png)

![img](distance formula.assets/dis1.png)

```python
def euclidean_distance(pt1,pt2):
  distance = 0
  for i in range(len(pt1)):
    distance += (pt1[i]-pt2[i])**2
   return distance ** 0.5
```



## 2. Manhattan Distance

![img](distance formula.assets/dis4.png)

![img](distance formula.assets/dis6.png)

```python
def manhattan_distance(pt1,pt2):
  distance = 0
  for i in range(len(pt1)):
    distance += abs(pt1[i]-pt2[i])
   return distance
```



## 3. Hamming Distance

각 차원마다 차이를 찾는 게 아니라, '같은지'의 여부만 고려

주로, 맞춤법 검사 알고리즘에 사용

e.g. there != thete 해밍거리는 1 (각 문자가 차원이고 각 차원은 네번째 문자 'r'과 't'를 제외하고 동일한 값을 가짐)

즉, 서로 다른 글자 개수만 세주는 것



* SciPy 라이브러리 통해 거리 구하기 가능
* `from scipy.spatial import distance`
  * `distance.euclidean()`
  * `distance.cityblock()`
  * `distance.hamming()` 

===================================================



## 4. Mean Absolute Error (MAE)

![Evaluation Metrics, Continued. Exploring different methods to evaluate… |  by Shubham Dhingra | May, 2021 | Towards Data Science](distance formula.assets/1*fY-Wt0n9VhTO61ESgOAMjQ.png)

실제 값과 예측 값의 차이 (error)를 절대값으로 변환해 평균화 

에러의 크기 그대로 반영 즉, 예측 결과물의 에러가 10이 나온 것이 5로 나온 것보다 2배가 나쁜 도메인에서 쓰기 적합

이상치가 많을 때도

## 5. Mean Square Error (MSE)

![img](distance formula.assets/img.png)

실제 값과 예측 값의 차이를 제곱해 평균

에러를 제곱하여 평균을 계산하니 값은 낮을수록 좋다

이상치 많으면 수치 늘어남





## 6. Root Mean Square Error (RMSE)

![img](distance formula.assets/img-20210605211722536.png)

제곱된 에러를 다시 루트로 풀어주므로 에러를 제곱해서 생기는 값의 왜곡이 덜 함



* sklearn 라이브러리
* `from sklearn.metrics import mean_squared_error`
  * `mean_absoulte_error(y_test, y_pred)`
  * `mean_squared_error(y_test, y_pred)`
  * `np.sqrt(mean_squared_error(y_test,y_pred))`

