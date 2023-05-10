# 1 ~ n까지의 소수 찾기 1: 재귀함수
## O(n)
### 종료 조건과 추가 변수 생성(i, tf)으로 인한 비효율성 있음

N = int(input())
prime = list(map(int, input().split()))
prime_num = 0

def is_prime(n: int, i = 2, tf = 0):
    if n < 2 or i > n: ## 종료 조건
        return
    if n % i == 0:
        if i == n:
            tf = 1
            return tf
        else:
            return ## not prime
    return is_prime(n, i+1, tf)
 
for i in range(N):
    if is_prime(prime[i]) == 1:
        prime_num += 1
        
print(prime_num)


# 소수 찾기 2: for loop
### n 이전까지 모든 수를 넣어야 하는 비효율성 있음
N = int(input())
prime = list(map(int, input().split()))
prime_num = 0

def is_prime(n: int):
    if n < 2:
        return False
    else: 
        for i in range(2, n):
            if n % i == 0:
                return False
        return True

for p in range(N):
    if is_prime(prime[p]) == True:
        prime_num += 1

print(prime_num)


# 소수 찾기 3: 제곱근
## O(n/2)
### 약수의 대칭성(16의 약수는 1, 2, 4, 8, 16)을 이용해 소수찾기 2 방법의 절반 정도만 loop를 돌림
import math

N = int(input())
prime = list(map(int, input().split()))
prime_num = 0

def is_prime(n: int):
    if n < 2:
        return False
    for i in range(2, int(math.sqrt(n))+1): ## 제곱근까지만 나누기(이전에 없으면 이후에도 없음)
        if n % i == 0:
            return False
    return True

for p in range(N):
    if is_prime(prime[p]) == True:
        prime_num += 1

print(prime_num)


# 소수 찾기 4: 제곱근 + 여러 개 수를 판별하는 경우(에라토스테네스)
## 
import math

def is_prime(n: int):
    arr = [True] * (n+1) # 특정 수가 지워졌는지 여부 판별
    arr[0] = False
    arr[1] = False ## 0 and 1 is not prime key
    
    for i in range(2, int(math.sqrt(n)+1)):
        if arr[i] == True: ## prime key
            j = 2 ## left prime key: 2(O), 4(X) -> start *2
            
            while (i * j) <= n: ## i ~ n에서
                arr[i * j] = False ## i의 배수를 지움
                j += 1
                
    return arr

arr = is_prime(50) ## 1~50 판별

for i in range(len(arr)):
    if arr[i] == True: ## prime keys
        print(i, end = ' ') ## 2 3 5 ... 43 47
