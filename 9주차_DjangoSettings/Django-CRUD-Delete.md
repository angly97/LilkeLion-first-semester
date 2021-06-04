## [Django] CRUD-Delete

>구현할 기능
>
>* 따로 html 만들 필요 없음
>* 수정하기 링크처럼, 삭제하기 링크 만들기
> * views.py의 delete함수에서 해당 오브젝트 삭제

### ▣ Delete

1. delete 구현

   1. views.py

      ```python
      def delete(request, id):
          delete_blog = Blog.objects.get(id=id)
      
          delete_blog.delete()
          return redirect('home')
      ```

   2. url.py

      - views.py에서 매개변수(id)를 받으면, 무조건 Path-converter 해줘야 함

      - 두번째 인자는 views.py의 delete 함수

        ```python
         path('delete/<str:id>', delete, name="delete"),
        ```

   3. detail.html에서 삭제하기 버튼 생성

      ```html
      <!--url.py에서 delete로 설정한 url로 이동-->
      <a href="{% url 'delete' blog.id %}">삭제하기</a>
      ```

      
