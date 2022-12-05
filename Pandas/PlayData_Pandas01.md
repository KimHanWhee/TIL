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
    - *`df.컬럼명`* ⇒ Series 반환
        
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
        
    - *`df['컬럼명']`* ⇒ Series 반환
        
        ```python
        print(df['c3'], type(df['c3']))
        # 0    24
        # 1    25
        # 2    26
        # Name: c3, dtype: int64 <class 'pandas.core.series.Series'>
        ```
        
    - *`df[['컬럼명', '컬럼명', ...]]`* ⇒ DataFrame 반환
        
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
        - *`df.loc[행 라벨]`* ⇒ 인덱싱 색인
            
            ```python
            print(df.loc['B'], type(df.loc['B']))
            # c1     5
            # c2    15
            # c3    25
            # Name: B, dtype: int64 <class 'pandas.core.series.Series'>
            ```
            
        - *`df.loc[행 라벨, 행 라벨, ...]`* ⇒ fancy 색인
            
            ```python
            print(df.loc[['B','C']], type(df.loc[['B','C']]))
            #    c1  c2  c3
            # B   5  15  25
            # C   6  16  26 <class 'pandas.core.frame.DataFrame'>
            ```
            
        - *`df.loc[행 라벨1 : 행 라벨2]`*  ⇒ 슬라이싱 색인, 행 라벨 2를 **포함**함.
            
            ```python
            print(df.loc['B':'E'], type(df.loc['B':'E'])) # 슬라이싱 색인
            # B   5  15  25
            # C   6  16  26
            # D   7  17  27
            # E   8  18  28 <class 'pandas.core.frame.DataFrame'>
            ```
            
        - *`df.loc[[True, ...]]`* ⇒ 불린 색인
            
            ```python
            print(df.loc[[True, False, False, False, False]]) # 불린 색인
            #    c1  c2  c3
            # A   4  14  24
            ```
            
    - **행 위치 이용**
        - *`df.iloc[행 위치]`* ⇒ 인덱싱 색인
            
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
            
        - *`df.iloc[[행 위치, 행 위치, ...]]`*  ⇒ fancy 색인
            
            ```python
            print(df.iloc[[0,2,-1]])
            #    c1  c2  c3
            # A   4  14  24
            # C   6  16  26
            # E   8  18  28
            ```
            
        - *`df.iloc[start:stop]`*  ⇒ 슬라이싱 색인, ****stop **전** 까지
            
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
            
        - *`df.iloc[[True, ...]]`* ⇒ 불린 색인
            
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
        - 기본 문법은 *********************************`df.loc[행 라벨, 컬럼 라벨]`*********************************
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
        - 기본문법은 *`df.iloc[행 위치, 컬럼 위치]`*
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
        - *`df.loc[행 라벨, 컬럼 라벨] = 값`*
        - 행 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
        - 컬럼 위치 지정 형식(인덱싱, fancy, 슬라이싱, 불린)
    - **위치 조회**
        - *`df.iloc[행 위치, 컬럼 위치] = 값`*
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
