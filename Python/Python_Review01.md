Python_Review01 (2022/11/29)
================
# Python 설치

### path 환경변수

⇒ 명령어 경로 지정

******************프로그램******************

- python 명령어 : python.exe
- java 명령어 : javac.exe. java.exe

### 파이썬 설치 폴더 확인

- **python.exe**
    
    파이썬을 실행 하기위한 프로그램
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6c92e6e9-43ad-454e-890a-235ba3c8ed8c/Untitled.png)
    
- **************scripts**************
    - 파이썬 관련 명령어를 사용할 수 있게 해주는 프로그램 (ex. pip)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70ddd7be-d362-4f53-98ed-2c3f8cc404a5/Untitled.png)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30ac2470-3953-4f49-8187-44089dfbdf50/Untitled.png)
        

## pycharm 설치

### File/Setting

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/89834626-4f85-4a8e-a386-4aac4aa99ba8/Untitled.png)

- Project ⇒ python interpreter
    - 사용가능한 패키지 확인 & ‘+’버튼으로 패키지 추가 가능
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db2e1ced-0788-47c4-9cdb-870574aacbb2/Untitled.png)
        
        ![제목 없음.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bae91fc0-c012-4917-b511-a7f3682db3ca/%EC%A0%9C%EB%AA%A9_%EC%97%86%EC%9D%8C.png)
        

### Python

- 모든 것이 객체(object)로 관리
- __bulitins__ 객체
    - ‘.’ 없이 사용가능
    
    ```python
    '''
        print(dir(__builtins__))
    
    '''
    '''
    'abs', 'all', 'any', 'ascii', 'bin', 'bool', 'breakpoint', 'bytearray', 'bytes', 'callable', 'chr', 'classmethod', 'compile', 
    'complex', 'copyright', 'credits', 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit', 'filter', 'float', 
    'format', 'frozenset', 'getattr', 'globals', 'hasattr', 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass', 
    'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview', 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 
    'print', 'property', 'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice', 'sorted', 'staticmethod', 'str', 
    'sum', 'super', 'tuple', 'type', 'vars', 'zip']
    '''
    
    # divmod 함수는 몫과 나머지 반환
    print(divmod(10, 3)) # (3, 1)
    x, y = divmod(10, 3)
    print("몫 : {} 나머지 : {}".format(x, y))
    
    # zip 함수는 key : value 쌍으로 묶어줄 때 사용
    x = ['name', 'age']
    y = ['홍길동', 20]
    print(dict(zip(x, y)))
    
    # reversed() ==> 거꾸로된 복사본 반환(원본 변경 없음)
    x = [1, 2, 3, 4, 5]
    print(list(reversed(x)), x)
    
    # list의 reverse() ==> 자신이 거꾸로 변경됨(원본 변경됨)
    x2 = [1, 2, 3, 4, 5]
    x2.reverse()
    print(x2)
    
    # sorted() ==> 정렬된 복사본 반환(원본 변경 없음)
    k = [85, 24, 67, 11, 4, 7]
    print(list(sorted(k)), k) # [4, 7, 11, 24, 67, 85] [85, 24, 67, 11, 4, 7]
    # list의 sort() ==> 자신이 정렬됨(원본 변경됨)
    k2 = [85, 24, 67, 11, 4, 7]
    k2.sort()
    print(k2) # [4, 7, 11, 24, 67, 85]
    
    # enumerate() ==> 반복문에서 index값 얻을 때 사용
    for n in [10, 20, 30]:
        print(n)
    for i, n in enumerate([10, 20, 30]) :
        print(i, n)
    
    for i, n in enumerate([10, 20, 30], 1) :
        print(i, n)
    ```
    

### 자료형 (Data Type)

- **일반 자료형 (scalar타입, 불변(immutable))**
    - **정수**
        - 음수, 0, 양수로 구성된 숫자
        - ex) 0, 5, 10, 25
    - **실수**
        - 소수점을 가지고 있는 숫자
        - ex) 0.1, 0.5, 1.5, 3.14
    - **논리**
        - True, False
    - **함수**
        - 기능 처리 담당
        
        <aside>
        💡 함수를 data로 처리하는 언어 
        python, javascript
        
        </aside>
        
    - **None**
        - 값이 없음 or null을 의미
- ****************************집합 자료형****************************
    - **문자열(str)**
        - 값 변경 불가(immutable), ‘’,””,””” “”” 로 표현
    - **리스트(list)**
        - 순서가 존재, 중복을 허용하고 값 변경 가능(mutable), [값1, 값2,…]로 표현
    - **튜플(tuple)**
        - 순서가 존재, 중복을 허용하고 값 변경은 불가(immutable), (값1, 값2,…)로 표현
    - **셋(set)**
        - 순서가 없음, 중복을 허용하지 않고 반드시 불변(immutable) 값만 저장, {값1, 값2,…}로 표현
    - **딕셔너리(dict)**
        - {”key값” : “value값”}로 표현

## escape 문자

- R**aw String (print(r’’))**
    - escape문자 무시
    
    ```python
    print("hello\tworld")
    # 출력
    # hello	world
    
    # raw string : escape 문자 무시
    print(r"hello\tworld")
    # 출력
    # hello\tworld
    ```
    

## 식별자 (identifier)

### 시스템 식별자

******************************************************시스템의 필요에 의해 미리 정의된 단어 ⇒ 키워드 예약어******************************************************

ex) print, if, for, pass, continue,…

<aside>
💡 밑 코드로 시스템 식별자를 출력하여 확인 가능

```python
import keyword

print(keyword.kwlist)
```

</aside>

### 사용자 식별자

************************************************************************사용자의 필요에 의해 정의된 단어************************************************************************

ex) m = 10, str = ‘hello’ 와 같은 변수명, 함수명, 클래스명 등

## 변수 (variable)

**모든 변수는** **참조형 변수**

**************************참조형 변수 ⇒************************** 변수에 가면 실제값이 아닌 값이 저장되어있는 **주소값**을 갖음

### 변수 선언

```python
m = 10

x = x2 = x3 = 100
print(x, x2, x3)

# 값 분해 ==> 반드시 갯수가 일치해야 한다
n, n2 = 100, 200 # 100, 200은 튜플 형태의 데이터 1개이다.
n, n2 = (100, 200)
print(n, n2) # 100 200

n, n2 = [1000, 2000]
print(n, n2) # 1000 2000 리스트도 작동 됨

def fun() :
    return "홍길동", 200 # 튜플 형태의 데이터 1개

result = fun()
print(result)  # ('홍길동', 200) 튜플 형태로 나타남

# 매우 중요
name, age = fun() # 튜플형태의 데이터가 각각 변수에 하나씩 들어감 == name, age = '홍길동', 200
print(name, age) # 홍길동 200

# 중첩형
xx = [10, 43, [65, 22, 54, [300]]]
print(xx[2][3][0]) # 300
# 분배, 모양이 반드시 같아야 함
[a,b, [c, d, e, [f]]] = [10, 43, [65, 22, 54, [300]]]
print(f) # 300

# dummy 변수 해당 값이 필요없을 때 선언
name, age = '홍길동', 200
name, _ = '홍길동', 400

print(name)

# _변수에 값이 저장이 되긴하지만 이 변수는 사용하지 않겠다는 의미가 더 강함
for _ in range(5) :
    pass

# 딕셔너리
x, y = {"name":"홍길동", "age":20}
print(x, y) # name, age

# 해당 함수의 형식 등 세부내용 출력
help(print)

# 기본 print함수 변경
print(1, 2, 4)                      # 1 2 4
print(10, 20, 40)                   # 10 20 40
print(1, 2, 4, sep=',', end=" ")    # 1,2,4 10 20 30
print(10, 20, 30)
```

### **id(변수)**

- 변수의 **주소값**을 가져오는 함수
    
    ```python
    m = 10
    print("실제값 : ", m)    # 실제값 :  10
    print("주소값 : ", id(m))# 주소값 :  140725955053504
    
    x = 10
    print("주소값 : ", id(x))# 주소값 :  140725955053504
    ```
    

### packing

```python
'''

    * 사용

    1. unpacking
        ==> 변수, 변수2, ... = *집합형

    2. packing
        ==> 변수, *변수 = 집합형

'''

# 1. unpacking
print(*"홍길동") # 홍 길 동
print(*[10, 20, 30]) # 10 20 30
print(*(100, 200, 300)) # 100_200 300

def fun(x) :
    print(x) # 홍길동

fun("홍길동")

def fun2(x, y, z) :
    print(x, y, z) # 홍 길 동

fun2(*"홍길동")
fun2(*[10, 20, 30]) # 10 20 30
fun2(*(100, 200, 300)) # 100 200 300

# 2. packing
# 기본적으로 반드시 갯수가 일치해야 한다
x, y = (10, 20)
print(x, y) # 10 20

# 갯수가 일치하지 않으면 *가 붙은 변수에 리스트로 묶어서 반환
x, *y = (10, 20, 30, 40)
print(x, y) # 10 [20, 30, 40]

# 함수
'''
    1. 기본적으로 갯수가 반드시 일치해야 한다
'''
# ㅈ
def fun(x, *x2) :
    print(x, x2)

fun(10, 20) # 10 (20,)
fun(10, 20, 30, 40) # 10 (20, 30, 40)
fun(10, 20, 604, 3, 2, 4, 5) # Process finished with exit code 0
```

### format, *(unpacking), **(unpacking)

```python
'''
    문자열 포맷

    1. "".format(값, 값2, ...)

    2. " %s %d %f %c   " % (값, 값2, ...)

        %s = 문자열
        %d = 정수
        %f = 실수
        %c = 문자

    3.
    n = '홍길동'
    f"이름:{n}" ==> format string, 변수를 "" 안에서 사용할 떄
'''

'''
    이름 : 홍길동 나이 : 20
    이름 : 홍길동2 나이 : 30
'''

print("이름 : {} 나이 : {} ".format("홍길동", 20)) # 이름 : 홍길동 나이 : 20
print("이름 : {1} 나이 : {0} ".format("홍길동", 20)) # 이름 : 20 나이 : 홍길동 {}안에 숫자로 순서 정해줄 수 있음
print("이름 : {0} 나이 : {1} ".format("홍길동", 20)) # 이름 : 홍길동 나이 : 20
print("이름 : {0} 별명 : {0} 나이 : {1} ".format("홍길동", 20)) # 이름 : 홍길동 별명 : 홍길동 나이 : 20 데이터 중복 사용가능

# 매우 중요, 키 = 캆형태, 이 경우 {}에 숫자 대신 키값이 들어감
print("이름 : {username} 나이 : {userage} ".format(username = "홍길동", userage = 20)) # 이름 : 홍길동 나이 : 20

# *는 분해(unpacking) ==> 집합형 데이터 분해 (딕셔너리 제외)
print('홍길동') # 홍길동
print(*'홍길동')# 홍 길 동
print([10, 20 , 30]) # [10, 20, 30]
print(*[10, 20 , 30])# 10 20 30

print("이름 : {0} 나이 : {1} ".format("홍길동", 20))
print("이름 : {0} 나이 : {0} ".format(["홍길동", 20])) # 데이터가 하나로 묶여 1값이 존재하지 않음
print("이름 : {0} 나이 : {1} ".format(*["홍길동", 20])) # *로 나눠서 출력
# 출력
# 이름 : 홍길동 나이 : 20
# 이름 : ['홍길동', 20] 나이 : ['홍길동', 20]
# 이름 : 홍길동 나이 : 20

# ** 분해(unpacking) ==> 딕셔너리 분해

x = {"name" : "홍길동", "age" : 20}

print("이름 : {name} 나이 : {age}".format(**x)) # 이름 : 홍길동 나이 : 20

help("FORMATTING")

# 숫자 3개마다 ,출력
print('{:,}'.format(1234567890)) # 1,234,567,890

print("이름:%s 나이:%d 키:%f 성별:%c" % ('홍길동', 30, 175.43654, '남'))

name = 'HongKilDong'
age = 20
height = 175.43654
print('이름:{name} 나이:{age} 키:{height}') # 이름:{name} 나이:{age} 키:{height}
print(f'이름:{name} 나이:{age} 키:{height}') # 이름:HongKilDong 나이:20 키:175.43654
print(f'이름:{name} 나이:{age + 20} 키:{height}') # 이름:HongKilDong 나이:40 키:175.43654
print(f'이름:{name} 나이:{age} 키:{height} 성년이냐?{age > 18}')  # 이름:HongKilDong 나이:20 키:175.43654 성년이냐?True
print(f'이름:{name.lower()} 나이:{age} 키:{height} 성년이냐?{age > 18}') # 이름:hongkildong 나이:20 키:175.43654 성년이냐?True
```

### 논리값

True, False 이외의 값도 논리값으로 사용된다. ⇒ 자바스크립트도 동일

<aside>
💡 아래의 경우 모두다 False로 처리된다(아래 경우 제외시 True로 처리)

1. 0
2. 빈 문자열 “”
3. 빈 리스트 []
4. 빈 딕셔너리 {}
5. None
</aside>

## 문자열

### python에서의 ****************값 조회****************

- **색인(indexing)** : 값 하나 조회
    - ex) a[0] ⇒ a 리스트에 0번째 인덱스에 해당하는 값
- **슬라이싱(slicing)** : 범위지정해서 여러개
    - ex) a[1:4] ⇒ a 리스트에 1번째 인덱스부터 4번재 인덱스 전까지 값

### **numpy 제공 값 조회**

- **색인**
- **슬라이싱**
- **fancy색인 : 위치 지정해서 여러개**
    - ex) a[0, 1, 3] → a리스트에서 0번째, 1번째, 3번째 인덱스에 있는 값을 모두 가져옴

************************문자열 종류************************

- ********bytes********
    - 네트워크 이용된 문자열
    
    <aside>
    💡 웹 크롤링은 기본적으로 bytes타입 문자열을 받음
    
    </aside>
    
    - 표현 : b’hello’
- **str**
    - 일반적인 문자열
    - 유니코드 타입
        
        <aside>
        💡 유니코드란?
        전세계의 모든 언어를 표현할 수 있는 것
        
        </aside>
        
    - 표현 : ‘hello’

**str ⇒ bytes로 bytes ⇒ str로 바꿔보기**

```python
# 1. str
s = "hello한글"

# str ==> bytes
s_bytes = s.encode('utf-8')
print(s, s_bytes) #hello한글 b'hello\xed\x95\x9c\xea\xb8\x80'

# bytes ==> str
s_str = s_bytes.decode('utf-8')
print(s_str) # hello한글
```
