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

## 시각화

### 기본

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
        

### 선그래프

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
