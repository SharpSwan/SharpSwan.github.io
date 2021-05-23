---
layout: post
title: 파이썬 자료구조 Chapter 02 바이트와 바이트 배열 # title에 [괄호] 사용 금지
date: 2021-05-23 11:55:00 +0900 # 한국 시간 포맷 +0900
description: 파이썬 자료구조 Chapter 02 바이트와 바이트 배열 # Add post description (optional)
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
  - [2.5 바이트와 바이트 배열](#25-바이트와-바이트-배열)
    - [2.5.1 비트와 비트 연산자](#251-비트와-비트-연산자)
  - [2.6 연습문제](#26-연습문제)
    - [2.6.1 문자열 전체 반전](#261-문자열-전체-반전)
    - [2.6.2 문자열 단어 단위로 반전](#262-문자열-단어-단위로-반전)
    - [2.6.3 단순 문자열 압축](#263-단순-문자열-압축)
    - [2.6.4 문자열 순열](#264-문자열-순열)
    - [2.6.5 회문](#265-회문)

---

## 2.5 바이트와 바이트 배열

파이썬은 원시 바이트<sup>raw byte</sup>를 처리하는 데 사용할 수 있는 데이터 타입으로 불변 타입의 바이트(byte)와 가변 타입의 바이트 배열(bytearray)을 제공

두 타입 모두 0~255 범위의 부호 없는 8 비트 정수 시퀀스

바이트 타입 : 문자열 타입과 유사

바이브 배열 타입 : 리스트 타입과 유사

```python
>>> blist = [1, 2, 3, 255]
>>> the_bytes = bytes(blist)
>>> the_bytes
b'\x01\x02\x03\xff'
>>> the_byte_array = bytearray(blist)
>>> the_byte_array
bytearray(b'\x01\x02\x03\xff')
>>>
>>> the_bytes[1] = 127 # 불변(immutable)
TypeError                     Traceback (most recent call last)
<ipython-input-70-d52bfbb74c55> in <module>
      6 the_byte_array
      7 
----> 8 the_bytes[1] = 127 # 불변(immutable)

TypeError: 'bytes' object does not support item assignment
>>>
>>> the_byte_array[1] = 127 # 가변(mutable)
>>> the_byte_array
bytearray(b'\x01\x7f\x03\xff')
```

---

### 2.5.1 비트와 비트 연산자

비트 연산자는 비트로 표현된 숫자 조작에 유용

예: 곱셈 연산자 대신 비트 연산자로 곱셈 가능

1 << x는 숫자 1을 x번만큼 **왼쪽으로 이동**<sup>left shift</sup>한다는 의미로 $2$<sup>$x$</sup>를 신속하게 계산 가능

또한 $x$ & $(x -1)$이 0 인지 확인하면, x가 2의 제곱인지 아닌지 신속하게 확인 가능

예: x가 4(=2<sup>2</sup>)인 경우, 4는 100<sub>(2)</sub>이고 x-1인 3은 011<sub>(2)</sub>

두 값에 비트 AND(&)을 적용하면 0이 된다. 즉 2<sup>x</sup>를 비트로 표현하면 100...0이 되고 2<sup>x</sup>을 비트로 표현하면 011...1이 되므로, 

이 두 값에 비트 AND 연산을 적용하면 0이 된다(x 는 0보다 큰 정수여야 함)

```python
>>> x = 4
>>> 1<< x
16
>>>
>>> x = 8
>>> x & (x-1)
0
>>>
>>> x = 6
>>> x & (x-1)
4
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

