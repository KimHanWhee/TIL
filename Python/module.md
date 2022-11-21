Python Module
=========================
# 순열과 조합!!(**combination**,permutation)

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
# (5, 2)(5, 8)(5, 3)(2, 8)(2, 3)(8, 3)한
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
