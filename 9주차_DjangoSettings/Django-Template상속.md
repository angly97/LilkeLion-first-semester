## [Django] Template 상속

>지난번 블로그 프로젝트에서 네비게이션 바를 추가하고 싶음

### ▣ 부트스트랩

1. bootstrap 검색 후 들어가 CSS코드 & JS코드를 head에 넣음

2. 모든 페이지마다 navbar 필요

   - 모든 페이지에 navbar 코드 복붙하기는 번거로움
   - 그래서! 쟝고에선 Template 상속 지원!
     - html에서 겹치는 부분을 base.html에 만들고 이걸 상속시킴

   

### ▣ Template 상속하기

1. base.html 생성

   - 프로젝트 설정 폴더(url.py, settings.py 있는 폴더)에 templates 폴더 안에 생성

   - navbar 코드 포함하여 위까지(html태그)까지 복사 후 base.html에 붙여넣기

   - 페이지마다 달라지는 부분은 block content로 묶음

     ```html
     <!-- base.html -->
     
     <!DOCTYPE html>
     <html lang="kr">
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         
         <!--부트스트랩 CSS 코드 & JS 코드 -->
         <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">
         <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4" crossorigin="anonymous"></script>
         <title>BLOG</title>
     
         <style>
             body{text-align: center;}
         </style>
     
     </head>
     <body>
     
         <!--navbar 컴포넌트 코드 -->
         <nav class="navbar navbar-expand-lg navbar-light bg-light">
             <div class="container-fluid">
               <a class="navbar-brand" href="#">Navbar</a>
               <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                 <span class="navbar-toggler-icon"></span>
               </button>
               <div class="collapse navbar-collapse" id="navbarSupportedContent">
                 <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                   <li class="nav-item">
                     <a class="nav-link active" aria-current="page" href="#">Home</a>
                   </li>
                   <li class="nav-item">
                     <a class="nav-link" href="#">Link</a>
                   </li>
                   <li class="nav-item dropdown">
                     <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                       Dropdown
                     </a>
                     <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                       <li><a class="dropdown-item" href="#">Action</a></li>
                       <li><a class="dropdown-item" href="#">Another action</a></li>
                       <li><hr class="dropdown-divider"></li>
                       <li><a class="dropdown-item" href="#">Something else here</a></li>
                     </ul>
                   </li>
                   <li class="nav-item">
                     <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
                   </li>
                 </ul>
                 <form class="d-flex">
                   <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
                   <button class="btn btn-outline-success" type="submit">Search</button>
                 </form>
               </div>
             </div>
           </nav>
     
           
           <div class ="containger">
     
             <!-- 이게 핵심!! -->
             {% block content %}
             {% endblock%}
     
           </div>
     
           </body>
     </html>
     ```

     

2. 각 페이지 html에서도 해당 부분 block content로 묶음

   ```html
   <!-- home.html -->
   
   <!-- Template 상속 -->
   {% extends 'base.html' %}
   
   <!--base.html의 block content에 해당-->
   {% block content %}
       <h1>Blog Project</h1>
   
       <div>
           <a href="{% url 'new' %}"> write blog </a>
       </div>
   
       {%for blog in blogs%}
           <div>
               <h3>{{blog.title}}</h3>
               {{blog.id}}
               {{blog.writer}}
   
               #추가된 부분
               {{blog.summary}} <a href="{%url 'detail' blog.id %}">...more</a>
               <br>
           </div>
       {%endfor%}
   {% endblock%}
   
   ```

   

3. settings.py 설정

   - TEMPLATES 부분의 DIRS에 base.html 경로 입력

     ```python
     TEMPLATES = [
         {
             'BACKEND': 'django.template.backends.django.DjangoTemplates',
             
             # 여기!
             'DIRS': ['django_db_project/templates'],
             'APP_DIRS': True,
             'OPTIONS': {
                 'context_processors': [
                     'django.template.context_processors.debug',
                     'django.template.context_processors.request',
                     'django.contrib.auth.context_processors.auth',
                     'django.contrib.messages.context_processors.messages',
                 ],
             },
         },
     ]
     ```

   

4. urls.py 정리

   1. Blog app 폴더 내에 urls.py 생성 후 기존 코드 복붙

      ```python
      from django.contrib import admin
      from django.urls import path
      
      #views의 모든 함수 import
      #from blog.views import *
      from .views import *
      
      urlpatterns = [
          
          #어드민 지우고, 홈도 메인페이지니까 지워
          #path('admin/', admin.site.urls),
          #path('',home,name="home"),
      
      
          #str은 자료형 & id는 views의 detail 함수 매개변수
          # 이렇게해서 id에 따라 다른 페이지 출력
          path('<str:id>', detail, name="detail"),
      
          path('new/', new, name="new"),
          path('create/', create, name="create"),
          path('edit/<str:id>', edit, name="edit"),
          path('update/<str:id>', update, name="update"),
          path('delete/<str:id>', delete, name="delete"),
      ]
      
      ```

   2. 기존 urls.py 수정

      > app 별로 urls.py를 관리하자!

      - home만 import & include import 추가
      - path는 admin과 home만
      - blog.url을 include

      ```python
      from django.contrib import admin
      from django.urls import path, include #include 추가
      
      #views의 home만 import
      from blog.views import home
      
      urlpatterns = [
          path('admin/', admin.site.urls),
          path('',home,name="home"),
      
          # blogs 아래 urls의 path를 포함
          # 근데 이제 모든 url 앞에 'blog/'가 붙음
          path('blog/', include('blog.urls'))
      
      ]
      
      ```

      

