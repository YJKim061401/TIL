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

