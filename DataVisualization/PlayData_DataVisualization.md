DataVisualization (2022/12/09)
================
1. matplotlib
    1. `pip install matplotlib`
    2. 라이브러리 이용 ⇒ 사용이 까다롭다
2. seaborn
    1. 라이브러리 이용
    2. matplotlib 기반
3. pandas
    1. matplotlib 기반

## 기본

- ****************************도화지 얻기****************************
    - **************`plt.figure()`**************
- ********************************하나의 붓 얻기********************************
    - `**plt.axes()**`
- ****************************chart 그리기****************************
    - `**plt.show()**`
    - `**plt.plot()**`
        
        ```python
        plt.plot([1, 2, 3, 4])  # y값 x값은 자동설정
        plt.plot([6, 5, 7, 2])  # y값 x값은 자동설정
        ```
        
- **도화지(figure)와 북(axes) 한꺼번에 얻기**
    - ******`plt.subplots()`******
        
        ```python
        fig, ax = plt.subplots()
        ```
        
- **하나의 도화지(figure)에 여러 axes(영역, 붓) 생성 ⇒ 배열로 반환**
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    import pandas as pd
    
    # 도화지 얻기
    fig, ax = plt.subplots(nrows=1, ncols=2)
    
    # chart 그리기
    ax[0].plot([1, 2, 3, 4])  # y값 x값은 자동설정
    ax[1].plot([6, 5, 7, 2])  # y값 x값은 자동설정
    
    plt.show()
    ```
    
- **하나의 figure에 여러개의 chart 시각화**
    - `**fig, ax = plt.subplots(행갯수, 열갯수)` ⇒ 배열로 반환**
    - *`**fig = plt.figure()**`*
        - *`**ax = fig.add_subplot(행, 열, 사용하고자하는 열값)**`*
        
        ```python
        fig = plt.figure()
        
        ax1 = fig.add_subplot(1, 2, 1) # 1행 2열의 첫번째 열 할당
        ax2 = fig.add_subplot(1, 2, 2) # 1행 2열의 두번째 열 할당
        
        ax1.plot([1, 2, 3, 4])
        ax2.plot([1, 2, 3, 4])
        plt.show()
        ```
        

## 선그래프

- `**plt.plot()` 함수 이용 또는  `ax.plot()`**
- ************************************선(line) 또는 마커(marker, point)그릴 때 사용************************************
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    import pandas as pd
    
    # 도화지 얻기
    fig = plt.figure(figsize=(10,4)) # (width, height) 인치
    
    ax1 = fig.add_subplot(1, 2, 1) # 1행 2열의 첫번째 열 할당
    plt.plot([1, 2, 3, 4]) # y값, x값은 자동 지정
    
    ax2 = fig.add_subplot(1, 2, 2) # 1행 2열의 두번째 열 할당
    plt.plot([1, 4, 6, 3], [1, 2, 3, 4]) # x값 y값
    plt.show()
    ```
    
- ****************************레이블 지정****************************
    - `**plt.xlabel(값)` ⇒ x축 이름 지정**
    - `**plt.ylabel(값)` ⇒ y축 이름 지정**
        
        ```python
        plt.plot([1, 4, 6, 3], [1, 2, 3, 4]) # x값 y값
        plt.xlabel("x값")
        plt.ylabel("y값")
        ```
        
- ************************************************************************************한글 처리 및 다양한 환경 설정 (Runtime Configuration 이용)************************************************************************************
    - `**plt.rc("키", 속성 = "값")**`
    - `**plt.rc("font", family="Malgun Gothic")**`
    - `**plt.style.use('theme')**`
        
        ```python
        # 한글 처리 및 다양한 환경설정 (Runtime Configuration 이용)
        plt.rc("font", family="Malgun Gothic")
        plt.rc("font", size=15)
        plt.style.use('fivethirtyeight')
        plt.rcParams['axes.unicode_minus'] = False
        ```
        
- ******************************축범위지정******************************
    - `**plt.axis([xmin, xmax, ymin, ymax])` ⇒ 지정하지 않으면 자동으로 데이터 값에 맞춤**
        
        ```python
        plt.plot([1, 4, 6, 3], [1, 2, 3, 4]) # x값 y값
        plt.axis([0,10, 0,8]) # x축 0~10 y축 0~8
        ```
        
- **축눈금지정**
    - `**plt.xticks(리스트)` ⇒ x축 눈금**
    - `**plt.yticks(리스트)` ⇒ y축 눈금**
        
        ```python
        # 축눈금 지정
        plt.xticks([0,5,10])
        plt.yticks([1,4,8])
        ```
        
    - `**plt.yticks(리스트, lables=리스트, rotation=눈금 글자 각도)**`
        
        ```python
        plt.xticks([0, 5, 10], labels=["1G", "5G", "10G"], rotation=45)
        plt.yticks([1, 4, 8], labels=["1만원", "4만원", "8만원"])
        ```
        
- **************************선 색상**************************
    - `**plt.plot(..., color=값)**`
        
        ```python
        plt.plot([1, 4, 6, 3], [1, 2, 3, 4], color="r") # 빨강
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], color="blue") # 파랑
        plt.plot([11, 4, 6, 3], [6, 12, 3, 3], color="#7f7f7f")
        ```
        
- **************************marker 지정**************************
    - `**plt.plot(..., marker="값")` ⇒ marker와 속성 지정 시 선 + marker 출력**
    - `**plt.plot(...,"값")` ⇒ marker 속성을 지정하지 않으면 선 없이 marker 출력**
        
        ```python
        plt.plot([1, 4, 6, 3], [1, 2, 3, 4], marker="P") # P와 선 출력
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], "*") # 별표만 출력
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], marker="*", color="blue") # 파란색 별
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], "*", color="r") # 빨간색 별
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], "gD") # color와 marker 같이표현
        ```
        
- ********************선스타일********************
    - `**plt.plot(..., linstyle="값")**`
        
        ```python
        plt.plot([1, 4, 6, 3], [1, 2, 3, 4], linestyle="-") # solid
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], linestyle="--") # 점선
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], linestyle="-.") # -.-.-
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], linestyle=":") # 점선
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], linestyle=":", color="yellow", marker="^") # color와 marker 같이표현
        ```
        
- ********범례(legend)********
    - ************************범례 방법1************************
        
        ```python
        plt.plot(..., label="값1")
        plt.plot(..., label="값2")
        plt.legend()
        ```
        
        - 예시
        
        ```python
        plt.plot([1, 4, 6, 3], [1, 2, 3, 4], label="1학년")
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], label="2학년")
        plt.plot([4, 13, 15, 8], [15, 21, 5, 2], label="3학년")
        
        plt.legend()
        plt.show()
        ```
        
    - ************************범례 방법2************************
        
        ```python
        plt.plot(...)
        plt.plot(...)
        plt.legend(["값1", "값2"])
        ```
        
        - 예시
        
        ```python
        plt.plot([1, 4, 6, 3], [1, 2, 3, 4], linestyle="-")
        plt.plot([4, 1, 5, 8], [12, 2, 35, 4], linestyle="--")
        plt.plot([4, 13, 15, 8], [15, 21, 5, 2], linestyle="-.")
        
        plt.legend(["1학년", "2학년", "3학년"])
        plt.show()
        ```
        
- ******************격자(grid)******************
    - `**plt.grid(visible=True, axis="both|x|y")**`
        - 지정한 축 기준으로 격자 생성
        
        ```python
        plt.grid(visible=True, axis="x", color='r', linestyle=":")
        # x축을 기준으로 빨간색 점선 생성
        ```
        
- **************타이틀**************
    - **`plt.title(label="값", loc="center|left|right", pad=30, fontdict=딕셔너리)`**
        - 지정한 문자와 속성들로 제목 생성됨
        
        ```python
        plt.title("학생 출석현황", loc="right", pad=10)
        ```
        

## 막대그래프

- `**plt.bar(x, y) => x는 종류(범주), y는 x범주에 해당되는 데이터 값 지정)**`
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    import pandas as pd
    
    # 도화지 얻기
    fig = plt.figure()
    
    # 하나의 붓 얻기
    ax = plt.axes()
    
    x = [0, 1, 2] # 범주
    y = [100, 200, 300] # x 범주에 해당되는 값
    plt.bar(x, y)
    
    plt.show()
    ```
    
- `**plt.barh(x, y)**`
    - 막대가 가로로 출력
- ****************`plt.bar()` 속성**
    
    ```python
    plt.bar(x, y,
            width=0.4,
            color="aliceblue",
            align="edge",
            edgecolor="skyblue",
            linewidth=2,
            tick_label=["1G", "2G", "3G"])
    ```
    
- **막대 여러개 쌓기**
    - 2개
    
    ```python
    x = [0, 1, 2] # 범주
    y1 = [100, 200, 300] # x 범주에 해당되는 값
    y2 = [200, 150, 50] # x 범주에 해당되는 값
    plt.bar(x, y1, label="y1")
    plt.bar(x, y2, label="y2", bottom=y1)
    
    plt.legend()
    plt.show()
    ```
    
    - 2개 이상
        - 2개 이상은 깨져서 나오므로 2개를 numpy 벡터연산으로 더해 변수 저장 후 나머지 하나 연결
    
    ```python
    x = [0,1,2] # 범주
    y1 = [100,200,300] # x에 해당되는 값
    y2 = [200,150,50]
    y1_2 = np.array(y1) +np.array(y2)
    y3 = [50,50,50]
    
    plt.bar(x, y1, label="y1")
    plt.bar(x, y2, label="y2", bottom=y1)
    plt.bar(x, y3, label="y3", bottom=y1_2)
    ```
    

## 산점도 (scatter plot)

- **두 변수간(x, y)의 상관관계를 점(dot)로 표현**
- **plt.scatter(x, y, s="dot크기", c="색상", alpha="투명도")**
    
    ```
    x = np.random.rand(50)
    y = np.random.rand(50)
    size = (40*np.random.rand((50))) **2
    color = np.random.rand(50)
    
    plt.scatter(x,y,s=size,c=color,alpha=0.2) # alpha는 투명도
    ```
    

## 파이차트

- ******************************범주(종류)의 구성비율을 원형으로 표현******************************
- ****************************************************구성비율의 종합은 100****************************************************
- ****************`**plt.pie()**`****************
    
    ```python
    value = [34, 32, 16, 18] # 총합 100
    labels = ['바나나', '사과', '귤', '수박']
    explode = (0.3, 0.1, 0, 0)
    
    plt.pie(value,
            labels=labels,
            autopct='%1.1f%%',
            startangle=180,     # 시작 각도 설정
            counterclock=False, # 기본적으로는 시계방향으로 간다.
            colors=["red", "blue", "green", "yellow"],
            explode=explode,
            shadow=True)
    ```
    

## 히스토그램

- **도수분포표**
    - 특정구간(범위)에 속하는 데이터의 개수를 표현
- **히스토그램**
    - 도수분포표를 시각화 한것
        - 막대그래프는 y값만 고려한다. x는 범주이기 때문에
        - 히스토그램은 x와 y값 모두 고려한다.
    
    ```python
    weight = [68, 81, 64, 56, 78, 74, 61, 77, 66, 68, 59, 71, 80, 59, 67, 81, 69, 73, 69, 74, 70, 65]
    print(sorted(weight), len(weight))
    
    plt.hist(weight)
    ```
    
- ************************범위의 개수 지정************************
    - ********`hist(..., bins=값)`********
        
        ```python
        fig, ax = plt.subplots(1, 3)
        ax[0].hist(weight)
        ax[1].hist(weight, bins=5)
        ax[2].hist(weight, bins=8)
        ```
        
    - 추가 속성
        - **********`**alpha` : 투명도**
        - `**histtype`**
            - **`bar`(기본값) : 막대 형태**
            - **`barstacked` : 여러 데이터가 쌓인 막대 형태**
            - **`step` : 내부가 비어 윤곽만 있는 막대형태**
            - **`stepfilled` : 내부가 차있는 막대형태**
