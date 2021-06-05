# numpy for beginner

## array 

### 1. arange 

numpy에서 원하는 숫자 범위를 모두 포함하는 배열을 만드는 함수

* `np.arange(31)`  # 0부터 30까지의 배열
* `np.arange(0,5,0.5)` #floating point 0.5 step
* `np.arange(30).reshape(5,6)` # array만들고 5 by 6 reshape

### 2. zeros

0으로 가득 찬 array 생성

* `np.zeros((2,5))` # 2 by 5 zero matrix 

### 3. ones 

1로 가득 찬 array 생성

* `np.ones((2,5))` # 2 by 5 one matrix

### 4. empty

empty는 초기화되지 않은 값으로 배열 생성

* `np.empty((3,5))` 

### 5.  _like

_like는 지정된 array의 shape 크기만큼 지정된 값으로 array를 채워 반환

* `test = np.arange(30).reshape(5,6)`
* `np.ones_like(test)` or `np.zeros_like(test)` 

1. import the bumpy package under the name **np** 

   `import numpy as np` 

2. create a **null**  vector of size 10

   `z = np.zeros(10)` 

   

   ## random

   1. `np.random.randint(시작,n-1)` 

      균일분포 정수 난수 1개 생성 

   2. `np.random.rand((m,n)`

      0부터 1사이의 균일분포 난수 matrix array 생성

   3. `np.random.randn((m,n))`  

      정규분포 난수 matrix array 생성 

   4. `np.random.random((m,n))` 

   

   

   

