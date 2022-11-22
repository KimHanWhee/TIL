Python02 (11/22)
======================
- **문자열**
    - **함수**
        - **str.count(문자)**
            - 지정한 문자 개수 반환
            
            ```python
            a = 'hobby bc'
            print(a.count('b'))
            
            # 출력
            # 3
            ```
            
        - **str.index(문자)**
            - 지정한 문자가 처음 나오는 인덱스 반환
            
            ```python
            a = 'hobby bc'
            print(a.index('b'))
            
            # 출력
            # 2
            ```
            
        - ********str.join(문자)**
            - 문자열이 지정한 문자 사이사이에 들어감
            
            ```python
            it = ':'
            data = 'abcd'
            print(it.join(data))
            
            # 출력
            # a:b:c:d
            ```
            
        - **str.strip(제거할 문자)**
            - 지정한 문자 제거
            
            ```python
            u = "<<<    spam and ham    >>>"
            print(u.strip('< >'))
            # 출력
            # spam and ham
            ```
            
        - **str.replace(문자, 대체할 문자)**
            - 문자열 중 처음에 지정한 문자를 대체할 문자로 전부 교체
            
            ```python
            u = 'spam and ham'
            print(u.replace('spam', 'tomato and egg')
            # 출력
            # tomato and egg and ham
            ```
            
        - **str.split(구분자)**
            - 구분자를 기준으로 문자를 나눠 각각 리스트에 저장 구분자 미입력 시 공백을 기준으로 나눔
            
            ```python
            u = 'tomato and egg and ham'
            print(u.split())
            # 출력
            # ['tomato', 'and', 'egg', 'and', 'ham']
            ```
- **함수**
    - **def 함수명(받은 매개변수(없을 경우 비워둠)) : {실행 할 코드}**
        
        ```python
        #리턴값x,매개인자x
        def note():
        	print(2+3)
        ```
        
        ```python
        #리턴값x,매개인자O
        def fib(n):
        	gob=n*2
        ```
        
        ```python
        #리턴값O,매개인자X
        def point():
        	pt=7.9
        	return pt
        ```
        
        ```python
        #리턴값O,매개인자O
        def myDate(k,e):
        	hap=k+e
        	avg=hap/2
        	if avg>=70: message='축합격' else: message='재시험'
        	return (hap,avg,message)
        ```
        
    - **람다(lambda)함수**
        - 함수를 간단하게 한 줄로 표현하는 함수
            - 실행 코드
                
                <aside>
                💡 lambda {인자} : 인자 활용 코드
                
                </aside>
                
                ```python
                print((lambda b : 9 * b + 2000) (4)) #4가 b에 할당됨
                # 4 * 9 + 2000이 되므로
                # 2036이 출력됨
                
                lambda_func = (lambda b : 9 * b + 2000)
                print(lambda_func(4)) #위와 같은결과
                ```
                
            - 람다함수 내에서의 조건문
                
                <aside>
                💡 lambda {인자} : {참일 시 실행코드} if 조건 else {거짓일 시 실행코드}
                
                </aside>
                
                ```python
                print((lambda a, b : a if a > b else b) (8, 47))
                ```
                
            - 인자 여러개도 받을 수 있음
                
                ```python
                last = (lambda a, b, c : a * b * c) (3, 2, 5)
                print(last)
                
                print((lambda a, b, c : a * b *c) (3, 2, 5))
                
                two = lambda a, b, c : a * b * c
                print(two(3, 2, 5))
                ```
                
- **************************************객체**************************************
    - 객체는 속성(상태, 특징)과 행위(행동, 동작, 기능)로 구성된 대상을 의미함.
- **클래스**
