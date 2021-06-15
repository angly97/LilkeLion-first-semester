## [Django] Heroku 배포하기



### ▣ 방법

1. Heroku 홈페이지 회원가입

   - [Cloud Application Platform | Heroku](https://www.heroku.com/)

2. Heroku CLI 설치

   - [The Heroku CLI | Heroku Dev Center](https://devcenter.heroku.com/articles/heroku-cli)
   - download intall 후 cli 설치

3. Git Bash 

   1. "heroku" 라고 쳤을 때 출력이 되면 heroku cli 설치 완료 

4. 배포를 위한 환경변수 적용

   - 코드 자체가 깃 허브에 올라가니까 보안이 필요한 시크릿 키나, AWS API키를 환경변수 처리 해줘야 함

   1. settings.py

      - 디버그는 불리언 형식으로 나오도록 코드 작성

      ```python
      # AWS 설정
      DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
      
      # 수정: 다운받은 .CSV 엑셀 파일에서 복붙 -> 그랬으나, 이젠 환경변수 처리 해줌 for 배포 전 보안
      AWS_ACCESS_KEY_ID = os.environ.get('AWS_ACCESS_KEY_ID')
      AWS_SECRET_ACCESS_KEY = os.environ.get('AWS_SECRET_ACCESS_KEY')
      
      AWS_STORAGE_BUCKET_NAME = 'likelion9th-django-lesson'
      
      AWS_S3_SIGNATURE_VERSION = 's3v4'
      AWS_S3_REGION_NAME = 'ap-northeast-2'
      
      # 수정: 배포를 위한 디버그 설정, 불리언으로 리턴 되도록
      DEBUG = (os.environ.get('DEBUG', 'True') != False)
      ```

5. .gitignore 파일 적용

   - 깃에게 이건 빼고, 이건 깃에 추가해라

   1. manage.py있는 위치에 gitignore 파일 생성 후 복붙
   2. gitignore.io 에서 Django 선택 후, '생성' 클릭
   3. 코드 복사 후, .gitignore 파일에 복붙

6. Heroku 용 파일 작성

   - Profile이라는 파일 생성

     1. manage.py가 있는 위치에 생성

     2. web: gunicorn 프로젝트명.wsgi --log-file 

        - 프로젝트 명 = wsgi.py 있는 폴더 명

        ```
        web: gunicorn django_db_project.wsgi --log-file
        ```

   - runtime.txt 파일 생성

     - 어떤 버전의 파이썬을 실행시킬지 알려줌
     - manage.py있는 위치에 생성
     - 내 파이썬 버전 작성

     ```
     python-3.9.5
     ```

7. 필요한 Dependency 설치

   - pip install gunicorn whitenoise dj-database-url psycopg2-binary

8. settings.py 수정

   1. Whiltenoise 설치

      * MIDDLEWARE에서 제일 SecurityMeddleware 바로 아래 내용 추가

      ```python
      MIDDLEWARE = [
          'django.middleware.security.SecurityMiddleware',
          
          # 추가
          'whitenoise.middleware.WhiteNoiseMiddleware',
          
          'django.contrib.sessions.middleware.SessionMiddleware',
          'django.middleware.common.CommonMiddleware',
          'django.middleware.csrf.CsrfViewMiddleware',
          'django.contrib.auth.middleware.AuthenticationMiddleware',
          'django.contrib.messages.middleware.MessageMiddleware',
          'django.middleware.clickjacking.XFrameOptionsMiddleware',
      ]
      ```

   2. ALLOWED_HOSTS 수정

      ```python
      ALLOWED_HOSTS = ['*']
      ```

   3. DB 관련 코드 수정

      - settings.py 제일 밑에 아래 코드 추가

        ```python
        import dj_database_url
        db_from_env = dj_database_url.config(corn_max_ate=500)
        DATABASES['default'].update(db_from_env)
        ```

9. requirements.txt에 내용 추가

   - pip freeze > requirements.txt

10. git에 수정된 파일 추가

    1. git add -A
    2. git commit -m 'for heroku'

11. Heroku  관련 명령어 실행

    >heroku는 깃으로 돌아간다. 
    >
    >- 즉, 수정이 되면 반드시 깃에 반영해줘야 함
    >- 10. git 수정된 파일 추가 -> 이거 반복 

    1. heroku login
       1. 아무 키 누르라는 영어 나옴 -> 엔터!
       2. 로그인 창 뜨면 login 눌러줌
       3. 로그인이 되어서 내 이메일이 뜸
    2. heroku create
       - 새로운 heroku 컨테이너를 만듦
       - 내 heroku 앱이 배포될 주소가 뜸
    3. git push heroku main
       - heroku앱이 자체적으로 깃에 저장
    4. heroku run python manage.py migrate
       - 서버에 올라가 있는 상태에서 수행 = heroky run ~
       - db 가 migration 되게 함
    5. heroku run python manage.py createsupersuser
    6. heroky open

12. Heroku에서 환경 변수 설정

    - 환경변수 처리한 것들을 heroku에게 알려줘야 함

    1. [Personal apps | Heroku](https://dashboard.heroku.com/apps) 

    2. 앱이 올라간 서버에 들어가

    3. Settings에 가서 Reveal Config Vars 

       - Config Vars에 KEY 넣어줌

         >DEBUG - False
         >
         >AWS_ACCESS_KEY_ID - AKIA32NLL4DS6EVL7OXX
         >
         >AWS_SECRET_ACCESS_KEY - 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

    4. 키 입력해주고 그냥 나가면 됨 
