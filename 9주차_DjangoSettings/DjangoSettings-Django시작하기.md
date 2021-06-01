## [Django Settings] Django 시작하기



### ▣ Django

- 개발 프레임워크
  - 라이브러리보다 더 구성이 되어있어서 개발 속도 더 빠름
- 시작하기
  1. 바탕화면에 Django 빈 폴더 생성
  2. VS Code에서 Django 폴더 열고 -> new teminal
  3. 가상환경 설정
     * 위의 터미널 창에 phthon -m venv 가상환경이름
     * source 가상환경이름/Scrtipt/activate
  4. django 시작하기
     * pip install django
     * django-admin startproject 프로젝트이름
       * 생성 된 프로젝트 내에 manage.py 생김 for 서버 구동
     * 서버 구동을 위해 manage.py 실행시키기
       * cd 프로젝트이름
       * python manage.py runserver

