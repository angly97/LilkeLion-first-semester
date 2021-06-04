## [Django] Django와 데이터베이스



### ▣ GitHub 업로드 순서

1. git init
2. git add
3. git commit -m "message"
4. git remote add [remote 이름] [repository 주소]
5. git push [remote이름] [올릴 branch 이름]



### ▣  ORM (Object Relation Mapping)

>파이썬에서 DB에 데이터 생성/수정/삭제 가능하게 함
>
>→ model.py를 건드리자 이제



### ▣  Blog 만들기

1. 우선 기본 셋팅 완료

2. models.py에 들어감

   1. 클래스 생성 후, 필드 설정 (필드 다 알 순 없고 필요할 때 검색해서 찾아 써)

      * models.BooleanField

      * models.CharField(max_length= )

      * models.DateField

        > 달력, 날짜

      * models.DateTimeField

        > 달력, 날짜, 시간

      * models.FloatField

      * models.IntegerField

      * models.TextField

        > max_length 지정하면, 폼에서는 제한 됨 
        >
        > But, 데이터베이스에는 영향 없음

   2. 각 인스턴스 이름 설정

      * 객체 호출 시 나오는 이름 설정

      ```python
      # models.py의 Blog 클래스 내부 함수
      def __str__(self):
          # 객체 호출 시, 포스팅 제목을 오브젝트 명으로
          return self.title
      ```

      

      ```python
      from django.db import models
      
      # 테이블이 될 클래스 생성
      # 클래스 명 = 테이블 명
      # models.Model 상속받음
      class Blog(models.Model):
      
          #제한이 있는 문자열(제한도 200자로 설정)
          title = models.CharField(max_length=200)
      
          writer = models.CharField(max_length=100)
          pub_date = models.DateTimeField()
          body=models.TextField()
      
          def __str__(self):
              # 객체 호출 시, 포스팅 제목을 오브젝트 명으로
              return self.title
      
      ```

   3. 클래스를 테이블로 만들 명령어

      * 클래스 만들었다고 바로 DB에 테이블 생성되지 않음

      * python manage.py makemigrations

        > models.py의 변경사항을 migrations 폴더에 저장

      * python manage.py migrate

        > migrations 폴더에 있는 ~~.py를 실행시켜 db.sqllite3 폴더에 적용

      * models.py에 변경사항 생기면 꼭 위의 순서대로 수행(makemigrations → migrate)

   4. 테이블 확인

      * admin 패널로 가능

        * urls.py에 admin path 설정 자동으로 되어있음

        1. 서버 구동 후, url 뒤에 /admin 입력 들어감

        2. super 유저 등록 필요

           >1. python manage.py createsuperuser
           >2. Username, Email, Password 입력 (비번 입력 시 터미널에 입력 안보임)

        3. admin.py에 들어감

           * models.py에 Blog 테이블을 만들었음을 알림

             ```python
             from django.contrib import admin
             
             # 추가한 내용
             from .models import Blog
             admin.site.register(Blog)
             ```

        4.  /admin 에 로그인 하면 Blog 확인 가능

   5. 데이터 입력 

      1. 우측의 Add Blog 클릭 후 데이터 입력 → SAVE 클릭