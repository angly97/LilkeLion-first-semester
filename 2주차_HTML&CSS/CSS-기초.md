# [CSS] 기초



### ▣ 기초 문법

* 선택자 (Selector)

  * 스타일 적용하려는 HTML 요소를 선택

* 속성

  * 지정할 스타일의 속성명
  * 단위 = 속성; 값;

* 값

  * 속성과 쌍을 이룸

  ```html
  <!-- P: 문단 = 선택자
  	 이 문단의 폰트는 맑은 고딕
  	 사이즈는 18
  	 색은 파란색					-->
  p{	
  	font-family:'맑은 고딕';
  	font-size: 18px;
  	color: blue;
  }
  ```

  

### ▣ CSS를 HTML에 적용

* 방법

  1. Link style

     * html 외부에 있는 css 파일 불러옴

     * head 태그 내에 link 태그 추가

     * rel 속성: 현재 문서와 연결될 문서 간 관계

       ```html
       <head>
           <title>내 소개 페이지</title>
           <link rel = "stylesheet" href="csstest.css">
       </head>
       ```

  2. Embedding style

     * head 태그에 style태그 css 코드추가

       ```html
       <head>
           <title>내 소개 페이지</title>
           <style>
               h1 {color:red;}
           </style>
       </head>
       ```

  3. Inline style

     * html요소에 직접! style 속성을 이용해 css 작성

       ```html
       <body>
           <h1 style="color:red;">
               빨간 제목
           </h1>
           <h1>그냥 제목</h1>
       </body>
       ```

       