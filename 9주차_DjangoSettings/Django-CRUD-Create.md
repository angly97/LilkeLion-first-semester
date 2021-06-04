## [Django] CRUD-Create

>구현할 기능
>
>* new: new.html 보여줌
>
>* create: new.html에서 받은 정보 데이터베이스에 저장
>
>cf. 컨트롤 + 알트 + 위아래 방향키 = 알트 + 드래그 효과(커서 늘어남)

### ▣ Create

1. new 만들기

   1. views.py에서 new 함수

      ```python
      def home(request):
      
          # Blog 객체들 전부 가져옴 
          blogs = Blog.objects.all()
          return render(request, "home.html", {'blogs': blogs})
      
      def detail(request, id):
      
          # Blog 객체 불러오기 가능
          blog= get_object_or_404(Blog, pk=id)
          return render(request, "detail.html", {'blog': blog})
      
      # 추가
      def new(request):
          return render(request, "new.html")
      ```

   2. url.py

      ```python
      
      urlpatterns = [
          path('admin/', admin.site.urls),
          path('',home,name="home"),
          path('<str:id>', detail, name="detail"),
      
          # 추가
          path('new/', new, name="new"),
      
      ]
      ```

   3. home.html에 new로 갈 수 있는 a태그

      ```html
      <body>
          <div class="containger">
              <h1>Blog Project</h1>
      
              # 추가
              <div>
                  <a href="{% url 'new' %}"> write blog </a>
              </div>
      
              {%for blog in blogs%}
      ```

   4. new.html

      * form은 post 방식

        * GET 

          > 데이터 얻는 요청
          >
          > 데이터가 url에 보임

        * POST

          > 데이터 생성하는 요청
          >
          > 데이터가 url에 안보임
          >
          > Csrf 공격 방지

        ```html
        <h1>Write Your Blog</h1>
        
        <form action="{% url 'create' %}" method="post">
        
            <!--Csrf 공격을 막기 위해 반드시 처음에 사용-->
            {%csrf_token%}
        
            <p>제목: <input type="text" name="title"></p>
            <p>작성자: <input type="text" name="writer"></p>
            본문: <textarea name="body" id="" cols="30" rows="10"></textarea>
        
            <button type="submit">submit</button>
        </form>
        ```

2. create 만들기

   1. views.py

      ```python
      # 이전 페이지로 돌아가기 위해 redirect 추가
      from django.shortcuts import render, get_object_or_404, redirect
      
      # 현재시각 사용하기 위해 import
      from django.utils import timezone
      
      ...
      
      # new.html에서 정보를 받아야 함 -> request.POST 사용
      def create(request):
      
          new_blog = Blog()
          new_blog.title = request.POST['title']
          new_blog.writer = request.POST['writer']
          new_blog.body = request.POST['body']
          new_blog.pub_date = timezone.now()
      
          new_blog.save()
      
          # 이때는 render 안 써 
          # 새로운 페이지로 넘어가는 게 아니라, 기능 수행 후 이전 페이지로 돌아가야 하니까
          # 새로운 객체의 id를 보내서 path
          return redirect('detail', new_blog.id)
      
      ```

   2. url.py

      ```python
          path('create/', create, name="create"),
      
      ```
      
      

