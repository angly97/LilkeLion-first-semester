## [Django] CRUD-Update

>구현할 기능
>
>* edit: edit.html 보여줌
>* update: edit.html에서 받은 정보 데이터베이스에 저장
>  * 수정할 데이터의 id값을 받아야 함
>

### ▣ Update

1. edit.html 생성

   1. views.py

      ```python
      # id값을 매개변수로 받아옴
      def edit(request, id):
          edit_blog = Blog.objects.get(id= id)
          return render(request, "edit.html", {'blog': edit_blog})
      
      ```

   2. url.py

      ```python
      path('edit/<str:id>', edit, name="edit")
      ```

   3. 위 요청을 받을 a태그는 detail.py에서 만듦

      ```html
      <body>
          <h1>{{blog.title}}</h1>
          작성자: {{blog.writer}}
          날짜: {{blog.pub_date}}
          {{blog.blog}}
      
          <!--edit.html로 이동-->
          <a href="{% url 'edit' blog.id %}">수정하기</a>
      </body>
      ```

   4. edit.html

      ```html
      <h1>Update Your Blog</h1>
      
      <form action="{% url 'update' blog.id %}" method="post">
      
          <!--Csrf 공격을 막기 위해 반드시 처음에 사용-->
          {%csrf_token%}
      
          <!--기존 오브젝트의 데이터가 미리 입력된 상태-->
          <p>제목: <input type="text" name="title" value="{{blog.title}}"></p>
          <p>작성자: <input type="text" name="writer" value="{{blog.writer}}"></p>
          본문: <textarea name="body" id="" cols="30" rows="10">
              {{blog.body}}
          </textarea>
      
          <button type="submit">submit</button>
      </form>
      ```

2. update 생성

   1. views.py

      ```python
      # create는 새로 만드는 거지만, update는 기존 것을 수정하니까 기존 것의 id 받아야 해
      def update(request, id):
          update_blog = Blog.objects.get(id=id)
      
          update_blog.title = request.POST['title']
          update_blog.writer = request.POST['writer']
          update_blog.body = request.POST['body']
          update_blog.pub_date = timezone.now()
      
          update_blog.save()
          return redirect('detail', update_blog.id)
      
      ```

   2. url.py

      ```python
      path('update/<str:id>', update, name="update")
      ```

      
