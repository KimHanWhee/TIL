Python Module
=========================
# 순열과 조합(**combination**,permutation)

### import

### from itertools import combinations

### combinations/permutations([리스트], 몇개 묶을건지!)

ex)

```
num_list = [5, 2, 8, 3]
comb = combinations(num_list, 2) #조합
perm = permutations(num_list, 2) #순열

# 조합
for i in comb :
    print(i , end='')
# 조합 출력
# (5, 2)(5, 8)(5, 3)(2, 8)(2, 3)(8, 3)
# 조합은 안에 있는 N개가 한번이라도 같이 묶였으면 출력X
# ex) (5, 2) = 출력 (2, 5) = 미출력 
# => 5와 2는 한번 같이 묶였으므로 배열 중 
# 먼저나오는 5가 먼저 출력되는 (5, 2)만 출력됨.

# 순열
for i in perm :
	  print(i , end='')

# 순열 출력
#(5, 2)(5, 8)(5, 3)(2, 5)(2, 8)(2, 3)(8, 5)(8, 2)(8, 3)(3, 5)(3, 2)(3, 8)
# 순열은 안에 숫자 N개가 같이 묶인적이 있어도 순서가 다르면 출력O
# ex) (5, 2) = 출력 (2, 5) = 출력 
# => 5와 2는 한번 같이 묶였음에도 순서가 다르므로 둘 다 출력됨!
```

# Time, Datetime

### import

### import time / import datetime

### **time**

- **time.sleep(시간(초))**
    - 이 코드를 만나면 지정한 시간(초)만큼 딜레이가 걸림
    
    ```python
    import time
    # 7단 구구단 출력
    n = 7
    for k in range(1, 10, 1) :
        print(f'{n} *{k} = {n * k}')
        time.sleep(0.2) #time.sleep을 만나서 0.2초 멈춘뒤 다음 연산 출력
    # 7 * 1 = 7 출력
    # 0.2초 정지
    # 7 * 2 = 14 출력
    # 0.2초 정지 ...
    ```
    
- **time.localtime()**
    - 현재 시간 정보를 반환해줌
    - 출력 시
    
    ```python
    time.struct_time(tm_year=2022, tm_mon=11, tm_mday=22, tm_hour=17, tm_min=29, tm_sec=23, tm_wday=1, tm_yday=326, tm_isdst=0)
    ```
    
    - time.localtme()에서의 요일
        
        <aside>
        💡 요일은 월 = 1, 화 = 2 … 토 = 5, 일 = 6 으로 반환 됨
        
        </aside>
        
    
    ```python
    tm_wday=1 # 1이므로 화요일 배열인덱스와 같아 활용하기 편함
    ```
    
    - 반환해주는 정보를 가지고 현재 날짜 , 요일 출력
    
    ```python
    import time
    
    c=time.localtime()
    
    def getDay(day):#0    1    2    3    4    5    6
        day_list = ['월','화','수','목','금','토','일'] #배열 인덱스와 같은것을 이용
        return(day_list[day]) #day = c[6] = tm_wday = 1이므로 1번 인덱스인 '화'가 반환
    
    years, month, day = c[0], c[1], c[2]
    print(f'{years}년 {month}월 {day}일 {getDay(c[6])}요일') 
    
    #출력
    # 2022년 11월 22일 화요일
    ```
