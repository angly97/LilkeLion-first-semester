## [Django] Django실습[2]



### ▣ Django 실습

* 워드 카운터 만들기
  * 글을 입력하면 단어 횟수 출력
  * Template은 지난 실습에서 input을 textarea로 수정하기만!
  * View는 우선 문자열 단어 수 세는 코드 작성
  
* home.html

  ```html
  <!--글을 입력하고 입력된 글을 result로 전송-->
  <div style="text-align: center;">
  
      <h1>Wordcount 페이지입니다.</h1>
      <br>
      <h3>여기에 문장을 입력해주세요.</h3>
      <form action="result">
          <textarea name="sentence" cols="60" rows=30></textarea>
          <br>
          <br>
          <input type="submit" value="제출">
  
      </form>
  </div>
  ```

* views.py

  ```python
  
  def home(request):
      return render(request,"home.html")
  
  def result(request):
  
      text = request.GET['sentence']
      words=text.split()
      wordDict = {}
  
      for word in words:
          if word in wordDict:
              wordDict[word]+=1
          else:
              wordDict[word]=1
  
  
      # 전체 입력 글 + 결과 카운트 + 전체 글자 수를 전송
      # wordDict는 꼭 items() 붙여야 오류 안 남
      return render(request,"result.html",{'fullText': text, 'wordDict':wordDict.items(), 'count': len(words)})
  
  ```

* 템플릿 언어

  * html에서 파이썬 문법 사용하게 하는 언어

  * 변수명

    ```html
    {{변수명}}
    ```

  * for문/if문

    ```html
    <!-- 중괄호 안에 %로 감싼 후 코드-->
    {%for i in range(5)%}
    ...
    {%endfor%}
    
    
    {%if not isEmpty%}
    ...
    {%endif%}
    ```

  * result.html 을 템플릿 언어로 작성

    ```html
    <div style="text-align: center;">
        <h1>입력한 텍스트 전문</h1>
        <div>
            {{fullText}}
        </div>
    
        <h3>당신이 입력한 텍스트는 {{count}}개의 단어로 구성되어 있습니다.</h3>
        <div>
            
            <!--wordDict는 이미 중괄호 안에 있으니까 2중 괄호 안함 -->
            {% for word, wc in wordDict %}
                {{word}} : {{wc}}
                <br>
            {% endfor %}
            
            
        </div>
    
    </div>
    ```

* url.py

  * 만일 app을 여러개 import하면 -> views도 여러개

    ```python
    <!--views가 같은 이름이어서 오류나는 것 방지-->
    from firstapp import views as fa
    from secondapp import views as sc
    ```

  * url 추가

    ```python
    urlpatterns = [
        path('admin/', admin.site.urls),
        path('',fa.welcome,name='welcome'),
        path('hello/', fa.hello, name='hello'),
    	
        #추가
        path('wc/', fa.home, name='wc'),
        path('wc/result/',fa.result, name='result'),
    
    ]
    ```

* 페이지 이동 링크 생성

  ```html
  <!--워드 카운트 페이지 이동; href에는 페이지 name 적기-->
  <a href="wc">워드 카운트 페이지로 이동</a>
  ```

  
