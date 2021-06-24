# Django 환경설정

python + django + vscode / pycharm

### 1. 아나콘다 version 확인

`conda -V`

### 2. 가상환경을 위한 프로젝트의 독립된 공간을 생성

### 3. 가상환경생성

`conda create -n "가상환경이름" python = 3.8.8`

### 4. 생성된 가상환경 리스트 확인

`conda info --envs`

### 5-1. 가상환경 활성화

`conda activate "가상환경이름"`

### 5-2. 가상환경 비활성화

`conda deactivate`

### 5-3. 가상환경 삭제

`conda remove -n "가상환경이름" --all`

### 6. django 설치

`conda activate "가상환경이름"`

`conda install django`

### 7. django 프로젝트 생성

`django-admin startpoint "프로젝트이름"`

### 8. 생성한 프로젝트로 위치 이동

`cd "프로젝트이름"`

### 9. server 실행

`python3 manage.py runserver`

### 10. 크롬 실행 후 아래 주소 입력

`http://127.0.0.1:8000`

### 11. application 생성 (추가)

`python3 manage.py startapp "app이름"`

> application구조?
>
> 하나의 프로젝트에서 구현되는 기능을 개별로 나누기 위함
>
> 특정 기능에 대한 수정이나 문제 발생 시 다른 기능에 미치는 영향이 줄어듦 

### 12. Setting.py 에 app 추가

프로젝트이름 > app이름 > setting.py

> INSTALLED_APPS = [
>      'django.contrib.admin',
>      'django.contrib.auth',
>      'django.contrib.contenttypes',
>      'django.contrib.sessions',
>      'django.contrib.messages',
>      'django.contrib.staticfiles',
>      '생성한 app이름'

### 13. app폴더에서 urls.py 생성 후 아래 내용 입력

> from django.urls import path
>   from . import views
>
> urlpatterns = [
>        path('', views.index)
>   ]

### 14. app에서 views.py의 인덱스 함수 실행 함수 결과를 client에 넘겨줌

> from django.shortcuts import render
> from django.http import HttpResponse
>
> def index(request):
>     return HttpResponse('이름')

### 15. server 실행

`python3 manage.py runserver`

### 16. views.py에서 html파일을 클라이언트에 응답할 때 render 함수 사용

> html페이지를 응답을 해줄때
>
> templates 폴더 생성 후 하위로 이전에 만들었던 app이름과 동일한 폴더 생성
>
> 앞단계에서 생성한 app폴더에 index.html 생성해서 구현



> MVC MVC?
>
> MVC : Model, View, Controller (설계 및 개발하는 소프트웨어 방법론)
>
> * Model : 데이터베이스, 어플리케이션 정보 등을 담는 데이터 집합소 (**models.py**)
> * View : 사용자에게 보이는 화면 (**templates**)
> * Controller : 사용자와 서버 간 인터페이스 역할, 로직 처리 (**views.py**)
>
> MTV : Model, Template, View (MVC와 같은 맥락)

## 모델 생성 후

#### Model.py 수정 후 장고 서버에 적용 

`python3 manage.py makemigrations`

`python3 manage.py migrate`



#### 장고 프로젝트 데이터베이스에 접근 후 확인 

`python3 manage.py dbshell`

#### 데이터베이스에 존재하는 테이블 확인

`.tables`

#### 테이블 정보 확인

`PRAGMA table_info(app이름)`

> 순서 (단순 Number) | 이름 | 형태 | notnull여부 | pk여부
>
> 1 | content | varcher(255) | 1 | 0



