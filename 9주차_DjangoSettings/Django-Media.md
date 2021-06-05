## [Django] Media



### ▣ 실습하기

> 사용자가 사진을 웹에 업로드하는 기능 

1. settings.py 에 MEDIA 설정

   ```python
   import os
   
   STATIC_URL = '/static/'
   
   # static 파일을 모으기 전에 현재 static 파일들이 어디있는 지 경로 써줌
   STATICFILES_DIRS =[
       os.path.join(BASE_DIR,'blog','static')
   ]
   # static 파일을 어디에 모을건지
   STATIC_ROOT = os.path.join(BASE_DIR, 'static')
   
   # 추가한 부분들!!
   # 사용자가 업로드한 파일 모으기
   MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
   
   # 사용자가 업로드한 파일 보여줄 때 맨 앞에 나오는 url 설정
   MEDIA_URL = '/media/'
   
   
   ```

2. urls.py 설정

   - 사용자가 요청한 사진은 url을 통해 보여줌

     ```python
     from django.contrib import admin
     from django.urls import path, include
     from blog.views import home
     
     # 2개 import 추가
     from django.conf import settings
     from django.conf.urls.static import static
     
     urlpatterns = [
         path('admin/', admin.site.urls),
         path('',home,name="home"),
         path('blog/', include('blog.urls')),
     
     ]+static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) 
       # 바로 위에 코드 외우지 마; 그냥 이걸로 미디어를 url로 설정할 수 있는 걸 알라
     
     
     ```

3. models.py 설정

   - 사용자가 글을 올리면 업로드할 사진을 저장해야 함

   - pip install pillow

   - Blog에 image필드 추가

     ```python
     from django.db import models
     
     class Blog(models.Model):
     
         title = models.CharField(max_length=200)
         writer = models.CharField(max_length=100)
         pub_date = models.DateTimeField()
         body=models.TextField()
     
         # upload_to: 업로드할 폴더 지정
         # settings.py에 MEDIA_URL로 지정한 media 폴더 안에 blog 폴더를 만들어서 관리할 목적
         # blank, null 을 true로 설정해서, 포스팅에 사진없어도 에러 안나게 끔
         image = models.ImageField(upload_to="blog/", blank=True, null=True)
     
         
         def __str__(self):
             # 객체 호출 시, 포스팅 제목을 오브젝트 명으로
             return self.title
     
         def summary(self):
             # 포스팅의 body를 100자까지 자름
             return self.body[:100]
     
     ```

4. 기존 데이터 삭제

   - 필드가 변경되었으니깐!

   1. 파일 탐색기 > 프로젝트 폴더 > blog > migrations
   2. 0001_initial 삭제
   3. pycache폴더 들어가서 0001_initial_python~~ 삭제
   4. 프로젝트 폴더로 가서 db_sqllite3 삭제

5. 다시 데이터 저장할 준비

   1. python manage.py makemigrations
   2. python manage.py migrate
   3. 슈퍼유저 다시 생성
      1. python manage.py createsuperuser

6. 사진 업로드 기능 추가

   1. new.html 코드 추가

      ```html
      <h1>Write Your Blog</h1>
      
      <!-- 추가: 파일도 같이 넘겨야 해서 enctype 속성 추가-->
      <form action="{% url 'create' %}" method="post" enctype="multipart/form-data">
      
          {%csrf_token%}
      
          <p>제목: <input type="text" name="title"></p>
          <p>작성자: <input type="text" name="writer"></p>
          <p>사진: <input type="file" name="image"></p>
      
          <!-- 추가 -->
          본문: <textarea name="body" id="" cols="30" rows="10"></textarea>
      
          <button type="submit">submit</button>
      </form>
      ```

   2. views.py에서 create 수정

      - 사진 저장하도록 추가

        ```python
        # new.html에서 정보를 받아야 함 -> request.POST 사용
        def create(request):
        
            new_blog = Blog()
            new_blog.title = request.POST['title']
            new_blog.writer = request.POST['writer']
            new_blog.body = request.POST['body']
            new_blog.pub_date = timezone.now()
        
            # 추가
            new_blog.image =request.FILES['image']
            new_blog.save()
        
            # 이때는 render 안 써 
            # 새로운 페이지로 넘어가는 게 아니라, 기능 수행 후 이전 페이지로 돌아가야 하니까
            # 새로운 객체의 id를 보내서 path
            return redirect('detail', new_blog.id)
        ```

   3. detail.html 수정

      - 저장한 사진을 보여주기 위함

        ```html
            <h1>{{blog.title}}</h1>
            <div>
                작성자: {{blog.writer}}
                <br>
                날짜: {{blog.pub_date}}
            </div>
            <hr>
        
            <!-- 추가: 사진의 url로 연결; 
                blog객체의 image 필드에 url이 있으니까-->
            <p><img src="{{blog.image.url}}" alt=""></p>
            
        
            <p>{{blog.body}}</p>
        
            <!--edit.html로 이동-->
            <a href="{% url 'edit' blog.id %}">수정하기</a>
            
            <!--url.py에서 delete로 설정한 url로 이동-->
            <a href="{% url 'delete' blog.id %}">삭제하기</a>
        
        ```

      - 사진없이 새 글 업로드 하면 에러나지 않도록 수정

        ```html
        <!-- 추가 : 템플릿 언어로 감싸 -->
        {% if blog.image %}
        
        <!--사진의 url로 연결; 
        blog객체의 image 필드에 url이 있으니까-->
        <p><img src="{{blog.image.url}}" alt=""></p>
        
        {% endif %}
        ```

        

