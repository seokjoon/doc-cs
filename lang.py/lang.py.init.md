## utuntu 18.04 기준 설치, 설정
* apt-get install python3-pip python3-venv
* create a virtual env: ``` python3 -m venv foo ```

## 가상 환경
* activate virtual env: ``` source foo/bin/activate ```
* deactivate virtual env: ``` deactivate ```
* 우분투에서는 가상 환경 내의 pip 등이 우선 적용(우분투 전역 pip는 pip3), 맥에서는 지역 경로를 포함해야 함

## pip
* 패키지 목록: ``` pip list ```
* 패키지 설치: ``` pip install bar ```
* 의존성 기록: ``` pip freeze > requirements.txt ```
* 의존성 설치: ``` pip install -r requirements.txt ```
* 모든 (전역) 패키지 삭제: ``` pip freeze > all.txt && pip uninstall -r all.txt -y ```
* 우분투에서는 다른 패키지 설치 위해 wheel 설치 필요할 수 있음: ``` pip install wheel ```

## fastapi
* pip install fastapi
* pip install "uvicorn[standard]"
* uvicorn main:app --reload --host 0.0.0.0

## django 설치
* 가상환경 내부에서 아래 진행 후 127.0.0.1:8000 에서 확인
	* 장고 패키지 설치: ``` pip install django ```
	* 프로젝트 생성 및 해당 폴더로 이동 ``` django-admin startproject project1 && cd project1```
	* 앱 생성: ``` django-admin startapp app1 ```
	* 서버 실행: ``` python manage.py runserver ```
