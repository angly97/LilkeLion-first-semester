# [HTML] 폼 태그

 

### ▣ Form

*  다양한 입력 태그들을 감싸줌

* 속성

  * action

    * 데이터를 보낼 URL 지정

  * method

    * 보내는 방식 지정

    * method = "get" 

      > 데이터 조회에만 사용
      >
      > https://myblog.com/db.jsp?**query=청소하는 법**
      >
      > 메세지 헤더에서 목적지 URL뒤에 입력한 데이터를 붙여서 전송  
      >
      > = 메세지 헤더에서 주소와 데이터를 함께 서버로 보냄
      >
      > ex. 네이버 검색 후 주소	→	https://search.naver.com/search.naver?where=nexearch&sm=top_hty&fbm=1&ie=utf8&query=청소하는+법

    * method = "post" 

      > 서버에 있는 데이터를 작성, 수정할 때 사용
      >
      > 메세지 헤더에는 주소만, 
      >
      > 메세지 바디에는 입력한 데이터를 숨겨서 전송 

    ```html
    <body>
        <h2>회원가입</h2>
        <form action = "my_app" method = "post">
            ...
        </form>
    </body>
    ```


  

### ▣ Input

* 사용자의 입력을 받는 빈 태그

* 속성

  * type

  * name

  * placeholder

    * input에 아무 값도 입력되지 않았을 때 나타나는 텍스트

  * value

    * 초기값 지정 가능

    ```html
    <body>
        <h2>회원가입</h2>
        <form action = "my_app" method = "post">
           
            <input type = "text" name = "id" placeholder = "아이디를 입력하세요." value = "abc0123">	
            <input type = "password" name = "pw" placeholder = "비밀번호를 입력하세요">
            
        </form>
    </body>
    ```



### ▣ Label

* 해당 라벨을 클릭 시, input 태그가 활성화 됨

* input 태그 바로 위에 위치

* 속성

  * for
    * 속성 값 = input태그의 id 속성 값

  ```html
  <!-- "아이디: "를 클릭하면 입력칸이 활성화 됨 -->
  <label for = "id">아이디: </label>
  <input type = "text" name = "id" placeholder = "아이디를 입력하세요.">	
  ```

* cf. div 태그

  * CSS

  * 태그들을 구분 짓고 나누기 위해 사용되는 태그

  * 한 칸을 차지하게 됨

    ```html
    <div>
        <label for = "id">아이디: </label>
        <input type = "text" name = "id" placeholder = "아이디를 입력하세요.">
    </div>
    <div>
        <label for = "pw">비밀번호: </label>
        <input type = "password" name = "pw" placeholder = "비밀번호를 입력하세요">
    </div>
    ```

  

### ▣ Select

* 콤보박스 생성

* 속성

  * name	→	필수적

* option 태그

  * 목록 아이템 생성
  * 속성
    * value	→	name 속성과 유사한 역할 (필수적)

  ```html
  <!-- https://~~?gender=female -->
  <select name = "gender">
      <option value = "female">여성</option>
  </select>
  ```

  

### ▣ Textarea

* 여러 글을 입력 받기 가능

  ```html
  <div>
      <label for = "introduce">자기소개: </label>
      
      <!-- cols는 가로 글자 수만큼, rows는 줄 수만큼 -->
      <textarea name = "introduce" cols = "30" rows="30" placeholder = "자기소개를 입력하세요.">
      	여기에 내용을 적으면 value없이도 초기값이 들어가게 됨
      </textarea>
      
  </div>
  ```



### ▣ Botton

* 버튼은 input type = "button" 으로도 생성 가능

* html 요소를 버튼 태그 내에 담을 수 있음

  * 이미지 버튼 제작 가능

    ```html
    <button type = "submit">
    	<img src = "dog.jpg">
    </button>
    
    <button type = "reset">
        리셋
    </button>
    ```

  

