## 1. 재귀호출 사용하기
: 함수 안에서 함수 자기자신을 호출하는 방식
    - 알고리즘 구현에 유용

```
def hello():
    print('Hello, world!')
    hello() ## 다시 def hello()문에 넣음: print('Hello, world!') 반복

hello()
//
Hello, world!
Hello, world!
Hello, world!
... (무한출력 -> 최대 재귀 깊이(1000) 초가 -> RecursionError)
```

### 1.1 재귀호출에 종료 조건 만들기
```
def hello(count):
    if count == 0: ## 종료 조건
        return
    
    print('Hello, world!', count)

    count -= 1
    hello(count) ## 다시 def hello(count)문에 넣음 -> if ~ count -=1까지 반복

hello(5)
//
Hello, world! 5
Hello, world! 4
Hello, world! 3
Hello, world! 2
Hello, world! 1 ## count == 0이면, 출력하지 않고 종료
```

## 2. 재귀호출로 팩토리얼 구하기
: k! = k * (k-1) * (k-2) * ... * 2 * 1
```
def factorial(n):
    if n == 1: ## 종료 조건
        return 1
    return n * factorial(n-1) ## n * (n-1로 재귀호출 한 값) ## 팩토리얼 식을 사용하여 반복

print(factorical(5))
// 120 ## 1 * 2 * 3 * 4 * 5
```

![image](https://user-images.githubusercontent.com/104348646/183852326-b64fce22-85f3-4a90-b1fd-fa6f87eb1f63.png)

## 4. 연습문제: 재귀호출로 회문 판별하기
다음 소스 코드를 완성하여 문자열이 팰리드롬(회문)인지 판별하고 결과를 출력하시오.
```
# 소스 코드
practice_recursive_function_palindrome.py
def is_palindrome(word):
    ____________________________________
print(is_palindrome('hello'))  
print(is_palindrome('level'))  
```
```
# 실행 결과  
False  
True  
```
```
left = word[0]; right = word[-1]

if len(word) < 1:
    return True
if left != right: ## False인 경우를 먼저 호출
    return False
return is_palindrome(word[1,-1]) ## word에서 left, right를 뺀 값을 word로 보냄
```

## 5. 심사문제: 재귀호출로 피보나치 수 구하기
```
def fibo(n: int):
    if n == 0:
        return 0
    elif n == 1 or n == 2:
        return 1
    else: 
        return fibo(n-1)+fibo(n-2) ## 피보나치 수열: f(n) = f(n-1) + f(n-2)

print(fibo(n))
```


* 참조: 코딩도장
    - https://dojang.io/mod/page/view.php?id=2352
