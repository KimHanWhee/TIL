Numpy (11/22)
====================
출처 [https://www.youtube.com/watch?v=LdoJAC26MI](https://www.youtube.com/watch?v=LdoJAC26MIc)c

# Numpy의 기본 사용법

## Numpy란?

- Numpy는 **다차원 배열**을 **효과적으로 처리**할 수 있도록 도와주는 도구
- 현실 세계의 다양한 데이터는 배열 형태로 표현 가능
- Python의 기본 List에 비해 빠르고 **강력한 기능**을 제공

## Numpy의 차원

- 1차원 축(행) : axis 0 ⇒ Vector
- 2차원 축(열) : axis 1 ⇒ Matrix
- 3차원 축(채널) : axis 2 ⇒ Tensor(3차원 이상)

## 리스트를 Numpy로 바꾸어보기

```python
import numpy as np #np = numpy 호칭

list_data = [1, 2, 3]
array = np.array(list_data)

print(array.size)   #몇개의 데이터가 들어있는지
print(array.dtype)  #타입
print(array[2])
```

## Numpy로 배열 초기화

```python
import numpy as np

#0부터 3까지의 배열 만들기
array1 = np.arange(4)
print(array1)   #[0, 1, 2, 3]

array2 = np.zeros((4, 4), dtype = float)  #4 * 4 배열을 다 0으로 채우고 타입은 float형을 지정해라
# [[0., 0., 0., 0.]
# [0., 0., 0., 0.]
# [0., 0., 0., 0.]
# [0., 0., 0., 0.]]

array3 = np.ones((3, 3), dtype=str)  #위랑동일 0이 아니라 1로 초기화
print(array3)
#[[1, 1, 1]
# [1, 1, 1]
# [1, 1, 1]]

# 0부터 99까지 랜덤하게 초기화 된 배열 만들기
array4 = np.random.randint(0, 100, (3, 3))
print(array4)
# [[91, 63, 6]
# [62, 21, 15]
# [78, 68, 35]]

# 평균이 0이고 표준편차가 1인 표준 정규를 띄는 배열
array5 = np.random.normal(0, 1, (3, 3))
print(array5)
# [[-0.85995876, -2.27512351, -1.15556506]
# [-0.5298595,   0.18397865,  0.03568352]
# [ 0.00741686, -0.54831076, -1.38529353]]
```

## Numpy로 다양한 형태 배열 합치기

```python
import numpy as np

# 다른 배열 두개 합치기
array1 = np.array([1, 2, 3]) 
array2 = np.array([4, 5, 6])
array3 = np.concatenate([array1, array2])

print(array3.shape)
print(array3)
# (6,)
# [1, 2, 3, 4, 5, 6]

# 위아래로 합치기
array1 = np.arange(4).reshape(1, 4)
array2 = np.arange(8).reshape(2, 4)
array3 = np.concatenate([array1, array2], axis=0)

print(array3.shape)
print(array3)
# (3, 4)
# [[0, 1, 2, 3]
#  [0, 1, 2, 3]
#  [4, 5, 6, 7]]

# 형태 변경
array1 = np.array([1, 2, 3, 4])
array2 = array1.reshape((2, 2))
print(array2.shape)
# (2, 2)

# 나누기
array = np.arange(8).reshape(2, 4)
left, right = np.split(array, [2], axis=1)

print(left.shape)
print(right.shape)
print(right[1][1])
# (2, 2)
# (2, 2)
# 7
```
