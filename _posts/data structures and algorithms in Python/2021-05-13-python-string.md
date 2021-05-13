---
layout: post
title: 파이썬 자료구조 Chapter 02 문자열 # title에 [괄호] 사용 금지
date: 2021-05-13 17:15:00 +0900 # 한국 시간 포맷 +0900
description: 파이썬 자료구조 Chapter 02 유니코드 문자열 문자열 메서드 # Add post description (optional)
img: /data-structures-and-algorithms-in-python/data-structures-and-algorithms-in-python.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [파이썬 자료구조와 알고리즘, 파이썬 내장 시퀀스 타입]
use_math: true
---
# PART 자료구조 Contents

- [PART 자료구조 Contents](#part-자료구조-contents)
- [chapter 02 내장 시퀀스](https://sharpswan.github.io/python-chapter02-copy-slicing/#chapter-02-%EB%82%B4%EC%9E%A5-%EC%8B%9C%ED%80%80%EC%8A%A4)
  - [2.1 깊은 복사와 슬라이싱 연산](https://sharpswan.github.io/python-chapter02-copy-slicing/#21-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%99%80-%EC%8A%AC%EB%9D%BC%EC%9D%B4%EC%8B%B1-%EC%97%B0%EC%82%B0)
    - [2.1.1 가변성](https://sharpswan.github.io/python-chapter02-copy-slicing/#211-%EA%B0%80%EB%B3%80%EC%84%B1)
    - [2.1.2 슬라이싱 연산자](https://sharpswan.github.io/python-chapter02-copy-slicing/#212-%EC%8A%AC%EB%9D%BC%EC%9D%B4%EC%8B%B1-%EC%97%B0%EC%82%B0%EC%9E%90)
  - [2.2 문자열](#22-문자열)
    - [2.2.1 유니코드 문자열](#221-유니코드-문자열)
    - [2.2.2 문자열 메서드](#222-문자열-메서드)
  - [2.3 튜플](#23-튜플)
    - [2.3.1 튜플 메서드](#231-튜플-메서드)
    - [2.3.2 튜플 언패킹](#232-튜플-언패킹)
    - [2.3.3 네임드 튜플](#233-네임드-튜플)
  - [2.4 리스트](#24-리스트)
    - [2.4.1 리스트 메서드](#241-리스트-메서드)
    - [2.4.2 리스트 언패킹](#242-리스트-언패킹)
    - [2.4.3 리스트 컴프리헨션](#243-리스트-컴프리헨션)
    - [2.4.4 리스트 메서드 성능 측정](#244-리스트-메서드-성능-측정)
  - [2.5 바이트와 바이트 배열](#25-바이트와-바이트-배열)
    - [2.5.1 비트와 비트 연산자](#251-비트와-비트-연산자)
  - [2.6 연습문제](#26-연습문제)
    - [2.6.1 문자열 전체 반전](#261-문자열-전체-반전)
    - [2.6.2 문자열 단어 단위로 반전](#262-문자열-단어-단위로-반전)
    - [2.6.3 단순 문자열 압축](#263-단순-문자열-압축)
    - [2.6.4 문자열 순열](#264-문자열-순열)
    - [2.6.5 회문](#265-회문)
  
  
---

## 2.2 문자열

파이썬 객체의 두가지 출력 형식

1. 문자열<sup>string</sup> 형식 : 사람을 위해 설계 됨

2. 표현 형식<sup>representational</sup> :  파이썬 인터프리터에서 사용하는 문자열로 보통 디버깅할 때 사용

파이썬 클래스 작성시 문자열 표현을 정의하는 것이 중요

### 2.2.1 유니코드 문자열

**유니코드**<sup>unicode</sup>는 전 세계 언어의 문자를 정의하기 위한 국제 표준 코드

공백, 특수문자, 수학 및 기타 분야의 기호들도 포함

파이썬 3부터 모든 문자열은 일반적인 바이트가 아닌 유니코드

문자 열 앞에 U 붙이면 유니코드 문자열을 만들 수 있음

```python
>>>u'잘가\0020세상 !'
'잘가 세상 !'
```

위의 이스케이스 시퀀스<sup>escape sequence</sup>는 서수 값이 0x0020인 유니코드 문자

일반적인 아스키 코드<sup>ASCII code</sup>의 표현은 7비트(아스키 코드를 확장한 ANSI 코드는 8비트)

유니코드 표현은 16비트 필요

---

### 2.2.2 문자열 메서드

**`join()`**

`A.join(B)` : 리스트 B에 있는 모든 문자열을 하나의 단일 문자열 A로 결합.

+를 사용할 수도 있지만 리스트에 많은 문자가 있다면 비효율적

```python
>>> slayer = ["버피", "앤", "아스틴"]
>>>" ".join(slayer)
'버피 앤 아스틴'
>>> "-<>-".join(slayer)
'버피-<>-앤-<>-아스틴'
>>>"".join(slayer)
'버피앤아스틴'
``` 

`join()` 메서드와 내장함수 `reversed()`를 같이 사용할 수 있음

```python
>>>"".join(reversed(slayer))
'아스틴앤버피'
```

---
**`ljust(), rjust()`**

`A.ljust(width, fillchar)` : 문자열 A **'맨 처음'** 부터 문자열을 포함한 길이 width 만큼 문자 fillchar를 채운다.

`A.rjust(width, fillchar)` : 문자열 A **'맨 끝'** 부터 문자열을 포함한 길이 width 만큼 문자 fillchar를 채운다.

```python
>>> name = "스칼렛"
>>> name.ljust(50, '-')
'스칼렛-----------------------------------------------' #len = 50

>>> name = "스칼렛"
>>> name.rjust(50, '-')
'-----------------------------------------------스칼렛' #len = 50
```
---
**`format()`**

A.format()은 문자열 A에 변수를 추가하거나 형식화하는데 사용
```python
>>> "{0} {1}".format("안녕,", "파이썬")
"안녕, 파이썬!"
>>> "이름: {who}, 나이: {age}".format(who="제임스", age=17)
'이름: 제임스, 나이: 17"
>>>"이름: {who}, 나이: {0}".format(12, who="에이미")
"이름: 에이미, 나이: 12"
```

파이썬 3.1부터 필드 이름이나 인덱스 생략 가능.

이런 경우 자동으로 순서대로 필드에 0부터 시작하는 번호를 매김

```python
>>> "{} {} {}".format("파이썬", "자료구조", "알고리즘")
'파이썬 자료구조 알고리즘'
```

+연산자를 사용하면 문자열 더 간결하게 결합 가능

지정자 s 는 문자열 형식, r은 표현 형식, a는 아스키 코드 형식을 의미

```python
>>> import decimal
>>> "{0} {0!s} {0!a}".format(decimal.Decimal("99.9"))
"99.9 99.9 Decimal('99.9')"
```

---

**문자열 언패킹**

문자열 매핑 언패킹<sup>mapping unpacking</sup> 연산자는 \*\* 이고 이를 사용하면 함수로 전달하기에 적합한 키-값 딕셔너리가 생성된다.

`local()` 메서드는 현재 스코프<sup>scope</sup>에 있는 지역 변수<sup>local variable</sup>을 딕셔너리로 반환한다.

```python
>>> hero = "버피"
>>> number = 999
>>> "{number}: {hero}".format(**locals())
'999: 버피'
```
---

**`splitlines()`**

A.splitlines()는  문자열 A에 대해 줄 바꿈 문자를 기준으로 분리한 결과를 문자열 리스트로 반환

```python
>>> slayres = "로미오\n줄리엣"
>>> slayres.splitlines()
['로미오', '줄리엣']
```

---

**`split()` 메서드**

`A.split(t, n)`은 문자열 A에서 문자열 t를 기준으로 정수 n번만큼 분리한 문자열 리스트 반환.

n을 지정하지 않으면 대상 문자열을 t로 최대한 분리

t도 지정하지 않으면 공백 문자<sup>whitespace</sup>로 구분한 문자열 리스트 반환

```python
>>> slayers ="버피*크리스-메리*16"
>>> fields = slayers.split("*")
>>> print(fields)
['버피', '크리스-메리', '16']

>>> job = fields[1].split("-")
>>> print(job)
['크리스', '메리']
```

`split()` 을 사용하여 모든 스페이스를 제거하는 함수 만들기

```python
def earse_space_from_string(string):
    s1 = string.split(" ")
    s2 = "".join(s1)
    return s2
```

비슷하게 `rsplit(t, n)` 메서드는 `split(t, n)`메서드와 같은 방식으로

문자열을 오른쪽에서 왼쪽으로 분리한 문자열 리스트를 반환한다

```python
>>> start = "안녕*세상*!"
>>> start.split("*", 1)
['안녕', '세상*!']
>>> start.rsplit("*", 1)
['안녕*세상', '!']
```

---

**`strip()`**

`A.strip(B)` :  문자열 A 앞 뒤의 문자열 B를 제거. 인수 B가 없으면 공백 문자를 제거.

```python
>>> slayers = "로미오 * 줄리엣999"
>>> slayers.strip("999")
'로미오 * 줄리엣'
```

`strip()` 메서드를 사용하여 한 파일에서 사용된 모든 단어를 알파벳순으로 출력하며 각 단어가 등장한 횟수도 함께 출력하는 함수

`count_unique_words.py`
```python
import string
import sys


def count_unique_word():
    words = {}
    strip = string.whitespace + string.punctuation + string.digits + "\"'"
    for filename in sys.argv[1:]:
        with open(filename) as file:
            for line in file:
                for word in line.lower().split():
                    word = word.strip(strip)
                    if len(word) > 2:
                        words[word] = words.get(word, 0) + 1

    for word in sorted(words):
        print("'{0}': {1}번".format(word, words[word]))


if __name__ == "__main__":
    count_unique_word()
```

`A.lstrip(chars)` :  문자열 A의 시작(왼쪽) 부분에 있는 문자열 chars 또는 공백을 제거

`A.rstrip(chars)` : 문자열 A의 끝(오른쪽) 부분에 있는 chars 또는 공백을 제거

---

**`swapcase()` 메서드**

`A.swapcase()` 는 문자열 A 에서 대소문자를 반전한 문자열의 복사본을 반환

```python
>>> slayers = "Buffy and Faith"
>>> slayers.swapcase()
'bUFFY AND fAITH'
```

`capitalize()` : 문자열 첫 글자 대문자로 변경한 복사본 반환

`lower()` : 전체 문자열을 소문자로 변경한 복사본 반환

`upper()` : 전체 문자열을 대문자로 변경한 복사본 반환

---

**`index()` `find()` 메서드**

문자열 안에서 또 다른 문자열의 인덱스를 찾는 메서드가 있다.

`A.index(sub, start, end)` : 문자열 A에서 부분 문자열 sub의 인덱스 위치를 반환하며 실패하면 `ValueError` 예외를 발생시킴.

`A.find(sub, start, end)` : 문자열 A에서 부분 문자열 sub의 인덱스 위치를 반환, 실패하면 -1을 반환

인덱스 start와 end는 문자열 범위, 생략할 경우 전체 문자열에서 부분 문자열 sub를 찾음

```python
>>> slayers = "Buffy and Faith"
>>> slayers.find("y")
4
>>> slayers.find("k")
-1
>>> slayers.index("k")
ValueError Traceback (most recent call last)
ValueError: substring not found
>>> slayers.index("y")
4
```

`rindex(sub, start, end)` : 문자열 끝(오른쪽)에서부터 일치하는 부분 문자열 sub의 인덱스를 반환

`rfind(sub, start, end)` : 마찬가지.

앞에서처럼 검색이 실패할 경우 `rindex()`는 `ValueError` 예외 발생, `rfind()` 메서드는 -1 리턴

---

**`count()` 메서드**

`A.count(sub, start, end)`는 문자열 A 에서 인덱스 start, end 범위 내의 부분 문자열 sub가 나온 횟수 반환

```python
>>> slayers = "Buffy is Buffy is Buffy"
>>> slayers.count("Buffy", 0, -1)
2
>>> slayers.count("Buffy")
3
```

---

**`replace()` 메서드**

`A.replace(old, new, maxreplace)` : 문자열 A에서 문자열 old를 대체 문자열 new로 maxrplace만큼 변경한 문자열의 복사본을 반환

maxreplace를 지정하지 않으면 모든 Old를 new 로 변경

```python
slayers = "Buffy is Buffy is Buffy"
slayers.replace("Buffy", "who", 2)

'who is who is Buffy'
```

---

**`f-strings`**

`f스트링`<sup>formatted string literal</sup> : 파이썬 3.6부터 사용 가능

문자열 앞에 접두사 f 를 붙이면 사용가능. 기존의 `%`나 `.format` 방식에 비해 간결, 직관적, 빠름

```python
>>> name = "Fread"
>>> f"his name is {name!r}."
"his name is 'Fread'."

>>> name = "Fread"
>>> f"his name is {repr(name)}" # repr() = !r"
"his name is 'Fread'"

>>> import decimal
>>> width = 10
>>> precision = 4
>>> value = decimal.Decimal("12.34567")
>>> f"결과 :{value:{width}.{precision}}" # 중첩 필드 사용
'결과 :     12.35'

>>> from datetime import datetime
>>> today = datetime(year =2021, month = 4, day = 27)
>>> f"{today:%B %d, %Y}" # 날짜 포맷 지정자(specifier) 사용
'April 27, 2021'

>>> number = 1024
>>> f"{number:#0x}" # 정수 포맷 지정자 사용(16진수 표현)
'0x400'
```

[스트링 관련 파이썬 공식문서 바로가기](https://www.python.org/dev/peps/pep-0498)



---

## 2.3 튜플


### 2.3.1 튜플 메서드

### 2.3.2 튜플 언패킹

### 2.3.3 네임드 튜플

---

## 2.4 리스트


### 2.4.1 리스트 메서드



### 2.4.2 리스트 언패킹

---

### 2.4.3 리스트 컴프리헨션

---

### 2.4.4 리스트 메서드 성능 측정

---

## 2.5 바이트와 바이트 배열

---

### 2.5.1 비트와 비트 연산자

## 2.6 연습문제

---

### 2.6.1 문자열 전체 반전

---

### 2.6.2 문자열 단어 단위로 반전

---

---

### 2.6.3 단순 문자열 압축

---

### 2.6.4 문자열 순열


---

### 2.6.5 회문

---

