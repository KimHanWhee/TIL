PlayData_Pandas03 (2022/12/08) 
=============================
- **Series 문자열**
    - *`**df["컬럼"].str.함수()**`*
        
        ```python
        df = pd.DataFrame({"name":["Hong","park","KIM"],
                           "age":[14,15,26],
                           "address":["seoul","pUsAN","JEJU"]})
        print(df)
        df["name"] = df["name"].str.replace("Hong", "HONG")
        df["address"] = df["address"].str.upper()
        print(df)
        #    name  age address
        # 0  HONG   14   SEOUL
        # 1  park   15   PUSAN
        # 2   KIM   26    JEJU
        ```
        
- ******날짜 함수******
    - ********************************************문자를 날짜로 변경********************************************
        - `**pd.to_datetime()**`
            - `format` ⇒ 지정된 문자열과 형식이 맞아야한다.
                
                ```python
                # 1. 문자를 날짜로 변경
                new_date = pd.to_datetime("2022-12-08")
                new_date = pd.to_datetime("2022년 12월 08일", format="%Y년 %m월 %d일")
                new_date = pd.to_datetime("20221208122530")
                new_date = pd.to_datetime("20221208122530", format="%Y%m%d%H%M%S")
                print(new_date)
                # 2022-12-08 12:25:30
                ```
                
    - **********************************************************범위지정해서 날짜 생성**********************************************************
        - **`pd.date_range()`**
            - `periods` ⇒ 몇개 출력 할건지
                
                ```python
                new_date = pd.date_range("2022-11-01", "2022-11-10")
                new_date = pd.date_range("2022-11-01", periods=5, freq="D") # freq 기본은 day
                new_date = pd.date_range("2022-11-01", periods=5, freq="m") # month
                new_date = pd.date_range("2022-11-01", periods=5, freq="Y") # Year
                print(new_date)
                # DatetimeIndex(['2022-12-31', '2023-12-31', '2024-12-31', '2025-12-31',
                #                '2026-12-31'],
                #               dtype='datetime64[ns]', freq='A-DEC')
                ```
                
    - ****************************************df에서 날짜 조회****************************************
        - **`pd.date_range()`**
            
            ```python
            new_date = pd.date_range("2022-11-01", periods=5, freq="D") # freq 기본은 day
            df = pd.DataFrame({'날짜':new_date})
            print(df)
            # 0 2022-11-01
            # 1 2022-11-02
            # 2 2022-11-03
            # 3 2022-11-04
            # 4 2022-11-05
            ```
            
            - **년도**
                
                ```python
                print(df["날짜"].dt.year) # 연도만 출력
                # 0    2022
                # 1    2022
                # 2    2022
                # 3    2022
                # 4    2022
                # Name: 날짜, dtype: int64
                ```
                
            - **월**
                
                ```python
                print(df["날짜"].dt.month) # 월만 출력
                # 0    11
                # 1    11
                # 2    11
                # 3    11
                # 4    11
                # Name: 날짜, dtype: int64
                ```
                
            - **일**
            
            ```
            print(df["날짜"].dt.day) # 일만 출력
            # 0    1
            # 1    2
            # 2    3
            # 3    4
            # 4    5
            # Name: 날짜, dtype: int64
            ```

### 병합

DataFrame 생성

```python
import numpy as np
import pandas as pd

df1 = pd.DataFrame({"x1":['A',"B",'C'],
                    "x2":[1,2,3]})

df2 = pd.DataFrame({"x1":['A',"B",'D'],
                    "x3":[10,20,30],
                    "x4":[9,8,6],})

print(df1)
#   x1  x2
# 0  A   1
# 1  B   2
# 2  C   3
print(df2)
#   x1  x3  x4
# 0  A  10   9
# 1  B  20   8
# 2  D  30   6
```

- **********inner병합(조인)**********
    
     두 개의 df간에 일치하는 행만 반환
    
    - **공통 컬럼이 있는 경우**
        - *`**pd.merge(df1, df2, on=공통 컬럼)**`*
        
        ```python
        new_df = pd.merge(df1, df2, on="x1")
        new_df = pd.merge(df1, df2[["x1","x3"]], on="x1")
        print(new_df)
        #   x1  x2  x3
        # 0  A   1  10
        # 1  B   2  20
        ```
        
    - **공통 컬럼이 없는 경우**
        - *`**pd.merge(df1, df2, left_on=df1컬럼, right_on=df2컬럼)**`*
            
            ```python
            new_df = pd.merge(df1, df2, left_on="x1", right_on="y1")
            print(new_df)
            #   x1  x2 y1  x3  x4
            # 0  A   1  A  10   9
            # 1  B   2  B  20   8
            ```
            
- **********outer병합(조인)**********
    
    두 개의 df 간에 일치하는 행 및 일치하지 않은 행 포합해서 반환
    
    - ************************************************공통 컬럼이 있는 경우************************************************
        - *`**pd.merge(df1, df2, on=공통 컬럼, how="inner(기본)|right|left|outer")**`*
            - *`how="left"` ⇒* 일치하지않는 df1 행 모두 반환
                
                ```python
                new_df = pd.merge(df1, df2, on="x1", how="left")
                print(new_df)
                #   x1  x2    x3   x4
                # 0  A   1  10.0  9.0
                # 1  B   2  20.0  8.0
                # 2  C   3   NaN  NaN
                ```
                
            - *`how="right"`* ⇒ 일치하지않는 df2 행 모두 반환
                
                ```python
                new_df = pd.merge(df1, df2, on="x1", how="right")
                print(new_df)
                #   x1   x2  x3  x4
                # 0  A  1.0  10   9
                # 1  B  2.0  20   8
                # 2  D  NaN  30   6
                ```
                
            - *`how="outer"`* ⇒ 일치하지않는 df1, df2 행 모두 반환
                
                ```python
                new_df = pd.merge(df1, df2, on="x1", how="outer")
                print(new_df)
                #   x1   x2    x3   x4
                # 0  A  1.0  10.0  9.0
                # 1  B  2.0  20.0  8.0
                # 2  C  3.0   NaN  NaN
                # 3  D  NaN  30.0  6.0
                ```
                
    - **공통 컬럼이 없는 경우**
        - *`**pd.merge(df1, df2, left_on=df1컬럼, right_on=df2컬럼, how="inner(기본)|right|left|outer")**`*
            
            ```python
            new_df = pd.merge(df1, df2, left_on="x1", right_on="y1", how="outer")
            print(new_df)
            #     x1   x2   y1    x3   x4
            # 0    A  1.0    A  10.0  9.0
            # 1    B  2.0    B  20.0  8.0
            # 2    C  3.0  NaN   NaN  NaN
            # 3  NaN  NaN    D  30.0  6.0
            ```
            

### 그룹핑(group by)

DataFrame 생성

```python
import numpy as np
import pandas as pd

df = pd.DataFrame({"사원번호":['A1','A2','A3','A4','A5'],
                    "월급":[100,200,150,250,120],
                    "부서번호":[10,20,10,20,30]})
print(df)
#   사원번호   월급  부서번호
# 0   A1  100    10
# 1   A2  200    20
# 2   A3  150    10
# 3   A4  250    20
# 4   A5  120    30
```

- **기본문법**
    - *`**df.groupby(by="컬럼명")[컬럼].그룹함수**`*
        - 부서별 sal 최대값/최소값/총합/평균/행개수 구하기
            
            ```python
            new_df = df.groupby(by="부서번호")["월급"].max()
            new_df = df.groupby(by="부서번호")["월급"].min()
            new_df = df.groupby(by="부서번호")["월급"].sum()
            new_df = df.groupby(by="부서번호")["월급"].mean()
            new_df = df.groupby(by="부서번호")["월급"].count()
            print(new_df)
            ```
            
        - DataFrame에 성별 추가 후 부서별 성별 월급 최대값 구하기
            
            ```python
            df = pd.DataFrame({"사원번호":['A1','A2','A3','A4','A5'],
                                "월급":[100,200,150,250,120],
                                "성별":['M',"F","F","M","M"],
                                "부서번호":[10,20,10,20,30]})
            print(df)
            #   사원번호   월급 성별  부서번호
            # 0   A1  100  M    10
            # 1   A2  200  F    20
            # 2   A3  150  F    10
            # 3   A4  250  M    20
            # 4   A5  120  M    30
            
            # 2. 부서별 성별 월급 최대값
            new_df = df.groupby(by=["부서번호", "성별"])["월급"].max()
            print(new_df)
            # 부서번호  성별
            # 10    F     150
            #       M     100
            # 20    F     200
            #       M     250
            # 30    M     120
            # Name: 월급, dtype: int64
            ```
            
- ******그룹 함수 한꺼번에 적용******
    - *`**df.groupby(by="컬럼명")[컬럼].agg([그룹함수, ...])**`*
        - **부서별 sal 최대값/최소값/총합/평균/행개수**
            
            ```python
            new_df = df.groupby(by="부서번호")["월급"].agg([np.max, np.min, np.sum, np.mean, "count"])
            new_df = df.groupby(by="부서번호")["월급"].agg(["max", "min", "sum", "mean", "count"])
            print(new_df)
            #       max  min  sum   mean  count
            # 부서번호
            # 10    150  100  250  125.0      2
            # 20    250  200  450  225.0      2
            # 30    120  120  120  120.0      1
            ```
            
        - **컬럼별로 그룹함수 지정**
            - *`**df.groupby(by="컬럼명").agg({**"컬럼1":['max', 'min'],**"컬럼2":['sum'],**...})***`
            
            ```python
            new_df = df.groupby(by="부서번호").agg({
                "월급":["max", "min"],
                "부서번호":["count"]
            })
            print(new_df)
            
            #       max  min count
            # 부서번호
            # 10    150  100     2
            # 20    250  200     2
            # 30    120  120     1
            ```
            
        - **병합 후 부서별 월급 최대값 출력**
            
            DataFrame 추가
            
            ```python
            import numpy as np
            import pandas as pd
            
            df1 = pd.DataFrame({"사원번호":['A1','A2','A3','A4','A5'],
                                "월급":[100,200,150,250,120],
                                "부서번호":[10,20,10,20,30]})
            df2 = pd.DataFrame({"부서번호":[10,20,30],
                                "부서명":["개발","인사","관리"]})
            ```
            
            ```python
            new_df = pd.merge(df1, df2, on="부서번호").groupby(by=["부서번호"])["월급"].max()
            print(new_df)
            # 부서번호
            # 10    150
            # 20    250
            # 30    120
            # Name: 월급, dtype: int64
            ```
            

### csv(comma-seperated value)읽기

- **csv파일 읽기**
    - `**pd.read_csv("파일 경로", encoding='utf-8')**`
        
        ```python
        df = pd.read_csv("./data/msft.csv", encoding='utf-8') # encoding='utf-8' 지정해서 한글처리 필요
        print(df.head())
        #         Date   Open   High    Low  Close   Volume
        # 0  7/21/2014  83.46  83.53  81.81  81.93  2359300
        # 1  7/18/2014  83.30  83.40  82.52  83.35  4020800
        # 2  7/17/2014  84.35  84.63  83.33  83.63  1974000
        # 3  7/16/2014  83.77  84.91  83.66  84.91  1755600
        # 4  7/15/2014  84.30  84.38  83.20  83.58  1874700
        ```
        
- **특정컬럼을 인덱스로 변경**
    - `**pd.read_csv("파일경로", index_col=컬럼 인덱스)**`
        
        ```python
        df = pd.read_csv("./data/msft.csv", index_col=0)
        print(df.head())
        #             Open   High    Low  Close   Volume
        # Date
        # 7/21/2014  83.46  83.53  81.81  81.93  2359300
        # 7/18/2014  83.30  83.40  82.52  83.35  4020800
        # 7/17/2014  84.35  84.63  83.33  83.63  1974000
        # 7/16/2014  83.77  84.91  83.66  84.91  1755600
        # 7/15/2014  84.30  84.38  83.20  83.58  1874700
        ```
        
- ****************************컬럼명 변경****************************
    - `**pd.read_csv('파일경로', header=0, names=[바꿀 컬럼 이름])**`
        
        ```python
        df = pd.read_csv('./data/msft.csv', header=0, names=[ 'date', 'open', 'high', 'low', 'close', 'volume'])
        print(df.head())
        #         date   open   high    low  close   volume
        # 0  7/21/2014  83.46  83.53  81.81  81.93  2359300
        # 1  7/18/2014  83.30  83.40  82.52  83.35  4020800
        # 2  7/17/2014  84.35  84.63  83.33  83.63  1974000
        # 3  7/16/2014  83.77  84.91  83.66  84.91  1755600
        # 4  7/15/2014  84.30  84.38  83.20  83.58  1874700
        ```
        
- **********************************************지정된 컬럼만 보기**********************************************
    - `**pd.read_csv('파일경로', usecols=[컬럼 이름/인덱스])**`
        
        ```python
        df = pd.read_csv('./data/msft.csv', usecols=["Date", "Open", "High"])
        df = pd.read_csv('./data/msft.csv', usecols=[0, 1, 2])
        print(df.head())
        #         Date   Open   High
        # 0  7/21/2014  83.46  83.53
        # 1  7/18/2014  83.30  83.40
        # 2  7/17/2014  84.35  84.63
        # 3  7/16/2014  83.77  84.91
        # 4  7/15/2014  84.30  84.38
        ```
        
- **지정된 개수만큼 처리**
    - `**pd.read_csv('./data/msft.csv', nrows=개수)**`
        
        ```python
        df = pd.read_csv('./data/msft.csv', nrows=4)
        print(df)
        #         Date   Open   High    Low  Close   Volume
        # 0  7/21/2014  83.46  83.53  81.81  81.93  2359300
        # 1  7/18/2014  83.30  83.40  82.52  83.35  4020800
        # 2  7/17/2014  84.35  84.63  83.33  83.63  1974000
        # 3  7/16/2014  83.77  84.91  83.66  84.91  1755600
        ```
        
- ****NaN처리****
    - `**pd.read_csv('파일경로', na_filter=True(기본값)|False)**`
        
        ```python
        df = pd.read_csv('./data/company3.csv') # na_filter = True(기본) NaN로 처리
        print(df)
        #    판매년도  판매월   제품   판매처    수량     금액
        # 0  2010    1  노트북   백화점  10.0  200.0
        # 1  2010    1  핸드폰  하이마트   5.0  200.0
        # 2  2010    1   PC   편의점   NaN  200.0
        # 3  2010    2  노트북   백화점   9.0    NaN
        
        df = pd.read_csv('./data/company3.csv', na_filter=False) # na_filter = False설정 시 NaN값 공백으로 처리
        print(df)
        #    판매년도  판매월   제품   판매처  수량   금액
        # 0  2010    1  노트북   백화점  10  200
        # 1  2010    1  핸드폰  하이마트   5  200
        # 2  2010    1   PC   편의점      200
        # 3  2010    2  노트북   백화점   9
        ```
        
- **지정한 값을 nan 변경**
    - `**pd.read_csv('파일경로', na_values=[지정값])**`
        
        ```python
        df = pd.read_csv('./data/company3.csv', na_values=[200, 10]) # => 지정값 NaN으로 변경
        print(df)
        #    판매년도  판매월   제품   판매처   수량  금액
        # 0  2010    1  노트북   백화점  NaN NaN
        # 1  2010    1  핸드폰  하이마트  5.0 NaN
        # 2  2010    1   PC   편의점  NaN NaN
        # 3  2010    2  노트북   백화점  9.0 NaN
        ```
        
- **,(쉼표)가 아닌 구분자로된 데이터 처리**
    - `**pd.read_csv("파일경로", sep='구분자', index_col=컬럼인덱스)**`
        
        ```python
        df = pd.read_csv("./data/msft_piped.txt")
        print(df.head())
        #               |Date|Open|High|Low|Close|Volume
        # 0  0|7/21/2014|83.46|83.53|81.81|81.93|2359300
        # 1    1|7/18/2014|83.3|83.4|82.52|83.35|4020800
        # 2  2|7/17/2014|84.35|84.63|83.33|83.63|1974000
        # 3  3|7/16/2014|83.77|84.91|83.66|84.91|1755600
        # 4    4|7/15/2014|84.3|84.38|83.2|83.58|1874700
        
        df = pd.read_csv("./data/msft_piped.txt", sep='|', index_col=0)
        print(df.head())
        #         Date   Open   High    Low  Close   Volume
        # 0  7/21/2014  83.46  83.53  81.81  81.93  2359300
        # 1  7/18/2014  83.30  83.40  82.52  83.35  4020800
        # 2  7/17/2014  84.35  84.63  83.33  83.63  1974000
        # 3  7/16/2014  83.77  84.91  83.66  84.91  1755600
        # 4  7/15/2014  84.30  84.38  83.20  83.58  1874700
        ```
        
- **csv로 파일저장**
    - `**데이터프레임.to_csv('저장할 파일 경로')**`
        
        ```python
        new_df = df.head(3)
        print(new_df)
        new_df.to_csv('./data/custom_out.csv')
        ```
