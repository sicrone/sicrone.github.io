---
title: "Python 관련 Tip 모음" 
excerpt: "Python을 이용하여 코딩작업 시 개인적으로 유용했던 Tip 정리. 지속적으로 추가 예정!!!" 
show_date: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  overlay_color: "#333"

categories: 
- coding
tags: 
- python
- tip
---

# Python 관련 Tip

## List
### List 복사하기
List를 다른 List로 assign하는 경우 메모리를 공유하여 사용함. 따라서, 두 List 중 하나의 값을 업데이트하면 나머지 다른 List의 값도 바뀜. 따라서, 단순 복사 시에는 copy() method를 사용하여야 함.

>List를 단순 assign한 경우

```python
>>> list1 = [1,2,3]
>>> list2 = list1
>>> list2
[1,2,3]
>>> list1[0] = 4
>>> list1
[4,2,3]
>>> list2
[4,2,3]
```

>List를 copy한 경우

```python
>>> list1 = [1,2,3]
>>> list2 = list1.copy()
>>> list2
[1,2,3]
>>> list1[0] = 4
>>> list1
[4,2,3]
>>> list2
[1,2,3]
```

### List 확장하기
List를 확장하는 방법에는 더하는 방법과 extend를 사용하는 방법이 있음

```python
>>> list1 = [1,2,3]
>>> list2 = [4,5,6]
>>> list1 + list2         # 방법 1-1 : 더하기
[1,2,3,4,5,6]
>>> list1 += list2        # 방법 1-2 : 더하기
[1,2,3,4,5,6]
>>> list1.extend(list2)   # 방법 2 : extend 사용하기
[1,2,3,4,5,6]
```

### List unpacking
List 내 각각의 값을 Index 필요없이 변수에 할당하는 방법
>방법 1

```python
>>> aaa = ['spikey', 48, 'Photo']
>>> name, age, hobby = aaa        # List unpacking
>>> name
'spikey'
>>> age
24
>>> hobby
'Photo'
```
>방법 2

```python
>>> aaa = ['spikey', 48, 'Photo']
>>> name, *ndata = aaa            # List unpacking
>>> name
'spikey'
>>> ndata
[24, 'Photo']
```

### List 내 개별 문자열을 합쳐서 문자열 만들기

개별 문자열들을 합치는 경우 `+`를 사용할 수 있으나, 문자열을 더해 나갈 때마다 문자열 객체를 생성하므로 메모리 관리 차원에서 join을 사용하는 것이 보다 효율적이다.

``` python
>>> a = ['I', 'am', 'a', 'boy.']
>>> print(' '.join(a))
I am a boy.
```

### List 내에서 가장 빈번하게 나오는 요소 찾기

collections 라이브러리 내 most_common을 이용하여  List 내에서 가장 빈번하게 나오는 요소를 찾을 수 있다.

```python
>>> from collections import Counter
>>> a = [1,1,2,3,5,6,2,5,6,7,4,1,2,1]
>>> cnt = Counter(a)
>>> print(cnt.most_common(2))
[(1,4), (2,3)]
```

### List에서 중복된 값 제거하기

List 내에서 중복된 값을 제거하기 위해서는 아래와 같이 두가지 방법을 사용할 수 있다.

```python
>>> ll = [1,2,3,4,3,2,3,4]
>>> list(set(ll))
[1,2,3,4]

>>> from collections import OrderedDict
>>> list(OrderedDict.fromkeys(ll).keys())
[1,2,3,4]
```

## Dictionary

### Dictionary 추가하기
List로 입력받은 자료를 dictionary에 추가하려면 아래와 같이 실행한다.

```python
>>> aaa = ['A','B','C','D','E']
>>> bbb = [1,2,3,4,5]
>>> ccc = dict(zip(aaa,bbb))
>>> ccc
{'A': 1, 'B': 2, 'C': 3, 'D': 4, 'E': 5}
```

또한 저장된 dictionary 내 요소를 얻기 위해서는 아래와 같이 실행한다.

```python
>>> ccc['c']
3
>>> ccc.get('D')
4
```



## I/O

### json 모듈 활용
List 형태의 데이터를 한번에 파일에 쓰거나 읽기 위해 json 모듈 내 dump, load명령어를 아래와 같이 사용할 수 있다.

```python
import json
aaa = ['a','b','c']
f = open('text.txt','w')
json.dump(data,f)
f.close()

f = open('text.txt','r')
bbb = json.load(f)
f.close()
```



20210912 계속 추가 예정
