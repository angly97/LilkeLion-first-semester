## [Django] Static



### ▣ 쟝고에서 다루는 파일

* 동적파일

  * 서버의 데이터들이 가공된 다음 보여지는 파일

* 정적파일

  * 미리 서버에 저장된 파일

  * 서버에 저장된 그대로르 서비스 해주는 파일

  * 종류

    * Static

      > 개발자가 서버 개발 시 미리 넣은 정적 파일(Img, js, css)

    * media

      > 사용자가 업로드할 수 있는 파일

      

### ▣ 실습하기

> 사자 사진을 블로그에 로고처럼 넣기

1. blog app에 static 폴더 생성

2. static 폴더에 멋사 로고 사진 넣음

3. settings.py 가서 STATIC 파일 설정

   - 정적 파일들 관리하기 위함

   - STATIC 부분 코드 추가

     ```python
     import os	# 추가
     
     STATIC_URL = '/static/'
     
     # 추가한 부분들
     # static 파일을 모으기 전에 현재 static 파일들이 어디있는 지 경로 써줌
     STATICFILES_DIRS =[
         os.path.join(BASE_DIR,'blog','satic')
     ]
     # static 파일을 어디에 모을건지
     STATIC_ROOT = os.path.join(BASE_DIR, 'static')
     
     
     ```

   - static 파일을 모으기 위한 명령어

     - python manage.py collectstatic

4. static에 저장된 사진을 모든 html에 띄우기

   1. base.html에 가서 static 로드

      ```html
      <body>
      
        <!--추가-->
        {% load static %}
      
          <!--navbar 컴포넌트 코드 -->
          <nav class="navbar navbar-expand-lg navbar-light bg-light">
              <div class="container-fluid">
      
                <!--추가: 로고 누르면 home으로 가도록 -->
                <a class="navbar-brand" href="{% url 'home' %}">
      
                <!--추가 : static 로드하기 위함이래...
                            nav바 왼쪽에 로고 붙음 -->
                <img src="{% static 'likelion_logo.png' %}" alt="" width="50" height="45">
      ```

   2. 나머지 네비바 링크 설정

      ```html
      <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="{% url 'new' %}">Write</a>
      </li>
      ```

      

