https://neo4j.com/use-cases/graph-data-science-artificial-intelligence/



여러 알고리즘 제공

https://neo4j.com/product/graph-data-science-library/?ref=sol-gds



> The machine learning procedures in Neo4j GDS allow you to train supervised machine learning models. Models can then be accessed via the [Model Catalog](https://neo4j.com/docs/graph-data-science/current/model-catalog/model-catalog/) and used to make predictions about your graph

https://neo4j.com/docs/graph-data-science/current/algorithms/ml-models/



Graph ML?

그래프 데이터에 기계학습을 적용하는 것 

적용가능한 기술을 발견하고 (e.g. 이미지용 ResNet or 텍스트용 BERT) 개발자 (e.g. Tensorflow, PyTorch)에 엑세스 

그러나 인기있는 ML 라이브러리는 그래프 데이터를 지원하지 않음 

마찬가지로 Neo4j와 같은 그래프 데이터 베이스는 데이터에 대해 기계학습알고리즘을 실행하는 방법을 제공하지않음 

제공이 부족한 이유? 데이터 구조의 유연성 (e.g. 모든 노드가 다른 노드와 여러 관계를 가질 수 있음)이 고정 계산 그래프, 고정 크기 텐서에 맞지 않기 때문 

또한 대부분의 그래프 ML에는 많은 양의 학습 데이터 필요 ![Screenshot 2021-08-22 at 12.32.11 AM](Neo4j_ML.assets/Screenshot 2021-08-22 at 12.32.11 AM.png)

진행과정

1. CSV파일 임포트 
2. 해당 데이터를 ML라이브러리로 수집
   1. 현재 작업에서 각 그래프를 노트, 관계 및 인접 행렬을 저장하는 특징 벡터와 함께 TFRecord로 미리 컴파일 
   2. 모든 노드 속성과 텍스트는 공통 사전을 사용하여 토큰화 
   3. 큰 그래프의 경우 그래프를 더 작은 훈련 예제로 분할하기 위한 체계가 필요 (e.g. 패치 또는 개별 노드 에지 노드 트리플에서 훈련)

===================

### GNN

* 수 많은 node와 edge로 연결된 구조인 graph로 데이터가 표현되어 있을 때 유용하게 적용될 수 있는 신경망 기술 
* graph DB는 node, edge, property를 갖는 graph의 형태로 데이터를 저장하고 쉽게 조회할 수 있도록 해줌

* GNN 응용분야
  * recommender system
    * 추천 시스템
  * combinatorial optimization
  * computer vision
  * Physics / chemistry
    * 분자나 세포 등 기본 단위들간의 연관 관계로부터 새로운 현상을 분석
  * drug discovery
    * 구성 성분 및 그들의 연관 관계로부터 신약 구조를 예측하거나 새로운 현상을 분석 
  * knolwdge graph 