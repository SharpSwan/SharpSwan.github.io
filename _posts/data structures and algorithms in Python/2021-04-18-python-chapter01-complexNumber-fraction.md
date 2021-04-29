---
layout: post
title: 파이썬 자료구조 Chapter 01 복소수, fraction 모듈, decimal 모듈, 진수, 넘파이 # title에 [괄호] 사용 금지
date: 2021-04-25 18:54:00 +0900 # 한국 시간 포맷 +0900
description: 파이썬 자료구조 Chapter 01 복소수, fraction 모듈 decimal 모듈, 진수, 넘파이 # Add post description (optional)
img: /data-structures-and-algorithms-in-python/data-structures-and-algorithms-in-python.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [파이썬 자료구조와 알고리즘, 파이썬 숫자]
use_math: true
---
# PART 자료구조 Contents

- [PART 자료구조 Contents](https://sharpswan.github.io/python-chapter01-integer-float/#part-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-contents)
- [Chapter 01 숫자](https://sharpswan.github.io/python-chapter01-integer-float/#chapter-01-%EC%88%AB%EC%9E%90)
  - [1.1 정수](https://sharpswan.github.io/python-chapter01-integer-float/#11-%EC%A0%95%EC%88%98)
  - [1.2 부동소수점](https://sharpswan.github.io/python-chapter01-integer-float/#12-%EB%B6%80%EB%8F%99%EC%86%8C%EC%88%98%EC%A0%90)
  - [1.2.1 부동소수점끼리 비교하기](https://sharpswan.github.io/python-chapter01-integer-float/#121-%EB%B6%80%EB%8F%99%EC%86%8C%EC%88%98%EC%A0%90%EB%81%BC%EB%A6%AC-%EB%B9%84%EA%B5%90%ED%95%98%EA%B8%B0)
  - [1.2.2 정수와 부동소수점 메서드](https://sharpswan.github.io/python-chapter01-integer-float/#122-%EC%A0%95%EC%88%98%EC%99%80-%EB%B6%80%EB%8F%99%EC%86%8C%EC%88%98%EC%A0%90-%EB%A9%94%EC%84%9C%EB%93%9C)
  - [1.3 복소수](#13-복소수)
  - [1.4 fraction 모듈](#14-fraction-모듈)
  - [1.5 decimal 모듈](#15-decimal-모듈)
  - [1.6 2진수, 8진수, 16진수](#16-2진수-8진수-16진수)
  - [1.7 연습문제](#17-연습문제)
  - [1.8 넘파이 패키지](#18-넘파이-패키지)


## 1.3 복소수

**복소수<sup>complex number</sup>**: $z = 3 + 4j$, 부동소수점 한 쌍을 갖는 *불변형*. `z.real`, `z.imag`, `z.conjugate()`같은 메서드로 실수부, 허수부, 켤레 복소수를 구할 수 있음.

*복소수 사용*: `cmath` 모듈 import
math 모듈에 있는 대부분의 삼각함수, 로그함수의 복소수 버전 제공

*복소수 전용 함수 제공*: `cmath.phase()`, `cmath.polar()`, `cmath.pi`, `cmath.e` 

<br>

## 1.4 fraction 모듈

파이썬에서 분수를 다루려면 `fraction` 모듈 사용해야 함

```python
from fractions import Fraction

Fraction(4,2) # 4/2

>>>Fraction(2, 1) # 4/2 = 2/1
```

`Fraction.denominator()` : 분모를 반환

`Fraction.numerator()` : 분자를 반환

`round(number1, places)` : 반올림

<br>

## 1.5 decimal 모듈

`deciomal.Decmal`: 정확한 10진법 부동소수점 숫자가 필요할 때

`Decimal()` : 정수 또는 문자열을 인수로 취함(\*파이썬 3.1부터 사용 가능)

`decomal.Decimnal.from_float()`: 부동소수점을 decimal.Decimal 타입으로 나타냄

**이 모듈은 부동소수점의 반올림, 비교, 뺄셈 등에서 나타내는 문제를 효율적으로 처리 가능**

```python
sum(0.1 for i in range(10)) == 1.0
>>>False # 0.1을 10번 더해도 1이 되지 않는다.

from decimal import Decimal
sum(Decimal("0.1") for i in range(10)) == Decimal("1.0")
>>>True
```


`decimal`모듈에는 `Decimal.exp(x)` 같은 내장함수가 있음 (대부분의 경우 사용 가능)

여기서 `X` : `decimal.Decimal` 객체 타입

`math`와 `cmath` 모듈에도 `exp()` 함수가 있으나 정확도가 필요하다면 `decimal` 모듈을 사용해야 함.

<br>

## 1.6 2진수, 8진수, 16진수

`bin(i)` 메서드: 정수 `i`의 2진수 문자열 반환

```python
>>>bin(999)
'0b1111100111'
```

`oct(i)`메서드: 정수 `i`의 8진수 문자열 반환

```python
>>> oct(999)
'0o1747'
```

`hex(i)` 메서드: 정수 `i`의 16진수 문자열 반환

```python
>>> hex(999)
'0x3e7'
```


<br>

## 1.7 연습문제

### 1.7.1 진법 변환

진법을 변환하는 함수 만들기. 다른 진법의 숫자를 10진수로 변환하기.

`convert_to_decimal.,py`
```python
#진법 변환
#다른 진법의 숫자를 10진수로 변환 (2<= base <= 10)

def convert_to_decimal(number, base):
    multiplier, result = 1, 0
    while number > 0:
        result += number % 10 * multiplier
        multiplier *= base        
        number = number //10
    return result


def test_convert_to_decimal():
    number, base =1001, 2
    assert(convert_to_decimal(number, base) == 9)
    print("테스트 통과!")
    
if __name__ == "__main__":
    test_convert_to_decimal()
```

반복문을 돌면서 `number % 10(base)`로 일의 자리 숫자를 하나씩 가져와서 계산함

10진수를 다른 진법의 숫자로 변환하는 함수(2<= base<=10)

`conver_to_from_decimal.py`
```python

def convert_from_decimal(number, base):
    multiplier, result = 1, 0
    while number > 0:
        result += number % base * multiplier
        multiplier *= 10    
        number = number //base
    return result


def test_convert_from_decimal():
    number, base =9, 2
    assert(convert_to_decimal(number, base) == 1001)
    print("테스트 통과!")
    
if __name__ == "__main__":
    test_convert_to_decimal()

```

base가 10보다 큰 경우 10 이상의 숫자는 숫자가 아니라 문자를 사용.

예: A = 10, B = 11, C =12

아래는 10진법 숫자를 20 이하의 진법으로 변환

`convert_from_decimal_larger_bases.py`
```python

def convert_from_decimal_larger_bases(number, base):
    strings = '0123456789ABCDEFGHIJ'
    result =""
    while number > 0:
        digit = number % base
        result = strings[digit] + result
        number = number //base
    return result


def test_convert_from_decimal_larger_bases():
    number, base =31, 16
    assert(convert_from_decimal_larger_bases(number, base) == "1F")
    print("테스트 통과!")
    
if __name__ == "__main__":
    test_convert_from_decimal_larger_bases()


```

다음 코드는 **재귀 함수** `(recursive function)`을 사용한 진법 변환

재귀 알고리즘에 대한 내용은 '8.2 재귀 알고리즘'을 참조

`convert_dec_to_any_base_rec.py`
```python
def convert_dec_to_any_base_rec(number, base):
    convertString = "012345679ABCDEF"
    if number < base:
        return convertString[number]
    else:
        return convert_dec_to_any_base_rec(number // base, base) \
            + convertString[number % base]


def test_convert_dec_to_any_base_rec():
    number = 9
    base = 2
    assert(convert_dec_to_any_base_rec(number, base) == "1001")
    print("테스트 통과!")


if __name__ == "__main__":
    test_convert_dec_to_any_base_rec()
```

<br>

### 1.7.2 최대공약수

두 정수의 최대 공약수<sup>greatest common divisor</sup>(GCD)

```python
def finding_gcd(a, b):
    while(b != 0):
        result = b
        a, b = b, a % b
    return result


def test_finding_gcd():
    number1 = 21
    number2 = 12
    assert(finding_gcd(number1, number2) == 3)
    print("테스트 통과!")


if __name__ == "__main__":
    test_finding_gcd()
```

### 1.7.3 random 모듈

난수를 생성하는 random 모듈. 실행 때마다 출력 결과는 다르다.

`testing_random.py`
```python
import random


def testing_random():
    """ random 모듈 테스트 """
    values = [1, 2, 3, 4]
    print(random.choice(values))
    print(random.choice(values))
    print(random.choice(values))
    print(random.sample(values, 2))
    print(random.sample(values, 3))

    """ values 리스트를 섞는다. """
    random.shuffle(values)
    print(values)

    """ 0~10의 임의의 정수를 생성한다. """
    print(random.randint(0, 10))
    print(random.randint(0, 10))


if __name__ == "__main__":
    testing_random()


>>>
3
3
4
[3, 1]
[4, 2, 3]
[4, 3, 2, 1]
3
4
```

### 1.7.4 피보나치 수열

피보나치 수열<sup>Fibonacci sequence</sup>는 첫째, 둘째항이 1이며 그 이후의 모든 항은 바로 앞 두항의 합인 수열이다.

`1 1 2 3 5 8 13 21 ...`

피보나치 수열을 세 가지 다른 방법으로 n 번째 숫자 찾는 코드

1. 재귀 호출을 사용하는 `find_fibonacci_seq_rec()`: 시간복잡도는 $O(2^n)$

2. 반복문을 사용 `find_fibonacci_seq_iter()`: 시간복잡도는 $O(n)$

3. 수식을 사용하는 `find_fibonacci_seq_form()`: 시간복잡도는 $O(1)$ (단 70번째 이상 결과는 정확하지 않음) 

`find_fibonacci_seq.py`
```python
import math


def find_fibonacci_seq_iter(n):
    if n < 2:
        return n
    a, b = 0, 1
    for i in range(n):
        a, b = b, a + b
    return a


def find_fibonacci_seq_rec(n):
    if n < 2:
        return n
    return find_fibonacci_seq_rec(n - 1) + find_fibonacci_seq_rec(n - 2)


def find_fibonacci_seq_form(n):
    sq5 = math.sqrt(5)
    phi = (1 + sq5) / 2
    return int(math.floor(phi ** n / sq5))


def test_find_fib():
    n = 10
    assert(find_fibonacci_seq_rec(n) == 55)
    assert(find_fibonacci_seq_iter(n) == 55)
    assert(find_fibonacci_seq_form(n) == 55)
    print("테스트 통과!")


if __name__ == "__main__":
    test_find_fib()
```

또한 다음과 같이 제너레이터<sup>generator</sup>를 사용하여 피보나치 수열을 구할 수 도 있다.

제너레이터: 파이썬의 시퀀스를 생성하는 객체

제너레이터를 순회할 때마다 마지막으로 호출된 요소를 기억하고 다음 값을 반환한다.

`yield` 문을 사용. 

`find_fibonacci_by_generator.py`
```python
def fib_generator():
    a, b = 0, 1
    while True:
        yield b
        a, b = b, a+b


if __name__ == "__main__":
    fg = fib_generator()
    for _ in range(10):
        print(next(fg), end=" ")

>>>
1 1 2 3 5 8 13 21 34 55 
```

<br>


### 1.7.5 소수(prime number)


소수(:두 개의 자연수를 곱하여 만들 수 없는 1보다 큰 자연수)를 만드는 세가지 방법

(즉 약수로 1과 자기 자신만을 가지는 수)


방법 1. 브루트 포스<sup>brute force</sup> 즉 무차별 대입 방법

방법 2. 제곱근 이용. $m = sqrt(n)$, $m * m = n$ 이라고 가정. n이 소수가 아니면 $n = a x b$ 이므로 $m * m = a * b$ 이다. m은 실수, n, a, b 는 자연수이다. 

그러면 다음 과 같은 세가지 경우가 있을 수 있다.

1) $a > m$ 이면 $b < m$
2) $a = m$ 이면 $b = m$
3) $a < m$ 이면 $b > m$

세가지 모두 $min(a,b) <=m$ 따라서 m까지의 수를 검색한다면 적어도 하나의 n과 나누어 떨어지는 수를 발견할 것임.

이것은 $n$이 소수가 아님을 보여주기에 충분하다.


방법 3. 확률론적 테스트와 페르마의 소정리<sup>Fermar's little theorem</sup>을 사용


`finding_prime.py`
```python
import math
import random


def finding_prime(number):
    num = abs(number)
    if num < 4:
        return True
    for x in range(2, num):
        if num % x == 0:
            return False
    return True


def finding_prime_sqrt(number):
    num = abs(number)
    if num < 4:
        return True
    for x in range(2, int(math.sqrt(num)) + 1):
        if number % x == 0:
            return False
    return True


def finding_prime_fermat(number):
    if number <= 102:
        for a in range(2, number):
            if pow(a, number - 1, number) != 1:
                return False
        return True
    else:
        for i in range(100):
            a = random.randint(2, number - 1)
            if pow(a, number - 1, number) != 1:
                return False
        return True


def test_finding_prime():
    number1 = 17
    number2 = 20
    assert(finding_prime(number1) is True)
    assert(finding_prime(number2) is False)
    assert(finding_prime_sqrt(number1) is True)
    assert(finding_prime_sqrt(number2) is False)
    assert(finding_prime_fermat(number1) is True)
    assert(finding_prime_fermat(number2) is False)
    print("테스트 통과!")


if __name__ == "__main__":
    test_finding_prime()

```

다음코드는 random 모듈을 사용하여 n 비트 소수를 생성.

3을 입력하면 $5(101$<sub>$(2)$</sub>$)$ 또는 $7$($111$<sub>$(2)$</sub>)의 결과가 나온다.

`generate_prime.py`
```python
import math
import random
import sys


def finding_prime_sqrt(number):
    num = abs(number)
    if num < 4:
        return True
    for x in range(2, int(math.sqrt(num)) + 1):
        if number % x == 0:
            return False
    return True


def generate_prime(number=3):
    while 1:
        p = random.randint(pow(2, number-2), pow(2, number-1)-1)
        p = 2 * p + 1
        if finding_prime_sqrt(p):
            return p


if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: generate_prime.py number")
        sys.exit()
    else:
        number = int(sys.argv[1])
        print(generate_prime(number))

>>>
$ python genereate_prime.py 3
5 (또는 7)
```


<br>

## 1.8 넘파이 패키지

넘파이<sup>Numpy</sup>(<https://www.numpy.org>): 대규모 다차원 배열 및 행렬 지원, 배열 연산에 쓰이는 수학 함수 라이브러리 제공

넘파이 배열: 임의의 차원<sup>dimension</sup>을 가짐.

넘파이 모듈의 array 메서드: '시퀀스의 시퀀서(리스트 또는 튜플)'을 2차원 넘파이 배열로 생성 가능

```python
np.array( ((11,12,13), (21,22,23), (31,32,33)) )
array([[11,12,13],
       [21,22,23],
       [31,32,33]])
```

`ndim` 속성<sup>attribute</sup>은 배열의 차원 수를 알려준다

```python

x = np.array( ((11,12,13), (21,22,23)) )
x.ndim

>>>
2
```

넘파이 모듈의 간단한 사용 예제

`testing_numpy.py`
```python
import numpy as np


def testing_numpy():
    ax = np.array([1, 2, 3])
    ay = np.array([3, 4, 5])
    print(ax)
    print(ax*2)
    print(ax+10)
    print(np.sqrt(ax))
    print(np.cos(ax))
    print(ax-ay)
    print(np.where(ax < 2, ax, 10))

    m = np.matrix([ax, ay, ax])
    print(m)
    print(m.T)

    grid1 = np.zeros(shape=(10, 10), dtype=float)
    grid2 = np.ones(shape=(10, 10), dtype=float)
    print(grid1)
    print(grid2)
    print(grid1[1]+10)
    print(grid2[:, 2]*2)


if __name__ == "__main__":
    testing_numpy()

>>>

[1 2 3]
[2 4 6]
[11 12 13]
[1.         1.41421356 1.73205081]
[ 0.54030231 -0.41614684 -0.9899925 ]
[-2 -2 -2]
[ 1 10 10]
[[1 2 3]
 [3 4 5]
 [1 2 3]]
[[1 3 1]
 [2 4 2]
 [3 5 3]]
[[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]]
[[1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]]
[10. 10. 10. 10. 10. 10. 10. 10. 10. 10.]
[2. 2. 2. 2. 2. 2. 2. 2. 2. 2.]
```
넘파이 배열은 파이썬 리스트보다 훨씬 효율적임. 

다음 테스트 결과를 살펴보자. (컴퓨터마다 차이는 있음)

`testing_numpy_speed.py`
```python
import numpy
import time


def trad_version():
    t1 = time.time()
    X = range(10000000)
    Y = range(10000000)
    Z = []
    for i in range(len(X)):
        Z.append(X[i] + Y[i])
    return time.time() - t1


def numpy_version():
    t1 = time.time()
    X = numpy.arange(10000000)
    Y = numpy.arange(10000000)
    Z = X + Y
    return time.time() - t1


if __name__ == "__main__":
    print(trad_version())
    print(numpy_version())


>>>
2.768224000930786
0.11034607887268066
```

