# 분류

* 지도학습의 대표적 유형 
* 기존 데이터가 어떤 레이블에 속한지 알고리즘을 통해 패턴을 이지하고 새롭게 관측된 데이터에 대한 레이블 판별

1. 결정트리
2. 나이브 베이즈
3. 서포트 벡터 머신
4. 로지스틱 회귀
5. 최소근접알고리즘
6. 앙상블



### 1. 결정트리

* 질문이나 네모상자 : Node
* 맨 위의 노드 : Root Node
* 마지막 노드 : Leaf Node
* 규칙 노드 : Decision Node
  * 규칙 노드에 따라 sub tree 생성 
* 유의점 :
  * 데이터 세트의 피처가 결합해 규칙조건을 만들 때 마다 규칙노드가 만들어지는데
  * 규칙이 많아 --> 결정 방식 복잡 --> 과적합 발생 
  * 트리를 어떻게 분할할 것인가가 중요 (최대한 균일한 데이터 세트를 구성할 수 있도록 분할)
  * 가지치기 이용 
* 장점 : 
  * 매우 쉽고 유연하게 적용될 수 있는 알고리즘
  * 데이터 스케일링이나 정규화 등의 사전 가공 영향 적음
* 단점 :
  * 많은 규칙 -> 복잡한 결정 방식 -> 과적합
  * 예측 성능 저하 
* 균일도 측정하는 대표적인 방법
  1. 정보이득
     1. 엔트로피 이용 `1 - 엔트로피 지수`
        1. 엔트로피 0이면 모든 값 동일, 1이면 불순도 최대 
  2. 지니 계수
     1. 불순도를 수치화한 지표 
     2. 0이 가장 평등 / 1이 불평등 
     3. 머신러닝의 경우, 지니 계수가 낮을수록 데이터 균일도가 높은 것으로 해석 



### (사이킷런) 결정트리 알고리즘에서는 *지니계수*를 이용하여 데이터 세트 분할 

1. 정보이득높거나 지니 계수 낮은 조건 찾고
2. 자식 트리 노드에 걸처 반복적으로 분할
3. 모든 데이터 특정 분류에 속하면
4. 분할을 멈추고 분류 결정



### 결정 트리 알고리즘 시각화

`pip install graphviz`

`conda install graphviz`

콘다 에러나면 일단 최신으로 업데이트 해보기

`conda update --all`



```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.tree import export_graphviz
import graphviz

# 의사결정트리 클래스 생성
dt_clf = DecisionTreeClassifier(random_state=156)

# 붓꽃 데이터 분리
iris_data = load_iris()
X_train, X_test, y_train, y_test = train_test_split(iris_data.data, iris_data.target, test_size=0.2, random_state=11)

# 학습
dt_clf.fit(X_train, y_train)

# export_graphviz()의 호출 결과로 out_file로 지정된 tree.dot 생성
export_graphviz(dt_clf, out_file="tree.dot", class_names=iris_data.target_names,
                feature_names=iris_data.feature_names, impurity=True, filled=True)

# 위에 생성된 tree.dot파일을 Graphviz가 읽어서 시각화
with open("tree.dot") as f:
    dot_graph = f.read()
        
graphviz.Source(dot_graph)
```



<img src="Untitled.assets/decistion-tree.png" alt="decistion-tree" style="zoom: 25%;" />



`export_graphviz(dt_clf, out_file="파일명", class_names=결정클래스명칭,
feature_names=피쳐이름, impurity=True (각 노드에 불순도 표시,지니계수), filled=True(노드 색상 표시))`

* samples =120개 : 전체 데이터가 120개
* value = [41, 40, 39] : Setosa 41개, Versicolor 40개, Virginica 39개로 구성 
* sample120개가 value=[41,40,39]의 분포도로 되어 있으므로 지니계수는 0.667 (불순도)
  * 결정트리는 **불순도를 최소화** 하는 것이 목표 
* class=setosa는 하위 노드를 가질 경우에 setosa의 개수가 41개로 제일 많다는 의미
* 색이 짙을수록 지니계수가 낮음
* 지니계수(불순도)가 0이 될때까지 계속 분류 



<img src="Untitled.assets/Screenshot 2021-07-27 at 11.07.55 AM.png" alt="Screenshot 2021-07-27 at 11.07.55 AM" style="zoom:50%;" />

#### 결정트리의 하이퍼 파라미터 튜닝

`max_depth` : 결정 트리의 최대 트리 깊이를 제어

e.g. max_depth = 3로 설정하면 더 간단한 결정 트리가 된다

`min_samples_split`: 자식 규칙 노드를 분할해 만들기 위한 최소한의 샘플 데이터 개수

e.g. min_samples_split=4로 설정하면 최소 샘플 개수가 4개 필요. 3개만 있는 경우에는 더 이상 자식 규칙 노드를 위한 분할을 하지 않음

분할할 샘플 개수가 최소 4개는 되어야지 분할 시작 

`min_samples_leaf` : 리프 노드가 될 수 있는 최소 샘플 개수

e.g. min_samples_leaf=4로 설정하면 리프노드가 될 수 있는 최소 sample개수가 4개 

#### 하이퍼 파라미터 튜닝을 통해 브랜치 노드를 줄이고 결정트리를 더 간결하게 만들어서 과적합 발생 방지

### Feature_importance_ 속성

트리를 만드는 결정에 각 피처가 얼마나 중요한지 평가

ndarray로 반환

0과1사이 값

[첫번째 피처 중요도, 두번째 피처 중요도,..]

중요도 값이 클수록 그 노드에서 불순도가 크게 감소 

<img src="Untitled.assets/Screenshot 2021-07-27 at 1.10.09 PM.png" alt="Screenshot 2021-07-27 at 1.10.09 PM" style="zoom:25%;" />

### overfitting

* make_classification() 사용해 과적합 시각화

<img src="Untitled.assets/Screenshot 2021-07-27 at 1.10.39 PM.png" alt="Screenshot 2021-07-27 at 1.10.39 PM" style="zoom:50%;" />

* 분류가 제대로 안되어 있음 (파란색과 빨간색 막 섞여있음)
* `min_samples_leaf` 이용해 노드 분류 규칙 완화하여 복잡도 줄이기

```python
from sklearn.datasets import make_classification
import matplotlib.pyplot as plt
%matplotlib inline

plt.title("3 Class values with 2 Features Sample data creation")

# 2차원 시각화를 위해서 feature는 2개, 결정값 클래스는 3가지 유형의 classification 샘플 데이터 생성. 
X_features, y_labels = make_classification(n_features=2, n_redundant=0, n_informative=2,
                             n_classes=3, n_clusters_per_class=1,random_state=0)

# plot 형태로 2개의 feature로 2차원 좌표 시각화, 각 클래스값은 다른 색깔로 표시됨.
plt.scatter(X_features[:, 0], X_features[:, 1], marker='o', c=y_labels, s=25, cmap='rainbow', edgecolor='k')


```

<img src="Untitled.assets/그림26-결정트리 과적합.JPG" alt="그림26-결정트리 과적합" style="zoom:50%;" />

Min_samples_leaf로 트리생성조건을 제약한 모델이 성능이 더 뛰어남

이유 : 테스트 데이터 세트는 학습 데이터 세트와 다른 데이터 세트인데, 학습 데이터에만 지나치게 최적화된 분류 기준은 오히려 테스트 데이터 세트에서 정확도를 떨어트릴 수 있음



