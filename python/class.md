# class 기초개념 복습

## class inheritance

* 상속 : 이미 만들어진 클래스의 변수와 함수를 그대로 이어받고 새로운 내용만 추가 
  * 부모클래스 (상위클래스 / 슈퍼클래스)
  * 자식클래스 (하위클래스 / 서브클래스)
* 자식 클래스가 부모 클래스의 변수와 행위를 그대로 이용가능

```python
# 부모 클래스
class Bicycle():
  
  def __init__(self,wheel_size, colour):
    self.wheel_size = wheel_size
    self.color = color
    
  def move(self,speed):
    print('자전거: 시속 {}km로 전진'.format(speed))
    
  def turn(self,direction):
    print('자전거: {}회전'.format(direction))
   
  def stop(self):
    print('자전거({},{}): 정지'.format(self.wheel_size, self.colour))
    
my_bicycle = Bicycle()
my_bicycle.move(30)
my_bicycle.turn('우')
my_bicycle.stop()
  
```



```python
class <자식클래스이름> (부모클래스이름):
  <코드블록>
```

```python
class FoldingBicycle(Bicycle):
  def __init__ (self, wheel_size, colour, state):
    #self.__wheel_size = wheel_size
    #self.__colour = colour
    super().__init__(wheel_size,colour) # 부모클래스의 변수들
    self.__state = state # 자식클래스에서 새로 추가한 변수
  def fold(self):
    self.__state = 'folding'
    print('자전거 : 접기, state = {}'.format(self.__state))
  def unfold(self):
    self.__state = 'unfolding'
    print('자전거 : 접기, state = {}'.format(self.__state))

fb = FoldingBicycle(30,'무지개','folding')
fb.move(30)
fb.fold()
fb.unfold()
```



