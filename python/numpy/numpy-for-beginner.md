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

   

   ## randoms

   1. `np.random.randint(시작,n-1)` 

      균일분포 정수 난수 1개 생성 

      ```python
      z1 = np.random.randint(0,10,10) # 0부터 9까지의 10개 난수 생성
      [output]
      [5 8 1 2 6 8 0 2 1 0]
   
   2. `np.random.rand((m,n)`
   
      0부터 1사이의 균일분포 난수 matrix array 생성
   
   3. `np.random.randn((m,n))`  
   
      정규분포 난수 matrix array 생성 
   
   4. `np.random.random((m,n))` 
   
   
   
   
   
   

## Array 합치기

### np.concatenate((a1,a2),axis = 0)

```python
arr1 = np.array([[1,2],[3,4]]) # arr1.shape (2,2)
arr2 = np.array([[5,6]])# arr2.shape(1,2)
np.concatenate((arr1,arr2),axis = 0)

[output]
array([[1, 2],
       [3, 4],
       [5, 6]])

np.concatenate((a, b.T), axis=1) # tanspose 행과 열 switch
[output]
array([[1, 2, 5],
       [3, 4, 6]])
```



* array의 shape를 보고 합칠 방향 (axis) 결정



### np.stack((a1,a2),axis = 0)

```python
arrays = [np.random.randn(3, 4) for _ in range(10)]

np.stack(arrays, axis=0).shape
(10,3,4)

np.stack(arrays, axis=1).shape
(3, 10, 4)

np.stack(arrays, axis=2).shape
(3, 4, 10)

a = np.array([1, 2, 3])
b = np.array([2, 3, 4])

np.stack((a, b))
array([[1, 2, 3],
       [2, 3, 4]])

np.stack((a, b), axis=-1)
array([[1, 2],
       [2, 3],
       [3, 4]])
```

* 배열들의 shape이 전부 동일해야함



## array 나누기

### np.split(array, indicies_or_sections, axis = 0)

```python
x = np.arange(9.0)
np.split(x, 3)
[array([0.,  1.,  2.]), array([3.,  4.,  5.]), array([6.,  7.,  8.])]
```

## array 곱하기

### np.dot(a1,a2)

* if a1 and a2 are 1-D arrays, it is inner product of vectors

  ```python
  a = np.array([1,2,3])
  b = np.array([4,5,6])
  np.dot((a,b))
  
  [output]
  32 = (4+10+18)
  
  a*b # 리스트처럼 곱해짐
  
  [output]
  array([4.10,18])
  ```

* if a1 and a2 are 2-D arrays, it is matrix multiplication 

* But using a1 @ a2 is preferred

  ```python
  a = np.array([[1,2],[3,4]])
  b = np.array([[5,6],[7,8]])
  
  np.dot(a,b) # a@b
  [output]
  array([[19, 22],
         [43, 50]])
  ```

  
  * 행렬곱셈
  * ![How to Multiply Matrices](numpy-for-beginner.assets/multiply-matrices.png)

* if a is an N-D array and b is M-D array, it is a sum product over the last axis if a and the second-to-last axis of b

* dot(a,b)[i,j,k,m] = sum(a[i,j,:]*b[k,:,m])

```python
a = np.arange(1,13).reshape(3,2,2)

b = np.arange(12,24).reshape(2,2,3)
print(a)
print(b)
np.dot(a,b)
print(np.dot(a,b).shape)

[output]
a = [[[ 1  2]
  [ 3  4]]

 [[ 5  6]
  [ 7  8]]

 [[ 9 10]
  [11 12]]]

b = [[[12 13 14]
  [15 16 17]]

 [[18 19 20]
  [21 22 23]]]

np.dot = [[[[ 42  45  48]
   [ 60  63  66]]

  [[ 96 103 110]
   [138 145 152]]]


 [[[150 161 172]
   [216 227 238]]

  [[204 219 234]
   [294 309 324]]]


 [[[258 277 296]
   [372 391 410]]

  [[312 335 358]
   [450 473 496]]]]

(3, 2, 2, 3)
```

