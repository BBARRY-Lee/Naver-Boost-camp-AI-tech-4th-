# 2. Module and Project

### 학습목표

- 파이썬 프로젝트의 기본이 되는 **모듈**과 **패키지**, 그리고 **프로젝트**의 개념
- 모듈과 패키지를 구성하고, 실제로 다른 개발자가 만든 모듈을 사용하는 방법

### 목차

---

## 1. Module

### 1-1. Module overview

- 파이썬은 대부분의 라이브러리가 이미 다른 사용자에 의해서 구현되어 있음
- 프로그램에서는 작은 프로그램 조각들, 모듈들을 모아 하나의 큰 프로그램을 개발함
- 프로그램을 모듈화 시키면 다른 프로그램이 사용하기 쉬움
예) 카카오톡 게임을 위한 카카오톡 접속 모듈

### 1-2. Module in Python

- Built-in Module인 Random을 사용,
난수를 쉽게 생성할 수 있음
    
    

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled.png)

### 1-3. 패키지

- 모듈을 모아놓은 단위, 하나의 프로그램

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%201.png)

### 1-4. Module 만들기

- 파이썬의 Module == py 파일을 의미
- 같은 폴더에 Module에 해당하는 .py 파일과 사용하는 .py을 저장한 후 import 문을 사용해서 module을 호출
- 

```python
fah_converter.py
def covert_c_to_f(celcius_value):
	return celcius_value * 9.0 / 5 + 32

module_ex.py
import fah_converter

print ("Enter a celsius value: "),
celsius = float(input())
fahrenheit = fah_converter.covert_c_to_f(celsius)
print ("That's ", fahrenheit, " degrees Fahrenheit")
```

### 1-5. namespace

- 모듈을 호출할 때 범위 정하는 방법
- 모듈 안에는 함수와 클래스 등이 존재 가능
- 필요한 내용만 골라서 호출 할 수 있음
- from 과 import 키워드를 사용함

```python
# Alias 설정하기 – 모듈명을 별칭으로 써서
import fah_converter as fah
print(fah.covert_c_to_f(41.6))
# fah_converter를 fah라는 이름으로 그 안에 covert_c_to_f 함수를 쓴다

# 모듈에서 특정 함수 또는 클래스만 호출하기
from fah_converter import covert_c_to_f
print(covert_c_to_f(41.6)) # covert_c_to_f 함수만 호출함

# 모듈에서 모든 함수 또는 클래스를 호출하기
from fah_converter import *
print(covert_c_to_f(41.6)) #전체 호출
```

### 1-6. Built-in Modules

- 파이썬이 기본 제공하는 라이브러리
- 문자처리, 웹, 수학 등 다양한 모듈이 제공됨
- 별다른 조치없이 import 문으로 활용 가능

```python
#난수
import random
print (random.randint (0,100)) # 0~100사이의 정수 난수를 생성
print (random.random()) # 일반적인 난수 생성

#시간
import time
print(time.localtime()) # 현재 시간 출력

#웹
import urllib.request
response = urllib.request.urlopen("http://thetemlab.io")
print(response.read())
```

- 수 많은 파이썬 모듈은 어떻게 검색할 것인가?
    1. 구글신에게 물어본다
    2. 모듈을 import후 구글 검색 또는 Help 쓰기
    3. 공식 문서를 읽어본다 [https://docs.python.org/3/library/](https://docs.python.org/3/library/)
- 실습 : 1 부터 100까지 특정 난수를 뽑고 싶다!

## 2. package

- 하나의 대형 프로젝트를 만드는 코드의 묶음
- 다양한 모듈들의 합, 폴더로 연결됨
- __init__ , **main** 등 키워드 파일명이 사용됨
- 다양한 오픈소스들이 모두 패키지로 관리됨

### 2-1. Package 만들기

1) 기능들을 세부적으로 나눠 폴더로 만듦

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%202.png)

2) 각 폴더별로 필요한 모듈을 구현함

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%203.png)

```python
# echo.py
def echo_play(echo_number):
print ("echo {} number start".format(echo_number))
```

3) 1차 Test –python shell

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%204.png)

4) 폴더별로__init__.py 구성하기

- 현재 폴더가 패키지임을 알리는 초기화 스크립트
- 없을 경우 패키지로 간주하지 않음 (3.3+ 부터는 X)
- 하위 폴더와 py 파일(모듈)을 모두 포함함
- import와 **all** keyword 사용

```python
__all__= ['image', 'stage', 'sound']

from . import image
from . import stage
from . import sound
```

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%205.png)

5) **main**.py 파일만들기

```python
from stage.main import game_start
from stage.sub import set_stage_level
from image.character import show_character
from sound.bgm import bgm_play

if **name** == '**main**':
	game_start()
	set_stage_level(5)
	bgm_play(10)
	show_character()
```

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%206.png)

### 2-2. package namespace

- Package 내에서 다른폴더의 모듈을 부를 때 상대참조로 호출하는 방법

```python
from game.graphic.render **import** render_test() # 절대참조
from **.render import** render_test() # . 현재디렉토리기준
from **..sound.echo import** echo_test() # .. 부모 디렉토리 기준
```

6) 실행하기–패키지이름만으로호출하기

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%207.png)

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%208.png)

## 3. 오픈소스 라이브러리 사용하기

### 3-1. 가상환경 설정하기 (Virtual Environment)

- 프로젝트 진행 시 필요한 패키지만 설치하는 환경
- 기본 인터프리터 + 프로젝트 종류별 패키지 설치
ex) 웹 프로젝트, 데이터 분석 프로젝트, 각각 패키지 관리할 수 있는 기능
- 다양한 패키지 관리 도구를 사용함
- 대표적인 도구 `**virtualenv**`와 `**conda**`가 있음
    
    ![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%209.png)
    

### 3-2. conda 가상환경

```bash
conda create -n my_project python=3.8
```

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%2010.png)

- 가상환경호출

```bash
conda activate my_project
```

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%2011.png)

- 가상환경해제

```bash
conda deactivate
```

### 3-3. 패키지 설치

```bash
conda install <패키지명>
# 설치하고자하는 패키지명 입력
conda install matplotlib
```

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%2012.png)

- Windows에서는 conda
- linux, mac에서는conda or pip

### 3-4. Conda 가상환경 예시

- `**matplotlib**` 활용한 그래프 표시
    - 대표적인 파이썬 그래프 관리 패키지
    - 엑셀과 같은 그래프들을 화면에 표시함
    - 다양한 데이터 분석 도구들과 함께 사용됨
    
    ```bash
    conda install <패키지명>
    # 설치하고자 하는 패키지명 입력
    conda install matplotlib
    conda install tqdm
    ```
    
    ![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%2013.png)
    

```python
import matplotlib.pyplot as plt
plt.plot([1,2,3,4])
plt.ylabel('some numbers')
plt.show()
```

![Untitled](2%20Module%20and%20Project%20d1fff210ff08497bb0a8847de7b470c8/Untitled%2014.png)

```python
from tqdm import tqdm
import time

for i in tqdm(range(100000)):
	if i % 1000 == 0:
		time.sleep(1)
```