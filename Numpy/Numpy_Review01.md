Numpy_Review01 (2022-12-01)
===========================

# Numpy

- 다차원 배열 최적화
- 벡터 연산 가능 (요소 간 연산)
1. 다차원 배열 생성 방법
    1. 1차원 (vector)
    2. 2차원 (행렬)
    3. 3차원 (tensor)
2. 데이터 조회 
    1. 색인 (인덱싱)
    2. 슬라이싱
    3. 정수형 색인 (fancy색인)
    4. 불린 색인 (boolean 색인)
3. 함수 정리
4. 차원 변경 방법

### 1차원 배열

```python
'''
    1차원 배열 색인
    - 인덱싱
    - 슬라이싱

    - 정수형 색인 (fancy 색인)
    - 불린 색인 (boolean 색인)
'''
import numpy as np

arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
print(arr1D) # [9 8 7 6 5 4 3]

# 1. 인덱싱
print(arr1D[0]) # 9
print(arr1D[-1]) # 3

# 2. 슬라이싱
print(arr1D[0:4]) # [9 8 7 6]
print(arr1D[-5:-1]) # [7 6 5 4]

print("전체:", arr1D[:]) # 전체: [9 8 7 6 5 4 3]
print("전체:", arr1D[...]) # 전체: [9 8 7 6 5 4 3]

# 3. 정수형 색인 (fancy 색인)
# [9 8 7 6 5 4 3]
x = [0, 2, 4]
print(arr1D[x], arr1D[[0, 2, 4]]) # [9 7 5] [9 7 5] 원하는 인덱스의 값 가져오기 반드시 중괄호 2중으로 쓰기

# 4. 불린색인
arr1D = np.array([9, 8, 7, 6])
x = [True, False, True, False]
print(arr1D[x]) # [9 7] True인 인덱스의 값만 가져옴

# 벡터 연산
print(arr1D*2) # [18 16 14 12] 요소값 연산
print(arr1D>2) # [ True  True  True  True] 요소값 비교연산
print(arr1D % 2 == 0) # [False  True False  True]

print("짝수값만 출력하시오", arr1D[arr1D % 2 == 0]) # [8 6]
```
