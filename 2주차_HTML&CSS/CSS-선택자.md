# [CSS] 선택자



### ▣ 선택자 (Selector)

* 스타일 적용하려는 HTML 요소를 선택
  * 동시에 여러개 지정 가능

    ```html
    h1, p{
    	color: red;
    }
    ```

* 단순 선택자

  * 타입 선택자

    * 해당 태그의 모든 요소에 스타일 적용

    * **태그{ 속성: 값}**

      ```html
      p{ color:red; }
      ```

  * 아이디 선택자

    * id로 스타일을 적용

    * id는 단 하나

    * **#아이디{ 속성: 값 }**

      ```html
      <head>
          <style>
              #diary{ background-color: yellow; }
          </style>
      </head>
      
      <p id = diary>
      	...내 일기...
      </p>
      ```

  * 클래스 선택자

    * 비슷한 특징을 갖는 요소를 지정하여 묶을 수 있음

    * 클래스 이름으로 스타일을 적용

    * 같은 클래스 이름이면 모두 적용 = 클래스 이름 중복 가능

    * **.클래스이름 {속성 : 값 }**

      ```html
      <head>
          <style>
              .contents{ font-size:24px }
          </style>
      </head>
      
      <p class = "contents">
          이것은 두번째 단락입니다.
      </p>
      <p class = "contents">
          이것은 세번째 단락입니다.
      </p>
      ```

  * 전체 선택자

    * 모든 요소에 스타일을 적용

    * 모드 요소에 적용해서 속도 저하될 가능성

      ```html
      *{ color:red; }
      ```

  * 속성 선택자

    * 특정 속성을 가지는 모든 요소에 스타일 적용

    * **선택자[속성="값"] { }**

      ```html
      a[target = "_blank"]{color:red;}
      ```

* 복합 선택자

  * 부모 - 나 - 자식(후손)

    * ```html
      <!-- section: 부모
      	 article: 나
      	 div, p: 자식(후손)
      	 div 안 p: 후손 	-->
      <section>
          <article>
              <div>
              	<p>...</p>
              </div>
              <p></p>
          </article>
      </section>
      ```

  * 자식 선택자

    * 선택자 A의 모든 자식 중 선택자 B와 일치하는 요소 선택

    * 선택자A>선택자B {color: red;}

      ![image-20210407215810849](/img/SonSelector.png)

      ```html
      <!-- article 태그의 모든 자식 중 p태그와 일치하는 자식 -->
      <head>
          <style>
          	article>p {color:red;}
          </style>
      </head>
      ```

  * 후손 선택자

    * 선택자 A의 모든 후손 중 선택자 B와 일치하는 요소 선택

    * 선택자A 선택자B { color: red; }
      ![image-20210407215616041](/img/DesSelector.png)

      ```html
      <!-- article 태그의 모든 후손 중 p태그와 일치하는 자식 -->
      <head>
          <style>
          	article p {color:red;}
          </style>
      </head>
      ```

* Pseudo 클래스 선택자

  * 요소의 특별한 상태를 지정할 때 씀

  * 상태

    * :link	→	방문하지 않은 링크의 경우

    * :visited	→	방문한 링크의 경우

    * :hover	→	마우스를 올렸을 때 링크의 경우

      ```html
      <head>
          <style>
              a:link {color:yellow}
              a:visited {color:green}
              a:hover {background-color: blue}
          </style>
      </head>
      ```
