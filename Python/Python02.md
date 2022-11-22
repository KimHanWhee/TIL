Python02 (11/22)
======================
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
- **************************************객체**************************************
    - 객체는 속성(상태, 특징)과 행위(행동, 동작, 기능)로 구성된 대상을 의미함.
- **클래스**
