## [Django] Form



### ▣ Form

* 입력공간

* 쟝고에서 form.py로 관리하게끔 지원

* 지금처럼 form태그로 하지 왜 굳이?

  * 지난 시간, blog객체에 image 필드 추가하고서, views.py 등등 수정함
  * form.py로 관리하면 db가 변해도 하나하나 수정 안해도 됨

  

### ▣ 실습하기

1. blog 테이블에 맞는 forms.py를 블로그 앱에 생성

   ```python
   from django import forms
   from .models import Blog
   
   # 쟝고에서 지원하는 forms를 상속받음
   class BlogForm(forms.ModelForm):
   
   # 이 정보를 가지고 Blog Form을 만들겠다
   class Meta:
        model = Blog

        # models.py에 있는 필드들 의미
        # pub_date는 글 작성시간을 자동으로 넣어야 하니까 form 가져오지 마
        fields = ['title','writer','body','image']
   
   
   ```

2. views.py 코드 추가

   - 위의 form 을 임포트

     - from .forms import BlogForm
   
   - 입력받는 공간을 new.html에 보내줌
   
     ```python
     # 입력을 위해 form을 new.html로 보내줌
     def new(request):
         form = BlogForm()
         return render(request, "new.html", {'form':form})
     ```
   
3. new.html 수정

   * 기존의 입력 태그 삭제 후, fom변수 사용

     ```html
     <h1>Write Your Blog</h1>
     
     <!--파일도 같이 넘겨야 해서 enctype 속성 추가-->
     <form action="{% url 'create' %}" method="post" enctype="multipart/form-data">
     
         <!--Csrf 공격을 막기 위해 반드시 처음에 사용-->
         {%csrf_token%}
     
         <!--form을 받음
     form의 각 요소를 p태그로 감싸 정리-->
         {{form.as_p}}
     
         <button type="submit">submit</button>
     </form>
     ```

     * p태그 대신 table로도 설정 가능

       ```html
       <table>
           {{form.as_table}}
       </table>
       ```

4. views.py 수정

   - create 함수에서 기존에 값 받아오던 방식 수정

   - form을 이용해 유효성 검사 후 받아오는 것으로 수정할 것

     ```python
     # new.html에서 정보를 받아야 함 -> request.POST 사용
     def create(request):
     
         form = BlogForm(request.POST, request.FILES)
     
         # form이 유효하면 임시저장
         # model의 필드를 다 담지 않기 때문(pub_date 없어)
         if form.is_valid():
             new_blog = form.save(commit=False)
             new_blog.pub_date = timezone.now()
             new_blog.save()
     
             # 이때는 render 안 써 
             # 새로운 페이지로 넘어가는 게 아니라, 기능 수행 후 이전 페이지로 돌아가야 하니까
             # 새로운 객체의 id를 보내서 path
             # 얘는 form이 유효하지 않으면 new_blog.id로 갈 수 없으니까 if문 안에 있어
             return redirect('detail', new_blog.id)
     
         # form이 유효하지 않으면
         else:
             return redirect('home')
     ```

     

   
