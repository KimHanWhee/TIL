python review02 (2022/11/30)
============================

## 리스트의 깊은 복사, 얕은 복사

### 깊은 복사

- 실제 값 복사

```python
# 1. 1차원, 깊은 복사
a = [1, 2, 3]
b1 = a[:]
b2 = a.copy()
b3 = list(a)
print(id(a), id(b1)) # 2387468236928 2387468479296 다른 주소값을 가짐
print(id(a), id(b2)) # 2387468236928 2387468479232
print(id(a), id(b3)) # 2387468236928 2387468479808

# 값 변경, 주소값이 다르므로 a가 변경되어도 b는 값이 변경되지 않음
a[0] = 100
print(a, b1) # [100, 2, 3] [1, 2, 3]
print(a, b2) # [100, 2, 3] [1, 2, 3]
print(a, b3) # [100, 2, 3] [1, 2, 3]
```

### 얕은 복사

- 주소 값 복사

```python
# 얕은 복사
a = [1, 2, 3]
b = a
print(id(a), id(b)) # 2387468214080 2387468214080 동일한 주소값

# 값 변경, 주소값에 해당하는 값이 변경됨으로 같은 주소값을 가진 b도 변경됨
a[0] = 100
print(a, b) # [100, 2, 3] [100, 2, 3]
```

### 중첩리스트

- 중첩 리스트(2차원)는 1차원 리스트와 기능 차이가 있음

```python
# 2. 2차원
x = [1, 2, [9, 8, 7]]

# 2. 2차원, 얕은 복사 주소값 동일
y = x
print(x, y, id(x), id(y)) # [1, 2, [9, 8, 7]] [1, 2, [9, 8, 7]] 2025781587520 2025781587520

# 2. 2차원, 깊은 복사 주소값 다름
y1 = x[:]
y2 = x.copy()
y3 = list(x)
print(x, y1, id(x), id(y1)) # [1, 2, [9, 8, 7]] [1, 2, [9, 8, 7]] 2025781587520 2025781587648
print(x, y2, id(x), id(y2)) # [1, 2, [9, 8, 7]] [1, 2, [9, 8, 7]] 2025781587520 2025781587584
print(x, y3, id(x), id(y3)) # [1, 2, [9, 8, 7]] [1, 2, [9, 8, 7]] 2025781587520 2025781587712

# 중첩리스트 변경
x[2][0] = 900
print(x, y1) # [1, 2, [900, 8, 7]] [1, 2, [900, 8, 7]] 
# **주소값이 다름에도 배열 안에 있는 배열은 얕은 복사로 처리되어 값이 변경됨**

x[1] = 900 # **배열값 변경시에는 깊은 복사가 적용되어 값이 변경이 안됨**
print(x, y1) # [1, 900, [9, 8, 7]] [1, 2, [9, 8, 7]]

# 깊은 복사된 리스트안의 리스트도 깊은 복사로 처리하기
import copy
y4 = copy.deepcopy(x) # **deepcopy를 이용하여 리스트안의 리스트 값 깊은복사 적용**

x[2][0] = 900
print(x, y1, y2, y3) # [1, 2, [900, 8, 7]] [1, 2, [900, 8, 7]] [1, 2, [900, 8, 7]] [1, 2, [900, 8, 7]]

**# 깊은 복사 적용됨**
print(x, y4) # [1, 2, [900, 8, 7]] [1, 2, [9, 8, 7]]
```

## 삼항연산자

```python
# 3항 연산자

result = 100 if False else 200
print(result)

# 문제 키보드로 점수를 입력받아서 60점 이상이면 "합격" 미만이면 "불합격" 출력

total = int(input("점수 입력 >>> "))
print("합격" if total >= 60 else "불합격")

# 3항 연산자 중첩
print(("아슬아슬했네요" if total < 70 else "여유로웠네요") if total >= 60 else "불합격")

# 2중 중첩
print(("아슬아슬했네요" if total < 70 else "여유로웠네요") if total >= 60 else ("아깝네요ㅠㅠ" if total > 50 else "더 노력합시다!"))
```

## 반복문

### for문

- 반복 횟수가 예측이 가능할 때
- 용도
    - 일정 횟수만큼 반복처리
    - 집합형 data처리

```python
for _ in "AAAAA":
    print("Hello")

for _ in [1, 2, 3, 4, 5] :
    print("Hello1")

for _ in range(5) :
    print("Hello2")
```

### while문

- 반복 횟수 예측이 힘들 때
- 무한루프 적용

### 보조 제어문

**break**

- 반복문을 빠져나올 때

******continue******

- 반복적으로 실행하는 문장들 중에서 일부분 건너뛸 때
- 반복문을 빠져나가지는 않음

**********else**********

- 반복문이 어떻게 종료되었는지 알 수 있다.
- break로 끝날 시에는 else문이 실행이 되지 않는다.

```python
for i, n in enumerate(range(5)) :
    print("A", i)
    # if i == 3 : break
    print("B", i)
    print("C", i)
else:
    print("break 적용 안된 경우에 실행")
print("프로그램 종료")
```

### dict comprehension

```python
# dict comprehension

x = {"대한민국" : "서울", "영국" : '런던', "미국" : "워싱턴"}

# 국가:수도 ==> 수도:나라
x2 = {v:k for k,v in x.items()}
print(x2)

# 수도 길이가 2인 값만 반환
x3 = {v:k for k, v in x.items() if len(v) == 2}
print(x3)
```

### generator comprehension

**특징**

- 한번에 한개 씩만 생성
- 메모리에 **유지X**
- next(), for문, list()를 사용해서 하나씩 값을 얻는다
- 성능면에서는 떨어지지만 메모리 효율성에서는 뛰어나다

<aside>
💡 for문에 range가 대표적인 generate이다.

</aside>

```python
# 1. list comprehension vs generate comprehension

x = [n for n in range(5)]
x2 = (n for n in range(5))
print(x, x2) # [0, 1, 2, 3, 4] <generator object <genexpr> at 0x000001627D24F9E0>

# 2. generator 값 조회
## 가. next() 함수 사용
print(next(x2))
print(next(x2))
print(next(x2))
print(next(x2))
print(next(x2))
# print(next(x2)) # 에러 발생 ==> 5번 모두 사용했기 때문에

## 나. for문 사용
x2 = (n for n in range(5)) # 위에서 모두 사용했기 때문에 다시 선언

for k in x2:
    print(k)

## 다. list() 사용
x2 = (n for n in range(5))
result = list(x2) # 더 이상 generator객체가 아니므로 재활용이 가능하다
print(result)
```

## 함수(function)

1. **반드시 호출되어야 한다. 호출 되어 함수가 실행된 후에는 호출한 곳으로 돌아온다.**
2. **함수 호출 시 인자값(전달값)과 함수의 파라미터 변수 개수가 일치해야한다.**
    - 개수가 달라도 가능한 방법
        1. default 파라미터 
            
            인자값 보다 파라미터 개수가 더 많은 겅우
            
            ```python
            def fun2(n = 100): # default 파라미더
                print("fun", n)
            fun2() # fun 100
            fun2(999) # fun 999
            
            def fun(n = 1, n2 = 2, n3 = 3) :
                print("fun", n, n2, n3)
            
            fun() # fun 1 2 3
            fun(10) # fun 10 2 3
            fun(10,30) # 1 30 3
            ```
            
        2. packing : 파라미터보다 인자값이 더 많은 경우
            
            ```python
            def fun4(*n) : # *를 사용하여 패킹
                print(n)
            
            fun4(1) # (1,)
            fun4(1, 2, 3) # (1, 2, 3)
            fun4(1, 2, 3, 4, 5, 6) # (1, 2, 3, 4, 5, 6)
            ```
            
        3. default 파라미터 + packing
            
            ```python
            def fun5(n = 10, *n2) :
                print(n, n2)
            
            fun5(9, 8) # 9 (8,)
            fun5(9, 8, 3, 5) # 9 (8, 3, 5)
            fun5(9, 8, 6, 7, 8, 9, 8) # 9 (8, 6, 7, 8, 9, 8)
            ```
            
3. **named 파라미터**
    - 실습
        
        호출 시 변수이름을 지정해서 그 변수에 해당하는 값을 보냄
        
        ```python
        # named 파라미터
        def fun6(x, y) :
            print(x, y)
        
        fun6(5, 2) # 5 2
        fun6(y = 5, x = 2) # 2 5 변수이름을 지정해서 그 변수에 해당 값을 보냄
        ```
        
        named 파라미터 + packing
        
        호출 시 지정한 변수 값을 키값으로 한 딕셔너리로 출력
        
        ```python
        def fun7(**k) : # *한개면 튜플 두개면 딕셔너리 딕셔너리는 키, 값 두개로 저장해야되서 그런듯
            print(k)
        
        fun7(x = 5, y = 2) # {'x': 5, 'y': 2}
        fun7(x = 5, y = 2, z = 40) # {'x': 5, 'y': 2, 'z': 40}
        ```
        
        named 파라미터 + packing + default 파라미터
        
        총 혼합
        
        ```python
        def fun8(n, n2 = 1, *n3, **n4) :
            print(n, n2, n3, n4)
        
        fun8(10,30,40,4, x = 99, y = 100) # 10 30 (40, 4) {'x': 99, 'y': 100}
        ```
        
4. **return 키워드 키워드 용도**
    1. 반환값이 존재할 때
        
        ex) return 값
        
    2. 함수를 중지할 때
        
        ex_ if 조건 : return
        
    
    ```python
    def fun() :
        print("1")
    		# 1만 출력하고 return을 활용하여 함수 종료 반복문에서의 break 같은 역할
        if True : return 
        print("2")
        print("3")
    
    fun() # 1
    ```
    
5. **리턴값은 여러개 가능하다. ⇒ 튜플 형식으로 하나만 리턴하지만 튜플 내에 데이터가 여러개 있다.**
    
    ```python
    def fun2() :
        return 10, 20
    
    result = fun2()
    print(result) # (10, 20)
    
    # 하나의 값을 갖는 tuple 표현 방법은?
    print(type((10))) # <class 'int'>
    print(type((10,))) # <class 'tuple'>
    ```
    
6. **일급 객체(first-class)**
    
    함수 특징인데 **함수를 data로 처리하는** 언어의 고유한 특성
    
    <aside>
    💡 변수 = 함수명 ⇒ 함수명() 형태가 아님 함수명만 써야한다
    
    </aside>
    
    1. 함수 명으로 된 변수 생성
    2. 함수 객체 생성
    3. **함수명 = 함수위치 저장, 참조만 가능 ()를 붙이면 실행 가능**
    
    함수 x 생성 ⇒ 함수명인 x로 된 이름의 x 변수 생성 ⇒ 함수 객체 생성
    
    x에는 함수의 위치가 저장됨 x로 함수 참조 가능
    
    x()로 함수 실행가능
    
    ```python
    def fun() :
        print("fun")
    
    # 1. 함수를 변수에 저장 가능하다.
    print(fun) # <function fun at 0x00000172015EC160> 주소값 출력
    fun() # fun 0x00000172015EC160주소에 있는 객체 실행
    x = fun # fun에 있는 주소값을 x로 얕은 복사
    x() # fun x에도 0x00000172015EC160 주소값이 들어있으므로 객체 실행가능하다
    
    # 2. 함수 호출 시 전달값으로 함수를 사용 가능
    def fun2(y): # 전달 받은 y도 fun의 주소값을 가지게 된다
        y() # fun
    
    fun2(fun) # fun2 함수 호출시 fun 함수 전달
    
    # 3. 함수 호출 시 리턴값으로 함수를 사용 가능
    def fun3() :
        return fun
    result = fun3()
    result()  # result = fun3() = fun 이므로 result에 ()를 붙여야 fun()이 되어 실행할 수 있다.
    ```
    

### Filter, Map,Sort(key=)

**filter**

- filter(함수, 집합형)
- 동작 : 집합형에서 값을 꺼내서 함수를 적용한다. 이때 함수 리턴값이 True인 경우에만 값을 반환한다

******map******

- map(함수, 집합형)
- 동작 : 집합형에서 값을 꺼내서 함수를 적용한다. 함수 적용 후 적용된 결과값을 반환한다.

**sort(key=함수명)**

- key에 선언한 해당함수를 리스트에 적용시켜줌

```python
def fun(x):
    return x % 2 == 0

result = filter(fun, range(10)) # [0, 1, 2, 3, ...,9] 0부터 하나씩 fun함수로 전달됨
print(list(result))

print()
# def fun2(x) :
#     return x.lower()
result = map(str.lower, ["Abc", "EdF", "FFF"])
print(list(result))

# 문제: 리스트에 저장된 문자열의 길이를 출력하시오.
result = map(len, ["Abc", "EdFCc", "FFFLHNKDksdf"]) # len도 함수라 이렇게 적어도 길이를 잰다!!!
print(list(result))

# 문제2: 리스트에 저장된 숫자를 문자로 바꿔라
result = map(str, [87,35,77]) # 캬 이것도 되네
print(list(result))

## 정렬
k = [85, 24, 67, 11, 4, 7]
k.sort()
k.sort(reverse=True)
print(k)
print()

# A(65) a(97) 외우기

x = ['132', '32', '12', '9', '5']
x.sort()
x.sort(key=int, reverse=True) # key를 이용해서 함수 int를 적용하여 숫자 배열로 바꿈
															# revers=True를 쓰면 역순으로 정렬
print(x)

# 문제: 이름 길이 순서로 정렬
x = ['세종대왕', '정조', '김유신', '영조', '황']
x.sort(key=len) # key를 이용해서 함수 len을 적용하여 이름 길이 순서로 오름차순 정렬
print(x)
```

## python 변수 종류 VS 자바의 변수 종류

### Python의 변수 종류

- 함수 scope ⇒ 변수의 인식(사용) 범위
    
    ```python
    '''
      변수 scope
    
    '''
    
    def fun():
        m = 10  # 지역변수(로컬변수): 함수안에서만 사용 가능
        print(m)
        
    # print(m)    # error 발생
    
    print()
    
    x=10      # 전역변수(global): 전역적으로 사용 가능
    def fun2():
        y=20   # 지역변수(로컬변수): 함수안에서만 사용 가능
        print(x)
        print(y)
    
    print(x)
    # print(y) # error 발생
    ```
    
    - 중첩이 가능하다
    
    ```python
    def fun():
        pass
        def fun2():
            pass
        fun2()
    fun()
    
    k = 100
    def fun():
        m = 1
        print("fun", m)
        print("fun", k)
        def fun2():
            n = 10
            print("fun2", m)
            print("fun2", n)
            print("fun2", k)
        fun2()
        # print("fun", n) # error
    fun()
    
    def fun():
        m = 1
        print("fun", m)
        def fun2():
            m = 10
            print("fun2", m)
        fun2()
    fun()
    
    m=99
    def fun3():
        m = 1
        print("fun3", m)
        def fun4():
            # nonlocal m
            global m # global을 써서 fun3안에 있는 m이아닌 밖에있는 m을 가져온다
            print("fun4", m)
            m = 10
            print("<<<<", m) # m을 함수내에서 다시 선언
        fun4()
    fun3()
    ```
    

### Java의 변수 종류

- 블럭 scope ⇒ 블럭의 안이냐 밖이냐로 구분

## 클래스 (class)

1. ********************************OOP (Object Oriented Programming)********************************
    - 객체 지향 프로그래밍
    
    <aside>
    💡 객체 지향 프로그래밍이란?
    객체(Object)를 사용해서 프로그래밍을 하는 방법론
    
    </aside>
    
2. ********객체(Object)란?********
    
    현실 세계에 존재하는 사물(물건)  ex) 컴퓨터, 책상, 의자,…
    
    - **객체 구성요소**
        - 속성 ⇒ 변수
        - 기능(동작) ⇒ 메서드
    
    **************모델링(modeling) ⇒ 추상화 작업**************
    
    필요한 속성이나, 기능을 선점
    
3. **클래스**
    
    객체를 생성하기 위한 일종의 설계도 (현실 세계 객체 ⇒ 가상, 프로그래밍 세계의 클래스)
    
    ****************class 문법****************
    
    class 클래스명
    
    - 생성자
        - 변수의 값을 초기화 하는 역할(변수 초기화)
    - **변수**(멤버 변수, 인스턴스 변수)
        - 객체의 속성(data)을 저장하는 용도
    - 메서드(멤버 메서드, 인스턴스 메서드, 레귤러 메서드)
        - 변수값 변경, 조회 등 변수를 활용하는 역할
4. **클래스 사용**
    
    <aside>
    💡 ⇒ 반드시 **클래스 생성** 부터 해야한다. (객체 생성)
         * 클래스 생성 ⇒ 메모리에 올리는 작업
    
    ⇒ 변수명 = 클래스명()
    
    </aside>
    
    ![image](https://user-images.githubusercontent.com/84313936/204997927-0886b5eb-564c-44d6-b558-29ec4f7fbd25.png)
    
    - 클래스를 **외부**에서 참조
        - s.변수, student().변수
5. **인스턴스**
    
    객체를 소프트웨어에 실체화 하면 그것을 **인스턴스**라고 부른다
    
    클래스로부터 객체를 선언하는 과정을 클래스의 **인스턴스화**라고 한다
    
6. **************클래스 내부**************
    - ********************클래스 변수********************
        - 임의의 메모리 (method area)
        - 프로그램 실행할 때 한번 만 생성
            - 객체 생성과는 무관하게 **클래스명.변수**로 접근가능하다.
            
            ```python
            class Student:
                # 클래스 변수, method area 메모리
                num = 0
                def __init__(self, age): # age는 로컬변수 stack 메모리
                    self.age = age       # self.age는 인스턴스 변수 heap 메모리
                    Student.num += 1 # 클래스 내부에서도 클래스명.변수 형태로 선언 해야함
            
            print(Student.num) # 0 객체생성과 무관 언제나 접근가능
            s = Student(10)
            print(Student.num) # 1
            s = Student(10)
            print(Student.num) # 2
            s = Student(10)
            print(Student.num) # 3 다른 객체 생성이 되어도 클래스변수는 공유가 된다
            ```
            
        - 프로그램 종료 시 삭제
        - 누적용으로 사용
    - **생성자(__init__) :** 객체가 생성될 때 호출되는 생성자, 호출될 때 생성된다.
        
        ```python
        class Student:
        		# 생성자 선언법
            def __init__(self):  # 생성자, 선언한 Student()가 아닌 __init__이라는 이름의 함수가 호출됨
                pass
        
        s = Student()  # 객체 생성(인스턴스화), Student() = 생성자 호출
        ```
        
    - ********************************************************로컬변수********************************************************
        - 함수 안에서 생성되는 변수
        - 호출 시 생성
        - stack 에 저장됨
        - 함수 종료 시 삭제
    - **인스턴스 변수(self.변수)**
        - heap에 저장됨
        - 객체 생성 시 매번 생성
        - 객체 소멸 시(인스턴스를 아무도 참조하지 않을 때) 삭제
            
            <aside>
            💡 **객체 소멸은 언제 될까?**
            
            예를 들어 s = student() ⇒ 100번지 라고 치자 
            그런데 이 이후에 s = student() ⇒ 200번지 가 한번 더 정의된 경우에는 100번지가 소멸된다.
            
            </aside>
            
        
        ```python
        class Student:
            def __init__(self, username, age):  # 생성자 name, age ==> 지역변수(로컬변수), stack
                self.username = username # 인스턴스 변수, 멤버 변수, heap, 저장위치가 다르므로 변수이름을 똑같이 맞춰도 된다
                self.userage = age   # 인스턴스 변수, 멤버 변수, heap
        
        s = Student("홍길동", 20) # 객체 생성(인스턴스화)
        print("이름:{} 나이:{}".format(s.username, s.userage)) # 이름:홍길동 나이:20
        ```
        
    - **self : 클래스 내에서 자기 자신을 호출하는 역할**
        - 밑 코드의 경우에는 self와 s 둘 다 Student()의 주소값을 가지고 있다.
            
            ```python
            class Student:
                def __init__(self, username, age):  # 생성자
                    self.username = username # 인스턴스 변수
                    self.userage = age   # 인스턴스 변수
                    print("self:", id(self)) # self: 2855588354416, s1에서 호출시 self: 2005304011264
            
            s = Student("홍길동", 20) # 객체 생성(인스턴스화)
            print("s:", id(s)) # s: 2855588354416
            
            print()
            
            s1 = Student("이순신", 33) # 객체 생성(인스턴스화)
            print("이름:{} 나이:{}".format(s1.username, s1.userage))
            print(id(s1)) # 2005304011264
            ```
            
    - ********************************************************************************멤버 메서드를 사용하여 인스턴스 변수 다뤄보기********************************************************************************
        
        ```python
        class Student:
            def __init__(self, username, age):  # 생성자
                self.username = username # 인스턴스 변수
                self.userage = age   # 인스턴스 변수
                print("self:", id(self)) #
        
            def set_username(self, username): # 멤버 메서드
                self.username = username
        
            def get_username(self): # username을 반환하는 멤버 메서드
                return self.username
        
            def set_userage(self, userage):
                self.userage = userage
        
            def get_userage(self):
                return self.userage
        
        s = Student("홍길동", 20) # 객체 생성(인스턴스화)
        print("이름:{} 나이:{}".format(s.username, s.userage)) # 이름:홍길동 나이:20
        print("이름:{} 나이:{}".format(s.get_username(), s.userage)) # username을 리턴하는 메서드를 만들어서 이름 출력
        
        # 이름 변경
        s.set_username("이순신")
        print("이름:{} 나이:{}".format(s.username, s.userage)) # 이름:이순신 나이:20
        
        # 나이 변경
        s.set_userage(50)
        print("이름:{} 나이:{}".format(s.username, s.userage))
        print("이름:{} 나이:{}".format(s.username, s.get_userage()))
        ```
        
    - **********************************클래스 메서드**********************************
        - 인스턴스 접근 불가 (클래스가 더 먼저 만들어져서 늦게 만들어진 인스턴스에 접근할 수 없다, 반대로 인스턴스는 클래스에 접근 가능하다.)
        - 객체 생성과 무관하다(인스턴스 메서드는 반드시 객체 생성이 되야함)
        - 자바에서는 어노테이션, 파이썬 에서는 decorator라고 불린다.
        
        ```python
        class Student:
            # 클래스 변수, method area 메모리
            num = 0
            def __init__(self, age): # age는 로컬변수 stack 메모리
                self.age = age       # self.age는 인스턴스 변수 heap 메모리
                Student.num += 1
        
            # 인스턴스 메서드
            def get_age(self):
                return self.age
        
            # 클래스 메서드
            @classmethod
            def get_num(cls):
                print("cls : ", id(cls)) # cls :  2124456473392
                # return Student.num
        				# id 값이 cls == Student이므로 클래스 메서드 내에서는 Student대신 cls를 쓴다.
                return cls.num
        
        print(Student.num)
        print(Student.get_num())
        print("Student", id(Student)) # Student 2124456473392
        ```
        
    
    ## 상속(inhertance)
    
    - **재사용** 성이 좋다
    
    예) 애완동물 관리 프로그램
    
    강아지
    
    - 속성 (변수)
        - **name**, species, **age**…
    - 기능 (메서드)
        - **cry()**, eat(), **sleep()**…
    
    고양이
    
    - 속성 (변수)
        - **name**, sex, **age**
    - 기능 (메서드)
        - **cry()**, **sleep()**…
    
    ```python
    # 1. 상속전 코드  ==> 각 개체마다 중복코드가 많다.
    
    class Dog:
        def __init__(self, name, age, species):
            self.name = name
            self.age = age
            self.species = species
    
        def cry(self):
            print("Dog.멍멍")
    
        def swim(self):
            print("Dog.swim")
    
    class Cat:
        def __init__(self, name, age, sex):
            self.name = name
            self.age = age
            self.sex = sex
    
        def cry(self):
            print("Cat.야옹")
    
        def run(self):
            print("Cat.run")
    
    c = Cat("야옹이", 2, "암컷")
    d = Dog("망치", 1, "불독")
    print("고양이, 이름:{} 나이:{} 성별:{}".format(c.name, c.age, c.sex)) #고양이, 이름:야옹이 나이:2 성별:암컷
    c.cry() # Cat.야옹
    c.run() # Cat.run
    print("강아지, 이름:{} 나이:{} 종:{}".format(d.name, d.age, d.species)) # 강아지, 이름:망치 나이:1 종:불독
    d.cry() # Dog.멍멍
    d.swim() # Dog.swim
    ```
    
    위에 표시한 것 처럼 중복된 속성이나 기능이 많을 경우 상속을 사용하면 된다
    
    ```python
    # 2. 상속후 코드
    
    class Pet:
        def __init__(self, name, age):
            self.name = name
            self.age = age
    
        def cry(self):
            print(f"{self.name}.cry")
    
    class Dog(Pet):  # 상속 문법 => 자식 클래스명(부모 클래스명)
        def __init__(self, name, age, species):
            super().__init__(name, age) # super()을 이용하여 부모 클래스에 변수 넘김
            self.species = species
    
        def swim(self):
            print("Dog.swim")
    
    class Cat(Pet):
        def __init__(self, name, age, sex):
            super().__init__(name, age)
            self.sex = sex
    
        def run(self):
            print("Cat.run")
    
    c = Cat("야옹이", 2, "암컷")
    d = Dog("망치", 1, "불독")
    print("고양이, 이름:{} 나이:{} 성별:{}".format(c.name, c.age, c.sex)) #고양이, 이름:야옹이 나이:2 성별:암컷
    c.cry() # Cat.야옹
    c.run() # Cat.run
    print("강아지, 이름:{} 나이:{} 종:{}".format(d.name, d.age, d.species)) # 강아지, 이름:망치 나이:1 종:불독
    d.cry() # Dog.멍멍
    d.swim() # Dog.swim
    ```
    
    **오버라이딩(Overriding)**
    
    부모 클래스에서 자식클래스로 전달된 기능 메서드를 자식 클래스에서 재정의 할수있다
    
    ```python
    # 2. 상속후 코드
    
    class Pet:
        def __init__(self, name, age):
            self.name = name
            self.age = age
    
        def cry(self):
            print("Pet.cry")
    
    class Dog(Pet):
        def __init__(self, name, age, species):
            super().__init__(name, age)
            self.species = species
    
        def swim(self):
            print("Dog.swim")
    
        **# 오버라이딩 메서드 부모에서 주어진 함수를 자식이 재정의**
        def cry(self):
            print("Dog.멍멍")
    
    class Cat(Pet):
        def __init__(self, name, age, sex):
            super().__init__(name, age)
            self.sex = sex
    
        def run(self):
            print("Cat.run")
    
        **# 오버라이딩 메서드 메서드 부모에서 주어진 함수를 자식이 재정의**
        def cry(self):
            print("Cat.야옹")
    
    c = Cat("야옹이", 2, "암컷")
    d = Dog("망치", 1, "불독")
    print("고양이, 이름:{} 나이:{} 성별:{}".format(c.name, c.age, c.sex)) 
    c.cry() # Cat.야옹
    c.run() # Cat.run
    print("강아지, 이름:{} 나이:{} 종:{}".format(d.name, d.age, d.species)) # 강아지, 이름:망치 나이:1 종:불독
    d.cry() # Dog.멍멍
    d.swim() # Dog.swim
    ```
    

## 모듈(module)과 패키지(package)

### **모듈**

- 하나의 파일 의미
- 모듈은 모듈에 접근할 수 없다
    - **import** 로 해결가능
        - module1.py
            
            ```python
            # module1.pu
            
            num = 2
            
            def fun() :
                print("module.fun")
            
            class Cat:
                pass
            ```
            
        - sample1.py
            - import 패키지명. 모듈명
            
            ```python
            # sample1.py ==> module1.py 접근
            
            import sample_package.module1
            
            # 관례적으로 다음 코드를 지정해서 시작점을 알려준다
            if __name__ == "__main__": # 자바로 치면 public void static main
                print(sample_package.module1.num)
                sample_package.module1.fun()
                c = sample_package.module1.Cat()
            ```
            
        - from 패키지명 import 모듈명
            
            ```python
            # sample1.py ==> module1.py 접근
            
            from sample_package import module1
            
            # 관례적으로 다음 코드를 지정해서 시작점을 알려준다
            if __name__ == "__main__":
                print(module1.num)
                module1.fun()
                c = module1.Cat()
            ```
            
        - 동시에 두개 모듈 참조
            
            ```python
            # sample1.py ==> module1.py, module2.py 접근
            
            '''
                경로 지정방법
            
                1. import 패키지명.모듈명
                2. from 패키지명 import 모듈명
            '''
            
            # from sample_package import module1
            # from sample_package import module2
            from sample_package import module1, module2
            
            # 관례적으로 다음 코드를 지정해서 시작점을 알려준다
            if __name__ == "__main__":
                print(module1.num)
                module1.fun()
                c = module1.Cat()
            
                print(module2.num)
                module2.fun2()
                c = module2.Dog()
            ```
            
        - from 패키지명, 모듈 import 멤버 ⇒ 가독성 떨어짐 (비권장)
            
            ```python
            # from sample_package import module1
            # from sample_package import module2
            
            from sample_package.module1 import num, fun, Cat
            
            # 관례적으로 다음 코드를 지정해서 시작점을 알려준다
            if __name__ == "__main__":
                print(num)
                fun()
                c = Cat()
            ```
            

### **패키지**

- 서로 관련된 모듈의 묶음(폴더, 디렉토리)

## 예외 처리 (exception handling)

### 예외 (exception)

- 프로그램 실행중에 발생되는 오류 의미 (일반적으로 에러라고 부름)
- 가장 큰 문제는 비정상 종료 됨

### 예외 처리

- 예외가 발생되도 끝까지 실행하도록 처리
- 예외 발생 코드를 수정하는 것은 불가능
- 정상 종료 + 예외 정보를 알려주는 역할을 한다

**예외 처리 방법**

- 예외 클래스 이용
    
    ```python
    '''
        예외 클래스 제공(상속 관계)
    '''
    
    print(AssertionError.mro()) # 클래스명.mro(), 해당 클래스에 계층 구조를 보는 방법
    # 출력 [<class 'AssertionError'>, <class 'Exception'>, <class 'BaseException'>, <class 'object'>]
    help(__builtins__) # 클래스 구조 확인
    # CLASSES
    #     object
    #         BaseException
    #             Exception
    #                 ArithmeticError
    #                     FloatingPointError
    ```
    
- try:except 사용
    
    ```python
    print("start")
    
    # 예외처리
    try:
        num = 0
        result = 10 / num
        print("결과값 : ", result)
    except ZeroDivisionError as e : # 여기서 지정한 zeroDivisionError는 ArithmeticError
    											   				# 와 같은 부모클래스로도 잡아낼 수 있다 자식클래스는 불가
        print("0으로 나눌 수 없습니다!", e)
    
    print("end - 정상종료")
    ```
    
- 다중 except 사용
    
    ```python
    try : 
    except ZeroDivisionError as e :  # 이런식으로 여러줄에 걸쳐 다중 exception 사용가능
    	pass
    except OverflowError as e :
    	pass
    except Exception as e : # 위에 지정한 예외가 아닌 예측 못한 에러일 경우 여기서 잡을 수 있음
    	pass
    ```
    
- finally문
    - 예외 발생 여부와 상관없이 반드시 실행되는 문장
    - except없이 try와 finally만 사용되는 경우는 예외 처리 목적이 아닌 반드시 실행 되어야 하는 문장을 알려주는 경우이다.
