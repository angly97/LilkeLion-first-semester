## [Django] Django실습[1]



### ▣ MTV

- Model-Template-View
- Front End
  - Template
    - 사용자가 보이는 영역
    - HTML/CSS, 템플릿 언어...
- Back End
  - Model
    - 데이터베이스
  - View
    - 데이터 처리하는 곳



### ▣ Django 실습 시작하기

> cf. App
>
> - 서비스의 소기능( ex. 메일App, 쇼핑 App, ...)



* 입력칸에 이름을 적고 제출누르면 인사말 출력하는 페이지 만들기

  * 요약

    1. App 생성

    2. Template 제작

    3. View 제작

    4. URL 연결

       

1. VS Code에서 가상환경과 프로젝트 만들고, 프로젝트로 이동

   - cd firstproject

2. app 생성

   * App은 manage.py를 이용해 만듦
     * python manage.py startapp 만들려는앱이름

   - project폴더 안의 project랑 같은 이름 폴더 안, settings.py에 들어감

     - 프로젝트가 방금 만든 앱이 자신의 앱인지 인식 못하기 때문에 , 이를 인식시키기 위하여

   - settings.py의 INSTALLED_APP에 코드 추가

     ```python
     INSTALLED_APPS = [
         'django.contrib.admin',
         'django.contrib.auth',
         'django.contrib.contenttypes',
         'django.contrib.sessions',
         'django.contrib.messages',
         'django.contrib.staticfiles',
         
         #앱이름.apps.앱이름(대문자 시작)Config, (콤마 중요) 
         'firstapp.apps.FirstappConfig',
     ]
     
     ```

3. template 만들기 (html 문서 만들기)

  1. welcome 페이지 설정

    * firstapp폴더에서 우클릭 -> template폴더 생성 -> html 파일 생성	

      ```html
      <!-- welcome.html -->
      <div style="text-align: center;">
      
          <h1>사용자의 이름을 입력하세요</h1>
          <br>
          <form action="">
              <label for="nameInput">이름: </label>
              <input id="nameInput" name="name">
              <input type="submit" value="제출">
          </form>
      </div>
      ```

    * views.py에 들어가 View 생성

      ```python
      #views.py
      
      from django.shortcuts import render
      
      # welcome함수를 호출하면 welcome.html 을 띄움
      def welcome(request):
          return render(request, "welcome.html")
      ```

    * url과 view함수 연결하기

      * 우리는 네이버띄우고 싶으면 네이버 url을 치지 welcome함수 호출 안해

      * 프로젝트 설정 폴더에서 작업

        1. firstproject 프로젝트 폴더 내의 firstproject 폴더 들어감

        2. url.py 에 들어감

           ```python
           # url과 view연결하기 위한 import
           from firstapp import views
           
           urlpatterns = [
               path('admin/', admin.site.urls),
           
               # url 주소가 비어있음 = 서버 구동시키고 첫페이지가 welcome이라는 뜻
               # name을 쓰는 이유: welcome을 다음부터는 url로 부른다는 건데, 다른 html에서 매번 url로 부르기 힘드니까 name으로 부르게 함
               path('', views.welcome, name="welcome")
           ]
           ```

        3. 서버 구동시키기

           * python manage.py runserver
             

  2. hello 페이지 설정

     * templates에 hello.html 추가 생성

       > view.py에서 가져온 userName을 사용 
       > ps. 중괄호 2개 겹쳐!

       ```html
       <!-- hello.html -->
       
       <div style="text-align: center;">
           <h1>반갑습니다! {{userName}}님</h1>
       </div>
       ```

     * view.py에 들어가 View 설정

       > 변수 값을 딕셔너리 형태로 넘겨줌

       ```python
       from django.shortcuts import render
       
       def welcome(request):
           return render(request, "welcome.html")
       
       #welcome.html의 input에서 이름 가져옴
       def hello(request):
           userName= request.GET['name']
           return render(request, "hello.html", {'userName': userName})
       
       ```

     * url.py

       ```python
       urlpatterns = [
           path('admin/', admin.site.urls),
           path('',views.welcome,name='welcome'),
           
           #추가
           path('hello/', views.hello, name='hello'),
       
       ]
       ```

     * welcome.html에서 form action 설정

       ```html
           <!--url.py에서 /hello 대신 그냥 hello쓰기로 정했음 ; name= hello를 통해-->
           <form action="hello">
               <label for="nameInput">이름: </label>
               <input id="nameInput" name="name">
               <input type="submit" value="제출">
           </form>
       ```

       