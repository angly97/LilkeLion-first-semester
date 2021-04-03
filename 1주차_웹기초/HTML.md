# HTML

> 인터넷이라는 선로에서 브라우저 기차를 태우고 HTML 문서 전송



### ▣ HTML 파일 만드는 제일 간단한 방법

1. 메모장을 킴
2. 인코딩을 utf-8 로 설정
3. 확장자를 .html 로 설정
4. 저장



### ▣ HTML 구성

1. 글  =>  **글**

2. 글을 감싸는 틀 (제목, 문단)  =>  **태그**    


3. 틀에 붙는 부가설명(사진, 링크)  =>  **속성**



### ▣ HTML 단축키

* Ctrl + n

  * new file 생성

* alt + l + o 

  * 라이브 서버 실행

* ! + Tab

  * 기본 셋팅

* ol>li*4

  * 순서있는 리스트 4개 생성

    

### ▣ HTML 코드의 분류

1. 이거 HTML문서라고 알려주는 태그


   ```
   <!DOCTYPE html>
   <html lang = 'ko'>
       
   </html>
   ```

2. 화면에는 안 보이지만 문서를 설명해주는 태그 (Title, 인코딩 방식 )

   ```html
   <head> 
       <!--인코딩 방식과 문서 제목 지정-->
       <meta charset = 'utf-8'> 
       <title>문서의 Title</title>
   </head>
   ```

3. 화면에 보이는 태그 (h1, h2, p...)>

   ```html
   <body>
   
   </body>
   ```

   * 제목 태그

     ```html
     <h1>큰 제목</h1>
     <h2>작은 제목</h2>
     ```

   * 문단 태그

     ```html
     <p>
     	문단 태그
     </p>
     ```

   * 개행 태그

     ```html
     줄 바꿈 태그<br> 
     ```

   * 사용자 입력 받아 전송하는 태그

     ```html
     <!-- action = "전송받을 대상"
     	 name = 입력값의 변수명과 유사  -->
     <form action = "receiver.php">
         ID: <input type = "text", name = "id">
         PW: <input type = "password", name = "pw">
         <input type = "submit">
         <br>        
     </form>
     ```

   * 이미지 태그

     ```html
     <!-- img는 현재 HTML 문서와 같은 위치에 있어야 함 -->
     <img src = "snowman.jpg", height = 300, width = 300>
     ```

   * 콤보 박스 태그

     ```html
     <select>
     	<!-- value = 변수명과 유사 -->
     	<option value = "goodday">좋은 날</option>
     	<option value = "goodday">슬픈 날</option>
     </select>
     ```

   * 넓은 입력 공간 태그

     ```html
     <textarea rows = 20, cols=30>
         
     </textarea>
     ```

   * 링크 태그

     ```html
     <h2>나의 일대기</h2>
     <ol>
         <li><a href = "1.html">유년기</a></li>
     	<li><a href = "2.html">사춘기</a></li>
     </ol>
     ```

     

     