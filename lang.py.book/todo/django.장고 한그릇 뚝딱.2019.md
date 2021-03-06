# Chapter 1 준비하기
2. 코드로 배우는 필수 이론
    * 2.1. Python
        * 리스트: 배열: []
            * list()
        * 튜플: 배열(상수): ()
        * 집합: 중복 불가, 순서 없음: set()
            * intersection(), &, union(), | , difference(), -
        * 딕셔너리: 연관배열, 객체, 해시: {}
            * keys(), values(), items(), del, get(), in
        * 인덱싱: [n], 양수/음수 포인팅
        * 슬라이싱: [n:m]
        * if, for, while
        * def, class
        	* self, __init__


# Chapter 2 ToDoList 만들기
1.1. 프로젝트 구성하기
    * django-admin startproject foo
1.2. Application 구성하기
    * python manage.py startapp bar
    * vi foo/foo/settings.py
        ``` INSTALLED_APPS = [ ..., 'bar', ... ] ```
1.3. URL 설정하기
    * python manage.py runserver 0.0.0.0:8000
        * foo/settings.py: ``` ALLOWED_HOSTS = ['*'] ```
    * foo/urls.py, bar/urls.py, bar/views.py
1.4. HTML 템플릿 사용하기
    * bar/templates/bar
1.5. MVC 따라 하기
    * models.py
    * python manage.py makemigrations
    * python manage.py migrate
    * python manage.py dbshell
        * .tables
        * pragma table_info(todo_todo)
    * bar/urls.py, bar/views.py
1.6. CRUD 따라 하기
    * views.py
        * Bar.objects
            * get(), all(), save(), delete()
        * render(), HttpResponseRedirect(), reverse()
2.2. MVC가 뭔데?
    * Field: CharField, DateField, EmailField, FileField, TextField, IntegerField. BooleanField, 


# Chapter 3 맛집 공유 사이트 만들기
1. Do
1.1. 프로젝트 및 app 구성하기
1.2. URL 및 템플릿 설정하기
    * comment block: {% comment %} ... {% endcomment %}
1.3. CRUD 구성하기
1.4. 이메일 보내기
1.5. PythonAnyWhere로 배포하기

2. Learn
2.1. 이메일 보내기 활용법
2.2. 배포 때 신경 써야 할 점과 또 다른 배포 방법은?
2.3. 배포된 프로젝트 최신 상태로 업데이트하기
2.4. 실전 예제 해결하기 (3)

3. Ask


# Chapter 4 엑셀 계산 사이트 만들기
1. Do
1.1. 가상 환경 세팅 및 Requirements 사용하기
1.2. 프로젝트 및 app 구성하기
1.3. CRUD 틀, admin 화면 만들기
1.4. 이메일 인증으로 회원 가입하기
1.5. 로그인 여부 판단 및 로그아웃
1.6. 파일 업로드하기
1.7. Pandas 사용하기
1.8. 프로젝트 완성하기

2. Learn
2.1. 로그인 심화
2.2. 템플릿 사용하기
2.3. 파일 업로드
2.4. 파일 다운로드하기
2.5. 실전 예제 해결하기 (4)

3. Ask


# Chapter 5 실전 프로젝트 해결하기
1. Learn
1.1. 프로젝트 설계 때 필요한 것들

2. Do
2.1. 실전 프로젝트 해결하기
2.2. 실전 프로젝트 풀이

3. Done
3.1. 실전 프로젝트 마무리