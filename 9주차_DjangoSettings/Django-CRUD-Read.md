## [Django] CRUD-Read

>C : Create
>
>R : Read
>
>U : Update
>
>D : Delete

### ▣ Read

* html 에 Blog 객체 출력

  1. views.py

     ```python
     from django.shortcuts import render
     
     # 데이터 불러오기 위해 import
     from .models import Blog
     
     def home(request):
     
         # Blog 객체들 전부 가져옴 
         blogs = Blog.objects.all()
         return render(request, "home.html", {'blogs': blogs})
     
     ```

  2. url.py

     ```python
     from django.contrib import admin
     from django.urls import path
     
     #views의 모든 함수 import
     from blog.views import *
     
     urlpatterns = [
         path('admin/', admin.site.urls),
         path('',home, name="home")
     ]
     
     ```

     

  3. templates 폴더에 home.html 생성

     ```html
     <!DOCTYPE html>
     <html lang="kr">
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>BLOG</title>
     
         <style>
             body{text-align: center;}
         </style>
     
     </head>
     <body>
         
         <!-- 핵심 부분 ! -->
         <div class="containger">
             <h1>Blog Project</h1>
     
             {%for blog in blogs%}
                 <div>
                     <h3>{{blog.title}}</h3>
                     {{blog.writer}}
                     {{blog.body}}
                     <br>
                 </div>
             {%endfor%}
     
         </div>
     </body>
     </html>
     ```

  4. 긴 내용 요약하기 (긴 내용 -> 요약본 출력)

     1. models.py의 Blog클래스에 코드 추가

        ```python
            def summary(self):
                # 포스팅의 body를 100자까지 자름
                return self.body[:100]
        ```

     2. home.html에서 summary 출력

        ```html
            <!-- 핵심 부분 ! -->
            <div class="containger">
                <h1>Blog Project</h1>
        
                {%for blog in blogs%}
                    <div>
                        <h3>{{blog.title}}</h3>
                        {{blog.writer}}
                        {{blog.summary}}		#body → summary로 변경
                        <br>
                    </div>
                {%endfor%}
        ```

        

* 요약된 내용 자세히 보기 (요약본 -> 긴 내용 출력)

  * Path-converter

    * 한 페이지 만들기 위해선, html파일 + 함수(views.py) + url연결(path설정) 필요

    * But, 많은 페이지들을 전부 이렇게 만들면 힘들어

    * 그래서! Path-converter로  id값을 통해  페이지 다르게 보여주기 가능

    * 그리고, views.py의 매개변수로 전달 가능

  1. views.py 에 detail 페이지에 대한 함수 추가

     ```python
     def detail(request, id):
     
         # 오브젝트 가져오거나 404띄우거나 
         # pk = primary key = id
         blog= get_object_or_404(Blog, pk=id)
         return render(request, "detail.html", {'blog': blog})
     
     ```

     *  blog= get_object_or_404(Blog, pk=id) 대신 →  blogs = Blog.objects.get(id=id) 가능

  2. url.py

     ```python
     urlpatterns = [
         path('admin/', admin.site.urls),
         path('',home,name="home"),
     
         #str은 자료형 & id는 views의 detail 함수 매개변수
         # 이렇게해서 id에 따라 다른 페이지 출력
         path('<str:id>', detail, name="detail"),
     
     ]
     ```

  3. url.py은 id를 어디서 얻어오지? 

     1. home.html에서 datail.html로 이동하는 링크 생성

        * detail이라는 이름의 url로 요청을 보내면서, blog.id도 전송

          ```html
          
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
          
          ```

  4. detail.html 생성

     ```html
     <!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Detail</title>
         
         <style>
             body{text-align: center;}
         </style>
     
     </head>
     <body>
         <h1>{{blog.title}}</h1>
         작성자: {{blog.writer}}
         날짜: {{blog.pub_date}}
         {{blog.blog}}
     </body>
     </html>
     ```

     

