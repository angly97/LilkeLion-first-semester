# [HTML] 링크 태그



### ▣ 링크 태그

* <a>

  * URL

    *  인터넷에서 HTML페이지, CSS문서, 이미지 등 자원의 위치를 나타냄

    * 주소 + 경로 

      > 주소 = www.주소.com
      >
      >  경로 = 경기도 수원시 XX아파트/A의 방/A

    * 절대 URL / 상대 URL

  * 속성

    * 필수적
    * 태그의 추가 정보 제공
    * 속성을 여러개 넣으려면 띄어쓰기로 구분
      ex. <a 속성1 ="값1" 속성2="값2">글</a>

  * 속성 종류

    * href 

      ```html
      <!-- href = hypertext reference; 하이퍼텍스트 참조 -->
      <a href = "https://wwww.google.com">구글</a>
      ```

    *  target

      > target = "self"	: 현재 탭에서 링크 여는 속성
      > target = "blank"	:	새 탭에서 링크 여는 속성

      ```html
      <!-- 링크를 클릭했을 때 해당 페이지를 어디에 열지 결정 -->
      <a href = "..." target = "_self">구글</a>
      ```