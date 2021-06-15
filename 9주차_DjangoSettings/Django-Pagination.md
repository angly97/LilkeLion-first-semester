## [Django] Pagination

>이용자가 많아지고 글이 많아질 경우
>
>블로그 객체를 잘라서 보내주는 paginator 
>
>cf. 여러줄 주석: 드래그 후 Ctrl + /

### ▣ Paginator

* http://127.0.0.1:8000/<strong>?page=1</strong>

  * '<a href="?page=1">'

  

### ▣ 실습하기

* blog 앱 아래 views.py

  ```python
  # 추가
  from django.core.paginator import Paginator
  
  def home(request):
  
      # Blog 객체들 전부 가져옴 
      # -> 수정: (paginator) 객체 전부 가져오지 않고, 페이지 단위로 가져옴
      blogs = Blog.objects.all()
  
      paginator = Paginator(blogs, 3) # 3개씩 쪼개서 보낼 것
      page = request.GET.get('page')  # 몇번째 페이지인지 받아오기
      
      blogs = paginator.get_page(page)
  
      return render(request, "home.html", {'blogs': blogs})
  
  ```

* home.html 수정

  *  '<a href="?page=1">' 이렇게 띄어쓰기 없어야 함!!

  ```html
  	...
  
      <!--한 페이지 내에 모든 글 보일 수 없을 때만 paginator 보이도록-->
      <!--이전 글이 있으면-->
      {% if blogs.has_previous %}
      <a href="?page=1">처음</a>
      <a href="?page={{blogs.previous_page_number}}">이전</a>
      {% endif %}
  
      <!--현재 몇 번째 페이지를 보고 있는지-->
      <span>{{blogs.number}}</span>
      <span>of</span>
      <span>{{blogs.paginator.num_pages}}</span>
  
      <!--다음 글이 있으면-->
      {% if blogs.has_next %}
      <a href="?page={{blogs.next_page_number}}">다음</a>
      <a href="?page={{blogs.paginator.num_pages}}">마지막</a>
      {% endif %}
  
  {% endblock%}
  ```

* QuerySet Method

  * 최신 순으로 글 가져오기

  ```python
  
  def home(request):
  
      # Blog 객체들 전부 가져옴 
      # -> 수정: (paginator) 객체 전부 가져오지 않고, 페이지 단위로 가져옴
      #blogs = Blog.objects.all()
      blogs = Blog.objects.order_by('-pub_date')  #최신글 순서대로 보고싶다
  
      paginator = Paginator(blogs, 3) # 포스팅 글을 3개씩 쪼개서 보낼 것
      page = request.GET.get('page')  # 몇번째 페이지인지 받아오기
      
      blogs = paginator.get_page(page)
  
      return render(request, "home.html", {'blogs': blogs})
  
  ```

  * filter 기능

    * ex. 내가 쓴 글만 확인

      ```python
      def home(request):
      
          # Blog 객체들 전부 가져옴 
          # -> 수정: (paginator) 객체 전부 가져오지 않고, 페이지 단위로 가져옴
          #blogs = Blog.objects.all()
          blogs = Blog.objects.order_by('-pub_date')  #최신글 순서대로 보고싶다
      	# 추가: 내가 쓴 글만 확인
          search = request.GET.get('search')
          if search == 'true':
              author = request.GET.get('writer')
              blogs = Blog.objects.filter(writer=author)
              return render(request, "home.html", {'blogs': blogs})
      
          paginator = Paginator(blogs, 3) # 포스팅 글을 3개씩 쪼개서 보낼 것
          page = request.GET.get('page')  # 몇번째 페이지인지 받아오기
          
          blogs = paginator.get_page(page)
      
          return render(request, "home.html", {'blogs': blogs})
      
      ```

    * home.html 수정

      ```html
      <!--이 링크를 누르면 search가 true가 되어 views.py의 if문 실행-->
      <a href="?search=true&writer={{user.nickname}}">내가 쓴 글</a>
      <h1>Blog Project</h1>
      
      ```

  * exclude 기능

    *  filter와 반대 기능

      > views.py의 home 함수 수정

      ```python
      # 내가 쓴 글만 확인 x
      search = request.GET.get('search')
      if search == 'true':
          author = request.GET.get('writer')
          
          # filter를 exclude로 변경만 해줌
          blogs = Blog.objects.exclude(writer=author)
          return render(request, "home.html", {'blogs': blogs})
      
      ```

      