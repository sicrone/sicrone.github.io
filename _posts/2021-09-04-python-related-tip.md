---
title: "Python 관련 Tip 모음" 
excerpt: "Python을 이용하여 코딩작업 시 개인적으로 유용했던 Tip 정리. 지속적으로 추가 예정!!!" 

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  overlay_color: "#333"

categories: 
- python 
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



20210904 계속 추가 예정