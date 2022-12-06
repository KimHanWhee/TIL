PlayData_Pandas02.md (2022/12/06)
========================

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
