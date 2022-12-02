Numpy_Review01 (2022-12-01)
===========================

# Numpy

- 다차원 배열 최적화
- 벡터 연산 가능 (요소 간 연산)
1. 다차원 배열 생성 방법
    - **스칼라**
    - **1차원 (vector) =** 스칼라의 모임
    - **2차원 (행렬) =** 벡터의 모임
    - **3차원 (tensor) =** 행렬의 모임
2. 데이터 조회 
    - **색인 (인덱싱)**
    - **슬라이싱**
    - **정수형 색인 (fancy색인)**
    - **불린 색인 (boolean 색인)**
        - **논리연산자**
            - **and, or, not 사용불가**
            - **&, |, ~ 으로 사용**

# 1차원 배열

### ******************************************1차원 배열 생성******************************************

- *`np.array(리스트)`*를 활용하여 ndarray 타입의 배열 생성

```python
arr = [1, 2, 3]
print(arr, type(arr)) # [1, 2, 3] <class 'list'>

arr1D = np.array(arr)
print(arr1D, type(arr1D)) # [1 2 3] <class 'numpy.ndarray'>

# 속성
print(arr1D.shape) # (3,)
print(arr1D.dtype) # int32
print(arr1D.ndim) # 1

arr = [1, 2, 3.]
arr1D = np.array(arr)
print(arr1D)
```

### **1차원 배열 색인**

- **인덱싱**
    
    ```python
    '''
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    # 1. 인덱싱
    print(arr1D[0]) # 9
    print(arr1D[-1]) # 3
    ```
    
- **슬라이싱**
    - [:], […] : 배열 전체 내용 가져오기
    - [n:m] : n부터 m 전까지 요소 가져오기
    
    ```python
    '''
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    # 2. 슬라이싱
    print(arr1D[0:4]) # [9 8 7 6]
    print(arr1D[-5:-1]) # [7 6 5 4]
    
    print("전체:", arr1D[:]) # 전체: [9 8 7 6 5 4 3]
    print("전체:", arr1D[...]) # 전체: [9 8 7 6 5 4 3]
    ```
    
- **정수형 색인 (fancy 색인)**
    
    ```python
    '''
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    # 3. 정수형 색인 (fancy 색인)
    # [9 8 7 6 5 4 3]
    x = [0, 2, 4]
    # **원하는 인덱스의 값 가져오기 반드시 중괄호 2중으로 쓰기**
    print(arr1D[x], arr1D[[0, 2, 4]]) # [9 7 5] [9 7 5] 
    ```
    

- **불린 색인 (boolean 색인)**
    
    ```python
    '''
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    # 1. 인덱싱
    print(arr1D[0]) # 9
    print(arr1D[-1]) # 3
    
    # 4. 불린색인
    arr1D = np.array([9, 8, 7, 6])
    x = [True, False, True, False]
    print(arr1D[x]) # [9 7] True인 인덱스의 값만 가져옴
    ```
    
- **벡터 연산**
    - 배열의 요소값을 하나씩 연산 할 수 있다.
    
    ```python
    # 벡터 연산
    print(arr1D*2) # [18 16 14 12] 요소값 연산
    print(arr1D>2) # [ True  True  True  True] 요소값 비교연산
    print(arr1D % 2 == 0) # [False  True False  True]
    
    print("짝수값만 출력하시오")
    print(arr1D[arr1D % 2 == 0]) # [8 6]
    print("8보다 큰 값만 출력하시오")
    print(arr1D[arr1D > 8])
    ```
    
- **짝수이면서 6보다 큰 값 출력**
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    
    # 짝수이면서 6보다 큰 값 출력
    print(arr1D[(arr1D % 2 == 0) & (arr1D > 6)]) # 8
    ```
    

### 배열 색인을 이용해서 값 변경

- **인덱싱을 이용한 값 변경**
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    # 1. 인덱싱 이용한 값 변경
    arr1D[0] = 900
    print(arr1D) # [900   8   7   6   5   4   3]
    ```
    
- **슬라이싱을 이용한 값 변경**
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    #2. 슬라이싱을 이용한 값 변경
    arr1D[1:4] = 800     # 1~3인덱스 값을 800으로 변경
    print(arr1D) # [900 800 800 800   5   4   3]
    ```
    
- **정수형 색인 (fancy)을 이용한 값 변경**
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    # 3. 정수형색인(fancy) 이용한 값 변경
    arr1D[[1, 3]] = 700  # 1번째 인덱스와 3번째인덱스를 700으로 변경
    print(arr1D) # [900 700 800 700   5   4   3]
    ```
    
- **불린색인을 이용한 값 변경**
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    print(arr1D) # [9 8 7 6 5 4 3]
    
    # 4. 불린색인 이용한 값 변경 ==> 800보다 같거나 큰 값은 -1로 변경
    arr1D[arr1D >= 800] = -1  # []안에 조건이 True인 경우들을 -1로 변경
    print(arr1D) # [ -1 700  -1 700   5   4   3]
    ```
    

### 1차원 배열 추가 및 삽입

- ******추가******
    - `**arr1D = np.append(arr, values, axis = None)**`
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    arr1D = np.append(arr1D, 10) # arrId에 10을 추가한 값 리턴
    arr1D = np.append(arr1D, [1, 2, 3])
    print(arr1D)
    ```
    
- **********삽입**********
    - `**arr1D = np.insert(arr, obj, value, axis = None)**`
    
    <aside>
    💡 **삭제나 삽입 시 슬라이싱을 쓰기위해서 np.s_를 사용해야한다
    
    ex)** arr1D= np.insert(arr1D, np.s_[0:2], 50)
    
    </aside>
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    arr1D = np.insert(arr1D, 0, 100) # arr1D의 0번째 인데스에 100 삽입
    arr1D = np.insert(arr1D, 0, [-1, -2])
    
    # fancy
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    arr1D = np.insert(arr1D, [0, 1, 2], [99, 88, 77])
    print(arr1D)
    ```
    

### 1차원 배열 삭제

- **삭제**
    - arr1D = np.delete(arr, obj, axis = None)
    
    <aside>
    💡 **삭제나 삽입 시 슬라이싱을 쓰기위해서 np.s_를 사용해야한다
    
    ex)** arr1D= np.delete(arr1D, np.s_[0:2])
    
    </aside>
    
    ```python
    import numpy as np
    
    arr1D = np.array([9, 8, 7, 6, 5, 4, 3])
    
    arr1D = np.delete(arr1D, 0)
    print(arr1D) # [8 7 6 5 4 3]
    arr1D = np.delete(arr1D, [1, 2])
    print(arr1D) # [8 5 4 3]
    
    arr1D= np.delete(arr1D, np.s_[0:2]) # 삭제나 삽입 시 슬라이싱을 쓰기위해서 np.s_를 사용해야한다
    print(arr1D)
    ```
    

### 얕은 복사 깊은 복사

- **************파이썬**************
    - [:], copy(), list()는 깊은 복사로 처리됨 ==> 복사본으로 생성
    - 중첩된 리스트는 얕은복사로 처리됨
    
    ```python
    # 1. 파이썬
    arr = [1, 2, [3, 4, 5]]
    arr2 = arr[:]
    print(id(arr), id(arr2)) # 2576801210304 2576802081728 깊은복사를 했기 때문에 주소값이 다르게 나온다
    
    arr[0] = -1
    arr[2][0] = 100
    print(arr, arr2) # [1, 2, [100, 4, 5]] [1, 2, [100, 4, 5]] 중첩 리스트는 깊은 복사를 해도 얕은 복사가 되어 값이 같이 변한다
    ```
    
- **********Numpy**********
    - [:]로 복사하면 주소값은 다르지만 내부적으로 연결이 되어있음.(뷰) 따라서 하나의 ndarray를 수정하면 다른 ndarray 영향을 미친다. (성능이슈 때문)
        
        ```python
        import numpy as np
        
        # 2. numpy
        arr2D = np.array([[1, 2, 3], [4, 5, 6]])
        print(arr2D)
        copy_arr2D = arr2D[:]
        print(id(arr2D), id(copy_arr2D)) # 2099801101872 2099801102064 numpy에선 주소만 다를 뿐 둘이 연결되어있다
        
        arr2D[0] = 100
        print(arr2D, copy_arr2D) # [[100 100 100] [  4   5   6]] 둘 다 값 바뀜
        ```
        
    - 깊은 복사 하는 방법
        - np.copy(값)
        - 값.copy
        
        ```python
        import numpy as np
        
        # 3. numpy - 깊은 복사 처리
        arr2D = np.array([[1, 2, 3], [4, 5, 6]])
        c_arr2D = np.copy(arr2D)
        c_arr2D2 = arr2D.copy()
        
        arr2D[0] = 100
        print(arr2D, c_arr2D, c_arr2D2) # 이 경우 깊은 복사가 되어 서로에게 값 변환 영향이 없다
        ```
        

### 타입변환

- ********************dtype 속성이용******************** (********************np.array(값, dtype=))**
    
    ```python
    import numpy as np
    
    arr1D = np.array([1, 2, 3])
    print(arr1D, arr1D.dtype)
    
    arr1D = np.array([1, 2, 3.])
    print(arr1D, arr1D.dtype)
    
    # int32 --> float32
    arr1D = np.array([1, 2, 3], dtype=np.float32)
    print(arr1D, arr1D.dtype) # [1. 2. 3.] float32
    
    # float --> int
    arr1D = np.array([10.4, 23.45, 3.13], dtype=np.int32)
    print(arr1D, arr1D.dtype)
    
    # int --> str(유니코드)
    arr1D = np.array([1, 2, 3], dtype=np.str_) # np.str을 쓰면 dprecate warning이 뜨면서 np.str_로 바꾸라고 조언함
    print(arr1D, arr1D.dtype)
    
    # int --> bytes
    arr1D = np.array([1, 2, 3], dtype=np.string_)
    print(arr1D, arr1D.dtype)
    ```
    
- ********************************************************************************astype함수를 이용한 형 변환********************************************************************************
    
    ```python
    import numpy as np
    
    # int32 --> float32
    arr1D = np.array([1, 2, 3])
    arr1D = arr1D.astype(np.float32)
    print(arr1D, arr1D.dtype)
    
    # float --> int
    arr1D = np.array([1, 2, 3])
    arr1D = arr1D.astype(np.int32)
    print(arr1D, arr1D.dtype)
    
    # int --> str(유니코드)
    arr1D = np.array([1, 2, 3])
    arr1D = arr1D.astype(np.str_)
    print(arr1D, arr1D.dtype)
    
    # int --> bytes
    # arr1D = np.array([1, 2, 3])
    arr1D = np.array([1, 2, 3]).astype(np.bytes_) # 이렇게 체인 형식으로 쓸 수도 있다
    print(arr1D, arr1D.dtype)
    ```
    

### 벡터연산 브로드캐스팅

- **벡터연산 (vectorized operation)**
    - 기존 파이썬에서 지원안된 요소간의 연산을 지원한다
    - 자동으로 브로드캐스팅이 적용된다
    
    ```python
    import numpy as np
    
    # 1. 파이썬
    arr = [1, 2, 3]
    arr2 = [10, 20, 30, 40, 50]
    print(arr + arr2) # [1, 2, 3, 10, 20, 30] 요소들끼리 값이 더해지지 않고 concat이 되버린다
    print(arr * 2) # [1, 2, 3, 1, 2, 3] 이것도 마찬가지로 arr이 두번 출력 될 뿐이다
    
    # 2. numpy
    arr1D_1 = np.array([1, 2, 3])
    arr1D_2 = np.array([10, 20, 30])
    print(arr1D_1 + arr1D_2) # [11 22 33] 요소끼리 연산되기 때문에 배열의 shape이 반드시 일치해야 한다. 다르면 에러 발생
    print(arr1D_1 - arr1D_2) # [ -9 -18 -27]
    print(arr1D_1 // arr1D_2) # [0 0 0]
    print(arr1D_1 * arr1D_2) # [10 40 90]
    ```
    
- **브로드캐스팅 (broadcasting)**
    - 새로 다른 차원을 이용해서 연산 시 연산이 가능하도록 내부적으로 차원을 맞춰준다.
        
        <aside>
        💡  밑에의 경우 내부적으로 스칼라를 벡터로 바꿔 [10, 10, 10]형태로 바꾼다.
        
        ```python
        print(arr1D_1 + 10) # [11 12 13]
        ```
        
        </aside>
        
        ```python
        # 벡터 + 스칼라 ==> 브로드캐스팅 적용
        print(arr1D_1 + 10) # [11 12 13] 이 경우 내부적으로 스칼라를 벡터로 바꿔 [10, 10, 10]형태로 바꾸는데, 이를 브로드캐스팅이라 한다.
        
        # 비교연산
        arr1D = np.arange(10)
        print(arr1D) # [0 1 2 3 4 5 6 7 8 9]
        print(arr1D > 5) # [False False False False False False  True  True  True  True]
        print(arr1D % 2 == 0) # [ True False  True False  True False  True False  True False]
        ```
        

# 2차원 배열

### 2차원 배열 생성

- **************************************************np.array(중첩리스트)**************************************************
- **np.array(리스트) 를 만든 후 shape 변경**
    - `arr1D.shape = (행, 열)`
    - `np.reshape(arr1D, newshape = (행, 열)`
    - `arr2D = np.arange(**12**).reshape(**3, 4**)`
    
    ```python
    import numpy as np
    
    # 1. np.array(중첩리스트)
    arr2D = np.array([[1, 2, 3],[4, 5, 6]])
    print(arr2D, arr2D.shape)
    
    # 2. np.array(리스트) 후 shape 변경
    # 가. shape 속성
    arr1D = np.arange(12) # 0~11
    print(arr1D) # [ 0  1  2  3  4  5  6  7  8  9 10 11]
    arr1D.shape = (3, 4) # 값 4개 짜리 배열이 3개
    arr1D.shape = (4, 3)
    arr1D.shape = (2, 6)
    arr1D.shape = (6, 2)
    arr1D.shape = (12, 1)
    arr1D.shape = (1, 12)
    arr1D.shape = (4, -1) # 4행 고정 열은 시스템이 설정
    arr1D.shape = (-1, 2) # 2열고정 행은 시스템이 설정
    print(arr1D)
    
    ```
    
    - arr1D.shape = (4, -1) => 4행 고정 열은 시스템이 계산
        - -1이면 컴퓨터가 스스로 계산 하여 정함, 만약 4행으로 못 만들 경우 에러
    - np.reshape(arr1D, (-1, 3) 3열 고정 행은 시스템이 계산
    
    ```python
    # 나. np.reshape(arr, shape)
    arr1D = np.arange(12)
    print(arr1D)
    
    arr2D = np.reshape(arr1D, newshape=(3, 4))
    arr2D = np.reshape(arr1D, newshape=(-1, 4)) # 열은 고정 행은 시스템이 설정
    print(arr2D)
    ```
    

### 2차원 배열 색인

**기본적으로 arr[행, 열] 형식을 따른다**

- **인덱싱**
    
    ```python
    import numpy as np
    
    arr2D = np.arange(12).reshape(3, 4)
    print(arr2D)
    
    # 1. 인덱싱
    print("1행 반환", arr2D[0]) # 1행 반환 [0 1 2 3]
    print("마지막행 반환", arr2D[-1]) # 마지막행 반환 [ 8  9 10 11] 행이 몇개인지 알기 힘들경우에 -1로 구한다
    print("1행 1열 반환", arr2D[0, 0]) # 1행 1열 반환 0  (몇번째 줄, 몇번째 번호)
    print("1행 마지막열 반환", arr2D[0,-1]) # 1행 마지막열 반환 3
    ```
    
- **슬라이싱**
    
    ```
    import numpy as np
    
    arr2D = np.arange(12).reshape(3,4)
    print(arr2D)
    
    print("모든 행의 1열 반환", arr2D[:, 0]) # 1열 반환 [0 4 8] ':'를 써서 모든행을 가리킨다
    print("모든 행의 2열 이후 반환", arr2D[:, 1:])
    '''
    [[ 1  2  3]
     [ 5  6  7]
     [ 9 10 11]]
     '''
    
    ```
    
- **정수형 색인 (fancy)**
    
    ```
    import numpy as np
    
    arr2D = np.arange(12).reshape(3,4)
    print(arr2D)
    
    print("1행과 3행만 반환", arr2D[[0, 2]])
    # [[ 0  1  2  3]
    #  [ 8  9 10 11]]
    
    print("1행과 3행에서 2열만 반환", arr2D[[0,2],1]) # 1행과 3행에서 2열만 반환 [1 9]
    print("1행과 3행에서 2열 이후 반환", arr2D[[0,2],1:])
    # [[ 1  2  3]
    #  [ 9 10 11]]
    
    ```
    
- **불린 색인 (boolean)**
    - **flatten**
        - 원하는 숫자를 뽑을 때 원본인 2차원 모양이 고장나는데, 이를 1차원으로 자동으로 바꿔준다 이를 flatten이라고 부른다.
    
    ```
    import numpy as np
    
    arr2D = np.arange(12).reshape(3,4)
    print(arr2D)
    
    # 4. boolean 색인 ==> flatten
    print("짝수만 출력", arr2D[arr2D % 2 == 0])
    ```
    

### 2차원배열 추가 및 삽입, 삭제

- **추가**
    
    `**arr1D = np.append(arr, values, axis=None)**`
    
    - axis = None 이면 flatten변경 후 마지막에 추가
    
    ```python
    arr = np.append(arr2D, [10, 9, 8])
    print(arr) # [ 1  2  3  4  5  6 10  9  8] ==> flatten됨
    ```
    
    - axis = 0이면 행추가
    
    ```python
    # 2 axis = 0 이면 이면 행으로 추가
    arr2D = np.array([[1, 2, 3], [4, 5, 6]])
    arr = np.append(arr2D, [[10, 9, 8]], axis=0)
    print(arr)
    # [[ 1  2  3]
    #  [ 4  5  6]
    #  [10  9  8]]
    ```
    
    - axis = 1이면 열추가
    
    ```python
    # 2 axis = 1이면 열로 추가
    arr2D = np.array([[1, 2, 3], [4, 5, 6]])
    arr = np.append(arr2D, [[10], [9]], axis=1)
    print(arr)
    # [[ 1  2  3 10]
    #  [ 4  5  6  9]]
    ```
    
- **삽입**
    
    `**arr1D = np.insert(arr, values, axis = None**`
    
    - axis=None 이면 flatten 변경 후에 삽입
        
        ```python
        arr2D = np.array([[1, 2, 3], [4, 5, 6]])
        print(arr2D)
        
        arr = np.insert(arr2D,0,[10, 9, 8]) # => [10  9  8  1  2  3  4  5  6]
        arr = np.insert(arr2D,0,[10])
        print(arr) # [10  1  2  3  4  5  6]
        ```
        
    - axis = 0 이면 행 삽입
        
        ```python
        arr2D = np.array([[1, 2, 3], [4, 5, 6]])
        print(arr2D)
        
        arr = np.insert(arr2D, 0, [10, 9, 8], axis=0) # 0번째 행에 10, 9, 8 삽입
        arr = np.insert(arr2D, 0, [100, 900, 800], axis=0)
        print(arr)
        # [[100 900 800]
        #  [  1   2   3]
        #  [  4   5   6]]
        
        arr = np.insert(arr2D, 0, 10, axis=0)
        print(arr)
        # [[10 10 10]
        # [ 1  2  3]
        # [ 4  5  6]]
        ```
        
    - axis = 1 이면 열 삽입
        
        ```python
        arr2D = np.array([[1, 2, 3], [4, 5, 6]])
        print(arr2D)
        
        arr = np.insert(arr2D, 0, [[10], [9]], axis=1)
        print(arr)
        # [[10  9  1  2  3]
        # [10  9  4  5  6]]
        
        arr = np.insert(arr2D, 0, 10, axis=1)
        print(arr)
        # [[10  1  2  3]
        # [10  4  5  6]]
        
        arr = np.insert(arr2D, 0, [10, 9], axis=1)
        print(arr)
        # [[10  1  2  3]
        # [ 9  4  5  6]]
        ```
        
- **삭제**
    
    `**arr1D = np.delete(arr, obj, axis=None)**`
    
    ```python
    arr2D = np.arange(25).reshape(5, 5)
    print(arr2D)
    '''
    [[ 0  1  2  3  4]
     [ 5  6  7  8  9]
     [10 11 12 13 14]
     [15 16 17 18 19]
     [20 21 22 23 24]]
    '''
    ```
    
    - axis=None이면 flatten된 후 삭제(기본값) ⇒ 대부분은 axis = 0이 기본값이다
        
        ```python
        # 1. axis = None 이면 flatten 적용 후 삭제
        arr = np.delete(arr2D, -1) # 마지막 값 삭제
        arr = np.delete(0, -1) # fancy 색인 0부터 마지막까지 전부 삭제
        arr = np.delete(arr2D, np.s_[:8]) # 슬라이싱 0부터 8번째 전까지만 삭제
        print(arr)
        ```
        
    - axis = 0, 행 삭제
        
        ```python
        arr = np.delete(arr2D, -1, axis=0) # 마지막 행 삭제
        arr = np.delete(arr2D, [0,-1], axis=0) # 첫번째, 마지막행 삭제
        arr = np.delete(arr2D, np.s_[:3], axis=0) # 처음부터 2번째 행 삭제
        ```
        
    - axis = 1, 열 삭제
        
        ```python
        arr = np.delete(arr2D, -1, axis=1) # 마지막 열 삭제
        arr = np.delete(arr2D, [0,-1], axis=1) # 처음, 마지막 열 삭제
        arr = np.delete(arr2D, np.s_[:3], axis=1) # 처음부터 2번째 열 삭제
        ```
        

# 다차원배열

**차원구별**

- ndim 속성 ⇒ 차원의 수 리턴 해줌
- 대괄호의 개수
    - [ ⇒ 1차원
    - [[ ⇒ 2차원
    - [[[ ⇒ 3차원

**모양**

- shape(행, 열)

**************축(axis)**************

- axis = None ⇒ flatten
- axis = 0 ⇒ 행
- axis = 1 ⇒ 열

### ****************************************다차원배열 병합****************************************

- 병합할 배열 생성
    
    ```python
    import numpy as np
    
    arr1 = np.arange(9).reshape(3, 3)
    print(arr1)
    # [[0 1 2]
    #  [3 4 5]
    #  [6 7 8]]
    
    arr2 = arr1 * 10
    print(arr2)
    # [[ 0 10 20]
    #  [30 40 50]
    #  [60 70 80]]
    ```
    
- **열병합**
    - **`np.hstack()`**
        - hstack은 파라미터가 **튜플** 형태로 들어가야한다
    - **************`np.column_stack()`**************
        - # column_stack은 파라미터가**튜플** 형태로 들어가야한다
    - **********`np.concatenate( , axis=1)`**
        - concatenate는 **집합형(리스트, 튜플, 셋, …)**으로만 들어가면 된다 (axis기본 값은 0이다.)
    
    ```python
    arr = np.hstack((arr1, arr2))
    arr = np.column_stack((arr1, arr2))
    arr = np.concatenate((arr1, arr2), axis=1) # 
    print(arr)
    # 결과 동일
    # [[ 0  1  2  0 10 20]
    #  [ 3  4  5 30 40 50]
    #  [ 6  7  8 60 70 80]]
    ```
    
- **행병합**
    - **`np.vstack()`**
        - vstack은 파라미터가 **튜플** 형태로 들어가야한다
    - `**np.row_stack()**`
        - row_stack은 파라미터가 **튜플** 형태로 들어가야한다
    - `**np.concatenate(, axis=0)**`
        - concatenate는 **집합형(리스트, 튜플, 셋, …)**으로만 들어가면 된다. (axis기본 값은 0이다.)
    
    ```python
    arr = np.vstack((arr1, arr2)) 
    arr = np.row_stack((arr1, arr2)) 
    arr = np.concatenate((arr1, arr2), axis=0)
    print(arr)
    # 결과 동일
    # [[ 0  1  2]
    #  [ 3  4  5]
    #  [ 6  7  8]
    #  [ 0 10 20]
    #  [30 40 50]
    #  [60 70 80]]
    ```
    

### 다차원배열 분할

- 분할 할 배열 생성
    
    ```python
    import numpy as np
    
    arr1 = np.arange(16).reshape(4, -1)
    print(arr1)
    # [[ 0  1  2  3]
    #  [ 4  5  6  7]
    #  [ 8  9 10 11]
    #  [12 13 14 15]]
    ```
    
- **********열분할**********
    - `**np.hsplit(arr, 등분 수(몇개로 나눌지))**`
    - `**np.split(arr, 등분 수, axis=1)**`
    
    ```python
    arr = np.hsplit(arr1, 4)
    print(arr)
    # **출력**
    # [array([[ 0,  1],
    #        [ 4,  5],
    #        [ 8,  9],
    #        [12, 13]]), array([[ 2,  3],
    #        [ 6,  7],
    #        [10, 11],
    #        [14, 15]])]
    
    a1, a2 = np.hsplit(arr1, 2) # **나눈 배열을 변수 두개에 각각 하나씩 저장할 수 있다**
    print(a1, a2)
    a1, a2 = np.split(arr1, 2, axis=1)
    print(a1, a2)
    # **출력**
    # [[ 0  1]
    #  [ 4  5]
    #  [ 8  9]
    #  [12 13]] [[ 2  3]
    #  [ 6  7]
    #  [10 11]
    #  [14 15]]
    ```
    
- **행분할**
    - `**np.vsplit(arr, 나눌 개수)**`
    - `**np.split(arr, 나눌 개수 axis=0)**`
    
    ```python
    a1, a2 = np.vsplit(arr1, 2)
    print(a1, a2)
    a1, a2 = np.split(arr1, 2, axis=0) # **나눈 배열을 변수에 각각 저장 가능**
    print(a1, a2)
    
    # [[0 1 2 3]
    #  [4 5 6 7]] [[ 8  9 10 11]
    #  [12 13 14 15]]
    ```
    

# 차원 변경

## 차원 증가

- `**arr.reshape(행,열)**`
    - 배열의 shape를 다시 정의해서 모양을 바꿈
- `**np.reshape(arr, (행,열))**`
    - 배열의 shape를 다시 정의해서 모양을 바꿈
- `**np.expand_dims(arr, axis=0/1)**`
    - 지정한 axis에 차원을 추가한다
        - axis=0일 경우: (3,)배열을 (1, 3) 배열로 바꿈
        
        ```python
        import numpy as np
        
        arr = np.array([10, 20, 30])
        print(arr, arr.shape) # [10 20 30] (3,)
        
        arr2D = np.expand_dims(arr, axis=0)
        print(arr2D, arr2D.shape) # [[10 20 30]] (1, 3)
        ```
        
        - axis = 1일 경우: (3,) 배열을 (3, 1) 배열로 바꿈
        
        ```python
        import numpy as np
        
        arr = np.array([10, 20, 30])
        print(arr, arr.shape) # [10 20 30] (3,)
        
        arr2D = np.expand_dims(arr, axis=1)
        print(arr2D, arr2D.shape) # [[10 20 30]] (3, 1)
        ```
        

<aside>
💡 **axis에 주어지는 수를 shape의 인덱스 번호라고 생각하면 쉬운거 같다..**

위 코드를 예시로 들어보자, axis = 0이면 shape(n, m)의 0번째 인덱스 값인 n에 차원이 추가된 것이다.. 반대로 axis = 1이면 shape(n, m)의 1번째 인덱스 값인 m에 차원이 추가된다.. (나중에 봤을 때 알아들을 수 있겠지..?)

</aside>

- *** 권장 `arr[np.newaxis, ...]`**
    - **강사님 강추 코드다!! 해당 배열의 전체(…)에(”:” 도 사용가능) newaxis로 차원이 하나 추가되는 것**

### 1차원 ⇒ 2차원

- 1차원 배열 생성
    
    ```python
    import numpy as np
    
    arr = np.array([10, 20, 30])
    print(arr, arr.shape) # [10 20 30] (3,) => 1차원
    ```
    
- 2차원으로 증가 시키기
    
    ```python
    arr2D = arr.reshape(1, -1)
    arr2D = np.reshape(arr, (1, -1))
    arr2D = np.expand_dims(arr, axis=0)
    arr2D = arr[np.newaxis, ...]
    # arr2D = arr[np.newaxis, :]
    print(arr2D, arr2D.shape) # [[10 20 30]] (1, 3)
    ```
    

### 2차원 ⇒ 3차원

- 2차원 코드 생성
    
    ```python
    import numpy as np
    # 2차원 ==> 3차원
    arr2D = np.arange(9).reshape(3, 3)
    print(arr2D)
    # [[0 1 2]
    #  [3 4 5]
    #  [6 7 8]]
    ```
    
- 3차원으로 증가 시키기
    
    ```python
    arr3D = arr2D.reshape(1, 3, 3) # 3차원이라 3개 지정
    arr3D = np.reshape(arr2D, (1, 3, 3))
    arr3D = np.expand_dims(arr2D, axis=0)
    arr3D = arr2D[np.newaxis, ...]
    print(arr3D)
    # [[[0 1 2]
    #   [3 4 5]
    #   [6 7 8]]]
    ```
    

## 차원 축소

- **`np.squeeze(arr, axis)`**
    - shape에서 값이 1인 것들을 삭제하는 함수이다. 예)*`(3, 1, 3) => (3, 3), (4, 2, 1) => (4, 2)`*
    - axis를 지정해주면 지정한 axis에서 1인 것을 삭제한다 (1이 아닌 axis를 지정하면 오류가 나는 거 같다)

### 2차원 → 1차원

- 2차원 배열 생성
    
    ```python
    import numpy as np
    
    # 모양이 (1, 3)인 배열
    arr2D = np.arange(3).reshape(1, 3)
    print(arr2D, arr2D.shape) 
    # [[0 1 2]] (1, 3)
    
    # 모양이 (3, 1)인 배열
    arr2D = np.arange(3).reshape(3, 1)
    print(arr2D, arr2D.shape)
    # [[0] [1] [2]] (3, 1)
    ```
    
- 1차원으로 축소
    
    ```python
    
    # 모양이 (1, 3)인 배열 축소 (1, 3)에서 axis=0 인 1삭제 
    arr1D = np.squeeze(arr2D, axis=0)
    arr1D = np.squeeze(arr2D) # axis를 안쓰면 1이 다지워짐(현재 코드는 안써도 무관)
    print(arr1D, arr1D.shape)
    # [0 1 2] (3,)
    
    # 모양이 (3, 1)인 배열 축소 (3, 1)에서 axis=1 인 1삭제 
    arr1D = np.squeeze(arr2D, axis=1)
    arr1D = np.squeeze(arr2D)
    print(arr1D, arr1D.shape)
    # [0 1 2] (3,)
    ```
    

### 3차원 → 2차원

```python
# (1, 4, 4) ==> (4, 4)
arr3D = np.arange(16).reshape(1, 4, 4)
arr2D = np.squeeze(arr3D, axis=0) # (1, 4, 4)에서 axis=0인 1 삭제
print(arr2D, arr2D.shape)

# (4, 1, 4) ==> (4, 4)
arr3D = np.arange(16).reshape(4, 1, 4)
arr2D = np.squeeze(arr3D, axis=1) # (4, 1, 4)에서 axis=1인 1 삭제
print(arr2D, arr2D.shape)

# (4, 4, 1) ==> (4, 4)
arr3D = np.arange(16).reshape(4, 4, 1)
arr2D = np.squeeze(arr3D, axis=2) # (4, 4, 1)에서 axis=2인 1 삭제
print(arr2D, arr2D.shape)

# 출력 값 동일
#[[ 0  1  2  3]
# [ 4  5  6  7]
# [ 8  9 10 11]
# [12 13 14 15]] (4, 4)
```

### 다차원 → 1차원

- flatten 혹은 ravel을 써서 1차원으로 바꿀 수 있다
    
    ```python
    arr3D = np.arange(16).reshape(1, 4, 4)
    print("flatten:", arr3D.flatten()) # flatten: [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15]
    # print("flatten:", arr3D.ravel()) # flatten: [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15]
    ```
    
    <aside>
    💡 **ravel vs flatten**
    ravel은 원본 값과 view로 연결됨(얕은 복사), flatten은 깊은 복사
    
    </aside>
    
- **flatten vs ravel 예시**
    
    ```python
    arr2D = np.arange(9).reshape(3, 3) # => 1~9까지 3행 3열 배열
    
    xxx = arr2D.flatten() # => flatten로 1차원으로 만든 값 xxx에 저장
    yyy = arr2D.ravel() # => ravel로 1차원으로 만든 값 yyy에 저장
    print("값 변경 전")
    print(arr2D, xxx, yyy)
    # 원본: [[0 1 2]
    #       [3 4 5]
    #       [6 7 8]] xxx : [0 1 2 3 4 5 6 7 8] yyy : [0 1 2 3 4 5 6 7 8]
    
    arr2D[0][0] = 100
    print("값 변경후")
    print(arr2D, xxx, yyy) 
    # flatten은 깊은복사, ravel은 얕은복사가 되서 원본 값 변경시 ravel값도 같이 변한다.
    # 원본: [[100 1 2]
    #          [3 4 5]
    #          [6 7 8]] xxx : [0 1 2 3 4 5 6 7 8] yyy : [0 1 2 3 4 5 6 7 8]
    ```
    

# 축 변경

- `**transpose()**`
- **`T`**
    - 축 변경 할 배열 생성
        
        ```python
        import numpy as np
        
        # 2차원 축 변경(행 -> 열)
        arr2D = np.array([[1, 2, 3],[4, 5, 6]])
        print(arr2D, arr2D.shape)
        # [[1 2 3]
        #  [4 5 6]] (2, 3)
        ```
        
    - 축 변경
        
        ```python
        # **매우 간단하다**
        print(arr2D.T)
        print(arr2D.transpose())
        # [[1 4]
        #  [2 5]
        #  [3 6]]
        ```
        
    
    ### 3차원 축 변경
    
    - `**transepose()**`
        - 3차원 배열에서는 축 지정이 가능하다.
        - 축 지정을 안 할 시에는 첫번째와 마지막을 바꾼다
        ex) (1, 6, 4) ⇒ (4, 6, 1)
    
    ```python
    arr3D = np.arange(24).reshape(2, 3, 4)
    print(arr3D.shape) # (2, 3, 4)
    
    xxx = arr3D.transpose()
    print(xxx.shape) # (4, 3, 2) 축 미지정 시 맨앞과 맨뒤를 바꿈
    
    # 축지정이 가능. 원본기준으로 원본에 1인 3이 제일 앞으로, 
    # 그다음 2인 4 0인 2가 마지막으로 온다
    xxx = arr3D.transpose((1,2,0))
    print(xxx.shape) # (3, 4, 2)
    ```
    
    <aside>
    💡 위 코드도 transepose안에 숫자들을 shape의 인덱스 번호라고 생각하면 간단하다.
    
    </aside>
    

## 이 외

### 범용함수 (**Universal function, ufunc)**

- 벡터 연산으로 처리하는 함수들이다.

<aside>
💡 함수 중에서 `**함수.(배열)**` 형식으로 사용이 됐을 때, 배열 안에 있는 값을 하나씩 꺼내서 함수를 적용시키는 함수를 나타낸다고 한다.

</aside>
