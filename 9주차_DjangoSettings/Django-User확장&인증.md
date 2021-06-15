## [Django] User 확장과 인증



### ▣ User 테이블

* 인스타그램에 들어가면 사용자마다 보여지는 페이지가 달라
* 각 사용자의 정보를 가지는 User테이블이 필요
* 이 User테이블을 쟝고에서 지원
* 서비스마다 저장한 User정보가 다름
  * 쇼핑몰이면, 주소
  * 에브리타임이면, 학교 소속 등
* 그래서!  기존에 있는 User를 대체할 새로운 테이블 생성
  * 컬럼을 확장시킴



### ▣ auth (Authentication: 인증) 모듈

* 지원 함수
  * authenticate
    * 로그인 요청 시,  입력된 유저 정보가 User테이블 정보와 일치한지 확인
  * login
    * User테이블에서 온 User객체를 통해 클라이언트를 인증된 상태로 만들어주는 함수
  * logout
    * 인증된 유저가 인증을 풀어달라고 요청



### ▣ 실습하기

1. account 앱 생성

   - user 계정을 위한
   - 쟝고에서 제공하는 user를 사용 →  models.py는 사용 X

   1. views.py

      * 함수이름 = login_view

        > 왜 그냥 login이라고 안해?
        >
        > → auth에서 가져오는 login 모듈과 충돌나지 않기 위해

      * login을 부르면 login_view 함수 실행됨

      * login.html에 POST로 요청보내면  login_view의 if문에서 처리됨

      * clean_data는 유효성 통과된 데이터를 의미

      ```python
      from django.shortcuts import redirect, render
      
      #AuthenticationFrom = 로그인 폼, UserCreationForm = 회원가입 폼
      from django.contrib.auth.forms import AuthenticationForm, UserCreationForm
      
      # 유저 인증을 위해
      from django.contrib.auth import authenticate , login, logout
      
      # 로그인 창 띄우는 함수
      def login_view(request):
      
          
          if request.method == 'POST':
              form= AuthenticationForm(request=request, data=request.POST)
              if form.is_valid():
                  username = form.cleaned_data.get("username")
                  password = form.cleaned_data.get("password")
      
                  # user = 인증을 받는 객체
                  user = authenticate(request=request, username=username, password=password)
                  if user is not None:    # user가 존재하면
                      login(request,user)
                  
              return redirect("home")
          else:
              # login.html을 랜더링 = GET 방식
              form = AuthenticationForm()
              return render(request, 'login.html', {'form':form})
      
      
      def logout_view(request):
          logout(request)
          return redirect("home")
      ```

   2. app에다가 urls.py 생성

      * blog 앱 아래의 urls.py에서 import 복붙

      * 근데 생각해보니까 blog 앱 밑의 urls.py에는 admin import 할 필요없음!(맨 윗 줄 삭제)

        ```python
        from django.urls import path
        from .views import *
        
        urlpatterns = [
            path('login/', login_view, name='login'),
        ]
        ```

   3. 프로젝트 폴더 아래의 urls.py

      ```python
      urlpatterns = [
          path('admin/', admin.site.urls),
          path('',home,name="home"),
      
          # blogs 아래 urls의 path를 포함
          # 근데 이제 모든 url 앞에 'blog/'가 붙음
          path('blog/', include('blog.urls')),
          
          # 추가!
          path('account/',include('account.urls')),
      
      ]+static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) 
        # 바로 위에 코드 외우지 마; 그냥 이걸로 미디어를 url로 설정할 수 있는 걸 알라
      
      ```

   4. templates 폴더 생성 후, login.html 생성

      * new.html 복붙 후 수정

      ```html
      
       {% extends 'base.html' %}
      
       <!--base.html의 block content에 해당-->
       {% block content %}
      
          <h1>Login</h1>
      
          <!--파일도 같이 넘겨야 해서 enctype 속성 추가-->
          <form action="{% url 'login' %}" method="post">
      
              <!--Csrf 공격을 막기 위해 반드시 처음에 사용-->
              {%csrf_token%}
      
              <!--form을 받음
                  form의 각 요소를 p태그로 감싸 정리-->
              {{form.as_p}}
      
              <button type="submit">submit</button>
          </form>
      
      {% endblock%}
      ```

   5. base.html 수정

      - 네비바에 Login 추가

        ```html
        <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="{% url 'new' %}">Write</a>
        </li>
        
        <!-- 수정하여 Login, Logout 탭 추가 -->
        <li class="nav-item">
            <a class="nav-link" href="{% url 'login' %}">Login</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="{% url 'logout' %}">Logout</a>
        </li>
        ```

2. login 후 

   - home.html에 수정

     ```html
     
     {% extends 'base.html' %}
     
     <!--base.html의 block content에 해당-->
     {% block content %}
     
         <!-- 추가: user가 인증된 유저라면, -->
         {% if user.is_authenticated %}
             {{user.username}}
         {% endif %}
         
         <h1>Blog Project</h1>
     
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

3. 회원가입

   1. views.py

      * form.save(commit)말고 form.save()함

        > form 에 적는 정보 외에 필요한 정보가 없기 때문에 그냥 save

      ```python
      from django.shortcuts import redirect, render
      
      #AuthenticationFrom = 로그인 폼, UserCreationForm = 회원가입 폼
      from django.contrib.auth.forms import AuthenticationForm, UserCreationForm
      
      # 유저 인증을 위해
      from django.contrib.auth import authenticate , login, logout
      
      # 로그인 창 띄우는 함수
      def login_view(request):
      ...
      
      
      def logout_view(request):
      ...
      
      # 추가
      def register_view(request):
          if request.method=='POST': 
              form = UserCreationForm(request.POST)
              if form.is_valid():
      
                  #commit 인자로 안넣어도 됨
                  user = form.save()
      
                  login(request, user)
              return redirect("home")
          else:
              form = UserCreationForm()
              return render(request,'signup.html', {'form': form})
      ```

   2. urls.py

      ```python
      from django.urls import path
      from .views import *
      
      urlpatterns = [
          path('login/', login_view, name='login'),
          path('logout/',logout_view,name="logout"),
          
          # 추가
          path('register/',register_view,name="signup"),
          
      ]
      ```

   3. signup.html

      * login.html 복붙 후 수정

      ```html
      
       {% extends 'base.html' %}
      
       <!--base.html의 block content에 해당-->
       {% block content %}
      
          <h1>Sign Up!</h1>
      
          <!--파일도 같이 넘겨야 해서 enctype 속성 추가-->
          <form action="{% url 'signup' %}" method="post">
      
              <!--Csrf 공격을 막기 위해 반드시 처음에 사용-->
              {%csrf_token%}
      
              <!--form을 받음
                  form의 각 요소를 p태그로 감싸 정리-->
              {{form.as_p}}
      
              <button type="submit">submit</button>
          </form>
      
      {% endblock%}
      ```

      * base.html의 네비바에 signup 추가

        ```html
        ...
        <li class="nav-item">
            <a class="nav-link" href="{% url 'signup' %}">SignUp</a>
        </li>
        ```

4. base.html 수정

   - 로그인되기 전에는 글쓰기 등 불가
   - 로그인 된 후에는 Login 표시 사라져야 함
   - 따라서 네비바 재구성

   ```html
   <!--로그인 후에만 보이게 함-->
   {% if user.is_authenticated %}
   <li class="nav-item">
       <a class="nav-link active" aria-current="page" href="{% url 'new' %}">Write</a>
   </li>
   <li class="nav-item">
       <a class="nav-link" href="{% url 'logout' %}">Logout</a>
   </li>
   {% endif %}
   
   <!--로그인 전에만 보이게 함-->
   {% if not user.is_authenticated %}
   <li class="nav-item">
       <a class="nav-link" href="{% url 'login' %}">Login</a>
   </li>
   <li class="nav-item">
       <a class="nav-link" href="{% url 'signup' %}">SignUp</a>
   </li>
   {% endif %}
   ```

5. User 확장

   - account 앱의 models.py

     - 기존의 UserCreationForm은 Username과 Password만 받았음

     ```python
     from django.db import models
     
     from django.contrib.auth.models import AbstractUser
     
     class CustomUser(AbstractUser):
         nickname = models.CharField(max_length=100)
         university = models.CharField(max_length=50)
         location = models.CharField(max_length=200) 
     ```

   - settings.py

     - 인증받을 유저 모델을 위의 모델로 사용하겠다고 설정해줘야 함

     ```python
     # 추가
     AUTH_USER_MODEL = 'account.CustomUser'
     
     ```

   - admin들 다 주석 처리

     - migrate하면 어드민이 문제가 생김

     - 아래 처럼 migrate하고 나서 주석 해제

       ```python
       # settings.py
       
       INSTALLED_APPS = [
           #'django.contrib.admin',
           
           'django.contrib.auth',
           'django.contrib.contenttypes',
           'django.contrib.sessions',
           'django.contrib.messages',
           'django.contrib.staticfiles',
           'blog.apps.BlogConfig',
           'account.apps.AccountConfig',
       ]
       ```

       ```python
       # urls.py
       
       # from django.contrib import admin
       from django.urls import path, include
       from blog.views import home
       from django.conf import settings
       from django.conf.urls.static import static
       
       urlpatterns = [
           # path('admin/', admin.site.urls),
           path('',home,name="home"),
       ...
       ```

   - migration 하기

     - python manage.py makemigrations 앱 이름
     - python manage.py migrate

   - form을 models.py에 맞게 변경

     - 기존 form은 username과 password만 입력받으니까

     1. account 앱 아래에 forms.py 생성

        ```python
        
        from django.contrib.auth.forms import UserCreationForm
        from .models import CustomUser
        
        # 기존 UserCreationForm을 상속받고 확장 시작
        class RegisterForm(UserCreationForm):
            class Meta:
                model = CustomUser
                fields = ['username','password1','password2','nickname','university','location']
        
        ```

     2. views.py에서 UserCreationForm → RegisterForm으로 수정

        ```python
        from django.shortcuts import redirect, render
        
        #AuthenticationFrom = 로그인 폼, UserCreationForm = 회원가입 폼
        from django.contrib.auth.forms import AuthenticationForm #, UserCreationForm -> UserCreationForm은 삭제
        
        from django.contrib.auth import authenticate , login, logout
        
        # 추가
        from .forms import RegisterForm
        ...
        
        def register_view(request):
            if request.method=='POST': 
                
                # 추가: UserCreationForm → RegisterForm으로 수정
                form = RegisterForm(request.POST)
                if form.is_valid():
                    user = form.save()
                    login(request, user)
                return redirect("home")
            else:
                # 추가: UserCreationForm → RegisterForm으로 수정
                form = RegisterForm()
                return render(request,'signup.html', {'form': form})
        
        ```

     3. account앱 아래의 admin.py 수정

        * 확장된 user를 등록
