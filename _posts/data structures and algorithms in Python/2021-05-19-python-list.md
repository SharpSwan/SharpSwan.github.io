---
layout: post
title: 파이썬 자료구조 Chapter 02 리스트 # title에 [괄호] 사용 금지
date: 2021-05-19 20:00:00 +0900 # 한국 시간 포맷 +0900
description: 파이썬 자료구조 Chapter 02 리스트 메서드 언패킹 컴프리헨션 성능 측정 # Add post description (optional)
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

## 2.4 리스트

일반적인 컴퓨터 과학에서 

**배열**<sup>array</sup> : 여러 요소(원소)들이 연속된 메모리에 순차적으로 저장되는 매우 간단한 구조. 요소에 **직접 접근**시 시간 복잡도 = $O(1)$ 어떤 위치에 항목을 **삽입**하려면 그 위치에서부터 모든 항목을 오른쪽으로 옮겨야하므로 시간복잡도 = $O(n)$

**연결 리스트**<sup>linked list</sup> : 여러 분리된 노드<sup>node</sup>가 서로 연결되어 있는 구조. 요소에 직접 접근시 시간 복잡도 = $O(n)$(연결리스트는 어떤 노드에 접근하려면 처음부터 순회<sup>iterating</sup>를 시작해야 한다. 어떤 노드를 삽입할 때 그 위치를 안다면 연결리스트 노드 수에 상관없이 시간 복잡도 = $O(1)$


파이썬에서 배열과 가장 유사한 객체 = **리스트** <sup>list</sup> 

리스트는 크기를 동적으로 조정할 수 있는 배열. 연결 리스트와 관련 없음

연결 리스트는 매우 중요한 **추상 데이터 타입**(ADT)

배열(또는 파이썬 리스트)과 연결 리스트의 차이점을 아는 것은 매우 중요

`append()`, `pop()`: 리스트 끝에서 항목을 추가하거나 제거할 때. 시간복잡도 = $O(1)$

`remove()`, `index()`, `멤버십 테스트 in`: 리스트 항목을 검색해야 하므로 시간복잡도= $O(n)$

`insert()` : 지정한 인덱스에 항목을 삽입한 후 , 그 이후의 인덱스 항목들을 한 칸씩 뒤로 밀어야 하므로 시간복잡도 = $O(n)$

검색이나 멤버십 테스트시 **빠른 속도** 가 필요하다면 **셋**<sup>set</sup>이나 **딕셔너리**<sup>dictionary</sup>같은 컬렉션 타입을 선택하는 것이 더 적합할 수 있음.

리스트에서 항목을 순서대로 정렬하여 보관하면 빠른 검색 제공

---

### 2.4.1 리스트 메서드

**`append()`**

`A.append(x)`는 리스트 A 끝에 항목 x를 추가. 

`A[len(A):] = [x]`와 동일한 의미

```python
>>> people = ["버피","페이스"]
>>> people.append("자일스")
>>> people
['버피', '페이스', '자일스']
>>> people[len(people):] = ["잰더"]
>>> people
['버피', '페이스', '자일스', '잰더']
```

---

**`extend()`**

`A.extend(c)`는 반복 가능한 모든 항목 c를 리스트 A에 추가. `A[len(A):] = c` 또는 `A += C`와 동일

```python
>>> people = ["버피","페이스"]
>>> people.extend("자일스")
>>> people
['버피', '페이스', '자', '일', '스']
>>> people +="윌로"
>>> people
['버피', '페이스', '자', '일', '스', '윌', '로']
>>> people +=["잰더"]
>>> people
['버피', '페이스', '자', '일', '스', '윌', '로', '잰더']
>>> people[len(people):] = "아스틴"
>>> people
['버피', '페이스', '자', '일', '스', '윌', '로', '잰더', '아', '스', '틴']
```

---

**`insert()`**

`A.insert(i, x)` 는 리스트 A의 인덱스 위치 i 에 항목 x 를 삽입한다

```python
>>> people = ["버피","페이스"]
>>> people.insert(1, "잰더")
>>> people
['버피', '잰더', '페이스']
```

---

**`remove()`**

`A.remove(x)` 는 리스트 A의 항목 X를 제거한다. X가 존재하지 않으면 `ValueError` 예외를 발생시킴

```python
>>> people = ["버피","페이스"]
>>> people.remove("버피")
>>> people
['페이스']
>>> people.remove("버피")
ValueError Traceback (most recent call last)
<ipython-input-12-bcef00a685a7> in <module>
      2 people.remove("버피")
      3 people
----> 4 people.remove("버피")

ValueError: list.remove(x): x not in list
```

---

**`pop()`**

`A.pop(x)`는 리스트 A에서 인덱스 x에 있는 항목을 제거하고 그 항목을 반환한다.

x를 지정하지 않으면, 리스트 맨 끝 항목을 제거하고 그 항목을 반환한다.

```python
>>> people = ["버피","페이스", "아스틴"]
>>> people.pop(1)
'페이스'
>>> people
['버피', '아스틴']
>>> people.pop()
'아스틴'
>> people
['버피']
```

---

**`del문`**

`del`문 : 리스트 인덱스를 지정, 특정 항목 삭제. 슬라이스를 사용하여 특정 범위 항목 삭제도 가능

```python
>>> a = [-1, 4, 5, 7, 10]
>>> del a[0]
>>> a
[4, 5, 7, 10]
>>> del a[2:3]
>>> a
[4, 5, 10]
>>> del a # 변수 a 자체를 삭제
>>> a

NameError                            Traceback (most recent call last)
<ipython-input-21-369f72d80e04> in <module>
      5 a
      6 del a # 변수 a 자체를 삭제
----> 7 a

NameError: name 'a' is not defined
```

객체 참조가 삭제 되고 다른 객체가 더 이상 그 데이터를 참조하지 않을 때

파이썬은 그 데이터 항목을 가비지 컬렉터<sup>garbage collector</sup>에 수집한다.

---

**`index()`**

`A.index(x)`: 리스트 A 에서 항목 x의 인덱스를 반환

```python
>>> people = ["버피", "페이스"]
>>> people.index("버피")
0
```

---

**`count()`**

`A.count(x)`: 리스트 A 에 항목 x가 몇개 들어 있는지 개수를 반환

```python
>>> people = ["버피", "페이스", "버피"]
>>> people.count("버피")
2
```

---

**`sort()`**

리스트 A의 항목을 정렬, 그 변수 자체에<sup>in place</sup>에 적용

`A.sort(key, reverse)`에 아무런 인수가 없으면 오름차순으로 정렬

인수를 지정할 때는 키워드 인수<sup>keyword argument</sup>를 사용해야 함

예: 리스트 항목을 내림차순으로 정렬하려면 `sort(reverse=True)`로 지정

인수 `key`를 지정하려면 함수를 넣어야함.

```python
>>> people = ["잰더", "페이스", "버피"]
>>> people.sort()
>>> people
['버피', '잰더', '페이스']
>>> people.sort(reverse=True)
>>> people
['페이스', '잰더', '버피']
```

응용 예제: 날짜 정렬 코드

```python
>>> import time
>>> timestamp = [
    "2021-05-05 01:17:31",
    "2021-05-05 02:17:28",
    "2021-05-05 06:39:26",
    "2021-05-10 07:30:35",
    "2021-05-10 11:32:33",
    "2021-05-10 12:35:48"
            ]
>>> def time_format(t):
        return time.strptime(t, '%Y-%m-%d %H:%M:%S')[0:6]

>>> timestamp.sort(key=time_format, reverse=True) #날짜를 최신순으로 정렬
>>> print(timestamp)
['2021-05-10 12:35:48', '2021-05-10 11:32:33', '2021-05-10 07:30:35', '2021-05-05 06:39:26', '2021-05-05 02:17:28', '2021-05-05 01:17:31']

>>> timestamp.sort(key= lambda x: time.strptime(x, '%Y-%m-%d %H:%M:%S')[0:6], reverse=True)
>>> print(timestamp)
['2021-05-10 12:35:48', '2021-05-10 11:32:33', '2021-05-10 07:30:35', '2021-05-05 06:39:26', '2021-05-05 02:17:28', '2021-05-05 01:17:31']
```

---

**`reverse()`**

`A.reverse()` 메서드 : 리스트 A의 항목 반전시켜 그 변수에 적용

`list[::-1]` 과 같음


```python
>>> people = ["잰더", "페이스", "버피"]
>>> people.reverse()
>>> people
['버피', '페이스', '잰더']
>>> people[::-1]
['잰더', '페이스', '버피']
```
---

### 2.4.2 리스트 언패킹

튜플 언패킹과 비슷

```python
>>> first, *rest = [1,2,3,4,5]
>>> first
1
>>> rest
[2, 3, 4, 5]
```

함수의 전달 인수로 리스트에 별(\*) 인수<sup>starred argument</sup>를 사용할 수 있음


```python
>>> def example_args(a, b, c):
        return a * b * c # 여기서 *는 곱셈

>>> L = [2,3,4]

>>> example_args(*L) # 리스트 언패킹
24
>>> example_args(2, *L[1:])
24
```

---

### 2.4.3 리스트 컴프리헨션

반복문의 표현식. 조건문을 포함할 수 도 있음. 형식은 다음과 같이 대괄호 **[ ]** 로 묶는다

* **[ 항목 for 항목 in 반복 가능한 객체 ]**
* **[ 표현식 for 항목 in 반복 가능한 객체 ]**
* **[ 표현식 for 항목 in 반복 가능한 객체 if 조건문 ]**

```python
>>> a = [y for y in range(1900, 1940) if y%4 == 0]
>>> a
[1900, 1904, 1908, 1912, 1916, 1920, 1924, 1928, 1932, 1936]

>>> b = [2**i for i in range(13)]
>>> b
[1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096]

>>> c = [x for x in b if x%2 ==0]
>>> c
[2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096]

>>> d = [str(round(355/113.0, i)) for i in range(1,6)]
>>> d
['3.1', '3.14', '3.142', '3.1416', '3.14159']

>>> words = 'Buffy is awesome and a vampire slayer'.split()
>>> e = [[w.upper(), w.lower(), len(w)] for w in words]

>>> for i in e:
        print(i)

['BUFFY', 'buffy', 5]
['IS', 'is', 2]
['AWESOME', 'awesome', 7]
['AND', 'and', 3]
['A', 'a', 1]
['VAMPIRE', 'vampire', 7]
['SLAYER', 'slayer', 6]
``` 

리스트 컴프리헨션은 **단순한 경우에만** 사용하는 것이 좋음

-> 가독성을 위해서는 여러 줄의 표현식과 조건문으로 표현하는 것이 리스트 컴프리헨션 한 줄로 표현하는 것보다 나을 수 있음

[구글 파이썬 스타일 가이드](https://github.com/google/styleguide/blob/gh-pages/pyguide.md) 에서 소개하는 리스트 컴프리헨션의 좋은 예와 나쁜 예 참조

1. 좋은 예

```python
Yes:
  result = [mapping_expr for value in iterable if filter_expr]

  result = [{'key': value} for value in iterable
            if a_long_filter_expression(value)]

  result = [complicated_transform(x)
            for x in iterable if predicate(x)]

  descriptive_name = [
      transform({'key': key, 'value': value}, color='black')
      for key, value in generate_iterable(some_input)
      if complicated_condition_is_met(key, value)
  ]

  result = []
  for x in range(10):
      for y in range(5):
          if x * y > 10:
              result.append((x, y))

  return {x: complicated_transform(x)
          for x in long_generator_function(parameter)
          if x is not None}

  squares_generator = (x**2 for x in range(10))

  unique_names = {user.name for user in users if user is not None}

  eat(jelly_bean for jelly_bean in jelly_beans
      if jelly_bean.color == 'black')
```


2. 나쁜 예

```python
No:
  result = [complicated_transform(
                x, some_argument=x+1)
            for x in iterable if predicate(x)]

  result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]

  return ((x, y, z)
          for x in range(5)
          for y in range(5)
          if x != y
          for z in range(5)
          if y != z)
```

---

### 2.4.4 리스트 메서드 성능 측정

테스트: `timeit` 모듈의 `Timer` 객체를 생성해 사용.

`Timer` 객체의 첫 번째 매개변수 : 측정하고자 하는 코드

두 번째 매개변수 : 테스트를 위한 설정문

`timeit` 모듈은 명령문을 정해진 횟수만큼 실행하는 데 걸리는 시간을 측정(기본값: `number = 1000000`)

테스트 완료 시 문장이 수행된 시간(밀리초)을 부동소수점 값으로 반환

```python
def test1():
    l = []
    for i in range(1000):
        l = l + [i]


def test2():
    l = []
    for i in range(1000):
        l.append(i)


def test3():
    l = [i for i in range(1000)]


def test4():
    l = list(range(1000))


if __name__ == "__main__":
    import timeit
    t1 = timeit.Timer("test1()", "from __main__ import test1")
    print("concat ", t1.timeit(number=1000), "milliseconds")
    t2 = timeit.Timer("test2()", "from __main__ import test2")
    print("append ", t2.timeit(number=1000), "milliseconds")
    t3 = timeit.Timer("test3()", "from __main__ import test3")
    print("comprehension ", t3.timeit(number=1000), "milliseconds")
    t4 = timeit.Timer("test4()", "from __main__ import test4")
    print("list range ", t4.timeit(number=1000), "milliseconds")

>>>
concat  0.9828926390000561 milliseconds
append  0.07194113500008825 milliseconds
comprehension  0.03139724599895999 milliseconds
list range  0.013271247000375297 milliseconds
```

종합적으로 리스트 메서드의 시간복잡도는 다음과 같음

n은 리스트의 총 항목수 k는 연산(조회 및 추가) 항목수

|연산|시간복잡도|
|:---:|:---:|
|인덱스 []접근|$O(1)$|
|인덱스 할당|$O(1)$|
|append()|$O(1)$|
|pop()|$O(1)$|
|pop(i)|$O(1)$|
|insert(i)|$O(1)$|
|insert(i, 항목)|$O(1)$|
|del 연산자|$O(1)$|
|삽입|$O(1)$|
|멤버십 테스트in|$O(1)$|
|슬라이스 [x,y]조회|$O(k)$|
|슬라이스 삭제|$O(n)$|
|슬라이스 할당|$O(n+k)$|
|reverse()|$O(n)$|
|연결<sup>concatenate</sup>|$O(k)$|
|sort()|$O(nlogn)$|
|곱하기|$O(nk)$|

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

