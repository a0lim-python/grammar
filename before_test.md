## 문자열(str)
* 입력 받기
  - input()
  ```
  a = input()
  a = int(input())
  a, b = map(int, input().split())
  a = list(map(int, input().split()))
  ```
  
  - sys.stdin.readline(): 반복 입력이 많은 경우, 시간 단축  
    : input()과 결과 같음. 단, 개행문자(\n)이 같이 입력 받아짐
  ```
  import sys
  for i in range(1000000):
    a = int(sys.stdin.readline()) // 0 ## 숫자는 int() 등으로 개행문자를 제거 cf) sys.stdin.readline() = '0\n'
    
  ## 값을 저장
  data = [sys.stdin.readline().strip() for i in range(1000000)] ## strip(): 문자열의 앞과 끝의 공백 문자를 제거
  ```

* 문자열 좌우 정렬
```
* ljust, center, rjust
s = ‘abcd’
n = 7
s.ljust(n) ## 왼쪽 정렬 // 'abcd   '
s.center(n) ## 가운데 정렬 '  abcd '
s.rjust(n) ## 오른쪽 정렬 // '   abcd'
```

* 문자열을 하나씩 나누어 리스트로 정리하기
```
a = '12345'
list(a) // ['1', '2', '3', '4', '5']
```

* 문자열 정렬(뒤집기)
  - array, list, tuple도 가능
  - [::-1]
```
a = '734 893'
a[::-1] // '398 437'
a[2:0:-1] // '437' ## a[0:2]인 '734'을 역순으로 뒤집기
```

* 단어 변환
  - replace
```
a = 'abc'
a = a.replace('a', '*')
print(a) ## '*bc'
```

* 변수 내의 위치 찾기
  - find
  ```
  a = 'abcd'
  a.find('a') // 0
  a.find('z') // -1
  ```
  - index
  ```
  a.index('a') // 0
  a.index('z') // ERROR
  ```

* 단어 삭제
  - remove: 값으로 삭제
  ```
  a = [1, 2, 1, 2, 3]
  a.remove(2)
  a // [1, 1, 2, 3] ## 처음 나오는 2를 삭제
  a.remove(5) // ValueError ## 없는 값을 삭제하는 경우 Error
  ```
  - del: 인덱스로 삭제
  ```
  a = [1, 2, 1, 2, 3]
  del a[3]
  a // [1, 2, 1, 3] ## a[3]을 삭제
  del a[7] // IndexError ## 없는 위치의 값을 삭제하는 경우 Error
  ```

* 대소문자 변환
```
a = 'abc'
a.upper() // 'ABC'
a.lower() // 'abc'
```

* import string
```
string.ascii_lowercase ## 소문자 // abcdefghijklmnopqrstuvwxyz
string.ascii_uppercase ## 대문자 // ABCDEFGHIJKLMNOPQRSTUVWXYZ
string.ascii_letters ## 대소문자 모두 // abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
string.digits ## 숫자 //0123456789
```

* 순열과 조합
```
import itertools
arr = ['A', 'B', 'C']

# 순열

itertools.permutations(arr, 2) ## arr 리스트 내에서 2개를 선택하여 나열하는 경우의 수
// 결과 : [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]

# 조합

itertools.combinations(arr, 2) ## arr 리스트 내에서 2개를 선택하는 경우의 수
// [('A', 'B'), ('A', 'C'), ('B', 'C')]
```

## 숫자형(int, float, ...)

* divmode
```
divmode(10, 3) ## 몫, 나머지 // (3, 1)
```

* 올림/반올림/내림
  - math.ceil(올림)
  ```
  import math
  
  math.ceil(31.415) // 32
  ```
  - round(반올림)
  ```
  round(31.415) // 32
  round(31.415, 2) // 31.42 ## 숫자를 소숫점 2째 자리까지 반올림
  round(31.415, -1) // 31.415 ## 숫자를 십 단위까지 반올림
  ```
  - math.floor, math.trunc(내림)
  ```
  import math
  
  math.floor(31.415) // 31
  math.floor(-31.415) // -32
  
  math.trunc(-31.415) // -31 ## 0을 향해 내림
  ```
* 정렬
  - 문자열도 가능(알파벳 순서)
  - sort: 원본을 변경
  ```
  ## 기본
  a = [1,5,3,4,2]
  a.sort() ## 오름차순 // [1,2,3,4,5]
  a.sort(reverse = True) ## 내림차순 // [5,4,3,2,1]
  
  ## sort + lambda
  b = [[1,2], [7,4], [7,1]]
  b.sort(key = lambda x: x[1]) ## 리스트 내에서 두번째 원소를 기준으로 오름차순 정렬 // [[7,1], [1,2], [7,4]]
  b.sort(key = lambda x: (-x[0], x[1])) ## 리스트 내에서 첫번째 원소를 기준으로 내림차순 -> 두번째 원소를 기준으로 오름차순 정렬 // [[7,1], [7,4], [1,2]]
  
  ### 숫자, 문자 혼합 + 문자열 원소를 내립차순으로 정렬하는 경우
  b = [[20, 'S'], [21, 'J'], [21, 'D']]
  b.sort(key = lambda x: (x[0], -x[1])) // TypeError: bad operand type for unary -: 'str'
  b.sort(key = lambda x: (-int(x[0]), x[1], reverse = True)) ## 숫자형 원소에 int() 변환 + 오름차순/내림차순 반대로 + reverse = True
  ```
  
  - sorted: 원본은 유지, 새 리스트 생성
  ```
  a = [1,5,3,4,2]
  b = sorted(a) // [1,2,3,4,5]
  a // [1,5,3,4,2]
  ```
* 숫자(문자열) 앞에 0 채우기
  - zfill
```
a = '1'
a.zfill(2) // '01'
```

* % 표현으로 변환
```
* 0.f%%: 소수점 없이 정수처럼 표시
print( "%0.f%%" % 40) // 40%

* 0.2f%%, 0.3f%% 등, 사용하고 싶은 소수점 자리까지 표시
print( "%0.2f%%" % 40) // 40.00%
```

* 진법
  - n진법 -> 10진법
  ```
  * int(num, base = n) ## n진법으로 적힌 문자열 num을 10진법으로 변환
  ```
  - 10진법 -> 2, 8, 16진법
  ```
  print(bin(10)) ## 숫자 10을 2진수로 변환 // 'Ob1010'
  print(oct(10)) ## 숫자 10을 8진수로 변환 // 'Oo12'
  print(hex(10)) ## 숫자 10을 16진수로 변환 // 'Oxa'
  
  print(bin(10)[2:] ## 진법 표시 제거 // '1010'
  ```
  - 10진법 -> n진법(n != 2, 8, 16)
    ```
    ## 1
    import string

    tmp = string.digits + string.ascii_lowercase ## 소문자 포함 -> 16진법 이상도 가능
    def convert(num, base) :
        q, r = divmod(num, base) ## q: 몫, r: 나머지
        if q == 0 :
            return tmp[r] 
        else :
            return convert(q, base) + tmp[r]

    print(convert(10,3)) ## 10을 3진법으로 변환 // '101'

    ## 2
    def solution(num):
        tmp = ''
        while num:
            tmp += str(n % n)
            num = num // n
        return tmp[::-1]
    ```
  - n진법 -> m진법: n진법 -> 10진법 -> m진법
    ```
    ## 위의 함수와 동일
    print(convert(int('4', base = 5), 3)) ## 5진법으로 표현된 '4'를 10진수로 변환 & 10진수를 3진법으로 변환
    ```

* 최대 공약수, 최소공배수
  - 유클리드 호제법
    ```
    def gcd(a, b): ## a, b의 최대공약수
        while b > 0:
            a, b = b, a % b
        return a

    def lcm(a, b): ## a, b의 최소공배수
        return a * b / gcd(a, b)
    ```

----------------------
## 리스트(list)

* 요소 추가
  - append  
    : x 자체를 추가  
      + list의 경우, list 자체를 형태 변환 없이 추가
  ```
  a = [1, 2, 3]
  a.append(4) // a = [1, 2, 3, 4]
  a.append([9]) // a= [1, 2, 3, [9]]
  ```
  
  - 슬라이싱
  ```
  a[len(a):len(a)] = [5, 5] // a = [1, 2, 3, 5, 5]
  ```
  
  - extend  
    : 리스트의 요소를 추가  
  ```
  a.extend([5, 5] // a = [1, 2, 3, 5, 5]
  cf) a.append([5, 5] // a = [1, 2, 3, [5, 5]]
  ```
* 리스트 반복
  - ```*```
  ```
  a * 2 // [1, 2, 3, 1, 2, 3]
  ```
  
* 리스트 결합
  - ```+```
  ```
  a = [1, 2, 3]
  b = [4, 5, 6]
  a + b // [1, 2, 3, 4, 5, 6]
  ```

* 리스트 뒤집기
   - reverse()
```
a = '734 893'
a = list(a) // ['7', '3', '4', ' ', '8', '9', '3'] // 변수 지정 필요
a.reverse // ['3', '9', '8', ' ', '4', '3', '7'] ## 변수 변환 필요 없음
result = '.'join(a) // '398 437'
```

* 리스트를 공백으로 구분해 출력
  - 문자
  ```
  a = ['1', '2', '3', '4']
  ' '.join(a) // 1 2 3 4 ## ''안에 구분자 입력
  ```
  - 숫자
  ```
  1. 문자형으로 변환 후 출력 -> 공백 출력은 문자/숫자 구분이 없음
  2. end = ' '
  a = [1, 2, 3, 4]
  for i in a:
      print(i, end = ' ') ## ''안에 구분자 입력
  print()
  ```

* 두 리스트에서 같은 위치의 원소간의 집합/연산
  - zip
```
mylist = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
new_list = list(map(list, zip(*mylist))) // [[1,4,7],[2,5,8],[3,6,9]]
```
```
## 여러 개의 Iterable 동시에 순회할 때 사용

list1 = [1,2,3,4]
list2 = [100,120,30,300]
list3 = [392,2,33,1]
answer = []

for num1, num2, num3 in zip(list1, list2, list3):
    print(num1+num2+num3)
// 493
// 124
// 66
// 305
```
```
## key 리스트와 value 리스트로 딕셔너리 생성하기

animals = ['cat', 'dog', 'lion']
sounds = ['meow', 'woof', 'roar']
answer = dict(zip(animals, sounds)) // {'cat': 'meow', 'dog': 'woof', 'lion': 'roar'}
```
```
## i번째 원소와 i+1번째 원소의 차를 출력하기

def solution(mylist):
    answer = []
    for number1, number2 in zip(mylist, mylist[1:]): ## mylist의 2번째 원소부터 시작하는 리스트를 이용하여 차를 구함
        answer.append(abs(number1 - number2)) ## abs: 절댓값으로 변환
    return answer

if __name__ == '__main__': ## 메인 함수(solution)의 선언, 시작
    mylist = [83, 48, 13, 4, 71, 11]    
    print(solution(mylist))
```

## 딕셔너리(dictionary)

* collections

    - defaultdict  
        : 존재하지 않는 키를 조회할 경우, 에러 메시지를 출력하는 대신 디폴트 값으로 해당 키에 대한 딕셔너리 아이템을 생성
    ```
    a = collections.defaultdict(int)
    a['A'] = 5
    a['B'] = 4
    a // defaultdict(<class 'int'>, {'A':5, 'B':4})

        -- 존재하지 않는 키인 C를 생성(기존: KeyError)
    a['C'] += 1 // defaultdict(<class 'int'>, {'A':5, 'B':4, 'C':1})
    ```

    - Counter  
        : 아이템에 대한 개수를 계산해 딕셔너리로 리턴
    ```
    a = [1,2,3,4,5,5,5,6,6]
    b = collections.Counter(a)
    b // Counter({5:3, 6:2, 1:1, 2:1, 3:1, 4:1})

    type(b) // <class 'collections.Counter'>

        -- 가장 빈도 수가 높은 요소 추출
    b.most_common(2) // [(5,3), (6,2)]
    ```

    - OrderdDict  
        : 입력 순서 유지(버전 3.7: 자동 / 3.6 이하: 유지 설정필요)
    ```
    collections.OrderDict({'banana':3, 'apple':4, 'pear':1, 'orange':2})
    // OrderDict({'banana':3, 'apple':4, 'pear':1, 'orange':2}) 로 순서 유지
    ```

## 튜플(tuple)

* tuple 형태의 반복구문
  - enumerate: (index, value)
```
t = [1,5,7,33,39,52]
for i in enumerate(t):
  print(i)
  
//
{0, 1)
(1, 5)
(2, 7)
(3, 33)
(4, 39)
(5, 52)
```

## 이중 리스트(double list)

* 이중 리스트 만들기
  - append
  ```
  a = [1, 2, 3]; b = [4, 5, 6]
  a.append(b) // a = [[1, 2, 3], [4, 5, 6]]
  a.append(b) // a = [1, 2, 3, [4, 5, 6], [4, 5, 6]]
  ```

  - ```+```
  ```
  a = [1, 2, 3]; b = [4, 5, 6]
  [a] + [b] // a = [[1, 2, 3], [4, 5, 6]]
  [a] + [b] + [b] // a = [[1, 2, 3], [4, 5, 6], [4, 5, 6]]
  ```

* 이중 리스트 내에서의 zip(unzip)
```
board = [[0,0,0,0,0],[0,0,1,0,3],[0,2,5,0,1],[4,2,4,4,2],[3,5,1,3,1]]
list(zip(*board)) // [(0, 0, 0, 4, 3), (0, 0, 2, 2, 5), (0, 1, 5, 4, 1), (0, 0, 0, 4, 3), (0, 3, 1, 2, 1)]
list(map(list,(zip(*board)))) ## 리스트 내부의 tuple을 list형식으로 변환 // [[0, 0, 0, 4, 3], [0, 0, 2, 2, 5], [0, 1, 5, 4, 1], [0, 0, 0, 4, 3], [0, 3, 1, 2, 1]]
```

* 연결 리스트 구현
  - 노드 구현: 각 노드는 value(val)와 다음 노드의 값(next)를 가짐 -> 위치 정보
```
class ListNode:
  def __init__(self, val = 0, next = None):
    self.val = val
    self.next = next
```
  - 연결 리스트 구현
```
  -- 재귀함수(my_function) 생성: solution 클래스에 저장
class solution:
  def my_function(self, l1: ListNode, l2: ListNode) -> ListNode: ## ListNode: 위의 ListNode 클래스를 사용(연결 리스트의 노드에 해당)
  rev = None
    if l1.val > l2.val:
      rev.append(l1.val)
    else:
      rev.append(l2.val)
    return

  -- l1 연결 리스트 생성
list1 = ListNode(1) ## val = 1
list2 = ListNode(2) ## val = 2
list3 = ListNode(4) ## val = 4
l1 = list1 ## l1 연결 리스트의 초기 값: list1 -> 1
list1.next = list2 ## 1의 다음 값은 list2(-> 2) => 1->2
list2.next = list3 ## 2의 다음 값은 list3(-> 4) => 1->2->4

  -- l2 연결 리스트 생성
list4 = ListNode(1) ## val = 1
list5 = ListNode(3) ## val = 3
list6 = ListNode(4) ## val = 4
l2 = list4 ## l1 연결 리스트의 초기 값: list4 -> 1
list4.next = list5 ## 1의 다음 값은 list5(-> 3) => 1->3
list5.next = list6 ## 5의 다음 값은 list6(-> 5) => 1->3->5

  -- 구현
head = my_function(l1, l2) ## my_function 실행
while head: ## 연결 리스트의 처음부터 마지막까지 반복
  print(head.val, end="") ## 첫번째 val을 출력
  if head.next:
    print("->", end="") ## 이후 "->"를 출력
  head = head.next ## head를 다음 값으로 지정
//
1->3->4
```

## 정규표현식
![image](https://user-images.githubusercontent.com/104348646/189825638-cc1bda2d-b8e8-4b73-ac4b-420d3c8e4a1b.png)

* 메타 문자(meta characters)
    ```
    . ^ $ * + ? { } [ ] \ | ( )
    \A \Z \b \B
    ```
    - ```[ ]```
        + ```[ ]``` 사이의 문자들과 매치
    ```
    front = 'abc'; back = 'xyz'
    [a] ## front는 매치, back은 'a'가 없으므로 매치 불가
    [a-z] ## 소문자 알파벳 모두
    [a-zA-Z] ## 알파벳 모두
    [0-9] ## 숫자
    ```
    ```
    \d - 숫자와 매치, [0-9]와 동일한 표현식이다.
    \D - 숫자가 아닌 것과 매치, [^0-9]와 동일한 표현식이다.
    \s - whitespace 문자와 매치, [ \t\n\r\f\v]와 동일한 표현식이다. 맨 앞의 빈 칸은 공백문자(space)를 의미한다.
    \S - whitespace 문자가 아닌 것과 매치, [^ \t\n\r\f\v]와 동일한 표현식이다.
    \w - 문자+숫자(alphanumeric)와 매치, [a-zA-Z0-9_]와 동일한 표현식이다.
    \W - 문자+숫자(alphanumeric)가 아닌 문자와 매치, [^a-zA-Z0-9_]와 동일한 표현식이다.
    ```

    - ```.```(dot)
        + \n을 제외한 모든 문자에 매치
    ```
    a.b ## a + 모든 문자 + b ## 매치: aab, a0b / 매치 불가: abc(a, b 사이에 문자 없음)
    a[.]b ## 매치: a.b / 매치 불가: a0b 등
    ```

    - ```*```
        + 반복: ```*``` 바로 앞에 있는 문자를 반복 가능(0 ~ inf번)
    ```
    ca*t ## c + a(0번 이상 반복) + t ## 매치: ct, cat, caaaaat
    ```

    - ```+```
        + 반복: ```+``` 바로 앞에 있는 문자를 반복 가능(1 ~ inf번)
    ```
    ca+t ## c + a(1번 이상 반복) + t ## 매치: cat, caaaaat ## 매치 불가: ct
    ```

    - {m, n}
        + 반복: 바로 앞에 있는 문자를 반복 가능(m ~ n번)
    ```
    ca{2}t ## c + a(2번만 반복) + t ## 매치: caat / 매치 불가: cat
    ca{2,5}t ## c + a(2 ~ 5번 반복) + t ## 매치: caat, caaat / 매치 불가: cat
    ```

    - ```?```
        + 반복: 있어도 되고 없어도 됨 (= {0, 1})
    ```
    ca?t ## c + a(0 ~ 1번 반복) + t ## 매치: ct, cat ## 매치 불가: caat
    ```

    - ```[^]```
        + ```^``` 바로 뒤에 있는 문자들의 집합이 없어야 매치
    ```
    [^abc] ## 매치: xyz / 매치 불가: abc, axyz
    ```

    - ```|```
        + 또는(or)
    ```
    a|b ## 매치: a, b
    ```

    - \d
        + 숫자를 의미
    - \w
        + 문자를 의미
    - \s
        + 스페이스(공백)을 의미
    ```
    \d\d\d ## 숫자가 3개 ## 매치: 000, 975
    \w\w\w ## 문자가 3개 ## 매치: abc, bse
    \s\s\s ## 스페이스가 3개 ## 매치: '   '
    ```

    - ```( )```
        + 그루핑: 특정 문자열이 계속해서 반복하는지 조사
    ```
    (ABC)+ ### ABC의 반복
    ```

    - ```^```
        + 문자열의 맨 처음

    - ```$```
        + 문자열의 맨 마지막

    - \A
        + 문자열의 맨 처음
        + re.MULTILINE 옵션을 사용하는 경우, 줄과 상관 없이 전체 문자열의 처음과만 매치

    - \Z
        + 문자열의 맨 마지막
        + re.MULTILINE 옵션을 사용하는 경우, 줄과 상관 없이 전체 문자열의 마지막과만 매치

* re 
    - sub
    ```
    import re
    
    a = 'gidfiemhs'
    a.sub('e', '') ## 'gidfiemhs'에서 'e'를 ''로 변경('e'를 삭제) // 'gidfimhs'

    text = '010-1234-5678 Kim'
    text.sub('^[0-9]{3}-[0-9]{3}-[0-9]{4}', '***-****-****') ## 전화번호를 *로 변환 // '***-****-**** Kim'
    ## ^          / [0-9] / {3} / - ##
    ## 처음에 위치 / 숫자 / 3개 / '-' ##
    ```
     + 예제: https://github.com/a0lim/PYTHON/blob/main/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4/lv1/72410.%E2%80%85%EC%8B%A0%EA%B7%9C%E2%80%85%EC%95%84%EC%9D%B4%EB%94%94%E2%80%85%EC%B6%94%EC%B2%9C/%EC%8B%A0%EA%B7%9C%E2%80%85%EC%95%84%EC%9D%B4%EB%94%94%E2%80%85%EC%B6%94%EC%B2%9C.py
