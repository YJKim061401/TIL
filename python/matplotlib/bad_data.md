* 단위 해석 
  * 통화 (currency)
  * 거리 etc
  * 단위를 잘못 해석해 전혀 다른 결론 내지 않기 
* NULL, NaN, undefiend etc 
* EDA

* 시각화 
  * 히스토그램 먼저 만들어 보는 것 권장 (특히 데이터 셋의 크기가 큰 경우)
  * 정규분포 확인 
* in terms of bad data in ML
  * 머신러닝 알고리즘을 위해서는 보통 많은 양의 데이터 필요 
  * 훈련 데이터의 대표성 is required 
    * 샘플이 작다면 sampliing noise 
    * 대표성이 적다면 sampling bias
  * 훈련 데이터에 관련 없는 특성이 적고 관련이 있는 특성이 충분해야 학습 진행 가능
  * feature engineering
    * feature selection : 가지고 있는 특성 중에서 훈련에 가장 유용한 특성을 선택
    * feature extraction : 특성을 결합하여 더 유용한 특성을 만듦