# Bootstrap

>CSS/JavaScript 기반 웹 프레임워크
>
>반응형 웹 지원 (자동으로 화면크기 조정)
>
>브라우저 호환성
>
>성능 다소 좋지 않음



### ▣ Bootstrap 시작하기

* 부트스트랩 CDN

  * 부트스트랩 CDN 코드를 head 태그 안에 삽입

    ```html
    <head>
        
    	<!-- 합쳐지고 최소화된 최신 CSS -->
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css">
    
        <!-- 부가적인 테마 -->
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap-theme.min.css">
    
        <!-- 합쳐지고 최소화된 최신 자바스크립트 -->
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/js/bootstrap.min.js"></script>
        
        
    </head> 
    ```

* JQuary CDN

  * JQuary CDN 코드를 head 태그 안에 삽입

    ```html
    <head>
        <script
          src="https://code.jquery.com/jquery-3.6.0.js"
          integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk="
          crossorigin="anonymous">
    	</script>
    </head>
    ```



### ▣ CSS 코드

> [CSS · 부트스트랩 (bootstrapk.com)](http://bootstrapk.com/css/#buttons) → 참고



* 컨테이너

  * 컨테이너로 내용을 감싸 여백 생성

  * body 태그 안에 작성

    ```html
    <body>
        <div class = container>
            
            <h1>민초현을 소개합니다</h1>
            <h2>민초현을 소개해요</h2>
            
        </div>
    </body>
    ```

* 버튼

  ```html
  <button type="button" class="btn btn-primary">Primary</button>
  ```

  * 제출 버튼 색 변경

    ```html
    <input type="submit" class="btn btn-primary">
    ```

* 탭
  
  * in 컴포넌트
* 그래프
  * in 컴포넌트
  * 진행바

