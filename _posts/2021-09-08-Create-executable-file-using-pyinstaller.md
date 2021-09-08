---
title: "pyinstaller를 이용하여 실행파일 만들기" 
excerpt: "pyinstaller를 이용하여 python에서 실행파일 만들기"
show_date: true
read_time: true

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "##0000FF"

categories: 
- python
tags: 
- pyinstaller
- python
- 실행파일
---

1. 아래의 명령어를 이용하여 **pyinstaller** 설치

```
pip install pyinstaller
```

2. 실행파일을 만들고자 하는 python 파일이 있는 경로에서 아래의 명령어 실행

```
pyinstaller 파일명.py
```
3. 실행파일(exe 형태) 하나만 만들고 싶을 경우

```
pyinstaller -F 파일명.py 
pyinstaller —onefile 파일명.py
```

4. GUI 형태의 실행파일을 만들 경우

```
pyinstaller -w 파일명.py
```

- 이 경우 python 코드 내에 포함되는 리소스(이미지 등) 파일 등도 실행파일의 경로 내 함께 포함되어야 함

5. GUI 형태의 실행파일을 하나의 실행파일로 만들 경우

```
pyinstaller -w -F 파일명.py
```

- 이 경우 파일 실행시 생성되는 임시경로가 매번 바뀌므로 python 코드 내에 포함되는 리소스 파일의 위치가 맞지 않아 오류가 발생함. 따라서 원 코드 내에 아래의 코드를 추가하여 경로를 맞춰줘야 함

```python
import OS

def resource_path(relative_path):
	try:
		base_path = sys._MEIPASS
	except Exception:
		base_path = os.path.abspath(".")

return os.path.join(base_path, relative_path)
```

- 이후 코드 내 리소스 파일 경로가 있는 부분을 **resource_path("경로가 포함된 파일명")**로 감싸준 후 아래의 명령어를 실행하면 코드 내에 포함된 리소스 파일이 실행파일의 경로에 포함되어 만들어짐

```
pyinstaller -w -F —add-data '.\gui_basic\*.png;gui_basic' 파일명.py
```

- 추가할 리소스 파일의 경로가 여러곳일 경우 —add-data 'src;dest'를 여러번 반복

6. 실행파일에 아이콘을 추가할 경우

```
pyinstaller -w -F -i 'icon.ico' 파일명.py
```