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
    - 객체를 만들려면 먼저 클래스를 선언해야함.
        - **class 클래스이름() : {실행될 코드}**
    
    ```python
    class Test() :  #클래스 선언
        userID = 'kimhanwhee'
        userPWD = '1234'
    
        def gugudan(self, n) :  #클래스 함수 안에서는 self.변수명 = 속성값으로 속성값을 설정하고
            for k in range(1, 10) : #self.변수명 으로 속성값을 가져옴(약속 느낌으로 쓰는듯)
                print(f'{n} * {k} = {n * k}')
            print('구구단 출력 끝')
            print(self.userID)  #self.변수명으로 속성값을 가져옴
            print(Test.userID)  #이렇게 클래스명으로도 가져와도 출력이 잘 됨
    
    Test().gugudan(9) #클래스 함수 밖에서는 클래스명.객체명으로 속성을 가져옴
    ```
