PlayData_Pandas01 (2022/12/05)
================================

# Pandas

DB의 table과 유사(행렬구조)

1. Pandas 생성방법
2. 조회
3. 컬럼 / 행추가 및 삭제
4. 함수
    1. DataFrame
    2. Series
5. 조인, merge
6. 그룹핑

### **Table**

- 행 ⇒ 레코드
- 열 ⇒ 컬럼
- **CRUD**(**C**reate, **R**ead, **U**pdate, **D**elete) 작업
    - **SQL**(**S**tructured, **Q**uery, **L**anguage) 언어 사용
- 테이블을 여러개로 나눠서 효율적으로 관리 가능
    - **Join**
        - 나눈 테이블에서 필요한 정보를 가져오는 것

### Data Frame

컬럼이 최소 2개 이상이어야 함. ⇒ 컬럼이 하나인 것은 **시리즈(Series)**라고 부른다.

- 컬럼 레이블(컬럼명)
- 행 인덱스(행명)
    - 기본적으로 0, 1, 2,…순서
- 위치값
    - 수정 불가
    - 행, 렬 모두 0, 1, 2…순서
    - 우리 눈에는 보이지 않음

<aside>
💡 레이블 또는 위치값을 이용해서 값 조회가 가능함.

</aside>

### DataFrame 생성

- **dict를 이용하여 DataFrame 생성**
    
    *`df = pd.DataFrame({key:값, key:값})`* ****⇒ key가 컬럼으로 저장됨.
    
    ```python
    import pandas as pd
    import numpy as np
    
    df = pd.DataFrame({"c1":[4, 5, 6],
                       "c2":[7, 8, 9],
                       "c3":[14, 25, 36]})
    print(df)
    
    # 출력
    #    c1  c2  c3 => 컬럼 레이블
    # 0   4   7  14
    # 1   5   8  25
    # 2   6   9  36
    # ⇑
    # 행 레이블(인덱스)
    ```
    
- **원하는 컬럼 순서 변경**
    
    *`df = pd.DataFrame({key:값, key:값}, columns = [컴럼명, ...)`*
    
    ```python
    df = pd.DataFrame({"c1":[4, 5, 6],
                       "c2":[7, 8, 9],
                       "c3":[14, 25, 36]}, columns=["c2", "c3", "c1"]) # <= 컬럼순서 지정
    print(df)
    # 출력
    #    c2  c3  c1
    # 0   7  14   4
    # 1   8  25   5
    # 2   9  36   6
    ```
    

### DataFrame 정보 얻기

- **컬럼 정보 얻기**
    - *`df.columns`⇒* **속성**
    - *`df.keys()` ⇒* **함수**
    
    ```python
    import pandas as pd
    import numpy as np
    
    df = pd.DataFrame({"c1":[4, 5, 6],
                       "c2":[7, 8, 9],
                       "c3":[14, 25, 36]})
    
    # 1. 컬럼 정보
    print(df.columns) # Index(['c1', 'c2', 'c3'], dtype='object')
    print(df.keys()) # Index(['c1', 'c2', 'c3'], dtype='object')
    ```
    
- **인덱스(행라벨) 정보 얻기**
    - *`df.index`*
    
    ```python
    # 2. 인덱스 정보(행라벨 정보)
    print(df.index) # RangeIndex(start=0, stop=3, step=1)
    ```
    
- **내용(데이터 정보)**
    - *`df.values`*
    - *`df.to_numpy()` ⇒* **권장**
    
    ```python
    # 3. 내용(데이터 정보)
    print(df.values)
    print(df.to_numpy())
    # [[ 4  7 14]
    #  [ 5  8 25]
    #  [ 6  9 36]]
    ```
    

### DataFrame 컬럼 및 인덱스 변경

- **********************컬럼 변경**********************
    - *`df.columns = [컬럼명, ...]`*
    
    ```python
    import pandas as pd
    import numpy as np
    
    df = pd.DataFrame({"c1":[4, 5, 6],
                       "c2":[7, 8, 9],
                       "c3":[14, 25, 36]})
    
    # 1. 원본
    print(df)
    #    c1  c2  c3
    # 0   4   7  14
    # 1   5   8  25
    # 2   6   9  36
    
    # 2. 컬럼명 변경
    df.columns = ["col1", "col2", "col3"] # 변경할 이름 지정 개수 맞춰야됨
    print(df)
    #    col1  col2  col3
    # 0     4     7    14
    # 1     5     8    25
    # 2     6     9    36
    ```
    
- ****************************인덱스 변경****************************
    - DataFrame 생성 후 변경
        - *`df.columns = [컬럼명, ...]`*
        
        ```python
        # 3. 인덱스 (행 레이블) 변경 ==> 기본은 0 1 2 ... 지정됨.
        df.index=[10, 20, 30]
        # df.index=["A", "B", "C"]
        print(df)
        #     col1  col2  col3
        # 10     4     7    14
        # 20     5     8    25
        # 30     6     9    36
        ```
        
    - DateFrame 생성하면서 변경
        - *`df = pd.DataFrame({key:값, key:값}, columns = [인덱스명, ...)`*
        
        ```python
        # 3. 인덱스 (행 레이블) 변경
        df = pd.DataFrame({"c1":[4, 5, 6],
                           "c2":[7, 8, 9],
                           "c3":[14, 25, 36]},
                          index=["A1", "B1", "C1"]) # 문자로도 변경 가능
        print(df)
        #     c1  c2  c3
        # A1   4   7  14
        # B1   5   8  25
        # C1   6   9  36
        ```
        

### 중첩

- **dict 중첩**
    - dict 중첩 시 밖에 있는 key값이 컬럼, 안에 있는 key값이 인덱스
        
        ```python
        df = pd.DataFrame({"key1":{"key1_1":[4, 5, 6], "key2_1":[14, 15, 16], "key3_1":[24, 25, 26]},
                           "key2":{"key1_1":[34, 35, 36], "key2_1":[44, 45, 46], "key3_1":[54, 55, 56]},
                           "key3":{"key1_1":[64, 65, 66], "key2_1":[74, 75, 76], "key3_1":[84, 85, 86]}
                           })
        print(df, type(df))
        #              key1          key2          key3  중첩 시 밖에 있는 key값이 컬럼, 안에있는 key값이 인덱스
        # key1_1  [4, 5, 6]           NaN           NaN
        # key2_1        NaN  [14, 15, 16]           NaN
        # key3_1        NaN           NaN  [24, 25, 26] <class 'pandas.core.frame.DataFrame'>
        ```
        
- ************************리스트 중첩************************
    - *`df = pd.DataFrame(중첩리스트)`* **⇒ 컬럼레이블과 행레이블이 자동으로 0 1 2 형식으로 지정**
    
    ```python
    import pandas as pd
    import numpy as np
    
    df = pd.DataFrame([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
    arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]) # ndarray로도 가능
    df = pd.DataFrame(arr)
    print(df, type(df))
    #    0  1  2
    # 0  1  2  3
    # 1  4  5  6
    # 2  7  8  9 <class 'pandas.core.frame.DataFrame'>
    ```
    
    - **컬럼명 지정**
        - *`df = pd.DataFrame(중첩리스트, columns=[컬럼명, ...])`*
        
        ```python
        df = pd.DataFrame([[1, 2, 3], [4, 5, 6], [7, 8, 9]], columns=["c1", "c2", "c3"])
        print(df, type(df))
        #    c1  c2  c3
        # 0   1   2   3
        # 1   4   5   6
        # 2   7   8   9 <class 'pandas.core.frame.DataFrame'>
        ```
        
    - **인덱스명 지정**
        - *`df = pd.DataFrame(중첩리스트, columns=[컬럼명, ...], index=[인덱스명,...])`*
        
        ```python
        df = pd.DataFrame([[1, 2, 3], [4, 5, 6], [7, 8, 9]], columns=["c1", "c2", "c3"], index=['A', 'B', 'C'])
        print(df)
        #    c1  c2  c3
        # A   1   2   3
        # B   4   5   6
        # C   7   8   9
        ```
        

### 시리즈(Series)

- ****************시리즈(Series) 생성****************
    - *`s1 = pd.Series([값,...], name="Series명)`*
    
    ```python
    s1 = pd.Series([1, 2, 3], name="sname") # name 속성을 추가할 수 있다
    s2 = pd.Series([11, 12, 13])
    s3 = pd.Series([21, 22, 23])
    print(s1, type(s1))
    # 0    1
    # 1    2
    # 2    3
    # Name: sname, dtype: int64 <class 'pandas.core.series.Series'>
    ```
    
    - **시리즈 DataFrame으로 합치기**
        - *`df = pd.DataFrame([s1, s2,...]`*
        
        ```python
        df = pd.DataFrame([s1, s2, s3])
        print(df)
        #             0   1   2
        # sname       1   2   3  # name을 지정하면 name이 인덱스로 들어간다
        # Unnamed 0  11  12  13  # name 미지정 시 unnamed가 뜨고 인덱스는 0, 1, 2 형태
        # Unnamed 1  21  22  23
        ```
        
    - ********************************인덱스값, 컬럼값 변경********************************
    
    ```python
    df = pd.DataFrame([s1, s2, s3], index=["A", "B", "C"])
    df.columns=["c1", "c2", "c3"]
    print(df)
    #    c1  c2  c3
    # A   1   2   3
    # B  11  12  13
    # C  21  22  23
    ```
    
    - ********************행렬 서로 바꾸기********************
        - `transpose()`
        
        ```python
        # transpose()
        print(df.T) # 행렬 바꾸기
        #     A   B   C
        # c1  1  11  21
        # c2  2  12  22
        # c3  3  13  23
        ```
        
    - ****************시리즈 DataFrame으로 바꾸기****************
        
        ```python
        # Series --> DataFrame
        s2 = pd.Series([11, 12, 13])
        df2 = s2.to_frame("age")
        print(s2, type(s2))
        # 0    11
        # 1    12
        # 2    13
        # dtype: int64 <class 'pandas.core.series.Series'>
        
        print(df2, type(df2))
        #    age
        # 0   11
        # 1   12
        # 2   13 <class 'pandas.core.frame.DataFrame'>
        ```
        

### 인덱스 관리

`기본값은 0 1 2 …`

기본 코드

```python
import numpy as np
import pandas as pd

df = pd.DataFrame({"date":['2022', '2023'],
                   "name":["홍길동", "이순신"],
                   "age":[20, 30]})
print(df)
#    date name  age
# 0  2022  홍길동   20
# 1  2023  이순신   30
```

- **새로운 값으로 index 설정**
    - *`df.index = [값, ...]`*
    
    ```python
    # 1. 새로운 값으로 index 설정
    df.index = ["사람1", "사람2"]
    print(df)
    #      date name  age
    # 사람1  2022  홍길동   20
    # 사람2  2023  이순신   30
    ```
    
- **기존 컬럼값으로 index 설정**
    - *`df.set_index("컬럼명")`*
    - *`def set_index(`)*
        - self
        - keys ⇒ 필수 파라미터
        - drop : bool = True ⇒ 기존 컬럼값 **삭제**하고 인덱스로 지정
        - append: bool = False ⇒ 기존 인덱스에 **새로운** 인덱스 추가
        - inplace: bool = False ⇒ 인덱스 지정된 **복사본**으로 저장
    - `*df.reset_index()`* ⇒ 인덱스를 컬럼으로 변경
    
    ```python
    # 2. 기존 컬럼값으로 index 설정
    new_df = df.set_index("date", inplace=False, drop=True, append=False) # 파라미터 중 inplace = False, True면 원본 변경, False면 원본 유지
    #      name  age
    # date
    # 2022  홍길동   20
    # 2023  이순신   30
    
    new_df = df.set_index("date", inplace=False, drop=False, append=False) # 파라미터 중 inplace = False, True면 원본 변경, False면 원본 유지
    #       date name  age
    # date
    # 2022  2022  홍길동   20
    # 2023  2023  이순신   30
    
    new_df = df.set_index("date", inplace=False, drop=False, append=True) # append = True => 기존 인덱스에 지정된 새로운 인덱스 추가
    #           date name  age
    #     date
    # 사람1 2022  2022  홍길동   20
    # 사람2 2023  2023  이순신   30
    
    print(df)
    #      date name  age
    # 사람1  2022  홍길동   20
    # 사람2  2023  이순신   30
    
    df.set_index("date", inplace=True)
    print(df)
    #      name  age
    # date
    # 2022  홍길동   20
    # 2023  이순신   30
    
    print(new_df)
    ```
    
- **명시적으로 지정된 인덱스를 재배치 (순서변경)**
    - *`df.reindex(존재하는 인덱스, 존재하는 인덱스, ...)`*
    
    ```python
    # 3. 명시적으로 지정된 인덱스를 재배치(순서 변경)
    list_value = np.arange(15).reshape(5, 3)
    print(list_value)
    # [[ 0  1  2]
    #  [ 3  4  5]
    #  [ 6  7  8]
    #  [ 9 10 11]
    #  [12 13 14]]
    
    df = pd.DataFrame(list_value, index = list('DCEAB'))
    df.columns = ['c1', 'c2', 'c3']
    print(df)
    #    c1  c2  c3
    # D   0   1   2
    # C   3   4   5
    # E   6   7   8
    # A   9  10  11
    # B  12  13  14
    
    # df.reindex(["A","B","C","D","E"]) # 변경 안됨 => inplace 지원여부를 확인해야함
    new_df = df.reindex(["A","B","C","D","E"]) # => new_df에 변경된 복사본을 저장
    print(new_df)
    #    c1  c2  c3
    # A   9  10  11
    # B  12  13  14
    # C   3   4   5
    # D   0   1   2
    # E   6   7   8
    ```
    
- **DataFrame 연결 시 인덱스 제외하고 연결**
    - `pd.concat(df, df2)`
    
    <aside>
    💡 그냥 연결 시 인덱스가 중복이 되므로 **ignore_index를 True**로 바꿔주자
    
    </aside>
    
    ```python
    # 4. DataFrame 연결 시 인덱스 제외하고 연결
    df = pd.DataFrame({"date":['2022', '2023'],
                       "name":["홍길동", "이순신"],
                       "age":[20, 30]})
    df2 = pd.DataFrame({"date":['2024', '2025'],
                       "name":["홍길동1", "이순신1"],
                       "age":[20, 30]})
    
    new_df = pd.concat([df, df2]) # ignore_index란 파라미터가 False임
    print(new_df) # 인덱스 중복
    #    date  name  age
    # 0  2022   홍길동   20
    # 1  2023   이순신   30
    # 0  2024  홍길동1   20
    # 1  2025  이순신1   30
    
    new_df = pd.concat([df, df2], ignore_index=True) # ignore index란 파라미터가 False임
    print(new_df) # 인덱스 중복 안됨
    # 0  2022   홍길동   20
    # 1  2023   이순신   30
    # 2  2024  홍길동1   20
    # 3  2025  이순신1   30
    ```
    

- **projection (열 선택)**
    - 내가 원하는 컬럼 선택
- **selection (행 선택)**
    - 내가 원하는 행 선
- **join (merge 함수)**
    - 여러 DataFrame 연결

### 조회

- **컬럼 조회 (Projection)**
    - *`**df.컬럼명`* ⇒ Series 반환**
        
        ```python
        import numpy as np
        import pandas as pd
        
        df = pd.DataFrame({"c1":[4, 5, 6],
                           "c2":[14, 15, 16],
                           "c3":[24, 25, 26]})
        
        print(df.c1, type(df.c1))
        # 0    4
        # 1    5
        # 2    6
        # Name: c1, dtype: int64 <class 'pandas.core.series.Series'> => Series 타입
        ```
        
    - *`**df['컬럼명']`* ⇒ Series 반환**
        
        ```python
        print(df['c3'], type(df['c3']))
        # 0    24
        # 1    25
        # 2    26
        # Name: c3, dtype: int64 <class 'pandas.core.series.Series'>
        ```
        
    - *`**df[['컬럼명', '컬럼명', ...]]`* ⇒ DataFrame 반환**
        
        ```python
        print(df[['c3', 'c1']], type(df[['c3', 'c1']]))
        #    c3  c1
        # 0  24   4
        # 1  25   5
        # 2  26   6 <class 'pandas.core.frame.DataFrame'>
        
        # 동일 컬럼 여러번 지정 가능하다
        print(df[['c3', 'c1', 'c1', 'c1']])
        #    c3  c1  c1  c1
        # 0  24   4   4   4
        # 1  25   5   5   5
        # 2  26   6   6   6
        ```
        
- **********************행 조회 (Selection********************************************)**********************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"c1":[4, 5, 6, 7, 8],
                       "c2":[14, 15, 16, 17, 18],
                       "c3":[24, 25, 26, 27, 28]},
                       index=list("ABCDE"))
    print(df)
    #    c1  c2  c3
    # A   4  14  24
    # B   5  15  25
    # C   6  16  26
    # D   7  17  27
    # E   8  18  28
    ```
    
    - **행 라벨 이용**
        - *`**df.loc[행 라벨]`* ⇒ 인덱싱 색인**
            
            ```python
            print(df.loc['B'], type(df.loc['B']))
            # c1     5
            # c2    15
            # c3    25
            # Name: B, dtype: int64 <class 'pandas.core.series.Series'>
            ```
            
        - *`**df.loc[행 라벨, 행 라벨, ...]`* ⇒ fancy 색인**
            
            ```python
            print(df.loc[['B','C']], type(df.loc[['B','C']]))
            #    c1  c2  c3
            # B   5  15  25
            # C   6  16  26 <class 'pandas.core.frame.DataFrame'>
            ```
            
        - *`**df.loc[행 라벨1 : 행 라벨2]`*  ⇒ 슬라이싱 색인, 행 라벨 2를 포함함.**
            
            ```python
            print(df.loc['B':'E'], type(df.loc['B':'E'])) # 슬라이싱 색인
            # B   5  15  25
            # C   6  16  26
            # D   7  17  27
            # E   8  18  28 <class 'pandas.core.frame.DataFrame'>
            ```
            
        - *`**df.loc[[True, ...]]`* ⇒ 불린 색인**
            
            ```python
            print(df.loc[[True, False, False, False, False]]) # 불린 색인
            #    c1  c2  c3
            # A   4  14  24
            ```
            
    - **행 위치 이용**
        - *`**df.iloc[행 위치]`* ⇒ 인덱싱 색인**
            
            ```python
            print(df.iloc[0])
            # c1     4
            # c2    14
            # c3    24
            # Name: A, dtype: int64
            
            print(df.iloc[-1])
            # c1     8
            # c2    18
            # c3    28
            # Name: E, dtype: int64
            ```
            
        - *`**df.iloc[[행 위치, 행 위치, ...]]`*  ⇒ fancy 색인**
            
            ```python
            print(df.iloc[[0,2,-1]])
            #    c1  c2  c3
            # A   4  14  24
            # C   6  16  26
            # E   8  18  28
            ```
            
        - *`**df.iloc[start:stop]`*  ⇒ 슬라이싱 색인, stop 전 까지**
            
            ```python
            print(df.iloc[1:4])
            # B   5  15  25
            # C   6  16  26
            # D   7  17  27
            #    c1  c2  c3
            
            print(df.iloc[::2])
            # A   4  14  24
            # C   6  16  26
            # E   8  18  28
            ```
            
        - *`**df.iloc[[True, ...]]`* ⇒ 불린 색인**
            
            ```python
            print(df.iloc[[True, False, False, False, False]])
            #    c1  c2  c3
            # A   4  14  24
            ```
            
- **행, 컬럼 조회**
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"c1":[4, 5, 6, 7, 8],
                       "c2":[14, 15, 16, 17, 18],
                       "c3":[24, 25, 26, 27, 28]},
                       index=list("ABCDE"))
    print(df)
    #    c1  c2  c3
    # A   4  14  24
    # B   5  15  25
    # C   6  16  26
    # D   7  17  27
    # E   8  18  28
    ```
    
    - ******************************레이블 조회******************************
        - 기본 문법은 *********************************`**df.loc[행 라벨, 컬럼 라벨]**`*********************************
        - 행 라벨 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
        - 컬럼 라벨 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
        
        ```python
        print("1. A행 c1컬럼")
        print(df.loc['A', 'c1']) # 4
        
        print("1. A행, B행 c1 컬럼")
        print(df.loc[['A','B'], 'c1'])
        # A    4
        # B    5
        # Name: c1, dtype: int64
        
        print("q. A행, C행 c1, c3 컬럼")
        print(df.loc[['A', 'C'], ['c1','c3']])
        #    c1  c3
        # A   4  24
        # C   6  26
        
        print("1. B~D행 c1, c3 컬럼")
        print(df.loc['B':'D', ['c1', 'c3']])
        #    c1  c3
        # B   5  25
        # C   6  26
        # D   7  27
        
        print("1. B~D행 c1~c3 컬럼")
        print(df.loc['B':'D', 'c1':'c3'])
        #    c1  c2  c3
        # B   5  15  25
        # C   6  16  26
        # D   7  17  27
        
        print("1. A, C, E헹 c1, c3컬럼 - 불린색인")
        print(df.loc[[True,False,True,False,True], [True,False,True]])
        #    c1  c3
        # A   4  24
        # C   6  26
        # E   8  28
        ```
        
    - ******************위치 조회******************
        - 기본문법은 *`**df.iloc[행 위치, 컬럼 위치]**`*
        - 행 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
        - 컬럼 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
        
        ```python
        print("1. A행 c1컬럼")
        print(df.iloc[0, 0]) # 4
        
        print("1. A행, B행 c1 컬럼")
        print(df.iloc[[0,1], 0])
        # A    4
        # B    5
        # Name: c1, dtype: int64
        
        print("q. A행, C행 c1, c3 컬럼")
        print(df.iloc[[0, 2], [0,2]])
        #    c1  c3
        # A   4  24
        # C   6  26
        
        print("1. B~D행 c1, c3 컬럼")
        print(df.iloc[1:4, [0, 2]])
        #    c1  c3
        # B   5  25
        # C   6  26
        # D   7  27
        
        print("1. B~D행 c1~c3 컬럼")
        print(df.iloc[1:4, 0:3])
        #    c1  c2  c3
        # B   5  15  25
        # C   6  16  26
        # D   7  17  27
        
        print("1. A, C, E헹 c1, c3컬럼 - 불린색인")
        print(df.iloc[[True,False,True,False,True], [True,False,True]])
        #    c1  c3
        # A   4  24
        # C   6  26
        # E   8  28
        ```
        
- ****************값 변경****************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"c1":[4, 5, 6, 7, 8],
                       "c2":[14, 15, 16, 17, 18],
                       "c3":[24, 25, 26, 27, 28]},
                       index=list("ABCDE"))
    print(df)
    #    c1  c2  c3
    # A   4  14  24
    # B   5  15  25
    # C   6  16  26
    # D   7  17  27
    # E   8  18  28
    ```
    
    - **************************************************************레이블 조회 후 값 변경**************************************************************
        - *`**df.loc[행 라벨, 컬럼 라벨] = 값**`*
        - 행 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
        - 컬럼 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
    - **위치 조회**
        - *`**df.iloc[행 위치, 컬럼 위치] = 값**`*
        - 행 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
        - 컬럼 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
    
    ```python
    print("1. A행 값을 모두 100으로 변경")
    df.loc['A'] = 100 # 인덱싱
    print(df)
    #     c1   c2   c3
    # A  100  100  100
    # B    5   15   25
    # C    6   16   26
    # D    7   17   27
    # E    8   18   28
    
    print("1. B,C 행값을 모두 200으로 변경")
    df.loc[['B', 'C']] = 200 # fancy
    print(df)
    #     c1   c2   c3
    # A  100  100  100
    # B  200  200  200
    # C  200  200  200
    # D    7   17   27
    # E    8   18   28
    
    print("1. B,D 행 c2, c3 컬럼 값을 모두 300으로 변경")
    df.loc[['B', 'D'], ['c2', 'c3']] = 300 # fancy
    print(df)
    #     c1   c2   c3
    # A  100  100  100
    # B  200  300  300
    # C  200  200  200
    # D    7  300  300
    # E    8   18   28
    
    print("1. B~D행 c1~c2 컬럼값 400으로 변경")
    # df.loc['B':'D', 'c1':'c2'] = 400
    df.iloc[1:4, 0:1] = 400 # 슬라이싱
    print(df)
    #     c1   c2   c3
    # A  100  100  100
    # B  400  300  300
    # C  400  200  200
    # D  400  300  300
    # E    8   18   28
    ```
    
- ************filter************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"c1":[4, 5, 6, 7, 8],
                       "c2":[14, 15, 16, 17, 18],
                       "c3":[24, 25, 26, 27, 28],
                       "d1":[24, 25, 27,45, 65]},
                       index=["mouse", "rabbit", "habit", "mount", "hunt"])
    print(df)
    #    c1  c2  c3
    # A   4  14  24
    # B   5  15  25
    # C   6  16  26
    # D   7  17  27
    # E   8  18  28
    ```
    
    - *`**df.filter()**`*
        - *`axis: Any = None`* ⇒ 0:행, 1: 열
        - **컬럼명, 행명으로 조회하기**
            - *`**items=None`* ⇒ 검색항목 지정**
            
            ```python
            print("1. c1 c3 컬럼 조회")
            print(df.filter(items=['c1', 'c3'], axis=1))
            #         c1  c3
            # mouse    4  24
            # rabbit   5  25
            # habit    6  26
            # mount    7  27
            # hunt     8  28
            
            print("2. rabbit mount 행 조회")
            print(df.filter(items=['rabbit', 'mount'], axis=0))
            #         c1  c2  c3
            # rabbit   5  15  25
            # mount    7  17  27
            ```
            
        - **특정 문자가 포함된 행, 레이블 조회하기**
            - *`**like: str | None = None`* ⇒ 비슷한 값 반환**
            
            ```python
            print("3. bit 포함된 행 조회")
            print(df.filter(like='bit', axis=0))
            #         c1  c2  c3
            # rabbit   5  15  25
            # habit    6  16  26
            
            print("4. c 포함된 컬럼 조회")
            print(df.filter(like='c', axis=1))
            #         c1  c2  c3
            # mouse    4  14  24
            # rabbit   5  15  25
            # habit    6  16  26
            # mount    7  17  27
            # hunt     8  18  28
            ```
            
        - **정규표현식을 이용한 조회**
            - *`**regex: str | None = None`* ⇒ 정규표현식**
                
                <aside>
                💡 **정규표현식 (regular expression)
                
                -** 일정한 패턴을 지정해서 패턴과 일치하는 문자열을 조회
                - 자바, 자바스크립트, 파이썬 지원
                
                </aside>
                
            
            ```python
            print("5. t로 끝나는 행 조회")
            print(df.filter(regex="t$", axis=0))
            #         c1  c2  c3  d1
            # rabbit   5  15  25  25
            # habit    6  16  26  27
            # mount    7  17  27  45
            # hunt     8  18  28  65
            
            print("6. m으로 시작하는 행 조회")
            print(df.filter(regex="^m", axis=0))
            #        c1  c2  c3  d1
            # mouse   4  14  24  24
            # mount   7  17  27  45
            
            print("7. 1~2 로 끝나는 컬럼 조회")
            print(df.filter(regex="[1-2]$", axis=1))
            #         c1  c2  d1
            # mouse    4  14  24
            # rabbit   5  15  25
            # habit    6  16  27
            # mount    7  17  45
            # hunt     8  18  65
            ```
            

### 컬럼

- ********************컬럼 추가********************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"국어":[4, 5, 6, 7, 8],
                       "영어":[14, 15, 16, 17, 18],
                       "수학":[24, 25, 26, 27, 28]})
    print(df)
    #   국어  영어  수학
    # 0   4  14  24
    # 1   5  15  25
    # 2   6  16  26
    # 3   7  17  27
    # 4   8  18  28
    ```
    
    - *`**df["새로운 컬럼"] = 값(리스트)**`*
        
        ```python
        # 1. 과학 컬럼 추가
        df["과학"] = [40, 35, 65, 71, 86]
        print(df)
        #    국어  영어  수학  과학
        # 0   4  14  24  40
        # 1   5  15  25  35
        # 2   6  16  26  65
        # 3   7  17  27  71
        # 4   8  18  28  86
        
        # 총합 컬럼 추가
        df["총합"] = df["국어"] + df["영어"] + df["수학"] + df["과학"]
        print(df)
        
        # 평균 컬럼 추가
        df["평균"] = df["총합"] / 4
        print(df)
        
        # 합격 여부 (평균 값이 25이상 합격 아니면 불합격)
        df["합격여부"] = ["합격" if avg > 25 else "불합격" for avg in df["평균"]]
        print(df)
        ```
        
    - *`**df.assign(컬럼명 = 리스트, 컬럼명 = 리스트, ...)**`*
        
        ```python
        # 1. 과학 컬럼 추가
        df = df.assign(과학=[40, 35, 65, 71, 86])
        print(df)
        #    국어  영어  수학  과학
        # 0   4  14  24  40
        # 1   5  15  25  35
        # 2   6  16  26  65
        # 3   7  17  27  71
        # 4   8  18  28  86
        # df = df.assign(총합=df["국어"] + df["영어"] + df["수학"] + df["과학"])
        def total_sum(x):
            return x["국어"] + x["영어"] + x["수학"] + x["과학"]
        
        total_sum2 = lambda df : df["국어"] + df["영어"] + df["수학"] + df["과학"]
        
        df = df.assign(총합=total_sum)
        df = df.assign(총합=lambda df : df["국어"] + df["영어"] + df["수학"] + df["과학"])
        print(df)
        #    국어  영어  수학  과학   총합
        # 0   4  14  24  40   82
        # 1   5  15  25  35   80
        # 2   6  16  26  65  113
        # 3   7  17  27  71  122
        # 4   8  18  28  86  140
        
        # 평균 컬럼 추가 ==> 일반함수 및 lambda 활용
        
        def avg(x):
            return x["총합"] / 4
        df = df.assign(평균=avg)
        print(df)
        
        df = df.assign(평균2=lambda df:df["총합"] / 4)
        print(df)
        
        # 합격여부 출력 => lambda 활용
        
        df = df.assign(합격여부= lambda df:["합격" if avg >= 25 else "불합격" for avg in df["평균"]])
        print(df)
        ```
        
    - *`**pd.concat()**`*
        
        ```python
        import numpy as np
        import pandas as pd
        
        df = pd.DataFrame({"국어":[4, 5, 6, 7, 8],
                           "영어":[14, 15, 16, 17, 18]})
        
        df2 = pd.DataFrame({"수학":[24, 25, 26, 27, 28]})
        # 국어, 영어컬럼과 수학컬럼 연결
        new_df = pd.concat([df, df2], axis=1)
        print(new_df)
        #    국어  영어  수학
        # 0   4  14  24
        # 1   5  15  25
        # 2   6  16  26
        # 3   7  17  27
        # 4   8  18  28
        ```
        
    
- **컬럼 삽입**
    
    DataFrame 생성
    
    ```python
    df = pd.DataFrame({"국어":[4, 5, 6, 7, 8],
                       "영어":[14, 15, 16, 17, 18]})
    ```
    
    - *`**df.insert(삽입할 컬럼위치, 컬럼명, 값, allow_duplicate=False)**`*
        - `allow_duplicate=True` 설정 시 중복 허용
        
        ```python
        df.insert(0, "수학",[24, 25, 26, 27, 28])
        print(df)
        #    수학  국어  영어
        # 0  24   4  14
        # 1  25   5  15
        # 2  26   6  16
        # 3  27   7  17
        # 4  28   8  18
        
        df.insert(1, "수학",[24, 25, 26, 27, 28], allow_duplicates=True) # allow_duplicate=False가 기본 값
        print(df)
        #    수학  수학  국어  영어 => allow_duplicates를 True로 설정해서 중복허용됨
        # 0  24  24   4  14
        # 1  25  25   5  15
        # 2  26  26   6  16
        # 3  27  27   7  17
        # 4  28  28   8  18
        ```
        
- ********************컬럼 삭제********************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"국어":[4, 5, 6, 7, 8],
                       "영어":[14, 15, 16, 17, 18],
                       "수학":[24, 25, 26, 27, 28],
                       "과학":[24, 25, 76, 27, 28],
                       "체육":[24, 45, 20, 27, 28],
                       "논술":[24, 25, 66, 7, 18]})
    print(df)
    #    국어  영어  수학  과학  체육  논술
    # 0   4  14  24  24  24  24
    # 1   5  15  25  25  45  25
    # 2   6  16  26  76  20  66
    # 3   7  17  27  27  27   7
    # 4   8  18  28  28  28  18
    ```
    
    - **********************************단일 컬럼 삭제**********************************
        - *`**df.pop('컬럼명')**`*
            
            ```python
            df.pop('국어') # => 일치하는 키가 없으면 에러발생
            print(df)
            #    영어  수학  과학  체육  논술
            # 0  14  24  24  24  24
            # 1  15  25  25  45  25
            # 2  16  26  76  20  66
            # 3  17  27  27  27   7
            # 4  18  28  28  28  18
            ```
            
        - *`**del df['컬럼명']**`*
            
            ```python
            del df['영어']
            print(df)
            #    수학  과학  체육  논술
            # 0  24  24  24  24
            # 1  25  25  45  25
            # 2  26  76  20  66
            # 3  27  27  27   7
            # 4  28  28  28  18
            ```
            
    - **************************************다중 컬럼 삭제**************************************
        - *`**df.drop(labels, axis=0|1)**`*
        - *`**df.drop(columns=값)`* ⇒ 컬럼 삭제 시**
            
            ```python
            # 2. 다중 컬럼 삭제
            df.drop(["체육", "논술"], axis=1, inplace=True)
            df.drop(columns=["과학"], inplace=True)
            print(df)
            #    수학
            # 0  24
            # 1  25
            # 2  26
            # 3  27
            # 4  28
            ```
            

### 행

- **************행 추가**************
    - 하나씩 추가
        - *`**df.append(df2)` (비권장)***
        
        <aside>
        💡 Warning 발생
        
        ```
        FutureWarning: The frame.append method is deprecated and will be removed from pandas in a future version. Use pandas.concat instead.
        new_df = df.append(df2, ignore_index=True)
        ```
        
        </aside>
        
        ```python
        new_df = df.append(df2, ignore_index=True) # pd.concat 쓰라는 warning 문구가 뜸
        print(new_df)
        ```
        
    - 여러개 추가
        - *`**pd.concat([df, df2], axis=0)` (권장)***
            
            ```python
            new_df = pd.concat([df, df2, df], axis=0, ignore_index=True)
            print(new_df)
            #     국어  영어  수학
            # 0    4  14  24
            # 1    5  15  25
            # 2    6  16  26
            # 3    7  17  27
            # 4    8  18  28
            # 5   94  84  94
            # 6   75  85  95
            # 7    4  14  24
            # 8    5  15  25
            # 9    6  16  26
            # 10   7  17  27
            # 11   8  18  28
            ```
            
        
- **************행 삭제**************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"국어":[4, 5, 6, 7, 8],
                       "영어":[14, 15, 16, 17, 18],
                       "수학":[24, 25, 26, 27, 28],
                       "과학":[24, 25, 76, 27, 28],
                       "체육":[24, 45, 20, 27, 28],
                       "논술":[24, 25, 66, 7, 18]
                       }, index=list("ABCDE"))
    print(df)
    #    국어  영어  수학  과학  체육  논술
    # A   4  14  24  24  24  24
    # B   5  15  25  25  45  25
    # C   6  16  26  76  20  66
    # D   7  17  27  27  27   7
    # E   8  18  28  28  28  18
    ```
    
    - *`**df.drop(labels, axis=0|1)**`*
        - *`labels: Hashable | Sequence[Hashable] | None = None,`*  **⇒ 삭제할 값**
        - *`axis: str | int = 0,`*
        - *`index: Hashable | Sequence[Hashable] | None = None,`*  **⇒ 행 삭제**
        - *`columns: Hashable | Sequence[Hashable] | None = None,`*  **⇒ 컬럼 삭제**
        - *`inplace: bool = False,`*  **********************************************************************************************************⇒ 원본을 바꿀건지 복사본을 만들건지**********************************************************************************************************
        - *`errors: Literal["ignore", "raise"] = "raise")`*
    - *`**df.drop(columns=값)` ⇒* 컬럼 삭제 시**
        
        ```python
        df.drop(['A', 'B'], inplace=True)
        print(df)
        #    국어  영어  수학  과학  체육  논술
        # C   6  16  26  76  20  66
        # D   7  17  27  27  27   7
        # E   8  18  28  28  28  18
        
        df.drop(['D', 'E'], inplace=True)
        print(df)
        #    국어  영어  수학  과학  체육  논술
        # C   6  16  26  76  20  66
        ```
        

### null

- ****************null 조회****************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"국어":[4, 5, 6, np.nan, 8],
                       "영어":[14, 15, 16, 17, np.nan],
                       "수학":[np.nan, 25, 26, 27, 28],
                       "과학":[np.nan, np.nan, np.nan, np.nan, np.nan]})
    
    print(df)
    # 0  4.0  14.0   NaN NaN
    # 1  5.0  15.0  25.0 NaN
    # 2  6.0  16.0  26.0 NaN
    # 3  NaN  17.0  27.0 NaN
    # 4  8.0   NaN  28.0 NaN
    ```
    
    - **************************************pandas 함수 이용**************************************
        - *`**pd.isna(df|Series)**`*
        - *`**pd.isnull(df|Series)**`*
        - ‘~’ ⇒ 부정에 의미
        
        ```python
        # null 찾기
        print(pd.isna(df))
        print(pd.isnull(df))
        
        print(pd.isna(df["국어"]))
        print(pd.isna(df[["국어", "영어"]]))
        print(pd.isnull(df["국어"]))
        print(pd.isnull(df[["국어", "영어"]]))
        
        m = "홍길동"
        print(pd.isna(m))
        print(pd.isnull(m))
        print(pd.isna(np.nan))
        print(pd.isnull(np.nan))
        
        # 부정
        print(pd.notnull(df))
        print(~pd.isnull(df))
        ```
        
    - **DataFrame 함수 이용**
        - *`**df.isnull()**`*
        - *`**df["컬럼"].isnull()**`*
        - *`**df[["컬럼", "컬럼"]].isnull()**`*
        
        ```python
        # null 찾기
        print(df.isnull())
        print(df["국어"].isnull())
        print(df["국어"].isnull().sum())
        print((~df["국어"].isnull()).sum())
        
        print(df[["국어", "영어"]].isnull())
        print(df[["국어", "영어"]].isnull().sum().sum()) # 널값 개수 찾기
        print(~df[["국어", "영어"]].isnull())
        print((~df[["국어", "영어"]].isnull()).sum().sum()) # 널값 개수 찾기
        ```
        
- ********************null 삭제********************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"국어":[4, 5, 6, np.nan, 8],
                       "영어":[14, 15, 16, 17, np.nan],
                       "수학":[np.nan, 25, 26, 27, 28],
                       "과학":[5, 4, 56, 43, 12]})
    
    print(df)
    # 0  4.0  14.0   NaN   5
    # 1  5.0  15.0  25.0   4
    # 2  6.0  16.0  26.0  56
    # 3  NaN  17.0  27.0  43
    # 4  8.0   NaN  28.0  12
    ```
    
    - *`**df.dropna()**`*
        - *`**def dropna()**`*
            - *`axis: str | int = 0,`*
                - `axis = 0` ⇒ 행 삭제
                - `axis = 1` ⇒ 열 삭제
            - *`how: str | _NoDefault = no_default,`* ****
                - `how='any'` ⇒ 하나라도 nan이면 삭제
                - `how='all'` ⇒ 모두 nan이면 삭제
            - *`thresh: int | _NoDefault = no_default,`*
            - *`subset: Hashable | Sequence[Hashable] | None = None,`*
            - *`inplace: bool = False) -> DataFrame | None` ⇒ 복사본 생성 or 원본 변경*
    - ************************************************하나라도 nan이면 삭제************************************************
        
        ```python
        print("1. 하나라도 nan이면 행 삭제")
        new_df = df.dropna(axis=0, how = "any")
        print(new_df)
        #     국어    영어    수학  과학
        # 1  5.0  15.0  25.0   4
        # 2  6.0  16.0  26.0  56
        
        print("2. 하나라도 nan이면 열 삭제")
        new_df = df.dropna(axis=1, how="any")
        print(new_df)
        #    과학
        # 0   5
        # 1   4
        # 2  56
        # 3  43
        # 4  12
        
        df = pd.DataFrame({"국어":[4,5,6,np.nan,np.nan],
                           "영어":[14,15,16,5,np.nan],
                           "수학":[np.nan,25,26,3,np.nan],
                           "과학":[4,5,6,34,np.nan],
                           "체육":[np.nan,np.nan,np.nan,np.nan,np.nan]})
        print(df)
        #     국어    영어    수학    과학  체육
        # 0  4.0  14.0   NaN   4.0 NaN
        # 1  5.0  15.0  25.0   5.0 NaN
        # 2  6.0  16.0  26.0   6.0 NaN
        # 3  NaN   5.0   3.0  34.0 NaN
        # 4  NaN   NaN   NaN   NaN NaN
        ```
        
    - **********모두 nan이면 삭제**********
        
        ```python
        print("3. 모두 nan이면 행 삭제")
        new_df = df.dropna(axis=0, how="all")
        print(new_df)
        #     국어    영어    수학    과학  체육
        # 0  4.0  14.0   NaN   4.0 NaN
        # 1  5.0  15.0  25.0   5.0 NaN
        # 2  6.0  16.0  26.0   6.0 NaN
        # 3  NaN   5.0   3.0  34.0 NaN
        
        print("4. 모두 nan이면 열 삭제")
        new_df = df.dropna(axis=1, how='all')
        print(new_df)
        #     국어    영어    수학    과학
        # 0  4.0  14.0   NaN   4.0
        # 1  5.0  15.0  25.0   5.0
        # 2  6.0  16.0  26.0   6.0
        # 3  NaN   5.0   3.0  34.0
        # 4  NaN   NaN   NaN   NaN
        ```
        
- ********************null값 변경********************
    
    DataFrame 생성
    
    ```python
    import numpy as np
    import pandas as pd
    
    df = pd.DataFrame({"국어":[4,5,6,np.nan,32],
                       "영어":[14,15,16,5,np.nan],
                       "수학":[np.nan,25,26,3,6],
                       "과학":[4,5,6,34,5]})
    print(df)
    #      국어    영어    수학  과학
    # 0   4.0  14.0   NaN   4
    # 1   5.0  15.0  25.0   5
    # 2   6.0  16.0  26.0   6
    # 3   NaN   5.0   3.0  34
    # 4  32.0   NaN   6.0   5
    ```
    
    - ******************************************************************임의의 값으로 변경(평균값, 중앙값)******************************************************************
        - *`**df.fillna(임의의 값)**`*
            
            ```python
            print("1. 임의의 값으로 변경")
            new_df = df.fillna(0)
            print(new_df)
            #      국어    영어    수학  과학
            # 0   4.0  14.0   0.0   4
            # 1   5.0  15.0  25.0   5
            # 2   6.0  16.0  26.0   6
            # 3   0.0   5.0   3.0  34
            # 4  32.0   0.0   6.0   5
            ```
            
        - *`**df.fillna({컬럼명: 값, 컬럼명: 값})**`*
            
            ```python
            print("2. 컬럼 단위로 null값을 임의의값으로 변경")
            new_df = df.fillna({"국어":0, "영어":-10, "수학": -20})
            print(new_df)
            #      국어    영어    수학  과학
            # 0   4.0  14.0 -20.0   4
            # 1   5.0  15.0  25.0   5
            # 2   6.0  16.0  26.0   6
            # 3   0.0   5.0   3.0  34
            # 4  32.0 -10.0   6.0   5
            ```
            
    - **************************************null 앞(forward)에 있는 값, 혹은 뒤(backward)에 있는 값으로 변경**************************************
        - *`**df.fillna(method = "ffill")`* ⇒ null값 앞(forward)에 있는 값으로**
            - 기본 DataFrame 변경됨
                
                ```python
                df = pd.DataFrame({"국어":[4,5,6,np.nan,32],
                                   "영어":[14,np.nan,16,5,10],
                                   "수학":[52,np.nan,25,26,3],
                                   "과학":[4,5,6,34,5]})
                print(df)
                #      국어    영어    수학  과학
                # 0   4.0  14.0  52.0   4
                # 1   5.0   NaN   NaN   5
                # 2   6.0  16.0  25.0   6
                # 3   NaN   5.0  26.0  34
                # 4  32.0  10.0   3.0   5
                
                print("3. null 앞에 있는 값으로 치환")
                new_df = df.fillna(method="ffill")
                print(new_df)
                #      국어    영어    수학  과학
                # 0   4.0  14.0  52.0   4
                # 1   5.0  14.0  52.0   5
                # 2   6.0  16.0  25.0   6
                # 3   6.0   5.0  26.0  34
                # 4  32.0  10.0   3.0   5
                ```
                
        - *`**df.fillna(method = "bfill")`* ⇒ null값 뒤(backward)에 있는 값으로**
            
            ```python
            print("4. null 뒤에 있는 값으로 치환")
            new_df = df.fillna(method="bfill")
            print(new_df)
            #      국어    영어    수학  과학
            # 0   4.0  14.0  52.0   4
            # 1   5.0  16.0  25.0   5
            # 2   6.0  16.0  25.0   6
            # 3  32.0   5.0  26.0  34
            # 4  32.0  10.0   3.0   5
            ```
            

### 정렬

DataFrame 생성

```python
import numpy as np
import pandas as pd

df = pd.DataFrame({"국어":[14,5,6,np.nan,32],
                   "영어":[14,15,16,5,np.nan],
                   "수학":[np.nan,25,26,3,6],
                   "과학":[4,5,6,34,5]},
                    index=list("BECAD"))
print(df)
#      국어    영어    수학  과학
# 0   14.0  14.0   NaN   4
# 1   5.0  15.0  25.0   5
# 2   6.0  16.0  26.0   6
# 3   NaN   5.0   3.0  34
# 4  32.0   NaN   6.0   5
```

- ************************************오름차순(기본): 모든 프로그램 언어의 기본************************************
- ******************내림차순******************
    
    *`**df.sort_values()**`*
    
    - *`ascending: bool | List[bool] | Tuple[bool, ...] = True,`* **⇒오름차순(기본)**
    - *`kind: str = "quicksort",`* **⇒ 정렬 알고리즘 지정**
    - *`na_position: str = "last",`* **⇒ null값의 위치 지정 (처음인지 마지막인지)**
    
    ```python
    print("1. 국어 컬럼으로 오름차순 정렬")
    new_df = df.sort_values(by=["국어"])
    new_df = df.sort_values(by=["국어"], ascending=False)
    new_df = df.sort_values(by=["국어"], ascending=False, na_position="first")
    print(new_df)
    
    df = pd.DataFrame({
              'col1': ['A', 'A', 'B', np.nan, 'D', 'C'],
              'col2': [2, 1, 9, 8, 7, 4],
              'col3': [0, 1, 9, 4, 2, 3],
              'col4': ['a', 'B', 'c', 'D', 'e', 'F']
            })
    print(df)
    #   col1  col2  col3 col4
    # 0    A     2     0    a
    # 1    A     1     1    B
    # 2    B     9     9    c
    # 3  NaN     8     4    D
    # 4    D     7     2    e
    # 5    C     4     3    F
    
    print("2. col1 col2 다중 정렬")
    new_df = df.sort_values(by=["col1", "col2"])
    new_df = df.sort_values(by=["col1", "col2"], ascending=False)
    print(new_df)
    
    print("3. col4 컬럼으로 오름차순 정렬")
    new_df = df.sort_values(by=["col4"])
    new_df = df.sort_values(by=["col4"], key=lambda col : col.str.lower())
    print(new_df)
    
    def xxx(col):
        print(col, type(col))
        return col.str.lower()
    new_df = df.sort_values(by='col4', key=xxx)
    # 0    a
    # 1    B
    # 2    c
    # 3    D
    # 4    e
    # 5    F
    # Name: col4, dtype: object <class 'pandas.core.series.Series'>
    # 65 A
    # 97 a
    #
    # Process finished with exit code 0
    
    # 외우기 A:65 a:97
    print(ord('A'), chr(65))
    print(ord('a'), chr(97))
    ```
    
    *`**df.sort_index()**`*  **⇒ 위치값이 아니고 레이블을 의미**
    
    - 행의 인덱스(레이블) 정렬
        - *`**df.sort_index(axis=0)**`*
            
            ```python
            # 1. 행 인덱스(레이블) 정렬
            new_df = df.sort_index(axis=0)
            new_df = df.sort_index(axis=0, ascending=False) # 내림차순
            print(new_df)
            #    korean  english  math  science  => 행의 순서가 내림차순으로 정렬됨
            # E     5.0     15.0  25.0        5
            # D    32.0      NaN   6.0        5
            # C     6.0     16.0  26.0        6
            # B    14.0     14.0   NaN        4
            # A     NaN      5.0   3.0       34
            ```
            
    - 열의 인덱스(레이블) 정렬
        - *`**df.sort_index(axis=1)**`*
            
            ```python
            # 2. 열 인덱스(레이블) 정렬
            new_df = df.sort_index(axis=1)
            new_df = df.sort_index(axis=1, ascending=False) # 내림차순
            print(new_df)
            #    science  math  korean  english  => 컬럼 순서가 알파벳 역순으로 정렬
            # B        4   NaN    14.0     14.0
            # E        5  25.0     5.0     15.0
            # C        6  26.0     6.0     16.0
            # A       34   3.0     NaN      5.0
            # D        5   6.0    32.0      NaN
            ```
            

## Data 수집

- 로컬 Data
- 웹사이트
- 크롤링
- DB

Data누락, 이상치

데이터 전처리

데이터 분석
