---
layout: post
title: 파이썬 자료구조 Chapter 02 튜플 # title에 [괄호] 사용 금지
date: 2021-05-15 14:30:00 +0900 # 한국 시간 포맷 +0900
description: 파이썬 자료구조 Chapter 02 튜플 메서드 언패킹 네임드 튜플 # Add post description (optional)
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
  - [2.3 튜플](#23-튜플)
    - [2.3.1 튜플 메서드](#231-튜플-메서드)
    - [2.3.2 튜플 언패킹](#232-튜플-언패킹)
    - [2.3.3 네임드 튜플](#233-네임드-튜플)
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

## 2.3 튜플

튜플<sup>tuple</sup> : 쉼표(,)로 구분된 값으로 이루어지는 불변 시퀀스 타입

중첩 가능. 값과 쉼표를 사용해 생성(괄호안에 쉼표 없이 값만 넣으면 튜플이 생성되지 않음)

```python
>>> empty = ()
>>> t1 = '안녕', # 또는 ('안녕',)
>>> len(empty)
0
>>> len(t1)
1
>>> t1
('안녕',)
>>> t2 = ('안녕',) 
>>> t2
>>> '안녕'
```

### 2.3.1 튜플 메서드

`A.count(x)` :  튜플 A 에 담긴 항목 X의 개수 반환

```python
>>> t = 1,5,7,8,9,4,1,4
>>> t.count(4)
2
```

`index(x)` : 항목 x의 엔덱스를 반환

```python
>>> t1 = 1,5,7
>>> t.index(5)
1
```

### 2.3.2 튜플 언패킹

파이썬에서 모든 반복가능한<sup>iterable</sup>객체는 **시퀀스 언패킹 연산자**<sup>sequence unpacking operator</sup> 사용하여 언패킹 가능

변수를 할당하는 문장에서 왼쪽 두개 이상의 변수를 사용하고 한 변수 앞에 \* 연산자가 붙으면, 오른쪽 값들 중 할당되고 남은 값들이 \* 연산자가 붙은 변수에 할당

```python
>>> x, *y = (1,2,3,4)
>>> x
1
>>> y
[2,3,4]

>>> *x, y = (1,2,3,4)
>>> x
[1,2,3]
>>> y
4
```

### 2.3.3 네임드 튜플

일반 튜플과 비슷한 성능과 특성 but 튜플 항목을 인덱스 위치 뿐만 아니라 이름으로도 참조 가능

**`collections.namedtuple()`**

1. 첫 번째 인수: 만들고자 하는 사용자 정의 튜플 데이터 타입의 이름(보통 왼쪽에 할당하는 변수의 이름과 똑같이 사용)

2. 두 번째 인수: 사용자 정의 튜플 각 항목을 지정하는 '공백으로 구분된 문자열' (리스트 또는 튜플 가능)

```python
>>> import collections
>>> Person = collections.namedtuple('Person', 'name age gender')
>>> # Person = collections.namedtuple('Person', ['name', 'age', 'gender'])
>>> # Person = collections.namedtuple('Person', ('name', 'age', 'gender'))
>>> p = Person('아스틴', 30, '남자')
>>> p
Person(name = '아스틴', age = 30, gender = '남자')
>>> p[0]
'아스틴'
>>> p.name
'아스틴'
>>> p.age = 20 # 에러: 일반 튜플과 마찬가지로 불변형이다.
Trabeback (most recent call last):
 File "<stdin>", line 1, in <module>
 AttiributeError: can't set attribute
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

