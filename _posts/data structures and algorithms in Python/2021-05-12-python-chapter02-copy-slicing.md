---
layout: post
title: 파이썬 자료구조 Chapter 02 깊은 복사와 슬라이싱 연산 # title에 [괄호] 사용 금지
date: 2021-05-12 13:12:00 +0900 # 한국 시간 포맷 +0900
description: 파이썬 자료구조 Chapter 02 깊은 복사와 슬라이싱 연산 # Add post description (optional)
img: /data-structures-and-algorithms-in-python/data-structures-and-algorithms-in-python.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [파이썬 자료구조와 알고리즘, 파이썬 내장 시퀀스 타입]
use_math: true
---

# PART 자료구조 Contents

- [PART 자료구조 Contents](#part-자료구조-contents)

- [chapter 02 내장 시퀀스](#chapter-02-내장-시퀀스)
  - [2.1 깊은 복사와 슬라이싱 연산](#21-깊은-복사와-슬라이싱-연산)
    - [2.1.1 가변성](#211-가변성)
    - [2.1.2 슬라이싱 연산자](#212-슬라이싱-연산자)
  - [2.2 문자열](https://sharpswan.github.io/python-string/#22-%EB%AC%B8%EC%9E%90%EC%97%B4)
    - [2.2.1 유니코드 문자열](https://sharpswan.github.io/python-string/#221-%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C-%EB%AC%B8%EC%9E%90%EC%97%B4)
    - [2.2.2 문자열 메서드](https://sharpswan.github.io/python-string/#222-%EB%AC%B8%EC%9E%90%EC%97%B4-%EB%A9%94%EC%84%9C%EB%93%9C)
  
  - [2.3 튜플](https://sharpswan.github.io/python-tuple/#23-%ED%8A%9C%ED%94%8C)  
    - [2.3.1 튜플 메서드](https://sharpswan.github.io/python-tuple/#231-%ED%8A%9C%ED%94%8C-%EB%A9%94%EC%84%9C%EB%93%9C)
    - [2.3.2 튜플 언패킹](https://sharpswan.github.io/python-tuple/#232-%ED%8A%9C%ED%94%8C-%EC%96%B8%ED%8C%A8%ED%82%B9)
    - [2.3.3 네임드 튜플](https://sharpswan.github.io/python-tuple/#233-%EB%84%A4%EC%9E%84%EB%93%9C-%ED%8A%9C%ED%94%8C)
  - [2.4 리스트](https://sharpswan.github.io/python-list/#24-%EB%A6%AC%EC%8A%A4%ED%8A%B8)
    - [2.4.1 리스트 메서드](https://sharpswan.github.io/python-list/#241-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EB%A9%94%EC%84%9C%EB%93%9C)
    - [2.4.2 리스트 언패킹](https://sharpswan.github.io/python-list/#242-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%96%B8%ED%8C%A8%ED%82%B9)
    - [2.4.3 리스트 컴프리헨션](https://sharpswan.github.io/python-list/#243-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%BB%B4%ED%94%84%EB%A6%AC%ED%97%A8%EC%85%98)
    - [2.4.4 리스트 메서드 성능 측정](https://sharpswan.github.io/python-list/#244-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%84%B1%EB%8A%A5-%EC%B8%A1%EC%A0%95)
  - [2.5 바이트와 바이트 배열](https://sharpswan.github.io/python-chapter02-byte/#25-%EB%B0%94%EC%9D%B4%ED%8A%B8%EC%99%80-%EB%B0%94%EC%9D%B4%ED%8A%B8-%EB%B0%B0%EC%97%B4)
    - [2.5.1 비트와 비트 연산자](https://sharpswan.github.io/python-chapter02-byte/#251-%EB%B9%84%ED%8A%B8%EC%99%80-%EB%B9%84%ED%8A%B8-%EC%97%B0%EC%82%B0%EC%9E%90)
  - [2.6 연습문제](#26-연습문제)
    - [2.6.1 문자열 전체 반전](#261-문자열-전체-반전)
    - [2.6.2 문자열 단어 단위로 반전](#262-문자열-단어-단위로-반전)
    - [2.6.3 단순 문자열 압축](#263-단순-문자열-압축)
    - [2.6.4 문자열 순열](#264-문자열-순열)
    - [2.6.5 회문](#265-회문)
  
---

# chapter 02 내장 시퀀스

내장 시퀀스<sup>sequence</sup> 타입

- 멤버십<sup>membership</sup>연산 : `in` 키워드 사용
- 크기 함수 : `len(seq)`
- 슬라이싱<sup>slicing</sup> 속성 : `seq[:1]`
- 반복성<sup>iterability</sup> : 반복문에 있는 데이터를 순회할 수 있음

<br>

파이썬의 5개 내장 시퀀스 타입

- 문자열 `'str'`
- 튜플 `'tuple'`
- 리스트 `'list'`
- 바이트 배열 `'bytearray'`
- 바이트 `'type'`

생성 방법

```python
l = []
type(l)
<class 'list'>

s = ""
type(s)
<class 'str'>

t = ()
type(t)
<class 'tuple'>

ba = bytearray(b"")
type(ba)
<class 'bytearray'>

b = bytes([])
type(b)
<class 'type'>
```

---

## 2.1 깊은 복사와 슬라이싱 연산

### 2.1.1 가변성

1장에서 배운 점 : 파이썬 숫자는 불변<sup>immutable</sup>

이번 장 : 가변<sup>mutable</sup>객체 타입에 대해.

가변 데이터 : 리스트, 바이트 

불변 데이터(효율적<sub>가변 데이터보다</sub>) : 튜플, 문자열, 바이트

일부 컬렉션 데이터 타입은 불변 데이터 타입으로 인덱싱 가능

<br>

파이썬의 모든 변수는 객체 참조<sup>reference</sup>이므로 가변 객체를 복사할 때 매우 주의해야 함!

a = b 일때 a 는 실제 b가 가리키는 (참조하는) 곳을 가리킨다.

따라서 **깊은 복사**<sup>deep copy</sup>의 개념을 이해하는 것이 중요함.

Deep copy 예제
```python
# 리스트(list)
myList = [1, 2, 3, 4]
newList = myList[:]
newList2 = list(myList2)

# 셋(set)
people = {"버피", "애인절", "자일스"}
slayers = people.copy()
slayers.discard("자일스")
slayers.remove("에인절")

slayers
>>>{'버피'}

people
>>>{'자일스', '버피', '애인절'}

# 딕셔너리(dict)
myDict = {"안녕" : "세상"}
newDict = myDict.copy()

# 기타 객체의 깊은 복사는 copy 모듈 사용
import copy
myObj = "다른 어떤 객체"
newObj = copy.copy(myObj) # 얕은 복사 (shallow copy)
newObj2 = copy.deepcopy(myObj) # 깊은 복사 (deep copy)
```

### 2.1.2 슬라이싱 연산자

```python
seq[시작]
seq[시작:끝]
seq[시작: 끝: 스텝]

# 오른쪽(맨 끝)부터 읽을 때는 음수로
word = '뱀파이어를 조심해!'
word[-1]
>>>'!'

word[-2]
>>>'해'

word[-2:]
>>>'뱀파이어를 조심'

word[-0]
>>>'뱀'
```

---

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

