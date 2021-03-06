# 군집화

### 비지도 학습

* 결과값이 없이 입력값만 주고 학습을 시켜서 유사성을 파악하게 하는 방식 (정답 없음)
* 데이터의 숨겨진 특징이나 구조를 발견하는 데 사용
* 정답이 없는 입력 데이터만 이용하기 때문에 입력값 자체의 특성과 분포만을 파악해서 그룹핑하는 군집화에 주로 사용



### 비지도 학습의 유형

* 비지도 변환
* 군집 (clustering)



### 비지도 변환

* 데이터를 새롭게 표현하여 사람이나 다른 머신러닝 알고리즘이 원래 데이터보다 쉽게 해석할 수 있도록 만드는 알고리즘 
* 차원축소
  * 많은 고차원 데이터를 특성의 수를 줄이면서 꼭 필요한 특징을 포함한 데이터로 표현하는 방법
  * 수백 개 이상의 피처로 구성된 데이터 셋의 경우
  * 피처 수가 상대적으로 적은 차원에서 학습한 모델보다 예측 신뢰도가 떨어지고 피처 간의 상관관계가 높아질 가능성이 커짐
  * 선형 회귀와 같은 선형 모델에서는 입력한 변수들 간의 상관관계가 높을 수록 다중공선상 문제가 발생 
  * 모델의 예측 성능이 떨어질 수 있음
* 비지도 변환으로 데이터를 구성하는 단위나 성분을 검색 : 많은 텍스트 문서에서 주제 추출



### 군집

* 데이터를 비슷한 것끼리 그룹으로 묶는 작업
* 사용되는 알고리즘 
  * K-평균
  * DBSCAN



### 군집화

* 데이터 포인트들을 별개의 군집으로 그룹화하는 것
* 유사성이 높은 데이터들을 동일한 그룹으로 분류하고
* 서로 다른 군집들이 상이성을 가지도록 그룹화 



### K-평균 알고리즘

* 군집화에서 가장 일반적으로 사용되는 알고리즘 

* 군집 중심점 (centroid)라는 특정한 임의 지점을 선택해서 해당 중심에 가까운 포인트들을 선택하는 군집화 기법

* * 장점

    ​     쉽고 간결한 알고리즘

    ​     대용량 데이터에도 활용 가능

    ​     일반적인 군집화에서 가장 많이 활용

    

    단점

    ​     속성의 개수가 많을 경우, 정확도 떨어짐 (PCA로 차원감소 필요)

    ​     반복 횟수가 많을 경우 느린 수행 시간

    ​     이상치 데이터에 취약 

    ​     몇 개의 군집을 선택해야 할지 가이드 어려움 



### 평균 이동 (mean shift)

* k-평균과 유사

* **거리** 중심이 아니라 데이터가 모여 있는 **밀도**가 가장 높은쪽으로 군집 중심점을 이동하면서 군집화 수행

* 일반 업무 기반의 정형 데이터 셋 보다는 컴퓨터 비전 영역에서 이미지나 영상 데이터에서 특정 개체를 구분하거나 움직임을 추적하는데 뛰어남

* k-평균과 유사하게 중심을 군집의 중심으로 지속적으로 움직이면서 군집화 수행

* 데이터의 분포도를 이용해 군집 중심점을 찾고

* 중심을 데이터가 모여있는 밀도가 가장 높은 곳으로 이동시킴 

* k-평균 : 중심에 소속된 데이터의 평균 거리 중심으로 이동 



### GMM

* 군집화를 적용하고자 하는 데이터가 여러 개의 가우시안 분포 (정규분포)를 가진 데이터 집합들이 섞여서 생성된 것이라는 가정하에 군집화 수행

* 전체 데이터 셋에서 서로 다른 정규 분포 형태를 추출해서 다른 정규 분포를 가진 데이터 셋을 각각 군집화 하는 것

* 장점 : k-평균보다 유연하게 다양한 데이터 셋에 잘 적용 가능

* 단점 : 군집화를 위한 수행 시간이 오래 걸림

* K-평균과 비교했을 때

  ​    \- k-평균 : 원형 범위에서 군집화 수행

  ​    - 데이터 셋이 원형의 범위를 가질수록 군집화 효율을 높아짐



### DBSCAN

* 데이터 밀도기반 군집화의 대표적인 알고리즘

* 특정 공간 내에 데이터 밀도 차이를 기반 알고리즘으로 하고 있어서 데이터의 분포가 기하학적으로 복잡한 데이터 셋에서도 효과적인 군집화 가능